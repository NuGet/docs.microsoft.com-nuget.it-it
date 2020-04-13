---
title: Creazione di pacchetti di simboli legacy (.symbols.nupkg)
description: Come creare pacchetti NuGet contenenti solo i simboli per supportare il debug di altri pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 374e9ccfc01cd06508e76529765db3f849342222
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "77476269"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a>Creazione di pacchetti di simboli legacy (.symbols.nupkg)

> [!Important]
> Il nuovo formato consigliato per i pacchetti di simboli è l'estensione snupkg. Vedere [Creazione di pacchetti di simboli (estensione snupkg)](Symbol-Packages-snupkg.md). </br>
> .symbols.nupkg è ancora supportato ma solo per motivi di compatibilità.

Oltre alla creazione di pacchetti per nuget.org o altre origini, NuGet supporta anche la creazione di pacchetti di simboli associati che possono essere pubblicati nei server di simboli. Il formato del pacchetto di simboli legacy, .symbols.nupkg, può essere inserito nel repository SymbolSource.

I consumer di pacchetti possono quindi aggiungere `https://nuget.smbsrc.net` alle loro origini dei simboli in Visual Studio, in modo da consentire l'esecuzione delle istruzioni nel codice del pacchetto nel debugger di Visual Studio. Vedere [Specifica di file di simboli (con estensione pdb) e di file di origine nel debugger di Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) per informazioni dettagliate su questo processo.

## <a name="creating-a-legacy-symbol-package"></a>Creazione di un pacchetto di simboli legacyCreating a legacy symbol package

Per creare un pacchetto di simboli legacy, seguire queste convenzioni:To create a legacy symbol package, follow these conventions:

- Assegnare al pacchetto principale (con il codice) il nome `{identifier}.nupkg` e includere tutti i file tranne i file `.pdb`.
- Assegnare al `{identifier}.symbols.nupkg` pacchetto di simboli `.pdb` legacy il nome e includere la DLL dell'assembly, i file, i file XMLDOC, i file di origine (vedere le sezioni che seguono).

È possibile creare entrambi i pacchetti con l'opzione `-Symbols`, da un file `.nuspec` o da un file di progetto:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Si noti che `pack` richiede Mono 4.4.2 su Mac OS X e non funziona nei sistemi Linux. In un Mac è anche necessario convertire i nomi di percorso di Windows nel file `.nuspec` in percorsi di tipo Unix.

## <a name="legacy-symbol-package-structure"></a>Struttura del pacchetto di simboli legacy

Un pacchetto di simboli legacy può essere destinato a più framework di destinazione `lib` nello stesso modo di un pacchetto `.pdb` di libreria, pertanto la struttura della cartella deve essere esattamente la stessa del pacchetto primario, includendo solo i file accanto alla DLL.

Ad esempio, un pacchetto di simboli legacy destinato a .NET 4.0 e Silverlight 4 avrebbe questo layout:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

I file di origine vengono quindi inseriti in una speciale cartella separata denominata `src`, che deve seguire la relativa struttura del repository di origine. Ciò è dovuto al fatto che i file PDB contengono i percorsi assoluti dei file di origine usati per compilare la DLL corrispondente e devono essere rilevati durante il processo di pubblicazione. Un percorso di base (prefisso di percorso comune) può essere rimosso. Si consideri, ad esempio, una libreria creata da questi file:For example, consider a library built from these files:

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

Oltre alla `lib` cartella, un pacchetto di simboli legacy dovrebbe contenere questo layout:From from the folder, a legacy symbol package would need to contain this layout:

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

Un pacchetto di simboli legacy può essere compilato in base alle convenzioni, da una `files` struttura di cartelle come descritto nella sezione precedente o specificandone il contenuto nella sezione del manifesto. Ad esempio, per compilare il pacchetto mostrato nella sezione precedente, usare il codice seguente nel file `.nuspec`:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a>Pubblicazione di un pacchetto di simboli legacyPublishing a legacy symbol package

> [!Important]
> Per eseguire il push dei pacchetti in nuget.org, è necessario usare [nuget.exe v4.9.1 o versione successiva](https://www.nuget.org/downloads), che implementa i [protocolli NuGet](../api/nuget-protocols.md) necessari.

1. Per praticità, salvare la chiave API con NuGet (vedere [Pubblicare un pacchetto](../nuget-org/publish-a-package.md)), che si applicherà sia a nuget.org che a symbolsource.org, dal momento che symbolsource.org controllerà con nuget.org per verificare che l'utente sia il proprietario del pacchetto.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Dopo aver pubblicato il pacchetto principale in nuget.org, eseguire il push del pacchetto `.symbols` di simboli legacy come indicato di seguito, che utilizzerà automaticamente symbolsource.org come destinazione a causa del file nel nome del file:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Per pubblicare in un repository di simboli diverso o per eseguire il push `-Source` di un pacchetto di simboli legacy che non segue la convenzione di denominazione, utilizzare l'opzione:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. È anche possibile eseguire il push sia dei pacchetti di simboli che di quelli principali in entrambi i repository contemporaneamente usando il codice seguente:

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > Con nuget.exe 4.5.0 o versioni successive, i pacchetti di simboli non vengono automaticamente inviati a symbolsource.org. È necessario eseguire il push dei pacchetti di simboli separatamente come spiegato nei passaggi precedenti.
   
In questo caso, NuGet pubblicherà `MyPackage.symbols.nupkg`, se presente, in https://nuget.smbsrc.net/ (URL di push per symbolsource.org), dopo la pubblicazione del pacchetto principale in nuget.org.

## <a name="see-also"></a>Vedere anche

* [Creazione di pacchetti di simboli (.snupkg)](Symbol-Packages-snupkg.md) - Il nuovo formato consigliato per i pacchetti di simboli
* [Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (Passaggio al nuovo motore SymbolSource) su symbolsource.org
