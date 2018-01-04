---
title: Trasformazioni di codice sorgente e file di configurazione per i pacchetti NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 20991d69-9e2e-4881-bbf2-96ae634e1872
description: "Informazioni dettagliate sulla capacità per i pacchetti NuGet di trasformare il codice sorgente e i file di configurazione (XML) durante l'installazione."
keywords: Installazione del pacchetto NuGet, trasformazioni del pacchetto NuGet, modifica dei file di configurazione, modifica del codice sorgente
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 7d380b7f2ff52ec39a2ac9a2b939ee51db6054f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="transforming-source-code-and-configuration-files"></a>Trasformazioni di codice sorgente e file di configurazione

Per i progetti che usano `packages.config` o `project.json`, NuGet supporta la capacità di eseguire trasformazioni del codice sorgente e dei file di configurazione in fase di installazione e disinstallazione dei pacchetti.

> [!Note]
> Le trasformazioni di codice sorgente e file di configurazione non vengono applicate quando un pacchetto viene installato in un progetto tramite [riferimenti ai pacchetti nei file di progetto](../Consume-Packages/Package-References-in-Project-Files.md). 

Una **trasformazione di codice sorgente** applica una sostituzione dei token unidirezionale ai file nella cartella `content` del pacchetto quando il pacchetto viene installato, dove i token fanno riferimento alle [proprietà di progetto](https://msdn.microsoft.com/library/vslangproj.projectproperties_properties.aspx) di Visual Studio. Ciò consente di inserire un file nello spazio dei nomi del progetto o di personalizzare il codice inserito in genere in `global.asax` in un progetto ASP.NET.

Una **trasformazione di file di configurazione** consente di modificare i file già esistenti in un progetto di destinazione, come `web.config` e `app.config`. Ad esempio, potrebbe essere necessario aggiungere un elemento per il pacchetto alla sezione `modules` del file di configurazione. Questa trasformazione viene eseguita includendo nel pacchetto file speciali che descrivono le sezioni da aggiungere ai file di configurazione. Quando si disinstalla un pacchetto, queste stesse modifiche vengono invertite, rendendola una trasformazione bidirezionale.


## <a name="specifying-source-code-transformations"></a>Specifica di trasformazioni di codice sorgente

1. I file da inserire dal pacchetto nel progetto devono trovarsi all'interno della cartella `content` del pacchetto. Ad esempio, se si vuole che un file denominato `ContosoData.cs` venga installato in una cartella `Models` del progetto di destinazione, deve trovarsi all'interno della cartella `content\Models` nel pacchetto.

2. Per indicare a NuGet di applicare la sostituzione dei token in fase di installazione, aggiungere `.pp` al nome file del codice sorgente. Dopo l'installazione, il file non avrà l'estensione `.pp`.

    Ad esempio, per eseguire trasformazioni in `ContosoData.cs`, denominare il file nel pacchetto `ContosoData.cs.pp`. Dopo l'installazione verrà visualizzato come `ContosoData.cs`.

3. Nel file del codice sorgente usare i token senza distinzione tra maiuscole e minuscole nel formato `$token$` per indicare i valori che NuGet deve sostituire con le proprietà del progetto:

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

Il token `$rootnamespace$` è la proprietà del progetto usata più di frequente; tutti gli altri sono elencati nella documentazione delle [proprietà ProjectProperties](https://msdn.microsoft.com/library/vslangproj.projectproperties_properties.aspx) su MSDN. Tenere in considerazione, naturalmente, che alcune proprietà potrebbero essere specifiche del tipo di progetto.


## <a name="specifying-config-file-transformations"></a>Specifica di trasformazioni di file di configurazione

Come descritto nelle sezioni successive, le trasformazioni di file di configurazione possono essere eseguite in due modi:

- Includere i file `app.config.transform` e `web.config.transform` nella cartella `content` del pacchetto, dove l'estensione `.transform` indica a NuGet che questi file contengono il codice XML da unire con i file di configurazione esistenti quando il pacchetto viene installato. Quando si disinstalla un pacchetto, lo stesso codice XML viene rimosso.
- (NuGet 2.6 e versioni successive) Includere i file `app.config.install.xdt` e `web.config.install.xdt` nella cartella `content` del pacchetto usando la [sintassi XDT](https://msdn.microsoft.com/library/dd465326.aspx) per descrivere le modifiche desiderate. Con questa opzione è anche possibile includere un file `.uninstall.xdt` per ripristinare le modifiche quando il pacchetto viene rimosso da un progetto.

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
    <system.webServer>
</configuration>
```

Per aggiungere un elemento `MyNuModule` alla sezione `modules` durante l'installazione del pacchetto, creare un file `web.config.transform` nella cartella `content` del pacchetto simile al seguente:

    
```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
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
    <system.webServer>
</configuration>
```

Si noti che NuGet non ha sostituito la sezione `modules`, ha semplicemente unito la nuova voce al suo interno aggiungendo solo i nuovi elementi e attributi. NuGet non modificherà elementi o attributi esistenti.

Quando il pacchetto viene disinstallato, NuGet esaminerà nuovamente i file `.transform` e rimuoverà gli elementi in esso contenuti dai file `.config` appropriati. Si noti che questo processo non avrà effetto sulle righe nel file `.config` modificate dopo l'installazione del pacchetto.

Come esempio più esteso, il pacchetto [Error Logging Modules and Handlers (ELMAH) per ASP.NET](https://www.nuget.org/packages/elmah/) aggiunge molte voci in `web.config`, che vengono nuovamente rimosse quando si disinstalla un pacchetto.

Per esaminare il relativo file `web.config.transform`, scaricare il pacchetto ELMAH dal collegamento precedente, modificare l'estensione del pacchetto da `.nupkg` a `.zip` e quindi aprire `content\web.config.transform` in tale file ZIP.

Per vedere l'effetto dell'installazione e della disinstallazione del pacchetto, creare un nuovo progetto ASP.NET in Visual Studio (il modello è disponibile in **Visual C# > Web** nella finestra di dialogo Nuovo progetto) e selezionare un'applicazione ASP.NET vuota. Aprire `web.config` per visualizzarne lo stato iniziale. Quindi fare clic con il pulsante destro del mouse sul progetto, selezionare **Gestisci pacchetti NuGet**, cercare ELMAH su nuget.org e installare la versione più recente. Notare tutte le modifiche apportate a `web.config`. Disinstallare quindi il pacchetto. `web.config` tornerà allo stato precedente.


### <a name="xdt-transforms"></a>Trasformazioni XDT

Con NuGet 2.6 e versioni successive, è possibile modificare i file di configurazione usando la [sintassi XDT](https://msdn.microsoft.com/library/dd465326.aspx). È anche possibile fare in modo che NuGet sostituisca i token con le [proprietà del progetto](https://msdn.microsoft.com/library/vslangproj.projectproperties_properties.aspx) includendo il nome della proprietà all'interno di delimitatori `$` (senza distinzione tra maiuscole e minuscole).

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
    <system.webServer>
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
    <system.webServer>
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
