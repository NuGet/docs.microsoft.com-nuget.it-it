---
title: Creare pacchetti NuGet multipiattaforma (per iOS, Android e Windows) | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: ae24824b-a138-4d12-a810-1f653ddffd32
description: Procedura dettagliata end-to-end sulla creazione di pacchetti NuGet per Xamarin che usano API native in iOS, Android e Windows.
keywords: creare un pacchetto, pacchetti per Xamarin, pacchetti multipiattaforma
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f372856232f151efcf972881cffbe7d4bb7ed6ee
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="create-cross-platform-packages"></a><span data-ttu-id="d8ab0-104">Creare pacchetti multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="d8ab0-104">Create cross-platform packages</span></span>

<span data-ttu-id="d8ab0-105">Un pacchetto multipiattaforma contiene codice che usa le API native in iOS, Android e Windows, a seconda del sistema operativo in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-105">A cross-platform package contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="d8ab0-106">Anche se si tratta di un'operazione semplice, è preferibile consentire agli sviluppatori di utilizzare il pacchetto da una libreria .NET Standard o PCL tramite una superficie di attacco delle API comune.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-106">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="d8ab0-107">In questa procedura dettagliata si creerà un pacchetto NuGet multipiattaforma che può essere usato in progetti per dispositivi mobili su iOS, Android e Windows.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-107">In this walkthrough you'll create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="d8ab0-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d8ab0-108">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="d8ab0-109">Creare la struttura del progetto e il codice di astrazione</span><span class="sxs-lookup"><span data-stu-id="d8ab0-109">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="d8ab0-110">Scrivere il codice specifico della piattaforma</span><span class="sxs-lookup"><span data-stu-id="d8ab0-110">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="d8ab0-111">Creare e aggiornare il file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="d8ab0-111">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="d8ab0-112">Creare un pacchetto per il componente</span><span class="sxs-lookup"><span data-stu-id="d8ab0-112">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="d8ab0-113">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="d8ab0-113">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="d8ab0-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d8ab0-114">Pre-requisites</span></span>

1. <span data-ttu-id="d8ab0-115">Visual Studio 2015 con la piattaforma UWP (Universal Windows Platform) e Xamarin.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-115">Visual Studio 2015 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="d8ab0-116">Installare l'edizione Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/). È anche possibile usare le edizioni Professional ed Enterprise.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-116">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="d8ab0-117">Per includere gli strumenti UWP e Xamarin, selezionare un'installazione personalizzata e selezionare le opzioni appropriate.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-117">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="d8ab0-118">Interfaccia della riga di comando di NuGet.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-118">NuGet CLI.</span></span> <span data-ttu-id="d8ab0-119">Scaricare la versione più recente di nuget.exe da [nuget.org/downloads](https://nuget.org/downloads), salvandola in una posizione di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-119">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="d8ab0-120">Aggiungere quindi tale posizione alla variabile di ambiente PATH, se necessario.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-120">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="d8ab0-121">Poiché nuget.exe è di per sé lo strumento dell'interfaccia della riga di comando e non un programma di installazione, assicurarsi di salvare il file scaricato dal browser invece di eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-121">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>


## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="d8ab0-122">Creare la struttura del progetto e il codice di astrazione</span><span class="sxs-lookup"><span data-stu-id="d8ab0-122">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="d8ab0-123">Scaricare ed eseguire l'[estensione Plugin for Xamarin Templates](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-123">Download and run the [Plugin for Xamarin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="d8ab0-124">Questi modelli consentiranno di creare facilmente la struttura del progetto necessaria per questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-124">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="d8ab0-125">In Visual Studio fare clic su **File > Nuovo > Progetto**, cercare `Plugin`, selezionare il modello **Plugin for Xamarin**, modificare il nome in LoggingLibrary e fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-125">In Visual Studio, **File > New > Project**, search for `Plugin`, select the **Plugin for Xamarin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Nuovo progetto di app vuota (Xamarin.Forms portabile) in Visual Studio](media/CrossPlatform-NewProject.png)

