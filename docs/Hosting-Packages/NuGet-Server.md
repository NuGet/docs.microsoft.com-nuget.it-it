---
title: Uso di NuGet.Server per ospitare feed NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 45138f80-9717-42c2-8b34-9a1bc1fb3eab
description: Come creare e ospitare un feed di pacchetti NuGet in qualsiasi server che esegue IIS usando NuGet.Server e rendendo i pacchetti disponibili tramite HTTP e OData.
keywords: Feed NuGet, raccolta NuGet, feed di pacchetti remoti, NuGet.Server
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f37b9b711a2bc8c39314214113045a6485f297a8
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="nugetserver"></a><span data-ttu-id="ffbf9-104">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="ffbf9-104">NuGet.Server</span></span>

<span data-ttu-id="ffbf9-105">NuGet.Server è un pacchetto fornito da .NET Foundation che crea un'applicazione ASP.NET in grado di ospitare un feed di pacchetti in qualsiasi server che esegue IIS.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-105">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="ffbf9-106">Per semplificare, NuGet.Server crea una cartella nel server disponibile tramite HTTP(S), nello specifico OData.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-106">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="ffbf9-107">È semplice da configurare ed è una soluzione ideale per scenari semplici.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-107">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="ffbf9-108">Creare un'applicazione Web ASP.NET vuota in Visual Studio e aggiungere il pacchetto NuGet.Server.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-108">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="ffbf9-109">Configurare la cartella `Packages` nell'applicazione e aggiungere i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-109">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="ffbf9-110">Distribuire l'applicazione in un server appropriato.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-110">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="ffbf9-111">Le sezioni seguenti descrivono questo processo in dettaglio con C#.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-111">The following sections walk through this process in detail, using C#.</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="ffbf9-112">Creare e distribuire un'applicazione Web ASP.NET con NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="ffbf9-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="ffbf9-113">In Visual Studio selezionare **File > Nuovo > Progetto**, impostare il framework di destinazione per .NET Framework 4.6 (vedere di seguito), cercare "ASP.NET" e selezionare il modello **Applicazione Web ASP.NET (.NET Framework)** per C#.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-113">In Visual Studio, select **File > New > Project**, set the target framework for .NET Framework 4.6 (see below), search for "ASP.NET", and select the **ASP.NET Web Application (.NET Framework)** template for C#.</span></span>

    ![Impostazione della destinazione su .NET Framework 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="ffbf9-115">Assegnare all'applicazione un nome appropriato *diverso* da NuGet.Server, selezionare OK e nella finestra di dialogo successiva selezionare il modello **Vuoto**, quindi selezionare OK.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template and select OK.</span></span>

1. <span data-ttu-id="ffbf9-116">Fare clic con il pulsante destro del mouse sul progetto, scegliere **Gestisci pacchetti NuGet**e nell'interfaccia utente di Gestione pacchetti cercare e installare la versione più recente del pacchetto NuGet.Server se si è scelto come destinazione .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-116">Right-click the project, select **Manage NuGet Packages**, and in the Package Manager UI search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="ffbf9-117">È anche possibile installarla dalla console di Gestione pacchetti con `Install-Package NuGet.Server`.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-117">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.)</span></span>

    ![Installazione del pacchetto NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > <span data-ttu-id="ffbf9-119">Se l'applicazione Web è destinata a .NET Framework 4.5.2, è invece necessario installare NuGet Server **2.10.3**.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-119">If your web application targets .NET Framework 4.5.2, you must install NuGet Server **2.10.3** instead.</span></span>

1. <span data-ttu-id="ffbf9-120">L'installazione di NuGet.Server converte l'applicazione Web vuota in un'origine di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="ffbf9-121">Crea una cartella `Packages` dell'applicazione e sovrascrive `web.config` per includere le impostazioni aggiuntive (vedere i commenti in tale file per altri dettagli).</span><span class="sxs-lookup"><span data-stu-id="ffbf9-121">It creates a `Packages` folder in the application and overwrites `web.config` to include additional settings (see the comments in that file for details).</span></span>

1. <span data-ttu-id="ffbf9-122">Per rendere disponibili i pacchetti nel feed quando si pubblica l'applicazione in un server, aggiungere i relativi file `.nupkg` nella cartella `Packages` in Visual Studio e quindi impostare **Azione di compilazione** su **Contenuto** e **Copia in directory di output** su **Copia sempre**:</span><span class="sxs-lookup"><span data-stu-id="ffbf9-122">To make packages available in the feed when you publish the application to a server, add their `.nupkg` files to the `Packages` folder in Visual Studio, then set their **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Copia dei pacchetti nella cartella Packages nel progetto](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="ffbf9-124">Eseguire il sito in locale in Visual Studio (senza eseguire il debug, ovvero CTRL+F5).</span><span class="sxs-lookup"><span data-stu-id="ffbf9-124">Run the site locally in Visual Studio (without debugging, that is Ctrl+F5).</span></span> <span data-ttu-id="ffbf9-125">Nella home page sono disponibili gli URL del feed dei pacchetti:</span><span class="sxs-lookup"><span data-stu-id="ffbf9-125">The home page provides the package feed URLs:</span></span>

    ![Home page predefinita per un'applicazione con NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="ffbf9-127">Fare clic su **qui** nell'area evidenziata nella figura per visualizzare il feed OData dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-127">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="ffbf9-128">La prima volta che si esegue l'applicazione, NuGet.Server ristruttura la cartella `Packages` in modo che contenga una cartella per ogni pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-128">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="ffbf9-129">Questo corrisponde al [layout di archiviazione locale](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introdotto in NuGet 3.3 per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-129">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="ffbf9-130">Quando si aggiungono altri pacchetti, continuare a seguire questa struttura.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-130">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="ffbf9-131">Dopo aver verificato la distribuzione locale, distribuire l'applicazione in qualsiasi altro sito interno o esterno, in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-131">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>
1. <span data-ttu-id="ffbf9-132">Dopo la distribuzione in `http://<domain>`, l'URL usato per l'origine dei pacchetti sarà `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-132">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="ffbf9-133">Configurazione della cartella dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="ffbf9-133">Configuring the Packages folder</span></span>

<span data-ttu-id="ffbf9-134">Con `NuGet.Server` 1.5 e versioni successive è possibile configurare la cartella dei pacchetti in modo più specifico usando il valore `appSetting/packagesPath` in `web.config`:</span><span class="sxs-lookup"><span data-stu-id="ffbf9-134">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="ffbf9-135">`packagesPath` può essere un percorso assoluto o virtuale.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-135">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="ffbf9-136">Quando `packagesPath` viene omesso o lasciato vuoto, il valore predefinito per la cartella dei pacchetti è `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-136">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="ffbf9-137">Aggiunta di pacchetti al feed esternamente</span><span class="sxs-lookup"><span data-stu-id="ffbf9-137">Adding packages to the feed externally</span></span>

<span data-ttu-id="ffbf9-138">Quando un sito NuGet.Server è in esecuzione, è possibile aggiungere o eliminare i pacchetti tramite nuget.exe a condizione di impostare un valore di chiave API in `web.config`.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-138">Once a NuGet.Server site is running, you can add or delete packages using nuget.exe provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="ffbf9-139">Dopo l'installazione del pacchetto NuGet.Server, `web.config` contiene un valore vuoto `appSetting/apiKey`:</span><span class="sxs-lookup"><span data-stu-id="ffbf9-139">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="ffbf9-140">Quando `apiKey` viene omesso o è vuoto, il push dei pacchetti nel feed è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-140">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="ffbf9-141">Per abilitare questa funzionalità, impostare `apiKey` su un valore (idealmente una password complessa) e aggiungere una chiave denominata `appSettings/requireApiKey` con il valore `true`:</span><span class="sxs-lookup"><span data-stu-id="ffbf9-141">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="ffbf9-142">Se il server è già protetto o non è necessaria una chiave API per altri motivi, ad esempio quando si usa un server privato in una rete del team locale, è possibile impostare `requireApiKey` su `false`.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-142">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="ffbf9-143">Tutti gli utenti con accesso al server possono quindi eseguire il push dei pacchetti o eliminarli.</span><span class="sxs-lookup"><span data-stu-id="ffbf9-143">All users with access to the server can then push or delete packages.</span></span>