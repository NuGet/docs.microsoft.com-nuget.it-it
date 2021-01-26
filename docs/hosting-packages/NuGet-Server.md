---
title: Uso di NuGet.Server per ospitare feed NuGet
description: Come creare e ospitare un feed di pacchetti NuGet in qualsiasi server che esegue IIS usando NuGet.Server e rendendo i pacchetti disponibili tramite HTTP e OData.
author: JonDouglas
ms.author: jodou
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 3a9fb843f071eda72b9469292a7276ad81f8c24d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774080"
---
# <a name="nugetserver"></a><span data-ttu-id="17a88-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="17a88-103">NuGet.Server</span></span>

<span data-ttu-id="17a88-104">NuGet.Server è un pacchetto fornito da .NET Foundation che crea un'applicazione ASP.NET in grado di ospitare un feed di pacchetti in qualsiasi server che esegue IIS.</span><span class="sxs-lookup"><span data-stu-id="17a88-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="17a88-105">Per semplificare, NuGet.Server crea una cartella nel server disponibile tramite HTTP(S), nello specifico OData.</span><span class="sxs-lookup"><span data-stu-id="17a88-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="17a88-106">È semplice da configurare ed è una soluzione ideale per scenari semplici.</span><span class="sxs-lookup"><span data-stu-id="17a88-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="17a88-107">Creare un'applicazione Web ASP.NET vuota in Visual Studio e aggiungere il pacchetto NuGet.Server.</span><span class="sxs-lookup"><span data-stu-id="17a88-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="17a88-108">Configurare la cartella `Packages` nell'applicazione e aggiungere i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="17a88-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="17a88-109">Distribuire l'applicazione in un server appropriato.</span><span class="sxs-lookup"><span data-stu-id="17a88-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="17a88-110">Le sezioni seguenti descrivono questo processo in dettaglio con C#.</span><span class="sxs-lookup"><span data-stu-id="17a88-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="17a88-111">Per altre domande su NuGet. Server, creare un problema in [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues) .</span><span class="sxs-lookup"><span data-stu-id="17a88-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="17a88-112">Creare e distribuire un'applicazione Web ASP.NET con NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="17a88-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="17a88-113">In Visual Studio selezionare **File > nuovo progetto >**, cercare "applicazione Web ASP.NET (.NET Framework)" e selezionare il modello corrispondente per **C#**.</span><span class="sxs-lookup"><span data-stu-id="17a88-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET Web Application (.NET Framework)", select the matching template for **C#**.</span></span>

    ![Selezionare il modello di progetto Web .NET Framework](media/Hosting_00-NuGet.Server-ProjectType.png)