<span data-ttu-id="d8ab0-127">La soluzione risultante contiene due progetti PCL, oltre a diversi progetti specifici della piattaforma:</span><span class="sxs-lookup"><span data-stu-id="d8ab0-127">The resulting solution contains two PCL projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="d8ab0-128">La libreria PCL denominata `Plugin.LoggingLibrary.Abstractions (Portable)` definisce l'interfaccia pubblica (la superficie di attacco delle API) del componente, in questo caso l'interfaccia `ILoggingLibrary` contenuta nel file ILoggingLibrary.cs,</span><span class="sxs-lookup"><span data-stu-id="d8ab0-128">The PCL named `Plugin.LoggingLibrary.Abstractions (Portable)`, defines the public interface (the API surface area) of the component, in this case the `ILoggingLibrary` interface contained in the ILoggingLibrary.cs file.</span></span> <span data-ttu-id="d8ab0-129">dove si definirà l'interfaccia per la libreria.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-129">This is where you'll define the interface to your library.</span></span>
- <span data-ttu-id="d8ab0-130">L'altra libreria PCL, `Plugin.LoggingLibrary (Portable)`, contiene il codice in CrossLoggingLibrary.cs che individuerà un'implementazione specifica della piattaforma dell'interfaccia astratta in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-130">The other PCL, `Plugin.LoggingLibrary (Portable)`, contains code in CrossLoggingLibrary.cs that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="d8ab0-131">In genere non è necessario modificare questo file.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-131">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="d8ab0-132">Ogni progetto specifico della piattaforma, ad esempio `Plugin.LoggingLibrary.Android`, contiene un'implementazione nativa dell'interfaccia nei rispettivi file LoggingLibraryImplementation.cs,</span><span class="sxs-lookup"><span data-stu-id="d8ab0-132">The platform-specific projects, such as `Plugin.LoggingLibrary.Android`, each contain contain a native implementation of the interface in their respective LoggingLibraryImplementation.cs files.</span></span> <span data-ttu-id="d8ab0-133">dove si compilerà il codice della libreria.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-133">This is where you'll build out your library's code.</span></span>

<span data-ttu-id="d8ab0-134">Per impostazione predefinita, il file ILoggingLibrary.cs del progetto Abstractions contiene una definizione dell'interfaccia, ma nessun metodo.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-134">By default, the ILoggingLibrary.cs file of the Abstractions project contains an interface definition, but no methods.</span></span> <span data-ttu-id="d8ab0-135">Ai fini di questa procedura dettagliata, aggiungere un metodo `Log` come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d8ab0-135">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="d8ab0-136">Scrivere il codice specifico della piattaforma</span><span class="sxs-lookup"><span data-stu-id="d8ab0-136">Write your platform-specific code</span></span>

