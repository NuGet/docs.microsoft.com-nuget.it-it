---
title: Creare pacchetti NuGet per la piattaforma UWP (Universal Windows Platform)
description: Procedura dettagliata end-to-end sulla creazione di pacchetti NuGet con un componente Windows Runtime per la piattaforma UWP (Universal Windows Platform).
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 77aa186291122a8d05018ecacd1329da459badad
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380760"
---
# <a name="create-uwp-packages"></a><span data-ttu-id="73195-103">Creare pacchetti UWP</span><span class="sxs-lookup"><span data-stu-id="73195-103">Create UWP packages</span></span>

<span data-ttu-id="73195-104">La [piattaforma UWP (Universal Windows Platform)](https://developer.microsoft.com/windows) è una piattaforma applicativa comune per ogni dispositivo che esegue Windows 10.</span><span class="sxs-lookup"><span data-stu-id="73195-104">The [Universal Windows Platform (UWP)](https://developer.microsoft.com/windows) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="73195-105">In questo modello le app UWP possono chiamare sia le API WinRT comuni a tutti i dispositivi che le API (incluse Win32 e .NET) specifiche della famiglia di dispositivi su cui l'app è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="73195-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="73195-106">Questa procedura dettagliata descrive come creare un pacchetto NuGet con un componente UWP nativo (incluso un controllo XAML) che può essere usato in progetti sia gestiti che nativi.</span><span class="sxs-lookup"><span data-stu-id="73195-106">In this walkthrough you create a NuGet package with a native UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73195-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="73195-107">Prerequisites</span></span>

1. <span data-ttu-id="73195-108">Visual Studio 2017 o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="73195-108">Visual Studio 2017 or Visual Studio 2015.</span></span> <span data-ttu-id="73195-109">Installare l'edizione 2017 Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/). È anche possibile usare le edizioni Professional ed Enterprise.</span><span class="sxs-lookup"><span data-stu-id="73195-109">Install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="73195-110">Interfaccia della riga di comando di NuGet.</span><span class="sxs-lookup"><span data-stu-id="73195-110">NuGet CLI.</span></span> <span data-ttu-id="73195-111">Scaricare la versione più recente `nuget.exe` da [nuget.org/downloads](https://nuget.org/downloads), salvandola in una posizione di propria scelta (il download include direttamente il file `.exe`).</span><span class="sxs-lookup"><span data-stu-id="73195-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="73195-112">Aggiungere quindi tale posizione alla variabile di ambiente PATH, se necessario.</span><span class="sxs-lookup"><span data-stu-id="73195-112">Then add that location to your PATH environment variable if it isn't already.</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="73195-113">Creare un componente Windows Runtime UWP</span><span class="sxs-lookup"><span data-stu-id="73195-113">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="73195-114">In Visual Studio scegliere **File > Nuovo > Progetto**, espandere il nodo **Visual C++ > Windows > Universale**, selezionare il modello **Componente Windows Runtime (Windows universale)**, modificare il nome in ImageEnhancer e fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="73195-114">In Visual Studio, choose **File > New > Project**, expand the **Visual C++ > Windows > Universal** node, select the **Windows Runtime Component (Universal Windows)** template, change the name to ImageEnhancer, and click OK.</span></span> <span data-ttu-id="73195-115">Accettare i valori predefiniti per Versione di destinazione e Versione minima quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="73195-115">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Creazione di un nuovo progetto del componente Windows Runtime UWP](media/UWP-NewProject.png)

1. <span data-ttu-id="73195-117">Fare clic con il pulsante destro sul progetto in Esplora soluzioni, scegliere **Aggiungi > Nuovo elemento**, fare clic sul nodo **Visual C++ > XAML**, selezionare **Controllo basato su modelli**, modificare il nome in AwesomeImageControl.cpp e fare clic su **Aggiungi**:</span><span class="sxs-lookup"><span data-stu-id="73195-117">Right click the project in Solution Explorer, select **Add > New Item**, click the **Visual C++ > XAML** node, select **Templated Control**, change the name to AwesomeImageControl.cpp, and click **Add**:</span></span>

    ![Aggiunta di un nuovo elemento Controllo basato su modelli XAML al progetto](media/UWP-NewXAMLControl.png)

1. <span data-ttu-id="73195-119">Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e selezionare Proprietà.Right-click the project in Solution Explorer and select **Properties.**</span><span class="sxs-lookup"><span data-stu-id="73195-119">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="73195-120">Nella pagina delle proprietà espandere **Proprietà di configurazione > C/C++** e fare clic su **File di output**.</span><span class="sxs-lookup"><span data-stu-id="73195-120">In the Properties page, expand **Configuration Properties > C/C++** and click **Output Files**.</span></span> <span data-ttu-id="73195-121">Nel riquadro a destra impostare il valore di **Genera file di documentazione XML** su Sì:</span><span class="sxs-lookup"><span data-stu-id="73195-121">In the pane on the right, change the value for **Generate XML Documentation Files** to Yes:</span></span>

    ![Impostazione di Genera file di documentazione XML su Sì](media/UWP-GenerateXMLDocFiles.png)

