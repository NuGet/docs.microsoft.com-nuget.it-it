---
title: Creare pacchetti NuGet per Novell (per iOS, Android e Windows) con Visual Studio 2017 o 2019
description: Procedura dettagliata end-to-end sulla creazione di pacchetti NuGet per Xamarin che usano API native in iOS, Android e Windows.
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: fce3c9a92dfee325f9e914bf3d6444601fb38b6c
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385682"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a><span data-ttu-id="7c30e-103">Creare pacchetti per Novell con Visual Studio 2017 o 2019</span><span class="sxs-lookup"><span data-stu-id="7c30e-103">Create packages for Xamarin with Visual Studio 2017 or 2019</span></span>

<span data-ttu-id="7c30e-104">Un pacchetto per Xamarin contiene codice che usa le API native in iOS, Android e Windows, a seconda del sistema operativo in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7c30e-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="7c30e-105">Anche se si tratta di un'operazione semplice, è preferibile consentire agli sviluppatori di utilizzare il pacchetto da una libreria .NET Standard o PCL tramite una superficie di attacco delle API comune.</span><span class="sxs-lookup"><span data-stu-id="7c30e-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="7c30e-106">In questa procedura dettagliata viene usato Visual Studio 2017 o 2019 per creare un pacchetto NuGet multipiattaforma che può essere usato in progetti per dispositivi mobili in iOS, Android e Windows.</span><span class="sxs-lookup"><span data-stu-id="7c30e-106">In this walkthrough you use Visual Studio 2017 or 2019 to create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="7c30e-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7c30e-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="7c30e-108">Creare la struttura del progetto e il codice di astrazione</span><span class="sxs-lookup"><span data-stu-id="7c30e-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="7c30e-109">Scrivere il codice specifico della piattaforma</span><span class="sxs-lookup"><span data-stu-id="7c30e-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="7c30e-110">Creare e aggiornare il file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="7c30e-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="7c30e-111">Creare un pacchetto per il componente</span><span class="sxs-lookup"><span data-stu-id="7c30e-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="7c30e-112">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="7c30e-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="7c30e-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7c30e-113">Prerequisites</span></span>

