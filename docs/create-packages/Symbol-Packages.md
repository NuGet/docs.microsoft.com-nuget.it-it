---
title: Creazione di pacchetti di simboli legacy (. symbols. nupkg)
description: Come creare pacchetti NuGet contenenti solo i simboli per supportare il debug di altri pacchetti NuGet in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: d9a96986bf80aa15423d7dcee6ea3fe59255252b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774546"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a>Creazione di pacchetti di simboli legacy (. symbols. nupkg)

> [!Important]
> Il nuovo formato consigliato per i pacchetti di simboli è l'estensione snupkg. Vedere [Creazione di pacchetti di simboli (estensione snupkg)](Symbol-Packages-snupkg.md). </br>
> .symbols.nupkg è ancora supportato ma solo per motivi di compatibilità.

Oltre alla compilazione di pacchetti per nuget.org o altre origini, NuGet supporta anche la creazione di pacchetti di simboli associati che possono essere pubblicati in server di simboli. Il formato del pacchetto di simboli legacy,. symbols. nupkg, può essere inserito nel repository SymbolSource.

I consumer di pacchetti possono quindi aggiungere `https://nuget.smbsrc.net` alle loro origini dei simboli in Visual Studio, in modo da consentire l'esecuzione delle istruzioni nel codice del pacchetto nel debugger di Visual Studio. Vedere [Specifica di file di simboli (con estensione pdb) e di file di origine nel debugger di Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) per informazioni dettagliate su questo processo.

## <a name="creating-a-legacy-symbol-package"></a>Creazione di un pacchetto di simboli legacy

Per creare un pacchetto di simboli legacy, attenersi alle convenzioni seguenti:

- Assegnare al pacchetto principale (con il codice) il nome `{identifier}.nupkg` e includere tutti i file tranne i file `.pdb`.
- Denominare il pacchetto di simboli legacy `{identifier}.symbols.nupkg` e includere la DLL dell'assembly, i file, i file xmldoc e i `.pdb` file di origine (vedere le sezioni seguenti).

È possibile creare entrambi i pacchetti con l'opzione `-Symbols`, da un file `.nuspec` o da un file di progetto:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Si noti che `pack` richiede Mono 4.4.2 su Mac OS X e non funziona nei sistemi Linux. In un Mac è anche necessario convertire i nomi di percorso di Windows nel file `.nuspec` in percorsi di tipo Unix.

## <a name="legacy-symbol-package-structure"></a>Struttura del pacchetto di simboli legacy

Un pacchetto di simboli legacy può essere destinato a più framework di destinazione nello stesso modo in cui è presente un pacchetto di libreria, quindi la struttura della `lib` cartella deve essere esattamente identica al pacchetto principale, includendo solo i `.pdb` file insieme alla dll.

Ad esempio, un pacchetto di simboli legacy destinato a .NET 4,0 e Silverlight 4 avrà questo layout:

```
\lib
    \net40
        \MyAssembly.dll
        \MyAssembly.pdb
    \sl40
        \MyAssembly.dll
        \MyAssembly.pdb
```

I file di origine vengono quindi inseriti in una speciale cartella separata denominata `src`, che deve seguire la relativa struttura del repository di origine. Ciò è dovuto al fatto che i file PDB contengono i percorsi assoluti dei file di origine usati per compilare la DLL corrispondente e devono essere rilevati durante il processo di pubblicazione. Un percorso di base (prefisso del percorso comune) può essere rimosso. Si consideri, ad esempio, una libreria compilata da questi file:

```
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
```

A parte la `lib` cartella, un pacchetto di simboli legacy deve contenere questo layout:

```
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
```

## <a name="referring-to-files-in-the-nuspec"></a>Riferimento ai file nel file nuspec

Un pacchetto di simboli legacy può essere compilato da convenzioni, da una struttura di cartelle come descritto nella sezione precedente o specificandone il contenuto nella `files` sezione del manifesto. Ad esempio, per compilare il pacchetto mostrato nella sezione precedente, usare il codice seguente nel file `.nuspec`:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a>Pubblicazione di un pacchetto di simboli legacy

> [!Important]
> Per eseguire il push dei pacchetti in nuget.org, è necessario usare [nuget.exe v4.9.1 o versione successiva](https://www.nuget.org/downloads), che implementa i [protocolli NuGet](../api/nuget-protocols.md) necessari.

1. Per praticità, salvare la chiave API con NuGet (vedere [Pubblicare un pacchetto](../nuget-org/publish-a-package.md)), che si applicherà sia a nuget.org che a symbolsource.org, dal momento che symbolsource.org controllerà con nuget.org per verificare che l'utente sia il proprietario del pacchetto.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Dopo aver pubblicato il pacchetto primario in nuget.org, eseguire il push del pacchetto di simboli legacy come indicato di seguito, che userà automaticamente symbolsource.org come destinazione a causa di `.symbols` nel nome file:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Per eseguire la pubblicazione in un repository di simboli diverso o per eseguire il push di un pacchetto di simboli legacy che non segue la convenzione di denominazione, usare l' `-Source` opzione:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. È anche possibile eseguire il push sia dei pacchetti di simboli che di quelli principali in entrambi i repository contemporaneamente usando il codice seguente:

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > Con nuget.exe 4.5.0 o versione successiva, i pacchetti di simboli non vengono inseriti automaticamente in symbolsource.org. È necessario eseguire il push dei pacchetti di simboli separatamente, come illustrato nei passaggi precedenti.
   
In questo caso, NuGet pubblicherà `MyPackage.symbols.nupkg`, se presente, in https://nuget.smbsrc.net/ (URL di push per symbolsource.org), dopo la pubblicazione del pacchetto principale in nuget.org.

## <a name="see-also"></a>Vedere anche

* [Creazione di pacchetti di simboli (con estensione snupkg)](Symbol-Packages-snupkg.md) : nuovo formato consigliato per i pacchetti di simboli
* [Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (Passaggio al nuovo motore SymbolSource) su symbolsource.org
