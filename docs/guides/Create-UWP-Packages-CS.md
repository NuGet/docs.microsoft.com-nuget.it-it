---
title: Creare pacchetti NuGet per la piattaforma UWP (Universal Windows Platform)
description: Procedura dettagliata end-to-end per la creazione di pacchetti NuGet tramite un componente Windows Runtime per la C#piattaforma UWP (Universal Windows Platform) in.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231805"
---
# <a name="create-uwp-packages-c"></a><span data-ttu-id="2495b-103">Creare pacchetti UWP (C#)</span><span class="sxs-lookup"><span data-stu-id="2495b-103">Create UWP packages (C#)</span></span>

<span data-ttu-id="2495b-104">La [piattaforma UWP (Universal Windows Platform)](/windows/uwp) è una piattaforma applicativa comune per ogni dispositivo che esegue Windows 10.</span><span class="sxs-lookup"><span data-stu-id="2495b-104">The [Universal Windows Platform (UWP)](/windows/uwp) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="2495b-105">In questo modello le app UWP possono chiamare sia le API WinRT comuni a tutti i dispositivi che le API (incluse Win32 e .NET) specifiche della famiglia di dispositivi su cui l'app è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2495b-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="2495b-106">In questa procedura dettagliata viene creato un pacchetto NuGet con C# un componente UWP (incluso un controllo XAML) che può essere usato nei progetti gestiti e nativi.</span><span class="sxs-lookup"><span data-stu-id="2495b-106">In this walkthrough you create a NuGet package with a C# UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2495b-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2495b-107">Prerequisites</span></span>

1. <span data-ttu-id="2495b-108">Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="2495b-108">Visual Studio 2019.</span></span> <span data-ttu-id="2495b-109">Installare l'edizione 2019 Community gratuitamente da [VisualStudio.com](https://www.visualstudio.com/); è anche possibile usare le edizioni Professional ed Enterprise.</span><span class="sxs-lookup"><span data-stu-id="2495b-109">Install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="2495b-110">Interfaccia della riga di comando di NuGet.</span><span class="sxs-lookup"><span data-stu-id="2495b-110">NuGet CLI.</span></span> <span data-ttu-id="2495b-111">Scaricare la versione più recente `nuget.exe` da [nuget.org/downloads](https://nuget.org/downloads), salvandola in una posizione di propria scelta (il download include direttamente il file `.exe`).</span><span class="sxs-lookup"><span data-stu-id="2495b-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="2495b-112">Aggiungere quindi tale posizione alla variabile di ambiente PATH, se necessario.</span><span class="sxs-lookup"><span data-stu-id="2495b-112">Then add that location to your PATH environment variable if it isn't already.</span></span> <span data-ttu-id="2495b-113">[Altre informazioni](/nuget/reference/nuget-exe-cli-reference#windows).</span><span class="sxs-lookup"><span data-stu-id="2495b-113">[More details](/nuget/reference/nuget-exe-cli-reference#windows).</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="2495b-114">Creare un componente Windows Runtime UWP</span><span class="sxs-lookup"><span data-stu-id="2495b-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="2495b-115">In Visual Studio scegliere **File > nuovo > progetto**, cercare "UWP c#", selezionare il modello **Windows Runtime Component (Windows universale)** , fare clic su Avanti, modificare il nome in ImageEnhancer e fare clic su Crea.</span><span class="sxs-lookup"><span data-stu-id="2495b-115">In Visual Studio, choose **File > New > Project**, search for "uwp c#", select the **Windows Runtime Component (Universal Windows)** template, click next, change the name to ImageEnhancer, and click Create.</span></span> <span data-ttu-id="2495b-116">Accettare i valori predefiniti per Versione di destinazione e Versione minima quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="2495b-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Creazione di un nuovo progetto del componente Windows Runtime UWP](media/UWP-NewProject-CS.png)

1. <span data-ttu-id="2495b-118">Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni, selezionare **aggiungi > nuovo elemento**, selezionare **controllo basato su modelli**, modificare il nome in AwesomeImageControl.cs e fare clic su **Aggiungi**:</span><span class="sxs-lookup"><span data-stu-id="2495b-118">Right click the project in Solution Explorer, select **Add > New Item**, select **Templated Control**, change the name to AwesomeImageControl.cs, and click **Add**:</span></span>

    ![Aggiunta di un nuovo elemento Controllo basato su modelli XAML al progetto](media/UWP-NewXAMLControl-CS.png)

1. <span data-ttu-id="2495b-120">Fare clic con il pulsante destro del mouse in Esplora soluzioni e scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="2495b-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="2495b-121">Nella pagina proprietà, scegliere scheda **compilazione** e Abilita **file di documentazione XML**:</span><span class="sxs-lookup"><span data-stu-id="2495b-121">In the Properties page, choose **Build** tab and enable **XML Documentation File**:</span></span>

    ![Impostazione di Genera file di documentazione XML su Sì](media/UWP-GenerateXMLDocFiles-CS.png)

1. <span data-ttu-id="2495b-123">Fare clic con il pulsante destro del mouse sulla *soluzione* ora, selezionare **compilazione batch**, selezionare le cinque caselle di compilazione nella finestra di dialogo come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2495b-123">Right click the *solution* now, select **Batch Build**, check the five build boxes in the dialog as shown below.</span></span> <span data-ttu-id="2495b-124">Ciò assicura che, quando si esegue una compilazione, venga generato un set completo di elementi per ogni sistema di destinazione supportato da Windows.</span><span class="sxs-lookup"><span data-stu-id="2495b-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Compilazione batch](media/UWP-BatchBuild-CS.png)