1. <span data-ttu-id="7c30e-114">Visual Studio 2017 o 2019 con piattaforma UWP (Universal Windows Platform) (UWP) e Novell.</span><span class="sxs-lookup"><span data-stu-id="7c30e-114">Visual Studio 2017 or 2019 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="7c30e-115">Installare l'edizione Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/). È anche possibile usare le edizioni Professional ed Enterprise.</span><span class="sxs-lookup"><span data-stu-id="7c30e-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="7c30e-116">Per includere gli strumenti UWP e Xamarin, selezionare un'installazione personalizzata e selezionare le opzioni appropriate.</span><span class="sxs-lookup"><span data-stu-id="7c30e-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="7c30e-117">Interfaccia della riga di comando di NuGet.</span><span class="sxs-lookup"><span data-stu-id="7c30e-117">NuGet CLI.</span></span> <span data-ttu-id="7c30e-118">Scaricare la versione più recente di nuget.exe da [nuget.org/downloads](https://nuget.org/downloads), salvandola in una posizione di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="7c30e-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="7c30e-119">Aggiungere quindi tale posizione alla variabile di ambiente PATH, se necessario.</span><span class="sxs-lookup"><span data-stu-id="7c30e-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="7c30e-120">Poiché nuget.exe è di per sé lo strumento dell'interfaccia della riga di comando e non un programma di installazione, assicurarsi di salvare il file scaricato dal browser invece di eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="7c30e-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="7c30e-121">Creare la struttura del progetto e il codice di astrazione</span><span class="sxs-lookup"><span data-stu-id="7c30e-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="7c30e-122">Scaricare ed eseguire l' [estensione per i modelli di plug-in .NET standard multipiattaforma](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7c30e-122">Download and run the [Cross-Platform .NET Standard Plugin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="7c30e-123">Questi modelli consentiranno di creare facilmente la struttura del progetto necessaria per questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="7c30e-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="7c30e-124">In Visual Studio 2017, **File > nuovo progetto >** , cercare `Plugin`, selezionare il modello di **plug-in della libreria .NET standard multipiattaforma** , modificare il nome in LoggingLibrary e fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="7c30e-124">In Visual Studio 2017, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Nuovo progetto app vuota (Novell. Forms Portable) in Visual Studio 2017](media/CrossPlatform-NewProject.png)

    <span data-ttu-id="7c30e-126">In Visual Studio 2019, **File > nuovo progetto >** , cercare `Plugin`, selezionare il modello di **Plug-In della libreria .NET standard multipiattaforma** e fare clic su Avanti.</span><span class="sxs-lookup"><span data-stu-id="7c30e-126">In Visual Studio 2019, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, and click Next.</span></span>

    ![Nuovo progetto app vuota (Novell. Forms Portable) in Visual Studio 2019](media/CrossPlatform-NewProject19-Part1.png)

    <span data-ttu-id="7c30e-128">Modificare il nome in LoggingLibrary e fare clic su Crea.</span><span class="sxs-lookup"><span data-stu-id="7c30e-128">Change the name to LoggingLibrary, and click Create.</span></span>

    ![Nuova configurazione di app vuota (Novell. Forms Portable) in Visual Studio 2019](media/CrossPlatform-NewProject19-Part2.png)

<span data-ttu-id="7c30e-130">La soluzione risultante contiene due progetti condivisi, insieme a un'ampia gamma di progetti specifici della piattaforma:</span><span class="sxs-lookup"><span data-stu-id="7c30e-130">The resulting solution contains two Shared projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="7c30e-131">Il progetto `ILoggingLibrary`, contenuto nel file di `ILoggingLibrary.shared.cs`, definisce l'interfaccia pubblica (superficie di attacco API) del componente.</span><span class="sxs-lookup"><span data-stu-id="7c30e-131">The `ILoggingLibrary` project, which is contained in the `ILoggingLibrary.shared.cs` file, defines the public interface (the API surface area) of the component.</span></span> <span data-ttu-id="7c30e-132">dove viene definita l'interfaccia per la libreria.</span><span class="sxs-lookup"><span data-stu-id="7c30e-132">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="7c30e-133">L'altro progetto condiviso contiene codice in `CrossLoggingLibrary.shared.cs` che individua un'implementazione specifica della piattaforma dell'interfaccia astratta in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7c30e-133">The other Shared project contains code in `CrossLoggingLibrary.shared.cs` that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="7c30e-134">In genere non è necessario modificare questo file.</span><span class="sxs-lookup"><span data-stu-id="7c30e-134">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="7c30e-135">I progetti specifici della piattaforma, ad esempio `LoggingLibrary.android.cs`, ognuno contengono un'implementazione nativa dell'interfaccia nei rispettivi file di `LoggingLibraryImplementation.cs` (VS 2017) o `LoggingLibrary.<PLATFORM>.cs` (VS 2019).</span><span class="sxs-lookup"><span data-stu-id="7c30e-135">The platform-specific projects, such as `LoggingLibrary.android.cs`, each contain contain a native implementation of the interface in their respective `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) files.</span></span> <span data-ttu-id="7c30e-136">dove si compila il codice della libreria.</span><span class="sxs-lookup"><span data-stu-id="7c30e-136">This is where you build out your library's code.</span></span>

<span data-ttu-id="7c30e-137">Per impostazione predefinita, il file ILoggingLibrary.shared.cs del progetto `ILoggingLibrary` contiene una definizione di interfaccia, ma nessun metodo.</span><span class="sxs-lookup"><span data-stu-id="7c30e-137">By default, the ILoggingLibrary.shared.cs file of the `ILoggingLibrary` project contains an interface definition, but no methods.</span></span> <span data-ttu-id="7c30e-138">Ai fini di questa procedura dettagliata, aggiungere un metodo `Log` come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7c30e-138">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace Plugin.LoggingLibrary
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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="7c30e-139">Scrivere il codice specifico della piattaforma</span><span class="sxs-lookup"><span data-stu-id="7c30e-139">Write your platform-specific code</span></span>

<span data-ttu-id="7c30e-140">Per eseguire un'implementazione specifica della piattaforma dell'interfaccia `ILoggingLibrary` e dei relativi metodi, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7c30e-140">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="7c30e-141">Aprire il file `LoggingLibraryImplementation.cs` (VS 2017) o `LoggingLibrary.<PLATFORM>.cs` (VS 2019) di ogni progetto di piattaforma e aggiungere il codice necessario.</span><span class="sxs-lookup"><span data-stu-id="7c30e-141">Open the `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) file of each platform project and add the necessary code.</span></span> <span data-ttu-id="7c30e-142">Ad esempio (usando il progetto piattaforma `Android`):</span><span class="sxs-lookup"><span data-stu-id="7c30e-142">For example (using the `Android` platform project):</span></span>

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Text;

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

1. <span data-ttu-id="7c30e-143">Ripetere questa implementazione nei progetti per ogni piattaforma che si vuole supportare.</span><span class="sxs-lookup"><span data-stu-id="7c30e-143">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="7c30e-144">Fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Compila soluzione** per controllare il lavoro e generare gli elementi per cui in seguito verrà creato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="7c30e-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="7c30e-145">Se vengono visualizzati errori su riferimenti mancanti, fare clic con il pulsante destro del mouse sulla soluzione, scegliere **Ripristina pacchetti NuGet** per installare le dipendenze ed eseguire di nuovo la compilazione.</span><span class="sxs-lookup"><span data-stu-id="7c30e-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="7c30e-146">Se si usa Visual Studio 2019, prima di selezionare **Ripristina pacchetti NuGet** e si tenta di ricompilare, è necessario modificare la versione di `MSBuild.Sdk.Extras` in `2.0.54` `LoggingLibrary.csproj`.</span><span class="sxs-lookup"><span data-stu-id="7c30e-146">If you are using Visual Studio 2019, before selecting **Restore NuGet Packages** and trying to rebuild, you need to change the version of `MSBuild.Sdk.Extras` to `2.0.54` in `LoggingLibrary.csproj`.</span></span> <span data-ttu-id="7c30e-147">È possibile accedere a questo file solo facendo clic con il pulsante destro del mouse sul progetto (sotto la soluzione) e selezionando `Unload Project`, quindi fare clic con il pulsante destro del mouse sul progetto scaricato e selezionare `Edit LoggingLibrary.csproj`.</span><span class="sxs-lookup"><span data-stu-id="7c30e-147">This file can only be accessed by first right-clicking the project (below the solution) and selecting `Unload Project`, after which you right-click on the unloaded project and select `Edit LoggingLibrary.csproj`.</span></span>

> [!Note]
> <span data-ttu-id="7c30e-148">Per eseguire la compilazione per iOS, è necessario un Mac in rete connesso a Visual Studio, come descritto in [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/) (Introduzione a Xamarin.iOS per Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="7c30e-148">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="7c30e-149">Se non è disponibile un Mac, cancellare il progetto iOS in Gestione configurazione (passaggio 3).</span><span class="sxs-lookup"><span data-stu-id="7c30e-149">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="7c30e-150">Creare e aggiornare il file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="7c30e-150">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="7c30e-151">Aprire un prompt dei comandi, passare alla cartella `LoggingLibrary`, di un livello inferiore rispetto alla posizione del file `.sln`, ed eseguire il comando `spec` di NuGet per creare il file `Package.nuspec` iniziale:</span><span class="sxs-lookup"><span data-stu-id="7c30e-151">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="7c30e-152">Rinominare questo file in `LoggingLibrary.nuspec` e aprirlo in un editor.</span><span class="sxs-lookup"><span data-stu-id="7c30e-152">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="7c30e-153">Aggiornare il file in modo che corrisponda a quanto segue, sostituendo YOUR_NAME con un valore appropriato.</span><span class="sxs-lookup"><span data-stu-id="7c30e-153">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="7c30e-154">Il valore `<id>`, in particolare, deve essere univoco in nuget.org. Vedere le convenzioni di denominazione descritte in [Creazione di un pacchetto](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="7c30e-154">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="7c30e-155">Tenere inoltre presente che è anche necessario aggiornare i tag relativi all'autore e alla descrizione o si verifica un errore durante il passaggio di creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="7c30e-155">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2018</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="7c30e-156">È possibile aggiungere alla versione del pacchetto il suffisso `-alpha`, `-beta` o `-rc` per contrassegnare il pacchetto come non definitivo. Per altre informazioni sulle versioni non definitive, vedere [Versioni non definitive](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="7c30e-156">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="7c30e-157">Aggiungere assembly di riferimento</span><span class="sxs-lookup"><span data-stu-id="7c30e-157">Add reference assemblies</span></span>

<span data-ttu-id="7c30e-158">Per includere gli assembly di riferimento specifici della piattaforma, aggiungere il codice seguente all'elemento `<files>` di `LoggingLibrary.nuspec` in modo appropriato alle piattaforme supportate:</span><span class="sxs-lookup"><span data-stu-id="7c30e-158">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="7c30e-159">Per abbreviare i nomi dei file DLL e XML, fare clic con il pulsante destro del mouse su un determinato progetto, scegliere la scheda **Libreria** e modificare i nomi degli assembly.</span><span class="sxs-lookup"><span data-stu-id="7c30e-159">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="7c30e-160">Aggiungere dipendenze</span><span class="sxs-lookup"><span data-stu-id="7c30e-160">Add dependencies</span></span>

<span data-ttu-id="7c30e-161">Se sono presenti dipendenze specifiche per le implementazioni native, usare l'elemento `<dependencies>` con gli elementi `<group>` per specificarle, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7c30e-161">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="7c30e-162">Il codice seguente, ad esempio, imposterà iTextSharp come dipendenza per la destinazione UAP:</span><span class="sxs-lookup"><span data-stu-id="7c30e-162">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="7c30e-163">File con estensione nuspec finale</span><span class="sxs-lookup"><span data-stu-id="7c30e-163">Final .nuspec</span></span>

<span data-ttu-id="7c30e-164">Il file `.nuspec` finale sarà simile al seguente, dove YOUR_NAME deve essere sostituito con un valore appropriato:</span><span class="sxs-lookup"><span data-stu-id="7c30e-164">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2018</copyright>
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

## <a name="package-the-component"></a><span data-ttu-id="7c30e-165">Creare un pacchetto per il componente</span><span class="sxs-lookup"><span data-stu-id="7c30e-165">Package the component</span></span>

<span data-ttu-id="7c30e-166">Dopo avere completato il file `.nuspec` che fa riferimento a tutti i file da includere nel pacchetto, è possibile eseguire il comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="7c30e-166">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="7c30e-167">Verrà generato `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="7c30e-167">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="7c30e-168">Aprendo il file in uno strumento come [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ed espandendo tutti i nodi, vengono visualizzati i contenuti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7c30e-168">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet Package Explorer che visualizza il pacchetto LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="7c30e-170">Un file `.nupkg` è solo un file ZIP con un'estensione diversa.</span><span class="sxs-lookup"><span data-stu-id="7c30e-170">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="7c30e-171">È anche possibile esaminare i contenuti del pacchetto, modificando `.nupkg` in `.zip`, ma si ricordi di ripristinare l'estensione prima di caricare un pacchetto in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7c30e-171">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="7c30e-172">Per rendere disponibile il pacchetto per altri sviluppatori, seguire le istruzioni in [Pubblicare un pacchetto](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="7c30e-172">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="7c30e-173">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="7c30e-173">Related topics</span></span>

- [<span data-ttu-id="7c30e-174">Informazioni di riferimento sul file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="7c30e-174">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="7c30e-175">Pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="7c30e-175">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="7c30e-176">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="7c30e-176">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="7c30e-177">Supporto di più versioni di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="7c30e-177">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="7c30e-178">Includere proprietà e destinazioni MSBuild in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="7c30e-178">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="7c30e-179">Creazione di pacchetti localizzati</span><span class="sxs-lookup"><span data-stu-id="7c30e-179">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)