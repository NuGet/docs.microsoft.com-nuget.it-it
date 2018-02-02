---
title: Uso di NuGet.Server per ospitare feed NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Come creare e ospitare un feed di pacchetti NuGet in qualsiasi server che esegue IIS usando NuGet.Server e rendendo i pacchetti disponibili tramite HTTP e OData.
keywords: Feed NuGet, raccolta NuGet, feed di pacchetti remoti, NuGet.Server
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4cb3f04954fac1b4a39284be187776ab4a19b364
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server è un pacchetto fornito da .NET Foundation che crea un'applicazione ASP.NET in grado di ospitare un feed di pacchetti in qualsiasi server che esegue IIS. Per semplificare, NuGet.Server crea una cartella nel server disponibile tramite HTTP(S), nello specifico OData. È semplice da configurare ed è una soluzione ideale per scenari semplici.

1. Creare un'applicazione Web ASP.NET vuota in Visual Studio e aggiungere il pacchetto NuGet.Server.
1. Configurare la cartella `Packages` nell'applicazione e aggiungere i pacchetti.
1. Distribuire l'applicazione in un server appropriato.

Le sezioni seguenti descrivono questo processo in dettaglio con C#.

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Creare e distribuire un'applicazione Web ASP.NET con NuGet.Server

1. In Visual Studio selezionare **File > Nuovo > Progetto**, impostare il framework di destinazione per .NET Framework 4.6 (vedere di seguito), cercare "ASP.NET" e selezionare il modello **Applicazione Web ASP.NET (.NET Framework)** per C#.

    ![Impostazione della destinazione su .NET Framework 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Assegnare all'applicazione un nome appropriato *diverso* da NuGet.Server, selezionare OK e nella finestra di dialogo successiva selezionare il modello **Vuoto**, quindi selezionare OK.

1. Fare clic con il pulsante destro del mouse sul progetto, scegliere **Gestisci pacchetti NuGet**e nell'interfaccia utente di Gestione pacchetti cercare e installare la versione più recente del pacchetto NuGet.Server se si è scelto come destinazione .NET Framework 4.6. È anche possibile installarla dalla console di Gestione pacchetti con `Install-Package NuGet.Server`.

    ![Installazione del pacchetto NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > Se l'applicazione Web è destinata a .NET Framework 4.5.2, è invece necessario installare NuGet Server **2.10.3**.

1. L'installazione di NuGet.Server converte l'applicazione Web vuota in un'origine di pacchetto. Crea una cartella `Packages` dell'applicazione e sovrascrive `web.config` per includere le impostazioni aggiuntive (vedere i commenti in tale file per altri dettagli).

1. Per rendere disponibili i pacchetti nel feed quando si pubblica l'applicazione in un server, aggiungere i relativi file `.nupkg` nella cartella `Packages` in Visual Studio e quindi impostare **Azione di compilazione** su **Contenuto** e **Copia in directory di output** su **Copia sempre**:

    ![Copia dei pacchetti nella cartella Packages nel progetto](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Eseguire il sito in locale in Visual Studio (senza eseguire il debug, ovvero CTRL+F5). Nella home page sono disponibili gli URL del feed dei pacchetti:

    ![Home page predefinita per un'applicazione con NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. Fare clic su **qui** nell'area evidenziata nella figura per visualizzare il feed OData dei pacchetti.

1. La prima volta che si esegue l'applicazione, NuGet.Server ristruttura la cartella `Packages` in modo che contenga una cartella per ogni pacchetto. Questo corrisponde al [layout di archiviazione locale](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introdotto in NuGet 3.3 per migliorare le prestazioni. Quando si aggiungono altri pacchetti, continuare a seguire questa struttura.

1. Dopo aver verificato la distribuzione locale, distribuire l'applicazione in qualsiasi altro sito interno o esterno, in base alle esigenze.
1. Dopo la distribuzione in `http://<domain>`, l'URL usato per l'origine dei pacchetti sarà `http://<domain>/nuget`.

## <a name="configuring-the-packages-folder"></a>Configurazione della cartella dei pacchetti

Con `NuGet.Server` 1.5 e versioni successive è possibile configurare la cartella dei pacchetti in modo più specifico usando il valore `appSetting/packagesPath` in `web.config`:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` può essere un percorso assoluto o virtuale.

Quando `packagesPath` viene omesso o lasciato vuoto, il valore predefinito per la cartella dei pacchetti è `~/Packages`.

## <a name="adding-packages-to-the-feed-externally"></a>Aggiunta di pacchetti al feed esternamente

Quando un sito NuGet.Server è in esecuzione, è possibile aggiungere o eliminare i pacchetti tramite nuget.exe a condizione di impostare un valore di chiave API in `web.config`.

Dopo l'installazione del pacchetto NuGet.Server, `web.config` contiene un valore vuoto `appSetting/apiKey`:

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

Quando `apiKey` viene omesso o è vuoto, il push dei pacchetti nel feed è disabilitato.

Per abilitare questa funzionalità, impostare `apiKey` su un valore (idealmente una password complessa) e aggiungere una chiave denominata `appSettings/requireApiKey` con il valore `true`:

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Se il server è già protetto o non è necessaria una chiave API per altri motivi, ad esempio quando si usa un server privato in una rete del team locale, è possibile impostare `requireApiKey` su `false`. Tutti gli utenti con accesso al server possono quindi eseguire il push dei pacchetti o eliminarli.