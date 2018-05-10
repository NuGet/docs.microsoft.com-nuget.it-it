---
title: Uso di NuGet.Server per ospitare feed NuGet
description: Come creare e ospitare un feed di pacchetti NuGet in qualsiasi server che esegue IIS usando NuGet.Server e rendendo i pacchetti disponibili tramite HTTP e OData.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 55501eedf6c5fdf054a602536ee8c03e7048d5d5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nugetserver"></a><span data-ttu-id="19347-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="19347-103">NuGet.Server</span></span>

<span data-ttu-id="19347-104">NuGet.Server è un pacchetto fornito da .NET Foundation che crea un'applicazione ASP.NET in grado di ospitare un feed di pacchetti in qualsiasi server che esegue IIS.</span><span class="sxs-lookup"><span data-stu-id="19347-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="19347-105">Per semplificare, NuGet.Server crea una cartella nel server disponibile tramite HTTP(S), nello specifico OData.</span><span class="sxs-lookup"><span data-stu-id="19347-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="19347-106">È semplice da configurare ed è una soluzione ideale per scenari semplici.</span><span class="sxs-lookup"><span data-stu-id="19347-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="19347-107">Creare un'applicazione Web ASP.NET vuota in Visual Studio e aggiungere il pacchetto NuGet.Server.</span><span class="sxs-lookup"><span data-stu-id="19347-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="19347-108">Configurare la cartella `Packages` nell'applicazione e aggiungere i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="19347-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="19347-109">Distribuire l'applicazione in un server appropriato.</span><span class="sxs-lookup"><span data-stu-id="19347-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="19347-110">Le sezioni seguenti descrivono questo processo in dettaglio con C#.</span><span class="sxs-lookup"><span data-stu-id="19347-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="19347-111">In caso di ulteriori domande su NuGet.Server, creare un problema in [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="19347-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="19347-112">Creare e distribuire un'applicazione Web ASP.NET con NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="19347-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="19347-113">In Visual Studio selezionare **File > Nuovo > Progetto**, cercare "ASP.NET", selezionare il modello **Applicazione Web ASP.NET (.NET Framework)** per C# e impostare **Framework** su ".NET Framework 4.6":</span><span class="sxs-lookup"><span data-stu-id="19347-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET", select the **ASP.NET Web Application (.NET Framework)** template for C#, and set **Framework** to ".NET Framework 4.6":</span></span>

    ![Impostazione del framework di destinazione per un nuovo progetto](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="19347-115">Assegnare all'applicazione un nome appropriato *diverso* da NuGet.Server, selezionare OK e nella finestra di dialogo successiva selezionare il modello **Vuoto**, quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="19347-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

1. <span data-ttu-id="19347-116">Fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="19347-116">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="19347-117">Nell'interfaccia utente di Gestione pacchetti selezionare la scheda **Sfoglia**, quindi cercare e installare la versione più recente del pacchetto NuGet.Server se si è scelto come destinazione .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="19347-117">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="19347-118">È anche possibile installarla dalla console di Gestione pacchetti con `Install-Package NuGet.Server`. Se richiesto, accettare le condizioni di licenza.</span><span class="sxs-lookup"><span data-stu-id="19347-118">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Installazione del pacchetto NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

1. <span data-ttu-id="19347-120">L'installazione di NuGet.Server converte l'applicazione Web vuota in un'origine di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="19347-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="19347-121">Installa svariati altri pacchetti, crea una cartella `Packages` nell'applicazione e modifica `web.config` per includere impostazioni aggiuntive (vedere i commenti in tale file per altri dettagli).</span><span class="sxs-lookup"><span data-stu-id="19347-121">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="19347-122">Controllare attentamente `web.config` dopo che il pacchetto NuGet.Server ha completato le modifiche al file.</span><span class="sxs-lookup"><span data-stu-id="19347-122">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="19347-123">NuGet.Server potrebbe non sovrascrivere gli elementi esistenti e creare invece elementi duplicati.</span><span class="sxs-lookup"><span data-stu-id="19347-123">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="19347-124">Quando in un secondo momento si prova a eseguire il progetto, tali duplicati causeranno un "Errore interno del server".</span><span class="sxs-lookup"><span data-stu-id="19347-124">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="19347-125">Ad esempio, se `web.config` contiene `<compilation debug="true" targetFramework="4.5.2" />` prima di installare NuGet.Server, il pacchetto non sovrascrive il file ma inserisce un secondo `<compilation debug="true" targetFramework="4.6" />`.</span><span class="sxs-lookup"><span data-stu-id="19347-125">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="19347-126">In tal caso, eliminare l'elemento con la versione meno recente del framework.</span><span class="sxs-lookup"><span data-stu-id="19347-126">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="19347-127">Per rendere disponibili i pacchetti nel feed quando si pubblica l'applicazione in un server, aggiungere tutti i file `.nupkg` nella cartella `Packages` in Visual Studio e quindi impostare per ognuno **Azione di compilazione** su **Contenuto** e **Copia in directory di output** su **Copia sempre**:</span><span class="sxs-lookup"><span data-stu-id="19347-127">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Copia dei pacchetti nella cartella Packages nel progetto](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="19347-129">Eseguire il sito in locale in Visual Studio (tramite **Debug > Avvia senza eseguire debug** o CTRL+F5).</span><span class="sxs-lookup"><span data-stu-id="19347-129">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="19347-130">Nella home page sono disponibili gli URL del feed dei pacchetti, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="19347-130">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="19347-131">Se si verificano errori, esaminare attentamente il file `web.config` per individuare gli eventuali elementi duplicati come indicato in precedenza nel passaggio 5.</span><span class="sxs-lookup"><span data-stu-id="19347-131">If you see errors, carefully inspect your `web.config` for duplicate elements are noted earlier with step 5.</span></span>

    ![Home page predefinita per un'applicazione con NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="19347-133">Fare clic su **qui** nell'area evidenziata nella figura per visualizzare il feed OData dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="19347-133">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="19347-134">La prima volta che si esegue l'applicazione, NuGet.Server ristruttura la cartella `Packages` in modo che contenga una cartella per ogni pacchetto.</span><span class="sxs-lookup"><span data-stu-id="19347-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="19347-135">Questo corrisponde al [layout di archiviazione locale](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introdotto in NuGet 3.3 per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="19347-135">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="19347-136">Quando si aggiungono altri pacchetti, continuare a seguire questa struttura.</span><span class="sxs-lookup"><span data-stu-id="19347-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="19347-137">Dopo aver verificato la distribuzione locale, distribuire l'applicazione in qualsiasi altro sito interno o esterno, in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="19347-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="19347-138">Dopo la distribuzione in `http://<domain>`, l'URL usato per l'origine dei pacchetti sarà `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="19347-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="19347-139">Configurazione della cartella dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="19347-139">Configuring the Packages folder</span></span>

<span data-ttu-id="19347-140">Con `NuGet.Server` 1.5 e versioni successive è possibile configurare la cartella dei pacchetti in modo più specifico usando il valore `appSetting/packagesPath` in `web.config`:</span><span class="sxs-lookup"><span data-stu-id="19347-140">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="19347-141">`packagesPath` può essere un percorso assoluto o virtuale.</span><span class="sxs-lookup"><span data-stu-id="19347-141">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="19347-142">Quando `packagesPath` viene omesso o lasciato vuoto, il valore predefinito per la cartella dei pacchetti è `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="19347-142">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="19347-143">Aggiunta di pacchetti al feed esternamente</span><span class="sxs-lookup"><span data-stu-id="19347-143">Adding packages to the feed externally</span></span>

<span data-ttu-id="19347-144">Quando un sito NuGet.Server è in esecuzione, è possibile aggiungere i pacchetti tramite [nuget push](../tools/cli-ref-push.md) a condizione di impostare un valore di chiave API in `web.config`.</span><span class="sxs-lookup"><span data-stu-id="19347-144">Once a NuGet.Server site is running, you can add packages using [nuget push](../tools/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="19347-145">Dopo l'installazione del pacchetto NuGet.Server, `web.config` contiene un valore vuoto `appSetting/apiKey`:</span><span class="sxs-lookup"><span data-stu-id="19347-145">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="19347-146">Quando `apiKey` viene omesso o è vuoto, il push dei pacchetti nel feed è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="19347-146">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="19347-147">Per abilitare questa funzionalità, impostare `apiKey` su un valore (idealmente una password complessa) e aggiungere una chiave denominata `appSettings/requireApiKey` con il valore `true`:</span><span class="sxs-lookup"><span data-stu-id="19347-147">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="19347-148">Se il server è già protetto o non è necessaria una chiave API per altri motivi, ad esempio quando si usa un server privato in una rete del team locale, è possibile impostare `requireApiKey` su `false`.</span><span class="sxs-lookup"><span data-stu-id="19347-148">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="19347-149">Tutti gli utenti con accesso al server possono quindi eseguire il push dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="19347-149">All users with access to the server can then push packages.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="19347-150">Rimozione dei pacchetti dal feed</span><span class="sxs-lookup"><span data-stu-id="19347-150">Removing packages from the feed</span></span>

<span data-ttu-id="19347-151">Con NuGet.Server, il comando [nuget delete](../tools/cli-ref-delete.md) rimuove un pacchetto dal repository, purché si includa la chiave API con il commento.</span><span class="sxs-lookup"><span data-stu-id="19347-151">With NuGet.Server, the [nuget delete](../tools/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="19347-152">Se si vuole invece modificare il comportamento per escludere il pacchetto dall'elenco, lasciandolo disponibile per il ripristino, modificare la chiave `enableDelisting` in `web.config` impostandola su true.</span><span class="sxs-lookup"><span data-stu-id="19347-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="19347-153">Supporto di NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="19347-153">NuGet.Server support</span></span>

<span data-ttu-id="19347-154">Per ulteriore assistenza per l'uso di NuGet.Server, creare un problema in [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="19347-154">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>