---
title: Creare pacchetti NuGet di .NET Standard con Visual Studio 2015 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: Procedura dettagliata end-to-end per la creazione di pacchetti NuGet di .NET Standard con NuGet 3.x e Visual Studio 2015.
keywords: creare un pacchetto, pacchetti .NET Standard, tabella di mapping .NET Standard
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e02888bf552997afe25e967f13e021e78e40d48d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="ccd99-104">Creare pacchetti .NET Standard con Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="ccd99-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="ccd99-105">*Si applica a NuGet 3.x. Per usare NuGet 4.x+, vedere [Creare pacchetti .NET Standard con Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md).*</span><span class="sxs-lookup"><span data-stu-id="ccd99-105">*Applies to NuGet 3.x. See [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="ccd99-106">La [libreria .NET Standard](/dotnet/articles/standard/library) è una specifica formale delle API .NET che devono essere disponibili in tutti i runtime .NET, per creare in questo modo maggiore uniformità nell'ecosistema .NET.</span><span class="sxs-lookup"><span data-stu-id="ccd99-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="ccd99-107">La libreria .NET Standard definisce un set uniforme di API della libreria di classi base per tutte le piattaforme .NET da implementare, indipendentemente dal carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ccd99-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="ccd99-108">Consente agli sviluppatori di produrre PCL che possono essere usate in tutti i runtime .NET e riduce, se non elimina, le direttive di compilazione condizionale specifiche della piattaforma nel codice condiviso.</span><span class="sxs-lookup"><span data-stu-id="ccd99-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="ccd99-109">Questa guida illustra la creazione di un pacchetto nuget per la libreria .NET Standard 1.4,</span><span class="sxs-lookup"><span data-stu-id="ccd99-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="ccd99-110">che funzionerà in .NET Framework 4.6.1, nella piattaforma UWP (Universal Windows Platform) 10, in .NET Core e in Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="ccd99-110">This will work across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="ccd99-111">Per informazioni dettagliate, vedere la [tabella di mapping .NET Standard](#net-standard-mapping-table) più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="ccd99-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

1. [<span data-ttu-id="ccd99-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ccd99-112">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="ccd99-113">Creare il progetto di libreria di classi</span><span class="sxs-lookup"><span data-stu-id="ccd99-113">Create the class library project</span></span>](#create-the-class-library-project)
1. [<span data-ttu-id="ccd99-114">Creare e aggiornare il file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="ccd99-114">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="ccd99-115">Creare un pacchetto per il componente</span><span class="sxs-lookup"><span data-stu-id="ccd99-115">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="ccd99-116">Opzioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ccd99-116">Additional options</span></span>](#additional-options)
1. [<span data-ttu-id="ccd99-117">Tabella di mapping .NET Standard</span><span class="sxs-lookup"><span data-stu-id="ccd99-117">.NET Standard mapping table</span></span>](#net-standard-mapping-table)
1. [<span data-ttu-id="ccd99-118">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="ccd99-118">Related topics</span></span>](#related-topics)


## <a name="pre-requisites"></a><span data-ttu-id="ccd99-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ccd99-119">Pre-requisites</span></span>

1. <span data-ttu-id="ccd99-120">Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="ccd99-120">Visual Studio 2015.</span></span> <span data-ttu-id="ccd99-121">Installare l'edizione Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/). È anche possibile usare le edizioni Professional ed Enterprise.</span><span class="sxs-lookup"><span data-stu-id="ccd99-121">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span>
1. <span data-ttu-id="ccd99-122">.NET Core: installare .NET Core con gli altri modelli e strumenti per Visual Studio 2015 da [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span><span class="sxs-lookup"><span data-stu-id="ccd99-122">.NET Core: Install .NET Core along with templates and other tools for Visual Studio 2015 from [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span></span>
1. <span data-ttu-id="ccd99-123">Interfaccia della riga di comando di NuGet.</span><span class="sxs-lookup"><span data-stu-id="ccd99-123">NuGet CLI.</span></span> <span data-ttu-id="ccd99-124">Scaricare la versione più recente di nuget.exe da [nuget.org/downloads](https://nuget.org/downloads), salvandola in una posizione di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="ccd99-124">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="ccd99-125">Aggiungere quindi tale posizione alla variabile di ambiente PATH, se necessario.</span><span class="sxs-lookup"><span data-stu-id="ccd99-125">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="ccd99-126">Poiché nuget.exe è di per sé lo strumento dell'interfaccia della riga di comando e non un programma di installazione, assicurarsi di salvare il file scaricato dal browser invece di eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="ccd99-126">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>



## <a name="create-the-class-library-project"></a><span data-ttu-id="ccd99-127">Creare il progetto di libreria di classi</span><span class="sxs-lookup"><span data-stu-id="ccd99-127">Create the class library project</span></span>

1. <span data-ttu-id="ccd99-128">In Visual Studio **File > Nuovo > Progetto**, espandere il nodo **Visual C# > Windows**, selezionare **Libreria di classi (portabile)**, modificare il nome in AppLogger e fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="ccd99-128">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![Creare il nuovo progetto di libreria di classi](media/NetStandard-NewProject.png)

1. <span data-ttu-id="ccd99-130">Nella finestra di dialogo **Aggiungi libreria di classi portabile** visualizzata selezionare le opzioni `.NET Framework 4.6` e `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="ccd99-130">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>
1. <span data-ttu-id="ccd99-131">Fare clic con il pulsante destro del mouse su `AppLogger (Portable)` in Esplora soluzioni, scegliere **Proprietà**, selezionare la scheda **Libreria**, quindi fare clic su **Imposta come destinazione la piattaforma standard .NET** nella sezione **Destinazione**.</span><span class="sxs-lookup"><span data-stu-id="ccd99-131">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="ccd99-132">Verrà chiesta una conferma e quindi sarà possibile scegliere `.NET Standard 1.4` nell'elenco a discesa:</span><span class="sxs-lookup"><span data-stu-id="ccd99-132">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![Impostazione della destinazione su .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="ccd99-134">Fare clic sulla scheda **Compilazione**, impostare **Configurazione** su `Release` e selezionare la casella **File di documentazione XML**.</span><span class="sxs-lookup"><span data-stu-id="ccd99-134">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>
1. <span data-ttu-id="ccd99-135">Aggiungere il codice al componente, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ccd99-135">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. <span data-ttu-id="ccd99-136">Compilare il progetto (con la configurazione Release) e controllare che nella cartella bin\Release vengano creati i file DLL e XML.</span><span class="sxs-lookup"><span data-stu-id="ccd99-136">Build the project (with the Release configuration) and check that DLL and XML files are produced within the bin\Release folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="ccd99-137">Creare e aggiornare il file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="ccd99-137">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="ccd99-138">Aprire un prompt dei comandi, passare alla cartella contenente la cartella `AppLogg.csproj` (di un livello inferiore rispetto alla posizione del file `.sln`) ed eseguire il comando `spec` di NuGet per creare il file `AppLogger.nuspec` iniziale:</span><span class="sxs-lookup"><span data-stu-id="ccd99-138">Open a command prompt, navigate to the folder containing `AppLogg.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

```
nuget spec
```

1. <span data-ttu-id="ccd99-139">Aprire `AppLogger.nuspec` in un editor e aggiornarlo in modo che corrisponda a quanto segue, sostituendo YOUR_NAME con un valore appropriato.</span><span class="sxs-lookup"><span data-stu-id="ccd99-139">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="ccd99-140">Il valore `<id>`, in particolare, deve essere univoco in nuget.org. Vedere le convenzioni di denominazione descritte in [Creazione di un pacchetto](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="ccd99-140">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="ccd99-141">Tenere inoltre presente che è anche necessario aggiornare i tag relativi all'autore e alla descrizione o si verificherà un errore durante il passaggio di creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ccd99-141">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>AppLogger.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>AppLogger</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. <span data-ttu-id="ccd99-142">Aggiungere gli assembly di riferimento al file `.nuspec`, in particolare la DLL della libreria e il file XML IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="ccd99-142">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="ccd99-143">Fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Compila soluzione** per generare tutti i file per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ccd99-143">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="ccd99-144">Creare un pacchetto per il componente</span><span class="sxs-lookup"><span data-stu-id="ccd99-144">Package the component</span></span>

<span data-ttu-id="ccd99-145">Dopo avere completato il file `.nuspec` che fa riferimento a tutti i file da includere nel pacchetto, è possibile eseguire il comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="ccd99-145">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack AppLogger.nuspec
```

<span data-ttu-id="ccd99-146">Verrà generato `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="ccd99-146">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="ccd99-147">Aprendo il file in uno strumento come [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ed espandendo tutti i nodi, verranno visualizzati i contenuti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ccd99-147">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![NuGet Package Explorer che visualizza il pacchetto AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="ccd99-149">Un file `.nupkg` è solo un file ZIP con un'estensione diversa.</span><span class="sxs-lookup"><span data-stu-id="ccd99-149">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="ccd99-150">È anche possibile esaminare i contenuti del pacchetto, modificando `.nupkg` in `.zip`, ma si ricordi di ripristinare l'estensione prima di caricare un pacchetto in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ccd99-150">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="ccd99-151">Per rendere disponibile il pacchetto per altri sviluppatori, seguire le istruzioni in [Pubblicare un pacchetto](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="ccd99-151">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="ccd99-152">Si noti che `pack` richiede Mono 4.4.2 su Mac OS X e non funziona nei sistemi Linux.</span><span class="sxs-lookup"><span data-stu-id="ccd99-152">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="ccd99-153">In un Mac è anche necessario convertire i nomi di percorso di Windows nel file `.nuspec` in percorsi di tipo Unix.</span><span class="sxs-lookup"><span data-stu-id="ccd99-153">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="additional-options"></a><span data-ttu-id="ccd99-154">Opzioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ccd99-154">Additional options</span></span>

<span data-ttu-id="ccd99-155">Le sezioni seguenti illustrano le opzioni aggiuntive per la creazione del pacchetto NuGet:</span><span class="sxs-lookup"><span data-stu-id="ccd99-155">The following sections go into additional options for NuGet package creation:</span></span>

- [<span data-ttu-id="ccd99-156">Dichiarazione delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="ccd99-156">Declaring dependencies</span></span>](#declaring-dependencies)
- [<span data-ttu-id="ccd99-157">Supporto di più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="ccd99-157">Supporting multiple target frameworks</span></span>](#supporting-multiple-target-frameworks)
- [<span data-ttu-id="ccd99-158">Aggiunta di destinazioni e proprietà per MSBuild</span><span class="sxs-lookup"><span data-stu-id="ccd99-158">Adding targets and props for MSBuild</span></span>](#adding-targets-and-props-for-msbuild)
- [<span data-ttu-id="ccd99-159">Creazione di pacchetti localizzati</span><span class="sxs-lookup"><span data-stu-id="ccd99-159">Creating localized packages</span></span>](#creating-localized-packages)
- [<span data-ttu-id="ccd99-160">Aggiunta di un file leggimi</span><span class="sxs-lookup"><span data-stu-id="ccd99-160">Adding a readme</span></span>](#adding-a-readme)

### <a name="declaring-dependencies"></a><span data-ttu-id="ccd99-161">Dichiarazione delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="ccd99-161">Declaring dependencies</span></span>

<span data-ttu-id="ccd99-162">Se sono presenti dipendenze da altri pacchetti NuGet, elencarle nell'elemento `<dependencies>` con gli elementi `<group>`.</span><span class="sxs-lookup"><span data-stu-id="ccd99-162">If you have any dependencies on other NuGet packages, list those in the `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="ccd99-163">Ad esempio, per dichiarare una dipendenza da NewtonSoft.Json 8.0.3 o versione successiva, aggiungere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="ccd99-163">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="ccd99-164">La sintassi dell'attributo *version* qui indica che la versione 8.0.3 o successiva è accettabile.</span><span class="sxs-lookup"><span data-stu-id="ccd99-164">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="ccd99-165">Per specificare intervalli di versioni diversi, vedere [Controllo delle versioni dei pacchetti](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="ccd99-165">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="supporting-multiple-target-frameworks"></a><span data-ttu-id="ccd99-166">Supporto di più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="ccd99-166">Supporting multiple target frameworks</span></span>

<span data-ttu-id="ccd99-167">Si supponga di voler sfruttare un'API in .NET Framework 4.6.2 non disponibile in .NET Standard 1.4.</span><span class="sxs-lookup"><span data-stu-id="ccd99-167">Suppose you'd like to take advantage of an API in .NET Framework 4.6.2 that is not available in .NET Standard 1.4.</span></span> <span data-ttu-id="ccd99-168">A questo scopo, prima di tutto sarà necessario verificare che la libreria esegua la compilazione per .NET 4.6.2 usando la compilazione condizionale o progetti condivisi.</span><span class="sxs-lookup"><span data-stu-id="ccd99-168">To do this, you'll first need to make sure the library compiles for .NET 4.6.2 by using conditional compilation or shared projects.</span></span> <span data-ttu-id="ccd99-169">In Visual Studio è possibile creare un progetto NetCore, aggiungere il framework scelto alla sezione dei framework multipli e quindi eseguire la compilazione. Si crea quindi il pacchetto usando la semplice tecnica della directory di lavoro basata sulle convenzioni:</span><span class="sxs-lookup"><span data-stu-id="ccd99-169">(In Visual Studio, you can create a NetCore project, add the framework of choice to the multiple framework section, and then build.) Then you create the package using the simple convention-based working directory technique as follows:</span></span>

1. <span data-ttu-id="ccd99-170">Nella cartella radice del progetto contenente il file `.nuspec` creare una cartella denominata `lib`.</span><span class="sxs-lookup"><span data-stu-id="ccd99-170">In the project's root folder containing your `.nuspec` file, create a folder named `lib`.</span></span>
1. <span data-ttu-id="ccd99-171">In `lib` creare cartelle per ogni piattaforma che si vuole supportare:</span><span class="sxs-lookup"><span data-stu-id="ccd99-171">Inside `lib`, create folders for each platform you want to support:</span></span>

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. <span data-ttu-id="ccd99-172">Nel file `.nuspec` aggiungere un nodo `files` sotto il nodo `package` e fare riferimento ai file in `lib` usando i caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="ccd99-172">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `lib` using wildcards.</span></span> <span data-ttu-id="ccd99-173">**Nota:** poiché le sostituzioni dei token non sono supportate con l'approccio della directory di lavoro basata sulle convenzioni, sostituirli con valori letterali:</span><span class="sxs-lookup"><span data-stu-id="ccd99-173">**Note:** Token replacements are not supported with the convention-based working directory approach, so replace them with literal values:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="ccd99-174">Creare di nuovo il pacchetto usando `nuget pack AppLogger.spec`.</span><span class="sxs-lookup"><span data-stu-id="ccd99-174">Create the package again using `nuget pack AppLogger.spec`.</span></span>

<span data-ttu-id="ccd99-175">Per altre informazioni dettagliate sull'uso di questa tecnica, vedere [Supporto di più versioni di .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)</span><span class="sxs-lookup"><span data-stu-id="ccd99-175">For more details on using this technique, see [Supporting Multiple .NET Framework Versions](../create-packages/supporting-multiple-target-frameworks.md)</span></span>

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="ccd99-176">Aggiunta di destinazioni e proprietà per MSBuild</span><span class="sxs-lookup"><span data-stu-id="ccd99-176">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="ccd99-177">In alcuni casi potrebbe essere necessario aggiungere destinazioni o proprietà di compilazione personalizzata nei progetti che utilizzano il pacchetto, ad esempio l'esecuzione di uno strumento o processo personalizzato durante la compilazione.</span><span class="sxs-lookup"><span data-stu-id="ccd99-177">In some cases you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="ccd99-178">A questo scopo, si aggiungono i file in una cartella `\build`, come illustrato nei passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="ccd99-178">You do this by adding files in a `\build` folder as described in the steps below.</span></span> <span data-ttu-id="ccd99-179">Quando NuGet installa un pacchetto con i file di \build, aggiunge un elemento di MSBuild nel file di progetto che punta ai file con estensione targets e props.</span><span class="sxs-lookup"><span data-stu-id="ccd99-179">When NuGet installs a package with \build files, it adds an MSBuild element in the project file pointing to the .targets and .props files.</span></span>

> [!Note]
> <span data-ttu-id="ccd99-180">Quando si usa `project.json`, le destinazioni non vengono aggiunte al progetto, ma vengono rese disponibili tramite `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="ccd99-180">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>


1. <span data-ttu-id="ccd99-181">Nella cartella del progetto contenente il file `.nuspec` creare una cartella denominata `build`.</span><span class="sxs-lookup"><span data-stu-id="ccd99-181">In the project folder containing the your `.nuspec` file, create a folder named `build`.</span></span>
1. <span data-ttu-id="ccd99-182">In `build` creare cartelle per ogni piattaforma supportata, in cui inserire i file `.targets` e `.props`:</span><span class="sxs-lookup"><span data-stu-id="ccd99-182">Inside `build`, create folders for each supported, and within those place your `.targets` and `.props` files:</span></span>

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. <span data-ttu-id="ccd99-183">Nel file `.nuspec` aggiungere un nodo `files` sotto il nodo `package` e fare riferimento ai file in `build` usando i caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="ccd99-183">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `build` using wildcards.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. <span data-ttu-id="ccd99-184">Creare di nuovo il pacchetto usando `nuget pack AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="ccd99-184">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>

<span data-ttu-id="ccd99-185">Per altre informazioni dettagliate, vedere [Includere proprietà e destinazioni MSBuild in un pacchetto](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="ccd99-185">For additional details, refer to [Include MSBuild props and targets in a package](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span></span>


### <a name="creating-localized-packages"></a><span data-ttu-id="ccd99-186">Creazione di pacchetti localizzati</span><span class="sxs-lookup"><span data-stu-id="ccd99-186">Creating localized packages</span></span>

<span data-ttu-id="ccd99-187">Per creare le versioni localizzate della libreria, è possibile creare pacchetti separati per le diverse impostazioni locali o includere gli assembly di risorse localizzate in un singolo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ccd99-187">To create localized versions of your library, you can either create separate packages for different locales, or include localized resource assemblies within a single package.</span></span> <span data-ttu-id="ccd99-188">Ecco come mettere in pratica quest'ultimo approccio per tedesco e italiano:</span><span class="sxs-lookup"><span data-stu-id="ccd99-188">Here's how to do the latter approach for German and Italian:</span></span>

1. <span data-ttu-id="ccd99-189">In ogni cartella del framework di destinazione sotto `lib`, creare cartelle per ogni lingua supportata diversa dall'inglese predefinito.</span><span class="sxs-lookup"><span data-stu-id="ccd99-189">Within each target framework folder under `lib`, create folders for each supported language other than the English default.</span></span> <span data-ttu-id="ccd99-190">In queste cartelle è possibile inserire assembly di risorse e file XML IntelliSense localizzati.</span><span class="sxs-lookup"><span data-stu-id="ccd99-190">In these folders you can place resource assemblies  and localized IntelliSense XML files.</span></span> <span data-ttu-id="ccd99-191">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ccd99-191">For example:</span></span>

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. <span data-ttu-id="ccd99-192">Nel file `.nuspec` fare riferimento a questi file nel nodo `<files>`:</span><span class="sxs-lookup"><span data-stu-id="ccd99-192">In the `.nuspec` file, reference these files in the `<files>` node:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="ccd99-193">Creare di nuovo il pacchetto usando `nuget pack AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="ccd99-193">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>


### <a name="adding-a-readme"></a><span data-ttu-id="ccd99-194">Aggiunta di un file leggimi</span><span class="sxs-lookup"><span data-stu-id="ccd99-194">Adding a readme</span></span>

<span data-ttu-id="ccd99-195">Quando si include un file `readme.txt` nella radice del pacchetto, Visual Studio lo visualizza quando il pacchetto viene installato direttamente.</span><span class="sxs-lookup"><span data-stu-id="ccd99-195">When you include a `readme.txt` file in the root of the package, Visual Studio will display it when the package is installed directly.</span></span>

> [!Note]
> <span data-ttu-id="ccd99-196">I file leggimi non vengono visualizzati per i pacchetti installati come dipendenza o per i progetti .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ccd99-196">Readme files are not shown for packages that are installed as a dependency, or for .NET Core projects.</span></span>


<span data-ttu-id="ccd99-197">A questo scopo, creare il file `readme.txt`, inserirlo nella cartella radice del progetto e farvi riferimento nel file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="ccd99-197">To do this, create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```


## <a name="net-standard-mapping-table"></a><span data-ttu-id="ccd99-198">Tabella di mapping .NET Standard</span><span class="sxs-lookup"><span data-stu-id="ccd99-198">.NET Standard mapping table</span></span>

|<span data-ttu-id="ccd99-199">Nome della piattaforma</span><span class="sxs-lookup"><span data-stu-id="ccd99-199">Platform Name</span></span> |<span data-ttu-id="ccd99-200">Alias</span><span class="sxs-lookup"><span data-stu-id="ccd99-200">Alias</span></span>|
|--------------|-----|
|<span data-ttu-id="ccd99-201">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="ccd99-201">.NET Standard</span></span> | <span data-ttu-id="ccd99-202">netstandard</span><span class="sxs-lookup"><span data-stu-id="ccd99-202">netstandard</span></span>| <span data-ttu-id="ccd99-203">1.0</span><span class="sxs-lookup"><span data-stu-id="ccd99-203">1.0</span></span>| <span data-ttu-id="ccd99-204">1.1</span><span class="sxs-lookup"><span data-stu-id="ccd99-204">1.1</span></span>| <span data-ttu-id="ccd99-205">1.2</span><span class="sxs-lookup"><span data-stu-id="ccd99-205">1.2</span></span>| <span data-ttu-id="ccd99-206">1.3</span><span class="sxs-lookup"><span data-stu-id="ccd99-206">1.3</span></span>| <span data-ttu-id="ccd99-207">1.4</span><span class="sxs-lookup"><span data-stu-id="ccd99-207">1.4</span></span>| <span data-ttu-id="ccd99-208">1,5</span><span class="sxs-lookup"><span data-stu-id="ccd99-208">1.5</span></span>| <span data-ttu-id="ccd99-209">1.6</span><span class="sxs-lookup"><span data-stu-id="ccd99-209">1.6</span></span>|
|<span data-ttu-id="ccd99-210">.NET Core</span><span class="sxs-lookup"><span data-stu-id="ccd99-210">.NET Core</span></span> | <span data-ttu-id="ccd99-211">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="ccd99-211">netcoreapp</span></span>| <span data-ttu-id="ccd99-212">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-212">&#x2192;</span></span>| <span data-ttu-id="ccd99-213">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-213">&#x2192;</span></span>| <span data-ttu-id="ccd99-214">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-214">&#x2192;</span></span>| <span data-ttu-id="ccd99-215">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-215">&#x2192;</span></span>| <span data-ttu-id="ccd99-216">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-216">&#x2192;</span></span>| <span data-ttu-id="ccd99-217">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-217">&#x2192;</span></span>| <span data-ttu-id="ccd99-218">1.0</span><span class="sxs-lookup"><span data-stu-id="ccd99-218">1.0</span></span>|
|<span data-ttu-id="ccd99-219">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="ccd99-219">.NET Framework</span></span>| <span data-ttu-id="ccd99-220">net</span><span class="sxs-lookup"><span data-stu-id="ccd99-220">net</span></span>| <span data-ttu-id="ccd99-221">4.5</span><span class="sxs-lookup"><span data-stu-id="ccd99-221">4.5</span></span>| <span data-ttu-id="ccd99-222">4.5.1</span><span class="sxs-lookup"><span data-stu-id="ccd99-222">4.5.1</span></span>| <span data-ttu-id="ccd99-223">4.6</span><span class="sxs-lookup"><span data-stu-id="ccd99-223">4.6</span></span>| <span data-ttu-id="ccd99-224">4.6.1</span><span class="sxs-lookup"><span data-stu-id="ccd99-224">4.6.1</span></span>| <span data-ttu-id="ccd99-225">4.6.2</span><span class="sxs-lookup"><span data-stu-id="ccd99-225">4.6.2</span></span>| <span data-ttu-id="ccd99-226">4.6.3</span><span class="sxs-lookup"><span data-stu-id="ccd99-226">4.6.3</span></span>|
|<span data-ttu-id="ccd99-227">Piattaforme Mono/Xamarin</span><span class="sxs-lookup"><span data-stu-id="ccd99-227">Mono/Xamarin Platforms</span></span>| <span data-ttu-id="ccd99-228">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-228">&#x2192;</span></span>| <span data-ttu-id="ccd99-229">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-229">&#x2192;</span></span>| <span data-ttu-id="ccd99-230">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-230">&#x2192;</span></span>| <span data-ttu-id="ccd99-231">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-231">&#x2192;</span></span>| <span data-ttu-id="ccd99-232">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-232">&#x2192;</span></span>| <span data-ttu-id="ccd99-233">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-233">&#x2192;</span></span>|
|<span data-ttu-id="ccd99-234">Piattaforma UWP (Universal Windows Platform)</span><span class="sxs-lookup"><span data-stu-id="ccd99-234">Universal Windows Platform</span></span>| <span data-ttu-id="ccd99-235">uap</span><span class="sxs-lookup"><span data-stu-id="ccd99-235">uap</span></span>| <span data-ttu-id="ccd99-236">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-236">&#x2192;</span></span>| <span data-ttu-id="ccd99-237">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-237">&#x2192;</span></span>| <span data-ttu-id="ccd99-238">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-238">&#x2192;</span></span>| <span data-ttu-id="ccd99-239">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-239">&#x2192;</span></span>|<span data-ttu-id="ccd99-240">10.0</span><span class="sxs-lookup"><span data-stu-id="ccd99-240">10.0</span></span>|
|<span data-ttu-id="ccd99-241">WINDOWS</span><span class="sxs-lookup"><span data-stu-id="ccd99-241">Windows</span></span>| <span data-ttu-id="ccd99-242">win</span><span class="sxs-lookup"><span data-stu-id="ccd99-242">win</span></span>| <span data-ttu-id="ccd99-243">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-243">&#x2192;</span></span>| <span data-ttu-id="ccd99-244">8.0</span><span class="sxs-lookup"><span data-stu-id="ccd99-244">8.0</span></span>| <span data-ttu-id="ccd99-245">8.1</span><span class="sxs-lookup"><span data-stu-id="ccd99-245">8.1</span></span>|
|<span data-ttu-id="ccd99-246">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="ccd99-246">Windows Phone</span></span>| <span data-ttu-id="ccd99-247">wpa</span><span class="sxs-lookup"><span data-stu-id="ccd99-247">wpa</span></span>| <span data-ttu-id="ccd99-248">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-248">&#x2192;</span></span>| <span data-ttu-id="ccd99-249">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ccd99-249">&#x2192;</span></span>|<span data-ttu-id="ccd99-250">8.1</span><span class="sxs-lookup"><span data-stu-id="ccd99-250">8.1</span></span>|
|<span data-ttu-id="ccd99-251">Silverlight per Windows Phone</span><span class="sxs-lookup"><span data-stu-id="ccd99-251">Windows Phone Silverlight</span></span>| <span data-ttu-id="ccd99-252">wp</span><span class="sxs-lookup"><span data-stu-id="ccd99-252">wp</span></span>| <span data-ttu-id="ccd99-253">8.0</span><span class="sxs-lookup"><span data-stu-id="ccd99-253">8.0</span></span>|



## <a name="related-topics"></a><span data-ttu-id="ccd99-254">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="ccd99-254">Related topics</span></span>

- [<span data-ttu-id="ccd99-255">Informazioni di riferimento sul file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="ccd99-255">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="ccd99-256">Pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="ccd99-256">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="ccd99-257">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="ccd99-257">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="ccd99-258">Supporto di più versioni di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="ccd99-258">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="ccd99-259">Includere proprietà e destinazioni MSBuild in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="ccd99-259">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="ccd99-260">Creazione di pacchetti localizzati</span><span class="sxs-lookup"><span data-stu-id="ccd99-260">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="ccd99-261">Documentazione della libreria .NET Standard</span><span class="sxs-lookup"><span data-stu-id="ccd99-261">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="ccd99-262">Portabilità in .NET Core da .NET Framework</span><span class="sxs-lookup"><span data-stu-id="ccd99-262">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
