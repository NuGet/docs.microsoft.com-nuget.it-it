---
title: Come creare pacchetti di simboli NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 09/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Come creare pacchetti NuGet contenenti solo i simboli per supportare il debug di altri pacchetti NuGet in Visual Studio.
keywords: Pacchetti di simboli NuGet, debug dei pacchetti NuGet, supporto per il debug di NuGet, simboli in pacchetti, convenzioni dei pacchetti di simboli
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 6b6ddb0ca8ac5d7589dc5cb6de66ee3aa5faf8b6
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="creating-symbol-packages"></a><span data-ttu-id="ff7b3-104">Creazione di pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="ff7b3-104">Creating symbol packages</span></span>

<span data-ttu-id="ff7b3-105">Oltre alla compilazione di pacchetti per nuget.org o altre origini, NuGet supporta anche la creazione dei pacchetti di simboli associati e la relativa pubblicazione nel repository SymbolSource.</span><span class="sxs-lookup"><span data-stu-id="ff7b3-105">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the SymbolSource repository.</span></span>

<span data-ttu-id="ff7b3-106">I consumer di pacchetti possono quindi aggiungere `https://nuget.smbsrc.net` alle loro origini dei simboli in Visual Studio, in modo da consentire l'esecuzione delle istruzioni nel codice del pacchetto nel debugger di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ff7b3-106">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="ff7b3-107">Vedere [Specifica di file di simboli (con estensione pdb) e di file di origine nel debugger di Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) per informazioni dettagliate su questo processo.</span><span class="sxs-lookup"><span data-stu-id="ff7b3-107">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="ff7b3-108">Creazione di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="ff7b3-108">Creating a symbol package</span></span>

