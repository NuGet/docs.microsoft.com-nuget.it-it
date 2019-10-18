---
title: Creare un pacchetto NuGet con l'interfaccia della riga di comando di nuget.exe
description: Guida dettagliata al processo di progettazione e creazione di un pacchetto NuGet, incluse le principali decisioni critiche, ad esempio quelle relative ai file e al controllo delle versioni.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 353654d12e137222ab24417f30fd22e9f027c324
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380701"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a><span data-ttu-id="a0f9c-103">Creare un pacchetto usando l'interfaccia della riga di comando di nuget.exe</span><span class="sxs-lookup"><span data-stu-id="a0f9c-103">Create a package using the nuget.exe CLI</span></span>

<span data-ttu-id="a0f9c-104">Indipendentemente dalle operazioni eseguite dal pacchetto o dal tipo di codice contenuto, è possibile usare uno degli strumenti dell'interfaccia della riga di comando, ovvero `nuget.exe` o `dotnet.exe`. per rendere disponibili tali funzionalità in un componente condivisibile e utilizzabile da altri sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="a0f9c-105">Per installare gli strumenti dell'interfaccia della riga di comando di NuGet, vedere [Installare gli strumenti client di NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-105">To install NuGet CLI tools, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="a0f9c-106">Si noti che Visual Studio non include automaticamente uno strumento dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-106">Note that Visual Studio does not automatically include a CLI tool.</span></span>

- <span data-ttu-id="a0f9c-107">Per i progetti non di tipo SDK, in genere progetti .NET Framework, seguire la procedura descritta in questo articolo per creare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-107">For non-SDK-style projects, typically .NET Framework projects, follow the steps described in this article to create a package.</span></span> <span data-ttu-id="a0f9c-108">Per istruzioni dettagliate sull'uso di Visual Studio e dell'interfaccia della riga di comando di `nuget.exe`, vedere [Creare e pubblicare un pacchetto .NET Framework](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-108">For step-by-step instructions using Visual Studio and the `nuget.exe` CLI, see [Create and publish a .NET Framework package](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span></span>

- <span data-ttu-id="a0f9c-109">Per i progetti .NET Core e .NET Standard che usano il [formato di tipo SDK](../resources/check-project-format.md), e qualsiasi altro progetto di tipo SDK, vedere [Creare un pacchetto NuGet con l'interfaccia della riga di comando di dotnet](creating-a-package-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-109">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, see [Create a NuGet package using the dotnet CLI](creating-a-package-dotnet-cli.md).</span></span>

- <span data-ttu-id="a0f9c-110">Per i progetti migrati da `packages.config` a [PackageReference](../consume-packages/package-references-in-project-files.md), usare [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-110">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

<span data-ttu-id="a0f9c-111">Da un punto di vista tecnico, un pacchetto NuGet è solo un file ZIP rinominato con l'estensione `.nupkg` e i cui contenuti rispettano determinate convenzioni.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-111">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="a0f9c-112">Questo argomento descrive il processo dettagliato di creazione di un pacchetto che soddisfa tali convenzioni.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-112">This topic describes the detailed process of creating a package that meets those conventions.</span></span>

<span data-ttu-id="a0f9c-113">La creazione di un pacchetto inizia con il codice compilato (assembly), i simboli e/o altri file che si vuole distribuire come pacchetto. Vedere [Panoramica e flusso di lavoro](overview-and-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-113">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="a0f9c-114">Questo processo è indipendente dalla compilazione o comunque dalla generazione dei file inseriti nel pacchetto, anche se è possibile usare le informazioni contenute in un file di progetto per mantenere sincronizzati i pacchetti e gli assembly compilati.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-114">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Important]
> <span data-ttu-id="a0f9c-115">Questo argomento si applica ai progetti non in stile SDK, in genere progetti diversi dai progetti .NET Core e .NET Standard che usano Visual Studio 2017 e versioni successive e NuGet 4.0+.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-115">This topic applies to non-SDK-style projects, typically projects other than .NET Core and .NET Standard projects using Visual Studio 2017 and higher versions and NuGet 4.0+.</span></span>

## <a name="decide-which-assemblies-to-package"></a><span data-ttu-id="a0f9c-116">Scegliere gli assembly per cui creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="a0f9c-116">Decide which assemblies to package</span></span>

<span data-ttu-id="a0f9c-117">La maggior parte dei pacchetti per utilizzo generico contiene uno o più assembly che gli altri sviluppatori possono usare nei propri progetti.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-117">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="a0f9c-118">In generale, l'ideale è avere un assembly per ogni pacchetto NuGet, purché ogni assembly abbia una propria utilità.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-118">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="a0f9c-119">Se ad esempio è presente un file `Utilities.dll` che dipende da `Parser.dll` e `Parser.dll` è utile di per sé, creare un pacchetto per ognuno.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-119">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="a0f9c-120">In questo modo gli sviluppatori possono usare `Parser.dll` indipendentemente da `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-120">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="a0f9c-121">Se la libreria è costituita da più assembly che non hanno una propria utilità, è consigliabile combinarli in un solo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-121">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="a0f9c-122">Usando l'esempio precedente, se `Parser.dll` contiene codice che viene usato solo da `Utilities.dll`, è consigliabile tenere `Parser.dll` nello stesso pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-122">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="a0f9c-123">Analogamente, se `Utilities.dll` dipende da `Utilities.resources.dll` e quest'ultimo non è utile di per sé, inserirli entrambi nello stesso pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-123">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="a0f9c-124">Le risorse sono di fatto un caso particolare.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-124">Resources are, in fact, a special case.</span></span> <span data-ttu-id="a0f9c-125">Quando un pacchetto viene installato in un progetto, NuGet aggiunge automaticamente alle DLL del pacchetto i riferimenti agli assembly, *escludendo* quelli denominati `.resources.dll` perché si presuppone che siano assembly satellite localizzati. Vedere [Creazione di pacchetti localizzati](creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-125">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="a0f9c-126">Per questo motivo, evitare di usare `.resources.dll` per i file che contengono invece codice essenziale per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-126">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="a0f9c-127">Se la libreria contiene assembly di interoperabilità COM, seguire le linee guida aggiuntive in [Creare pacchetti con assembly di interoperabilità COM](author-packages-with-com-interop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-127">If your library contains COM interop assemblies, follow additional the guidelines in [Create packages with COM interop assemblies](author-packages-with-com-interop-assemblies.md).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="a0f9c-128">Ruolo e struttura del file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="a0f9c-128">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="a0f9c-129">Dopo avere deciso per quali file si vuole creare un pacchetto, il passaggio successivo prevede la creazione di un manifesto del pacchetto in un file XML `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-129">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="a0f9c-130">Il manifesto:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-130">The manifest:</span></span>

1. <span data-ttu-id="a0f9c-131">Descrive i contenuti del pacchetto e viene incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-131">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="a0f9c-132">Gestisce la creazione del pacchetto e indica a NuGet come installare il pacchetto in un progetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-132">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="a0f9c-133">Il manifesto, ad esempio, identifica le altre dipendenze del pacchetto in modo che NuGet possa installare anche tali dipendenze quando viene installato il pacchetto principale.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-133">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="a0f9c-134">Contiene le proprietà sia obbligatorie che facoltative, come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-134">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="a0f9c-135">Per informazioni dettagliate, incluse le altre proprietà non citate qui, vedere [Informazioni di riferimento sul file .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-135">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="a0f9c-136">Proprietà obbligatorie:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-136">Required properties:</span></span>

- <span data-ttu-id="a0f9c-137">Identificatore del pacchetto, che deve essere univoco nella raccolta che ospita il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-137">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="a0f9c-138">Numero di versione specifico nel formato *Major.Minor.Patch[-Suffix]* dove *-Suffix* identifica le [versioni preliminari](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="a0f9c-138">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="a0f9c-139">Titolo del pacchetto come deve essere visualizzato nell'host (ad esempio, nuget.org)</span><span class="sxs-lookup"><span data-stu-id="a0f9c-139">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="a0f9c-140">Informazioni sull'autore e sul proprietario.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-140">Author and owner information.</span></span>
- <span data-ttu-id="a0f9c-141">Descrizione estesa del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-141">A long description of the package.</span></span>

<span data-ttu-id="a0f9c-142">Proprietà facoltative comuni:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-142">Common optional properties:</span></span>

- <span data-ttu-id="a0f9c-143">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="a0f9c-143">Release notes</span></span>
- <span data-ttu-id="a0f9c-144">Informazioni sul copyright</span><span class="sxs-lookup"><span data-stu-id="a0f9c-144">Copyright information</span></span>
- <span data-ttu-id="a0f9c-145">Breve descrizione dell'[interfaccia utente di Gestione pacchetti in Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="a0f9c-145">A short description for the [Package Manager UI in Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span></span>
- <span data-ttu-id="a0f9c-146">ID impostazioni locali</span><span class="sxs-lookup"><span data-stu-id="a0f9c-146">A locale ID</span></span>
- <span data-ttu-id="a0f9c-147">URL progetto</span><span class="sxs-lookup"><span data-stu-id="a0f9c-147">Project URL</span></span>
- <span data-ttu-id="a0f9c-148">Licenza come espressione o file (`licenseUrl` è deprecato, usare l'elemento di metadati [`license` di nuspec](../reference/nuspec.md#license))</span><span class="sxs-lookup"><span data-stu-id="a0f9c-148">License as an expression or file (`licenseUrl` is being deprecated, use the [`license` nuspec metadata element](../reference/nuspec.md#license))</span></span>
- <span data-ttu-id="a0f9c-149">URL dell'icona</span><span class="sxs-lookup"><span data-stu-id="a0f9c-149">An icon URL</span></span>
- <span data-ttu-id="a0f9c-150">Elenchi di dipendenze e riferimenti</span><span class="sxs-lookup"><span data-stu-id="a0f9c-150">Lists of dependencies and references</span></span>
- <span data-ttu-id="a0f9c-151">Tag di supporto per le ricerche nella raccolta</span><span class="sxs-lookup"><span data-stu-id="a0f9c-151">Tags that assist in gallery searches</span></span>

<span data-ttu-id="a0f9c-152">Di seguito è riportato un file `.nuspec` tipico (ma fittizio), con commenti che descrivono le proprietà:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-152">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
        <!-- The identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- The package version number that is used when resolving dependencies -->
        <version>1.8.3-beta</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

<span data-ttu-id="a0f9c-153">Per informazioni dettagliate sulla dichiarazione delle dipendenze e sulla specifica dei numeri di versione, vedere [packages.config](../reference/packages-config.md) e [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-153">For details on declaring dependencies and specifying version numbers, see [packages.config](../reference/packages-config.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="a0f9c-154">È anche possibile esporre gli asset dalle dipendenze direttamente nel pacchetto usando gli attributi `include` ed `exclude` nell'elemento `dependency`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-154">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="a0f9c-155">Vedere la [sezione Dipendenze delle informazioni di riferimento sul file .nuspec](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-155">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="a0f9c-156">Poiché il manifesto è incluso nel pacchetto creato, per trovare altri esempi, esaminare i pacchetti esistenti.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-156">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="a0f9c-157">Una valida fonte è la cartella *global-packages* nel computer, la posizione della quale viene restituita dal comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-157">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="a0f9c-158">Andare a qualsiasi cartella *pacchetto\versione*, copiare il file `.nupkg` in un file `.zip`, quindi aprire il file `.zip` ed esaminare il file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-158">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="a0f9c-159">Quando si crea un file `.nuspec` da un progetto di Visual Studio, il manifesto contiene token che vengono sostituiti con le informazioni provenienti dal progetto quando il pacchetto viene compilato.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-159">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="a0f9c-160">Vedere [Creazione del file con estensione nuspec da un progetto di Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-160">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="create-the-nuspec-file"></a><span data-ttu-id="a0f9c-161">Creare il file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="a0f9c-161">Create the .nuspec file</span></span>

<span data-ttu-id="a0f9c-162">La creazione di un manifesto completo inizia in genere con un file `.nuspec` di base generato con uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-162">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="a0f9c-163">Directory di lavoro basata sulle convenzioni</span><span class="sxs-lookup"><span data-stu-id="a0f9c-163">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="a0f9c-164">DLL dell'assembly</span><span class="sxs-lookup"><span data-stu-id="a0f9c-164">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="a0f9c-165">Progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a0f9c-165">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="a0f9c-166">Nuovo file con valori predefiniti</span><span class="sxs-lookup"><span data-stu-id="a0f9c-166">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="a0f9c-167">Si modifica quindi il file manualmente in modo che descriva il contenuto esatto che dovrà essere incluso nel pacchetto finale.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-167">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="a0f9c-168">I file `.nuspec` generati contengono segnaposto che devono essere modificati prima di creare il pacchetto con il comando `nuget pack`,</span><span class="sxs-lookup"><span data-stu-id="a0f9c-168">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="a0f9c-169">che ha esito negativo se il file `.nuspec` contiene segnaposto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-169">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="a0f9c-170">Da una directory di lavoro basata sulle convenzioni</span><span class="sxs-lookup"><span data-stu-id="a0f9c-170">From a convention-based working directory</span></span>

<span data-ttu-id="a0f9c-171">Dato che un pacchetto NuGet è solo un file ZIP rinominato con l'estensione `.nupkg`, spesso è più semplice creare la struttura di cartelle necessaria nel file system locale e quindi creare il file `.nuspec` direttamente da tale struttura.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-171">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="a0f9c-172">Il comando `nuget pack` aggiunge quindi automaticamente tutti i file in tale struttura di cartelle, escluse le cartelle che iniziano con `.`, per poter mantenere i file privati nella stessa struttura.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-172">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="a0f9c-173">Il vantaggio di questo approccio è che non è necessario specificare nel manifesto i file che si vuole includere nel pacchetto, come illustrato più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-173">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="a0f9c-174">È sufficiente fare in modo che il processo di compilazione generi l'esatta struttura di cartelle da inserire nel pacchetto, per poter facilmente includere altri file che altrimenti potrebbero non fare parte di un progetto:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-174">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="a0f9c-175">Contenuto e codice sorgente da inserire nel progetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-175">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="a0f9c-176">Script PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0f9c-176">PowerShell scripts</span></span>
- <span data-ttu-id="a0f9c-177">Trasformazioni della configurazione esistente e dei file del codice sorgente di un progetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-177">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="a0f9c-178">Le convenzioni delle cartelle sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-178">The folder conventions are as follows:</span></span>

| <span data-ttu-id="a0f9c-179">Cartella</span><span class="sxs-lookup"><span data-stu-id="a0f9c-179">Folder</span></span> | <span data-ttu-id="a0f9c-180">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a0f9c-180">Description</span></span> | <span data-ttu-id="a0f9c-181">Azione durante l'installazione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="a0f9c-181">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a0f9c-182">(radice)</span><span class="sxs-lookup"><span data-stu-id="a0f9c-182">(root)</span></span> | <span data-ttu-id="a0f9c-183">Percorso del file readme.txt</span><span class="sxs-lookup"><span data-stu-id="a0f9c-183">Location for readme.txt</span></span> | <span data-ttu-id="a0f9c-184">Visual Studio visualizza un file readme.txt nella radice del pacchetto quando il pacchetto viene installato.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-184">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="a0f9c-185">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="a0f9c-185">lib/{tfm}</span></span> | <span data-ttu-id="a0f9c-186">File di assembly (`.dll`), di documentazione (`.xml`) e di simboli (`.pdb`) per il moniker del framework di destinazione (TFM, Target Framework Moniker) specificato</span><span class="sxs-lookup"><span data-stu-id="a0f9c-186">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="a0f9c-187">Gli assembly vengono aggiunti come riferimenti per la compilazione, oltre che per il runtime. `.xml` e `.pdb` vengono copiati nelle cartelle di progetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-187">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="a0f9c-188">Per la creazione di sottocartelle specifiche del framework di destinazione, vedere [Supporto di più framework di destinazione](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-188">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="a0f9c-189">ref/{tfm}</span><span class="sxs-lookup"><span data-stu-id="a0f9c-189">ref/{tfm}</span></span> | <span data-ttu-id="a0f9c-190">File di assembly (`.dll`) e di simboli (`.pdb`) per il moniker del framework di destinazione (TFM, Target Framework Moniker) specificato</span><span class="sxs-lookup"><span data-stu-id="a0f9c-190">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="a0f9c-191">Gli assembly vengono aggiunti come riferimenti solo per la fase di compilazione. Non verrà quindi copiato nulla nella cartella bin del progetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-191">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="a0f9c-192">runtimes</span><span class="sxs-lookup"><span data-stu-id="a0f9c-192">runtimes</span></span> | <span data-ttu-id="a0f9c-193">File di assembly (`.dll`), di simboli (`.pdb`) e di risorse native (`.pri`) specifici dell'architettura</span><span class="sxs-lookup"><span data-stu-id="a0f9c-193">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="a0f9c-194">Gli assembly vengono aggiunti come riferimenti solo per il runtime. Gli altri file vengono copiati nelle cartelle di progetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-194">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="a0f9c-195">Deve esistere sempre un assembly specifico `AnyCPU` corrispondente (TFM) sotto la cartella `/ref/{tfm}` per fornire l'assembly della fase di compilazione corrispondente.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-195">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="a0f9c-196">Vedere [Supporto di più framework di destinazione](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-196">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="a0f9c-197">contenuto</span><span class="sxs-lookup"><span data-stu-id="a0f9c-197">content</span></span> | <span data-ttu-id="a0f9c-198">File arbitrari</span><span class="sxs-lookup"><span data-stu-id="a0f9c-198">Arbitrary files</span></span> | <span data-ttu-id="a0f9c-199">I contenuti vengono copiati nella radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-199">Contents are copied to the project root.</span></span> <span data-ttu-id="a0f9c-200">La cartella **content** può essere considerata come la radice dell'applicazione di destinazione che in definitiva utilizza il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-200">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="a0f9c-201">Per fare in modo che il pacchetto aggiunga un'immagine nella cartella */images* dell'applicazione, inserirla nella cartella *content/images* del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-201">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="a0f9c-202">build</span><span class="sxs-lookup"><span data-stu-id="a0f9c-202">build</span></span> | <span data-ttu-id="a0f9c-203">*(3.x+)* File `.targets` e `.props` di MSBuild</span><span class="sxs-lookup"><span data-stu-id="a0f9c-203">*(3.x+)* MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="a0f9c-204">Vengono automaticamente inseriti nel progetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-204">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="a0f9c-205">buildMultiTargeting</span><span class="sxs-lookup"><span data-stu-id="a0f9c-205">buildMultiTargeting</span></span> | <span data-ttu-id="a0f9c-206">*(4.0+)* File `.targets` e `.props` di MSBuild per l'assegnazione di più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="a0f9c-206">*(4.0+)* MSBuild `.targets` and `.props` files for cross-framework targeting</span></span> | <span data-ttu-id="a0f9c-207">Vengono automaticamente inseriti nel progetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-207">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="a0f9c-208">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="a0f9c-208">buildTransitive</span></span> | <span data-ttu-id="a0f9c-209">*(5.0 +)* File `.targets` e `.props` di MSBuild che si propagano in modo transitivo a qualsiasi progetto che gli utilizza.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-209">*(5.0+)* MSBuild `.targets` and `.props` files that flow transitively to any consuming project.</span></span> <span data-ttu-id="a0f9c-210">Vedere la pagina delle [funzionalità](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-210">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> | <span data-ttu-id="a0f9c-211">Vengono automaticamente inseriti nel progetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-211">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="a0f9c-212">tools</span><span class="sxs-lookup"><span data-stu-id="a0f9c-212">tools</span></span> | <span data-ttu-id="a0f9c-213">Script di PowerShell e programmi accessibili dalla console di Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="a0f9c-213">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="a0f9c-214">La cartella `tools` viene aggiunta alla variabile di ambiente `PATH` solo per la console di Gestione pacchetti, in particolare *non* alla variabile `PATH` impostata per MSBuild durante la compilazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-214">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="a0f9c-215">Poiché la struttura di cartelle può contenere un numero indeterminato di assembly per un numero indeterminato di framework di destinazione, questo metodo è necessario quando si creano pacchetti che supportano più framework.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-215">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="a0f9c-216">In ogni caso, dopo avere creato la struttura di cartelle desiderata, eseguire il comando seguente in tale cartella per creare il file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-216">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="a0f9c-217">Anche in questo caso, il file `.nuspec` generato non contiene riferimenti espliciti ai file nella struttura di cartelle.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-217">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="a0f9c-218">NuGet include tutti i file automaticamente quando viene creato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-218">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="a0f9c-219">È tuttavia necessario modificare i valori dei segnaposto nelle altre parti del manifesto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-219">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="a0f9c-220">Da una DLL dell'assembly</span><span class="sxs-lookup"><span data-stu-id="a0f9c-220">From an assembly DLL</span></span>

<span data-ttu-id="a0f9c-221">Nel semplice caso della creazione di un pacchetto da un assembly, è possibile generare un file `.nuspec` dai metadati nell'assembly usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-221">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="a0f9c-222">Usando questo formato, alcuni segnaposto nel manifesto vengono sostituiti con i valori specifici dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-222">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="a0f9c-223">La proprietà `<id>`, ad esempio, viene impostata sul nome dell'assembly e `<version>` viene impostata sulla versione dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-223">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="a0f9c-224">Le altre proprietà del manifesto non hanno tuttavia valori corrispondenti nell'assembly e perciò contengono ancora i segnaposto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-224">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="a0f9c-225">Da un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a0f9c-225">From a Visual Studio project</span></span>

<span data-ttu-id="a0f9c-226">La creazione di un file `.nuspec` da un file `.csproj` o `.vbproj` è utile perché viene fatto automaticamente riferimento agli altri pacchetti che sono stati installati in tale progetto come a dipendenze.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-226">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="a0f9c-227">È sufficiente usare il comando seguente nella stessa cartella del file di progetto:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-227">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="a0f9c-228">Il file `<project-name>.nuspec` risultante contiene *token* che in fase di creazione del pacchetto vengono sostituiti con i valori del progetto, inclusi i riferimenti agli altri pacchetti già installati.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-228">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="a0f9c-229">In presenza di dipendenze del pacchetto da includere nel file con estensione *nuspec*, usare invece `nuget pack` e ottenere il file con estensione *nuspec* dall'interno del file con estensione *nupkg* generato.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-229">If you have package dependencies to include in the *.nuspec*, instead use `nuget pack`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="a0f9c-230">Ad esempio, usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-230">For example, use the following command.</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

<span data-ttu-id="a0f9c-231">Un token è delimitato dai simboli `$` su entrambi i lati della proprietà del progetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-231">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="a0f9c-232">Ad esempio, il valore `<id>` in un manifesto generato in questo modo solitamente viene visualizzato come segue:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-232">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="a0f9c-233">Questo token viene sostituito con il valore `AssemblyName` del file di progetto in fase di creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-233">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="a0f9c-234">Per il mapping esatto dei valori del progetto ai token di `.nuspec`, vedere le [informazioni di riferimento in Token di sostituzione](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-234">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="a0f9c-235">I token evitano di dover aggiornare i valori fondamentali, ad esempio il numero di versione, nel file `.nuspec` quando si aggiorna il progetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-235">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="a0f9c-236">È sempre possibile sostituire i token con valori letterali, se necessario.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-236">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="a0f9c-237">Tenere presente che sono disponibili diverse altre opzioni di creazione del pacchetto quando si usa un progetto di Visual Studio, come illustrato più avanti in [Esecuzione di nuget pack per generare il file con estensione nupkg](#run-nuget-pack-to-generate-the-nupkg-file).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-237">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#run-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="a0f9c-238">Pacchetti a livello di soluzione</span><span class="sxs-lookup"><span data-stu-id="a0f9c-238">Solution-level packages</span></span>

<span data-ttu-id="a0f9c-239">*Solo NuGet 2. x. Non disponibile in NuGet 3.0 +.*</span><span class="sxs-lookup"><span data-stu-id="a0f9c-239">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="a0f9c-240">NuGet 2.x supportava la nozione di pacchetto a livello di soluzione che installa strumenti o comandi aggiuntivi per la console di Gestione pacchetti (contenuti della cartella `tools`), ma non aggiunge riferimenti, contenuto o personalizzazioni delle compilazioni ai progetti della soluzione.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-240">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="a0f9c-241">Tali pacchetti non contengono file nelle cartelle `lib`, `content` o `build` dirette e nessuna dipendenza ha file nelle rispettive cartelle `lib`, `content` o `build`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-241">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="a0f9c-242">NuGet tiene traccia dei pacchetti a livello di soluzione installati in un file `packages.config` nella cartella `.nuget`, invece che nel file `packages.config` del progetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-242">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="a0f9c-243">Nuovo file con valori predefiniti</span><span class="sxs-lookup"><span data-stu-id="a0f9c-243">New file with default values</span></span>

<span data-ttu-id="a0f9c-244">Il comando seguente crea un manifesto predefinito con segnaposto, che assicura di iniziare con la struttura di file corretta:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-244">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="a0f9c-245">Se si omette \<package-name\>, il file risultante è `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-245">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="a0f9c-246">Se come nome si specifica ad esempio `Contoso.Utility.UsefulStuff`, il file è `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-246">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="a0f9c-247">Il file `.nuspec` risultante contiene segnaposto per i valori come `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-247">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="a0f9c-248">Assicurarsi di modificare il file prima di usarlo per creare il file `.nupkg` finale.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-248">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="a0f9c-249">Scegliere un identificatore univoco del pacchetto e impostare il numero di versione</span><span class="sxs-lookup"><span data-stu-id="a0f9c-249">Choose a unique package identifier and setting the version number</span></span>

<span data-ttu-id="a0f9c-250">L'identificatore del pacchetto (elemento `<id>`) e il numero di versione (elemento `<version>`) sono i due valori più importanti del manifesto perché identificano in modo univoco il codice esatto contenuto nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-250">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="a0f9c-251">**Procedure consigliate per l'identificatore del pacchetto:**</span><span class="sxs-lookup"><span data-stu-id="a0f9c-251">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="a0f9c-252">**Univocità**: l'identificatore deve essere univoco in nuget.org o in qualsiasi raccolta che ospita il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-252">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="a0f9c-253">Prima di scegliere un identificatore, eseguire una ricerca nella raccolta applicabile per controllare se il nome è già in uso.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-253">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="a0f9c-254">Per evitare conflitti, è consigliabile usare il nome della società come prima parte dell'identificatore, ad esempio `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-254">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="a0f9c-255">**Nomi simili a spazi dei nomi**: seguono un modello simile a quello degli spazi dei nomi in .NET, usando la notazione del punto invece dei trattini.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-255">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="a0f9c-256">Usare, ad esempio, `Contoso.Utility.UsefulStuff` invece di `Contoso-Utility-UsefulStuff` o `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-256">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="a0f9c-257">Per gli utenti è anche utile che l'identificatore del pacchetto corrisponda agli spazi dei nomi usati nel codice.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-257">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="a0f9c-258">**Pacchetti di esempio**: se si produce un pacchetto di codice di esempio che illustra come usare un altro pacchetto, collegare `.Sample` come suffisso all'identificatore, come in `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-258">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="a0f9c-259">Il pacchetto di esempio, ovviamente, avrà una dipendenza da un altro pacchetto. Quando si crea un pacchetto di esempio, usare il metodo della directory di lavoro basata sulle convenzioni descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-259">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="a0f9c-260">Nella cartella `content` inserire il codice di esempio in una cartella denominata `\Samples\<identifier>` come in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-260">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="a0f9c-261">**Procedure consigliate per la versione del pacchetto:**</span><span class="sxs-lookup"><span data-stu-id="a0f9c-261">**Best practices for the package version:**</span></span>

- <span data-ttu-id="a0f9c-262">In generale, impostare la versione del pacchetto in modo che corrisponda alla libreria, anche se non è strettamente necessario.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-262">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="a0f9c-263">È davvero semplicissimo quando si limita un pacchetto a un singolo assembly, come descritto precedentemente in [Scelta degli assembly per cui creare un pacchetto](#decide-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-263">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#decide-which-assemblies-to-package).</span></span> <span data-ttu-id="a0f9c-264">In generale, tenere presente che, durante la risoluzione delle dipendenze, di per sé NuGet gestisce le versioni dei pacchetti, non le versioni degli assembly.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-264">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="a0f9c-265">Quando si usa uno schema della versione non standard, tenere in considerazione le regole di controllo delle versioni di NuGet, come illustrato in [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-265">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../concepts/package-versioning.md).</span></span>

> <span data-ttu-id="a0f9c-266">Per informazioni sul controllo delle versioni, vedere anche la serie seguente di brevi post di blog:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-266">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - <span data-ttu-id="a0f9c-267">[Part 1: Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html) (Parte 1: Affrontare l'inferno delle DLL)</span><span class="sxs-lookup"><span data-stu-id="a0f9c-267">[Part 1: Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)</span></span>
> - <span data-ttu-id="a0f9c-268">[Part 2: The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html) (Parte 2: L'algoritmo principale)</span><span class="sxs-lookup"><span data-stu-id="a0f9c-268">[Part 2: The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)</span></span>
> - <span data-ttu-id="a0f9c-269">[Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html) (Parte 3: Unificazione tramite i reindirizzamenti di binding)</span><span class="sxs-lookup"><span data-stu-id="a0f9c-269">[Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)</span></span>

## <a name="add-a-readme-and-other-files"></a><span data-ttu-id="a0f9c-270">Aggiungere un file leggimi e altri file</span><span class="sxs-lookup"><span data-stu-id="a0f9c-270">Add a readme and other files</span></span>

<span data-ttu-id="a0f9c-271">Per specificare direttamente i file da includere nel pacchetto, usare il nodo `<files>` nel file `.nuspec`, che *segue* il tag `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-271">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> <span data-ttu-id="a0f9c-272">Quando si usa l'approccio della directory di lavoro basata sulle convenzioni, è possibile inserire il file readme.txt nella radice del pacchetto e gli altri contenuti nella cartella `content`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-272">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="a0f9c-273">Non sono necessari elementi `<file>` nel manifesto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-273">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="a0f9c-274">Quando si include un file denominato `readme.txt` nella radice del pacchetto, Visual Studio visualizza i contenuti del file come testo normale subito dopo avere installato direttamente il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-274">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="a0f9c-275">I file leggimi non vengono visualizzati per i pacchetti installati come dipendenze.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-275">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="a0f9c-276">Ecco ad esempio come viene visualizzato il file leggimi per il pacchetto HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-276">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Visualizzazione di un file leggimi per un pacchetto NuGet durante l'installazione](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="a0f9c-278">Se si include un nodo `<files>` vuoto nel file `.nuspec`, NuGet non include nel pacchetto altri contenuti diversi dal contenuto della cartella `lib`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-278">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="include-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="a0f9c-279">Includere proprietà e destinazioni MSBuild in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="a0f9c-279">Include MSBuild props and targets in a package</span></span>

<span data-ttu-id="a0f9c-280">In alcuni casi, potrebbe essere necessario aggiungere destinazioni o proprietà di compilazione personalizzata nei progetti che utilizzano il pacchetto, ad esempio l'esecuzione di uno strumento o processo personalizzato durante la compilazione.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-280">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="a0f9c-281">A tale scopo, inserire i file nel formato `<package_id>.targets` o `<package_id>.props` (ad esempio `Contoso.Utility.UsefulStuff.targets`) nella cartella `\build` del progetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-281">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="a0f9c-282">I file nella cartella radice `\build` sono considerati adatti a tutti i framework di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-282">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="a0f9c-283">Per indicare file specifici del framework, inserirli prima nelle sottocartelle appropriate, come di seguito:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-283">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="a0f9c-284">Nel file `.nuspec` assicurarsi quindi di fare riferimento a questi file nel nodo `<files>`:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-284">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

<span data-ttu-id="a0f9c-285">La possibilità di includere file props e targets di MSBuild in un pacchetto è stata [introdotta con NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), pertanto è consigliabile aggiungere l'attributo `minClientVersion="2.5"` all'elemento `metadata` per indicare la versione client NuGet minima richiesta per utilizzare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-285">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="a0f9c-286">Quando installa un pacchetto con i file `\build`, NuGet aggiunge elementi `<Import>` di MSBuild nel file di progetto che puntano ai file `.targets` e `.props`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-286">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="a0f9c-287">(`.props` viene aggiunto all'inizio del file di progetto;  `.targets` viene aggiunto in basso. Viene aggiunto un elemento `<Import>` MSBuild condizionale separato per ogni Framework di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-287">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="a0f9c-288">I file `.props` e `.targets` di MSBuild per l'assegnazione di più framework di destinazione possono essere posizionati nella cartella `\buildMultiTargeting`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-288">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildMultiTargeting` folder.</span></span> <span data-ttu-id="a0f9c-289">Durante l'installazione del pacchetto, NuGet aggiunge elementi `<Import>` corrispondenti al file di progetto, a condizione che il framework di destinazione non sia impostato (la proprietà MSBuild `$(TargetFramework)` deve essere vuota).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-289">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="a0f9c-290">Con NuGet 3.x, le destinazioni non vengono aggiunte al progetto, ma vengono rese disponibili tramite `{projectName}.nuget.g.targets` e `{projectName}.nuget.g.props`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-290">With NuGet 3.x, targets are not added to the project but are instead made available through `{projectName}.nuget.g.targets` and `{projectName}.nuget.g.props`.</span></span>

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="a0f9c-291">Eseguire nuget pack per generare il file con estensione nupkg</span><span class="sxs-lookup"><span data-stu-id="a0f9c-291">Run nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="a0f9c-292">Quando si usa un assembly o la directory di lavoro basata sulle convenzioni, creare un pacchetto eseguendo `nuget pack` con il file `.nuspec`, sostituendo `<project-name>` con il nome file specifico:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-292">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="a0f9c-293">Quando si usa un progetto di Visual Studio, eseguire `nuget pack` con il file di progetto, che carica automaticamente il file `.nuspec` del progetto e sostituisce il token usando i valori del file di progetto:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-293">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="a0f9c-294">L'uso diretto del file di progetto è necessario per la sostituzione dei token perché il progetto è l'origine dei valori dei token.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-294">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="a0f9c-295">La sostituzione dei token non avviene se si usa `nuget pack` con un file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-295">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="a0f9c-296">In tutti i casi, `nuget pack` esclude le cartelle che iniziano con un punto, ad esempio `.git` o `.hg`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-296">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="a0f9c-297">NuGet indica se sono presenti errori nel file `.nuspec` che richiedono una correzione, ad esempio se si dimentica di modificare i valori dei segnaposto nel manifesto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-297">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="a0f9c-298">Dopo la corretta esecuzione di `nuget pack`, è disponibile un file `.nupkg` che è possibile pubblicare in una raccolta appropriata, come illustrato in [Pubblicazione di un pacchetto](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-298">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="a0f9c-299">Per esaminare un pacchetto dopo averlo creato, è possibile aprirlo nello strumento [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer),</span><span class="sxs-lookup"><span data-stu-id="a0f9c-299">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="a0f9c-300">che offre una visualizzazione grafica dei contenuti del pacchetto e del manifesto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-300">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="a0f9c-301">È anche possibile rinominare il file `.nupkg` risultante in un file `.zip` ed esplorarne il contenuto direttamente.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-301">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="a0f9c-302">Opzioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a0f9c-302">Additional options</span></span>

<span data-ttu-id="a0f9c-303">Tra le altre funzionalità, è possibile usare diverse opzioni della riga di comando con `nuget pack` per escludere i file, eseguire l'override del numero di versione nel manifesto e modificare la cartella di output.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-303">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="a0f9c-304">Per un elenco completo, vedere le [informazioni di riferimento sul comando pack](../reference/cli-reference/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-304">For a complete list, refer to the [pack command reference](../reference/cli-reference/cli-ref-pack.md).</span></span>

<span data-ttu-id="a0f9c-305">Le seguenti sono alcune opzioni comuni ai progetti di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-305">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="a0f9c-306">**Progetti di riferimento**: se il progetto fa riferimento ad altri progetti, è possibile aggiungere i progetti a cui si fa riferimento come parte del pacchetto o come dipendenze, usando l'opzione `-IncludeReferencedProjects`:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-306">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="a0f9c-307">Questo processo di inclusione è ricorsivo, quindi se `MyProject.csproj` fa riferimento ai progetti B e C e tali progetti fanno riferimento a D, E e F, i file di B, C, D, E e F vengono inclusi nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-307">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="a0f9c-308">Se un progetto a cui si fa riferimento include un proprio file `.nuspec`, NuGet aggiunge invece tale progetto a cui si fa riferimento come dipendenza.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-308">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="a0f9c-309">È necessario creare un pacchetto per il progetto e pubblicarlo separatamente.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-309">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="a0f9c-310">**Configurazione della build**: per impostazione predefinita, NuGet usa la configurazione della build predefinita impostata nel file di progetto, in genere *Debug*.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-310">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="a0f9c-311">Per creare un pacchetto per i file da una configurazione della build differente, ad esempio *Release*, usare l'opzione `-properties` con la configurazione:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-311">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="a0f9c-312">**Simboli**: per includere i simboli che consentono agli utenti di eseguire il codice del pacchetto un'istruzione alla volta nel debugger, usare l'opzione `-Symbols`:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-312">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a><span data-ttu-id="a0f9c-313">Testare l'installazione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="a0f9c-313">Test package installation</span></span>

<span data-ttu-id="a0f9c-314">Prima di pubblicare un pacchetto, in genere si preferisce testarne il processo di installazione in un progetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-314">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="a0f9c-315">I test assicurano che i file necessari vengano inseriti nei percorsi corretti all'interno del progetto.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-315">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="a0f9c-316">È possibile testare manualmente le installazioni in Visual Studio o dalla riga di comando seguendo i normali [passaggi di installazione del pacchetto](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-316">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

<span data-ttu-id="a0f9c-317">Per i test automatizzati, il processo di base è il seguente:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-317">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="a0f9c-318">Copiare il file `.nupkg` in una cartella locale.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-318">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="a0f9c-319">Aggiungere la cartella alle origini del pacchetto usando il comando `nuget sources add -name <name> -source <path>`. Vedere [nuget sources](../reference/cli-reference/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-319">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../reference/cli-reference/cli-ref-sources.md)).</span></span> <span data-ttu-id="a0f9c-320">Si noti che è necessario impostare l'origine locale solo una volta in ogni computer.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-320">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="a0f9c-321">Installare il pacchetto da tale origine usando `nuget install <packageID> -source <name>` dove `<name>` corrisponde al nome dell'origine specificata in `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-321">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="a0f9c-322">Specificando l'origine, il pacchetto viene con certezza installato solo da tale origine.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-322">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="a0f9c-323">Esaminare il file system per controllare che i file siano installati correttamente.</span><span class="sxs-lookup"><span data-stu-id="a0f9c-323">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0f9c-324">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a0f9c-324">Next Steps</span></span>

<span data-ttu-id="a0f9c-325">Dopo aver creato un pacchetto, ovvero un file `.nupkg`, è possibile pubblicarlo nella raccolta di propria scelta, come descritto in [Pubblicazione di un pacchetto](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="a0f9c-325">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="a0f9c-326">Potrebbe anche essere necessario estendere le funzionalità del pacchetto o supportare altri scenari, come descritto negli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-326">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="a0f9c-327">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="a0f9c-327">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="a0f9c-328">Supporto di più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="a0f9c-328">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="a0f9c-329">Trasformazioni di file di origine e di configurazione</span><span class="sxs-lookup"><span data-stu-id="a0f9c-329">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="a0f9c-330">Localizzazione</span><span class="sxs-lookup"><span data-stu-id="a0f9c-330">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="a0f9c-331">Versioni non definitive</span><span class="sxs-lookup"><span data-stu-id="a0f9c-331">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="a0f9c-332">Impostare il tipo di pacchetto</span><span class="sxs-lookup"><span data-stu-id="a0f9c-332">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="a0f9c-333">Creare pacchetti con assembly di interoperabilità COM</span><span class="sxs-lookup"><span data-stu-id="a0f9c-333">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="a0f9c-334">Sono infine disponibili altri tipi di pacchetti da tenere presenti:</span><span class="sxs-lookup"><span data-stu-id="a0f9c-334">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="a0f9c-335">Pacchetti nativi</span><span class="sxs-lookup"><span data-stu-id="a0f9c-335">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="a0f9c-336">Pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="a0f9c-336">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
