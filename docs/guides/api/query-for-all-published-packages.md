---
title: Query per recuperare tutti i pacchetti pubblicati su nuget.org
description: Tramite l'API NuGet, è possibile eseguire una query per recuperare tutti i pacchetti pubblicati su nuget.org e rimanere aggiornati nel tempo.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 7e611b568538e0acfcbad2e5d986a0f9382ac8fd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774115"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a>Query per recuperare tutti i pacchetti pubblicati su nuget.org

Un modello di query comune sull'API OData V2 legacy prevedeva l'enumerazione di tutti i pacchetti pubblicati su nuget.org, ordinati in base alla data di pubblicazione del pacchetto. Gli scenari che richiedono questo tipo di query su nuget.org variano notevolmente:

- Replica completa di nuget.org
- Individuazione del rilascio di nuove versioni di un pacchetto
- Ricerca di pacchetti che dipendono dal pacchetto in uso

La modalità legacy di esecuzione di questa operazione dipendeva dall'ordinamento dell'entità del pacchetto OData in base a un timestamp e dallo spostamento all'interno del set di risultati di dimensioni elevate usando i parametri `skip` e `top` (dimensioni della pagina). Sfortunatamente, questo approccio presenta alcuni svantaggi:

- Possibilità di pacchetti mancanti, dal momento che le query sono effettuate su dati che spesso cambiano ordine
- Tempi di risposta delle query rallentati, poiché le query non sono ottimizzate (le query più ottimizzate sono quelle che supportano uno scenario principale per il client NuGet ufficiale)
- Uso di API deprecate e non documentate, il che significa che il supporto di tali query in futuro non è garantito
- Impossibilità di riprodurre la cronologia nell'ordine esatto in cui si è verificata

Per questo motivo, è possibile fare riferimento alla guida seguente per gestire gli scenari menzionati in precedenza in modo più affidabile e valido sia oggi che in futuro.

## <a name="overview"></a>Panoramica

Al centro di questa guida si trova una risorsa dell'[API NuGet](../../api/overview.md) chiamata **catalogo**. Il catalogo è un'API di sola aggiunta che consente al chiamante di visualizzare una cronologia completa dei pacchetti aggiunti, modificati ed eliminati da nuget.org. Se si è interessati a tutti o anche a un subset di pacchetti pubblicati in nuget.org, il catalogo è un ottimo modo per rimanere sempre aggiornati con il set di pacchetti attualmente disponibili.

