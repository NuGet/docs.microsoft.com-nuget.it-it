---
title: Creare e pubblicare un pacchetto .NET Standard con Visual Studio in Windows
description: Esercitazione sulla creazione e pubblicazione di un pacchetto NuGet .NET Standard con Visual Studio 2017 in Windows.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: c75785d361f25564c8a59d7a2d85924c570a7b9a
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467808"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="6fe64-103">Guida introduttiva: Creare e pubblicare un pacchetto NuGet con Visual Studio (.NET Standard, solo Windows)</span><span class="sxs-lookup"><span data-stu-id="6fe64-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="6fe64-104">La creazione di un pacchetto NuGet da una libreria di classi .NET Standard in Visual Studio in Windows e la pubblicazione in nuget.org tramite uno strumento di interfaccia della riga di comando sono un processo semplice.</span><span class="sxs-lookup"><span data-stu-id="6fe64-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="6fe64-105">Questa guida introduttiva si applica solo a Visual Studio 2017 per Windows.</span><span class="sxs-lookup"><span data-stu-id="6fe64-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="6fe64-106">Visual Studio per Mac non include le funzionalità descritte di seguito.</span><span class="sxs-lookup"><span data-stu-id="6fe64-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="6fe64-107">Usare invece gli [strumenti dell'interfaccia della riga di comando dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6fe64-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fe64-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6fe64-108">Prerequisites</span></span>