1. <span data-ttu-id="17a88-115">Impostare **Framework** su ".NET Framework 4,6".</span><span class="sxs-lookup"><span data-stu-id="17a88-115">Set **Framework** to ".NET Framework 4.6".</span></span>

    ![Impostazione del framework di destinazione per un nuovo progetto](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="17a88-117">Assegnare all'applicazione un nome appropriato *diverso* da NuGet.Server, selezionare OK e nella finestra di dialogo successiva selezionare il modello **Vuoto**, quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="17a88-117">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

    ![Selezionare il progetto Web vuoto](media/Hosting_02-NuGet.Server-Empty.png)

1. <span data-ttu-id="17a88-119">Fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="17a88-119">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="17a88-120">Nell'interfaccia utente di Gestione pacchetti selezionare la scheda **Sfoglia**, quindi cercare e installare la versione più recente del pacchetto NuGet.Server se si è scelto come destinazione .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="17a88-120">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="17a88-121">È anche possibile installarlo dalla console di gestione pacchetti con `Install-Package NuGet.Server` . Se richiesto, accettare le condizioni di licenza.</span><span class="sxs-lookup"><span data-stu-id="17a88-121">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Installazione del pacchetto NuGet.Server](media/Hosting_03-NuGet.Server-Package.png)

1. <span data-ttu-id="17a88-123">L'installazione di NuGet.Server converte l'applicazione Web vuota in un'origine di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="17a88-123">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="17a88-124">Installa svariati altri pacchetti, crea una cartella `Packages` nell'applicazione e modifica `web.config` per includere impostazioni aggiuntive (vedere i commenti in tale file per altri dettagli).</span><span class="sxs-lookup"><span data-stu-id="17a88-124">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="17a88-125">Controllare attentamente `web.config` dopo che il pacchetto NuGet.Server ha completato le modifiche al file.</span><span class="sxs-lookup"><span data-stu-id="17a88-125">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="17a88-126">NuGet.Server potrebbe non sovrascrivere gli elementi esistenti e creare invece elementi duplicati.</span><span class="sxs-lookup"><span data-stu-id="17a88-126">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="17a88-127">Quando in un secondo momento si prova a eseguire il progetto, tali duplicati causeranno un "Errore interno del server".</span><span class="sxs-lookup"><span data-stu-id="17a88-127">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="17a88-128">Ad esempio, se `web.config` contiene `<compilation debug="true" targetFramework="4.5.2" />` prima di installare NuGet.Server, il pacchetto non sovrascrive il file ma inserisce un secondo `<compilation debug="true" targetFramework="4.6" />`.</span><span class="sxs-lookup"><span data-stu-id="17a88-128">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="17a88-129">In tal caso, eliminare l'elemento con la versione meno recente del framework.</span><span class="sxs-lookup"><span data-stu-id="17a88-129">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="17a88-130">Eseguire il sito in locale in Visual Studio (tramite **Debug > Avvia senza eseguire debug** o CTRL+F5).</span><span class="sxs-lookup"><span data-stu-id="17a88-130">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="17a88-131">Nella home page sono disponibili gli URL del feed dei pacchetti, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="17a88-131">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="17a88-132">Se vengono visualizzati errori, controllare attentamente la presenza `web.config` di elementi duplicati come indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="17a88-132">If you see errors, carefully inspect your `web.config` for duplicate elements as noted earlier.</span></span>

    ![Home page predefinita per un'applicazione con NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  <span data-ttu-id="17a88-134">La prima volta che si esegue l'applicazione, NuGet.Server ristruttura la cartella `Packages` in modo che contenga una cartella per ogni pacchetto.</span><span class="sxs-lookup"><span data-stu-id="17a88-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="17a88-135">Questo corrisponde al [layout di archiviazione locale](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introdotto in NuGet 3.3 per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="17a88-135">This matches the [local storage layout](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="17a88-136">Quando si aggiungono altri pacchetti, continuare a seguire questa struttura.</span><span class="sxs-lookup"><span data-stu-id="17a88-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="17a88-137">Dopo aver verificato la distribuzione locale, distribuire l'applicazione in qualsiasi altro sito interno o esterno, in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="17a88-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="17a88-138">Dopo la distribuzione in `http://<domain>`, l'URL usato per l'origine dei pacchetti sarà `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="17a88-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="17a88-139">Aggiunta di pacchetti al feed esternamente</span><span class="sxs-lookup"><span data-stu-id="17a88-139">Adding packages to the feed externally</span></span>

<span data-ttu-id="17a88-140">Quando un sito NuGet.Server è in esecuzione, è possibile aggiungere i pacchetti tramite [nuget push](../reference/cli-reference/cli-ref-push.md) a condizione di impostare un valore di chiave API in `web.config`.</span><span class="sxs-lookup"><span data-stu-id="17a88-140">Once a NuGet.Server site is running, you can add packages using [nuget push](../reference/cli-reference/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="17a88-141">Dopo l'installazione del pacchetto NuGet.Server, `web.config` contiene un valore vuoto `appSetting/apiKey`:</span><span class="sxs-lookup"><span data-stu-id="17a88-141">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="17a88-142">Quando `apiKey` viene omesso o è vuoto, il push dei pacchetti nel feed è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="17a88-142">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="17a88-143">Per abilitare questa funzionalità, impostare `apiKey` su un valore (idealmente una password complessa) e aggiungere una chiave denominata `appSettings/requireApiKey` con il valore `true`:</span><span class="sxs-lookup"><span data-stu-id="17a88-143">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="17a88-144">Se il server è già protetto o non è necessaria una chiave API per altri motivi, ad esempio quando si usa un server privato in una rete del team locale, è possibile impostare `requireApiKey` su `false`.</span><span class="sxs-lookup"><span data-stu-id="17a88-144">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="17a88-145">Tutti gli utenti con accesso al server possono quindi eseguire il push dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="17a88-145">All users with access to the server can then push packages.</span></span>

<span data-ttu-id="17a88-146">A partire da NuGet. Server 3.0.0, l'URL per il push dei pacchetti è stato modificato in `http://<domain>/nuget` .</span><span class="sxs-lookup"><span data-stu-id="17a88-146">Starting with NuGet.Server 3.0.0, the URL for pushing packages was change to `http://<domain>/nuget`.</span></span> <span data-ttu-id="17a88-147">Prima della versione 3.0.0, l'URL di push era `http://<domain>/api/v2/package` .</span><span class="sxs-lookup"><span data-stu-id="17a88-147">Prior to the 3.0.0 release, the push URL was `http://<domain>/api/v2/package`.</span></span>

<span data-ttu-id="17a88-148">Con NuGet 3.2.1 e versioni successive, questo URL legacy `/api/v2/package` è abilitato in aggiunta a per `/nuget` impostazione predefinita tramite `enableLegacyPushRoute: true` l'opzione nella configurazione di avvio ( `NuGetODataConfig.cs` per impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="17a88-148">With NuGet 3.2.1 and newer, this legacy URL `/api/v2/package` is enabled in addition to `/nuget` by default via `enableLegacyPushRoute: true` option in your startup config (`NuGetODataConfig.cs` by default).</span></span> <span data-ttu-id="17a88-149">Si noti che questa funzionalità non funziona quando più feed sono ospitati nello stesso progetto.</span><span class="sxs-lookup"><span data-stu-id="17a88-149">Note that this feature does not work when multiple feeds are hosted in the same project.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="17a88-150">Rimozione dei pacchetti dal feed</span><span class="sxs-lookup"><span data-stu-id="17a88-150">Removing packages from the feed</span></span>

<span data-ttu-id="17a88-151">Con NuGet.Server, il comando [nuget delete](../reference/cli-reference/cli-ref-delete.md) rimuove un pacchetto dal repository, purché si includa la chiave API con il commento.</span><span class="sxs-lookup"><span data-stu-id="17a88-151">With NuGet.Server, the [nuget delete](../reference/cli-reference/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="17a88-152">Se si vuole invece modificare il comportamento per escludere il pacchetto dall'elenco, lasciandolo disponibile per il ripristino, modificare la chiave `enableDelisting` in `web.config` impostandola su true.</span><span class="sxs-lookup"><span data-stu-id="17a88-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="17a88-153">Configurazione della cartella dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="17a88-153">Configuring the Packages folder</span></span>

<span data-ttu-id="17a88-154">Con `NuGet.Server` 1,5 e versioni successive, è possibile personalizzare la cartella del pacchetto usando il `appSettings/packagesPath` valore in `web.config` :</span><span class="sxs-lookup"><span data-stu-id="17a88-154">With `NuGet.Server` 1.5 and later, you can customize the package folder using the `appSettings/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="17a88-155">`packagesPath` può essere un percorso assoluto o virtuale.</span><span class="sxs-lookup"><span data-stu-id="17a88-155">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="17a88-156">Quando `packagesPath` viene omesso o lasciato vuoto, il valore predefinito per la cartella dei pacchetti è `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="17a88-156">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="making-packages-available-when-you-publish-the-web-app"></a><span data-ttu-id="17a88-157">Rendere disponibili i pacchetti quando si pubblica l'app Web</span><span class="sxs-lookup"><span data-stu-id="17a88-157">Making packages available when you publish the web app</span></span>

<span data-ttu-id="17a88-158">Per rendere disponibili i pacchetti nel feed quando si pubblica l'applicazione in un server, aggiungere tutti i file `.nupkg` nella cartella `Packages` in Visual Studio e quindi impostare per ognuno **Azione di compilazione** su **Contenuto** e **Copia in directory di output** su **Copia sempre**:</span><span class="sxs-lookup"><span data-stu-id="17a88-158">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

![Copia dei pacchetti nella cartella Packages nel progetto](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a><span data-ttu-id="17a88-160">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="17a88-160">Release Notes</span></span>

<span data-ttu-id="17a88-161">Note sulla versione per NuGet. Server sono disponibili nella [pagina della versione GitHub](https://github.com/NuGet/NuGet.Server/releases).</span><span class="sxs-lookup"><span data-stu-id="17a88-161">Release notes for NuGet.Server are available on the [GitHub release page](https://github.com/NuGet/NuGet.Server/releases).</span></span>
<span data-ttu-id="17a88-162">Sono inclusi i dettagli sulle correzioni di bug e sulle nuove funzionalità aggiunte.</span><span class="sxs-lookup"><span data-stu-id="17a88-162">This includes details about bug fixes and new features that are added.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="17a88-163">Supporto di NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="17a88-163">NuGet.Server support</span></span>

<span data-ttu-id="17a88-164">Per ulteriori informazioni sull'utilizzo di NuGet. Server, creare un problema in [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues) .</span><span class="sxs-lookup"><span data-stu-id="17a88-164">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>
