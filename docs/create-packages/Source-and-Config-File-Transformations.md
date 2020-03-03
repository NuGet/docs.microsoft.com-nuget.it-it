---
title: Trasformazioni di codice sorgente e file di configurazione per i pacchetti NuGet
description: Informazioni dettagliate sulla capacità per i pacchetti NuGet di trasformare il codice sorgente e i file di configurazione (XML) durante l'installazione.
author: karann-msft
ms.author: karann
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 2fefd9cff4d151111023521c31d58878743775bf
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231175"
---
# <a name="transforming-source-code-and-configuration-files"></a>Trasformazioni di codice sorgente e file di configurazione

Una **trasformazione di codice sorgente** applica una sostituzione dei token unidirezionale ai file nella cartella `content` o `contentFiles` del pacchetto (`content` per i clienti che usano `packages.config` e `contentFiles` per `PackageReference`) quando il pacchetto viene installato, dove i token fanno riferimento alle [proprietà di progetto](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) di Visual Studio. Ciò consente di inserire un file nello spazio dei nomi del progetto o di personalizzare il codice inserito in genere in `global.asax` in un progetto ASP.NET.

Una **trasformazione di file di configurazione** consente di modificare i file già esistenti in un progetto di destinazione, come `web.config` e `app.config`. Ad esempio, potrebbe essere necessario aggiungere un elemento per il pacchetto alla sezione `modules` del file di configurazione. Questa trasformazione viene eseguita includendo nel pacchetto file speciali che descrivono le sezioni da aggiungere ai file di configurazione. Quando si disinstalla un pacchetto, queste stesse modifiche vengono invertite, rendendola una trasformazione bidirezionale.

## <a name="specifying-source-code-transformations"></a>Specifica di trasformazioni di codice sorgente

1. I file da inserire dal pacchetto nel progetto devono trovarsi all'interno delle cartelle `content` e `contentFiles` del pacchetto. Ad esempio, se si vuole che un file denominato `ContosoData.cs` venga installato in una cartella `Models` del progetto di destinazione, deve trovarsi all'interno delle cartelle `content\Models` e `contentFiles\{lang}\{tfm}\Models` nel pacchetto.

1. Per indicare a NuGet di applicare la sostituzione dei token in fase di installazione, aggiungere `.pp` al nome file del codice sorgente. Dopo l'installazione, il file non avrà l'estensione `.pp`.

    Ad esempio, per eseguire trasformazioni in `ContosoData.cs`, denominare il file nel pacchetto `ContosoData.cs.pp`. Dopo l'installazione verrà visualizzato come `ContosoData.cs`.

1. Nel file del codice sorgente usare i token senza distinzione tra maiuscole e minuscole nel formato `$token$` per indicare i valori che NuGet deve sostituire con le proprietà del progetto:

    ```cs
    namespace $rootnamespace$.Models
    {
        public struct CategoryInfo
        {
            public string categoryid;
            public string description;
            public string htmlUrl;
            public string rssUrl;
            public string title;
        }
    }
    ```

    Al momento dell'installazione, NuGet sostituisce `$rootnamespace$` con `Fabrikam` supponendo il progetto di destinazione il cui spazio dei nomi radice è `Fabrikam`.

Il token `$rootnamespace$` è la proprietà del progetto usata più di frequente. Tutte le altre sono elencate nelle [proprietà del progetto](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7). Tenere in considerazione, naturalmente, che alcune proprietà potrebbero essere specifiche del tipo di progetto.

## <a name="specifying-config-file-transformations"></a>Specifica di trasformazioni di file di configurazione

Come descritto nelle sezioni successive, le trasformazioni di file di configurazione possono essere eseguite in due modi:

