---
title: Guida introduttiva alla creazione e alla pubblicazione di un pacchetto NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/03/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: Esercitazione dettagliata sulla creazione e sulla pubblicazione di un pacchetto NuGet sia con l'interfaccia della riga di comando nuget.exe che con Visual Studio.
keywords: creazione di un pacchetto NuGet, pubblicazione di un pacchetto NuGet, esercitazione su NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53d29283c9e786fc27e9a608d7d251d8d0b5b0b2
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2018
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="e1d35-104">Creare e pubblicare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="e1d35-104">Create and publish a package</span></span>

<span data-ttu-id="e1d35-105">La creazione di un pacchetto NuGet da una libreria di classi .NET e la pubblicazione in nuget.org sono un processo semplice, che viene illustrato in questo articolo usando l'interfaccia della riga di comando di NuGet e Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e1d35-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org. This article walks you through the process using the NuGet command-line interface (CLI) and Visual Studio.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="e1d35-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e1d35-106">Pre-requisites</span></span>

1. <span data-ttu-id="e1d35-107">Installare un'edizione di Visual Studio 2017 da [visualstudio.com](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="e1d35-107">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/).</span></span>

1. <span data-ttu-id="e1d35-108">Installare lo strumento dell'interfaccia della riga di comando di NuGet, `nuget.exe`, scaricando la versione più recente di `nuget.exe` da [nuget.org/downloads](https://nuget.org/downloads) e salvare il file `.exe` in una posizione nella variabile PATH.</span><span class="sxs-lookup"><span data-stu-id="e1d35-108">Install the NuGet CLI tool, `nuget.exe`, by downloading the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), and saving the `.exe` to a location in your PATH.</span></span> <span data-ttu-id="e1d35-109">Tenere presente che il download *è* solo lo strumento e non un programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="e1d35-109">Note that the download *is* the tool itself, not an installer.</span></span>

1. <span data-ttu-id="e1d35-110">Creare un progetto libreria di classi .NET appropriato per il codice per cui si vuole creare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e1d35-110">Create a suitable .NET Class Library project for the code you want to package.</span></span> <span data-ttu-id="e1d35-111">Se non si ha già un progetto, è possibile crearne uno semplice come segue:</span><span class="sxs-lookup"><span data-stu-id="e1d35-111">If you don't already have a project, you can create a simple one as follows:</span></span>
    1. <span data-ttu-id="e1d35-112">In Visual Studio scegliere **File > Nuovo > Progetto**, espandere il nodo **Visual C# > Windows**, selezionare il modello "Libreria di classi", assegnare al progetto il nome AppLogger e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1d35-112">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > Windows** node, select the "Class Library" template, name the project AppLogger, and click **OK**.</span></span>
    1. <span data-ttu-id="e1d35-113">Fare clic con il pulsante destro del mouse sul file di progetto risultante e scegliere **Compila** per verificare che il progetto sia stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="e1d35-113">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="e1d35-114">La DLL è presente nella cartella Debug (o Release se si crea invece tale configurazione).</span><span class="sxs-lookup"><span data-stu-id="e1d35-114">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

    <span data-ttu-id="e1d35-115">In un vero pacchetto NuGet si implementeranno ovviamente diverse utili funzionalità in base alle quali gli altri utenti potranno compilare le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e1d35-115">Within a real NuGet package, of course, you'll implement many useful features upon which others can build applications.</span></span> <span data-ttu-id="e1d35-116">In questa procedura dettagliata tuttavia non si scriverà codice aggiuntivo perché una libreria di classi dal modello è sufficiente per creare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e1d35-116">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span>

## <a name="create-the-nuspec-package-manifest-file"></a><span data-ttu-id="e1d35-117">Creare il file manifesto del pacchetto con estensione nuspec</span><span class="sxs-lookup"><span data-stu-id="e1d35-117">Create the .nuspec package manifest file</span></span>