1. <span data-ttu-id="2495b-126">Nella finestra di dialogo Compilazione batch fare clic su **Compila** per verificare il progetto e creare i file di output necessari per il pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="2495b-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="2495b-127">In questa procedura dettagliata vengono usati gli elementi Debug per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2495b-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="2495b-128">Per il pacchetto non di debug, selezionare invece le opzioni Versione nella finestra di dialogo Compilazione batch e fare riferimento alle cartelle Versione risultanti nei passaggi che seguono.</span><span class="sxs-lookup"><span data-stu-id="2495b-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="2495b-129">Creare e aggiornare il file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="2495b-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="2495b-130">Per creare il file `.nuspec` iniziale, eseguire i tre passaggi elencati sotto.</span><span class="sxs-lookup"><span data-stu-id="2495b-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="2495b-131">Le sezioni che seguono forniscono quindi indicazioni dettagliate sugli altri aggiornamenti necessari.</span><span class="sxs-lookup"><span data-stu-id="2495b-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="2495b-132">Aprire un prompt dei comandi e passare alla cartella contenente `ImageEnhancer.csproj`, che sarà una sottocartella sotto la posizione in cui si trova il file della soluzione.</span><span class="sxs-lookup"><span data-stu-id="2495b-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.csproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="2495b-133">Eseguire il comando [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) per generare `ImageEnhancer.nuspec` (il nome del file viene ricavato dal nome del file di `.csroj`):</span><span class="sxs-lookup"><span data-stu-id="2495b-133">Run the [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.csroj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="2495b-134">Aprire `ImageEnhancer.nuspec` in un editor e aggiornarlo in modo che corrisponda a quanto segue, sostituendo YOUR_NAME con un valore appropriato.</span><span class="sxs-lookup"><span data-stu-id="2495b-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="2495b-135">Non lasciare uno dei valori di $propertyName $.</span><span class="sxs-lookup"><span data-stu-id="2495b-135">Do not leave any of the $propertyName$ values.</span></span> <span data-ttu-id="2495b-136">Il valore `<id>`, in particolare, deve essere univoco in nuget.org. Vedere le convenzioni di denominazione descritte in [Creazione di un pacchetto](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="2495b-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="2495b-137">Tenere inoltre presente che è anche necessario aggiornare i tag relativi all'autore e alla descrizione o si verifica un errore durante il passaggio di creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2495b-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2020</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="2495b-138">Per i pacchetti compilati per uso pubblico, prestare particolare attenzione all'elemento `<tags>`, perché questi tag consentono ad altri utenti di trovare il pacchetto e di conoscerne le funzioni.</span><span class="sxs-lookup"><span data-stu-id="2495b-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="2495b-139">Aggiunta di metadati Windows al pacchetto</span><span class="sxs-lookup"><span data-stu-id="2495b-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="2495b-140">Un componente Windows Runtime richiede metadati che descrivono tutti i tipi disponibili pubblicamente, per consentire ad altre app e librerie di utilizzare il componente.</span><span class="sxs-lookup"><span data-stu-id="2495b-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="2495b-141">Questi metadati sono contenuti in un file con estensione winmd, che viene creato quando si compila il progetto e deve essere incluso nel pacchetto NuGet</span><span class="sxs-lookup"><span data-stu-id="2495b-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="2495b-142">insieme a un file XML con dati IntelliSense che viene compilato nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="2495b-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="2495b-143">Aggiungere il nodo `<files>` seguente al file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="2495b-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="2495b-144">Aggiunta di contenuto XAML</span><span class="sxs-lookup"><span data-stu-id="2495b-144">Adding XAML content</span></span>

<span data-ttu-id="2495b-145">Per includere un controllo XAML con il componente, è necessario aggiungere il file XAML contenente il modello predefinito per il controllo (generato dal modello di progetto).</span><span class="sxs-lookup"><span data-stu-id="2495b-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="2495b-146">Anche questo va inserito nella sezione `<files>`:</span><span class="sxs-lookup"><span data-stu-id="2495b-146">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="2495b-147">Aggiunta di librerie di implementazione native</span><span class="sxs-lookup"><span data-stu-id="2495b-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="2495b-148">All'interno del componente, la logica di base del tipo ImageEnhancer si trova nel codice nativo, che è contenuto nei vari assembly `ImageEnhancer.winmd` generati per ogni runtime di destinazione (ARM, ARM64, x86 e x64).</span><span class="sxs-lookup"><span data-stu-id="2495b-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.winmd` assemblies that are generated for each target runtime (ARM, ARM64, x86, and x64).</span></span> <span data-ttu-id="2495b-149">Per includerli nel pacchetto, farvi riferimento nella sezione `<files>` insieme ai file di risorse PRI associati:</span><span class="sxs-lookup"><span data-stu-id="2495b-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="2495b-150">File con estensione nuspec finale</span><span class="sxs-lookup"><span data-stu-id="2495b-150">Final .nuspec</span></span>

<span data-ttu-id="2495b-151">Il file `.nuspec` finale sarà simile al seguente, dove YOUR_NAME deve essere sostituito con un valore appropriato:</span><span class="sxs-lookup"><span data-stu-id="2495b-151">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="2495b-152">Creare un pacchetto per il componente</span><span class="sxs-lookup"><span data-stu-id="2495b-152">Package the component</span></span>

<span data-ttu-id="2495b-153">Con il `.nuspec` completato che fa riferimento a tutti i file che è necessario includere nel pacchetto, si è pronti per eseguire il comando [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) :</span><span class="sxs-lookup"><span data-stu-id="2495b-153">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="2495b-154">Questo codice genera `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="2495b-154">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="2495b-155">Aprendo il file in uno strumento come [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ed espandendo tutti i nodi, vengono visualizzati i contenuti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2495b-155">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet Package Explorer che visualizza il pacchetto ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="2495b-157">Un file `.nupkg` è solo un file ZIP con un'estensione diversa.</span><span class="sxs-lookup"><span data-stu-id="2495b-157">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="2495b-158">È anche possibile esaminare i contenuti del pacchetto, modificando `.nupkg` in `.zip`, ma si ricordi di ripristinare l'estensione prima di caricare un pacchetto in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="2495b-158">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="2495b-159">Per rendere disponibile il pacchetto per altri sviluppatori, seguire le istruzioni in [Pubblicare un pacchetto](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="2495b-159">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="2495b-160">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="2495b-160">Related topics</span></span>

- [<span data-ttu-id="2495b-161">Informazioni di riferimento sul file .nuspec</span><span class="sxs-lookup"><span data-stu-id="2495b-161">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="2495b-162">Pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="2495b-162">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="2495b-163">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="2495b-163">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="2495b-164">Supporto di più versioni di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="2495b-164">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="2495b-165">Includere proprietà e destinazioni MSBuild in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="2495b-165">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="2495b-166">Creazione di pacchetti localizzati</span><span class="sxs-lookup"><span data-stu-id="2495b-166">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)