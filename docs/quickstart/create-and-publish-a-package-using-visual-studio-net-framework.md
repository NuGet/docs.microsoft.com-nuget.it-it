---
title: Creare e pubblicare un pacchetto .NET Framework con Visual Studio in Windows
description: Esercitazione sulla creazione e pubblicazione di un pacchetto NuGet .NET Framework con Visual Studio 2017 in Windows.
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: 68593211da1a34649c7050753a5db0f3a03cb41b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549628"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a><span data-ttu-id="4d609-103">Guida introduttiva: Creare e pubblicare un pacchetto con Visual Studio (.NET Framework, Windows)</span><span class="sxs-lookup"><span data-stu-id="4d609-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework, Windows)</span></span>

<span data-ttu-id="4d609-104">La creazione di un pacchetto NuGet da una libreria di classi .NET Framework prevede la creazione della DLL in Visual Studio in Windows, quindi l'uso dello strumento da riga di comando nuget.exe per creare e pubblicare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4d609-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio on Windows, then using the nuget.exe command line tool to create and publish the package.</span></span>

> [!Note]
> <span data-ttu-id="4d609-105">Questa guida introduttiva si applica solo a Visual Studio 2017 per Windows.</span><span class="sxs-lookup"><span data-stu-id="4d609-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="4d609-106">Visual Studio per Mac non include le funzionalità descritte di seguito.</span><span class="sxs-lookup"><span data-stu-id="4d609-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="4d609-107">Usare invece gli [strumenti dell'interfaccia della riga di comando dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4d609-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d609-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4d609-108">Prerequisites</span></span>

1. <span data-ttu-id="4d609-109">Installare qualsiasi edizione di Visual Studio 2017 da [visualstudio.com](https://www.visualstudio.com/) con qualsiasi carico di lavoro correlato a .NET.</span><span class="sxs-lookup"><span data-stu-id="4d609-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="4d609-110">Visual Studio 2017 include automaticamente le funzionalità di NuGet quando viene installato un carico di lavoro .NET.</span><span class="sxs-lookup"><span data-stu-id="4d609-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="4d609-111">Installare l'interfaccia della riga di comando `nuget.exe` scaricandola da [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), salvare il file `.exe` in una cartella appropriata e aggiungere tale cartella alla variabile di ambiente PATH.</span><span class="sxs-lookup"><span data-stu-id="4d609-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="4d609-112">[Registrarsi per ottenere un account gratuito in nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) se non è già disponibile.</span><span class="sxs-lookup"><span data-stu-id="4d609-112">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="4d609-113">Quando si crea un nuovo account, viene inviato un messaggio di posta elettronica di conferma.</span><span class="sxs-lookup"><span data-stu-id="4d609-113">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="4d609-114">È necessario confermare l'account prima di poter caricare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4d609-114">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="4d609-115">Creare un progetto di libreria di classi</span><span class="sxs-lookup"><span data-stu-id="4d609-115">Create a class library project</span></span>

<span data-ttu-id="4d609-116">È possibile usare un progetto libreria di classi .NET Framework esistente per il codice che si vuole includere in un pacchetto oppure creare un progetto semplice come segue:</span><span class="sxs-lookup"><span data-stu-id="4d609-116">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="4d609-117">In Visual Studio scegliere **File > Nuovo > Progetto**, selezionare il nodo **Visual C#**, selezionare il modello "Libreria di classi (.NET Framework)", assegnare al progetto il nome AppLogger e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d609-117">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="4d609-118">Fare clic con il pulsante destro del mouse sul file di progetto risultante e scegliere **Compila** per verificare che il progetto sia stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="4d609-118">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="4d609-119">La DLL è presente nella cartella Debug (o Release se si crea invece tale configurazione).</span><span class="sxs-lookup"><span data-stu-id="4d609-119">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="4d609-120">In un vero pacchetto NuGet si implementano ovviamente molte funzionalità utili, che altri possono sfruttare per compilare nuove applicazioni.</span><span class="sxs-lookup"><span data-stu-id="4d609-120">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="4d609-121">È anche possibile impostare i framework di destinazione desiderati.</span><span class="sxs-lookup"><span data-stu-id="4d609-121">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="4d609-122">Ad esempio, vedere le guide per [UWP](../guides/create-uwp-packages.md) e [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="4d609-122">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="4d609-123">In questa procedura dettagliata tuttavia non si scriverà codice aggiuntivo perché una libreria di classi dal modello è sufficiente per creare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4d609-123">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="4d609-124">Tuttavia, se si desidera del codice funzionale per il pacchetto, usare le opzioni riportate di seguito:</span><span class="sxs-lookup"><span data-stu-id="4d609-124">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
using System;

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
> <span data-ttu-id="4d609-125">A meno che non esista un motivo valido per decidere diversamente, .NET Standard è la destinazione preferita per i pacchetti NuGet, perché garantisce la compatibilità con la gamma più ampia di progetti consumer.</span><span class="sxs-lookup"><span data-stu-id="4d609-125">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="4d609-126">Vedere [Creare e pubblicare un pacchetto con Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="4d609-126">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="4d609-127">Configurare le proprietà del progetto per il pacchetto</span><span class="sxs-lookup"><span data-stu-id="4d609-127">Configure project properties for the package</span></span>

<span data-ttu-id="4d609-128">Un pacchetto NuGet contiene un manifesto (file `.nuspec`), che contiene i metadati pertinenti, ad esempio l'identificatore del pacchetto, il numero di versione, la descrizione e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="4d609-128">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="4d609-129">Alcuni di questi metadati possono essere recuperati direttamente dalle proprietà del progetto, evitando così di doverli aggiornare separatamente sia nel progetto che nel manifesto.</span><span class="sxs-lookup"><span data-stu-id="4d609-129">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="4d609-130">Questa sezione descrive come impostare le proprietà pertinenti.</span><span class="sxs-lookup"><span data-stu-id="4d609-130">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="4d609-131">Selezionare il comando di menu **Progetto > Proprietà** e quindi selezionare la scheda **Applicazione**.</span><span class="sxs-lookup"><span data-stu-id="4d609-131">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="4d609-132">Nel campo **Nome assembly** assegnare un identificatore univoco al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4d609-132">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="4d609-133">È necessario assegnare al pacchetto un identificatore univoco in nuget.org o per qualsiasi host in uso.</span><span class="sxs-lookup"><span data-stu-id="4d609-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="4d609-134">Per questa procedura dettagliata, si consiglia di includere "Sample" o "Test" nel nome, perché il passaggio di pubblicazione descritto più avanti rende il pacchetto visibile pubblicamente (nonostante sia improbabile che chiunque lo usi effettivamente).</span><span class="sxs-lookup"><span data-stu-id="4d609-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="4d609-135">Se si tenta di pubblicare un pacchetto con un nome già esistente, viene visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="4d609-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="4d609-136">Selezionare il pulsante **Informazioni assembly** che visualizza una finestra di dialogo in cui è possibile immettere altre proprietà che provengono dal manifesto (vedere [Informazioni di riferimento sul file .nuspec - Token di sostituzione](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="4d609-136">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="4d609-137">I campi più comunemente usati sono **Titolo**, **Descrizione**, **Azienda**, **Copyright** e **Versione assembly**.</span><span class="sxs-lookup"><span data-stu-id="4d609-137">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="4d609-138">Queste proprietà vengono infine visualizzate con il pacchetto in un host come nuget.org, pertanto assicurarsi che siano sufficientemente descrittive.</span><span class="sxs-lookup"><span data-stu-id="4d609-138">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Informazioni sull'assembly in un progetto .NET Framework in Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="4d609-140">Facoltativo: per visualizzare e modificare direttamente le proprietà, aprire il file `Properties/AssemblyInfo.cs` nel progetto.</span><span class="sxs-lookup"><span data-stu-id="4d609-140">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="4d609-141">Quando vengono impostate le proprietà, impostare la configurazione del progetto su **Versione** e ricompilare il progetto per generare le DLL aggiornate.</span><span class="sxs-lookup"><span data-stu-id="4d609-141">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="4d609-142">Generare il manifesto iniziale</span><span class="sxs-lookup"><span data-stu-id="4d609-142">Generate the initial manifest</span></span>

<span data-ttu-id="4d609-143">Ora che è disponibile una DLL e le proprietà del progetto sono impostate, è possibile usare il comando `nuget spec` per generare un file iniziale `.nuspec` dal progetto.</span><span class="sxs-lookup"><span data-stu-id="4d609-143">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="4d609-144">Questo passaggio include i token di sostituzione rilevanti per recuperare le informazioni dal file di progetto.</span><span class="sxs-lookup"><span data-stu-id="4d609-144">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="4d609-145">Eseguire `nuget spec` una sola volta per generare il manifesto iniziale.</span><span class="sxs-lookup"><span data-stu-id="4d609-145">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="4d609-146">Quando si aggiorna il pacchetto, è possibile cambiare i valori nel progetto o modificare direttamente il manifesto.</span><span class="sxs-lookup"><span data-stu-id="4d609-146">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="4d609-147">Aprire un prompt dei comandi e passare alla cartella del progetto contenente il file `AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="4d609-147">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="4d609-148">Eseguire il comando seguente: `nuget spec AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="4d609-148">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="4d609-149">Specificando un progetto, NuGet crea un manifesto che corrisponde al nome del progetto, in questo caso `AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="4d609-149">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="4d609-150">Vengono anche inclusi i token di sostituzione nel manifesto.</span><span class="sxs-lookup"><span data-stu-id="4d609-150">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="4d609-151">Aprire `AppLogger.nuspec` in un editor di testo per esaminarne il contenuto, che dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4d609-151">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a><span data-ttu-id="4d609-152">Modificare il manifesto</span><span class="sxs-lookup"><span data-stu-id="4d609-152">Edit the manifest</span></span>

1. <span data-ttu-id="4d609-153">NuGet genera un errore se si prova a creare un pacchetto con i valori predefiniti nel file `.nuspec`, quindi è necessario modificare i campi seguenti prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="4d609-153">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="4d609-154">Per la descrizione dell'uso di questi campi, vedere [Informazioni di riferimento sul file .nuspec - Elementi dei metadati facoltativi](../reference/nuspec.md#optional-metadata-elements).</span><span class="sxs-lookup"><span data-stu-id="4d609-154">See [.nuspec file reference - optional metadata elements](../reference/nuspec.md#optional-metadata-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="4d609-155">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="4d609-155">licenseUrl</span></span>
    - <span data-ttu-id="4d609-156">projectUrl</span><span class="sxs-lookup"><span data-stu-id="4d609-156">projectUrl</span></span>
    - <span data-ttu-id="4d609-157">iconUrl</span><span class="sxs-lookup"><span data-stu-id="4d609-157">iconUrl</span></span>
    - <span data-ttu-id="4d609-158">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="4d609-158">releaseNotes</span></span>
    - <span data-ttu-id="4d609-159">tag</span><span class="sxs-lookup"><span data-stu-id="4d609-159">tags</span></span>

1. <span data-ttu-id="4d609-160">Per i pacchetti compilati per uso pubblico, prestare particolare attenzione alla proprietà **Tags**, perché i tag consentono ad altri utenti di trovare il pacchetto in origini come nuget.org e di comprenderne le funzioni.</span><span class="sxs-lookup"><span data-stu-id="4d609-160">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="4d609-161">È anche possibile aggiungere altri elementi al manifesto in questo momento, come descritto in [Informazioni di riferimento sul file .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="4d609-161">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="4d609-162">Salvare il file prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="4d609-162">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="4d609-163">Eseguire il comando pack</span><span class="sxs-lookup"><span data-stu-id="4d609-163">Run the pack command</span></span>

1. <span data-ttu-id="4d609-164">Da un prompt dei comandi nella cartella contenente il file `.nuspec`, eseguire il comando `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="4d609-164">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="4d609-165">NuGet genera un file `.nupkg` nel formato *identificatore-versione.nupkg* nella cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="4d609-165">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="4d609-166">Pubblicare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="4d609-166">Publish the package</span></span>

<span data-ttu-id="4d609-167">Dopo aver creato un file `.nupkg`, pubblicarlo in nuget.org usando `nuget.exe` insieme a una chiave API acquisita da nuget.org. Per nuget.org è necessario usare `nuget.exe` 4.1.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="4d609-167">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="4d609-168">Acquisire la chiave API</span><span class="sxs-lookup"><span data-stu-id="4d609-168">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="4d609-169">Pubblicare con nuget push</span><span class="sxs-lookup"><span data-stu-id="4d609-169">Publish with nuget push</span></span>

1. <span data-ttu-id="4d609-170">Passare alla cartella contenente il file `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="4d609-170">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="4d609-171">Eseguire il comando seguente, specificando il nome del pacchetto e sostituendo il valore di chiave con la chiave API:</span><span class="sxs-lookup"><span data-stu-id="4d609-171">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="4d609-172">nuget.exe visualizza i risultati del processo di pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="4d609-172">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="4d609-173">Vedere [nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="4d609-173">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="4d609-174">Errori di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="4d609-174">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="4d609-175">Gestire il pacchetto pubblicato</span><span class="sxs-lookup"><span data-stu-id="4d609-175">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="4d609-176">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="4d609-176">Related topics</span></span>

- [<span data-ttu-id="4d609-177">Creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="4d609-177">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="4d609-178">Pubblicare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="4d609-178">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="4d609-179">Pacchetti in versione non definitiva</span><span class="sxs-lookup"><span data-stu-id="4d609-179">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="4d609-180">Supportare più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="4d609-180">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="4d609-181">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="4d609-181">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="4d609-182">Creazione di pacchetti localizzati</span><span class="sxs-lookup"><span data-stu-id="4d609-182">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
