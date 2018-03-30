---
title: Guida introduttiva alla creazione e alla pubblicazione di un pacchetto NuGet .NET Standard con Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/18/2018
ms.topic: quickstart
ms.prod: nuget
ms.technology: ''
description: Esercitazione sulla creazione e pubblicazione di un pacchetto NuGet .NET Standard con Visual Studio 2017.
keywords: Creazione del pacchetto NuGet, pubblicazione del pacchetto NuGet, esercitazione NuGet, creare un pacchetto NuGet in Visual Studio, pacchetto msbuild
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: cdfaf437b30f507f1227f9e6dbd8b039c5bf4402
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="create-and-publish-a-package-using-visual-studio-net-standard"></a><span data-ttu-id="feb54-104">Creare e pubblicare un pacchetto con Visual Studio (.NET Standard)</span><span class="sxs-lookup"><span data-stu-id="feb54-104">Create and publish a package using Visual Studio (.NET Standard)</span></span>

<span data-ttu-id="feb54-105">La creazione di un pacchetto NuGet da una libreria di classi .NET Standard in Visual Studio e la pubblicazione in nuget.org tramite uno strumento di interfaccia della riga di comando sono un processo semplice.</span><span class="sxs-lookup"><span data-stu-id="feb54-105">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio, and then publish it to nuget.org using a CLI tool.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="feb54-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="feb54-106">Prerequisites</span></span>

