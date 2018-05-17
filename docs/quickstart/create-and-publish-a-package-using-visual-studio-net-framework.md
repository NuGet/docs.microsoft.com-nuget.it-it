---
title: Guida introduttiva alla creazione e alla pubblicazione di un pacchetto NuGet .NET Framework con Visual Studio
description: Esercitazione sulla creazione e pubblicazione di un pacchetto NuGet .NET Framework con Visual Studio 2017.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/13/2018
ms.topic: quickstart
ms.openlocfilehash: 01760034a121b1ff6f227e006415779898c4cf6d
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2018
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework"></a><span data-ttu-id="b8a96-103">Guida introduttiva: Creare e pubblicare un pacchetto con Visual Studio (.NET Framework)</span><span class="sxs-lookup"><span data-stu-id="b8a96-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework)</span></span>

<span data-ttu-id="b8a96-104">La creazione di un pacchetto NuGet da una libreria di classi .NET Framework prevede la creazione della DLL in Visual Studio, quindi l'uso dello strumento da riga di comando nuget.exe per creare e pubblicare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b8a96-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio, then using the nuget.exe command line tool to create and publish the package.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8a96-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b8a96-105">Prerequisites</span></span>

1. <span data-ttu-id="b8a96-106">Installare qualsiasi edizione di Visual Studio 2017 da [visualstudio.com](https://www.visualstudio.com/) con qualsiasi carico di lavoro correlato a .NET.</span><span class="sxs-lookup"><span data-stu-id="b8a96-106">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="b8a96-107">Visual Studio 2017 include automaticamente le funzionalità di NuGet quando viene installato un carico di lavoro .NET.</span><span class="sxs-lookup"><span data-stu-id="b8a96-107">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="b8a96-108">Installare l'interfaccia della riga di comando `nuget.exe` scaricandola da [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), salvare il file `.exe` in una cartella appropriata e aggiungere tale cartella alla variabile di ambiente PATH.</span><span class="sxs-lookup"><span data-stu-id="b8a96-108">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="b8a96-109">[Registrarsi per ottenere un account gratuito in nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) se non è già disponibile.</span><span class="sxs-lookup"><span data-stu-id="b8a96-109">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="b8a96-110">Quando si crea un nuovo account, viene inviato un messaggio di posta elettronica di conferma.</span><span class="sxs-lookup"><span data-stu-id="b8a96-110">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="b8a96-111">È necessario confermare l'account prima di poter caricare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b8a96-111">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="b8a96-112">Creare un progetto di libreria di classi</span><span class="sxs-lookup"><span data-stu-id="b8a96-112">Create a class library project</span></span>

<span data-ttu-id="b8a96-113">È possibile usare un progetto libreria di classi .NET Framework esistente per il codice che si vuole includere in un pacchetto oppure creare un progetto semplice come segue:</span><span class="sxs-lookup"><span data-stu-id="b8a96-113">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="b8a96-114">In Visual Studio scegliere **File > Nuovo > Progetto**, selezionare il nodo **Visual C#**, selezionare il modello "Libreria di classi (.NET Framework)", assegnare al progetto il nome AppLogger e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8a96-114">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="b8a96-115">Fare clic con il pulsante destro del mouse sul file di progetto risultante e scegliere **Compila** per verificare che il progetto sia stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="b8a96-115">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="b8a96-116">La DLL è presente nella cartella Debug (o Release se si crea invece tale configurazione).</span><span class="sxs-lookup"><span data-stu-id="b8a96-116">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="b8a96-117">In un vero pacchetto NuGet si implementano ovviamente molte funzionalità utili, che altri possono sfruttare per compilare nuove applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b8a96-117">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="b8a96-118">È anche possibile impostare i framework di destinazione desiderati.</span><span class="sxs-lookup"><span data-stu-id="b8a96-118">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="b8a96-119">Ad esempio, vedere le guide per [UWP](../guides/create-uwp-packages.md) e [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="b8a96-119">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="b8a96-120">In questa procedura dettagliata tuttavia non si scriverà codice aggiuntivo perché una libreria di classi dal modello è sufficiente per creare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b8a96-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="b8a96-121">Tuttavia, se si desidera del codice funzionale per il pacchetto, usare le opzioni riportate di seguito:</span><span class="sxs-lookup"><span data-stu-id="b8a96-121">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="b8a96-122">A meno che non esista un motivo valido per decidere diversamente, .NET Standard è la destinazione preferita per i pacchetti NuGet, perché garantisce la compatibilità con la gamma più ampia di progetti consumer.</span><span class="sxs-lookup"><span data-stu-id="b8a96-122">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="b8a96-123">Vedere [Creare e pubblicare un pacchetto con Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="b8a96-123">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="b8a96-124">Configurare le proprietà del progetto per il pacchetto</span><span class="sxs-lookup"><span data-stu-id="b8a96-124">Configure project properties for the package</span></span>

<span data-ttu-id="b8a96-125">Un pacchetto NuGet contiene un manifesto (file `.nuspec`), che contiene i metadati pertinenti, ad esempio l'identificatore del pacchetto, il numero di versione, la descrizione e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="b8a96-125">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="b8a96-126">Alcuni di questi metadati possono essere recuperati direttamente dalle proprietà del progetto, evitando così di doverli aggiornare separatamente sia nel progetto che nel manifesto.</span><span class="sxs-lookup"><span data-stu-id="b8a96-126">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="b8a96-127">Questa sezione descrive come impostare le proprietà pertinenti.</span><span class="sxs-lookup"><span data-stu-id="b8a96-127">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="b8a96-128">Selezionare il comando di menu **Progetto > Proprietà** e quindi selezionare la scheda **Applicazione**.</span><span class="sxs-lookup"><span data-stu-id="b8a96-128">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="b8a96-129">Nel campo **Nome assembly** assegnare un identificatore univoco al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b8a96-129">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="b8a96-130">È necessario assegnare al pacchetto un identificatore univoco in nuget.org o per qualsiasi host in uso.</span><span class="sxs-lookup"><span data-stu-id="b8a96-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="b8a96-131">Per questa procedura dettagliata, si consiglia di includere "Sample" o "Test" nel nome, perché il passaggio di pubblicazione descritto più avanti rende il pacchetto visibile pubblicamente (nonostante sia improbabile che chiunque lo usi effettivamente).</span><span class="sxs-lookup"><span data-stu-id="b8a96-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="b8a96-132">Se si tenta di pubblicare un pacchetto con un nome già esistente, viene visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="b8a96-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="b8a96-133">Selezionare il pulsante **Informazioni assembly** che visualizza una finestra di dialogo in cui è possibile immettere altre proprietà che provengono dal manifesto (vedere [Informazioni di riferimento sul file .nuspec - Token di sostituzione](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="b8a96-133">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="b8a96-134">I campi più comunemente usati sono **Titolo**, **Descrizione**, **Azienda**, **Copyright** e **Versione assembly**.</span><span class="sxs-lookup"><span data-stu-id="b8a96-134">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="b8a96-135">Queste proprietà vengono infine visualizzate con il pacchetto in un host come nuget.org, pertanto assicurarsi che siano sufficientemente descrittive.</span><span class="sxs-lookup"><span data-stu-id="b8a96-135">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Informazioni sull'assembly in un progetto .NET Framework in Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="b8a96-137">Facoltativo: per visualizzare e modificare direttamente le proprietà, aprire il file `Properties/AssemblyInfo.cs` nel progetto.</span><span class="sxs-lookup"><span data-stu-id="b8a96-137">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="b8a96-138">Quando vengono impostate le proprietà, impostare la configurazione del progetto su **Versione** e ricompilare il progetto per generare le DLL aggiornate.</span><span class="sxs-lookup"><span data-stu-id="b8a96-138">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="b8a96-139">Generare il manifesto iniziale</span><span class="sxs-lookup"><span data-stu-id="b8a96-139">Generate the initial manifest</span></span>

<span data-ttu-id="b8a96-140">Ora che è disponibile una DLL e le proprietà del progetto sono impostate, è possibile usare il comando `nuget spec` per generare un file iniziale `.nuspec` dal progetto.</span><span class="sxs-lookup"><span data-stu-id="b8a96-140">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="b8a96-141">Questo passaggio include i token di sostituzione rilevanti per recuperare le informazioni dal file di progetto.</span><span class="sxs-lookup"><span data-stu-id="b8a96-141">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="b8a96-142">Eseguire `nuget spec` una sola volta per generare il manifesto iniziale.</span><span class="sxs-lookup"><span data-stu-id="b8a96-142">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="b8a96-143">Quando si aggiorna il pacchetto, è possibile cambiare i valori nel progetto o modificare direttamente il manifesto.</span><span class="sxs-lookup"><span data-stu-id="b8a96-143">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="b8a96-144">Aprire un prompt dei comandi e passare alla cartella del progetto contenente il file `AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="b8a96-144">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="b8a96-145">Eseguire il comando seguente: `nuget spec AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="b8a96-145">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="b8a96-146">Specificando un progetto, NuGet crea un manifesto che corrisponde al nome del progetto, in questo caso `AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="b8a96-146">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="b8a96-147">Vengono anche inclusi i token di sostituzione nel manifesto.</span><span class="sxs-lookup"><span data-stu-id="b8a96-147">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="b8a96-148">Aprire `AppLogger.nuspec` in un editor di testo per esaminarne il contenuto, che dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b8a96-148">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

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

## <a name="edit-the-manifest"></a><span data-ttu-id="b8a96-149">Modificare il manifesto</span><span class="sxs-lookup"><span data-stu-id="b8a96-149">Edit the manifest</span></span>

1. <span data-ttu-id="b8a96-150">NuGet genera un errore se si prova a creare un pacchetto con i valori predefiniti nel file `.nuspec`, quindi è necessario modificare i campi seguenti prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="b8a96-150">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="b8a96-151">Vedere [Informazioni di riferimento sul file .nuspec - Singoli elementi](../reference/nuspec.md#single-elements) per una descrizione di come vengono usati questi campi.</span><span class="sxs-lookup"><span data-stu-id="b8a96-151">See [.nuspec file reference - single elements](../reference/nuspec.md#single-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="b8a96-152">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="b8a96-152">licenseUrl</span></span>
    - <span data-ttu-id="b8a96-153">projectUrl</span><span class="sxs-lookup"><span data-stu-id="b8a96-153">projectUrl</span></span>
    - <span data-ttu-id="b8a96-154">iconUrl</span><span class="sxs-lookup"><span data-stu-id="b8a96-154">iconUrl</span></span>
    - <span data-ttu-id="b8a96-155">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="b8a96-155">releaseNotes</span></span>
    - <span data-ttu-id="b8a96-156">tag</span><span class="sxs-lookup"><span data-stu-id="b8a96-156">tags</span></span>

1. <span data-ttu-id="b8a96-157">Per i pacchetti compilati per uso pubblico, prestare particolare attenzione alla proprietà **Tags**, perché i tag consentono ad altri utenti di trovare il pacchetto in origini come nuget.org e di comprenderne le funzioni.</span><span class="sxs-lookup"><span data-stu-id="b8a96-157">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="b8a96-158">È anche possibile aggiungere altri elementi al manifesto in questo momento, come descritto in [Informazioni di riferimento sul file .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="b8a96-158">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="b8a96-159">Salvare il file prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="b8a96-159">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="b8a96-160">Eseguire il comando pack</span><span class="sxs-lookup"><span data-stu-id="b8a96-160">Run the pack command</span></span>

1. <span data-ttu-id="b8a96-161">Da un prompt dei comandi nella cartella contenente il file `.nuspec`, eseguire il comando `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="b8a96-161">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="b8a96-162">NuGet genera un file `.nupkg` nel formato *identificatore-versione.nupkg* nella cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="b8a96-162">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="b8a96-163">Pubblicare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="b8a96-163">Publish the package</span></span>

<span data-ttu-id="b8a96-164">Dopo aver creato un file `.nupkg`, pubblicarlo in nuget.org usando `nuget.exe` insieme a una chiave API acquisita da nuget.org. Per nuget.org è necessario usare `nuget.exe` 4.1.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="b8a96-164">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="b8a96-165">Acquisire la chiave API</span><span class="sxs-lookup"><span data-stu-id="b8a96-165">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="b8a96-166">Pubblicare con nuget push</span><span class="sxs-lookup"><span data-stu-id="b8a96-166">Publish with nuget push</span></span>

1. <span data-ttu-id="b8a96-167">Passare alla cartella contenente il file `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="b8a96-167">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="b8a96-168">Eseguire il comando seguente, specificando il nome del pacchetto e sostituendo il valore di chiave con la chiave API:</span><span class="sxs-lookup"><span data-stu-id="b8a96-168">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="b8a96-169">nuget.exe visualizza i risultati del processo di pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="b8a96-169">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="b8a96-170">Vedere [nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="b8a96-170">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="b8a96-171">Errori di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="b8a96-171">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="b8a96-172">Gestire il pacchetto pubblicato</span><span class="sxs-lookup"><span data-stu-id="b8a96-172">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="b8a96-173">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="b8a96-173">Related topics</span></span>

- [<span data-ttu-id="b8a96-174">Creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="b8a96-174">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="b8a96-175">Pubblicare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="b8a96-175">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="b8a96-176">Pacchetti in versione non definitiva</span><span class="sxs-lookup"><span data-stu-id="b8a96-176">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="b8a96-177">Supportare più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="b8a96-177">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="b8a96-178">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="b8a96-178">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="b8a96-179">Creazione di pacchetti localizzati</span><span class="sxs-lookup"><span data-stu-id="b8a96-179">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
