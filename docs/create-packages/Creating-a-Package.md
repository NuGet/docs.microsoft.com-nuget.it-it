---
title: Come creare un pacchetto NuGet
description: Guida dettagliata al processo di progettazione e creazione di un pacchetto NuGet, incluse le principali decisioni critiche, ad esempio quelle relative ai file e al controllo delle versioni.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 1657479e1a87f7022caa2fd991127b4ca702cdac
ms.sourcegitcommit: 00c4c809c69c16fcf4d81012eb53ea22f0691d0b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2018
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="bbeeb-103">Creazione di pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="bbeeb-103">Creating NuGet packages</span></span>

<span data-ttu-id="bbeeb-104">Indipendentemente dalle operazioni eseguite dal pacchetto o dal tipo di codice contenuto, `nuget.exe` viene usato per rendere disponibili tali funzionalità in un componente condivisibile e utilizzabile da altri sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-104">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="bbeeb-105">Per installare `nuget.exe`, vedere [Installare l'interfaccia della riga di comando di NuGet](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-105">To install `nuget.exe`, see [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span> <span data-ttu-id="bbeeb-106">Si noti che `nuget.exe` non è incluso automaticamente in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-106">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="bbeeb-107">Da un punto di vista tecnico, un pacchetto NuGet è solo un file ZIP rinominato con l'estensione `.nupkg` e i cui contenuti rispettano determinate convenzioni.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-107">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="bbeeb-108">Questo argomento descrive il processo dettagliato di creazione di un pacchetto che soddisfa tali convenzioni.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-108">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="bbeeb-109">Per una procedura dettagliata specifica, vedere [Guida introduttiva: Creare e pubblicare un pacchetto](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-109">For a focused walkthrough, refer to [Quickstart: create and publish a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="bbeeb-110">La creazione di un pacchetto inizia con il codice compilato (assembly), i simboli e/o altri file che si vuole distribuire come pacchetto. Vedere [Panoramica e flusso di lavoro](overview-and-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-110">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="bbeeb-111">Questo processo è indipendente dalla compilazione o comunque dalla generazione dei file inseriti nel pacchetto, anche se è possibile usare le informazioni contenute in un file di progetto per mantenere sincronizzati i pacchetti e gli assembly compilati.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-111">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Note]
> <span data-ttu-id="bbeeb-112">Questo argomento si applica a tipi di progetto diversi dai progetti .NET Core, che usano Visual Studio 2017 e NuGet 4.0+.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-112">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="bbeeb-113">In questi progetti .NET Core, NuGet usa direttamente le informazioni contenute nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-113">In those .NET Core projects, NuGet uses information in the project file directly.</span></span> <span data-ttu-id="bbeeb-114">Per informazioni dettagliate, vedere [Creare pacchetti .NET Standard con Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) e [Pack e restore di NuGet come destinazioni MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-114">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="bbeeb-115">Scelta degli assembly per cui creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="bbeeb-115">Deciding which assemblies to package</span></span>

<span data-ttu-id="bbeeb-116">La maggior parte dei pacchetti per utilizzo generico contiene uno o più assembly che gli altri sviluppatori possono usare nei propri progetti.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-116">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="bbeeb-117">In generale, l'ideale è avere un assembly per ogni pacchetto NuGet, purché ogni assembly abbia una propria utilità.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-117">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="bbeeb-118">Se ad esempio è presente un file `Utilities.dll` che dipende da `Parser.dll` e `Parser.dll` è utile di per sé, creare un pacchetto per ognuno.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-118">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="bbeeb-119">In questo modo gli sviluppatori possono usare `Parser.dll` indipendentemente da `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-119">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="bbeeb-120">Se la libreria è costituita da più assembly che non hanno una propria utilità, è consigliabile combinarli in un solo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-120">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="bbeeb-121">Usando l'esempio precedente, se `Parser.dll` contiene codice che viene usato solo da `Utilities.dll`, è consigliabile tenere `Parser.dll` nello stesso pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-121">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="bbeeb-122">Analogamente, se `Utilities.dll` dipende da `Utilities.resources.dll` e quest'ultimo non è utile di per sé, inserirli entrambi nello stesso pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-122">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="bbeeb-123">Le risorse sono di fatto un caso particolare.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-123">Resources are, in fact, a special case.</span></span> <span data-ttu-id="bbeeb-124">Quando un pacchetto viene installato in un progetto, NuGet aggiunge automaticamente alle DLL del pacchetto i riferimenti agli assembly, *escludendo* quelli denominati `.resources.dll` perché si presuppone che siano assembly satellite localizzati. Vedere [Creazione di pacchetti localizzati](creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-124">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="bbeeb-125">Per questo motivo, evitare di usare `.resources.dll` per i file che contengono invece codice essenziale per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-125">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="bbeeb-126">Se la libreria contiene assembly di interoperabilità COM, seguire le linee guida aggiuntive in [Creazione di pacchetti con assembly di interoperabilità COM](#authoring-packages-with-com-interop-assemblies).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-126">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="bbeeb-127">Ruolo e struttura del file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="bbeeb-127">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="bbeeb-128">Dopo avere deciso per quali file si vuole creare un pacchetto, il passaggio successivo prevede la creazione di un manifesto del pacchetto in un file XML `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-128">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="bbeeb-129">Il manifesto:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-129">The manifest:</span></span>

1. <span data-ttu-id="bbeeb-130">Descrive i contenuti del pacchetto e viene incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-130">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="bbeeb-131">Gestisce la creazione del pacchetto e indica a NuGet come installare il pacchetto in un progetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-131">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="bbeeb-132">Il manifesto, ad esempio, identifica le altre dipendenze del pacchetto in modo che NuGet possa installare anche tali dipendenze quando viene installato il pacchetto principale.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-132">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="bbeeb-133">Contiene le proprietà sia obbligatorie che facoltative, come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-133">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="bbeeb-134">Per informazioni dettagliate, incluse le altre proprietà non citate qui, vedere [Informazioni di riferimento sul file .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-134">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="bbeeb-135">Proprietà obbligatorie:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-135">Required properties:</span></span>

- <span data-ttu-id="bbeeb-136">Identificatore del pacchetto, che deve essere univoco nella raccolta che ospita il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-136">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="bbeeb-137">Numero di versione specifico nel formato *Major.Minor.Patch[-Suffix]* dove *-Suffix* identifica le [versioni preliminari](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="bbeeb-137">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="bbeeb-138">Titolo del pacchetto come deve essere visualizzato nell'host (ad esempio, nuget.org)</span><span class="sxs-lookup"><span data-stu-id="bbeeb-138">The package title as it should appears on the host (like nuget.org)</span></span>
- <span data-ttu-id="bbeeb-139">Informazioni sull'autore e sul proprietario.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-139">Author and owner information.</span></span>
- <span data-ttu-id="bbeeb-140">Descrizione estesa del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-140">A long description of the package.</span></span>

<span data-ttu-id="bbeeb-141">Proprietà facoltative comuni:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-141">Common optional properties:</span></span>

- <span data-ttu-id="bbeeb-142">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="bbeeb-142">Release notes</span></span>
- <span data-ttu-id="bbeeb-143">Informazioni sul copyright</span><span class="sxs-lookup"><span data-stu-id="bbeeb-143">Copyright information</span></span>
- <span data-ttu-id="bbeeb-144">Breve descrizione dell'[interfaccia utente di Gestione pacchetti in Visual Studio](../tools/package-manager-ui.md)</span><span class="sxs-lookup"><span data-stu-id="bbeeb-144">A short description for the [Package Manager UI in Visual Studio](../tools/package-manager-ui.md)</span></span>
- <span data-ttu-id="bbeeb-145">ID impostazioni locali</span><span class="sxs-lookup"><span data-stu-id="bbeeb-145">A locale ID</span></span>
- <span data-ttu-id="bbeeb-146">URL della home page e della licenza</span><span class="sxs-lookup"><span data-stu-id="bbeeb-146">Home page and license URLs</span></span>
- <span data-ttu-id="bbeeb-147">URL dell'icona</span><span class="sxs-lookup"><span data-stu-id="bbeeb-147">An icon URL</span></span>
- <span data-ttu-id="bbeeb-148">Elenchi di dipendenze e riferimenti</span><span class="sxs-lookup"><span data-stu-id="bbeeb-148">Lists of dependencies and references</span></span>
- <span data-ttu-id="bbeeb-149">Tag di supporto per le ricerche nella raccolta</span><span class="sxs-lookup"><span data-stu-id="bbeeb-149">Tags that assist in gallery searches</span></span>

<span data-ttu-id="bbeeb-150">Di seguito è riportato un file `.nuspec` tipico (ma fittizio), con commenti che descrivono le proprietà:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-150">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

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

         <!-- License and project URLs provide links for the gallery -->
        <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

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

<span data-ttu-id="bbeeb-151">Per informazioni dettagliate sulla dichiarazione delle dipendenze e sulla specifica dei numeri di versione, vedere [Controllo delle versioni dei pacchetti](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-151">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="bbeeb-152">È anche possibile esporre gli asset dalle dipendenze direttamente nel pacchetto usando gli attributi `include` ed `exclude` nell'elemento `dependency`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-152">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="bbeeb-153">Vedere la [sezione Dipendenze delle informazioni di riferimento sul file .nuspec](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-153">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="bbeeb-154">Poiché il manifesto è incluso nel pacchetto creato, per trovare altri esempi, esaminare i pacchetti esistenti.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-154">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="bbeeb-155">Una valida fonte è la cartella *global-packages* nel computer, la posizione della quale viene restituita dal comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-155">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="bbeeb-156">Andare a qualsiasi cartella *pacchetto\versione*, copiare il file `.nupkg` in un file `.zip`, quindi aprire il file `.zip` ed esaminare il file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-156">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="bbeeb-157">Quando si crea un file `.nuspec` da un progetto di Visual Studio, il manifesto contiene token che vengono sostituiti con le informazioni provenienti dal progetto quando il pacchetto viene compilato.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-157">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="bbeeb-158">Vedere [Creazione del file con estensione nuspec da un progetto di Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-158">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="bbeeb-159">Creazione del file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="bbeeb-159">Creating the .nuspec file</span></span>

<span data-ttu-id="bbeeb-160">La creazione di un manifesto completo inizia in genere con un file `.nuspec` di base generato con uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-160">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="bbeeb-161">Directory di lavoro basata sulle convenzioni</span><span class="sxs-lookup"><span data-stu-id="bbeeb-161">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="bbeeb-162">DLL dell'assembly</span><span class="sxs-lookup"><span data-stu-id="bbeeb-162">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="bbeeb-163">Progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bbeeb-163">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="bbeeb-164">Nuovo file con valori predefiniti</span><span class="sxs-lookup"><span data-stu-id="bbeeb-164">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="bbeeb-165">Si modifica quindi il file manualmente in modo che descriva il contenuto esatto che dovrà essere incluso nel pacchetto finale.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-165">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="bbeeb-166">I file `.nuspec` generati contengono segnaposto che devono essere modificati prima di creare il pacchetto con il comando `nuget pack`,</span><span class="sxs-lookup"><span data-stu-id="bbeeb-166">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="bbeeb-167">che ha esito negativo se il file `.nuspec` contiene segnaposto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-167">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="bbeeb-168">Da una directory di lavoro basata sulle convenzioni</span><span class="sxs-lookup"><span data-stu-id="bbeeb-168">From a convention-based working directory</span></span>

<span data-ttu-id="bbeeb-169">Dato che un pacchetto NuGet è solo un file ZIP rinominato con l'estensione `.nupkg`, spesso è più semplice creare la struttura di cartelle desiderata nel file system locale, quindi creare il file `.nuspec` direttamente da tale struttura.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-169">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, its often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="bbeeb-170">Il comando `nuget pack` aggiunge quindi automaticamente tutti i file in tale struttura di cartelle, escluse le cartelle che iniziano con `.`, per poter mantenere i file privati nella stessa struttura.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-170">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you keep private files in the same structure).</span></span>

<span data-ttu-id="bbeeb-171">Il vantaggio di questo approccio è che non è necessario specificare nel manifesto i file che si vuole includere nel pacchetto, come illustrato più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-171">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="bbeeb-172">È sufficiente fare in modo che il processo di compilazione generi l'esatta struttura di cartelle da inserire nel pacchetto, per poter facilmente includere altri file che altrimenti potrebbero non fare parte di un progetto:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-172">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="bbeeb-173">Contenuto e codice sorgente da inserire nel progetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-173">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="bbeeb-174">Script di PowerShell. I pacchetti usati in NuGet 2.x possono includere anche script di installazione, non supportati in NuGet 3.x e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-174">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="bbeeb-175">Trasformazioni della configurazione esistente e dei file del codice sorgente di un progetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-175">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="bbeeb-176">Le convenzioni delle cartelle sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-176">The folder conventions are as follows:</span></span>

| <span data-ttu-id="bbeeb-177">Cartella</span><span class="sxs-lookup"><span data-stu-id="bbeeb-177">Folder</span></span> | <span data-ttu-id="bbeeb-178">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bbeeb-178">Description</span></span> | <span data-ttu-id="bbeeb-179">Azione durante l'installazione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="bbeeb-179">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bbeeb-180">(radice)</span><span class="sxs-lookup"><span data-stu-id="bbeeb-180">(root)</span></span> | <span data-ttu-id="bbeeb-181">Percorso del file readme.txt</span><span class="sxs-lookup"><span data-stu-id="bbeeb-181">Location for readme.txt</span></span> | <span data-ttu-id="bbeeb-182">Visual Studio visualizza un file readme.txt nella radice del pacchetto quando il pacchetto viene installato.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-182">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="bbeeb-183">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="bbeeb-183">lib/{tfm}</span></span> | <span data-ttu-id="bbeeb-184">File di assembly (`.dll`), di documentazione (`.xml`) e di simboli (`.pdb`) per il moniker del framework di destinazione (TFM, Target Framework Moniker) specificato</span><span class="sxs-lookup"><span data-stu-id="bbeeb-184">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="bbeeb-185">Gli assembly vengono aggiunti come riferimenti. `.xml` e `.pdb` vengono copiati nelle cartelle di progetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-185">Assemblies are added as references; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="bbeeb-186">Per la creazione di sottocartelle specifiche del framework di destinazione, vedere [Supporto di più framework di destinazione](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-186">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="bbeeb-187">runtimes</span><span class="sxs-lookup"><span data-stu-id="bbeeb-187">runtimes</span></span> | <span data-ttu-id="bbeeb-188">File di assembly (`.dll`), di simboli (`.pdb`) e di risorse native (`.pri`) specifici dell'architettura</span><span class="sxs-lookup"><span data-stu-id="bbeeb-188">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="bbeeb-189">Gli assembly vengono aggiunti come riferimenti. Gli altri file vengono copiati nelle cartelle di progetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-189">Assemblies are added as references; other files are copied into project folders.</span></span> <span data-ttu-id="bbeeb-190">Vedere [Supporto di più framework di destinazione](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-190">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="bbeeb-191">contenuto</span><span class="sxs-lookup"><span data-stu-id="bbeeb-191">content</span></span> | <span data-ttu-id="bbeeb-192">File arbitrari</span><span class="sxs-lookup"><span data-stu-id="bbeeb-192">Arbitrary files</span></span> | <span data-ttu-id="bbeeb-193">I contenuti vengono copiati nella radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-193">Contents are copied to the project root.</span></span> <span data-ttu-id="bbeeb-194">La cartella **content** può essere considerata come la radice dell'applicazione di destinazione che in definitiva utilizza il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-194">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="bbeeb-195">Per fare in modo che il pacchetto aggiunga un'immagine nella cartella */images* dell'applicazione, inserirla nella cartella *content/images* del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-195">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="bbeeb-196">build</span><span class="sxs-lookup"><span data-stu-id="bbeeb-196">build</span></span> | <span data-ttu-id="bbeeb-197">File `.targets` e `.props` MSBuild</span><span class="sxs-lookup"><span data-stu-id="bbeeb-197">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="bbeeb-198">Vengono automaticamente inseriti nel file di progetto o in `project.lock.json` (NuGet 3.x+).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-198">Automatically inserted into the project file or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="bbeeb-199">tools</span><span class="sxs-lookup"><span data-stu-id="bbeeb-199">tools</span></span> | <span data-ttu-id="bbeeb-200">Script di PowerShell e programmi accessibili dalla console di Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="bbeeb-200">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="bbeeb-201">La cartella `tools` viene aggiunta alla variabile di ambiente `PATH` solo per la console di Gestione pacchetti, in particolare *non* alla variabile `PATH` impostata per MSBuild durante la compilazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-201">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="bbeeb-202">Poiché la struttura di cartelle può contenere un numero indeterminato di assembly per un numero indeterminato di framework di destinazione, questo metodo è necessario quando si creano pacchetti che supportano più framework</span><span class="sxs-lookup"><span data-stu-id="bbeeb-202">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks</span></span> 

<span data-ttu-id="bbeeb-203">In ogni caso, dopo avere creato la struttura di cartelle desiderata, eseguire il comando seguente in tale cartella per creare il file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-203">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="bbeeb-204">Anche in questo caso, il file `.nuspec` generato non contiene riferimenti espliciti ai file nella struttura di cartelle.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-204">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="bbeeb-205">NuGet include tutti i file automaticamente quando viene creato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-205">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="bbeeb-206">È tuttavia necessario modificare i valori dei segnaposto nelle altre parti del manifesto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-206">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="bbeeb-207">Da una DLL dell'assembly</span><span class="sxs-lookup"><span data-stu-id="bbeeb-207">From an assembly DLL</span></span>

<span data-ttu-id="bbeeb-208">Nel semplice caso della creazione di un pacchetto da un assembly, è possibile generare un file `.nuspec` dai metadati nell'assembly usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-208">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="bbeeb-209">Usando questo formato, alcuni segnaposto nel manifesto vengono sostituiti con i valori specifici dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-209">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="bbeeb-210">La proprietà `<id>`, ad esempio, viene impostata sul nome dell'assembly e `<version>` viene impostata sulla versione dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-210">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="bbeeb-211">Le altre proprietà del manifesto non hanno tuttavia valori corrispondenti nell'assembly e perciò contengono ancora i segnaposto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-211">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="bbeeb-212">Da un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bbeeb-212">From a Visual Studio project</span></span>

<span data-ttu-id="bbeeb-213">La creazione di un file `.nuspec` da un file `.csproj` o `.vbproj` è utile perché viene fatto automaticamente riferimento agli altri pacchetti che sono stati installati in tale progetto come a dipendenze.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-213">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="bbeeb-214">È sufficiente usare il comando seguente nella stessa cartella del file di progetto:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-214">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="bbeeb-215">Il file `<project-name>.nuspec` risultante contiene *token* che in fase di creazione del pacchetto vengono sostituiti con i valori del progetto, inclusi i riferimenti agli altri pacchetti già installati.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-215">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="bbeeb-216">Un token è delimitato dai simboli `$` su entrambi i lati della proprietà del progetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-216">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="bbeeb-217">Ad esempio, il valore `<id>` in un manifesto generato in questo modo solitamente viene visualizzato come segue:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-217">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="bbeeb-218">Questo token viene sostituito con il valore `AssemblyName` del file di progetto in fase di creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-218">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="bbeeb-219">Per il mapping esatto dei valori del progetto ai token di `.nuspec`, vedere le [informazioni di riferimento in Token di sostituzione](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-219">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="bbeeb-220">I token evitano di dover aggiornare i valori fondamentali, ad esempio il numero di versione, nel file `.nuspec` quando si aggiorna il progetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-220">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="bbeeb-221">È sempre possibile sostituire i token con valori letterali, se necessario.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-221">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="bbeeb-222">Tenere presente che sono disponibili diverse altre opzioni di creazione del pacchetto quando si usa un progetto di Visual Studio, come illustrato più avanti in [Esecuzione di nuget pack per generare il file con estensione nupkg](#running-nuget-pack-to-generate-the-nupkg-file).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-222">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="bbeeb-223">Pacchetti a livello di soluzione</span><span class="sxs-lookup"><span data-stu-id="bbeeb-223">Solution-level packages</span></span>

<span data-ttu-id="bbeeb-224">*Solo NuGet 2.x. Non disponibile in NuGet 3.0+.*</span><span class="sxs-lookup"><span data-stu-id="bbeeb-224">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="bbeeb-225">NuGet 2.x supportava la nozione di pacchetto a livello di soluzione che installa strumenti o comandi aggiuntivi per la console di Gestione pacchetti (contenuti della cartella `tools`), ma non aggiunge riferimenti, contenuto o personalizzazioni delle compilazioni ai progetti della soluzione.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-225">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="bbeeb-226">Tali pacchetti non contengono file nelle cartelle `lib`, `content` o `build` dirette e nessuna dipendenza ha file nelle rispettive cartelle `lib`, `content` o `build`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-226">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="bbeeb-227">NuGet tiene traccia dei pacchetti a livello di soluzione installati in un file `packages.config` nella cartella `.nuget`, invece che nel file `packages.config` del progetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-227">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="bbeeb-228">Nuovo file con valori predefiniti</span><span class="sxs-lookup"><span data-stu-id="bbeeb-228">New file with default values</span></span>

<span data-ttu-id="bbeeb-229">Il comando seguente crea un manifesto predefinito con segnaposto, che assicura di iniziare con la struttura di file corretta:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-229">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="bbeeb-230">Se si omette \<package-name\>, il file risultante è `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-230">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="bbeeb-231">Se come nome si specifica ad esempio `Contoso.Utility.UsefulStuff`, il file è `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-231">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="bbeeb-232">Il file `.nuspec` risultante contiene segnaposto per i valori come `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-232">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="bbeeb-233">Assicurarsi di modificare il file prima di usarlo per creare il file `.nupkg` finale.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-233">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="bbeeb-234">Scelta di un identificatore univoco del pacchetto e impostazione del numero di versione</span><span class="sxs-lookup"><span data-stu-id="bbeeb-234">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="bbeeb-235">L'identificatore del pacchetto (elemento `<id>`) e il numero di versione (elemento `<version>`) sono i due valori più importanti del manifesto perché identificano in modo univoco il codice esatto contenuto nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-235">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="bbeeb-236">**Procedure consigliate per l'identificatore del pacchetto:**</span><span class="sxs-lookup"><span data-stu-id="bbeeb-236">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="bbeeb-237">**Univocità**: l'identificatore deve essere univoco in nuget.org o in qualsiasi raccolta che ospita il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-237">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="bbeeb-238">Prima di scegliere un identificatore, eseguire una ricerca nella raccolta applicabile per controllare se il nome è già in uso.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-238">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="bbeeb-239">Per evitare conflitti, è consigliabile usare il nome della società come prima parte dell'identificatore, ad esempio `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-239">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="bbeeb-240">**Nomi simili a spazi dei nomi**: seguono un modello simile a quello degli spazi dei nomi in .NET, usando la notazione del punto invece dei trattini.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-240">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="bbeeb-241">Usare, ad esempio, `Contoso.Utility.UsefulStuff` invece di `Contoso-Utility-UsefulStuff` o `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-241">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="bbeeb-242">Per gli utenti è anche utile che l'identificatore del pacchetto corrisponda agli spazi dei nomi usati nel codice.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-242">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="bbeeb-243">**Pacchetti di esempio**: se si produce un pacchetto di codice di esempio che illustra come usare un altro pacchetto, collegare `.Sample` come suffisso all'identificatore, come in `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-243">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="bbeeb-244">Il pacchetto di esempio avrà naturalmente una dipendenza dall'altro pacchetto. Quando si crea un pacchetto di esempio, usare il metodo della directory di lavoro basata sulle convenzioni descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-244">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="bbeeb-245">Nella cartella `content` inserire il codice di esempio in una cartella denominata `\Samples\<identifier>` come in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-245">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="bbeeb-246">**Procedure consigliate per la versione del pacchetto:**</span><span class="sxs-lookup"><span data-stu-id="bbeeb-246">**Best practices for the package version:**</span></span>

- <span data-ttu-id="bbeeb-247">In generale, impostare la versione del pacchetto in modo che corrisponda alla libreria, anche se non è strettamente necessario.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-247">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="bbeeb-248">È davvero semplicissimo quando si limita un pacchetto a un singolo assembly, come descritto precedentemente in [Scelta degli assembly per cui creare un pacchetto](#deciding-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-248">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="bbeeb-249">In generale, tenere presente che, durante la risoluzione delle dipendenze, di per sé NuGet gestisce le versioni dei pacchetti, non le versioni degli assembly.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-249">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="bbeeb-250">Quando si usa uno schema della versione non standard, tenere in considerazione le regole di controllo delle versioni di NuGet, come illustrato in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-250">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="bbeeb-251">Per informazioni sul controllo delle versioni, vedere anche la serie seguente di brevi post di blog:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-251">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - <span data-ttu-id="bbeeb-252">[Part 1: Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html) (Parte 1: Affrontare l'inferno delle DLL)</span><span class="sxs-lookup"><span data-stu-id="bbeeb-252">[Part 1: Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)</span></span>
> - <span data-ttu-id="bbeeb-253">[Part 2: The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html) (Parte 2: L'algoritmo principale)</span><span class="sxs-lookup"><span data-stu-id="bbeeb-253">[Part 2: The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)</span></span>
> - <span data-ttu-id="bbeeb-254">[Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html) (Parte 3: Unificazione tramite i reindirizzamenti di binding)</span><span class="sxs-lookup"><span data-stu-id="bbeeb-254">[Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)</span></span>

## <a name="setting-a-package-type"></a><span data-ttu-id="bbeeb-255">Impostazione di un tipo di pacchetto</span><span class="sxs-lookup"><span data-stu-id="bbeeb-255">Setting a package type</span></span>

<span data-ttu-id="bbeeb-256">Con NuGet 3.5+, i pacchetti possono essere contrassegnati con uno specifico *tipo di pacchetto* per indicarne l'uso previsto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-256">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="bbeeb-257">I pacchetti non contrassegnati con un tipo, inclusi tutti i pacchetti creati con versioni precedenti di NuGet, usano il tipo `Dependency` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-257">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="bbeeb-258">I pacchetti di tipo `Dependency` aggiungono asset in fase di compilazione o di esecuzione ad applicazioni e librerie e possono essere installati in qualsiasi tipo di progetto, presupponendo che siano compatibili.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-258">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="bbeeb-259">I pacchetti di tipo `DotnetCliTool` sono estensioni dell'[interfaccia della riga di comando di .NET](/dotnet/articles/core/tools/index) e vengono richiamati dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-259">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="bbeeb-260">Tali pacchetti possono essere installati solo nei progetti .NET Core e non hanno effetto sulle operazioni di ripristino.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-260">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="bbeeb-261">Per altre informazioni su queste estensioni in base al progetto, vedere la documentazione sull'[estendibilità in .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-261">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="bbeeb-262">I pacchetti di tipo personalizzato usano un identificatore di tipo arbitrario che è conforme alle stesse regole di formato degli ID dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-262">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="bbeeb-263">I tipi diversi da `Dependency` e `DotnetCliTool`, tuttavia, non vengono riconosciuti da Gestione pacchetti NuGet in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-263">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="bbeeb-264">I tipi di pacchetto vengono impostati nel file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-264">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="bbeeb-265">Per la compatibilità con le versioni precedenti è meglio *non* impostare in modo esplicito il tipo `Dependency` e basarsi invece sul fatto che NuGet presuppone questo tipo quando non viene specificato alcun tipo.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-265">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="bbeeb-266">`.nuspec`: indica il tipo di pacchetto in un nodo `packageTypes\packageType` sotto l'elemento `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-266">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="bbeeb-267">Aggiunta di un file leggimi e di altri file</span><span class="sxs-lookup"><span data-stu-id="bbeeb-267">Adding a readme and other files</span></span>

<span data-ttu-id="bbeeb-268">Per specificare direttamente i file da includere nel pacchetto, usare il nodo `<files>` nel file `.nuspec`, che *segue* il tag `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-268">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

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
> <span data-ttu-id="bbeeb-269">Quando si usa l'approccio della directory di lavoro basata sulle convenzioni, è possibile inserire il file readme.txt nella radice del pacchetto e gli altri contenuti nella cartella `content`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-269">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="bbeeb-270">Non sono necessari elementi `<file>` nel manifesto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-270">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="bbeeb-271">Quando si include un file denominato `readme.txt` nella radice del pacchetto, Visual Studio visualizza i contenuti del file come testo normale subito dopo avere installato direttamente il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-271">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="bbeeb-272">I file leggimi non vengono visualizzati per i pacchetti installati come dipendenze.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-272">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="bbeeb-273">Ecco ad esempio come viene visualizzato il file leggimi per il pacchetto HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-273">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Visualizzazione di un file leggimi per un pacchetto NuGet durante l'installazione](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="bbeeb-275">Se si include un nodo `<files>` vuoto nel file `.nuspec`, NuGet non include nel pacchetto altri contenuti diversi dal contenuto della cartella `lib`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-275">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="bbeeb-276">Inclusione di proprietà e destinazioni MSBuild in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="bbeeb-276">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="bbeeb-277">In alcuni casi, potrebbe essere necessario aggiungere destinazioni o proprietà di compilazione personalizzata nei progetti che utilizzano il pacchetto, ad esempio l'esecuzione di uno strumento o processo personalizzato durante la compilazione.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-277">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="bbeeb-278">A tale scopo, inserire i file nel formato `<package_id>.targets` o `<package_id>.props` (ad esempio `Contoso.Utility.UsefulStuff.targets`) nella cartella `\build` del progetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-278">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="bbeeb-279">I file nella cartella radice `\build` sono considerati adatti a tutti i framework di destinazione.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-279">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="bbeeb-280">Per fornire file specifici del framework, inserirli prima nelle sottocartelle appropriate, come di seguito:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-280">To provide framework-specific files, first place those within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="bbeeb-281">Nel file `.nuspec` assicurarsi quindi di fare riferimento a questi file nel nodo `<files>`:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-281">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

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

<span data-ttu-id="bbeeb-282">La possibilità di includere file props e targets di MSBuild in un pacchetto è stata [introdotta con NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), pertanto è consigliabile aggiungere l'attributo `minClientVersion="2.5"` all'elemento `metadata` per indicare la versione client NuGet minima richiesta per utilizzare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-282">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="bbeeb-283">Quando installa un pacchetto con i file `\build`, NuGet aggiunge elementi `<Import>` di MSBuild nel file di progetto che puntano ai file `.targets` e `.props`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-283">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="bbeeb-284">`.props` viene aggiunto all'inizio del file di progetto, `.targets` viene aggiunto alla fine. Viene aggiunto un elemento `<Import>` di MSBuild condizionale separato per ogni framework di destinazione.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-284">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="bbeeb-285">I file `.props` e `.targets` di MSBuild per l'assegnazione di più framework di destinazione possono essere posizionati nella cartella `\buildCrossTargeting`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-285">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildCrossTargeting` folder.</span></span> <span data-ttu-id="bbeeb-286">Durante l'installazione del pacchetto, NuGet aggiunge elementi `<Import>` corrispondenti al file di progetto, a condizione che il framework di destinazione non sia impostato (la proprietà MSBuild `$(TargetFramework)` deve essere vuota).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-286">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="bbeeb-287">Con NuGet 3.x, le destinazioni non vengono aggiunte al progetto, ma vengono rese disponibili tramite `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-287">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="bbeeb-288">Creazione di pacchetti con assembly di interoperabilità COM</span><span class="sxs-lookup"><span data-stu-id="bbeeb-288">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="bbeeb-289">I pacchetti che contengono gli assembly di interoperabilità COM devono includere un [file di destinazioni](#including-msbuild-props-and-targets-in-a-package) appropriato in modo che i metadati `EmbedInteropTypes` corretti vengano aggiunti ai progetti usando il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-289">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="bbeeb-290">Per impostazione predefinita, i metadati `EmbedInteropTypes` sono sempre false per tutti gli assembly quando viene usato PackageReference, quindi il file di destinazioni aggiunge i metadati in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-290">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="bbeeb-291">Per evitare conflitti, il nome della destinazione deve essere univoco. L'ideale è usare una combinazione del nome del pacchetto dell'assembly che viene incorporato, sostituendo `{InteropAssemblyName}` nell'esempio riportato di seguito con tale valore.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-291">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="bbeeb-292">Per un esempio, vedere anche [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-292">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="bbeeb-293">Si noti che, quando si usa il formato di gestione `packages.config`, l'aggiunta di riferimenti agli assembly dai pacchetti fa sì che NuGet e Visual Studio cerchino gli assembly di interoperabilità COM e impostino `EmbedInteropTypes` su true nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-293">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="bbeeb-294">In questo caso viene eseguito l'override delle destinazioni.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-294">In this case the targets are overriden.</span></span>

<span data-ttu-id="bbeeb-295">Per impostazione predefinita inoltre gli [asset di compilazione non vengono trasferiti in modo transitivo](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-295">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="bbeeb-296">I pacchetti creati come descritto qui funzionano diversamente quando ne viene eseguito il pull come dipendenza transitiva da un progetto al riferimento al progetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-296">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="bbeeb-297">L'utente del pacchetto ne può consentire il trasferimento modificando il valore predefinito di PrivateAssets in modo che non includa la compilazione.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-297">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="bbeeb-298">Esecuzione di nuget pack per generare il file con estensione nupkg</span><span class="sxs-lookup"><span data-stu-id="bbeeb-298">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="bbeeb-299">Quando si usa un assembly o la directory di lavoro basata sulle convenzioni, creare un pacchetto eseguendo `nuget pack` con il file `.nuspec`, sostituendo `<project-name>` con il nome file specifico:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-299">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="bbeeb-300">Quando si usa un progetto di Visual Studio, eseguire `nuget pack` con il file di progetto, che carica automaticamente il file `.nuspec` del progetto e sostituisce il token usando i valori del file di progetto:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-300">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="bbeeb-301">L'uso diretto del file di progetto è necessario per la sostituzione dei token perché il progetto è l'origine dei valori dei token.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-301">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="bbeeb-302">La sostituzione dei token non avviene se si usa `nuget pack` con un file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-302">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="bbeeb-303">In tutti i casi, `nuget pack` esclude le cartelle che iniziano con un punto, ad esempio `.git` o `.hg`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-303">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="bbeeb-304">NuGet indica se sono presenti errori nel file `.nuspec` che richiedono una correzione, ad esempio se si dimentica di modificare i valori dei segnaposto nel manifesto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-304">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="bbeeb-305">Dopo la corretta esecuzione di `nuget pack`, è disponibile un file `.nupkg` che è possibile pubblicare in una raccolta appropriata, come illustrato in [Pubblicazione di un pacchetto](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-305">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="bbeeb-306">Per esaminare un pacchetto dopo averlo creato, è possibile aprirlo nello strumento [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer),</span><span class="sxs-lookup"><span data-stu-id="bbeeb-306">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="bbeeb-307">che offre una visualizzazione grafica dei contenuti del pacchetto e del manifesto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-307">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="bbeeb-308">È anche possibile rinominare il file `.nupkg` risultante in un file `.zip` ed esplorarne il contenuto direttamente.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-308">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="bbeeb-309">Opzioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="bbeeb-309">Additional options</span></span>

<span data-ttu-id="bbeeb-310">Tra le altre funzionalità, è possibile usare diverse opzioni della riga di comando con `nuget pack` per escludere i file, eseguire l'override del numero di versione nel manifesto e modificare la cartella di output.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-310">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="bbeeb-311">Per un elenco completo, vedere le [informazioni di riferimento sul comando pack](../tools/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-311">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="bbeeb-312">Le seguenti sono alcune opzioni comuni ai progetti di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-312">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="bbeeb-313">**Progetti di riferimento**: se il progetto fa riferimento ad altri progetti, è possibile aggiungere i progetti a cui si fa riferimento come parte del pacchetto o come dipendenze, usando l'opzione `-IncludeReferencedProjects`:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-313">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="bbeeb-314">Questo processo di inclusione è ricorsivo, quindi se `MyProject.csproj` fa riferimento ai progetti B e C e tali progetti fanno riferimento a D, E e F, i file di B, C, D, E e F vengono inclusi nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-314">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="bbeeb-315">Se un progetto a cui si fa riferimento include un proprio file `.nuspec`, NuGet aggiunge invece tale progetto a cui si fa riferimento come dipendenza.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-315">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="bbeeb-316">È necessario creare un pacchetto per il progetto e pubblicarlo separatamente.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-316">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="bbeeb-317">**Configurazione della build**: per impostazione predefinita, NuGet usa la configurazione della build predefinita impostata nel file di progetto, in genere *Debug*.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-317">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="bbeeb-318">Per creare un pacchetto per i file da una configurazione della build differente, ad esempio *Release*, usare l'opzione `-properties` con la configurazione:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-318">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="bbeeb-319">**Simboli**: per includere i simboli che consentono agli utenti di eseguire il codice del pacchetto un'istruzione alla volta nel debugger, usare l'opzione `-Symbols`:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-319">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="bbeeb-320">Test dell'installazione pacchetto</span><span class="sxs-lookup"><span data-stu-id="bbeeb-320">Testing package installation</span></span>

<span data-ttu-id="bbeeb-321">Prima di pubblicare un pacchetto, in genere si preferisce testarne il processo di installazione in un progetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-321">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="bbeeb-322">I test assicurano che i file necessari vengano inseriti nei percorsi corretti all'interno del progetto.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-322">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="bbeeb-323">È possibile testare manualmente le installazioni in Visual Studio o dalla riga di comando seguendo i normali [passaggi di installazione del pacchetto](../consume-packages/ways-to-install-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-323">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/ways-to-install-a-package.md).</span></span>

<span data-ttu-id="bbeeb-324">Per i test automatizzati, il processo di base è il seguente:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-324">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="bbeeb-325">Copiare il file `.nupkg` in una cartella locale.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-325">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="bbeeb-326">Aggiungere la cartella alle origini del pacchetto usando il comando `nuget sources add -name <name> -source <path>`. Vedere [nuget sources](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-326">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="bbeeb-327">Si noti che è necessario impostare l'origine locale solo una volta in ogni computer.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-327">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="bbeeb-328">Installare il pacchetto da tale origine usando `nuget install <packageID> -source <name>` dove `<name>` corrisponde al nome dell'origine specificata in `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-328">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="bbeeb-329">Specificando l'origine, il pacchetto viene con certezza installato solo da tale origine.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-329">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="bbeeb-330">Esaminare il file system per controllare che i file siano installati correttamente.</span><span class="sxs-lookup"><span data-stu-id="bbeeb-330">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbeeb-331">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bbeeb-331">Next Steps</span></span>

<span data-ttu-id="bbeeb-332">Dopo aver creato un pacchetto, ovvero un file `.nupkg`, è possibile pubblicarlo nella raccolta di propria scelta, come descritto in [Pubblicazione di un pacchetto](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="bbeeb-332">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="bbeeb-333">Potrebbe anche essere necessario estendere le funzionalità del pacchetto o supportare altri scenari, come descritto negli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-333">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="bbeeb-334">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="bbeeb-334">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="bbeeb-335">Supporto di più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="bbeeb-335">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="bbeeb-336">Trasformazioni di file di origine e di configurazione</span><span class="sxs-lookup"><span data-stu-id="bbeeb-336">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="bbeeb-337">Localizzazione</span><span class="sxs-lookup"><span data-stu-id="bbeeb-337">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="bbeeb-338">Versioni non definitive</span><span class="sxs-lookup"><span data-stu-id="bbeeb-338">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="bbeeb-339">Sono infine disponibili altri tipi di pacchetti da tenere presenti:</span><span class="sxs-lookup"><span data-stu-id="bbeeb-339">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="bbeeb-340">Pacchetti nativi</span><span class="sxs-lookup"><span data-stu-id="bbeeb-340">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="bbeeb-341">Pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="bbeeb-341">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
