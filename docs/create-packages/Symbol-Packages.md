---
title: Come creare pacchetti di simboli NuGet
description: Come creare pacchetti NuGet contenenti solo i simboli per supportare il debug di altri pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e917895d0fa6ed6dc4bc24b72afc7fa0770f2dd0
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843368"
---
# <a name="creating-symbol-packages"></a>Creazione di pacchetti di simboli

Oltre alla compilazione di pacchetti per nuget.org o altre origini, NuGet supporta anche la creazione dei pacchetti di simboli associati e la relativa pubblicazione nel repository SymbolSource.

I consumer di pacchetti possono quindi aggiungere `https://nuget.smbsrc.net` alle loro origini dei simboli in Visual Studio, in modo da consentire l'esecuzione delle istruzioni nel codice del pacchetto nel debugger di Visual Studio. Vedere [Specifica di file di simboli (con estensione pdb) e di file di origine nel debugger di Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) per informazioni dettagliate su questo processo.

## <a name="creating-a-symbol-package"></a>Creazione di un pacchetto di simboli

Per creare un pacchetto di simboli, seguire queste convenzioni:

- Assegnare al pacchetto principale (con il codice) il nome `{identifier}.nupkg` e includere tutti i file tranne i file `.pdb`.
- Assegnare al pacchetto di simboli il nome `{identifier}.symbols.nupkg` e includere la DLL dell'assembly, i file `.pdb`, i file XMLDOC e i file di origine (vedere le sezioni successive).

È possibile creare entrambi i pacchetti con l'opzione `-Symbols`, da un file `.nuspec` o da un file di progetto:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Si noti che `pack` richiede Mono 4.4.2 su Mac OS X e non funziona nei sistemi Linux. In un Mac è anche necessario convertire i nomi di percorso di Windows nel file `.nuspec` in percorsi di tipo Unix.

## <a name="symbol-package-structure"></a>Struttura di un pacchetto di simboli

Un pacchetto di simboli può avere come destinazione più framework di destinazione analogamente a un pacchetto di librerie, pertanto la struttura della cartella `lib` deve corrispondere esattamente a quella del pacchetto principale, includendo solo i file `.pdb` insieme alla DLL.

Ad esempio, un pacchetto di simboli che ha come destinazione .NET 4.0 e Silverlight 4 dovrebbe avere questo layout:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

I file di origine vengono quindi inseriti in una speciale cartella separata denominata `src`, che deve seguire la relativa struttura del repository di origine. Ciò è dovuto al fatto che i file PDB contengono i percorsi assoluti dei file di origine usati per compilare la DLL corrispondente e devono essere rilevati durante il processo di pubblicazione. Un percorso di base (prefisso di percorso comune) può essere rimosso. Si consideri ad esempio una libreria compilata da questi file:

    C:\Projects
        \MyProject
            \Common
                \MyClass.cs
            \Full
                \Properties
                    \AssemblyInfo.cs
                \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
            \Silverlight
                \Properties
                    \AssemblyInfo.cs
                \MySilverlightExtensions.cs
                \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)

A parte la cartella `lib`, un pacchetto di simboli dovrà contenere questo layout:

    \src
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs

## <a name="referring-to-files-in-the-nuspec"></a>Riferimento ai file nel file nuspec

Un pacchetto di simboli può essere generato in base alle convenzioni, da una struttura di cartelle come descritto nella sezione precedente oppure specificandone il contenuto nella sezione `files` del manifesto. Ad esempio, per compilare il pacchetto mostrato nella sezione precedente, usare il codice seguente nel file `.nuspec`:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a>Pubblicazione di un pacchetto di simboli

> [!Important]
> Per eseguire il push dei pacchetti in nuget.org, è necessario usare [nuget.exe v4.1.0 o versione successiva](https://www.nuget.org/downloads), che implementa i [protocolli NuGet](../api/nuget-protocols.md) necessari.

1. Per praticità, salvare la chiave API con NuGet (vedere [Pubblicare un pacchetto](../create-packages/publish-a-package.md)), che si applicherà sia a nuget.org che a symbolsource.org, dal momento che symbolsource.org controllerà con nuget.org per verificare che l'utente sia il proprietario del pacchetto.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Dopo avere pubblicato il pacchetto principale su nuget.org, eseguire il push del pacchetto di simboli come indicato di seguito, che userà automaticamente symbolsource.org come destinazione a causa di `.symbols` nel nome di file:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Per procedere alla pubblicazione in un repository di simboli diverso o per eseguire il push di un pacchetto di simboli che non segue la convenzione di denominazione, usare l'opzione `-Source`:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. È anche possibile eseguire il push sia dei pacchetti di simboli che di quelli principali in entrambi i repository contemporaneamente usando il codice seguente:

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > Con nuget.exe 4.5.0 o versioni successive, non viene eseguito automaticamente il push dei pacchetti di simboli in symbolsource.org, ma sarà necessario eseguire il push dei pacchetti di simboli separatamente, come illustrato nel passaggio successivo.
   
In questo caso, NuGet pubblicherà `MyPackage.symbols.nupkg`, se presente, in https://nuget.smbsrc.net/ (URL di push per symbolsource.org), dopo la pubblicazione del pacchetto principale in nuget.org.

## <a name="see-also"></a>Vedere anche

[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (Passaggio al nuovo motore SymbolSource) su symbolsource.org