<span data-ttu-id="d8ab0-137">Per eseguire un'implementazione specifica della piattaforma dell'interfaccia `ILoggingLibrary` e dei relativi metodi, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d8ab0-137">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="d8ab0-138">Aprire il file `LoggingLibraryImplementation.cs` di ogni progetto della piattaforma e aggiungere il codice necessario,</span><span class="sxs-lookup"><span data-stu-id="d8ab0-138">Open the `LoggingLibraryImplementation.cs` file of each platform project and add the necessary code.</span></span> <span data-ttu-id="d8ab0-139">ad esempio (usando il progetto `Plugin.LoggingLibrary.Android`):</span><span class="sxs-lookup"><span data-stu-id="d8ab0-139">For example (using the `Plugin.LoggingLibrary.Android` project):</span></span>

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. <span data-ttu-id="d8ab0-140">Ripetere questa implementazione nei progetti per ogni piattaforma che si vuole supportare.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-140">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="d8ab0-141">Fare clic con il pulsante destro del mouse sul progetto iOS, scegliere **Proprietà**, fare clic sulla scheda **Compilazione** e rimuovere "\iPhone" dalle impostazioni **Percorso di output** e **File di documentazione XML**.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-141">Right-click the iOS project, select **Properties**, click the **Build** tab, and remove "\iPhone" from the **Output path** and **XML documentation file** settings.</span></span> <span data-ttu-id="d8ab0-142">Questa operazione viene eseguita solo per facilitare il resto della procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-142">This is just for later convenience in this walkthrough.</span></span> <span data-ttu-id="d8ab0-143">Salvare il file al termine.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-143">Save the file when done.</span></span>
1. <span data-ttu-id="d8ab0-144">Fare clic con il pulsante destro del mouse sulla soluzione, scegliere **Gestione configurazione** e selezionare le caselle **Compilazione** per le librerie PCL e ogni piattaforma supportata.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-144">Right-click the solution, select **Configuration Manager...**, and check the **Build** boxes for the PCLs and each platform you're supporting.</span></span>
1. <span data-ttu-id="d8ab0-145">Fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Compila soluzione** per controllare il lavoro e generare gli elementi per cui in seguito verrà creato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-145">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you'll package next.</span></span> <span data-ttu-id="d8ab0-146">Se vengono visualizzati errori su riferimenti mancanti, fare clic con il pulsante destro del mouse sulla soluzione, scegliere **Ripristina pacchetti NuGet** per installare le dipendenze ed eseguire di nuovo la compilazione.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-146">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="d8ab0-147">Per eseguire la compilazione per iOS, è necessario un Mac in rete connesso a Visual Studio, come descritto in [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/) (Introduzione a Xamarin.iOS per Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="d8ab0-147">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="d8ab0-148">Se non è disponibile un Mac, cancellare il progetto iOS in Gestione configurazione (passaggio 3).</span><span class="sxs-lookup"><span data-stu-id="d8ab0-148">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>


## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="d8ab0-149">Creare e aggiornare il file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="d8ab0-149">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="d8ab0-150">Aprire un prompt dei comandi, passare alla cartella `LoggingLibrary`, di un livello inferiore rispetto alla posizione del file `.sln`, ed eseguire il comando `spec` di NuGet per creare il file `Package.nuspec` iniziale:</span><span class="sxs-lookup"><span data-stu-id="d8ab0-150">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

```
nuget spec
```

1. <span data-ttu-id="d8ab0-151">Rinominare questo file in `LoggingLibrary.nuspec` e aprirlo in un editor.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-151">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="d8ab0-152">Aggiornare il file in modo che corrisponda a quanto segue, sostituendo YOUR_NAME con un valore appropriato.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-152">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="d8ab0-153">Il valore `<id>`, in particolare, deve essere univoco in nuget.org. Vedere le convenzioni di denominazione descritte in [Creazione di un pacchetto](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="d8ab0-153">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="d8ab0-154">Tenere inoltre presente che è anche necessario aggiornare i tag relativi all'autore e alla descrizione o si verificherà un errore durante il passaggio di creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-154">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```
    
> [!Tip]
> <span data-ttu-id="d8ab0-155">È possibile aggiungere alla versione del pacchetto il suffisso `-alpha`, `-beta` o `-rc` per contrassegnare il pacchetto come non definitivo. Per altre informazioni sulle versioni non definitive, vedere [Versioni non definitive](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="d8ab0-155">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="d8ab0-156">Aggiungere assembly di riferimento</span><span class="sxs-lookup"><span data-stu-id="d8ab0-156">Add reference assemblies</span></span>

<span data-ttu-id="d8ab0-157">Per includere gli assembly di riferimento specifici della piattaforma, aggiungere il codice seguente all'elemento `<files>` di `LoggingLibrary.nuspec` in modo appropriato alle piattaforme supportate:</span><span class="sxs-lookup"><span data-stu-id="d8ab0-157">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> <span data-ttu-id="d8ab0-158">Per abbreviare i nomi dei file DLL e XML, fare clic con il pulsante destro del mouse su un determinato progetto, scegliere la scheda **Libreria** e modificare i nomi degli assembly.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-158">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>


### <a name="add-dependencies"></a><span data-ttu-id="d8ab0-159">Aggiungere dipendenze</span><span class="sxs-lookup"><span data-stu-id="d8ab0-159">Add dependencies</span></span>

<span data-ttu-id="d8ab0-160">Se sono presenti dipendenze specifiche per le implementazioni native, usare l'elemento `<dependencies>` con gli elementi `<group>` per specificarle, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d8ab0-160">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

<span data-ttu-id="d8ab0-161">Il codice seguente, ad esempio, imposterà iTextSharp come dipendenza per la destinazione UAP:</span><span class="sxs-lookup"><span data-stu-id="d8ab0-161">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="d8ab0-162">File con estensione nuspec finale</span><span class="sxs-lookup"><span data-stu-id="d8ab0-162">Final .nuspec</span></span>

<span data-ttu-id="d8ab0-163">Il file `.nuspec` finale sarà simile al seguente, dove YOUR_NAME deve essere sostituito con un valore appropriato:</span><span class="sxs-lookup"><span data-stu-id="d8ab0-163">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="d8ab0-164">Creare un pacchetto per il componente</span><span class="sxs-lookup"><span data-stu-id="d8ab0-164">Package the component</span></span>

<span data-ttu-id="d8ab0-165">Dopo avere completato il file `.nuspec` che fa riferimento a tutti i file da includere nel pacchetto, è possibile eseguire il comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="d8ab0-165">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="d8ab0-166">Verrà generato `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-166">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="d8ab0-167">Aprendo il file in uno strumento come [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ed espandendo tutti i nodi, verranno visualizzati i contenuti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d8ab0-167">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![NuGet Package Explorer che visualizza il pacchetto LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="d8ab0-169">Un file `.nupkg` è solo un file ZIP con un'estensione diversa.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-169">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="d8ab0-170">È anche possibile esaminare i contenuti del pacchetto, modificando `.nupkg` in `.zip`, ma si ricordi di ripristinare l'estensione prima di caricare un pacchetto in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d8ab0-170">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>


<span data-ttu-id="d8ab0-171">Per rendere disponibile il pacchetto per altri sviluppatori, seguire le istruzioni in [Pubblicare un pacchetto](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="d8ab0-171">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="d8ab0-172">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="d8ab0-172">Related topics</span></span>

- [<span data-ttu-id="d8ab0-173">Informazioni di riferimento sul file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="d8ab0-173">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="d8ab0-174">Pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="d8ab0-174">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="d8ab0-175">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="d8ab0-175">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="d8ab0-176">Supporto di più versioni di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="d8ab0-176">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="d8ab0-177">Inclusione di proprietà e destinazioni MSBuild in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="d8ab0-177">Including MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="d8ab0-178">Creazione di pacchetti localizzati</span><span class="sxs-lookup"><span data-stu-id="d8ab0-178">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)