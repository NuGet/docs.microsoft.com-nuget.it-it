---
title: Creare e pubblicare un pacchetto .NET Standard con Visual Studio in Windows
description: Esercitazione sulla creazione e pubblicazione di un pacchetto NuGet .NET Standard con Visual Studio in Windows.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: quickstart
ms.openlocfilehash: d9eccfa373a5a283542fd158e76ba74b1872f3d6
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842129"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="02381-103">Guida introduttiva: Creare e pubblicare un pacchetto NuGet con Visual Studio (.NET Standard, solo Windows)</span><span class="sxs-lookup"><span data-stu-id="02381-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="02381-104">La creazione di un pacchetto NuGet da una libreria di classi .NET Standard in Visual Studio in Windows e la pubblicazione in nuget.org tramite uno strumento di interfaccia della riga di comando sono un processo semplice.</span><span class="sxs-lookup"><span data-stu-id="02381-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="02381-105">Se si usa Visual Studio per Mac, fare riferimento a [queste informazioni](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) per la creazione di un pacchetto NuGet o usare gli [strumenti dell'interfaccia della riga di comando dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="02381-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02381-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="02381-106">Prerequisites</span></span>

1. <span data-ttu-id="02381-107">Installare qualsiasi edizione di Visual Studio 2017 o versione successiva da [visualstudio.com](https://www.visualstudio.com/) con qualsiasi carico di lavoro correlato a .NET.</span><span class="sxs-lookup"><span data-stu-id="02381-107">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="02381-108">Visual Studio 2017 e versioni successive includono automaticamente le funzionalità di NuGet quando viene installato un carico di lavoro .NET.</span><span class="sxs-lookup"><span data-stu-id="02381-108">Visual Studio 2017 and higher automatically include NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="02381-109">Installare l'interfaccia della riga di comando `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="02381-109">Install the `dotnet` CLI.</span></span>

   <span data-ttu-id="02381-110">Per l'interfaccia della riga di comando `dotnet`, a partire da Visual Studio 2017, l'interfaccia della riga di comando `dotnet` viene installata automaticamente con qualsiasi carico di lavoro .NET Core correlato.</span><span class="sxs-lookup"><span data-stu-id="02381-110">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="02381-111">In caso contrario, installare [.NET Core SDK](https://www.microsoft.com/net/download/) per ottenere l'interfaccia della riga di comando `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="02381-111">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="02381-112">L'interfaccia della riga di comando `dotnet` è necessaria per i progetti .NET Standard che usano il [formato di tipo SDK](../resources/check-project-format.md) (attributo SDK).</span><span class="sxs-lookup"><span data-stu-id="02381-112">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="02381-113">Il modello di libreria di classi predefinito in Visual Studio 2017 e versioni successive, usato in questo articolo, usa l'attributo SDK.</span><span class="sxs-lookup"><span data-stu-id="02381-113">The default class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="02381-114">Per questo articolo, è consigliabile usare l'interfaccia della riga di comando `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="02381-114">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="02381-115">Sebbene sia possibile pubblicare un pacchetto NuGet usando l'interfaccia della riga di comando `nuget.exe`, alcuni dei passaggi descritti in questo articolo sono specifici per i progetti di tipo SDK e l'interfaccia della riga di comando dotnet.</span><span class="sxs-lookup"><span data-stu-id="02381-115">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="02381-116">L'interfaccia della riga di comando nuget.exe per i [progetti non di tipo SDK](../resources/check-project-format.md) (in genere .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="02381-116">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span> <span data-ttu-id="02381-117">Se si utilizza un progetto non di tipo SDK, seguire le procedure in [Creare e pubblicare un pacchetto .NET Framework (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) per creare e pubblicare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="02381-117">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package.</span></span>

1. <span data-ttu-id="02381-118">[Registrarsi per ottenere un account gratuito in nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) se non è già disponibile.</span><span class="sxs-lookup"><span data-stu-id="02381-118">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="02381-119">Quando si crea un nuovo account, viene inviato un messaggio di posta elettronica di conferma.</span><span class="sxs-lookup"><span data-stu-id="02381-119">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="02381-120">È necessario confermare l'account prima di poter caricare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="02381-120">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="02381-121">Creare un progetto di libreria di classi</span><span class="sxs-lookup"><span data-stu-id="02381-121">Create a class library project</span></span>

<span data-ttu-id="02381-122">È possibile usare un progetto libreria di classi .NET Standard esistente per il codice che si vuole includere in un pacchetto oppure creare un progetto semplice come segue:</span><span class="sxs-lookup"><span data-stu-id="02381-122">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="02381-123">In Visual Studio scegliere **File > Nuovo > Progetto**, espandere il nodo **Visual C# > .NET Standard**, selezionare il modello "Libreria di classi (.NET Standard)", assegnare al progetto il nome AppLogger e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="02381-123">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="02381-124">Fare clic con il pulsante destro del mouse sul file di progetto risultante e scegliere **Compila** per verificare che il progetto sia stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="02381-124">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="02381-125">La DLL è presente nella cartella Debug (o Release se si crea invece tale configurazione).</span><span class="sxs-lookup"><span data-stu-id="02381-125">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="02381-126">In un vero pacchetto NuGet si implementano ovviamente molte funzionalità utili, che altri possono sfruttare per compilare nuove applicazioni.</span><span class="sxs-lookup"><span data-stu-id="02381-126">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="02381-127">In questa procedura dettagliata tuttavia non si scriverà codice aggiuntivo perché una libreria di classi dal modello è sufficiente per creare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="02381-127">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="02381-128">Tuttavia, se si desidera del codice funzionale per il pacchetto, usare le opzioni riportate di seguito:</span><span class="sxs-lookup"><span data-stu-id="02381-128">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="02381-129">A meno che non esista un motivo valido per decidere diversamente, .NET Standard è la destinazione preferita per i pacchetti NuGet, perché garantisce la compatibilità con la gamma più ampia di progetti consumer.</span><span class="sxs-lookup"><span data-stu-id="02381-129">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="02381-130">Configurare le proprietà del pacchetto</span><span class="sxs-lookup"><span data-stu-id="02381-130">Configure package properties</span></span>

1. <span data-ttu-id="02381-131">Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e scegliere il comando di menu **Proprietà**, quindi selezionare la scheda **Pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="02381-131">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="02381-132">La scheda **Pacchetto** viene visualizzata solo per i progetti di tipo SDK in Visual Studio, in genere progetti di libreria di classi .NET Standard o .NET Core. Per i progetti non di tipo SDK (in genere .NET Framework), [eseguire la migrazione del progetto](../reference/migrate-packages-config-to-package-reference.md) e usare l'interfaccia della riga di comando `dotnet` oppure vedere [Creare e pubblicare un pacchetto .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) per istruzioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="02381-132">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Proprietà del pacchetto NuGet in un progetto di Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="02381-134">Per i pacchetti compilati per uso pubblico, prestare particolare attenzione alla proprietà **Tags**, perché i tag consentono ad altri utenti di trovare il pacchetto e di comprenderne le funzioni.</span><span class="sxs-lookup"><span data-stu-id="02381-134">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="02381-135">Assegnare al pacchetto un identificatore univoco e compilare tutte le altre proprietà desiderate.</span><span class="sxs-lookup"><span data-stu-id="02381-135">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="02381-136">Per una descrizione delle diverse proprietà, vedere [Informazioni di riferimento sul file .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="02381-136">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="02381-137">Tutte queste proprietà vengono incluse nel manifesto `.nuspec` creato da Visual Studio per il progetto.</span><span class="sxs-lookup"><span data-stu-id="02381-137">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="02381-138">È necessario assegnare al pacchetto un identificatore univoco in nuget.org o per qualsiasi host in uso.</span><span class="sxs-lookup"><span data-stu-id="02381-138">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="02381-139">Per questa procedura dettagliata, si consiglia di includere "Sample" o "Test" nel nome, perché il passaggio di pubblicazione descritto più avanti rende il pacchetto visibile pubblicamente (nonostante sia improbabile che chiunque lo usi effettivamente).</span><span class="sxs-lookup"><span data-stu-id="02381-139">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="02381-140">Se si tenta di pubblicare un pacchetto con un nome già esistente, viene visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="02381-140">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="02381-141">Facoltativo: per visualizzare le proprietà direttamente nel file di progetto, fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e selezionare **Edit AppLogger.csproj** (Modifica AppLogger.csproj).</span><span class="sxs-lookup"><span data-stu-id="02381-141">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="02381-142">Questa opzione è disponibile solo a partire da Visual Studio 2017 per i progetti che usano l'attributo SDK.</span><span class="sxs-lookup"><span data-stu-id="02381-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="02381-143">In caso contrario, fare clic con il pulsante destro del mouse sul progetto e scegliere **Scarica progetto**.</span><span class="sxs-lookup"><span data-stu-id="02381-143">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="02381-144">Fare quindi clic con il pulsante destro del mouse sul progetto scaricato e scegliere **Modifica AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="02381-144">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="02381-145">Eseguire il comando pack</span><span class="sxs-lookup"><span data-stu-id="02381-145">Run the pack command</span></span>

1. <span data-ttu-id="02381-146">Impostare la configurazione da **rilasciare**.</span><span class="sxs-lookup"><span data-stu-id="02381-146">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="02381-147">Fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** e scegliere il comando **Pack**.</span><span class="sxs-lookup"><span data-stu-id="02381-147">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Comando pack NuGet nel menu di scelta rapida del progetto di Visual Studio](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="02381-149">Se non viene visualizzato il comando **Pack**, il progetto non è probabilmente un progetto di tipo SDK ed è necessario usare l'interfaccia della riga di comando `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="02381-149">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="02381-150">[Eseguire la migrazione del progetto](../reference/migrate-packages-config-to-package-reference.md) e usare l'interfaccia della riga di comando `dotnet` oppure vedere [Creare e pubblicare un pacchetto .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) per istruzioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="02381-150">Either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="02381-151">Visual Studio compila il progetto e crea il file `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="02381-151">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="02381-152">Esaminare i dettagli nella finestra **Output** (simile alla seguente), che contiene il percorso del file di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="02381-152">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="02381-153">Si noti inoltre che l'assembly compilato si trova in `bin\Release\netstandard2.0` secondo quanto conforme alla destinazione .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="02381-153">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="02381-154">Opzione alternativa: pacchetto con MSBuild</span><span class="sxs-lookup"><span data-stu-id="02381-154">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="02381-155">In alternativa all'uso del comando di menu **Pack** (Pacchetto), NuGet 4.x+ e MSBuild 15.1+ supportano una destinazione `pack` quando il progetto contiene i dati necessari del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="02381-155">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="02381-156">Aprire un prompt dei comandi, passare alla cartella del progetto ed eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="02381-156">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="02381-157">(In genere, è consigliabile avviare il "Prompt dei comandi per gli sviluppatori per Visual Studio" dal menu Start, in modo che venga configurato con tutti i percorsi necessari per MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="02381-157">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="02381-158">Pertanto, è possibile trovare il pacchetto nella cartella `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="02381-158">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="02381-159">Per altre opzioni con `msbuild -t:pack`, vedere [Pack e restore di NuGet come destinazioni MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="02381-159">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="02381-160">Pubblicare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="02381-160">Publish the package</span></span>

<span data-ttu-id="02381-161">Dopo aver creato un file `.nupkg`, pubblicarlo in nuget.org usando l'interfaccia della riga di comando `nuget.exe` o `dotnet.exe` insieme a una chiave API acquisita da nuget.org.</span><span class="sxs-lookup"><span data-stu-id="02381-161">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="02381-162">Acquisire la chiave API</span><span class="sxs-lookup"><span data-stu-id="02381-162">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="02381-163">Pubblicare con dotnet nuget push (interfaccia della riga di comando dotnet)</span><span class="sxs-lookup"><span data-stu-id="02381-163">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="02381-164">Questo passaggio è l'alternativa consigliata all'uso di `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="02381-164">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="02381-165">Prima di poter pubblicare il pacchetto, è necessario aprire una riga di comando.</span><span class="sxs-lookup"><span data-stu-id="02381-165">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="02381-166">Pubblicare con nuget push (interfaccia della riga di comando nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="02381-166">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="02381-167">Questo passaggio è un'alternativa all'uso di `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="02381-167">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="02381-168">Aprire una riga di comando e passare alla cartella che contiene il file `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="02381-168">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="02381-169">Eseguire il comando seguente, specificando il nome del pacchetto (ID pacchetto univoco) e sostituendo il valore di chiave con la chiave API:</span><span class="sxs-lookup"><span data-stu-id="02381-169">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="02381-170">nuget.exe visualizza i risultati del processo di pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="02381-170">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="02381-171">Vedere [nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="02381-171">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="02381-172">Errori di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="02381-172">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="02381-173">Gestire il pacchetto pubblicato</span><span class="sxs-lookup"><span data-stu-id="02381-173">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="02381-174">Aggiunta di un file leggimi e di altri file</span><span class="sxs-lookup"><span data-stu-id="02381-174">Adding a readme and other files</span></span>

<span data-ttu-id="02381-175">Per specificare direttamente i file da includere nel pacchetto, modificare il file di progetto e usare la proprietà `content`:</span><span class="sxs-lookup"><span data-stu-id="02381-175">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="02381-176">Verrà incluso un file denominato `readme.txt` nella radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="02381-176">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="02381-177">Visual Studio visualizza i contenuti del file come testo normale subito dopo avere installato direttamente il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="02381-177">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="02381-178">I file leggimi non vengono visualizzati per i pacchetti installati come dipendenze.</span><span class="sxs-lookup"><span data-stu-id="02381-178">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="02381-179">Ecco ad esempio come viene visualizzato il file leggimi per il pacchetto HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="02381-179">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Visualizzazione di un file leggimi per un pacchetto NuGet durante l'installazione](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="02381-181">La semplice aggiunta del file readme.txt nella radice del progetto non consente di includerlo nel pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="02381-181">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="02381-182">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="02381-182">Related topics</span></span>

- [<span data-ttu-id="02381-183">Creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="02381-183">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="02381-184">Pubblicare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="02381-184">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="02381-185">Pacchetti in versione non definitiva</span><span class="sxs-lookup"><span data-stu-id="02381-185">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="02381-186">Supportare più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="02381-186">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="02381-187">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="02381-187">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="02381-188">Creazione di pacchetti localizzati</span><span class="sxs-lookup"><span data-stu-id="02381-188">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="02381-189">Documentazione della libreria .NET Standard</span><span class="sxs-lookup"><span data-stu-id="02381-189">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="02381-190">Portabilità in .NET Core da .NET Framework</span><span class="sxs-lookup"><span data-stu-id="02381-190">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
