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
ms.openlocfilehash: 36a7c2b1d056dddf07a59737de1c3e94294689ac
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="create-and-publish-a-package"></a>Creare e pubblicare un pacchetto

La creazione di un pacchetto NuGet da una libreria di classi .NET e la pubblicazione in nuget.org sono un processo semplice, che viene illustrato nei passaggi seguenti usando l'interfaccia della riga di comando di NuGet e Visual Studio:

- [Prerequisiti](#install-pre-requisites)
- [Creare il file manifesto del pacchetto con estensione nuspec](#create-the-nuspec-package-manifest-file)
- [Eseguire il comando pack](#run-the-pack-command)
- [Pubblicare il pacchetto](#publish-the-package)

## <a name="pre-requisites"></a>Prerequisiti

1. Installare un'edizione di Visual Studio 2017 da [visualstudio.com](https://www.visualstudio.com/).

1. Installare lo strumento dell'interfaccia della riga di comando di NuGet, `nuget.exe`, scaricando la versione più recente di `nuget.exe` da [nuget.org/downloads](https://nuget.org/downloads) e salvare il file `.exe` in una posizione nella variabile PATH. Tenere presente che il download *è* solo lo strumento e non un programma di installazione.

1. Creare un progetto libreria di classi .NET appropriato per il codice per cui si vuole creare il pacchetto. Se non si ha già un progetto, è possibile crearne uno semplice come segue:
    1. In Visual Studio scegliere **File > Nuovo > Progetto**, espandere il nodo **Visual C# > Windows**, selezionare il modello "Libreria di classi", assegnare al progetto il nome AppLogger e fare clic su **OK**.
    1. Fare clic con il pulsante destro del mouse sul file di progetto risultante e scegliere **Compila** per verificare che il progetto sia stato creato correttamente. La DLL è presente nella cartella Debug (o Release se si crea invece tale configurazione).

    In un vero pacchetto NuGet si implementeranno ovviamente diverse utili funzionalità in base alle quali gli altri utenti potranno compilare le applicazioni. In questa procedura dettagliata tuttavia non si scriverà codice aggiuntivo perché una libreria di classi dal modello è sufficiente per creare un pacchetto.

## <a name="create-the-nuspec-package-manifest-file"></a>Creare il file manifesto del pacchetto con estensione nuspec

Per ogni pacchetto NuGet è necessario un manifesto, ovvero un file `.nuspec`, che ne descriva i contenuti e le dipendenze. Il comando `nuget spec` crea automaticamente questo file che viene quindi personalizzato dall'utente. In questo esempio si crea il file `.nuspec` da un file di progetto. È anche possibile creare il manifesto in altro modo, come illustrato in [Creare un pacchetto](../create-packages/creating-a-package.md).

1. Aprire un prompt dei comandi e passare alla cartella contenente il file di progetto (`.csproj`).

1. Eseguire il comando `spec` dell'interfaccia della riga di comando di NuGet per generare il manifesto, il cui nome si basa su quello del progetto, ad esempio `AppLogger.nuspec`:

    ```
    nuget spec
    ```

1. Aprire il file in un editor di testo. Il manifesto è simile al codice sotto, dove i token nel formato *$`<token>`$* devono essere sostituiti durante il processo di creazione del pacchetto con i valori del file Properties/AssemblyInfo.cs del progetto. Per altre informazioni dettagliate sui token, vedere [Creazione di un file con estensione nuspec](../create-packages/creating-a-package.md#creating-the-nuspec-file).

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

1. Selezionare un ID pacchetto univoco in nuget.org. È consigliabile usare le convenzione di denominazione descritte in [Creazione di un pacchetto](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Assicurarsi di aggiornare i tag author e description per evitare che si verifichi un errore nel passaggio successivo. Ecco un file `.nuspec` aggiornato come esempio:

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
> Per i pacchetti compilati per uso pubblico, prestare particolare attenzione all'elemento `<tags>`, perché questi tag consentono ad altri utenti di trovare il pacchetto e di conoscerne le funzioni.

## <a name="run-the-pack-command"></a>Eseguire il comando pack

Per compilare un pacchetto NuGet (un file `.nupkg`) da un progetto, eseguire il comando `pack`:

```
nuget pack AppLogger.csproj
```

Questo comando crea `AppLogger.1.0.0.0.nupkg` usando il nome del pacchetto e il numero di versione del file `.nuspec`. Questo comando genera avvisi se i valori predefiniti dei diversi campi del file `.nuspec` non sono stati aggiornati.

## <a name="publish-the-package"></a>Pubblicare il pacchetto

Dopo avere creato un file `.nupkg`, lo si pubblica in nuget.org usando il comando `push`. In alternativa, è possibile usare il [flusso di lavoro di pubblicazione di nuget.org](../create-packages/publish-a-package.md#publish-to-nugetorg).

> [!Warning]
> I pacchetti pubblicati in nuget.org sono visibili pubblicamente dagli altri sviluppatori. Per ospitare i pacchetti privatamente, vedere [Hosting dei pacchetti](../hosting-packages/overview.md).


1. Creare un account gratuito in [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) o eseguire l'accesso se ne è già disponibile uno. Quando si crea un nuovo account, viene inviato un messaggio di posta elettronica di conferma. È necessario confermare l'account prima di poter caricare un pacchetto.

1. Dopo avere eseguito l'accesso, selezionare il nome utente (in alto a destra), quindi selezionare **Chiavi API**.

1. Selezionare **Crea**, specificare un nome per la chiave, selezionare **Seleziona ambiti > Push**. In **Chiave API** immettere * in **Criterio GLOB**, quindi selezionare **Crea**.

1. Dopo avere creato la chiave, selezionare **Copia** per recuperare la chiave di accesso che sarà necessaria nell'interfaccia della riga di comando:

    ![Copia della chiave API negli Appunti](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > Salvare la chiave in una posizione sicura e mantenerla segreta. Se la chiave viene accidentalmente rivelata, è sempre possibile generarla di nuovo in qualsiasi momento. È anche possibile rimuovere la chiave API se non si vuole più eseguire il push tramite l'interfaccia della riga di comando.

1. Al prompt dei comandi eseguire il comando seguente, specificando il nome del pacchetto e sostituendo la chiave con il valore copiato nel passaggio 4:

    ```
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```
    
1. nuget.exe visualizza i risultati del processo di pubblicazione:

    ```
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. Dal profilo in nuget.org selezionare **Manage Packages** (Gestisci pacchetti) per visualizzare quello appena pubblicato. Viene anche inviato un messaggio di posta elettronica di conferma. Si noti che l'indicizzazione e la visualizzazione del pacchetto nei risultati della ricerca, dove gli altri utenti possono trovarlo, potrebbero richiedere qualche minuto. In questo intervallo di tempo la pagina del pacchetto visualizza un messaggio simile al seguente:

    ![Il pacchetto non è stato ancora indicizzato. Verrà visualizzato nei risultati della ricerca e sarà disponibile per l'installazione e il ripristino al termine dell'indicizzazione.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> **Ricerca dei virus**: tutti i pacchetti caricati in nuget.org vengono analizzati alla ricerca di virus e rifiutati se vengono trovati virus. Tutti i pacchetti elencati in nuget.org vengono anche analizzati periodicamente.

L'operazione è ora completata. È stato pubblicato in [nuget.org](https://www.nuget.org/) il primo pacchetto NuGet, che gli altri sviluppatori possono usare nei propri progetti.

## <a name="related-topics"></a>Argomenti correlati

- [Creare un pacchetto](../create-packages/creating-a-package.md)
- [Pubblicare un pacchetto](../create-packages/publish-a-package.md)
- [Supportare più framework di destinazione](../create-packages/supporting-multiple-target-frameworks.md)
- [Controllo delle versioni dei pacchetti](../reference/package-versioning.md)
- [Creazione di pacchetti localizzati](../create-packages/creating-localized-packages.md)
