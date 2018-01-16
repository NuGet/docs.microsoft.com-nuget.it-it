---
title: Guida introduttiva alla creazione e alla pubblicazione di un pacchetto NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/3/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 91781ed6-da5c-49f0-b973-16dd8ad84229
description: Esercitazione dettagliata sulla creazione e sulla pubblicazione di un pacchetto NuGet sia con l'interfaccia della riga di comando nuget.exe che con Visual Studio.
keywords: creazione di un pacchetto NuGet, pubblicazione di un pacchetto NuGet, esercitazione su NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ab5235537d869047075b93f9d8255ae9e61dfedd
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/10/2018
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="4e46f-104">Creare e pubblicare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="4e46f-104">Create and publish a package</span></span>

<span data-ttu-id="4e46f-105">La creazione di un pacchetto NuGet da una libreria di classi .NET e la pubblicazione in nuget.org sono un processo semplice, che viene illustrato nei passaggi seguenti usando l'interfaccia della riga di comando di NuGet e Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="4e46f-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org. The following steps walk you through the process using the NuGet command-line interface (CLI) and Visual Studio:</span></span>

- [<span data-ttu-id="4e46f-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4e46f-106">Pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="4e46f-107">Creare il file manifesto del pacchetto con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="4e46f-107">Create the .nuspec package manifest file</span></span>](#create-the-nuspec-package-manifest-file)
- [<span data-ttu-id="4e46f-108">Eseguire il comando pack</span><span class="sxs-lookup"><span data-stu-id="4e46f-108">Run the pack command</span></span>](#run-the-pack-command)
- [<span data-ttu-id="4e46f-109">Pubblicare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="4e46f-109">Publish the package</span></span>](#publish-the-package)

## <a name="pre-requisites"></a><span data-ttu-id="4e46f-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4e46f-110">Pre-requisites</span></span>

1. <span data-ttu-id="4e46f-111">Installare un'edizione di Visual Studio 2017 da [visualstudio.com](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="4e46f-111">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/).</span></span>

1. <span data-ttu-id="4e46f-112">Installare lo strumento dell'interfaccia della riga di comando di NuGet, `nuget.exe`, scaricando la versione più recente di `nuget.exe` da [nuget.org/downloads](https://nuget.org/downloads) e salvare il file `.exe` in una posizione nella variabile PATH.</span><span class="sxs-lookup"><span data-stu-id="4e46f-112">Install the NuGet CLI tool, `nuget.exe`, by downloading the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), and saving the `.exe` to a location in your PATH.</span></span> <span data-ttu-id="4e46f-113">Tenere presente che il download *è* solo lo strumento e non un programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="4e46f-113">Note that the download *is* the tool itself, not an installer.</span></span>

1. <span data-ttu-id="4e46f-114">Creare un progetto libreria di classi .NET appropriato per il codice per cui si vuole creare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4e46f-114">Create a suitable .NET Class Library project for the code you want to package.</span></span> <span data-ttu-id="4e46f-115">Se non si ha già un progetto, è possibile crearne uno semplice come segue:</span><span class="sxs-lookup"><span data-stu-id="4e46f-115">If you don't already have a project, you can create a simple one as follows:</span></span>
    1. <span data-ttu-id="4e46f-116">In Visual Studio scegliere **File > Nuovo > Progetto**, espandere il nodo **Visual C# > Windows**, selezionare il modello "Libreria di classi", assegnare al progetto il nome AppLogger e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e46f-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > Windows** node, select the "Class Library" template, name the project AppLogger, and click **OK**.</span></span>
    1. <span data-ttu-id="4e46f-117">Fare clic con il pulsante destro del mouse sul file di progetto risultante e scegliere **Compila** per verificare che il progetto sia stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="4e46f-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="4e46f-118">La DLL è presente nella cartella Debug (o Release se si crea invece tale configurazione).</span><span class="sxs-lookup"><span data-stu-id="4e46f-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

    <span data-ttu-id="4e46f-119">In un vero pacchetto NuGet si implementeranno ovviamente diverse utili funzionalità in base alle quali gli altri utenti potranno compilare le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="4e46f-119">Within a real NuGet package, of course, you'll implement many useful features upon which others can build applications.</span></span> <span data-ttu-id="4e46f-120">In questa procedura dettagliata tuttavia non si scriverà codice aggiuntivo perché una libreria di classi dal modello è sufficiente per creare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4e46f-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span>

## <a name="create-the-nuspec-package-manifest-file"></a><span data-ttu-id="4e46f-121">Creare il file manifesto del pacchetto con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="4e46f-121">Create the .nuspec package manifest file</span></span>

<span data-ttu-id="4e46f-122">Per ogni pacchetto NuGet è necessario un manifesto, ovvero un file `.nuspec`, che ne descriva i contenuti e le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="4e46f-122">Every NuGet package needs a manifest&mdash;a `.nuspec` file&mdash;to describe its contents and its dependencies.</span></span> <span data-ttu-id="4e46f-123">Il comando `nuget spec` crea automaticamente questo file che viene quindi personalizzato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="4e46f-123">The `nuget spec` command creates this file for you, which you then customize.</span></span> <span data-ttu-id="4e46f-124">In questo esempio si crea il file `.nuspec` da un file di progetto. È anche possibile creare il manifesto in altro modo, come illustrato in [Creare un pacchetto](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="4e46f-124">In this example you create the `.nuspec` from a project file; you can also create the manifest through other means as described on [Create a Package](../create-packages/creating-a-package.md).</span></span>

1. <span data-ttu-id="4e46f-125">Aprire un prompt dei comandi e passare alla cartella contenente il file di progetto (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="4e46f-125">Open a command prompt and navigate to the folder containing your project file (`.csproj`).</span></span>

1. <span data-ttu-id="4e46f-126">Eseguire il comando `spec` dell'interfaccia della riga di comando di NuGet per generare il manifesto, il cui nome si basa su quello del progetto, ad esempio `AppLogger.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="4e46f-126">Run the NuGet CLI `spec` command to generate the manifest, which is named after your project, such as `AppLogger.nuspec`:</span></span>

    ```
    nuget spec
    ```

1. <span data-ttu-id="4e46f-127">Aprire il file in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="4e46f-127">Open the file in a text editor.</span></span> <span data-ttu-id="4e46f-128">Il manifesto è simile al codice sotto, dove i token nel formato `<token>` (ad esempio, `$id$`) devono essere sostituiti durante il processo di creazione del pacchetto con i valori del file Properties/AssemblyInfo.cs del progetto.</span><span class="sxs-lookup"><span data-stu-id="4e46f-128">The manifest looks something like the code below, where tokens in the form `<token>` (such as `$id$`) are be replaced during the packaging process with values from the project's Properties/AssemblyInfo.cs file.</span></span> <span data-ttu-id="4e46f-129">Per altre informazioni dettagliate sui token, vedere [Creazione di un file con estensione nuspec](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="4e46f-129">For more details on tokens, see [Creating a .nuspec file](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
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
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="4e46f-130">Selezionare un ID pacchetto univoco in nuget.org. È consigliabile usare le convenzione di denominazione descritte in [Creazione di un pacchetto](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="4e46f-130">Select a package ID that is unique across nuget.org. We recommend using the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="4e46f-131">Assicurarsi di aggiornare i tag author e description per evitare che si verifichi un errore nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="4e46f-131">Be sure to update the author and description tags or you get an error in the next step.</span></span> <span data-ttu-id="4e46f-132">Ecco un file `.nuspec` aggiornato come esempio:</span><span class="sxs-lookup"><span data-stu-id="4e46f-132">Here's an updated `.nuspec` file as an example:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="4e46f-133">Per i pacchetti compilati per uso pubblico, prestare particolare attenzione all'elemento `<tags>`, perché questi tag consentono ad altri utenti di trovare il pacchetto e di conoscerne le funzioni.</span><span class="sxs-lookup"><span data-stu-id="4e46f-133">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="4e46f-134">Eseguire il comando pack</span><span class="sxs-lookup"><span data-stu-id="4e46f-134">Run the pack command</span></span>

<span data-ttu-id="4e46f-135">Per compilare un pacchetto NuGet (un file `.nupkg`) da un progetto, eseguire il comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="4e46f-135">To build a NuGet package (a `.nupkg` file) from a project, run the `pack` command:</span></span>

```
nuget pack AppLogger.csproj
```

<span data-ttu-id="4e46f-136">Questo comando crea `AppLogger.1.0.0.0.nupkg` usando il nome del pacchetto e il numero di versione del file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="4e46f-136">This command creates `AppLogger.1.0.0.0.nupkg` using the package name and version number from the `.nuspec` file.</span></span> <span data-ttu-id="4e46f-137">Questo comando genera avvisi se i valori predefiniti dei diversi campi del file `.nuspec` non sono stati aggiornati.</span><span class="sxs-lookup"><span data-stu-id="4e46f-137">The command issues warnings if you haven't updated various fields in the `.nuspec` file from their default values.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="4e46f-138">Pubblicare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="4e46f-138">Publish the package</span></span>

<span data-ttu-id="4e46f-139">Dopo avere creato un file `.nupkg`, lo si pubblica in nuget.org usando il comando `push`.</span><span class="sxs-lookup"><span data-stu-id="4e46f-139">Once you have a `.nupkg` file, you publish it to nuget.org using the `push` command.</span></span> <span data-ttu-id="4e46f-140">In alternativa, è possibile usare il [flusso di lavoro di pubblicazione di nuget.org](../create-packages/publish-a-package.md#publish-to-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="4e46f-140">(Alternately, you can use the [nuget.org publishing workflow](../create-packages/publish-a-package.md#publish-to-nugetorg).</span></span>

> [!Warning]
> <span data-ttu-id="4e46f-141">I pacchetti pubblicati in nuget.org sono visibili pubblicamente dagli altri sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="4e46f-141">The packages you publish to nuget.org are publicly visible to other developers.</span></span> <span data-ttu-id="4e46f-142">Per ospitare i pacchetti privatamente, vedere [Hosting dei pacchetti](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="4e46f-142">To host packages privately, see [Hosting packages](../hosting-packages/overview.md).</span></span>

1. <span data-ttu-id="4e46f-143">Creare un account gratuito in [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) o eseguire l'accesso se ne è già disponibile uno.</span><span class="sxs-lookup"><span data-stu-id="4e46f-143">Create a free account on [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), or log in if you already have one.</span></span> <span data-ttu-id="4e46f-144">Quando si crea un nuovo account, viene inviato un messaggio di posta elettronica di conferma.</span><span class="sxs-lookup"><span data-stu-id="4e46f-144">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="4e46f-145">È necessario confermare l'account prima di poter caricare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4e46f-145">You must confirm the account before you can upload a package.</span></span>

1. <span data-ttu-id="4e46f-146">Dopo avere eseguito l'accesso, selezionare il nome utente (in alto a destra), quindi selezionare **Chiavi API**.</span><span class="sxs-lookup"><span data-stu-id="4e46f-146">Once logged in, select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="4e46f-147">Selezionare **Crea**, specificare un nome per la chiave, selezionare **Seleziona ambiti > Push**. In **Chiave API** immettere \* in **Criterio GLOB**, quindi selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4e46f-147">Select **Create**, provide a name for your key, select **Select Scopes > Push**Under **API Key**, enter \* for **Glob pattern**, then select **Create**.</span></span>

1. <span data-ttu-id="4e46f-148">Dopo avere creato la chiave, selezionare **Copia** per recuperare la chiave di accesso che sarà necessaria nell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="4e46f-148">Once the key is created, select **Copy** to retrieve the access key you'll need in the CLI:</span></span>

    ![Copia della chiave API negli Appunti](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > <span data-ttu-id="4e46f-150">Salvare la chiave in una posizione sicura e mantenerla segreta.</span><span class="sxs-lookup"><span data-stu-id="4e46f-150">Save your key in a secure location and keep is a secret.</span></span> <span data-ttu-id="4e46f-151">Se la chiave viene accidentalmente rivelata, è sempre possibile generarla di nuovo in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="4e46f-151">If your key is accidentally revealed, you can always regenerate it at any time.</span></span> <span data-ttu-id="4e46f-152">È anche possibile rimuovere la chiave API se non si vuole più eseguire il push tramite l'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="4e46f-152">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

1. <span data-ttu-id="4e46f-153">Al prompt dei comandi eseguire il comando seguente, specificando il nome del pacchetto e sostituendo la chiave con il valore copiato nel passaggio 4:</span><span class="sxs-lookup"><span data-stu-id="4e46f-153">At a command prompt, run the following command, specifying your package name and replacing the key with the value copied in step 4:</span></span>

    ```
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="4e46f-154">nuget.exe visualizza i risultati del processo di pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="4e46f-154">nuget.exe displays the results of the publishing process:</span></span>

    ```
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. <span data-ttu-id="4e46f-155">Dal profilo in nuget.org selezionare **Manage Packages** (Gestisci pacchetti) per visualizzare quello appena pubblicato.</span><span class="sxs-lookup"><span data-stu-id="4e46f-155">From your profile on nuget.org, Select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="4e46f-156">Viene anche inviato un messaggio di posta elettronica di conferma.</span><span class="sxs-lookup"><span data-stu-id="4e46f-156">You also receive a confirmation email.</span></span> <span data-ttu-id="4e46f-157">Si noti che l'indicizzazione e la visualizzazione del pacchetto nei risultati della ricerca, dove gli altri utenti possono trovarlo, potrebbero richiedere qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="4e46f-157">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="4e46f-158">In questo intervallo di tempo la pagina del pacchetto visualizza un messaggio simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4e46f-158">During that time your package page shows the message below:</span></span>

    ![Il pacchetto non è stato ancora indicizzato.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> <span data-ttu-id="4e46f-161">**Ricerca dei virus**: tutti i pacchetti caricati in nuget.org vengono analizzati alla ricerca di virus e rifiutati se vengono trovati virus.</span><span class="sxs-lookup"><span data-stu-id="4e46f-161">**Virus scanning**: All packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="4e46f-162">Tutti i pacchetti elencati in nuget.org vengono anche analizzati periodicamente.</span><span class="sxs-lookup"><span data-stu-id="4e46f-162">All packages listed on nuget.org are also scanned periodically.</span></span>

<span data-ttu-id="4e46f-163">L'operazione è ora completata.</span><span class="sxs-lookup"><span data-stu-id="4e46f-163">And that's it!</span></span> <span data-ttu-id="4e46f-164">È stato pubblicato in [nuget.org](https://www.nuget.org/) il primo pacchetto NuGet, che gli altri sviluppatori possono usare nei propri progetti.</span><span class="sxs-lookup"><span data-stu-id="4e46f-164">You've just published your first NuGet package to [nuget.org](https://www.nuget.org/), that other developers can use in their own projects.</span></span>

## <a name="related-topics"></a><span data-ttu-id="4e46f-165">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="4e46f-165">Related topics</span></span>

- [<span data-ttu-id="4e46f-166">Creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="4e46f-166">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="4e46f-167">Pubblicare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="4e46f-167">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="4e46f-168">Supportare più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="4e46f-168">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="4e46f-169">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="4e46f-169">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="4e46f-170">Creazione di pacchetti localizzati</span><span class="sxs-lookup"><span data-stu-id="4e46f-170">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