1. <span data-ttu-id="6fe64-109">Installare qualsiasi edizione di Visual Studio 2017 da [visualstudio.com](https://www.visualstudio.com/) con qualsiasi carico di lavoro correlato a .NET.</span><span class="sxs-lookup"><span data-stu-id="6fe64-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="6fe64-110">Visual Studio 2017 include automaticamente le funzionalità di NuGet quando viene installato un carico di lavoro .NET.</span><span class="sxs-lookup"><span data-stu-id="6fe64-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="6fe64-111">Installare uno degli strumenti dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="6fe64-111">Install one of the CLI tools.</span></span>

   * <span data-ttu-id="6fe64-112">Per l'interfaccia della riga di comando `dotnet`, installare [.NET Core SDK](https://www.microsoft.com/net/download/).</span><span class="sxs-lookup"><span data-stu-id="6fe64-112">For the `dotnet` CLI, install the [.NET Core SDK](https://www.microsoft.com/net/download/).</span></span> <span data-ttu-id="6fe64-113">L'interfaccia della riga di comando dotnet è necessaria per i progetti .NET Standard che usano il formato in stile SDK (attributo SDK).</span><span class="sxs-lookup"><span data-stu-id="6fe64-113">The dotnet CLI is required for .NET Standard projects that use the SDK-style format (SDK attribute).</span></span>

   * <span data-ttu-id="6fe64-114">Per l'interfaccia della riga di comando `nuget.exe`, scaricarla da [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), salvare il file `.exe` in una cartella appropriata e aggiungere tale cartella alla variabile di ambiente PATH.</span><span class="sxs-lookup"><span data-stu-id="6fe64-114">For the `nuget.exe` CLI, download it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving the `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span> <span data-ttu-id="6fe64-115">L'interfaccia della riga di comando nuget.exe viene usata per le librerie .NET Standard in formato non in stile SDK.</span><span class="sxs-lookup"><span data-stu-id="6fe64-115">The nuget.exe CLI is used for .NET Standard libraries in the non-SDK-style format.</span></span>

1. <span data-ttu-id="6fe64-116">[Registrarsi per ottenere un account gratuito in nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) se non è già disponibile.</span><span class="sxs-lookup"><span data-stu-id="6fe64-116">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="6fe64-117">Quando si crea un nuovo account, viene inviato un messaggio di posta elettronica di conferma.</span><span class="sxs-lookup"><span data-stu-id="6fe64-117">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="6fe64-118">È necessario confermare l'account prima di poter caricare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6fe64-118">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="6fe64-119">Creare un progetto di libreria di classi</span><span class="sxs-lookup"><span data-stu-id="6fe64-119">Create a class library project</span></span>

<span data-ttu-id="6fe64-120">È possibile usare un progetto libreria di classi .NET Standard esistente per il codice che si vuole includere in un pacchetto oppure creare un progetto semplice come segue:</span><span class="sxs-lookup"><span data-stu-id="6fe64-120">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="6fe64-121">In Visual Studio scegliere **File > Nuovo > Progetto**, espandere il nodo **Visual C# > .NET Standard**, selezionare il modello "Libreria di classi (.NET Standard)", assegnare al progetto il nome AppLogger e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6fe64-121">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="6fe64-122">Fare clic con il pulsante destro del mouse sul file di progetto risultante e scegliere **Compila** per verificare che il progetto sia stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="6fe64-122">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="6fe64-123">La DLL è presente nella cartella Debug (o Release se si crea invece tale configurazione).</span><span class="sxs-lookup"><span data-stu-id="6fe64-123">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="6fe64-124">In un vero pacchetto NuGet si implementano ovviamente molte funzionalità utili, che altri possono sfruttare per compilare nuove applicazioni.</span><span class="sxs-lookup"><span data-stu-id="6fe64-124">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="6fe64-125">In questa procedura dettagliata tuttavia non si scriverà codice aggiuntivo perché una libreria di classi dal modello è sufficiente per creare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6fe64-125">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="6fe64-126">Tuttavia, se si desidera del codice funzionale per il pacchetto, usare le opzioni riportate di seguito:</span><span class="sxs-lookup"><span data-stu-id="6fe64-126">Still, if you'd like some functional code for the package, use the following:</span></span>

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

> [!Tip]
> <span data-ttu-id="6fe64-127">A meno che non esista un motivo valido per decidere diversamente, .NET Standard è la destinazione preferita per i pacchetti NuGet, perché garantisce la compatibilità con la gamma più ampia di progetti consumer.</span><span class="sxs-lookup"><span data-stu-id="6fe64-127">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="6fe64-128">Configurare le proprietà del pacchetto</span><span class="sxs-lookup"><span data-stu-id="6fe64-128">Configure package properties</span></span>

1. <span data-ttu-id="6fe64-129">Scegliere il comando di menu **Progetto > Proprietà** e quindi selezionare la scheda **Pacchetto**. (La scheda **Pacchetto** viene visualizzata solo per i progetti di libreria di classi .NET Standard. Se la destinazione è .NET Framework, vedere invece [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) (Creare e pubblicare un pacchetto .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="6fe64-129">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="6fe64-130">Se non viene visualizzata per un progetto .NET Standard, potrebbe essere necessario aggiornare Visual Studio 2017 alla versione più recente.)</span><span class="sxs-lookup"><span data-stu-id="6fe64-130">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![Proprietà del pacchetto NuGet in un progetto di Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="6fe64-132">Per i pacchetti compilati per uso pubblico, prestare particolare attenzione alla proprietà **Tags**, perché i tag consentono ad altri utenti di trovare il pacchetto e di comprenderne le funzioni.</span><span class="sxs-lookup"><span data-stu-id="6fe64-132">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="6fe64-133">Assegnare al pacchetto un identificatore univoco e compilare tutte le altre proprietà desiderate.</span><span class="sxs-lookup"><span data-stu-id="6fe64-133">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="6fe64-134">Per una descrizione delle diverse proprietà, vedere [Informazioni di riferimento sul file .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="6fe64-134">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="6fe64-135">Tutte queste proprietà vengono incluse nel manifesto `.nuspec` creato da Visual Studio per il progetto.</span><span class="sxs-lookup"><span data-stu-id="6fe64-135">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="6fe64-136">È necessario assegnare al pacchetto un identificatore univoco in nuget.org o per qualsiasi host in uso.</span><span class="sxs-lookup"><span data-stu-id="6fe64-136">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="6fe64-137">Per questa procedura dettagliata, si consiglia di includere "Sample" o "Test" nel nome, perché il passaggio di pubblicazione descritto più avanti rende il pacchetto visibile pubblicamente (nonostante sia improbabile che chiunque lo usi effettivamente).</span><span class="sxs-lookup"><span data-stu-id="6fe64-137">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="6fe64-138">Se si tenta di pubblicare un pacchetto con un nome già esistente, viene visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="6fe64-138">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="6fe64-139">Facoltativo: per visualizzare le proprietà direttamente nel file di progetto, fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e selezionare **Edit AppLogger.csproj** (Modifica AppLogger.csproj).</span><span class="sxs-lookup"><span data-stu-id="6fe64-139">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="6fe64-140">Eseguire il comando pack</span><span class="sxs-lookup"><span data-stu-id="6fe64-140">Run the pack command</span></span>

1. <span data-ttu-id="6fe64-141">Impostare la configurazione da **rilasciare**.</span><span class="sxs-lookup"><span data-stu-id="6fe64-141">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="6fe64-142">Fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** e scegliere il comando **Pack**.</span><span class="sxs-lookup"><span data-stu-id="6fe64-142">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Comando pack NuGet nel menu di scelta rapida del progetto di Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="6fe64-144">Visual Studio compila il progetto e crea il file `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="6fe64-144">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="6fe64-145">Esaminare i dettagli nella finestra **Output** (simile alla seguente), che contiene il percorso del file di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6fe64-145">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="6fe64-146">Si noti inoltre che l'assembly compilato si trova in `bin\Release\netstandard2.0` secondo quanto conforme alla destinazione .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="6fe64-146">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="6fe64-147">Opzione alternativa: pacchetto con MSBuild</span><span class="sxs-lookup"><span data-stu-id="6fe64-147">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="6fe64-148">In alternativa all'uso del comando di menu **Pack** (Pacchetto), NuGet 4.x+ e MSBuild 15.1+ supportano una destinazione `pack` quando il progetto contiene i dati necessari del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6fe64-148">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="6fe64-149">Aprire un prompt dei comandi, passare alla cartella del progetto ed eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="6fe64-149">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="6fe64-150">(In genere, è consigliabile avviare il "Prompt dei comandi per gli sviluppatori per Visual Studio" dal menu Start, in modo che venga configurato con tutti i percorsi necessari per MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="6fe64-150">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="6fe64-151">Pertanto, è possibile trovare il pacchetto nella cartella `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="6fe64-151">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="6fe64-152">Per altre opzioni con `msbuild -t:pack`, vedere [Pack e restore di NuGet come destinazioni MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="6fe64-152">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="6fe64-153">Pubblicare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="6fe64-153">Publish the package</span></span>

<span data-ttu-id="6fe64-154">Dopo aver creato un file `.nupkg`, pubblicarlo in nuget.org usando l'interfaccia della riga di comando `nuget.exe` o `dotnet.exe` insieme a una chiave API acquisita da nuget.org.</span><span class="sxs-lookup"><span data-stu-id="6fe64-154">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="6fe64-155">Acquisire la chiave API</span><span class="sxs-lookup"><span data-stu-id="6fe64-155">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="6fe64-156">Pubblicare con dotnet nuget push (interfaccia della riga di comando dotnet)</span><span class="sxs-lookup"><span data-stu-id="6fe64-156">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="6fe64-157">Questo passaggio è un'alternativa all'uso di `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="6fe64-157">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="6fe64-158">Pubblicare con nuget push (interfaccia della riga di comando nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="6fe64-158">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="6fe64-159">Questo passaggio è un'alternativa all'uso di `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="6fe64-159">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="6fe64-160">Passare alla cartella contenente il file `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="6fe64-160">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="6fe64-161">Eseguire il comando seguente, specificando il nome del pacchetto e sostituendo il valore di chiave con la chiave API:</span><span class="sxs-lookup"><span data-stu-id="6fe64-161">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="6fe64-162">nuget.exe visualizza i risultati del processo di pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="6fe64-162">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="6fe64-163">Vedere [nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="6fe64-163">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="6fe64-164">Errori di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="6fe64-164">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="6fe64-165">Gestire il pacchetto pubblicato</span><span class="sxs-lookup"><span data-stu-id="6fe64-165">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="6fe64-166">Aggiunta di un file leggimi e di altri file</span><span class="sxs-lookup"><span data-stu-id="6fe64-166">Adding a readme and other files</span></span>

<span data-ttu-id="6fe64-167">Per specificare direttamente i file da includere nel pacchetto, modificare il file di progetto e usare la proprietà `content`:</span><span class="sxs-lookup"><span data-stu-id="6fe64-167">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="6fe64-168">Verrà incluso un file denominato `readme.txt` nella radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6fe64-168">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="6fe64-169">Visual Studio visualizza i contenuti del file come testo normale subito dopo avere installato direttamente il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6fe64-169">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="6fe64-170">I file leggimi non vengono visualizzati per i pacchetti installati come dipendenze.</span><span class="sxs-lookup"><span data-stu-id="6fe64-170">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="6fe64-171">Ecco ad esempio come viene visualizzato il file leggimi per il pacchetto HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="6fe64-171">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Visualizzazione di un file leggimi per un pacchetto NuGet durante l'installazione](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="6fe64-173">La semplice aggiunta del file readme.txt nella radice del progetto non consente di includerlo nel pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="6fe64-173">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="6fe64-174">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="6fe64-174">Related topics</span></span>

- [<span data-ttu-id="6fe64-175">Creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="6fe64-175">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="6fe64-176">Pubblicare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="6fe64-176">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="6fe64-177">Pacchetti in versione non definitiva</span><span class="sxs-lookup"><span data-stu-id="6fe64-177">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="6fe64-178">Supportare più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="6fe64-178">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="6fe64-179">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="6fe64-179">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="6fe64-180">Creazione di pacchetti localizzati</span><span class="sxs-lookup"><span data-stu-id="6fe64-180">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="6fe64-181">Documentazione della libreria .NET Standard</span><span class="sxs-lookup"><span data-stu-id="6fe64-181">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="6fe64-182">Portabilità in .NET Core da .NET Framework</span><span class="sxs-lookup"><span data-stu-id="6fe64-182">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