Questa guida è da intendersi come una presentazione generale, ma se si è interessati a informazioni più dettagliate sul catalogo, vedere il relativo [documento di riferimento per l'API](../../api/catalog-resource.md).

I passaggi seguenti possono essere implementati in qualsiasi linguaggio di programmazione scelto. Se si vuole un esempio completo in esecuzione, prendere in considerazione l'[esempio in C#](#c-sample-code) menzionato di seguito.

In caso contrario, attenersi alla guida seguente per creare un lettore del catalogo affidabile.

## <a name="initialize-a-cursor"></a>Inizializzare un cursore

Il primo passaggio per la creazione di un lettore del catalogo affidabile consiste nell'implementazione di un cursore. Per i dettagli completi sulla progettazione di un cursore del catalogo, vedere il [documento di riferimento per il catalogo](../../api/catalog-resource.md#cursor). In breve, il cursore è un punto nel tempo fino al quale sono stati elaborati gli eventi nel catalogo. Gli eventi nel catalogo rappresentano le pubblicazioni dei pacchetti e altre modifiche dei pacchetti. Se si è interessati a tutti i pacchetti pubblicati in NuGet fin dall'inizio, è necessario inizializzare il cursore su un timestamp di "valore minimo" (ad esempio `DateTime.MinValue` in .NET). Se si è interessati solo ai pacchetti pubblicati a partire dalla data odierna, è possibile usare il timestamp corrente come valore del cursore iniziale.

In questa guida il cursore sarà inizializzato su un timestamp risalente a un'ora prima. Per il momento, il timestamp verrà semplicemente salvato in memoria.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>Determinare l'URL dell'indice del catalogo

Il percorso di ogni risorsa (endpoint) nell'API NuGet deve essere individuato tramite l'[indice del servizio](../../api/service-index.md). Poiché questa guida è incentrata su nuget.org, verrà usato l'indice del servizio di nuget.org.

```
GET https://api.nuget.org/v3/index.json
```

Il documento di servizio è un documento JSON contenente tutte le risorse in nuget.org. Cercare la risorsa con il `@type` valore della proprietà `Catalog/3.0.0` . Il valore della proprietà `@id` associato è l'URL per l'indice del catalogo stesso. 

## <a name="find-new-catalog-leaves"></a>Trovare nuovi elementi foglia del catalogo

Usando il valore della proprietà `@id` individuato nel passaggio precedente, scaricare l'indice del catalogo:

```
GET https://api.nuget.org/v3/catalog0/index.json
```

Deserializzare l'[indice del catalogo](../../api/catalog-resource.md#catalog-index). Applicare un filtro per escludere tutti gli [oggetti della pagina del catalogo](../../api/catalog-resource.md#catalog-page-object-in-the-index) con `commitTimeStamp` minore o uguale al valore del cursore corrente.

Per ogni pagina del catalogo rimanente, scaricare il documento completo usando la proprietà `@id`.

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

Deserializzare la [pagina del catalogo](../../api/catalog-resource.md#catalog-page). Applicare un filtro per escludere tutti gli [oggetti foglia del catalogo](../../api/catalog-resource.md#catalog-item-object-in-a-page) con `commitTimeStamp` minore o uguale al valore del cursore corrente.

Dopo avere scaricato tutte le pagine di catalogo non escluse tramite l'applicazione del filtro, è disponibile un set di oggetti foglia del catalogo che rappresentano i pacchetti che sono stati pubblicati, rimossi, elencati o eliminati nel periodo di tempo trascorso tra il timestamp del cursore e il momento attuale.

## <a name="process-catalog-leaves"></a>Elaborare gli elementi foglia del catalogo

A questo punto, è possibile eseguire qualsiasi operazione di elaborazione personalizzata sugli elementi del catalogo. Se si ha bisogno dell'ID e della versione del pacchetto, è possibile esaminare le proprietà `nuget:id` e `nuget:version` degli oggetti elemento del catalogo trovati nelle pagine. Assicurarsi di esaminare la proprietà `@type` per sapere se l'elemento del catalogo riguarda un pacchetto esistente o un pacchetto eliminato.

Se si è interessati ai metadati sul pacchetto (come la descrizione, le dipendenze, le dimensioni del pacchetto .nupkg e così via), è possibile recuperare il [documento foglia del catalogo](../../api/catalog-resource.md#catalog-leaf) usando la proprietà `@id`.

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

Questo documento contiene tutti i metadati inclusi nella [risorsa dei metadati del pacchetto](../../api/registration-base-url-resource.md) e molto altro.

Questo è il passaggio in cui viene implementata la logica personalizzata. Gli altri passaggi in questa guida vengono implementati all'incirca in modo analogo, indipendentemente dalle operazioni eseguite sugli elementi foglia del catalogo.

### <a name="downloading-the-nupkg"></a>Download del pacchetto .nupkg

Se si è interessati al download del pacchetto .nupkg per i pacchetti individuati nel catalogo, è possibile usare la [risorsa di contenuto del pacchetto](../../api/package-base-address-resource.md). Tuttavia, si noti che sussiste un breve ritardo tra quando viene rilevato un pacchetto nel catalogo e quando è disponibile nella risorsa di contenuto del pacchetto. Pertanto, se si verifica l'errore `404 Not Found` mentre si tenta di scaricare un pacchetto .nupkg per un pacchetto rilevato nel catalogo, è sufficiente ripetere il tentativo in un secondo momento. La correzione di questo ritardo è registrata nel problema GitHub [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).

## <a name="move-the-cursor-forward"></a>Spostare in avanti il cursore

Dopo avere elaborato correttamente gli elementi del catalogo, è necessario determinare il nuovo valore del cursore da salvare. A tale scopo, trovare il valore `commitTimeStamp` massimo (il più recente in ordine cronologico) di tutti gli elementi del catalogo elaborati. Questo è il nuovo valore del cursore. Salvarlo in una risorsa di archiviazione permanente, come un database, un file system o un archivio BLOB. Se si vogliono ottenere altri elementi del catalogo, partire semplicemente dal [primo passaggio](#initialize-a-cursor) inizializzando il valore del cursore da questo archivio permanente.

Se l'applicazione genera errori o un'eccezione, non spostare in avanti il cursore. Spostare in avanti il cursore significa che non è più necessario elaborare gli elementi del catalogo prima del cursore.

Se per qualche motivo è presente un bug nella modalità di elaborazione degli elementi figlio del catalogo, è possibile semplicemente spostare il cursore indietro nel tempo e consentire al codice di rielaborare gli elementi del catalogo precedenti.

## <a name="c-sample-code"></a>Codice di esempio C#

Poiché il catalogo è un set di documenti JSON disponibili tramite HTTP, è possibile interagire con esso tramite qualsiasi linguaggio di programmazione che disponga di un client HTTP e di un deserializzatore JSON.

Gli esempi in C# sono disponibili nel [repository NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>SDK del catalogo

Il modo più semplice per usare il catalogo consiste nell'usare il pacchetto SDK del catalogo .NET in versione non definitiva `NuGet.Protocol.Catalog` , disponibile in Azure Artifacts usando l'URL di origine del pacchetto NuGet seguente: `https://pkgs.dev.azure.com/dnceng/public/_packaging/nuget-build/nuget/v3/index.json` .

È possibile installare questo pacchetto in un progetto compatibile con `netstandard1.3` o versione successiva, come NET Framework 4.6.

Un esempio che usa questo pacchetto è disponibile su GitHub nel [progetto NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).

#### <a name="sample-output"></a>Output di esempio

```output
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a>Esempio minimo

Per un esempio con un numero minore di dipendenze che illustra l'interazione con il catalogo in maggiore dettaglio, vedere il [progetto di esempio CatalogReaderExample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample). Il progetto ha come destinazione `netcoreapp2.0` e dipende da [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (per la risoluzione dell'indice del servizio) e da [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (per la deserializzazione JSON).

La logica principale del codice è visibile nel [file Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).

#### <a name="sample-output"></a>Output di esempio

```output
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