1. <span data-ttu-id="73195-123">Fare clic con il pulsante destro del mouse sulla *soluzione*, scegliere **Compilazione batch** e selezionare le tre caselle Debug nella finestra di dialogo, come illustrato sotto.</span><span class="sxs-lookup"><span data-stu-id="73195-123">Right click the *solution* now, select **Batch Build**, check the three Debug boxes in the dialog as shown below.</span></span> <span data-ttu-id="73195-124">Ciò assicura che, quando si esegue una compilazione, venga generato un set completo di elementi per ogni sistema di destinazione supportato da Windows.</span><span class="sxs-lookup"><span data-stu-id="73195-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Compilazione batch](media/UWP-BatchBuild.png)

1. <span data-ttu-id="73195-126">Nella finestra di dialogo Compilazione batch fare clic su **Compila** per verificare il progetto e creare i file di output necessari per il pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="73195-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="73195-127">In questa procedura dettagliata vengono usati gli elementi Debug per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="73195-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="73195-128">Per il pacchetto non di debug, selezionare invece le opzioni Versione nella finestra di dialogo Compilazione batch e fare riferimento alle cartelle Versione risultanti nei passaggi che seguono.</span><span class="sxs-lookup"><span data-stu-id="73195-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="73195-129">Creare e aggiornare il file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="73195-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="73195-130">Per creare il file `.nuspec` iniziale, eseguire i tre passaggi elencati sotto.</span><span class="sxs-lookup"><span data-stu-id="73195-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="73195-131">Le sezioni che seguono forniscono quindi indicazioni dettagliate sugli altri aggiornamenti necessari.</span><span class="sxs-lookup"><span data-stu-id="73195-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="73195-132">Aprire un prompt dei comandi e passare alla cartella contenente `ImageEnhancer.vcxproj`, che sarà una sottocartella sotto la posizione in cui si trova il file della soluzione.</span><span class="sxs-lookup"><span data-stu-id="73195-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.vcxproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="73195-133">Eseguire il comando `spec` di NuGet per generare `ImageEnhancer.nuspec`. Il nome del file viene ricavato dal nome del file `.vcxproj`:</span><span class="sxs-lookup"><span data-stu-id="73195-133">Run the NuGet `spec` command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.vcxproj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="73195-134">Aprire `ImageEnhancer.nuspec` in un editor e aggiornarlo in modo che corrisponda a quanto segue, sostituendo YOUR_NAME con un valore appropriato.</span><span class="sxs-lookup"><span data-stu-id="73195-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="73195-135">Il valore `<id>`, in particolare, deve essere univoco in nuget.org. Vedere le convenzioni di denominazione descritte in [Creazione di un pacchetto](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="73195-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="73195-136">Tenere inoltre presente che è anche necessario aggiornare i tag relativi all'autore e alla descrizione o si verifica un errore durante il passaggio di creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="73195-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="73195-137">Per i pacchetti compilati per uso pubblico, prestare particolare attenzione all'elemento `<tags>`, perché questi tag consentono ad altri utenti di trovare il pacchetto e di conoscerne le funzioni.</span><span class="sxs-lookup"><span data-stu-id="73195-137">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="73195-138">Aggiunta di metadati Windows al pacchetto</span><span class="sxs-lookup"><span data-stu-id="73195-138">Adding Windows metadata to the package</span></span>

<span data-ttu-id="73195-139">Un componente Windows Runtime richiede metadati che descrivono tutti i tipi disponibili pubblicamente, per consentire ad altre app e librerie di utilizzare il componente.</span><span class="sxs-lookup"><span data-stu-id="73195-139">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="73195-140">Questi metadati sono contenuti in un file con estensione winmd, che viene creato quando si compila il progetto e deve essere incluso nel pacchetto NuGet</span><span class="sxs-lookup"><span data-stu-id="73195-140">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="73195-141">insieme a un file XML con dati IntelliSense che viene compilato nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="73195-141">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="73195-142">Aggiungere il nodo `<files>` seguente al file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="73195-142">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="73195-143">Aggiunta di contenuto XAML</span><span class="sxs-lookup"><span data-stu-id="73195-143">Adding XAML content</span></span>

<span data-ttu-id="73195-144">Per includere un controllo XAML con il componente, è necessario aggiungere il file XAML contenente il modello predefinito per il controllo (generato dal modello di progetto).</span><span class="sxs-lookup"><span data-stu-id="73195-144">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="73195-145">Anche questo va inserito nella sezione `<files>`:</span><span class="sxs-lookup"><span data-stu-id="73195-145">This also goes in the `<files>` section:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="73195-146">Aggiunta di librerie di implementazione native</span><span class="sxs-lookup"><span data-stu-id="73195-146">Adding the native implementation libraries</span></span>

<span data-ttu-id="73195-147">Nel componente la logica principale del tipo ImageEnhancer si trova nel codice nativo, che è contenuto nei diversi assembly `ImageEnhancer.dll` generati per ogni runtime di destinazione (ARM, x86 e x64).</span><span class="sxs-lookup"><span data-stu-id="73195-147">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.dll` assemblies that are generated for each target runtime (ARM, x86, and x64).</span></span> <span data-ttu-id="73195-148">Per includerli nel pacchetto, farvi riferimento nella sezione `<files>` insieme ai file di risorse PRI associati:</span><span class="sxs-lookup"><span data-stu-id="73195-148">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a><span data-ttu-id="73195-149">Aggiunta del file con estensione targets</span><span class="sxs-lookup"><span data-stu-id="73195-149">Adding .targets</span></span>

<span data-ttu-id="73195-150">Per i progetti C++ e JavaScript che potrebbero utilizzare il pacchetto NuGet è poi necessario un file con estensione targets per identificare i file di assembly e winmd necessari.</span><span class="sxs-lookup"><span data-stu-id="73195-150">Next, C++ and JavaScript projects that might consume your NuGet package need a .targets file to identify the necessary assembly and winmd files.</span></span> <span data-ttu-id="73195-151">(I progetti di Visual Basic di C e Visual Basic eseguire questa operazione automaticamente.) Creare questo file copiando `ImageEnhancer.targets` il testo riportato di `.nuspec` seguito e salvarlo nella stessa cartella del file.</span><span class="sxs-lookup"><span data-stu-id="73195-151">(C# and Visual Basic projects do this automatically.) Create this file by copying the text below into `ImageEnhancer.targets` and save it in the same folder as the `.nuspec` file.</span></span> <span data-ttu-id="73195-152">_Nota_: questo file `.targets` deve avere lo stesso nome dell'ID di pacchetto (ad esempio, l'elemento `<Id>` nel file `.nupspec`):</span><span class="sxs-lookup"><span data-stu-id="73195-152">_Note_: This `.targets` file needs to be the same name as the package ID (e.g. the `<Id>` element in the `.nupspec` file):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

<span data-ttu-id="73195-153">Fare quindi riferimento a `ImageEnhancer.targets` nel file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="73195-153">Then refer to `ImageEnhancer.targets` in your `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="73195-154">File con estensione nuspec finale</span><span class="sxs-lookup"><span data-stu-id="73195-154">Final .nuspec</span></span>

<span data-ttu-id="73195-155">Il file `.nuspec` finale sarà simile al seguente, dove YOUR_NAME deve essere sostituito con un valore appropriato:</span><span class="sxs-lookup"><span data-stu-id="73195-155">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>     
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="73195-156">Creare un pacchetto per il componente</span><span class="sxs-lookup"><span data-stu-id="73195-156">Package the component</span></span>

<span data-ttu-id="73195-157">Dopo avere completato il file `.nuspec` che fa riferimento a tutti i file da includere nel pacchetto, è possibile eseguire il comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="73195-157">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="73195-158">Questo codice genera `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="73195-158">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="73195-159">Aprendo il file in uno strumento come [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ed espandendo tutti i nodi, vengono visualizzati i contenuti seguenti:</span><span class="sxs-lookup"><span data-stu-id="73195-159">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet Package Explorer che visualizza il pacchetto ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="73195-161">Un file `.nupkg` è solo un file ZIP con un'estensione diversa.</span><span class="sxs-lookup"><span data-stu-id="73195-161">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="73195-162">È anche possibile esaminare i contenuti del pacchetto, modificando `.nupkg` in `.zip`, ma si ricordi di ripristinare l'estensione prima di caricare un pacchetto in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="73195-162">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="73195-163">Per rendere disponibile il pacchetto per altri sviluppatori, seguire le istruzioni in [Pubblicare un pacchetto](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="73195-163">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="73195-164">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="73195-164">Related topics</span></span>

- [<span data-ttu-id="73195-165">Riferimento .nuspec</span><span class="sxs-lookup"><span data-stu-id="73195-165">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="73195-166">Pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="73195-166">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="73195-167">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="73195-167">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="73195-168">Supporto di più versioni di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="73195-168">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="73195-169">Includere proprietà e destinazioni MSBuild in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="73195-169">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="73195-170">Creazione di pacchetti localizzati</span><span class="sxs-lookup"><span data-stu-id="73195-170">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
