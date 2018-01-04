---
title: Creare pacchetti NuGet di .NET Standard 2.0 con Visual Studio 2017 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: Procedura dettagliata end-to-end per la creazione di pacchetti NuGet di .NET Standard 2.0 con NuGet 4.x e Visual Studio 2017.
keywords: creare un pacchetto, pacchetti .NET Standard, .NET Core
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82e413119b12503336becd6019e4fa3e4ac0b1f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a><span data-ttu-id="73cfd-104">Creare pacchetti .NET Standard 2.0 con Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="73cfd-104">Create .NET Standard 2.0 packages with Visual Studio 2017</span></span>

<span data-ttu-id="73cfd-105">*Si applica a NuGet 4.x+ e MSBuild 15.3+ forniti con Visual Studio 2017 Update 3. Per le versioni precedenti di Visual Studio 2017, queste istruzioni si applicano a .NET Standard da 1.4 a 1.6 modificando la proprietà \<TargetFramework\>. Per usare NuGet 3.x+, vedere [Creare pacchetti .NET Standard con Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span><span class="sxs-lookup"><span data-stu-id="73cfd-105">*Applies to NuGet 4.x+ and MSBuild 15.3+ as provided with Visual Studio 2017 Update 3. For earlier versions of Visual Studio 2017, these instructions apply to .NET Standard 1.4 to 1.6 by changing the \<TargetFramework\> property. Also see [Create .NET Standard Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) for working with NuGet 3.x+.*</span></span>

<span data-ttu-id="73cfd-106">La [libreria .NET Standard](https://docs.microsoft.com/dotnet/articles/standard/library) è una specifica formale delle API .NET che devono essere disponibili in tutti i runtime .NET, per creare in questo modo maggiore uniformità nell'ecosistema .NET.</span><span class="sxs-lookup"><span data-stu-id="73cfd-106">The [.NET Standard Library](https://docs.microsoft.com/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="73cfd-107">La libreria .NET Standard definisce un set uniforme di API della libreria di classi base per tutte le piattaforme .NET da implementare, indipendentemente dal carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="73cfd-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="73cfd-108">Consente agli sviluppatori di produrre PCL che possono essere usate in tutti i runtime .NET e riduce, se non elimina, le direttive di compilazione condizionale specifiche della piattaforma nel codice condiviso.</span><span class="sxs-lookup"><span data-stu-id="73cfd-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="73cfd-109">Questa guida illustra la creazione di un pacchetto nuget per la libreria .NET Standard 2.0 con Visual Studio 2017 Update 3 e NuGet 4.0.</span><span class="sxs-lookup"><span data-stu-id="73cfd-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 2.0 with Visual Studio 2017 Update 3 and NuGet 4.0.</span></span>

1. [<span data-ttu-id="73cfd-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="73cfd-110">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="73cfd-111">Creare il progetto di libreria di classi</span><span class="sxs-lookup"><span data-stu-id="73cfd-111">Create the class library project</span></span>](#create-the-netstandard-class-library-project)
1. [<span data-ttu-id="73cfd-112">Modificare i metadati nel file con estensione csproj</span><span class="sxs-lookup"><span data-stu-id="73cfd-112">Edit metadata in the .csproj file</span></span>](#edit-metadata-in-the-csproj-file)
1. [<span data-ttu-id="73cfd-113">Creare un pacchetto per il componente</span><span class="sxs-lookup"><span data-stu-id="73cfd-113">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="73cfd-114">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="73cfd-114">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="73cfd-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="73cfd-115">Pre-requisites</span></span>

<span data-ttu-id="73cfd-116">Per questa procedura dettagliata è necessario Visual Studio 2017 Update 3 con il carico di lavoro **Sviluppo multipiattaforma .NET Core**.</span><span class="sxs-lookup"><span data-stu-id="73cfd-116">This walkthrough requires Visual Studio 2017 Update 3 with the **.NET Core cross-platform development** workload.</span></span> <span data-ttu-id="73cfd-117">È possibile installare l'edizione Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/) o usare le edizioni Professional ed Enterprise.</span><span class="sxs-lookup"><span data-stu-id="73cfd-117">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/), or use the Professional and Enterprise editions.</span></span>

<span data-ttu-id="73cfd-118">Il carico di lavoro necessario viene visualizzato come segue nel programma di installazione di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="73cfd-118">The require workload appears as follows in the Visual Studio installer:</span></span>

![Carico di lavoro Sviluppo multipiattaforma .NET Core nel programma di installazione di Visual Studio](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a><span data-ttu-id="73cfd-120">Creare il nuovo progetto di libreria di classi .NET Standard</span><span class="sxs-lookup"><span data-stu-id="73cfd-120">Create the .NET Standard class library project</span></span>

1. <span data-ttu-id="73cfd-121">In Visual Studio **File > Nuovo > Progetto**, espandere il nodo **Visual C# > .NET Standard**, selezionare **Class Library (Net Standard)** (Libreria di classi - .Net Standard), modificare il nome in AppLogger e fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="73cfd-121">In Visual Studio, **File > New > Project**, expand the **Visual C# > .NET Standard** node, select **Class Library (Net Standard)**, change the name to AppLogger, and click OK.</span></span>

    ![Creare il nuovo progetto di libreria di classi](media/NuGet4-02-NewProject.png)

1. <span data-ttu-id="73cfd-123">Impostare la configurazione della build su **Release**.</span><span class="sxs-lookup"><span data-stu-id="73cfd-123">Change the build configuration to **Release**.</span></span>
1. <span data-ttu-id="73cfd-124">Fare clic con il pulsante destro del mouse sul progetto `AppLogger` in Esplora soluzioni, scegliere **Proprietà**, selezionare la scheda **Compilazione**, selezionare la casella per **File di documentazione XML** e impostare il nome file su `AppLogger.xml`,</span><span class="sxs-lookup"><span data-stu-id="73cfd-124">Right-click the `AppLogger` project in Solution Explorer, select **Properties**, select the **Build** tab, check the box for **XML documentation file**, and set the filename to just `AppLogger.xml`.</span></span> <span data-ttu-id="73cfd-125">quindi salvare il progetto.</span><span class="sxs-lookup"><span data-stu-id="73cfd-125">Then save the project.</span></span>

1. <span data-ttu-id="73cfd-126">Aggiungere il codice al componente, ad esempio il seguente (che chiaramente visualizza solo i messaggi nella console):</span><span class="sxs-lookup"><span data-stu-id="73cfd-126">Add your code to the component, such as the following (which clearly just outputs messages to the console):</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. <span data-ttu-id="73cfd-127">Compilare il progetto (con la configurazione Release) e controllare che nella cartella `bin\Release\netstandard2.0` vengano creati i file DLL e XML.</span><span class="sxs-lookup"><span data-stu-id="73cfd-127">Build the project (with the Release configuration) and check that DLL and XML files are produced within the `bin\Release\netstandard2.0` folder.</span></span>

## <a name="edit-metadata-in-the-csproj-file"></a><span data-ttu-id="73cfd-128">Modificare i metadati nel file con estensione csproj</span><span class="sxs-lookup"><span data-stu-id="73cfd-128">Edit metadata in the .csproj file</span></span>

<span data-ttu-id="73cfd-129">Con i progetti NuGet 4.0 e .NET Core, i metadati del pacchetto sono contenuti direttamente nel file `.csproj` invece che in file esterni, ad esempio `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="73cfd-129">With NuGet 4.0 and .NET Core projects, package metadata is contained directly in the `.csproj` file instead of external files such as a `.nuspec`.</span></span> <span data-ttu-id="73cfd-130">Per una descrizione completa di tali metadati, vedere [Pack e restore di NuGet come destinazioni MSBuild](../schema/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="73cfd-130">A full description of that metadata is found in [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

1. <span data-ttu-id="73cfd-131">Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni, scegliere **Modifica AppLogger.csproj** e quindi modificare il primo gruppo di proprietà per includere le informazioni sul pacchetto, ad esempio le seguenti:</span><span class="sxs-lookup"><span data-stu-id="73cfd-131">Right-click the project in Solution Explorer, select **Edit AppLogger.csproj**, and then edit the first property group to include package information such as the following:</span></span>

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. <span data-ttu-id="73cfd-132">Salvare il progetto, quindi fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Compila soluzione** per generare nuovamente tutti i file per il pacchetto, questa volta con i metadati corretti.</span><span class="sxs-lookup"><span data-stu-id="73cfd-132">Save the project, then right-click the solution and select **Build Solution** to again generate all the files for the package, this time with the correct metadata.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="73cfd-133">Creare un pacchetto per il componente</span><span class="sxs-lookup"><span data-stu-id="73cfd-133">Package the component</span></span>

<span data-ttu-id="73cfd-134">NuGet 4.0 supporta una destinazione pack tramite MSBuild versione 15.1+ (incluso MSBuild 15.3 come parte di Visual Studio 2017 Update 3) quando il progetto contiene i metadati del pacchetto necessari, aggiunti nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="73cfd-134">NuGet 4.0 supports a pack target using MSBuild version 15.1+ (including MSBuild 15.3 as part of Visual Studio 2017 Update 3) when the project contains the necessary package metadata, as was added in the previous section.</span></span> <span data-ttu-id="73cfd-135">Per richiamare MSBuild in questo modo, è sufficiente specificare nella riga di comando la destinazione pack nella stessa cartella del file `.csproj`:</span><span class="sxs-lookup"><span data-stu-id="73cfd-135">To invoke MSBuild in this way, simply specify the pack target on the command line in the same folder as the `.csproj` file:</span></span>

    msbuild /t:pack /p:Configuration=Release

<span data-ttu-id="73cfd-136">Per opzioni aggiuntive con `msbuild /t:pack`, inclusi ad esempio i file di contenuto, i simboli e il codice sorgente, vedere [Pack e restore di NuGet come destinazioni MSBuild](../schema/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="73cfd-136">For additional options with `msbuild /t:pack`, such as including content files, symbols, and source code, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

<span data-ttu-id="73cfd-137">In ogni caso, il comando precedente genera `AppLogger.YOUR_NAME.1.0.0.nupkg` nella cartella `bin\Release` per impostazione predefinita, perché compila tale configurazione.</span><span class="sxs-lookup"><span data-stu-id="73cfd-137">In any case, the command above generates `AppLogger.YOUR_NAME.1.0.0.nupkg` in the `bin\Release` folder by default, as it builds that configuration.</span></span> <span data-ttu-id="73cfd-138">Se si omette l'opzione `/p`, la configurazione predefinita sarà `Debug`.</span><span class="sxs-lookup"><span data-stu-id="73cfd-138">If you omit the `/p` switch, the default configuration will be `Debug`.</span></span> 

<span data-ttu-id="73cfd-139">Aprendo il file in uno strumento come [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ed espandendo tutti i nodi, verranno visualizzati i contenuti seguenti:</span><span class="sxs-lookup"><span data-stu-id="73cfd-139">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![NuGet Package Explorer che visualizza il pacchetto AppLogger](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="73cfd-141">Un file `.nupkg` è solo un file ZIP con un'estensione diversa.</span><span class="sxs-lookup"><span data-stu-id="73cfd-141">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="73cfd-142">È anche possibile esaminare i contenuti del pacchetto, modificando `.nupkg` in `.zip`, ma si ricordi di ripristinare l'estensione prima di caricare un pacchetto in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="73cfd-142">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="73cfd-143">Per rendere disponibile il pacchetto per altri sviluppatori, seguire le istruzioni in [Pubblicare un pacchetto](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="73cfd-143">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="73cfd-144">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="73cfd-144">Related topics</span></span>

- <span data-ttu-id="73cfd-145">[Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md) contiene tutti i dettagli della descrizione del pacchetto direttamente nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="73cfd-145">[Package References in Project Files](../consume-packages/package-references-in-project-files.md) describes all the details of describing your package directly in the project file.</span></span>
- <span data-ttu-id="73cfd-146">[Pack e restore di NuGet come destinazioni MSBuild](../schema/msbuild-targets.md) descrive tutte le opzioni per l'uso di `msbuild /t:pack` per creare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="73cfd-146">[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md) describes all the options for using `msbuild /t:pack` to create the package.</span></span>
- [<span data-ttu-id="73cfd-147">Documentazione della libreria .NET Standard</span><span class="sxs-lookup"><span data-stu-id="73cfd-147">.NET Standard Library documentation</span></span>](https://docs.microsoft.com/dotnet/articles/standard/library)
- [<span data-ttu-id="73cfd-148">Portabilità in .NET Core da .NET Framework</span><span class="sxs-lookup"><span data-stu-id="73cfd-148">Porting to .NET Core from .NET Framework</span></span>](https://docs.microsoft.com/dotnet/articles/core/porting/index)
