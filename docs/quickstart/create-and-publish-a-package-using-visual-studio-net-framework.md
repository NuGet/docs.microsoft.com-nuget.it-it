---
title: Creare e pubblicare un pacchetto .NET Framework con Visual Studio in Windows
description: Esercitazione sulla creazione e pubblicazione di un pacchetto NuGet .NET Framework con Visual Studio 2017 in Windows.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: ffa2128b577673e980f4115f37f8685858c36250
ms.sourcegitcommit: 6cffa6ef59b922df2d87aa9c24034d00542983cd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2018
ms.locfileid: "37963159"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a>Guida introduttiva: Creare e pubblicare un pacchetto con Visual Studio (.NET Framework, Windows)

La creazione di un pacchetto NuGet da una libreria di classi .NET Framework prevede la creazione della DLL in Visual Studio in Windows, quindi l'uso dello strumento da riga di comando nuget.exe per creare e pubblicare il pacchetto.

> [!Note]
> Questa guida introduttiva si applica solo a Visual Studio 2017 per Windows. Visual Studio per Mac non include le funzionalità descritte di seguito. Usare invece gli [strumenti dell'interfaccia della riga di comando dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Prerequisiti

1. Installare qualsiasi edizione di Visual Studio 2017 da [visualstudio.com](https://www.visualstudio.com/) con qualsiasi carico di lavoro correlato a .NET. Visual Studio 2017 include automaticamente le funzionalità di NuGet quando viene installato un carico di lavoro .NET.

1. Installare l'interfaccia della riga di comando `nuget.exe` scaricandola da [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), salvare il file `.exe` in una cartella appropriata e aggiungere tale cartella alla variabile di ambiente PATH.

1. [Registrarsi per ottenere un account gratuito in nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) se non è già disponibile. Quando si crea un nuovo account, viene inviato un messaggio di posta elettronica di conferma. È necessario confermare l'account prima di poter caricare un pacchetto.

## <a name="create-a-class-library-project"></a>Creare un progetto di libreria di classi

È possibile usare un progetto libreria di classi .NET Framework esistente per il codice che si vuole includere in un pacchetto oppure creare un progetto semplice come segue:

1. In Visual Studio scegliere **File > Nuovo > Progetto**, selezionare il nodo **Visual C#**, selezionare il modello "Libreria di classi (.NET Framework)", assegnare al progetto il nome AppLogger e fare clic su **OK**.

1. Fare clic con il pulsante destro del mouse sul file di progetto risultante e scegliere **Compila** per verificare che il progetto sia stato creato correttamente. La DLL è presente nella cartella Debug (o Release se si crea invece tale configurazione).

In un vero pacchetto NuGet si implementano ovviamente molte funzionalità utili, che altri possono sfruttare per compilare nuove applicazioni. È anche possibile impostare i framework di destinazione desiderati. Ad esempio, vedere le guide per [UWP](../guides/create-uwp-packages.md) e [Xamarin](../guides/create-packages-for-xamarin.md).

In questa procedura dettagliata tuttavia non si scriverà codice aggiuntivo perché una libreria di classi dal modello è sufficiente per creare un pacchetto. Tuttavia, se si desidera del codice funzionale per il pacchetto, usare le opzioni riportate di seguito:

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
> A meno che non esista un motivo valido per decidere diversamente, .NET Standard è la destinazione preferita per i pacchetti NuGet, perché garantisce la compatibilità con la gamma più ampia di progetti consumer. Vedere [Creare e pubblicare un pacchetto con Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).

## <a name="configure-project-properties-for-the-package"></a>Configurare le proprietà del progetto per il pacchetto

Un pacchetto NuGet contiene un manifesto (file `.nuspec`), che contiene i metadati pertinenti, ad esempio l'identificatore del pacchetto, il numero di versione, la descrizione e altro ancora. Alcuni di questi metadati possono essere recuperati direttamente dalle proprietà del progetto, evitando così di doverli aggiornare separatamente sia nel progetto che nel manifesto. Questa sezione descrive come impostare le proprietà pertinenti.

1. Selezionare il comando di menu **Progetto > Proprietà** e quindi selezionare la scheda **Applicazione**.

1. Nel campo **Nome assembly** assegnare un identificatore univoco al pacchetto.

    > [!Important]
    > È necessario assegnare al pacchetto un identificatore univoco in nuget.org o per qualsiasi host in uso. Per questa procedura dettagliata, si consiglia di includere "Sample" o "Test" nel nome, perché il passaggio di pubblicazione descritto più avanti rende il pacchetto visibile pubblicamente (nonostante sia improbabile che chiunque lo usi effettivamente).
    >
    > Se si tenta di pubblicare un pacchetto con un nome già esistente, viene visualizzato un errore.

1. Selezionare il pulsante **Informazioni assembly** che visualizza una finestra di dialogo in cui è possibile immettere altre proprietà che provengono dal manifesto (vedere [Informazioni di riferimento sul file .nuspec - Token di sostituzione](../reference/nuspec.md#replacement-tokens)). I campi più comunemente usati sono **Titolo**, **Descrizione**, **Azienda**, **Copyright** e **Versione assembly**. Queste proprietà vengono infine visualizzate con il pacchetto in un host come nuget.org, pertanto assicurarsi che siano sufficientemente descrittive.

    ![Informazioni sull'assembly in un progetto .NET Framework in Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. Facoltativo: per visualizzare e modificare direttamente le proprietà, aprire il file `Properties/AssemblyInfo.cs` nel progetto.

1. Quando vengono impostate le proprietà, impostare la configurazione del progetto su **Versione** e ricompilare il progetto per generare le DLL aggiornate.

## <a name="generate-the-initial-manifest"></a>Generare il manifesto iniziale

Ora che è disponibile una DLL e le proprietà del progetto sono impostate, è possibile usare il comando `nuget spec` per generare un file iniziale `.nuspec` dal progetto. Questo passaggio include i token di sostituzione rilevanti per recuperare le informazioni dal file di progetto.

Eseguire `nuget spec` una sola volta per generare il manifesto iniziale. Quando si aggiorna il pacchetto, è possibile cambiare i valori nel progetto o modificare direttamente il manifesto.

1. Aprire un prompt dei comandi e passare alla cartella del progetto contenente il file `AppLogger.csproj`.

1. Eseguire il comando seguente: `nuget spec AppLogger.csproj`. Specificando un progetto, NuGet crea un manifesto che corrisponde al nome del progetto, in questo caso `AppLogger.nuspec`. Vengono anche inclusi i token di sostituzione nel manifesto.

1. Aprire `AppLogger.nuspec` in un editor di testo per esaminarne il contenuto, che dovrebbe essere simile al seguente:

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

## <a name="edit-the-manifest"></a>Modificare il manifesto

1. NuGet genera un errore se si prova a creare un pacchetto con i valori predefiniti nel file `.nuspec`, quindi è necessario modificare i campi seguenti prima di procedere. Vedere [Informazioni di riferimento sul file .nuspec - Singoli elementi](../reference/nuspec.md#single-elements) per una descrizione di come vengono usati questi campi.

    - licenseUrl
    - projectUrl
    - iconUrl
    - releaseNotes
    - tag

1. Per i pacchetti compilati per uso pubblico, prestare particolare attenzione alla proprietà **Tags**, perché i tag consentono ad altri utenti di trovare il pacchetto in origini come nuget.org e di comprenderne le funzioni.

1. È anche possibile aggiungere altri elementi al manifesto in questo momento, come descritto in [Informazioni di riferimento sul file .nuspec](../reference/nuspec.md).

1. Salvare il file prima di procedere.

## <a name="run-the-pack-command"></a>Eseguire il comando pack

1. Da un prompt dei comandi nella cartella contenente il file `.nuspec`, eseguire il comando `nuget pack`.

1. NuGet genera un file `.nupkg` nel formato *identificatore-versione.nupkg* nella cartella corrente.

## <a name="publish-the-package"></a>Pubblicare il pacchetto

Dopo aver creato un file `.nupkg`, pubblicarlo in nuget.org usando `nuget.exe` insieme a una chiave API acquisita da nuget.org. Per nuget.org è necessario usare `nuget.exe` 4.1.0 o versione successiva.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Acquisire la chiave API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Pubblicare con nuget push

1. Passare alla cartella contenente il file `.nupkg`.

1. Eseguire il comando seguente, specificando il nome del pacchetto e sostituendo il valore di chiave con la chiave API:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe visualizza i risultati del processo di pubblicazione:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Vedere [nuget push](../tools/cli-ref-push.md).

### <a name="publish-errors"></a>Errori di pubblicazione

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Gestire il pacchetto pubblicato

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Argomenti correlati

- [Creare un pacchetto](../create-packages/creating-a-package.md)
- [Pubblicare un pacchetto](../create-packages/publish-a-package.md)
- [Pacchetti in versione non definitiva](../create-packages/Prerelease-Packages.md)
- [Supportare più framework di destinazione](../create-packages/supporting-multiple-target-frameworks.md)
- [Controllo delle versioni dei pacchetti](../reference/package-versioning.md)
- [Creazione di pacchetti localizzati](../create-packages/creating-localized-packages.md)
