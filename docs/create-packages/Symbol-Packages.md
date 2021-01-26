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
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a><span data-ttu-id="96c51-103">Creazione di pacchetti di simboli legacy (. symbols. nupkg)</span><span class="sxs-lookup"><span data-stu-id="96c51-103">Creating legacy symbol packages (.symbols.nupkg)</span></span>

> [!Important]
> <span data-ttu-id="96c51-104">Il nuovo formato consigliato per i pacchetti di simboli è l'estensione snupkg.</span><span class="sxs-lookup"><span data-stu-id="96c51-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="96c51-105">Vedere [Creazione di pacchetti di simboli (estensione snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="96c51-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="96c51-106">.symbols.nupkg è ancora supportato ma solo per motivi di compatibilità.</span><span class="sxs-lookup"><span data-stu-id="96c51-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="96c51-107">Oltre alla compilazione di pacchetti per nuget.org o altre origini, NuGet supporta anche la creazione di pacchetti di simboli associati che possono essere pubblicati in server di simboli.</span><span class="sxs-lookup"><span data-stu-id="96c51-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages that can be published to symbol servers.</span></span> <span data-ttu-id="96c51-108">Il formato del pacchetto di simboli legacy,. symbols. nupkg, può essere inserito nel repository SymbolSource.</span><span class="sxs-lookup"><span data-stu-id="96c51-108">The legacy symbol package format, .symbols.nupkg, can be pushed to the SymbolSource repository.</span></span>

<span data-ttu-id="96c51-109">I consumer di pacchetti possono quindi aggiungere `https://nuget.smbsrc.net` alle loro origini dei simboli in Visual Studio, in modo da consentire l'esecuzione delle istruzioni nel codice del pacchetto nel debugger di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="96c51-109">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="96c51-110">Vedere [Specifica di file di simboli (con estensione pdb) e di file di origine nel debugger di Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) per informazioni dettagliate su questo processo.</span><span class="sxs-lookup"><span data-stu-id="96c51-110">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-legacy-symbol-package"></a><span data-ttu-id="96c51-111">Creazione di un pacchetto di simboli legacy</span><span class="sxs-lookup"><span data-stu-id="96c51-111">Creating a legacy symbol package</span></span>

<span data-ttu-id="96c51-112">Per creare un pacchetto di simboli legacy, attenersi alle convenzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="96c51-112">To create a legacy symbol package, follow these conventions:</span></span>

- <span data-ttu-id="96c51-113">Assegnare al pacchetto principale (con il codice) il nome `{identifier}.nupkg` e includere tutti i file tranne i file `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="96c51-113">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="96c51-114">Denominare il pacchetto di simboli legacy `{identifier}.symbols.nupkg` e includere la DLL dell'assembly, i file, i file xmldoc e i `.pdb` file di origine (vedere le sezioni seguenti).</span><span class="sxs-lookup"><span data-stu-id="96c51-114">Name the legacy symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="96c51-115">È possibile creare entrambi i pacchetti con l'opzione `-Symbols`, da un file `.nuspec` o da un file di progetto:</span><span class="sxs-lookup"><span data-stu-id="96c51-115">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="96c51-116">Si noti che `pack` richiede Mono 4.4.2 su Mac OS X e non funziona nei sistemi Linux.</span><span class="sxs-lookup"><span data-stu-id="96c51-116">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="96c51-117">In un Mac è anche necessario convertire i nomi di percorso di Windows nel file `.nuspec` in percorsi di tipo Unix.</span><span class="sxs-lookup"><span data-stu-id="96c51-117">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="legacy-symbol-package-structure"></a><span data-ttu-id="96c51-118">Struttura del pacchetto di simboli legacy</span><span class="sxs-lookup"><span data-stu-id="96c51-118">Legacy symbol package structure</span></span>

<span data-ttu-id="96c51-119">Un pacchetto di simboli legacy può essere destinato a più framework di destinazione nello stesso modo in cui è presente un pacchetto di libreria, quindi la struttura della `lib` cartella deve essere esattamente identica al pacchetto principale, includendo solo i `.pdb` file insieme alla dll.</span><span class="sxs-lookup"><span data-stu-id="96c51-119">A legacy symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="96c51-120">Ad esempio, un pacchetto di simboli legacy destinato a .NET 4,0 e Silverlight 4 avrà questo layout:</span><span class="sxs-lookup"><span data-stu-id="96c51-120">For example, a legacy symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

```
\lib
    \net40
        \MyAssembly.dll
        \MyAssembly.pdb
    \sl40
        \MyAssembly.dll
        \MyAssembly.pdb