<span data-ttu-id="e1d35-118">Per ogni pacchetto NuGet è necessario un manifesto, ovvero un file `.nuspec`, che ne descriva i contenuti e le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="e1d35-118">Every NuGet package needs a manifest&mdash;a `.nuspec` file&mdash;to describe its contents and its dependencies.</span></span> <span data-ttu-id="e1d35-119">Il comando `nuget spec` crea automaticamente questo file che viene quindi personalizzato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="e1d35-119">The `nuget spec` command creates this file for you, which you then customize.</span></span> <span data-ttu-id="e1d35-120">In questo esempio si crea il file `.nuspec` da un file di progetto. È anche possibile creare il manifesto in altro modo, come illustrato in [Creare un pacchetto](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="e1d35-120">In this example you create the `.nuspec` from a project file; you can also create the manifest through other means as described on [Create a Package](../create-packages/creating-a-package.md).</span></span>

1. <span data-ttu-id="e1d35-121">Aprire un prompt dei comandi e passare alla cartella contenente il file di progetto (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="e1d35-121">Open a command prompt and navigate to the folder containing your project file (`.csproj`).</span></span>

1. <span data-ttu-id="e1d35-122">Eseguire il comando `spec` dell'interfaccia della riga di comando di NuGet per generare il manifesto, il cui nome si basa su quello del progetto, ad esempio `AppLogger.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="e1d35-122">Run the NuGet CLI `spec` command to generate the manifest, which is named after your project, such as `AppLogger.nuspec`:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="e1d35-123">Aprire il file in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="e1d35-123">Open the file in a text editor.</span></span> <span data-ttu-id="e1d35-124">Il manifesto è simile al codice sotto, dove i token nel formato `<token>` (ad esempio, `$id$`) devono essere sostituiti durante il processo di creazione del pacchetto con i valori del file Properties/AssemblyInfo.cs del progetto.</span><span class="sxs-lookup"><span data-stu-id="e1d35-124">The manifest looks something like the code below, where tokens in the form `<token>` (such as `$id$`) are be replaced during the packaging process with values from the project's Properties/AssemblyInfo.cs file.</span></span> <span data-ttu-id="e1d35-125">Per altre informazioni dettagliate sui token, vedere [Creazione di un file con estensione nuspec](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="e1d35-125">For more details on tokens, see [Creating a .nuspec file](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span></span>

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

1. <span data-ttu-id="e1d35-126">Selezionare un ID pacchetto univoco in nuget.org. È consigliabile usare le convenzione di denominazione descritte in [Creazione di un pacchetto](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="e1d35-126">Select a package ID that is unique across nuget.org. We recommend using the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="e1d35-127">Assicurarsi di aggiornare i tag author e description per evitare che si verifichi un errore nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="e1d35-127">Be sure to update the author and description tags or you get an error in the next step.</span></span> <span data-ttu-id="e1d35-128">Ecco un file `.nuspec` aggiornato come esempio:</span><span class="sxs-lookup"><span data-stu-id="e1d35-128">Here's an updated `.nuspec` file as an example:</span></span>

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
> <span data-ttu-id="e1d35-129">Per i pacchetti compilati per uso pubblico, prestare particolare attenzione all'elemento `<tags>`, perché questi tag consentono ad altri utenti di trovare il pacchetto e di conoscerne le funzioni.</span><span class="sxs-lookup"><span data-stu-id="e1d35-129">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="e1d35-130">Eseguire il comando pack</span><span class="sxs-lookup"><span data-stu-id="e1d35-130">Run the pack command</span></span>

<span data-ttu-id="e1d35-131">Per compilare un pacchetto NuGet (un file `.nupkg`) da un progetto, eseguire il comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="e1d35-131">To build a NuGet package (a `.nupkg` file) from a project, run the `pack` command:</span></span>

```cli
nuget pack AppLogger.csproj
```

<span data-ttu-id="e1d35-132">Questo comando crea `AppLogger.1.0.0.0.nupkg` usando il nome del pacchetto e il numero di versione del file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="e1d35-132">This command creates `AppLogger.1.0.0.0.nupkg` using the package name and version number from the `.nuspec` file.</span></span> <span data-ttu-id="e1d35-133">Questo comando genera avvisi se i valori predefiniti dei diversi campi del file `.nuspec` non sono stati aggiornati.</span><span class="sxs-lookup"><span data-stu-id="e1d35-133">The command issues warnings if you haven't updated various fields in the `.nuspec` file from their default values.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="e1d35-134">Pubblicare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="e1d35-134">Publish the package</span></span>

<span data-ttu-id="e1d35-135">Dopo avere creato un file `.nupkg`, lo si pubblica in nuget.org usando il comando `push`.</span><span class="sxs-lookup"><span data-stu-id="e1d35-135">Once you have a `.nupkg` file, you publish it to nuget.org using the `push` command.</span></span> <span data-ttu-id="e1d35-136">In alternativa, è possibile usare il [flusso di lavoro di pubblicazione di nuget.org](../create-packages/publish-a-package.md#publish-to-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="e1d35-136">(Alternately, you can use the [nuget.org publishing workflow](../create-packages/publish-a-package.md#publish-to-nugetorg).</span></span>

> [!Warning]
> <span data-ttu-id="e1d35-137">I pacchetti pubblicati in nuget.org sono visibili pubblicamente dagli altri sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="e1d35-137">The packages you publish to nuget.org are publicly visible to other developers.</span></span> <span data-ttu-id="e1d35-138">Per ospitare i pacchetti privatamente, vedere [Hosting dei pacchetti](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="e1d35-138">To host packages privately, see [Hosting packages](../hosting-packages/overview.md).</span></span>

1. <span data-ttu-id="e1d35-139">Creare un account gratuito in [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) o eseguire l'accesso se ne è già disponibile uno.</span><span class="sxs-lookup"><span data-stu-id="e1d35-139">Create a free account on [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), or log in if you already have one.</span></span> <span data-ttu-id="e1d35-140">Quando si crea un nuovo account, viene inviato un messaggio di posta elettronica di conferma.</span><span class="sxs-lookup"><span data-stu-id="e1d35-140">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="e1d35-141">È necessario confermare l'account prima di poter caricare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e1d35-141">You must confirm the account before you can upload a package.</span></span>

1. <span data-ttu-id="e1d35-142">Dopo avere eseguito l'accesso, selezionare il nome utente (in alto a destra), quindi selezionare **Chiavi API**.</span><span class="sxs-lookup"><span data-stu-id="e1d35-142">Once logged in, select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="e1d35-143">Selezionare **Crea**, specificare un nome per la chiave, selezionare **Seleziona ambiti > Push** in **Chiave API**, immettere \* in **Criterio GLOB** e quindi selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e1d35-143">Select **Create**, provide a name for your key, select **Select Scopes > Push** under **API Key**, enter \* for **Glob pattern**, then select **Create**.</span></span>

1. <span data-ttu-id="e1d35-144">Dopo avere creato la chiave, selezionare **Copia** per recuperare la chiave di accesso che sarà necessaria nell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="e1d35-144">Once the key is created, select **Copy** to retrieve the access key you'll need in the CLI:</span></span>

    ![Copia della chiave API negli Appunti](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > <span data-ttu-id="e1d35-146">Salvare la chiave in una posizione sicura e mantenerla segreta.</span><span class="sxs-lookup"><span data-stu-id="e1d35-146">Save your key in a secure location and keep it secret.</span></span> <span data-ttu-id="e1d35-147">Se la chiave viene accidentalmente rivelata, è possibile generarla di nuovo in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="e1d35-147">If your key is accidentally revealed, you can regenerate it at any time.</span></span> <span data-ttu-id="e1d35-148">È anche possibile rimuovere la chiave API se non si vuole più eseguire il push tramite l'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="e1d35-148">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

1. <span data-ttu-id="e1d35-149">Al prompt dei comandi eseguire il comando seguente, specificando il nome del pacchetto e sostituendo la chiave con il valore copiato nel passaggio 4:</span><span class="sxs-lookup"><span data-stu-id="e1d35-149">At a command prompt, run the following command, specifying your package name and replacing the key with the value copied in step 4:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="e1d35-150">nuget.exe visualizza i risultati del processo di pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="e1d35-150">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. <span data-ttu-id="e1d35-151">Dal profilo in nuget.org selezionare **Manage Packages** (Gestisci pacchetti) per visualizzare quello appena pubblicato.</span><span class="sxs-lookup"><span data-stu-id="e1d35-151">From your profile on nuget.org, Select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="e1d35-152">Viene anche inviato un messaggio di posta elettronica di conferma.</span><span class="sxs-lookup"><span data-stu-id="e1d35-152">You also receive a confirmation email.</span></span> <span data-ttu-id="e1d35-153">Si noti che l'indicizzazione e la visualizzazione del pacchetto nei risultati della ricerca, dove gli altri utenti possono trovarlo, potrebbero richiedere qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="e1d35-153">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="e1d35-154">In questo intervallo di tempo la pagina del pacchetto visualizza un messaggio simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="e1d35-154">During that time your package page shows the message below:</span></span>

    ![Il pacchetto non è stato ancora indicizzato.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> <span data-ttu-id="e1d35-157">**Ricerca dei virus**: tutti i pacchetti caricati in nuget.org vengono analizzati alla ricerca di virus e rifiutati se vengono trovati virus.</span><span class="sxs-lookup"><span data-stu-id="e1d35-157">**Virus scanning**: All packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="e1d35-158">Tutti i pacchetti elencati in nuget.org vengono anche analizzati periodicamente.</span><span class="sxs-lookup"><span data-stu-id="e1d35-158">All packages listed on nuget.org are also scanned periodically.</span></span>

<span data-ttu-id="e1d35-159">L'operazione è ora completata.</span><span class="sxs-lookup"><span data-stu-id="e1d35-159">And that's it!</span></span> <span data-ttu-id="e1d35-160">È stato pubblicato in [nuget.org](https://www.nuget.org/) il primo pacchetto NuGet, che gli altri sviluppatori possono usare nei propri progetti.</span><span class="sxs-lookup"><span data-stu-id="e1d35-160">You've just published your first NuGet package to [nuget.org](https://www.nuget.org/), that other developers can use in their own projects.</span></span>

## <a name="related-topics"></a><span data-ttu-id="e1d35-161">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="e1d35-161">Related topics</span></span>

- [<span data-ttu-id="e1d35-162">Creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="e1d35-162">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="e1d35-163">Pubblicare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="e1d35-163">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="e1d35-164">Supportare più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="e1d35-164">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="e1d35-165">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="e1d35-165">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="e1d35-166">Creazione di pacchetti localizzati</span><span class="sxs-lookup"><span data-stu-id="e1d35-166">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
