---
title: Risorsa di catalogo, API NuGet V3
description: Il catalogo è un indice di tutti i pacchetti create ed eliminate in nuget.org.
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d4c13200494ed3c6fa897ce0083a52c13688b44b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547393"
---
# <a name="catalog"></a>Catalog

Il **catalogo** è una risorsa in cui vengono registrate tutte le operazioni di pacchetto in un'origine di pacchetto, ad esempio creazioni e delle eliminazioni. La risorsa di catalogo contiene il `Catalog` digitare il [indice del servizio](service-index.md).

> [!Note]
> Poiché il catalogo non viene usato dal client NuGet ufficiale, non tutte le origini pacchetto implementano il catalogo.

> [!Note]
> Il catalogo di nuget.org non è attualmente disponibile in Cina. Per altre informazioni, vedere [NuGet/NuGetGallery & 4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Controllo delle versioni

Nell'esempio `@type` valore viene usato:

Valore di @type   | Note
------------- | -----
Catalog/3.0.0 | La versione iniziale

## <a name="base-url"></a>URL di base

URL del punto di ingresso per le API seguenti è il valore della `@id` proprietà associato alla risorsa menzionati in precedenza `@type` valori. In questo argomento Usa l'URL segnaposto `{@id}`.

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL disponibili il supporto di risorsa catalogo solo i metodi HTTP `GET` e `HEAD`.

## <a name="catalog-index"></a>Indice del catalogo

L'indice del catalogo è un documento in un percorso noto contenente un elenco di elementi di catalogo, ordinati in ordine cronologico. È il punto di ingresso della risorsa di catalogo.

L'indice è costituito da pagine di catalogo. Ogni pagina del catalogo contiene gli elementi del catalogo. Ogni elemento del catalogo rappresenta un evento relativi a un singolo pacchetto in un punto nel tempo. Un elemento del catalogo può rappresentare un pacchetto che è stato creato, non in elenco, rimesse in vendita o eliminata dall'origine del pacchetto. Elaborando gli elementi del catalogo in ordine cronologico, il client può generare una panoramica aggiornata di ogni pacchetto che esiste nell'origine pacchetto V3.

In breve, i BLOB catalogo hanno la struttura gerarchica seguente:

- **Indice**: il punto di ingresso per il catalogo.
- **Pagina**: un raggruppamento di elementi del catalogo.
- **Foglia**: un documento che rappresenta un elemento del catalogo, che è uno snapshot dello stato di un singolo pacchetto.

Ogni oggetto catalogo include una proprietà denominata la `commitTimeStamp` che rappresenta quando l'elemento è stato aggiunto al catalogo. Gli elementi del catalogo vengono aggiunti a una pagina del catalogo in batch denominati commit. Tutti gli elementi di catalogo nella stesso commit è lo stesso timestamp di commit (`commitTimeStamp`) e ID commit (`commitId`). Gli elementi del catalogo in modalità di commit della stessa rappresentano gli eventi che si sono verificati quasi lo stesso punto nel tempo sull'origine del pacchetto. Vi è alcun ordine all'interno di un commit di catalogo.

Poiché ogni ID di pacchetto e la versione è univoco, non sarà mai più di un elemento del catalogo in un commit. Ciò garantisce che sempre gli elementi del catalogo per un singolo pacchetto possono essere ordinati in modo non ambiguo rispetto al timestamp di commit.

Si è mai possibile più di un commit nel catalogo per `commitTimeStamp`. In altre parole, il `commitId` ridondante con la `commitTimeStamp`.

A differenza di [risorsa dei metadati del pacchetto](registration-base-url-resource.md), che vengono indicizzati per ID pacchetto, il catalogo è indicizzata (e queryable) solo dal tempo.

Gli elementi del catalogo vengono sempre aggiunti al catalogo in un ordine cronologico, a incremento progressivo costante. Ciò significa che se un commit catalogo viene aggiunto all'ora X quindi alcun commit catalogo non verrà mai aggiunto con un tempo inferiore o uguale a X.

La richiesta seguente recupera l'indice del catalogo.

    GET {@id}

L'indice del catalogo è un documento JSON che contiene un oggetto con le proprietà seguenti:

nome            | Tipo             | Obbligatorio | Note
--------------- | ---------------- | -------- | -----
commitId        | stringa           | sì      | Un ID univoco associato al commit più recente
commitTimeStamp | stringa           | sì      | Un timestamp del commit più recente
count           | numero intero          | sì      | Il numero di pagine nell'indice
elementi           | Matrice di oggetti | sì      | Una matrice di oggetti, ogni oggetto che rappresenta una pagina

Ogni elemento di `items` matrice è un oggetto con alcuni dettagli minimi sugli ogni pagina. Questi oggetti della pagina non contengono foglia del catalogo (elementi). L'ordine degli elementi in questa matrice non è definito. Le pagine possono essere ordinate dal client in memoria con relativi `commitTimeStamp` proprietà.

Come vengono introdotte nuove pagine, il `count` verrà incrementato e nuovi oggetti verranno visualizzato nei `items` matrice.

Man mano che gli elementi vengono aggiunti al catalogo, l'indice `commitId` cambierà e `commitTimeStamp` aumenterà. Queste due proprietà che sono essenzialmente un riepilogo su pagina di tutti i `commitId` e `commitTimeStamp` i valori di `items` matrice.

### <a name="catalog-page-object-in-the-index"></a>Oggetto pagina in corrispondenza dell'indice del catalogo

Gli oggetti della pagina del catalogo trovati dell'indice del catalogo `items` proprietà hanno le proprietà seguenti:

nome            | Tipo    | Obbligatorio | Note
--------------- | ------- | -------- | -----
@id             | stringa  | sì      | L'URL al recupero di una pagina del catalogo
commitId        | stringa  | sì      | Un ID univoco associato con il commit più recente in questa pagina
commitTimeStamp | stringa  | sì      | Un timestamp del commit più recente in questa pagina
count           | numero intero | sì      | Il numero di elementi nella pagina catalogo

A differenza di [risorsa dei metadati del pacchetto](registration-base-url-resource.md) che in alcuni casi inlines lascia nell'indice, elementi foglia del catalogo non è mai resa inline in corrispondenza dell'indice e deve sempre essere recuperato tramite la pagina `@id` URL.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Pagina del catalogo

La pagina del catalogo è una raccolta di elementi del catalogo. Si tratta di un documento recuperato usando uno del `@id` i valori disponibili nell'indice del catalogo. L'URL a una pagina del catalogo non può essere prevedibile e deve essere individuata utilizzando solo l'indice del catalogo.

Nella pagina dell'indice del catalogo solo con il timestamp di commit più elevato o in una nuova pagina, vengono aggiunti nuovi elementi di catalogo. Dopo avere aggiunto una pagina con un timestamp di commit superiore nel catalogo, pagine meno recenti vengono mai aggiunti o modificate.

Documento di pagina del catalogo è un oggetto JSON con le proprietà seguenti:

nome            | Tipo             | Obbligatorio | Note
--------------- | ---------------- | -------- | -----
commitId        | stringa           | sì      | Un ID univoco associato con il commit più recente in questa pagina
commitTimeStamp | stringa           | sì      | Un timestamp del commit più recente in questa pagina
count           | numero intero          | sì      | Il numero di elementi nella pagina
elementi           | Matrice di oggetti | sì      | Gli elementi del catalogo in questa pagina
Elemento padre          | stringa           | sì      | Un URL per l'indice del catalogo

Ogni elemento di `items` matrice è un oggetto con alcuni dettagli minimi sull'elemento del catalogo. Questi oggetti elemento non contengono tutti i dati dell'elemento del catalogo. L'ordine degli elementi della pagina `items` matrice non è definita. Gli elementi possono essere ordinati dal client in memoria con relativi `commitTimeStamp` proprietà.

Il numero di elementi del catalogo in una pagina viene definito dall'implementazione del server. Per nuget.org, sono disponibili al massimo 550 elementi in ogni pagina, anche se il numero effettivo potrebbe essere più piccolo per alcune pagine a seconda delle dimensioni del batch di commit successivo in corrispondenza del punto nel tempo.

Quando vengono introdotti nuovi elementi, il `count` viene incrementato e nuovo catalogo elemento oggetti vengono visualizzati nei `items` matrice.

Quando vengono aggiunti elementi alla pagina, il `commitId` modifiche e `commitTimeStamp` aumenta. Queste due proprietà che sono essenzialmente un riepilogo su tutti `commitId` e `commitTimeStamp` i valori di `items` matrice.

### <a name="catalog-item-object-in-a-page"></a>Oggetto di elemento in una pagina del catalogo

Gli oggetti elemento del catalogo trovati nella pagina del catalogo `items` proprietà hanno le proprietà seguenti:

nome            | Tipo    | Obbligatorio | Note
--------------- | ------- | -------- | -----
@id             | stringa  | sì      | L'URL per recuperare l'elemento del catalogo
@type           | stringa  | sì      | Il tipo dell'elemento del catalogo
commitId        | stringa  | sì      | L'ID commit associato a questo elemento del catalogo
commitTimeStamp | stringa  | sì      | Il timestamp di commit di questo elemento del catalogo
NuGet:ID        | stringa  | sì      | L'ID del pacchetto che è correlato questo foglia
NuGet:Version   | stringa  | sì      | La versione del pacchetto che è correlato questo foglia

Il `@type` valore sarà uno dei due valori seguenti:

1. `nuget:PackageDetails`: corrisponde al `PackageDetails` tipo nel documento foglia del catalogo.
1. `nuget:PackageDelete`: corrisponde al `PackageDelete` tipo nel documento foglia del catalogo.

Per altre informazioni sulle implicazioni di ogni tipo, vedere la [corrispondenti elementi di tipo](#item-types) sotto.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Foglia del catalogo

La foglia del catalogo contiene i metadati relativi a un ID di pacchetto specifico e una versione a un certo punto nel tempo. Si tratta di un documento recuperato tramite il `@id` valore trovato in una pagina del catalogo. L'URL a un nodo foglia del catalogo non può essere prevedibile e deve essere individuato tramite una pagina di un catalogo.

Il documento foglia del catalogo è un oggetto JSON con le proprietà seguenti:

nome                    | Tipo                       | Obbligatorio | Note
----------------------- | -------------------------- | -------- | -----
@type                   | stringa o matrice di stringhe | sì      | I tipi di elemento del catalogo
catalog:commitId        | stringa                     | sì      | Un ID commit associato a questo elemento del catalogo
catalog:commitTimeStamp | stringa                     | sì      | Il timestamp di commit di questo elemento del catalogo
ID                      | stringa                     | sì      | L'ID del pacchetto dell'elemento del catalogo
Pubblicato               | stringa                     | sì      | La data di pubblicazione dell'elemento del catalogo pacchetti
version                 | stringa                     | sì      | La versione del pacchetto dell'elemento del catalogo

### <a name="item-types"></a>Tipi di elemento

Il `@type` proprietà è una stringa o matrice di stringhe. Per praticità, se il `@type` valore è una stringa, deve essere considerato tra tutte le matrici di dimensioni. Non tutti i valori possibili per `@type` sono documentati. Tuttavia, ogni elemento del catalogo ha esattamente uno dei due valori di tipo stringa seguenti:

1. `PackageDetails`: rappresenta uno snapshot dei metadati del pacchetto
1. `PackageDelete`: rappresenta un pacchetto che è stato eliminato

### <a name="package-details-catalog-items"></a>Dettagli del pacchetto di elementi di catalogo

Elementi con il tipo di catalogo `PackageDetails` contengono uno snapshot dei metadati del pacchetto per un pacchetto specifico (combinazione di ID e versione). Un elemento del catalogo dei dettagli del pacchetto viene generato quando un'origine pacchetto rileva uno qualsiasi dei seguenti scenari:

1. È un pacchetto **push**.
1. È un pacchetto **elencati**.
1. È un pacchetto **rimossa dall'elenco**.
1. È un pacchetto **ridisposto**.

Adattamento dinamico di un pacchetto è un movimento di amministrazione che essenzialmente genera un falso push di un pacchetto esistente senza modifiche al pacchetto stesso. In nuget.org, dopo avere corretto un bug in uno dei processi in background che usano il catalogo viene usato un adattamento dinamico.

I client utilizzano gli elementi del catalogo non tentare di determinare quale di questi scenari l'elemento del catalogo di prodotti. Al contrario, il client deve semplicemente aggiornare qualsiasi indice o una visualizzazione gestita con i metadati contenuti nell'elemento del catalogo. Inoltre, gli elementi del catalogo duplicati o con ridondanza devono essere gestiti normalmente (in modo idempotente).

Gli elementi del catalogo dei dettagli del pacchetto hanno le proprietà seguenti oltre a quelli [incluso in tutti gli elementi foglia del catalogo](#catalog-leaf).

nome                    | Tipo                       | Obbligatorio | Note
----------------------- | -------------------------- | -------- | -----
authors                 | stringa                     | No       |
created                 | stringa                     | No       | Timestamp di quando è stato creato il pacchetto. Proprietà di fallback: `published`.
dependencyGroups        | Matrice di oggetti           | No       | Stesso formato del [risorsa dei metadati del pacchetto](registration-base-url-resource.md#package-dependency-group)
Descrizione             | stringa                     | No       |
iconUrl                 | stringa                     | No       |
isPrerelease            | boolean                    | No       | La versione del pacchetto è o meno versione non definitiva. Possono essere rilevati da `version`.
language                | stringa                     | No       |
licenseUrl              | stringa                     | No       |
disponibili                  | boolean                    | No       | Se il pacchetto è elencato
minClientVersion        | stringa                     | No       |
packageHash             | stringa                     | sì      | L'hash del pacchetto, la codifica mediante [Base64 standard](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | stringa                     | sì      |
packageSize             | numero intero                    | sì      | Le dimensioni del pacchetto. nupkg pacchetto in byte
projectUrl              | stringa                     | No       |
releaseNotes            | stringa                     | No       |
requireLicenseAgreement | boolean                    | No       | Si supponga `false` se escluso
summary                 | stringa                     | No       |
tag                    | Matrice di stringhe           | No       |
title                   | stringa                     | No       |
verbatimVersion         | stringa                     | No       | La stringa di versione perché si trova in origine nel file con estensione nuspec

Il pacchetto `version` proprietà è la stringa di versione completo, normalizzato. Ciò significa che i dati di compilazione di SemVer 2.0.0 possono essere inclusi di seguito.

Il `created` timestamp è quando il pacchetto prima di tutto è stato ricevuto dall'origine del pacchetto, in genere un breve periodo di tempo prima di timestamp di commit dell'elemento del catalogo.

Il `packageHashAlgorithm` è una stringa definita dall'implementazione del server che rappresenta l'algoritmo hash usato per produrre il `packageHash`. NuGet.org sempre usato il `packageHashAlgorithm` pari a `SHA512`.

Il `published` timestamp è ora quando il pacchetto è stato ultima indicato.

> [!Note]
> In nuget.org, il `published` valore è impostato per l'anno 1900 quando il pacchetto è incluso nell'elenco.

#### <a name="sample-request"></a>Richiesta di esempio

OTTIENI https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Elementi del catalogo di eliminazione pacchetto

Elementi con il tipo di catalogo `PackageDelete` contengono un set minimo di informazioni che indicano ai client di catalogo che un pacchetto è stato eliminato dall'origine del pacchetto e non è più disponibile per qualsiasi operazione di pacchetto (ad esempio, ripristino).

> [!Note]
> È possibile che un pacchetto da eliminare e ripubblicate in un secondo momento usando lo stesso ID di pacchetto e di una versione. In nuget.org, questo è un caso molto raro come interrompe presupposto del client ufficiali che un ID del pacchetto e versione implica il contenuto di un pacchetto specifico. Per altre informazioni sull'eliminazione di pacchetti in nuget.org, vedere [nostri criteri](../policies/deleting-packages.md).

Gli elementi del catalogo di eliminazione pacchetto non sono proprietà aggiuntive oltre a quelli [incluso in tutti gli elementi foglia del catalogo](#catalog-leaf).

Il `version` proprietà corrisponde alla stringa di versione originale trovata nel file con estensione nuspec pacchetto.

Il `published` proprietà indica il tempo quando pacchetto è stato eliminato, ovvero in genere come breve periodo di tempo prima di timestamp di commit dell'elemento del catalogo.

#### <a name="sample-request"></a>Richiesta di esempio

OTTIENI https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Cursore

### <a name="overview"></a>Panoramica

In questa sezione viene descritto un concetto di client che, anche se non è necessariamente obbligatoria per il protocollo, deve far parte di qualsiasi implementazione di client catalogo pratiche.

Poiché il catalogo è una struttura di dati di solo accodamento indicizzata dal tempo, il client deve memorizzare un **cursore** in locale, che rappresenta al massimo il punto temporizzato nel client ha elaborato gli elementi del catalogo. Si noti che questo valore del cursore non deve essere generato mai tramite clock del computer del client. Al contrario, il valore deve provenire da un oggetto di catalogo `commitTimestamp` valore.

Ogni volta che il client vuole elaborare nuovi eventi sull'origine del pacchetto, è necessario solo query del catalogo per tutti gli elementi di catalogo con un timestamp di commit maggiore relativo cursore stored. Dopo che il client ha elaborato correttamente tutti i nuovi elementi del catalogo, registra il timestamp di commit più recente degli elementi del catalogo elaborati solo come il nuovo valore del cursore.

Con questo approccio, il client può essere assicurarsi di non perdere gli eventi del pacchetto che si è verificato l'origine del pacchetto.
Inoltre, il client non ha mai rielaborare vecchi eventi prima del timestamp di commit registrate del cursore.

Questo concetto avanzato dei cursori viene usato per molti dei processi in background di nuget.org e viene usato per mantenere aggiornato l'API V3 stessa. 

### <a name="initial-value"></a>Valore iniziale

Quando il client di catalogo avvio per la prima volta (e pertanto non ha alcun valore del cursore), valore predefinito è cursore deve utilizzare. Di NET `System.DateTimeOffset.MinValue` o tali analoga cenno a timestamp minimo rappresentabile.

### <a name="iterating-over-catalog-items"></a>Scorrere gli elementi del catalogo

Per eseguire una query per il set successivo di elementi del catalogo per l'elaborazione, il client deve:

1. Recuperare il valore del cursore registrato da un archivio locale.
1. Scaricare e deserializzare l'indice del catalogo.
1. Trova tutte le pagine con un timestamp di commit del catalogo *maggiore* il cursore.
1. Dichiarare un elenco vuoto di elementi di catalogo da elaborare.
1. Per ogni pagina catalogo corrispondente nel passaggio 3:
   1. Scaricare e deserializzare la pagina del catalogo.
   1. Trova tutti gli elementi con un timestamp di commit del catalogo *maggiore* il cursore.
   1. Aggiungere tutti gli elementi di catalogo corrispondente all'elenco dichiarato nel passaggio 4.
1. Per ordinare l'elenco di elementi di catalogo timestamp di commit.
1. Elaborare ogni elemento del catalogo in sequenza:
   1. Scaricare e deserializzare l'elemento del catalogo.
   1. Rispondere in modo appropriato al tipo dell'elemento del catalogo.
   1. Elaborare il documento di elemento del catalogo in modalità specifiche del client.
1. Registrare il timestamp di commit dell'ultimo elemento di catalogo come il nuovo valore del cursore.

Con questo algoritmo di base, l'implementazione client può creare una visualizzazione completa di tutti i pacchetti disponibili nell'origine pacchetto. Il client debba essere eseguiti solo questo algoritmo periodicamente per essere sempre informati delle modifiche più recenti per l'origine del pacchetto.

> [!Note]
> Questo è l'algoritmo usato da tale nuget.org per mantenere la [i metadati del pacchetto](registration-base-url-resource.md), [il contenuto del pacchetto](package-base-address-resource.md), [ricerca](search-query-service-resource.md) e [Autocomplete](search-autocomplete-service-resource.md) risorse aggiornate.

### <a name="dependent-cursors"></a>Cursori dipendenti

Si supponga che sono presenti due client di catalogo che presentano una dipendenza inerente dove output del client dipende output del client. 

#### <a name="example"></a>Esempio

Ad esempio, in nuget.org un pacchetto pubblicato di recente non deve essere visualizzati nella risorsa di ricerca prima che venga visualizzata nella risorsa dei metadati del pacchetto. Questo avviene perché l'operazione di "ripristino" eseguita dal client NuGet ufficiale Usa la risorsa dei metadati del pacchetto. Se un cliente consente di individuare un pacchetto con il servizio di ricerca, si deve essere in grado di ripristinare il pacchetto usando la risorsa dei metadati del pacchetto. In altre parole, la risorsa di ricerca dipende dalla risorsa dei metadati del pacchetto. Ogni risorsa dispone di un processo in background di client catalogo l'aggiornamento di tale risorsa. Ogni client ha un proprio cursore.

Poiché entrambe le risorse vengono create all'esterno del catalogo, il cursore del client di catalogo che aggiorna la risorsa di ricerca *non devono andare oltre* il cursore del client di catalogo di metadati del pacchetto.

#### <a name="algorithm"></a>Algoritmo

Per implementare questa limitazione, è sufficiente modificare l'algoritmo precedente per essere:

1. Recuperare il valore del cursore registrato da un archivio locale.
1. Scaricare e deserializzare l'indice del catalogo.
1. Trova tutte le pagine con un timestamp di commit del catalogo *maggiore* cursore **minore o uguale al cursore della dipendenza.**
1. Dichiarare un elenco vuoto di elementi di catalogo da elaborare.
1. Per ogni pagina catalogo corrispondente nel passaggio 3:
   1. Scaricare e deserializzare la pagina del catalogo.
   1. Trova tutti gli elementi con un timestamp di commit del catalogo *maggiore* cursore **minore o uguale al cursore della dipendenza.**
   1. Aggiungere tutti gli elementi di catalogo corrispondente all'elenco dichiarato nel passaggio 4.
1. Per ordinare l'elenco di elementi di catalogo timestamp di commit.
1. Elaborare ogni elemento del catalogo in sequenza:
   1. Scaricare e deserializzare l'elemento del catalogo.
   1. Rispondere in modo appropriato al tipo dell'elemento del catalogo.
   1. Elaborare il documento di elemento del catalogo in modalità specifiche del client.
1. Registrare il timestamp di commit dell'ultimo elemento di catalogo come il nuovo valore del cursore.

Utilizza questo algoritmo modificato, è possibile compilare un sistema del catalogo dipendenti client di produzione di tutti i propri indici specifici, gli elementi e così via.