<span data-ttu-id="ff7b3-109">Per creare un pacchetto di simboli, seguire queste convenzioni:</span><span class="sxs-lookup"><span data-stu-id="ff7b3-109">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="ff7b3-110">Assegnare al pacchetto principale (con il codice) il nome `{identifier}.nupkg` e includere tutti i file tranne i file `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="ff7b3-110">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="ff7b3-111">Assegnare al pacchetto di simboli il nome `{identifier}.symbols.nupkg` e includere la DLL dell'assembly, i file `.pdb`, i file XMLDOC e i file di origine (vedere le sezioni successive).</span><span class="sxs-lookup"><span data-stu-id="ff7b3-111">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="ff7b3-112">È possibile creare entrambi i pacchetti con l'opzione `-Symbols`, da un file `.nuspec` o da un file di progetto:</span><span class="sxs-lookup"><span data-stu-id="ff7b3-112">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="ff7b3-113">Si noti che `pack` richiede Mono 4.4.2 su Mac OS X e non funziona nei sistemi Linux.</span><span class="sxs-lookup"><span data-stu-id="ff7b3-113">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="ff7b3-114">In un Mac è anche necessario convertire i nomi di percorso di Windows nel file `.nuspec` in percorsi di tipo Unix.</span><span class="sxs-lookup"><span data-stu-id="ff7b3-114">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="ff7b3-115">Struttura di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="ff7b3-115">Symbol package structure</span></span>

<span data-ttu-id="ff7b3-116">Un pacchetto di simboli può avere come destinazione più framework di destinazione analogamente a un pacchetto di librerie, pertanto la struttura della cartella `lib` deve corrispondere esattamente a quella del pacchetto principale, includendo solo i file `.pdb` insieme alla DLL.</span><span class="sxs-lookup"><span data-stu-id="ff7b3-116">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="ff7b3-117">Ad esempio, un pacchetto di simboli che ha come destinazione .NET 4.0 e Silverlight 4 dovrebbe avere questo layout:</span><span class="sxs-lookup"><span data-stu-id="ff7b3-117">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="ff7b3-118">I file di origine vengono quindi inseriti in una speciale cartella separata denominata `src`, che deve seguire la relativa struttura del repository di origine.</span><span class="sxs-lookup"><span data-stu-id="ff7b3-118">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="ff7b3-119">Ciò è dovuto al fatto che i file PDB contengono i percorsi assoluti dei file di origine usati per compilare la DLL corrispondente e devono essere rilevati durante il processo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="ff7b3-119">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="ff7b3-120">Un percorso di base (prefisso di percorso comune) può essere rimosso. Si consideri ad esempio una libreria compilata da questi file:</span><span class="sxs-lookup"><span data-stu-id="ff7b3-120">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="ff7b3-121">A parte la cartella `lib`, un pacchetto di simboli dovrà contenere questo layout:</span><span class="sxs-lookup"><span data-stu-id="ff7b3-121">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="ff7b3-122">Riferimento ai file nel file nuspec</span><span class="sxs-lookup"><span data-stu-id="ff7b3-122">Referring to files in the nuspec</span></span>

<span data-ttu-id="ff7b3-123">Un pacchetto di simboli può essere generato in base alle convenzioni, da una struttura di cartelle come descritto nella sezione precedente oppure specificandone il contenuto nella sezione `files` del manifesto.</span><span class="sxs-lookup"><span data-stu-id="ff7b3-123">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="ff7b3-124">Ad esempio, per compilare il pacchetto mostrato nella sezione precedente, usare il codice seguente nel file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="ff7b3-124">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="ff7b3-125">Pubblicazione di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="ff7b3-125">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="ff7b3-126">Per eseguire il push dei pacchetti in nuget.org, è necessario usare [nuget.exe v4.1.0 o versione successiva](https://www.nuget.org/downloads), che implementa i [protocolli NuGet](../api/nuget-protocols.md) necessari.</span><span class="sxs-lookup"><span data-stu-id="ff7b3-126">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="ff7b3-127">Per praticità, salvare la chiave API con NuGet (vedere [Pubblicare un pacchetto](../create-packages/publish-a-package.md)), che si applicherà sia a nuget.org che a symbolsource.org, dal momento che symbolsource.org controllerà con nuget.org per verificare che l'utente sia il proprietario del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ff7b3-127">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="ff7b3-128">Dopo avere pubblicato il pacchetto principale su nuget.org, eseguire il push del pacchetto di simboli come indicato di seguito, che userà automaticamente symbolsource.org come destinazione a causa di `.symbols` nel nome di file:</span><span class="sxs-lookup"><span data-stu-id="ff7b3-128">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```
> [!Note]
> <span data-ttu-id="ff7b3-129">Con nuget.exe 4.5.0 o versioni successive, non viene eseguito automaticamente il push dei pacchetti di simboli in symbolsource.org, ma sarà necessario eseguire il push dei pacchetti di simboli separatamente, come illustrato nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="ff7b3-129">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the next step.</span></span>

1. <span data-ttu-id="ff7b3-130">Per procedere alla pubblicazione in un repository di simboli diverso o per eseguire il push di un pacchetto di simboli che non segue la convenzione di denominazione, usare l'opzione `-Source`:</span><span class="sxs-lookup"><span data-stu-id="ff7b3-130">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

1. <span data-ttu-id="ff7b3-131">È anche possibile eseguire il push sia dei pacchetti di simboli che di quelli principali in entrambi i repository contemporaneamente usando il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="ff7b3-131">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="ff7b3-132">In questo caso, NuGet pubblicherà `MyPackage.symbols.nupkg`, se presente, in https://nuget.smbsrc.net/ (URL di push per symbolsource.org), dopo la pubblicazione del pacchetto principale in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ff7b3-132">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="ff7b3-133">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ff7b3-133">See Also</span></span>

<span data-ttu-id="ff7b3-134">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (Passaggio al nuovo motore SymbolSource) su symbolsource.org</span><span class="sxs-lookup"><span data-stu-id="ff7b3-134">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
