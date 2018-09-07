---
title: Uso di NuGet.Server per ospitare feed NuGet
description: Come creare e ospitare un feed di pacchetti NuGet in qualsiasi server che esegue IIS usando NuGet.Server e rendendo i pacchetti disponibili tramite HTTP e OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: e99d42744ec860976ae098be94e747ec4bc9a7c6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551956"
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server è un pacchetto fornito da .NET Foundation che crea un'applicazione ASP.NET in grado di ospitare un feed di pacchetti in qualsiasi server che esegue IIS. Per semplificare, NuGet.Server crea una cartella nel server disponibile tramite HTTP(S), nello specifico OData. È semplice da configurare ed è una soluzione ideale per scenari semplici.

1. Creare un'applicazione Web ASP.NET vuota in Visual Studio e aggiungere il pacchetto NuGet.Server.
1. Configurare la cartella `Packages` nell'applicazione e aggiungere i pacchetti.
1. Distribuire l'applicazione in un server appropriato.

Le sezioni seguenti descrivono questo processo in dettaglio con C#.

In caso di ulteriori domande su NuGet.Server, creare un problema in [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Creare e distribuire un'applicazione Web ASP.NET con NuGet.Server

1. In Visual Studio selezionare **File > Nuovo > Progetto**, cercare "ASP.NET", selezionare il modello **Applicazione Web ASP.NET (.NET Framework)** per C# e impostare **Framework** su ".NET Framework 4.6":

    ![Impostazione del framework di destinazione per un nuovo progetto](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Assegnare all'applicazione un nome appropriato *diverso* da NuGet.Server, selezionare OK e nella finestra di dialogo successiva selezionare il modello **Vuoto**, quindi selezionare **OK**.

1. Fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**.

1. Nell'interfaccia utente di Gestione pacchetti selezionare la scheda **Sfoglia**, quindi cercare e installare la versione più recente del pacchetto NuGet.Server se si è scelto come destinazione .NET Framework 4.6. È anche possibile installarla dalla console di Gestione pacchetti con `Install-Package NuGet.Server`. Se richiesto, accettare le condizioni di licenza.

    ![Installazione del pacchetto NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

1. L'installazione di NuGet.Server converte l'applicazione Web vuota in un'origine di pacchetto. Installa svariati altri pacchetti, crea una cartella `Packages` nell'applicazione e modifica `web.config` per includere impostazioni aggiuntive (vedere i commenti in tale file per altri dettagli).

    > [!Important]
    > Controllare attentamente `web.config` dopo che il pacchetto NuGet.Server ha completato le modifiche al file. NuGet.Server potrebbe non sovrascrivere gli elementi esistenti e creare invece elementi duplicati. Quando in un secondo momento si prova a eseguire il progetto, tali duplicati causeranno un "Errore interno del server". Ad esempio, se `web.config` contiene `<compilation debug="true" targetFramework="4.5.2" />` prima di installare NuGet.Server, il pacchetto non sovrascrive il file ma inserisce un secondo `<compilation debug="true" targetFramework="4.6" />`. In tal caso, eliminare l'elemento con la versione meno recente del framework.

1. Per rendere disponibili i pacchetti nel feed quando si pubblica l'applicazione in un server, aggiungere tutti i file `.nupkg` nella cartella `Packages` in Visual Studio e quindi impostare per ognuno **Azione di compilazione** su **Contenuto** e **Copia in directory di output** su **Copia sempre**:

    ![Copia dei pacchetti nella cartella Packages nel progetto](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Eseguire il sito in locale in Visual Studio (tramite **Debug > Avvia senza eseguire debug** o CTRL+F5). Nella home page sono disponibili gli URL del feed dei pacchetti, come indicato di seguito. Se si verificano errori, esaminare attentamente il file `web.config` per individuare gli eventuali elementi duplicati come indicato in precedenza nel passaggio 5.

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

Quando un sito NuGet.Server è in esecuzione, è possibile aggiungere i pacchetti tramite [nuget push](../tools/cli-ref-push.md) a condizione di impostare un valore di chiave API in `web.config`.

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

Se il server è già protetto o non è necessaria una chiave API per altri motivi, ad esempio quando si usa un server privato in una rete del team locale, è possibile impostare `requireApiKey` su `false`. Tutti gli utenti con accesso al server possono quindi eseguire il push dei pacchetti.

## <a name="removing-packages-from-the-feed"></a>Rimozione dei pacchetti dal feed

Con NuGet.Server, il comando [nuget delete](../tools/cli-ref-delete.md) rimuove un pacchetto dal repository, purché si includa la chiave API con il commento.

Se si vuole invece modificare il comportamento per escludere il pacchetto dall'elenco, lasciandolo disponibile per il ripristino, modificare la chiave `enableDelisting` in `web.config` impostandola su true.

## <a name="nugetserver-support"></a>Supporto di NuGet.Server

Per ulteriore assistenza per l'uso di NuGet.Server, creare un problema in [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).