```

<span data-ttu-id="96c51-121">I file di origine vengono quindi inseriti in una speciale cartella separata denominata `src`, che deve seguire la relativa struttura del repository di origine.</span><span class="sxs-lookup"><span data-stu-id="96c51-121">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="96c51-122">Ciò è dovuto al fatto che i file PDB contengono i percorsi assoluti dei file di origine usati per compilare la DLL corrispondente e devono essere rilevati durante il processo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="96c51-122">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="96c51-123">Un percorso di base (prefisso del percorso comune) può essere rimosso. Si consideri, ad esempio, una libreria compilata da questi file:</span><span class="sxs-lookup"><span data-stu-id="96c51-123">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="96c51-124">A parte la `lib` cartella, un pacchetto di simboli legacy deve contenere questo layout:</span><span class="sxs-lookup"><span data-stu-id="96c51-124">Apart from the `lib` folder, a legacy symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="96c51-125">Riferimento ai file nel file nuspec</span><span class="sxs-lookup"><span data-stu-id="96c51-125">Referring to files in the nuspec</span></span>

<span data-ttu-id="96c51-126">Un pacchetto di simboli legacy può essere compilato da convenzioni, da una struttura di cartelle come descritto nella sezione precedente o specificandone il contenuto nella `files` sezione del manifesto.</span><span class="sxs-lookup"><span data-stu-id="96c51-126">A legacy symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="96c51-127">Ad esempio, per compilare il pacchetto mostrato nella sezione precedente, usare il codice seguente nel file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="96c51-127">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a><span data-ttu-id="96c51-128">Pubblicazione di un pacchetto di simboli legacy</span><span class="sxs-lookup"><span data-stu-id="96c51-128">Publishing a legacy symbol package</span></span>

> [!Important]
> <span data-ttu-id="96c51-129">Per eseguire il push dei pacchetti in nuget.org, è necessario usare [nuget.exe v4.9.1 o versione successiva](https://www.nuget.org/downloads), che implementa i [protocolli NuGet](../api/nuget-protocols.md) necessari.</span><span class="sxs-lookup"><span data-stu-id="96c51-129">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="96c51-130">Per praticità, salvare la chiave API con NuGet (vedere [Pubblicare un pacchetto](../nuget-org/publish-a-package.md)), che si applicherà sia a nuget.org che a symbolsource.org, dal momento che symbolsource.org controllerà con nuget.org per verificare che l'utente sia il proprietario del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="96c51-130">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="96c51-131">Dopo aver pubblicato il pacchetto primario in nuget.org, eseguire il push del pacchetto di simboli legacy come indicato di seguito, che userà automaticamente symbolsource.org come destinazione a causa di `.symbols` nel nome file:</span><span class="sxs-lookup"><span data-stu-id="96c51-131">After publishing your primary package to nuget.org, push the legacy symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="96c51-132">Per eseguire la pubblicazione in un repository di simboli diverso o per eseguire il push di un pacchetto di simboli legacy che non segue la convenzione di denominazione, usare l' `-Source` opzione:</span><span class="sxs-lookup"><span data-stu-id="96c51-132">To publish to a different symbol repository, or to push a legacy symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="96c51-133">È anche possibile eseguire il push sia dei pacchetti di simboli che di quelli principali in entrambi i repository contemporaneamente usando il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="96c51-133">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="96c51-134">Con nuget.exe 4.5.0 o versione successiva, i pacchetti di simboli non vengono inseriti automaticamente in symbolsource.org. È necessario eseguire il push dei pacchetti di simboli separatamente, come illustrato nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="96c51-134">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="96c51-135">In questo caso, NuGet pubblicherà `MyPackage.symbols.nupkg`, se presente, in https://nuget.smbsrc.net/ (URL di push per symbolsource.org), dopo la pubblicazione del pacchetto principale in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="96c51-135">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="96c51-136">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="96c51-136">See also</span></span>

* <span data-ttu-id="96c51-137">[Creazione di pacchetti di simboli (con estensione snupkg)](Symbol-Packages-snupkg.md) : nuovo formato consigliato per i pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="96c51-137">[Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md) - The new recommended format for symbol packages</span></span>
* <span data-ttu-id="96c51-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (Passaggio al nuovo motore SymbolSource) su symbolsource.org</span><span class="sxs-lookup"><span data-stu-id="96c51-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