1. <span data-ttu-id="feb54-107">Installare qualsiasi edizione di Visual Studio 2017 da [visualstudio.com](https://www.visualstudio.com/) con qualsiasi carico di lavoro correlato a .NET.</span><span class="sxs-lookup"><span data-stu-id="feb54-107">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="feb54-108">Visual Studio 2017 include automaticamente le funzionalità di NuGet quando viene installato un carico di lavoro .NET.</span><span class="sxs-lookup"><span data-stu-id="feb54-108">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="feb54-109">Installare l'interfaccia della riga di comando `nuget.exe` scaricandola da [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), salvare il file `.exe` in una cartella appropriata e aggiungere tale cartella alla variabile di ambiente PATH.</span><span class="sxs-lookup"><span data-stu-id="feb54-109">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="feb54-110">In alternativa, se è installato [.NET Core SDK](https://www.microsoft.com/net/download/), è possibile usare l'interfaccia della riga di comando `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="feb54-110">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="feb54-111">[Registrarsi per ottenere un account gratuito in nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) se non è già disponibile.</span><span class="sxs-lookup"><span data-stu-id="feb54-111">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="feb54-112">Quando si crea un nuovo account, viene inviato un messaggio di posta elettronica di conferma.</span><span class="sxs-lookup"><span data-stu-id="feb54-112">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="feb54-113">È necessario confermare l'account prima di poter caricare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="feb54-113">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="feb54-114">Creare un progetto di libreria di classi</span><span class="sxs-lookup"><span data-stu-id="feb54-114">Create a class library project</span></span>

<span data-ttu-id="feb54-115">È possibile usare un progetto libreria di classi .NET Standard esistente per il codice che si vuole includere in un pacchetto oppure creare un progetto semplice come segue:</span><span class="sxs-lookup"><span data-stu-id="feb54-115">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="feb54-116">In Visual Studio scegliere **File > Nuovo > Progetto**, espandere il nodo **Visual C# > .NET Standard**, selezionare il modello "Libreria di classi (.NET Standard)", assegnare al progetto il nome AppLogger e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="feb54-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="feb54-117">Fare clic con il pulsante destro del mouse sul file di progetto risultante e scegliere **Compila** per verificare che il progetto sia stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="feb54-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="feb54-118">La DLL è presente nella cartella Debug (o Release se si crea invece tale configurazione).</span><span class="sxs-lookup"><span data-stu-id="feb54-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="feb54-119">In un vero pacchetto NuGet si implementano ovviamente molte funzionalità utili, che altri possono sfruttare per compilare nuove applicazioni.</span><span class="sxs-lookup"><span data-stu-id="feb54-119">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="feb54-120">In questa procedura dettagliata tuttavia non si scriverà codice aggiuntivo perché una libreria di classi dal modello è sufficiente per creare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="feb54-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="feb54-121">Tuttavia, se si desidera del codice funzionale per il pacchetto, usare le opzioni riportate di seguito:</span><span class="sxs-lookup"><span data-stu-id="feb54-121">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="feb54-122">A meno che non esista un motivo valido per decidere diversamente, .NET Standard è la destinazione preferita per i pacchetti NuGet, perché garantisce la compatibilità con la gamma più ampia di progetti consumer.</span><span class="sxs-lookup"><span data-stu-id="feb54-122">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="feb54-123">Configurare le proprietà del pacchetto</span><span class="sxs-lookup"><span data-stu-id="feb54-123">Configure package properties</span></span>

1. <span data-ttu-id="feb54-124">Scegliere il comando di menu **Progetto > Proprietà** e quindi selezionare la scheda **Pacchetto**. La scheda **Pacchetto** viene visualizzata solo per i progetti di libreria di classi .NET Standard. Se la destinazione è .NET Framework, vedere invece [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) (Creare e pubblicare un pacchetto .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="feb54-124">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.)</span></span>

    ![Proprietà del pacchetto NuGet in un progetto di Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="feb54-126">Per i pacchetti compilati per uso pubblico, prestare particolare attenzione alla proprietà **Tags**, perché i tag consentono ad altri utenti di trovare il pacchetto e di comprenderne le funzioni.</span><span class="sxs-lookup"><span data-stu-id="feb54-126">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="feb54-127">Assegnare al pacchetto un identificatore univoco e compilare tutte le altre proprietà desiderate.</span><span class="sxs-lookup"><span data-stu-id="feb54-127">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="feb54-128">Per una descrizione delle diverse proprietà, vedere [Informazioni di riferimento sul file .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="feb54-128">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="feb54-129">Tutte queste proprietà vengono incluse nel manifesto `.nuspec` creato da Visual Studio per il progetto.</span><span class="sxs-lookup"><span data-stu-id="feb54-129">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="feb54-130">È necessario assegnare al pacchetto un identificatore univoco in nuget.org o per qualsiasi host in uso.</span><span class="sxs-lookup"><span data-stu-id="feb54-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="feb54-131">Per questa procedura dettagliata, si consiglia di includere "Sample" o "Test" nel nome, perché il passaggio di pubblicazione descritto più avanti rende il pacchetto visibile pubblicamente (nonostante sia improbabile che chiunque lo usi effettivamente).</span><span class="sxs-lookup"><span data-stu-id="feb54-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="feb54-132">Se si tenta di pubblicare un pacchetto con un nome già esistente, viene visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="feb54-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="feb54-133">Facoltativo: per visualizzare le proprietà direttamente nel file di progetto, fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e selezionare **Edit AppLogger.csproj** (Modifica AppLogger.csproj).</span><span class="sxs-lookup"><span data-stu-id="feb54-133">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="feb54-134">Eseguire il comando pack</span><span class="sxs-lookup"><span data-stu-id="feb54-134">Run the pack command</span></span>

1. <span data-ttu-id="feb54-135">Impostare la configurazione da **rilasciare**.</span><span class="sxs-lookup"><span data-stu-id="feb54-135">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="feb54-136">Fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** e scegliere il comando **Pack**.</span><span class="sxs-lookup"><span data-stu-id="feb54-136">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Comando pack NuGet nel menu di scelta rapida del progetto di Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="feb54-138">Visual Studio compila il progetto e crea il file `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="feb54-138">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="feb54-139">Esaminare i dettagli nella finestra **Output** (simile alla seguente), che contiene il percorso del file di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="feb54-139">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="feb54-140">Si noti inoltre che l'assembly compilato si trova in `bin\Release\netstandard2.0` secondo quanto conforme alla destinazione .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="feb54-140">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="feb54-141">Opzione alternativa: pacchetto con MSBuild</span><span class="sxs-lookup"><span data-stu-id="feb54-141">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="feb54-142">In alternativa all'uso del comando di menu **Pack** (Pacchetto), NuGet 4.x+ e MSBuild 15.1+ supportano una destinazione `pack` quando il progetto contiene i dati necessari del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="feb54-142">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="feb54-143">Aprire un prompt dei comandi, passare alla cartella del progetto ed eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="feb54-143">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="feb54-144">(In genere, è consigliabile avviare il "Prompt dei comandi per gli sviluppatori per Visual Studio" dal menu Start, in modo che venga configurato con tutti i percorsi necessari per MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="feb54-144">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="feb54-145">Pertanto, è possibile trovare il pacchetto nella cartella `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="feb54-145">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="feb54-146">Per altre opzioni con `msbuild /t:pack`, vedere [Pack e restore di NuGet come destinazioni MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="feb54-146">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="feb54-147">Pubblicare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="feb54-147">Publish the package</span></span>

<span data-ttu-id="feb54-148">Dopo aver creato un file `.nupkg`, pubblicarlo in nuget.org usando l'interfaccia della riga di comando `nuget.exe` o `dotnet.exe` insieme a una chiave API acquisita da nuget.org.</span><span class="sxs-lookup"><span data-stu-id="feb54-148">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="feb54-149">Acquisire la chiave API</span><span class="sxs-lookup"><span data-stu-id="feb54-149">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="feb54-150">Pubblicare con nuget push</span><span class="sxs-lookup"><span data-stu-id="feb54-150">Publish with nuget push</span></span>

<span data-ttu-id="feb54-151">Questo passaggio è un'alternativa all'uso di `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="feb54-151">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="feb54-152">Passare alla cartella contenente il file `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="feb54-152">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="feb54-153">Eseguire il comando seguente, specificando il nome del pacchetto e sostituendo il valore di chiave con la chiave API:</span><span class="sxs-lookup"><span data-stu-id="feb54-153">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="feb54-154">nuget.exe visualizza i risultati del processo di pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="feb54-154">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="feb54-155">Vedere [nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="feb54-155">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="feb54-156">Pubblicare con dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="feb54-156">Publish with dotnet nuget push</span></span>

<span data-ttu-id="feb54-157">Questo passaggio è un'alternativa all'uso di `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="feb54-157">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="feb54-158">Errori di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="feb54-158">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="feb54-159">Gestire il pacchetto pubblicato</span><span class="sxs-lookup"><span data-stu-id="feb54-159">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="feb54-160">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="feb54-160">Related topics</span></span>

- [<span data-ttu-id="feb54-161">Creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="feb54-161">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="feb54-162">Pubblicare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="feb54-162">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="feb54-163">Supportare più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="feb54-163">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="feb54-164">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="feb54-164">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="feb54-165">Creazione di pacchetti localizzati</span><span class="sxs-lookup"><span data-stu-id="feb54-165">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="feb54-166">Documentazione della libreria .NET Standard</span><span class="sxs-lookup"><span data-stu-id="feb54-166">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="feb54-167">Portabilità in .NET Core da .NET Framework</span><span class="sxs-lookup"><span data-stu-id="feb54-167">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)