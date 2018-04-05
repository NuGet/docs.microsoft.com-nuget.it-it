---
title: Creare pacchetti NuGet di .NET Standard e .NET Framework con Visual Studio 2015 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: Procedura dettagliata end-to-end per la creazione di pacchetti NuGet di .NET Standard e .NET Framework con NuGet 3.x e Visual Studio 2015.
keywords: creare un pacchetto, pacchetti .NET Standard, pacchetti .NET Framework
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: dbe0a0788b5fc9ba37f7db601bd51c3e4f78f5b8
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="4f9cd-104">Creare pacchetti .NET Standard e .NET Framework con Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="4f9cd-104">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="4f9cd-105">**Nota:** Visual Studio 2017 è consigliato per lo sviluppo di librerie .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-105">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="4f9cd-106">Visual Studio 2015 può funzionare, ma in questa versione gli strumenti .NET Core hanno raggiunto solo lo stato di anteprima.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-106">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="4f9cd-107">Per utilizzare NuGet 4.x+ e Visual Studio 2017, vedere [Creare e pubblicare un pacchetto con Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="4f9cd-107">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="4f9cd-108">La [libreria .NET Standard](/dotnet/articles/standard/library) è una specifica formale delle API .NET che devono essere disponibili in tutti i runtime .NET, per creare in questo modo maggiore uniformità nell'ecosistema .NET.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-108">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="4f9cd-109">La libreria .NET Standard definisce un set uniforme di API della libreria di classi base per tutte le piattaforme .NET da implementare, indipendentemente dal carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-109">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="4f9cd-110">Consente agli sviluppatori di produrre codice utilizzabile in tutti i runtime .NET e riduce, se non elimina, le direttive di compilazione condizionale specifiche della piattaforma nel codice condiviso.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-110">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="4f9cd-111">Questa guida illustra la creazione di un pacchetto NuGet destinato a .NET Standard Library 1.4 o .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-111">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="4f9cd-112">Una libreria .NET Standard 1.4 funziona in .NET Framework 4.6.1, in Universal Windows Platform 10, in .NET Core e in Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-112">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="4f9cd-113">Per informazioni dettagliate, vedere la [tabella di mapping .NET Standard](/dotnet/standard/net-standard#net-implementation-support) (documentazione di .NET).</span><span class="sxs-lookup"><span data-stu-id="4f9cd-113">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="4f9cd-114">È possibile scegliere altre versioni della libreria .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-114">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f9cd-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4f9cd-115">Prerequisites</span></span>

1. <span data-ttu-id="4f9cd-116">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="4f9cd-116">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="4f9cd-117">(Solo .NET Standard) [.NET Core SDK](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="4f9cd-117">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="4f9cd-118">Interfaccia della riga di comando di NuGet.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-118">NuGet CLI.</span></span> <span data-ttu-id="4f9cd-119">Scaricare la versione più recente di nuget.exe da [nuget.org/downloads](https://nuget.org/downloads), salvandola in una posizione di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-119">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="4f9cd-120">Aggiungere quindi tale posizione alla variabile di ambiente PATH, se necessario.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-120">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="4f9cd-121">Poiché nuget.exe è di per sé lo strumento dell'interfaccia della riga di comando e non un programma di installazione, assicurarsi di salvare il file scaricato dal browser invece di eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-121">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="4f9cd-122">Creare il progetto di libreria di classi</span><span class="sxs-lookup"><span data-stu-id="4f9cd-122">Create the class library project</span></span>

1. <span data-ttu-id="4f9cd-123">In Visual Studio **File > Nuovo > Progetto**, espandere il nodo **Visual C# > Windows**, selezionare **Libreria di classi (portabile)**, modificare il nome in AppLogger e selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-123">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Creare il nuovo progetto di libreria di classi](media/NetStandard-NewProject.png)

1. <span data-ttu-id="4f9cd-125">Nella finestra di dialogo **Aggiungi libreria di classi portabile** visualizzata selezionare le opzioni per `.NET Framework 4.6` e `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-125">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="4f9cd-126">(Se la destinazione è .NET Framework, è possibile selezionare qualsiasi opzione appropriata.)</span><span class="sxs-lookup"><span data-stu-id="4f9cd-126">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="4f9cd-127">Se la destinazione è .NET Standard, fare clic con il pulsante destro del mouse su `AppLogger (Portable)` in Esplora soluzioni, scegliere **Proprietà**, selezionare la scheda **Libreria**, quindi selezionare **Imposta come destinazione la piattaforma standard .NET** nella sezione **Destinazione**.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-127">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="4f9cd-128">Questa azione richiede di confermare l'operazione e in seguito è possibile selezionare `.NET Standard 1.4` (o un'altra versione disponibile) nell'elenco a discesa:</span><span class="sxs-lookup"><span data-stu-id="4f9cd-128">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Impostazione della destinazione su .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="4f9cd-130">Fare clic sulla scheda **Compilazione**, impostare **Configurazione** su `Release` e selezionare la casella **File di documentazione XML**.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-130">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="4f9cd-131">Aggiungere il codice al componente, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4f9cd-131">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="4f9cd-132">Impostare la configurazione su Versione, compilare il progetto e controllare che nella cartella `bin\Release` vengano creati i file DLL e XML.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-132">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="4f9cd-133">Creare e aggiornare il file con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="4f9cd-133">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="4f9cd-134">Aprire un prompt dei comandi, passare alla cartella contenente la cartella `AppLogger.csproj` (di un livello inferiore rispetto alla posizione del file `.sln`) ed eseguire il comando `spec` di NuGet per creare il file `AppLogger.nuspec` iniziale:</span><span class="sxs-lookup"><span data-stu-id="4f9cd-134">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="4f9cd-135">Aprire `AppLogger.nuspec` in un editor e aggiornarlo in modo che corrisponda a quanto segue, sostituendo YOUR_NAME con un valore appropriato.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-135">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="4f9cd-136">Il valore `<id>`, in particolare, deve essere univoco in nuget.org. Vedere le convenzioni di denominazione descritte in [Creazione di un pacchetto](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="4f9cd-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="4f9cd-137">Tenere inoltre presente che è anche necessario aggiornare i tag relativi all'autore e alla descrizione o si verifica un errore durante il passaggio di creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="4f9cd-138">Aggiungere gli assembly di riferimento al file `.nuspec`, in particolare la DLL della libreria e il file XML IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="4f9cd-138">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="4f9cd-139">Se la destinazione è .NET Standard, le voci vengono visualizzate in modo simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4f9cd-139">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="4f9cd-140">Se la destinazione è .NET Framework, le voci vengono visualizzate in modo simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4f9cd-140">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="4f9cd-141">Fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Compila soluzione** per generare tutti i file per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-141">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="4f9cd-142">Dichiarazione delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="4f9cd-142">Declaring dependencies</span></span>

<span data-ttu-id="4f9cd-143">Se sono presenti dipendenze da altri pacchetti NuGet, elencarle nell'elemento `<dependencies>` del manifesto con gli elementi `<group>`.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-143">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="4f9cd-144">Ad esempio, per dichiarare una dipendenza da NewtonSoft.Json 8.0.3 o versione successiva, aggiungere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="4f9cd-144">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="4f9cd-145">La sintassi dell'attributo *version* qui indica che la versione 8.0.3 o successiva è accettabile.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-145">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="4f9cd-146">Per specificare intervalli di versioni diversi, vedere [Controllo delle versioni dei pacchetti](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4f9cd-146">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="4f9cd-147">Aggiunta di un file leggimi</span><span class="sxs-lookup"><span data-stu-id="4f9cd-147">Adding a readme</span></span>

<span data-ttu-id="4f9cd-148">Creare il file `readme.txt`, inserirlo nella cartella radice del progetto e farvi riferimento nel file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="4f9cd-148">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="4f9cd-149">Visual Studio visualizza il file `readme.txt` quando il pacchetto viene installato in un progetto.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-149">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="4f9cd-150">Il file non viene visualizzato quando viene installato in progetti .NET Core o per i pacchetti che vengono installati come dipendenza.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-150">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="4f9cd-151">Creare un pacchetto per il componente</span><span class="sxs-lookup"><span data-stu-id="4f9cd-151">Package the component</span></span>

<span data-ttu-id="4f9cd-152">Dopo avere completato il file `.nuspec` che fa riferimento a tutti i file da includere nel pacchetto, è possibile eseguire il comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="4f9cd-152">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="4f9cd-153">Questo codice genera `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-153">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="4f9cd-154">Aprendo il file in uno strumento come [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ed espandendo tutti i nodi, vengono visualizzati i contenuti seguenti (per .NET Standard):</span><span class="sxs-lookup"><span data-stu-id="4f9cd-154">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![NuGet Package Explorer che visualizza il pacchetto AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="4f9cd-156">Un file `.nupkg` è solo un file ZIP con un'estensione diversa.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-156">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="4f9cd-157">È anche possibile esaminare i contenuti del pacchetto, modificando `.nupkg` in `.zip`, ma si ricordi di ripristinare l'estensione prima di caricare un pacchetto in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-157">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="4f9cd-158">Per rendere disponibile il pacchetto per altri sviluppatori, seguire le istruzioni in [Pubblicare un pacchetto](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="4f9cd-158">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="4f9cd-159">Si noti che `pack` richiede Mono 4.4.2 su Mac OS X e non funziona nei sistemi Linux.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-159">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="4f9cd-160">In un Mac è anche necessario convertire i nomi di percorso di Windows nel file `.nuspec` in percorsi di tipo Unix.</span><span class="sxs-lookup"><span data-stu-id="4f9cd-160">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="4f9cd-161">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="4f9cd-161">Related topics</span></span>

- [<span data-ttu-id="4f9cd-162">Informazioni di riferimento sul file .nuspec</span><span class="sxs-lookup"><span data-stu-id="4f9cd-162">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="4f9cd-163">Supporto di più versioni di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="4f9cd-163">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="4f9cd-164">Includere proprietà e destinazioni MSBuild in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="4f9cd-164">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="4f9cd-165">Creazione di pacchetti localizzati</span><span class="sxs-lookup"><span data-stu-id="4f9cd-165">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="4f9cd-166">Pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="4f9cd-166">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="4f9cd-167">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="4f9cd-167">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="4f9cd-168">Documentazione della libreria .NET Standard</span><span class="sxs-lookup"><span data-stu-id="4f9cd-168">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="4f9cd-169">Portabilità in .NET Core da .NET Framework</span><span class="sxs-lookup"><span data-stu-id="4f9cd-169">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