- Includere i file `app.config.transform` e `web.config.transform` nella cartella `content` del pacchetto, dove l'estensione `.transform` indica a NuGet che questi file contengono il codice XML da unire con i file di configurazione esistenti quando il pacchetto viene installato. Quando si disinstalla un pacchetto, lo stesso codice XML viene rimosso.
- Includere i file `app.config.install.xdt` e `web.config.install.xdt` nella cartella `content` del pacchetto usando la [sintassi XDT](https://msdn.microsoft.com/library/dd465326.aspx) per descrivere le modifiche desiderate. Con questa opzione è anche possibile includere un file `.uninstall.xdt` per ripristinare le modifiche quando il pacchetto viene rimosso da un progetto.

> [!Note]
> Le trasformazioni non vengono applicate ai file `.config` a cui si fa riferimento come collegamento in Visual Studio.

Il vantaggio dell'uso di XDT è dato dal fatto che, invece di unire semplicemente due file statici, fornisce una sintassi per la modifica della struttura di un DOM XML tramite la corrispondenza tra elementi e attributi basata sul supporto XPath completo. XDT può quindi aggiungere, aggiornare o rimuovere elementi, inserire nuovi elementi in una posizione specifica oppure sostituire o rimuovere elementi (inclusi i nodi figlio). Ciò rende molto semplice creare trasformazioni di disinstallazione che annullano tutte le trasformazioni eseguite durante l'installazione del pacchetto.

### <a name="xml-transforms"></a>Trasformazioni XML

`app.config.transform` e `web.config.transform` nella cartella `content` di un pacchetto contengono solo gli elementi da unire nei file `app.config` e `web.config` esistenti del progetto.

Ad esempio, si supponga che il progetto contenga inizialmente il contenuto seguente in `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Per aggiungere un elemento `MyNuModule` alla sezione `modules` durante l'installazione del pacchetto, creare un file `web.config.transform` nella cartella `content` del pacchetto simile al seguente:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Dopo che NuGet ha installato il pacchetto, NuGet `web.config` avrà l'aspetto seguente:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Si noti che NuGet non ha sostituito la sezione `modules`, ha semplicemente unito la nuova voce al suo interno aggiungendo solo i nuovi elementi e attributi. NuGet non modificherà elementi o attributi esistenti.

Quando il pacchetto viene disinstallato, NuGet esaminerà nuovamente i file `.transform` e rimuoverà gli elementi in esso contenuti dai file `.config` appropriati. Si noti che questo processo non avrà effetto sulle righe nel file `.config` modificate dopo l'installazione del pacchetto.

Come esempio più esteso, il pacchetto [Error Logging Modules and Handlers (ELMAH) per ASP.NET](https://www.nuget.org/packages/elmah/) aggiunge molte voci in `web.config`, che vengono nuovamente rimosse quando si disinstalla un pacchetto.

Per esaminare il relativo file `web.config.transform`, scaricare il pacchetto ELMAH dal collegamento precedente, modificare l'estensione del pacchetto da `.nupkg` a `.zip` e quindi aprire `content\web.config.transform` in tale file ZIP.

Per vedere l'effetto dell'installazione e della disinstallazione del pacchetto, creare un nuovo progetto ASP.NET in Visual Studio (il modello è disponibile in **Visual C# > Web** nella finestra di dialogo Nuovo progetto) e selezionare un'applicazione ASP.NET vuota. Aprire `web.config` per visualizzarne lo stato iniziale. Quindi fare clic con il pulsante destro del mouse sul progetto, selezionare **Gestisci pacchetti NuGet**, cercare ELMAH su nuget.org e installare la versione più recente. Notare tutte le modifiche apportate a `web.config`. Disinstallare quindi il pacchetto. `web.config` tornerà allo stato precedente.

### <a name="xdt-transforms"></a>Trasformazioni XDT

> [!Note]
> Come indicato nella [sezione problemi di compatibilità dei pacchetti della documentazione per la migrazione da `packages.config` a `PackageReference`](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), le trasformazioni xdt, come descritto di seguito, sono supportate solo da `packages.config`. Se si aggiungono i file seguenti al pacchetto, i consumer che usano il pacchetto con `PackageReference` non avranno le trasformazioni applicate (fare riferimento a [questo esempio](https://github.com/NuGet/Samples/tree/master/XDTransformExample) per fare in modo che le trasformazioni xdt funzionino con`PackageReference`).

È possibile modificare i file di configurazione usando la [sintassi XDT](https://msdn.microsoft.com/library/dd465326.aspx). È anche possibile fare in modo che NuGet sostituisca i token con le [proprietà del progetto](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) includendo il nome della proprietà all'interno di delimitatori `$` (senza distinzione tra maiuscole e minuscole).

Ad esempio, il file seguente `app.config.install.xdt` inserirà un elemento `appSettings` in `app.config` contenente i valori `FullPath`, `FileName` e `ActiveConfigurationSettings` dal progetto:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <appSettings xdt:Transform="Insert">
        <add key="FullPath" value="$FullPath$" />
        <add key="FileName" value="$filename$" />
        <add key="ActiveConfigurationSettings " value="$ActiveConfigurationSettings$" />
    </appSettings>
</configuration>
```

Per fare un altro esempio, si supponga che il progetto contenga inizialmente il contenuto seguente in `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Per aggiungere un elemento `MyNuModule` alla sezione `modules` durante l'installazione del pacchetto, il file `web.config.install.xdt` del pacchetto dovrebbe contenere il codice seguente:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" xdt:Transform="Insert" />
        </modules>
    </system.webServer>
</configuration>
```

Dopo l'installazione del pacchetto, `web.config` sarà simile al seguente:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Per rimuovere solo l'elemento `MyNuModule` durante la disinstallazione del pacchetto, il file `web.config.uninstall.xdt` dovrebbe contenere il codice seguente:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" xdt:Transform="Remove" xdt:Locator="Match(name)" />
        </modules>
    </system.webServer>
</configuration>
```
