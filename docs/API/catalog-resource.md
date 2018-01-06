---
title: Catalogo, API NuGet V3 | Documenti Microsoft
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/30/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: cfd338b5-6253-48c0-88ba-17c6b98fc935
description: "Il catalogo è un indice di tutti i pacchetti creati ed eliminati in nuget.org."
keywords: Catalogo delle API V3 NuGet, log delle transazioni nuget.org, replicare NuGet.org, clonare NuGet.org, solo di Accodamento record di NuGet.org
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 4c98b7cbd92575f6905e98a5bca5602a4d8ac0dd
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="catalog"></a>Catalog

Il **catalogo** è una risorsa che registra tutte le operazioni su un'origine del pacchetto, ad esempio eliminazioni e le operazioni di creazione del pacchetto. La risorsa di catalogo ha il `Catalog` digitare il [indice servizio](service-index.md).

> [!Note]
> Poiché il catalogo non viene utilizzato dal client NuGet ufficiale, non tutte le origini pacchetto implementano il catalogo.

> [!Note]
> Il catalogo nuget.org non è attualmente disponibile in Cina. Per ulteriori informazioni, vedere [NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Controllo delle versioni

Le operazioni seguenti `@type` valore viene utilizzato:

Valore di @type   | Note
------------- | -----
Catalog/3.0.0 | La versione iniziale

## <a name="base-url"></a>URL di base

L'URL del punto di ingresso per le API seguente è il valore di `@id` proprietà associato alla risorsa menzionati in precedenza `@type` valori. Questo argomento viene utilizzato l'URL di segnaposto `{@id}`.

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL, vedere il supporto di risorsa catalogo solo i metodi HTTP `GET` e `HEAD`.

## <a name="catalog-index"></a>Indice del catalogo

L'indice del catalogo è un documento in un percorso noto che include un elenco di elementi di catalogo, ordinati in cronologically. È il punto di ingresso della risorsa di catalogo.

L'indice è costituita da pagine di catalogo. Ogni pagina di catalogo contiene gli elementi del catalogo. Ogni elemento del catalogo rappresenta un evento relativi a un singolo pacchetto in un punto nel tempo. Un elemento del catalogo può rappresentare un pacchetto che è stato creato, non in elenco, rimesse in vendita o eliminata dall'origine del pacchetto. Gli elementi del catalogo in ordine cronologico di elaborazione, il client può compilare una visualizzazione aggiornata di ogni pacchetto esiste nell'origine pacchetto V3.

In breve, BLOB catalogo hanno la struttura gerarchica seguente:

- **Indice**: il punto di ingresso per il catalogo.
- **Pagina**: un raggruppamento di elementi di catalogo.
- **Foglia**: un documento che rappresenta un elemento del catalogo, che è uno snapshot dello stato di un singolo pacchetto.

Ogni oggetto del catalogo contiene una proprietà denominata la `commitTimeStamp` che rappresenta quando l'elemento è stato aggiunto al catalogo. Gli elementi del catalogo vengono aggiunti a una pagina di catalogo in batch chiamato commit. Tutti gli elementi di catalogo nello stesso commit è lo stesso timestamp di commit (`commitTimeStamp`) ed eseguire il commit ID (`commitId`). Gli elementi del catalogo in modalità di commit della stessa rappresentano eventi verificatisi alla stesso punto nel tempo sull'origine del pacchetto. Non sussiste alcun ordinamento all'interno di un commit di catalogo.

Poiché ogni ID di pacchetto e la versione è univoco, non sarà mai più di un elemento del catalogo in un'operazione di commit. In questo modo si garantisce che sempre gli elementi del catalogo per un singolo pacchetto possono essere ordinati in modo univoco rispetto a timestamp di commit.

Si è mai essere più di un solo commit al catalogo per `commitTimeStamp`. In altre parole, il `commitId` è ridondante con la `commitTimeStamp`.

Al contrario di [risorsa dei metadati del pacchetto](registration-base-url-resource.md), che è ordinato per ID pacchetto, il catalogo è indicizzata (e queryable) solo dal tempo.

Gli elementi del catalogo vengono sempre aggiunti al catalogo in un ordine cronologico, a incremento progressivo costante. Ciò significa che se un commit catalogo viene aggiunto in fase di X quindi alcun commit catalogo non verrà mai aggiunto con un tempo minore o uguale a X.

La richiesta seguente recupera l'indice del catalogo.

```
GET {@id}
```

L'indice del catalogo è un documento JSON che contiene un oggetto con le proprietà seguenti:

nome            | Tipo             | Obbligatorio | Note
--------------- | ---------------- | -------- | -----
commitId        | stringa           | sì      | Un ID univoco associato il commit di più recente
commitTimeStamp | stringa           | sì      | Un timestamp dell'ultimo commit
count           | numero intero          | sì      | Il numero di pagine nell'indice
Elementi           | Matrice di oggetti | sì      | Una matrice di oggetti, ogni oggetto che rappresenta una pagina

Ogni elemento di `items` matrice è un oggetto con alcuni dettagli minimi su ogni pagina. Questi oggetti non contengono le foglie catalogo (elementi). Non è definito l'ordine degli elementi nella matrice. Le pagine possono essere ordinate dal client tramite i relativi `commitTimeStamp` proprietà.

Come vengono introdotte nuove pagine, il `count` verrà incrementato e nuovi oggetti verranno visualizzato nel `items` matrice.

Quando vengono aggiunti al catalogo, l'indice `commitId` cambierà e `commitTimeStamp` aumenterà. Queste due proprietà sono essenzialmente un riepilogo sulla pagina tutte `commitId` e `commitTimeStamp` i valori di `items` matrice.

### <a name="catalog-page-object-in-the-index"></a>Oggetto pagina in corrispondenza dell'indice del catalogo

Gli oggetti della pagina catalogo trovato in tale indice `items` proprietà sono le seguenti proprietà:

nome            | Tipo    | Obbligatorio | Note
--------------- | ------- | -------- | -----
@id             | stringa  | sì      | L'URL alla pagina catalogo fetch
commitId        | stringa  | sì      | Un ID univoco associato a tale operazione più recente in questa pagina
commitTimeStamp | stringa  | sì      | Un timestamp del commit della più recente in questa pagina
count           | numero intero | sì      | Il numero di elementi nella pagina catalogo

Al contrario di [risorsa dei metadati del pacchetto](registration-base-url-resource.md) che in alcuni casi inline lascia in corrispondenza dell'indice, lascia catalogo non è mai resa inline in corrispondenza dell'indice e deve sempre essere recuperate utilizzando la pagina `@id` URL.

### <a name="sample-request"></a>Richiesta di esempio

```
GET https://api.nuget.org/v3/catalog0/index.json
```

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Pagina catalogo

Pagina catalogo è una raccolta di elementi di catalogo. Si tratta di un documento recuperato usando uno del `@id` i valori presenti in tale indice. L'URL a una pagina di catalogo non deve essere prevedibili e deve essere individuata utilizzando solo l'indice del catalogo.

Nuovi elementi di catalogo vengono aggiunti alla pagina nell'indice catalogo solo con il timestamp di commit più alto o in una nuova pagina. Dopo aver aggiunto una pagina con un timestamp di commit superiore al catalogo, vengono aggiunti o modificate mai pagine precedenti.

Documento di pagina del catalogo è un oggetto JSON con le proprietà seguenti:

nome            | Tipo             | Obbligatorio | Note
--------------- | ---------------- | -------- | -----
commitId        | stringa           | sì      | Un ID univoco associato a tale operazione più recente in questa pagina
commitTimeStamp | stringa           | sì      | Un timestamp del commit della più recente in questa pagina
count           | numero intero          | sì      | Il numero di elementi nella pagina
Elementi           | Matrice di oggetti | sì      | Gli elementi del catalogo in questa pagina
Elemento padre          | stringa           | sì      | Un URL per l'indice del catalogo

Ogni elemento di `items` matrice è un oggetto con alcuni dettagli minimi sull'elemento del catalogo. Questi oggetti non contengono tutti i dati dell'elemento del catalogo. L'ordine degli elementi della pagina `items` matrice non è definita. Gli elementi possono essere ordinati dal client tramite i relativi `commitTimeStamp` proprietà.

Il numero di elementi di catalogo in una pagina viene definito dall'implementazione di server. Per nuget.org, esistono più 550 elementi in ogni pagina, anche se il numero effettivo potrebbe essere più piccolo per dependong alcune pagine alle dimensioni del batch di commit successivo in corrispondenza del punto nel tempo.

Come vengono introdotti nuovi elementi, il `count` viene incrementato e nuovo catalogo elemento oggetti vengono visualizzati nel `items` matrice.

Quando vengono aggiunti elementi alla pagina, il `commitId` le modifiche e `commitTimeStamp` aumenta. Queste due proprietà sono essenzialmente un riepilogo su tutti `commitId` e `commitTimeStamp` i valori di `items` matrice.

### <a name="catalog-item-object-in-a-page"></a>Oggetto in una pagina del catalogo

Gli oggetti elemento del catalogo, vedere la pagina Catalogo `items` proprietà sono le seguenti proprietà:

nome            | Tipo    | Obbligatorio | Note
--------------- | ------- | -------- | -----
@id             | stringa  | sì      | L'URL per recuperare l'elemento del catalogo
@type           | stringa  | sì      | Il tipo dell'elemento del catalogo
commitId        | stringa  | sì      | L'ID commit associato a questo elemento del catalogo
commitTimeStamp | stringa  | sì      | Il timestamp di commit di questo elemento del catalogo
NuGet:ID        | stringa  | sì      | L'ID del pacchetto che riguarda questa foglia
NuGet:Version   | stringa  | sì      | La versione del pacchetto che riguarda questa foglia

Il `@type` valore sarà uno dei due valori seguenti:

1. `nuget:PackageDetails`: corrisponde al `PackageDetails` tipo foglia nel catalogo.
1. `nuget:PackageDelete`: corrisponde alla `PackageDelete` tipo foglia nel catalogo.

Per ulteriori dettagli sul ogni tipo, vedere il [corrispondenti elementi di tipo](#item-types) sotto.

### <a name="sample-request"></a>Richiesta di esempio

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Catalogo foglia

La foglia di catalogo contiene i metadati relativi a un pacchetto specifico ID e una versione a un certo punto nel tempo. Si tratta di un documento recuperato tramite il `@id` valore trovato in una pagina di catalogo. L'URL a un nodo foglia catalogo non deve essere predictedable e deve essere individuata utilizzando una pagina di un catalogo.

Documento di foglia del catalogo è un oggetto JSON con le proprietà seguenti:

nome                    | Tipo                       | Obbligatorio | Note
----------------------- | -------------------------- | -------- | -----
@type                   | stringa o matrice di stringhe | sì      | Il tipo di elemento del catalogo
catalogo: commitId        | stringa                     | sì      | Un ID di commit associato a questo elemento del catalogo
catalogo: commitTimeStamp | stringa                     | sì      | Il timestamp di commit di questo elemento del catalogo
ID                      | stringa                     | sì      | L'ID del pacchetto dell'elemento del catalogo
Pubblicato               | stringa                     | sì      | La data di pubblicazione dell'elemento del catalogo di pacchetto
version                 | stringa                     | sì      | La versione del pacchetto dell'elemento del catalogo

### <a name="item-types"></a>Tipi di elemento

Il `@type` proprietà è una stringa o matrice di stringhe. Per praticità, se il `@type` valore è una stringa, devono essere considerato come una matrice di dimensioni di uno. Non tutti i valori possibili per `@type` sono documentati. Tuttavia, ogni elemento del catalogo è esattamente uno dei due valori di tipo stringa seguente:

1. `PackageDetails`: rappresenta uno snapshot dei metadati del pacchetto
1. `PackageDelete`: rappresenta un pacchetto che è stato eliminato

### <a name="package-details-catalog-items"></a>I dettagli del pacchetto di elementi di catalogo

Elementi con il tipo di catalogo `PackageDetails` contengono uno snapshot di metadati del pacchetto per un pacchetto specifico (combinazione di ID e versione). Un elemento del catalogo dei dettagli del pacchetto viene generato quando un'origine del pacchetto si verifica uno qualsiasi dei seguenti scenari:

1. Un pacchetto è **inserito**.
1. Un pacchetto è **elencati**.
1. Un pacchetto è **non in elenco**.
1. Un pacchetto è **ridisposto**.

Ridisposizione un pacchetto è un movimento amministrativo che essenzialmente genera un falso push di un pacchetto esistente senza apportare modifiche al pacchetto stesso. In nuget.org, viene utilizzato un ridisposizione dopo avere corretto un bug in uno dei processi in background che utilizzano il catalogo.

I client utilizzano gli elementi del catalogo non tentare di determinare quale di questi scenari generato l'elemento del catalogo. Al contrario, il client deve limitarsi ad aggiornare qualsiasi indice o una visualizzazione gestita con i metadati contenuti nell'elemento del catalogo. Inoltre, gli elementi del catalogo duplicata o ridondante devono essere gestiti normalmente (in modo idempotente).

Gli elementi del catalogo dei dettagli del pacchetto sono le seguenti proprietà oltre a quelli [incluso nel catalogo foglie](#catalog-leaf).

nome                    | Tipo                       | Obbligatorio | Note
----------------------- | -------------------------- | -------- | -----
authors                 | stringa                     | No       |
created                 | stringa                     | sì      | Un timestamp di creazione innanzitutto il pacchetto
dependencyGroups        | Matrice di oggetti           | No       | Stesso formato del [risorsa dei metadati del pacchetto](registration-base-url-resource.md#package-dependency-group)
Descrizione             | stringa                     | No       |
iconUrl                 | stringa                     | No       |
isPrerelease            | boolean                    | sì      | Se è o meno la versione del pacchetto non definitive
language                | stringa                     | No       |
licenseUrl              | stringa                     | No       |
disponibili                  | boolean                    | No       | Se il pacchetto verrà elencato
Oggetto MinClientVersion        | stringa                     | No       |
packageHash             | stringa                     | sì      | L'hash del pacchetto, utilizzando la codifica [standard base 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | stringa                     | sì      |
packageSize             | numero intero                    | sì      | Le dimensioni di .nupkg il pacchetto in byte
projectUrl              | stringa                     | No       |
releaseNotes            | stringa                     | No       |
requireLicenseAgreement | boolean                    | No       | Si supponga `false` se escluso
summary                 | stringa                     | No       |
tag                    | Matrice di stringhe           | No       |
title                   | stringa                     | No       |
verbatimVersion         | stringa                     | No       | La stringa di versione perché originariamente è stata trovata nel. nuspec

Il pacchetto `version` proprietà è la stringa di versione completo, normalizzato. Ciò significa che i dati di compilazione SemVer 2.0.0 possono essere inclusi di seguito.

Il `created` timestamp è quando il pacchetto è stato ricevuto dall'origine del pacchetto, ovvero in genere un breve periodo di tempo prima di timestamp di commit dell'elemento del catalogo.

Il `packageHashAlgorithm` è una stringa definita dal represeting di implementazione di server l'algoritmo hash utilizzato per produrre il `packageHash`. NuGet.org sempre usato il `packageHashAlgorithm` valore `SHA512`.

Il `published` timestamp è l'ora dell'ultima elencato quando il pacchetto.

> [!Note]
> In nuget.org, il `published` è impostato su anni 1900 quando il pacchetto è incluso nell'elenco.

#### <a name="sample-request"></a>Richiesta di esempio

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

#### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Eliminare gli elementi di catalogo pacchetto

Elementi con il tipo di catalogo `PackageDelete` contengono un set minimo di informazioni che indicano ai client di catalogo che un pacchetto è stato eliminato dall'origine del pacchetto e non è più disponibile per qualsiasi operazione di pacchetto (ad esempio ripristino).

> [!Note]
> È possibile che un pacchetto da eliminare e ripubblicate in un secondo momento utilizzando il stesso ID di pacchetto e la versione. In nuget.org, questo è un caso raro come interrompe il presupposto ufficiale del client che un ID del pacchetto e versione implica il contenuto di un pacchetto specifico. Per ulteriori informazioni sull'eliminazione di pacchetti in nuget.org, vedere [nell'informativa](../policies/deleting-packages.md).

Eliminare gli elementi di catalogo pacchetto non dispongono di alcuna proprietà aggiuntive oltre a quelli [incluso nel catalogo foglie](#catalog-leaf).

Il `version` proprietà corrisponde alla stringa di versione originale, vedere il. nuspec pacchetto.

Il `published` proprietà indica il tempo quando pacchetto è stato eliminato, che è in genere come breve periodo di tempo prima di timestamp di commit dell'elemento del catalogo.

#### <a name="sample-request"></a>Richiesta di esempio

```
GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json
```

#### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Cursore

### <a name="overview"></a>Panoramica

In questa sezione viene descritto un concetto di client che, anche se non è necessariamente obbligatoria per il protocollo, deve essere parte di qualsiasi implementazione client catalogo pratiche.

Poiché il catalogo è una struttura di data append-only indicizzata dal tempo, il client deve archiviare un **cursore** localmente, che rappresentano fino a il punto nel tempo che il client ha elaborato gli elementi del catalogo. Si noti che questo valore di cursore non deve essere generato mai usando il formato di computer del client. Al contrario, il valore deve provenire da un oggetto di catalogo `commitTimestamp` valore.

Ogni volta che il client richiede l'elaborazione di nuovi eventi sull'origine del pacchetto, è necessario solo il catalogo di query per tutti gli elementi di catalogo con un timestamp di commit maggiore il cursore stored. Dopo che il client ha elaborato correttamente tutti i nuovi elementi di catalogo, registra il timestamp di commit più recente degli elementi del catalogo solo elaborati come nuovo valore di cursore.

Questo approccio, il client può essere assicurarsi di perdere tutti gli eventi del pacchetto che si è verificata l'origine del pacchetto.
Inoltre, il client non deve mai rielaborare gli eventi precedenti prima di timestamp di commit registrate del cursore.

Questo concetto molto efficace dei cursori viene utilizzato per la maggior parte dei processi in background nuget.org e viene utilizzato per mantenere la stessa interfaccia API di V3 aggiornati. 

### <a name="initial-value"></a>Valore iniziale

Quando il client di catalogo avvio per la prima volta (e pertanto non ha alcun valore cursore), deve utilizzare un valore di cursore predefinito di. Del NET `System.DateTimeOffset.MinValue` o alcuni un concetto analogo di timestamp rappresentabile minimo.

### <a name="iterating-over-catalog-items"></a>Scorrere gli elementi del catalogo

Per eseguire una query per il set successivo di elementi di catalogo da elaborare, il client deve:

1. Recuperare il valore di cursore registrati da un archivio locale.
1. Scaricare e deserializzare l'indice del catalogo.
1. Trova tutte le pagine con un timestamp di commit del catalogo *maggiore* il cursore.
1. Dichiarare un elenco vuoto di elementi di catalogo da elaborare.
1. Per ogni pagina di catalogo corrispondenza nel passaggio 3:
   1. Download e la deserializzazione della pagina di catalogo.
   1. Trova tutti gli elementi con un timestamp di commit del catalogo *maggiore* il cursore.
   1. Aggiungere tutti gli elementi di catalogo corrispondente all'elenco dichiarato nel passaggio 4.
1. Ordinare l'elenco di elementi di catalogo timestamp di commit.
1. Elaborazione di ogni elemento del catalogo in sequenza:
   1. Scaricare e deserializzare l'elemento del catalogo.
   1. Rispondere nel modo appropriato al tipo dell'elemento del catalogo.
   1. Elaborare il documento di elemento di catalogo in modo specifiche del client.
1. Registrare il timestamp di commit dell'ultimo elemento di catalogo come nuovo valore di cursore.

Con questo algoritmo di base, l'implementazione del client può creare una visualizzazione completa di tutti i pacchetti disponibili nell'origine pacchetto. Il client è necessario eseguire solo l'algoritmo periodicamente per tenere sempre le ultime modifiche apportate all'origine del pacchetto.

> [!Note]
> Si tratta dell'algoritmo che nuget.org viene utilizzata per mantenere il [dei metadati del pacchetto](registration-base-url-resource.md), [il contenuto del pacchetto](package-base-address-resource.md), [ricerca](search-query-service-resource.md) e [completamento automatico](search-autocomplete-service-resource.md) risorse aggiornate.

### <a name="dependent-cursors"></a>Cursori dipendenti

Si supponga che sono disponibili due client di catalogo che hanno una dipendenza inherant in output del client dipende da output del client. 

#### <a name="example"></a>Esempio

Ad esempio, in nuget.org un pacchetto appena pubblicato non deve essere visualizzati nella risorsa di ricerca prima che venga visualizzato nella risorsa di metadati del pacchetto. Questo avviene perché l'operazione di "ripristino" eseguita dal client ufficiale NuGet Usa la risorsa dei metadati del pacchetto. Se un cliente consente di individuare un pacchetto tramite il servizio di ricerca, è possibile ripristinare correttamente il pacchetto utilizzando la risorsa dei metadati del pacchetto. In altre parole, la risorsa di ricerca dipende la risorsa dei metadati del pacchetto. Ogni risorsa ha un processo in background catalogo client l'aggiornamento di tale risorsa. Ogni client ne ha il proprio tipo di cursore.

Poiché entrambe le risorse vengono create di fuori del catalogo, il cursore del client che aggiorna la risorsa di ricerca catalogo *non devono andare oltre* il cursore del client di catalogo di metadati del pacchetto.

#### <a name="algorithm"></a>Algoritmo

Per implementare questa restrizione, semplice modificare l'algoritmo precedente:

1. Recuperare il valore di cursore registrati da un archivio locale.
1. Scaricare e deserializzare l'indice del catalogo.
1. Trova tutte le pagine con un timestamp di commit del catalogo *maggiore* il cursore **minore o uguale al cursore della dipendenza.**
1. Dichiarare un elenco vuoto di elementi di catalogo da elaborare.
1. Per ogni pagina di catalogo corrispondenza nel passaggio 3:
   1. Download e la deserializzazione della pagina di catalogo.
   1. Trova tutti gli elementi con un timestamp di commit del catalogo *maggiore* il cursore **minore o uguale al cursore della dipendenza.**
   1. Aggiungere tutti gli elementi di catalogo corrispondente all'elenco dichiarato nel passaggio 4.
1. Ordinare l'elenco di elementi di catalogo timestamp di commit.
1. Elaborazione di ogni elemento del catalogo in sequenza:
   1. Scaricare e deserializzare l'elemento del catalogo.
   1. Rispondere nel modo appropriato al tipo dell'elemento del catalogo.
   1. Elaborare il documento di elemento di catalogo in modo specifiche del client.
1. Registrare il timestamp di commit dell'ultimo elemento di catalogo come nuovo valore di cursore.

Utilizzo di questo algoritmo modificato, è possibile compilare un sistema del client di catalogo dipendenti che produce tutti i propri indici specifici, gli elementi e così via.
