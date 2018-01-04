---
title: Come creare un pacchetto NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 456797cb-e3e4-4b88-9b01-8b5153cee802
description: Guida dettagliata al processo di progettazione e creazione di un pacchetto NuGet, incluse le principali decisioni critiche, ad esempio quelle relative ai file e al controllo delle versioni.
keywords: creazione di un pacchetto NuGet, creazione di un pacchetto, manifesto nuspec, convenzioni dei pacchetti NuGet, versione del pacchetto NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e7a2c4d02afb2387161c22fe5bd443eb0991ea8c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="55689-104">Creazione di pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="55689-104">Creating NuGet packages</span></span>

<span data-ttu-id="55689-105">Indipendentemente dalle operazioni eseguite dal pacchetto o dal tipo di codice contenuto, `nuget.exe` viene usato per rendere disponibili tali funzionalità in un componente condivisibile e utilizzabile da altri sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="55689-105">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="55689-106">Per installare `nuget.exe`, vedere [Installare l'interfaccia della riga di comando di NuGet](../guides/Install-NuGet.md#nuget-cli).</span><span class="sxs-lookup"><span data-stu-id="55689-106">To install `nuget.exe`, see [Install NuGet CLI](../guides/Install-NuGet.md#nuget-cli).</span></span> <span data-ttu-id="55689-107">Si noti che `nuget.exe` non è incluso automaticamente in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="55689-107">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="55689-108">Da un punto di vista tecnico, un pacchetto NuGet è solo un file ZIP rinominato con l'estensione `.nupkg` e i cui contenuti rispettano determinate convenzioni.</span><span class="sxs-lookup"><span data-stu-id="55689-108">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="55689-109">Questo argomento descrive il processo dettagliato di creazione di un pacchetto che soddisfa tali convenzioni.</span><span class="sxs-lookup"><span data-stu-id="55689-109">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="55689-110">Per una procedura dettagliata specifica, vedere la [guida introduttiva Creare e pubblicare un pacchetto](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="55689-110">For a focused walkthrough, refer to [Create and Publish a Package Quickstart](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="55689-111">La creazione di un pacchetto inizia con il codice compilato (assembly), i simboli e/o altri file che si vuole distribuire come pacchetto. Vedere [Panoramica e flusso di lavoro](Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="55689-111">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](Overview-and-Workflow.md)).</span></span> <span data-ttu-id="55689-112">Questo processo è indipendente dalla compilazione o comunque dalla generazione dei file inseriti nel pacchetto, anche se è possibile usare le informazioni contenute in un file di progetto per mantenere sincronizzati i pacchetti e gli assembly compilati.</span><span class="sxs-lookup"><span data-stu-id="55689-112">This process is independent from compiling or otherwise generating the files that go into the package, although you can use draw from information in a project file to keep the compiled assemblines and packages in sync.</span></span>

<span data-ttu-id="55689-113">Contenuto dell'argomento:</span><span class="sxs-lookup"><span data-stu-id="55689-113">In this topic:</span></span>

- [<span data-ttu-id="55689-114">Scelta degli assembly per cui creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="55689-114">Deciding which assemblies to package</span></span>](#deciding-which-assemblies-to-package)
- [<span data-ttu-id="55689-115">Ruolo e struttura del file `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="55689-115">The role and structure of the `.nuspec` file</span></span>](#the-role-and-structure-of-the-nuspec-file)
- <span data-ttu-id="55689-116">[Creazione del file `.nuspec`](#creating-the-nuspec-file) da:</span><span class="sxs-lookup"><span data-stu-id="55689-116">[Creating the `.nuspec` file](#creating-the-nuspec-file) from:</span></span>
    - [<span data-ttu-id="55689-117">Directory di lavoro basata sulle convenzioni</span><span class="sxs-lookup"><span data-stu-id="55689-117">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
    - [<span data-ttu-id="55689-118">DLL dell'assembly</span><span class="sxs-lookup"><span data-stu-id="55689-118">An assembly DLL</span></span>](#from-an-assembly-dll)
    - [<span data-ttu-id="55689-119">Progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="55689-119">A Visual Studio project</span></span>](#from-a-visual-studio-project)
    - [<span data-ttu-id="55689-120">Nuovo file con valori predefiniti</span><span class="sxs-lookup"><span data-stu-id="55689-120">New file with default values</span></span>](#new-file-with-default-values)    
- [<span data-ttu-id="55689-121">Scelta di un identificatore univoco del pacchetto e impostazione del numero di versione</span><span class="sxs-lookup"><span data-stu-id="55689-121">Choosing a unique package identifier and setting the version number</span></span>](#choosing-a-unique-package-identifier-and-setting-the-version-number)
- <span data-ttu-id="55689-122">[Impostazione di un tipo di pacchetto](#setting-a-package-type) (NuGet 3.5 e versioni successive)</span><span class="sxs-lookup"><span data-stu-id="55689-122">[Setting a package type](#setting-a-package-type) (NuGet 3.5 and later)</span></span>
- [<span data-ttu-id="55689-123">Aggiunta di un file leggimi e di altri file</span><span class="sxs-lookup"><span data-stu-id="55689-123">Adding a readme and other files</span></span>](#adding-a-readme-and-other-files)
- [<span data-ttu-id="55689-124">Inclusione di proprietà e destinazioni MSBuild in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="55689-124">Including MSBuild props and targets in a package</span></span>](#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="55689-125">Creazione di pacchetti contenenti assembly di interoperabilità COM</span><span class="sxs-lookup"><span data-stu-id="55689-125">Authoring packages that contain COM interop assemblies</span></span>](#authoring-packages-with-com-interop-assemblies)
- [<span data-ttu-id="55689-126">Esecuzione di nuget pack per generare il file con estensione nupkg</span><span class="sxs-lookup"><span data-stu-id="55689-126">Running nuget pack to generate the .nupkg file</span></span>](#running-nuget-pack-to-generate-the-nupkg-file)

<span data-ttu-id="55689-127">Dopo avere eseguito questi passaggi fondamentali, sarà possibile incorporare diverse altre funzionalità, come illustrato in questa documentazione.</span><span class="sxs-lookup"><span data-stu-id="55689-127">After these core steps, you can incorporate a variety of other features as described elsewhere in this documentation.</span></span> <span data-ttu-id="55689-128">Vedere [Passaggi successivi](#next-steps) più avanti.</span><span class="sxs-lookup"><span data-stu-id="55689-128">See [Next steps](#next-steps) below.</span></span>

> [!Note]
> <span data-ttu-id="55689-129">Questo argomento si applica a tipi di progetto diversi dai progetti .NET Core, che usano Visual Studio 2017 e NuGet 4.0+.</span><span class="sxs-lookup"><span data-stu-id="55689-129">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="55689-130">In tali progetti .NET Core NuGet usa direttamente le informazioni contenute nel file `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="55689-130">In those .NET Core projects, NuGet uses information in the `.csproj` file directly.</span></span> <span data-ttu-id="55689-131">Per informazioni dettagliate, vedere [Creare pacchetti .NET Standard con Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) e [Pack e restore di NuGet come destinazioni MSBuild](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="55689-131">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="55689-132">Scelta degli assembly per cui creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="55689-132">Deciding which assemblies to package</span></span>

<span data-ttu-id="55689-133">La maggior parte dei pacchetti per utilizzo generico contiene uno o più assembly che gli altri sviluppatori possono usare nei propri progetti.</span><span class="sxs-lookup"><span data-stu-id="55689-133">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="55689-134">In generale, l'ideale è avere un assembly per ogni pacchetto NuGet, purché ogni assembly abbia una propria utilità.</span><span class="sxs-lookup"><span data-stu-id="55689-134">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="55689-135">Se ad esempio è presente un file `Utilities.dll` che dipende da `Parser.dll` e `Parser.dll` è utile di per sé, creare un pacchetto per ognuno.</span><span class="sxs-lookup"><span data-stu-id="55689-135">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="55689-136">In questo modo gli sviluppatori possono usare `Parser.dll` indipendentemente da `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="55689-136">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="55689-137">Se la libreria è costituita da più assembly che non hanno una propria utilità, è consigliabile combinarli in un solo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="55689-137">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="55689-138">Usando l'esempio precedente, se `Parser.dll` contiene codice che viene usato solo da `Utilities.dll`, è consigliabile tenere `Parser.dll` nello stesso pacchetto.</span><span class="sxs-lookup"><span data-stu-id="55689-138">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>
    - <span data-ttu-id="55689-139">Analogamente, se `Utilities.dll` dipende da `Utilities.resources.dll` e quest'ultimo non è utile di per sé, inserirli entrambi nello stesso pacchetto.</span><span class="sxs-lookup"><span data-stu-id="55689-139">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="55689-140">Le risorse sono di fatto un caso particolare.</span><span class="sxs-lookup"><span data-stu-id="55689-140">Resources are, in fact, a special case.</span></span> <span data-ttu-id="55689-141">Quando un pacchetto viene installato in un progetto, NuGet aggiunge automaticamente alle DLL del pacchetto i riferimenti agli assembly, *escludendo* quelli denominati `.resources.dll` perché si presuppone che siano assembly satellite localizzati. Vedere [Creazione di pacchetti localizzati](creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="55689-141">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="55689-142">Per questo motivo, evitare di usare `.resources.dll` per i file che contengono invece codice essenziale per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="55689-142">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="55689-143">Se la libreria contiene assembly di interoperabilità COM, seguire le linee guida aggiuntive in [Creazione di pacchetti con assembly di interoperabilità COM](#authoring-packages-with-com-interop-assemblies).</span><span class="sxs-lookup"><span data-stu-id="55689-143">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="55689-144">Ruolo e struttura del file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="55689-144">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="55689-145">Dopo avere deciso per quali file si vuole creare un pacchetto, il passaggio successivo prevede la creazione di un manifesto del pacchetto in un file XML `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="55689-145">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="55689-146">Il manifesto:</span><span class="sxs-lookup"><span data-stu-id="55689-146">The manifest:</span></span>

1. <span data-ttu-id="55689-147">Descrive i contenuti del pacchetto e viene incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="55689-147">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="55689-148">Gestisce la creazione del pacchetto e indica a NuGet come installare il pacchetto in un progetto.</span><span class="sxs-lookup"><span data-stu-id="55689-148">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="55689-149">Il manifesto, ad esempio, identifica le altre dipendenze del pacchetto in modo che NuGet possa installare anche tali dipendenze quando viene installato il pacchetto principale.</span><span class="sxs-lookup"><span data-stu-id="55689-149">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="55689-150">Contiene le proprietà sia obbligatorie che facoltative, come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="55689-150">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="55689-151">Per informazioni dettagliate, incluse le altre proprietà non citate qui, vedere [Informazioni di riferimento sul file .nuspec](../schema/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="55689-151">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../schema/nuspec.md).</span></span>

<span data-ttu-id="55689-152">Proprietà obbligatorie:</span><span class="sxs-lookup"><span data-stu-id="55689-152">Required properties:</span></span>

- <span data-ttu-id="55689-153">Identificatore del pacchetto, che deve essere univoco nella raccolta che ospita il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="55689-153">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="55689-154">Numero di versione specifico nel formato *Major.Minor.Patch[-Suffix]* dove *-Suffix* identifica le [versioni preliminari](Prerelease-Packages.md)</span><span class="sxs-lookup"><span data-stu-id="55689-154">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](Prerelease-Packages.md)</span></span>
- <span data-ttu-id="55689-155">Titolo del pacchetto come deve essere visualizzato nell'host (ad esempio, nuget.org)</span><span class="sxs-lookup"><span data-stu-id="55689-155">The package title as it should appears on the host (like nuget.org)</span></span>
- <span data-ttu-id="55689-156">Informazioni sull'autore e sul proprietario.</span><span class="sxs-lookup"><span data-stu-id="55689-156">Author and owner information.</span></span>
- <span data-ttu-id="55689-157">Descrizione estesa del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="55689-157">A long description of the package.</span></span>

<span data-ttu-id="55689-158">Proprietà facoltative comuni:</span><span class="sxs-lookup"><span data-stu-id="55689-158">Common optional properties:</span></span>

- <span data-ttu-id="55689-159">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="55689-159">Release notes</span></span>
- <span data-ttu-id="55689-160">Informazioni sul copyright</span><span class="sxs-lookup"><span data-stu-id="55689-160">Copyright information</span></span>
- <span data-ttu-id="55689-161">Breve descrizione dell'[interfaccia utente di Gestione pacchetti in Visual Studio](../Tools/Package-Manager-UI.md)</span><span class="sxs-lookup"><span data-stu-id="55689-161">A short description for the [Package Manager UI in Visual Studio](../Tools/Package-Manager-UI.md)</span></span>
- <span data-ttu-id="55689-162">ID impostazioni locali</span><span class="sxs-lookup"><span data-stu-id="55689-162">A locale ID</span></span>
- <span data-ttu-id="55689-163">URL della home page e della licenza</span><span class="sxs-lookup"><span data-stu-id="55689-163">Home page and license URLs</span></span>
- <span data-ttu-id="55689-164">URL dell'icona</span><span class="sxs-lookup"><span data-stu-id="55689-164">An icon URL</span></span>
- <span data-ttu-id="55689-165">Elenchi di dipendenze e riferimenti</span><span class="sxs-lookup"><span data-stu-id="55689-165">Lists of dependencies and references</span></span>
- <span data-ttu-id="55689-166">Tag di supporto per le ricerche nella raccolta</span><span class="sxs-lookup"><span data-stu-id="55689-166">Tags that assist in gallery searches</span></span>

<span data-ttu-id="55689-167">Di seguito è riportato un file `.nuspec` tipico (ma fittizio), con commenti che descrivono le proprietà:</span><span class="sxs-lookup"><span data-stu-id="55689-167">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

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

    <!-- Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  -->
    <owners>dejanatc, rjdey</owners>

    <!-- License and project URLs provide links for the gallery -->
    <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
    <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

    <!-- The icon is used in Visual Studio's package manager UI -->
    <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

    <!-- If true, this value prompts the user to accept the license when
            installing the package. -->
    <requireLicenseAcceptance>false</requireLicenseAcceptance>

    <!-- Any details about this particular release -->
    <releaseNotes>Bug fixes and performance improvements</releaseNotes>

    <!-- The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. -->
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

<span data-ttu-id="55689-168">Per informazioni dettagliate sulla dichiarazione delle dipendenze e sulla specifica dei numeri di versione, vedere [Controllo delle versioni dei pacchetti](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="55689-168">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="55689-169">È anche possibile esporre gli asset dalle dipendenze direttamente nel pacchetto usando gli attributi `include` ed `exclude` nell'elemento `dependency`.</span><span class="sxs-lookup"><span data-stu-id="55689-169">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="55689-170">Vedere la [sezione Dipendenze delle informazioni di riferimento sul file .nuspec](../Schema/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="55689-170">See [.nuspec Reference - Dependencies](../Schema/nuspec.md#dependencies).</span></span>

<span data-ttu-id="55689-171">Poiché il manifesto è incluso nel pacchetto creato, per trovare altri esempi, esaminare i pacchetti esistenti.</span><span class="sxs-lookup"><span data-stu-id="55689-171">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="55689-172">Una valida fonte è la cache globale dei pacchetti sul computer, la posizione della quale viene restituita dal comando seguente:</span><span class="sxs-lookup"><span data-stu-id="55689-172">A good source is the global package cache on your machine, the location of which is returned by the following command:</span></span>

```
nuget locals -list global-packages
```

<span data-ttu-id="55689-173">Andare a qualsiasi cartella *pacchetto\versione*, copiare il file `.nupkg` in un file `.zip`, quindi aprire il file `.zip` ed esaminare il file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="55689-173">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="55689-174">Quando si crea un file `.nuspec` da un progetto di Visual Studio, il manifesto contiene token che devono essere sostituiti con le informazioni provenienti dal progetto quando il pacchetto viene compilato.</span><span class="sxs-lookup"><span data-stu-id="55689-174">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are be replaced with information from the project when the package is built.</span></span> <span data-ttu-id="55689-175">Vedere [Creazione del file con estensione nuspec da un progetto di Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="55689-175">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="55689-176">Creazione del file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="55689-176">Creating the .nuspec file</span></span>

<span data-ttu-id="55689-177">La creazione di un manifesto completo inizia in genere con un file `.nuspec` di base generato con uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="55689-177">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="55689-178">Directory di lavoro basata sulle convenzioni</span><span class="sxs-lookup"><span data-stu-id="55689-178">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="55689-179">DLL dell'assembly</span><span class="sxs-lookup"><span data-stu-id="55689-179">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="55689-180">Progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="55689-180">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="55689-181">Nuovo file con valori predefiniti</span><span class="sxs-lookup"><span data-stu-id="55689-181">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="55689-182">Si modifica quindi il file manualmente in modo che descriva il contenuto esatto che dovrà essere incluso nel pacchetto finale.</span><span class="sxs-lookup"><span data-stu-id="55689-182">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="55689-183">I file `.nuspec` generati contengono segnaposto che devono essere modificati prima di creare il pacchetto con il comando `nuget pack`,</span><span class="sxs-lookup"><span data-stu-id="55689-183">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="55689-184">che ha esito negativo se il file `.nuspec` contiene segnaposto.</span><span class="sxs-lookup"><span data-stu-id="55689-184">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="55689-185">Da una directory di lavoro basata sulle convenzioni</span><span class="sxs-lookup"><span data-stu-id="55689-185">From a convention-based working directory</span></span>

<span data-ttu-id="55689-186">Poiché un pacchetto NuGet è solo un file ZIP rinominato con l'estensione `.nupkg`, spesso è più semplice creare la struttura di cartelle desiderata nel file system, quindi creare il file `.nuspec` direttamente da tale struttura.</span><span class="sxs-lookup"><span data-stu-id="55689-186">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, its often easiest to create the folder structure you want on the file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="55689-187">Il comando `nuget pack` aggiunge quindi automaticamente tutti i file in tale struttura di cartelle, escluse le cartelle che iniziano con `.`, per poter mantenere i file privati nella stessa struttura.</span><span class="sxs-lookup"><span data-stu-id="55689-187">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you keep private files in the same structure).</span></span>

<span data-ttu-id="55689-188">Il vantaggio di questo approccio è che non è necessario specificare nel manifesto i file che si vuole includere nel pacchetto, come illustrato più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="55689-188">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="55689-189">È sufficiente fare in modo che il processo di compilazione generi l'esatta struttura di cartelle da inserire nel pacchetto, per poter facilmente includere altri file che altrimenti potrebbero non fare parte di un progetto:</span><span class="sxs-lookup"><span data-stu-id="55689-189">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="55689-190">Contenuto e codice sorgente da inserire nel progetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="55689-190">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="55689-191">Script di PowerShell. I pacchetti usati in NuGet 2.x possono includere anche script di installazione, non supportati in NuGet 3.x e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="55689-191">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="55689-192">Trasformazioni della configurazione esistente e dei file del codice sorgente di un progetto.</span><span class="sxs-lookup"><span data-stu-id="55689-192">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="55689-193">Le convenzioni delle cartelle sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="55689-193">The folder conventions are as follows:</span></span>

| <span data-ttu-id="55689-194">Cartella</span><span class="sxs-lookup"><span data-stu-id="55689-194">Folder</span></span> | <span data-ttu-id="55689-195">Descrizione</span><span class="sxs-lookup"><span data-stu-id="55689-195">Description</span></span> | <span data-ttu-id="55689-196">Azione durante l'installazione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="55689-196">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="55689-197">(radice)</span><span class="sxs-lookup"><span data-stu-id="55689-197">(root)</span></span> | <span data-ttu-id="55689-198">Percorso del file readme.txt</span><span class="sxs-lookup"><span data-stu-id="55689-198">Location for readme.txt</span></span> | <span data-ttu-id="55689-199">Visual Studio visualizza un file readme.txt nella radice del pacchetto quando il pacchetto viene installato.</span><span class="sxs-lookup"><span data-stu-id="55689-199">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="55689-200">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="55689-200">lib/{tfm}</span></span> | <span data-ttu-id="55689-201">File di assembly (`.dll`), di documentazione (`.xml`) e di simboli (`.pdb`) per il moniker del framework di destinazione (TFM, Target Framework Moniker) specificato</span><span class="sxs-lookup"><span data-stu-id="55689-201">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="55689-202">Gli assembly vengono aggiunti come riferimenti. `.xml` e `.pdb` vengono copiati nelle cartelle di progetto.</span><span class="sxs-lookup"><span data-stu-id="55689-202">Assemblies are added as references; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="55689-203">Per la creazione di sottocartelle specifiche del framework di destinazione, vedere [Supporto di più framework di destinazione](Supporting-Multiple-Target-Frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="55689-203">See [Supporting multiple target frameworks](Supporting-Multiple-Target-Frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="55689-204">runtimes</span><span class="sxs-lookup"><span data-stu-id="55689-204">runtimes</span></span> | <span data-ttu-id="55689-205">File di assembly (`.dll`), di simboli (`.pdb`) e di risorse native (`.pri`) specifici dell'architettura</span><span class="sxs-lookup"><span data-stu-id="55689-205">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="55689-206">Gli assembly vengono aggiunti come riferimenti. Gli altri file vengono copiati nelle cartelle di progetto.</span><span class="sxs-lookup"><span data-stu-id="55689-206">Assemblies are added as references; other files are copied into project folders.</span></span> <span data-ttu-id="55689-207">Vedere [Supporto di più framework di destinazione](Supporting-Multiple-Target-Frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="55689-207">See [Supporting multiple target frameworks](Supporting-Multiple-Target-Frameworks.md).</span></span> |
| <span data-ttu-id="55689-208">contenuto</span><span class="sxs-lookup"><span data-stu-id="55689-208">content</span></span> | <span data-ttu-id="55689-209">File arbitrari</span><span class="sxs-lookup"><span data-stu-id="55689-209">Arbitrary files</span></span> | <span data-ttu-id="55689-210">I contenuti vengono copiati nella radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="55689-210">Contents are copied to the project root.</span></span> <span data-ttu-id="55689-211">La cartella **content** può essere considerata come la radice dell'applicazione di destinazione che in definitiva utilizza il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="55689-211">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="55689-212">Per fare in modo che il pacchetto aggiunga un'immagine nella cartella */images* dell'applicazione, inserirla nella cartella *content/images* del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="55689-212">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="55689-213">build</span><span class="sxs-lookup"><span data-stu-id="55689-213">build</span></span> | <span data-ttu-id="55689-214">File `.targets` e `.props` MSBuild</span><span class="sxs-lookup"><span data-stu-id="55689-214">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="55689-215">Vengono automaticamente inseriti nel file di progetto (NuGet 2.x) o in `project.lock.json` (NuGet 3.x+).</span><span class="sxs-lookup"><span data-stu-id="55689-215">Automatically inserted into the project file (NuGet 2.x) or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="55689-216">tools</span><span class="sxs-lookup"><span data-stu-id="55689-216">tools</span></span> | <span data-ttu-id="55689-217">Script di PowerShell e programmi accessibili dalla console di Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="55689-217">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="55689-218">La cartella `tools` viene aggiunta alla variabile di ambiente `PATH` solo per la console di Gestione pacchetti, in particolare *non* alla variabile `PATH` impostata per MSBuild durante la compilazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="55689-218">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="55689-219">Poiché la struttura di cartelle può contenere un numero indeterminato di assembly per un numero indeterminato di framework di destinazione, questo metodo è necessario quando si creano pacchetti che supportano più framework</span><span class="sxs-lookup"><span data-stu-id="55689-219">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks</span></span> 

<span data-ttu-id="55689-220">In ogni caso, dopo avere creato la struttura di cartelle desiderata, eseguire il comando seguente in tale cartella per creare il file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="55689-220">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```
nuget spec
```

<span data-ttu-id="55689-221">Anche in questo caso, il file `.nuspec` generato non contiene riferimenti espliciti ai file nella struttura di cartelle.</span><span class="sxs-lookup"><span data-stu-id="55689-221">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="55689-222">NuGet include tutti i file automaticamente quando viene creato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="55689-222">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="55689-223">È tuttavia necessario modificare i valori dei segnaposto nelle altre parti del manifesto.</span><span class="sxs-lookup"><span data-stu-id="55689-223">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="55689-224">Da una DLL dell'assembly</span><span class="sxs-lookup"><span data-stu-id="55689-224">From an assembly DLL</span></span>

<span data-ttu-id="55689-225">Nel semplice caso della creazione di un pacchetto da un assembly, è possibile generare un file `.nuspec` dai metadati nell'assembly usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="55689-225">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```
nuget spec <assembly-name>.dll
```

<span data-ttu-id="55689-226">Usando questo formato, alcuni segnaposto nel manifesto vengono sostituiti con i valori specifici dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="55689-226">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="55689-227">La proprietà `<id>`, ad esempio, viene impostata sul nome dell'assembly e `<version>` viene impostata sulla versione dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="55689-227">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="55689-228">Le altre proprietà del manifesto non hanno tuttavia valori corrispondenti nell'assembly e perciò contengono ancora i segnaposto.</span><span class="sxs-lookup"><span data-stu-id="55689-228">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="55689-229">Da un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="55689-229">From a Visual Studio project</span></span>

<span data-ttu-id="55689-230">La creazione di un file `.nuspec` da un file `.csproj` o `.vbproj` è utile perché viene fatto automaticamente riferimento agli altri pacchetti che sono stati installati in tale progetto come a dipendenze.</span><span class="sxs-lookup"><span data-stu-id="55689-230">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="55689-231">È sufficiente usare il comando seguente nella stessa cartella del file di progetto:</span><span class="sxs-lookup"><span data-stu-id="55689-231">Simply use the following command in the same folder as the project file:</span></span>

```
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="55689-232">Il file `<project-name>.nuspec` risultante contiene *token* che in fase di creazione del pacchetto vengono sostituiti con i valori del progetto, inclusi i riferimenti agli altri pacchetti già installati.</span><span class="sxs-lookup"><span data-stu-id="55689-232">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="55689-233">Un token è delimitato dai simboli `$` su entrambi i lati della proprietà del progetto.</span><span class="sxs-lookup"><span data-stu-id="55689-233">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="55689-234">Ad esempio, il valore `<id>` in un manifesto generato in questo modo solitamente viene visualizzato come segue:</span><span class="sxs-lookup"><span data-stu-id="55689-234">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="55689-235">Questo token viene sostituito con il valore `AssemblyName` del file di progetto in fase di creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="55689-235">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="55689-236">Per il mapping esatto dei valori del progetto ai token di `.nuspec`, vedere le [informazioni di riferimento in Token di sostituzione](../schema/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="55689-236">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../schema/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="55689-237">I token evitano di dover aggiornare i valori fondamentali, ad esempio il numero di versione, nel file `.nuspec` quando si aggiorna il progetto.</span><span class="sxs-lookup"><span data-stu-id="55689-237">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="55689-238">È sempre possibile sostituire i token con valori letterali, se necessario.</span><span class="sxs-lookup"><span data-stu-id="55689-238">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="55689-239">Tenere presente che sono disponibili diverse altre opzioni di creazione del pacchetto quando si usa un progetto di Visual Studio, come illustrato più avanti in [Esecuzione di nuget pack per generare il file con estensione nupkg](#running-nuget-pack-to-generate-the-nupkg-file).</span><span class="sxs-lookup"><span data-stu-id="55689-239">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="55689-240">Pacchetti a livello di soluzione</span><span class="sxs-lookup"><span data-stu-id="55689-240">Solution-level packages</span></span>

<span data-ttu-id="55689-241">*Solo NuGet 2.x. Non disponibile in NuGet 3.0+.*</span><span class="sxs-lookup"><span data-stu-id="55689-241">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="55689-242">NuGet 2.x supportava la nozione di pacchetto a livello di soluzione che installa strumenti o comandi aggiuntivi per la console di Gestione pacchetti (contenuti della cartella `tools`), ma non aggiunge riferimenti, contenuto o personalizzazioni delle compilazioni ai progetti della soluzione.</span><span class="sxs-lookup"><span data-stu-id="55689-242">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="55689-243">Tali pacchetti non contengono file nelle cartelle `lib`, `content` o `build` dirette e nessuna dipendenza ha file nelle rispettive cartelle `lib`, `content` o `build`.</span><span class="sxs-lookup"><span data-stu-id="55689-243">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span> 

<span data-ttu-id="55689-244">NuGet tiene traccia dei pacchetti a livello di soluzione installati in un file `packages.config` nella cartella `.nuget`, invece che nel file `packages.config` del progetto.</span><span class="sxs-lookup"><span data-stu-id="55689-244">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="55689-245">Nuovo file con valori predefiniti</span><span class="sxs-lookup"><span data-stu-id="55689-245">New file with default values</span></span>

<span data-ttu-id="55689-246">Il comando seguente crea un manifesto predefinito con segnaposto, che assicura di iniziare con la struttura di file corretta:</span><span class="sxs-lookup"><span data-stu-id="55689-246">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```
nuget spec [<package-name>]
```

<span data-ttu-id="55689-247">Se si omette \<package-name\>, il file risultante è `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="55689-247">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="55689-248">Se come nome si specifica ad esempio `Contoso.Utility.UsefulStuff`, il file è `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="55689-248">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="55689-249">Il file `.nuspec` risultante contiene segnaposto per i valori come `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="55689-249">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="55689-250">Assicurarsi di modificare il file prima di usarlo per creare il file `.nupkg` finale.</span><span class="sxs-lookup"><span data-stu-id="55689-250">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="55689-251">Scelta di un identificatore univoco del pacchetto e impostazione del numero di versione</span><span class="sxs-lookup"><span data-stu-id="55689-251">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="55689-252">L'identificatore del pacchetto (elemento `<id>`) e il numero di versione (elemento `<version>`) sono i due valori più importanti del manifesto perché identificano in modo univoco il codice esatto contenuto nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="55689-252">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="55689-253">**Procedure consigliate per l'identificatore del pacchetto:**</span><span class="sxs-lookup"><span data-stu-id="55689-253">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="55689-254">**Univocità**: l'identificatore deve essere univoco in nuget.org o in qualsiasi raccolta che ospita il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="55689-254">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="55689-255">Prima di scegliere un identificatore, eseguire una ricerca nella raccolta applicabile per controllare se il nome è già in uso.</span><span class="sxs-lookup"><span data-stu-id="55689-255">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="55689-256">Per evitare conflitti, è consigliabile usare il nome della società come prima parte dell'identificatore, ad esempio `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="55689-256">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="55689-257">**Nomi simili a spazi dei nomi**: seguono un modello simile a quello degli spazi dei nomi in .NET, usando la notazione del punto invece dei trattini.</span><span class="sxs-lookup"><span data-stu-id="55689-257">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="55689-258">Usare, ad esempio, `Contoso.Utility.UsefulStuff` invece di `Contoso-Utility-UsefulStuff` o `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="55689-258">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="55689-259">Per gli utenti è anche utile che l'identificatore del pacchetto corrisponda agli spazi dei nomi usati nel codice.</span><span class="sxs-lookup"><span data-stu-id="55689-259">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="55689-260">**Pacchetti di esempio**: se si produce un pacchetto di codice di esempio che illustra come usare un altro pacchetto, collegare `.Sample` come suffisso all'identificatore, come in `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="55689-260">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="55689-261">Il pacchetto di esempio avrà naturalmente una dipendenza dall'altro pacchetto. Quando si crea un pacchetto di esempio, usare il metodo della directory di lavoro basata sulle convenzioni descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="55689-261">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="55689-262">Nella cartella `content` inserire il codice di esempio in una cartella denominata `\Samples\<identifier>` come in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="55689-262">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="55689-263">**Procedure consigliate per la versione del pacchetto:**</span><span class="sxs-lookup"><span data-stu-id="55689-263">**Best practices for the package version:**</span></span>

- <span data-ttu-id="55689-264">In generale, impostare la versione del pacchetto in modo che corrisponda alla libreria, anche se non è strettamente necessario.</span><span class="sxs-lookup"><span data-stu-id="55689-264">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="55689-265">È davvero semplicissimo quando si limita un pacchetto a un singolo assembly, come descritto precedentemente in [Scelta degli assembly per cui creare un pacchetto](#deciding-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="55689-265">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="55689-266">In generale, tenere presente che, durante la risoluzione delle dipendenze, di per sé NuGet gestisce le versioni dei pacchetti, non le versioni degli assembly.</span><span class="sxs-lookup"><span data-stu-id="55689-266">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="55689-267">Quando si usa uno schema della versione non standard, tenere in considerazione le regole di controllo delle versioni di NuGet, come illustrato in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="55689-267">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="55689-268">Per informazioni sul controllo delle versioni, vedere anche la serie seguente di brevi post di blog:</span><span class="sxs-lookup"><span data-stu-id="55689-268">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - <span data-ttu-id="55689-269">[Part 1: Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html) (Parte 1: Affrontare l'inferno delle DLL)</span><span class="sxs-lookup"><span data-stu-id="55689-269">[Part 1: Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)</span></span>
> - <span data-ttu-id="55689-270">[Part 2: The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html) (Parte 2: L'algoritmo principale)</span><span class="sxs-lookup"><span data-stu-id="55689-270">[Part 2: The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)</span></span>
> - <span data-ttu-id="55689-271">[Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html) (Parte 3: Unificazione tramite i reindirizzamenti di binding)</span><span class="sxs-lookup"><span data-stu-id="55689-271">[Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)</span></span>

## <a name="setting-a-package-type"></a><span data-ttu-id="55689-272">Impostazione di un tipo di pacchetto</span><span class="sxs-lookup"><span data-stu-id="55689-272">Setting a package type</span></span>

<span data-ttu-id="55689-273">Con NuGet 3.5+, i pacchetti possono essere contrassegnati con uno specifico *tipo di pacchetto* per indicarne l'uso previsto.</span><span class="sxs-lookup"><span data-stu-id="55689-273">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="55689-274">I pacchetti non contrassegnati con un tipo, inclusi tutti i pacchetti creati con versioni precedenti di NuGet, usano il tipo `Dependency` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="55689-274">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="55689-275">I pacchetti di tipo `Dependency` aggiungono asset in fase di compilazione o di esecuzione ad applicazioni e librerie e possono essere installati in qualsiasi tipo di progetto, presupponendo che siano compatibili.</span><span class="sxs-lookup"><span data-stu-id="55689-275">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="55689-276">I pacchetti di tipo `DotnetCliTool` sono estensioni dell'[interfaccia della riga di comando di .NET](https://docs.microsoft.com/dotnet/articles/core/tools/index) e vengono richiamati dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="55689-276">`DotnetCliTool` type packages are extensions to the [.NET CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="55689-277">Tali pacchetti possono essere installati solo nei progetti .NET Core e non hanno effetto sulle operazioni di ripristino.</span><span class="sxs-lookup"><span data-stu-id="55689-277">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="55689-278">Per altre informazioni su queste estensioni in base al progetto, vedere la documentazione sull'[estendibilità in .NET Core](https://docs.microsoft.com/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).</span><span class="sxs-lookup"><span data-stu-id="55689-278">More details about these per-project extensions are available in the  [.NET Core extensibility](https://docs.microsoft.com/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

    <span data-ttu-id="55689-279">Quando viene installato un pacchetto DotnetCliTool, Visual Studio inserisce il pacchetto nel nodo `tools` di `project.json` invece che nel nodo `dependencies`.</span><span class="sxs-lookup"><span data-stu-id="55689-279">When a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

- <span data-ttu-id="55689-280">I pacchetti di tipo personalizzato usano un identificatore di tipo arbitrario che è conforme alle stesse regole di formato degli ID dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="55689-280">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="55689-281">I tipi diversi da `Dependency` e `DotnetCliTool`, tuttavia, non vengono riconosciuti da Gestione pacchetti NuGet in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="55689-281">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="55689-282">I tipi di pacchetti vengono impostati nel file `.nuspec` o in `project.json`.</span><span class="sxs-lookup"><span data-stu-id="55689-282">Package types are set either in the `.nuspec` file or in `project.json`.</span></span> <span data-ttu-id="55689-283">In entrambi i casi, per la compatibilità con le versioni precedenti è meglio *non* impostare in modo esplicito il tipo `Dependency` e basarsi invece su NuGet presupponendo questo tipo quando non viene specificato nessun tipo.</span><span class="sxs-lookup"><span data-stu-id="55689-283">In both cases, it's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="55689-284">`.nuspec`: indica il tipo di pacchetto in un nodo `packageTypes\packageType` sotto l'elemento `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="55689-284">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

- <span data-ttu-id="55689-285">`project.json`: indica il tipo di pacchetto in un codice json della proprietà `packOptions.packageType`:</span><span class="sxs-lookup"><span data-stu-id="55689-285">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="55689-286">Aggiunta di un file leggimi e di altri file</span><span class="sxs-lookup"><span data-stu-id="55689-286">Adding a readme and other files</span></span>

<span data-ttu-id="55689-287">Per specificare direttamente i file da includere nel pacchetto, usare il nodo `<files>` nel file `.nuspec`, che *segue* il tag `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="55689-287">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

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
> <span data-ttu-id="55689-288">Quando si usa l'approccio della directory di lavoro basata sulle convenzioni, è possibile inserire il file readme.txt nella radice del pacchetto e gli altri contenuti nella cartella `content`.</span><span class="sxs-lookup"><span data-stu-id="55689-288">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="55689-289">Non sono necessari elementi `<file>` nel manifesto.</span><span class="sxs-lookup"><span data-stu-id="55689-289">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="55689-290">Quando si include un file denominato `readme.txt` nella radice del pacchetto, Visual Studio visualizza i contenuti del file come testo normale subito dopo avere installato direttamente il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="55689-290">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="55689-291">I file leggimi non vengono visualizzati per i pacchetti installati come dipendenze.</span><span class="sxs-lookup"><span data-stu-id="55689-291">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="55689-292">Ecco ad esempio come viene visualizzato il file leggimi per il pacchetto HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="55689-292">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Visualizzazione di un file leggimi per un pacchetto NuGet durante l'installazione](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="55689-294">Se si include un nodo `<files>` vuoto nel file `.nuspec`, NuGet non include nel pacchetto altri contenuti diversi dal contenuto della cartella `lib`.</span><span class="sxs-lookup"><span data-stu-id="55689-294">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="55689-295">Inclusione di proprietà e destinazioni MSBuild in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="55689-295">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="55689-296">In alcuni casi, potrebbe essere necessario aggiungere destinazioni o proprietà di compilazione personalizzata nei progetti che utilizzano il pacchetto, ad esempio l'esecuzione di uno strumento o processo personalizzato durante la compilazione.</span><span class="sxs-lookup"><span data-stu-id="55689-296">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="55689-297">A tale scopo, inserire i file nel formato `<package_id>.targets` o `<package_id>.props` (ad esempio `Contoso.Utility.UsefulStuff.targets`) nella cartella `\build` del progetto.</span><span class="sxs-lookup"><span data-stu-id="55689-297">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="55689-298">I file nella cartella radice `\build` sono considerati adatti a tutti i framework di destinazione.</span><span class="sxs-lookup"><span data-stu-id="55689-298">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="55689-299">Per fornire file specifici del framework, inserirli prima nelle sottocartelle appropriate, come di seguito:</span><span class="sxs-lookup"><span data-stu-id="55689-299">To provide framework-specific files, first place those within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="55689-300">Nel file `.nuspec` assicurarsi quindi di fare riferimento a questi file nel nodo `<files>`:</span><span class="sxs-lookup"><span data-stu-id="55689-300">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
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

<span data-ttu-id="55689-301">NuGet 2.x, quando installa un pacchetto con i file `\build`, aggiunge un elemento `<Import>` di MSBuild nel file di progetto che punta ai file `.targets` e `.props`.</span><span class="sxs-lookup"><span data-stu-id="55689-301">When NuGet 2.x installs a package with `\build` files, it adds an MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="55689-302">`.props` viene aggiunto all'inizio del file di progetto, `.targets` viene aggiunto alla fine.</span><span class="sxs-lookup"><span data-stu-id="55689-302">(`.props` is added at the top of the project file; `.targets` is added at the bottom.)</span></span>

<span data-ttu-id="55689-303">Con NuGet 3.x, le destinazioni non vengono aggiunte al progetto, ma vengono rese disponibili tramite `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="55689-303">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="55689-304">Creazione di pacchetti con assembly di interoperabilità COM</span><span class="sxs-lookup"><span data-stu-id="55689-304">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="55689-305">I pacchetti che contengono gli assembly di interoperabilità COM devono includere un [file di destinazioni](#including-msbuild-props-and-targets-in-a-package) appropriato in modo che i metadati `EmbedInteropTypes` corretti vengano aggiunti ai progetti usando il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="55689-305">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="55689-306">Per impostazione predefinita, i metadati `EmbedInteropTypes` sono sempre false per tutti gli assembly quando viene usato PackageReference, quindi il file di destinazioni aggiunge i metadati in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="55689-306">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="55689-307">Per evitare conflitti, il nome della destinazione deve essere univoco. L'ideale è usare una combinazione del nome del pacchetto dell'assembly che viene incorporato, sostituendo `{InteropAssemblyName}` nell'esempio riportato di seguito con tale valore.</span><span class="sxs-lookup"><span data-stu-id="55689-307">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="55689-308">Per un esempio, vedere anche [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop).</span><span class="sxs-lookup"><span data-stu-id="55689-308">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml      
<Target Name="EmbeddingAssemblyNameFromPackageId" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <PropertyGroup>
    <_InteropAssemblyFileName>{InteropAssemblyName}</_InteropAssemblyFileName>
  </PropertyGroup>
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '$(_InteropAssemblyFileName)' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="55689-309">Si noti che, quando si usa il formato di riferimento `packages.config`, l'aggiunta di riferimenti agli assembly dai pacchetti fa sì che NuGet e Visual Studio cerchino gli assembly di interoperabilità COM e impostino `EmbedInteropTypes` su true nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="55689-309">Note that when using the `packages.config` reference format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="55689-310">In questo caso viene eseguito l'override delle destinazioni.</span><span class="sxs-lookup"><span data-stu-id="55689-310">In this case the targets are overriden.</span></span>

<span data-ttu-id="55689-311">Per impostazione predefinita inoltre gli [asset di compilazione non vengono trasferiti in modo transitivo](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="55689-311">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="55689-312">I pacchetti creati come descritto qui funzionano diversamente quando ne viene eseguito il pull come dipendenza transitiva da un progetto al riferimento al progetto.</span><span class="sxs-lookup"><span data-stu-id="55689-312">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="55689-313">L'utente del pacchetto ne può consentire il trasferimento modificando il valore predefinito di PrivateAssets in modo che non includa la compilazione.</span><span class="sxs-lookup"><span data-stu-id="55689-313">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>  

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="55689-314">Esecuzione di nuget pack per generare il file con estensione nupkg</span><span class="sxs-lookup"><span data-stu-id="55689-314">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="55689-315">Quando si usa un assembly o la directory di lavoro basata sulle convenzioni, creare un pacchetto eseguendo `nuget pack` con il file `.nuspec`, sostituendo `<manifest-name>` con il nome file specifico:</span><span class="sxs-lookup"><span data-stu-id="55689-315">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<manifest-name>` with your specific filename:</span></span>

```
nuget pack <project-name>.nuspec
```

<span data-ttu-id="55689-316">Quando si usa un progetto di Visual Studio, eseguire `nuget pack` con il file di progetto, che carica automaticamente il file `.nuspec` del progetto e sostituisce il token usando i valori del file di progetto:</span><span class="sxs-lookup"><span data-stu-id="55689-316">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="55689-317">L'uso diretto del file di progetto è necessario per la sostituzione dei token perché il progetto è l'origine dei valori dei token.</span><span class="sxs-lookup"><span data-stu-id="55689-317">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="55689-318">La sostituzione dei token non avviene se si usa `nuget pack` con un file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="55689-318">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="55689-319">In tutti i casi, `nuget pack` esclude le cartelle che iniziano con un punto, ad esempio `.git` o `.hg`.</span><span class="sxs-lookup"><span data-stu-id="55689-319">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="55689-320">NuGet indica se sono presenti errori nel file `.nuspec` che richiedono una correzione, ad esempio se si dimentica di modificare i valori dei segnaposto nel manifesto.</span><span class="sxs-lookup"><span data-stu-id="55689-320">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="55689-321">Dopo la corretta esecuzione di `nuget pack`, è disponibile un file `.nupkg` che è possibile pubblicare in una raccolta appropriata, come illustrato in [Pubblicazione di un pacchetto](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="55689-321">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="55689-322">Per esaminare un pacchetto dopo averlo creato, è possibile aprirlo nello strumento [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer),</span><span class="sxs-lookup"><span data-stu-id="55689-322">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="55689-323">che offre una visualizzazione grafica dei contenuti del pacchetto e del manifesto.</span><span class="sxs-lookup"><span data-stu-id="55689-323">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="55689-324">È anche possibile rinominare il file `.nupkg` risultante in un file `.zip` ed esplorarne il contenuto direttamente.</span><span class="sxs-lookup"><span data-stu-id="55689-324">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="55689-325">Opzioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="55689-325">Additional options</span></span>

<span data-ttu-id="55689-326">Tra le altre funzionalità, è possibile usare diverse opzioni della riga di comando con `nuget pack` per escludere i file, eseguire l'override del numero di versione nel manifesto e modificare la cartella di output.</span><span class="sxs-lookup"><span data-stu-id="55689-326">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="55689-327">Per un elenco completo, vedere le [informazioni di riferimento sul comando pack](../tools/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="55689-327">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="55689-328">Le seguenti sono alcune opzioni comuni ai progetti di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="55689-328">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="55689-329">**Progetti di riferimento**: se il progetto fa riferimento ad altri progetti, è possibile aggiungere i progetti a cui si fa riferimento come parte del pacchetto o come dipendenze, usando l'opzione `-IncludeReferencedProjects`:</span><span class="sxs-lookup"><span data-stu-id="55689-329">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="55689-330">Questo processo di inclusione è ricorsivo, quindi se `MyProject.csproj` fa riferimento ai progetti B e C e tali progetti fanno riferimento a D, E e F, i file di B, C, D, E e F vengono inclusi nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="55689-330">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="55689-331">Se un progetto a cui si fa riferimento include un proprio file `.nuspec`, NuGet aggiunge invece tale progetto a cui si fa riferimento come dipendenza.</span><span class="sxs-lookup"><span data-stu-id="55689-331">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="55689-332">È necessario creare un pacchetto per il progetto e pubblicarlo separatamente.</span><span class="sxs-lookup"><span data-stu-id="55689-332">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="55689-333">**Configurazione della build**: per impostazione predefinita, NuGet usa la configurazione della build predefinita impostata nel file di progetto, in genere *Debug*.</span><span class="sxs-lookup"><span data-stu-id="55689-333">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="55689-334">Per creare un pacchetto per i file da una configurazione della build differente, ad esempio *Release*, usare l'opzione `-properties` con la configurazione:</span><span class="sxs-lookup"><span data-stu-id="55689-334">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="55689-335">**Simboli**: per includere i simboli che consentono agli utenti di eseguire il codice del pacchetto un'istruzione alla volta nel debugger, usare l'opzione `-Symbols`:</span><span class="sxs-lookup"><span data-stu-id="55689-335">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="55689-336">Test dell'installazione pacchetto</span><span class="sxs-lookup"><span data-stu-id="55689-336">Testing package installation</span></span>

<span data-ttu-id="55689-337">Prima di pubblicare un pacchetto, in genere si preferisce testarne il processo di installazione in un progetto.</span><span class="sxs-lookup"><span data-stu-id="55689-337">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="55689-338">I test assicurano che i file necessari vengano inseriti nei percorsi corretti all'interno del progetto.</span><span class="sxs-lookup"><span data-stu-id="55689-338">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="55689-339">È possibile testare manualmente le installazioni in Visual Studio o dalla riga di comando seguendo i normali [passaggi di installazione del pacchetto](../Quickstart/Use-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="55689-339">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../Quickstart/Use-a-Package.md).</span></span>

<span data-ttu-id="55689-340">Per i test automatizzati, il processo di base è il seguente:</span><span class="sxs-lookup"><span data-stu-id="55689-340">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="55689-341">Copiare il file `.nupkg` in una cartella locale.</span><span class="sxs-lookup"><span data-stu-id="55689-341">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="55689-342">Aggiungere la cartella alle origini del pacchetto usando il comando `nuget sources -name <name> -source <path>`. Vedere [nuget sources](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="55689-342">Add the folder to your package sources using the `nuget sources -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="55689-343">Si noti che è necessario impostare l'origine locale solo una volta in ogni computer.</span><span class="sxs-lookup"><span data-stu-id="55689-343">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="55689-344">Installare il pacchetto da tale origine usando `nuget install <packageID> -source <name>` dove `<name>` corrisponde al nome dell'origine specificata in `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="55689-344">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="55689-345">Specificando l'origine, il pacchetto viene con certezza installato solo da tale origine.</span><span class="sxs-lookup"><span data-stu-id="55689-345">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="55689-346">Esaminare il file system per controllare che i file siano installati correttamente.</span><span class="sxs-lookup"><span data-stu-id="55689-346">Examine the file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55689-347">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="55689-347">Next Steps</span></span>

<span data-ttu-id="55689-348">Dopo aver creato un pacchetto, ovvero un file `.nupkg`, è possibile pubblicarlo nella raccolta di propria scelta, come descritto in [Pubblicazione di un pacchetto](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="55689-348">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="55689-349">Potrebbe anche essere necessario estendere le funzionalità del pacchetto o supportare altri scenari, come descritto negli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="55689-349">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="55689-350">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="55689-350">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="55689-351">Supporto di più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="55689-351">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="55689-352">Trasformazioni di file di origine e di configurazione</span><span class="sxs-lookup"><span data-stu-id="55689-352">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="55689-353">Localizzazione</span><span class="sxs-lookup"><span data-stu-id="55689-353">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="55689-354">Versioni non definitive</span><span class="sxs-lookup"><span data-stu-id="55689-354">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="55689-355">Sono infine disponibili altri tipi di pacchetti da tenere presenti:</span><span class="sxs-lookup"><span data-stu-id="55689-355">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="55689-356">Pacchetti nativi</span><span class="sxs-lookup"><span data-stu-id="55689-356">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="55689-357">Pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="55689-357">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
