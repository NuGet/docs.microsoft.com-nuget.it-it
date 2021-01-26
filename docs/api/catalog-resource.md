---
title: Risorsa catalogo, API NuGet V3
description: Il catalogo è un indice di tutti i pacchetti creati ed eliminati in nuget.org.
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 11485f583d6993919f6bb8acabcc87d9e4261975
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774155"
---
# <a name="catalog"></a>Catalogo

Il **Catalogo** è una risorsa che registra tutte le operazioni sui pacchetti in un'origine del pacchetto, ad esempio creazioni ed eliminazioni. Il tipo della risorsa di catalogo è `Catalog` nell' [indice del servizio](service-index.md). È possibile utilizzare questa risorsa per [eseguire una query per tutti i pacchetti pubblicati](../guides/api/query-for-all-published-packages.md).

> [!Note]
> Poiché il catalogo non viene usato dal client NuGet ufficiale, non tutte le origini dei pacchetti implementano il catalogo.

> [!Note]
> Attualmente, il catalogo nuget.org non è disponibile in Cina. Per altri dettagli, vedere [NuGet/NuGetGallery # 4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Controllo delle versioni

`@type`Viene utilizzato il valore seguente:

Valore della proprietà @type   | Note
------------- | -----
Catalog/3.0.0 | Versione iniziale

## <a name="base-url"></a>URL di base

L'URL del punto di ingresso per le API seguenti è il valore della `@id` proprietà associata ai valori di risorsa menzionati sopra `@type` . In questo argomento viene utilizzato l'URL segnaposto `{@id}` .

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL trovati nella risorsa di catalogo supportano solo i metodi HTTP `GET` e `HEAD` .

## <a name="catalog-index"></a>Indice Catalogo

L'indice del catalogo è un documento in una posizione nota che include un elenco di elementi del catalogo, ordinati in ordine cronologico. Si tratta del punto di ingresso della risorsa di catalogo.

L'indice è costituito da pagine di catalogo. Ogni pagina del catalogo contiene elementi del catalogo. Ogni elemento del catalogo rappresenta un evento relativo a un singolo pacchetto in un momento specifico. Un elemento del catalogo può rappresentare un pacchetto creato, non incluso nell'elenco, incluso di un elenco o eliminato dall'origine del pacchetto. Elaborando gli elementi del catalogo in ordine cronologico, il client può compilare una visualizzazione aggiornata di ogni pacchetto presente nell'origine del pacchetto V3.

In breve, i BLOB del catalogo hanno la struttura gerarchica seguente:

- **Index**: il punto di ingresso per il catalogo.
- **Pagina**: raggruppamento di elementi di catalogo.
- **Foglia**: un documento che rappresenta un elemento del catalogo, che è uno snapshot dello stato di un singolo pacchetto.

Ogni oggetto catalogo dispone di una proprietà denominata `commitTimeStamp` che rappresenta il momento in cui l'elemento è stato aggiunto al catalogo. Gli elementi del catalogo vengono aggiunti a una pagina del catalogo in batch chiamati commit. Tutti gli elementi del catalogo nello stesso commit hanno lo stesso timestamp di commit ( `commitTimeStamp` ) e l'ID commit ( `commitId` ). Gli elementi del catalogo inseriti nello stesso commit rappresentano gli eventi che si sono verificati allo stesso punto nel tempo nell'origine del pacchetto. Nessun ordine all'interno di un commit del catalogo.

Poiché ogni ID e versione del pacchetto è univoca, non sarà mai presente più di un elemento del catalogo in un commit. In questo modo si garantisce che gli elementi del catalogo per un singolo pacchetto possano essere ordinati in modo non ambiguo rispetto al timestamp di commit.

Non è mai presente più di un commit nel catalogo per `commitTimeStamp` . In altre parole, `commitId` è ridondante con `commitTimeStamp` .

Diversamente dalla [risorsa dei metadati del pacchetto](registration-base-url-resource.md), indicizzata in base all'ID del pacchetto, il catalogo è indicizzato (e Queryable) solo in base all'ora.

Gli elementi del catalogo vengono sempre aggiunti al catalogo in base a un ordine cronologico a incremento progressivo costante. Ciò significa che se viene aggiunto un commit del catalogo all'ora X, non verrà aggiunto alcun commit del catalogo con un'ora minore o uguale a X.

La richiesta seguente recupera l'indice del catalogo.

```
GET {@id}
```

L'indice del catalogo è un documento JSON che contiene un oggetto con le proprietà seguenti:

Nome            | Type             | Necessario | Note
--------------- | ---------------- | -------- | -----
commitId        | string           | sì      | ID univoco associato al commit più recente
commitTimeStamp | string           | sì      | Timestamp del commit più recente
count           | numero intero          | sì      | Numero di pagine nell'indice.
items           | matrice di oggetti | sì      | Matrice di oggetti, ognuno dei quali rappresenta una pagina

Ogni elemento nella `items` matrice è un oggetto con alcune informazioni minime su ogni pagina. Questi oggetti della pagina non contengono le foglie del catalogo (elementi). L'ordine degli elementi in questa matrice non è definito. Le pagine possono essere ordinate dal client in memoria usando la relativa `commitTimeStamp` Proprietà.

Quando vengono introdotte nuove pagine, `count` verrà incrementato e i nuovi oggetti verranno visualizzati nella `items` matrice.

Quando gli elementi vengono aggiunti al catalogo, l'indice `commitId` verrà modificato e l'oggetto `commitTimeStamp` aumenterà. Queste due proprietà sono essenzialmente un riepilogo di tutte le pagine `commitId` e `commitTimeStamp` i valori nella `items` matrice.

### <a name="catalog-page-object-in-the-index"></a>Oggetto pagina catalogo nell'indice

Gli oggetti della pagina del catalogo trovati nella proprietà dell'indice del catalogo `items` hanno le proprietà seguenti:

Nome            | Type    | Necessario | Note
--------------- | ------- | -------- | -----
@id             | string  | sì      | URL per recuperare la pagina del catalogo
commitId        | string  | sì      | ID univoco associato al commit più recente in questa pagina
commitTimeStamp | string  | sì      | Timestamp del commit più recente in questa pagina
count           | numero intero | sì      | Numero di elementi nella pagina catalogo

Diversamente dalla [risorsa dei metadati del pacchetto](registration-base-url-resource.md) , che in alcuni casi rimane inline nell'indice, le foglie del catalogo non vengono mai inserite nell'indice e devono sempre essere recuperate tramite l'URL della pagina `@id` .

### <a name="sample-request"></a>Richiesta di esempio

```
GET https://api.nuget.org/v3/catalog0/index.json
```

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Pagina Catalogo

La pagina catalogo è una raccolta di elementi del catalogo. Si tratta di un documento recuperato utilizzando uno dei `@id` valori disponibili nell'indice del catalogo. L'URL di una pagina del catalogo non può essere prevedibile e deve essere individuato utilizzando solo l'indice del catalogo.

I nuovi elementi del catalogo vengono aggiunti alla pagina nell'indice del catalogo solo con il timestamp di commit massimo o con una nuova pagina. Una volta aggiunta una pagina con un timestamp di commit superiore al catalogo, le pagine precedenti non vengono mai aggiunte o modificate.

Il documento della pagina del catalogo è un oggetto JSON con le proprietà seguenti:

Nome            | Type             | Necessario | Note
--------------- | ---------------- | -------- | -----
commitId        | string           | sì      | ID univoco associato al commit più recente in questa pagina
commitTimeStamp | string           | sì      | Timestamp del commit più recente in questa pagina
count           | numero intero          | sì      | Numero di elementi nella pagina
items           | matrice di oggetti | sì      | Gli elementi del catalogo in questa pagina
padre          | string           | sì      | URL dell'indice del catalogo

Ogni elemento nella `items` matrice è un oggetto con alcune informazioni minime sull'elemento del catalogo. Questi oggetti elemento non contengono tutti i dati dell'elemento del catalogo. L'ordine degli elementi nella matrice della pagina `items` non è definito. Gli elementi possono essere ordinati dal client in memoria usando la relativa `commitTimeStamp` Proprietà.

Il numero di elementi del catalogo in una pagina viene definito dall'implementazione del server. Per nuget.org, sono presenti al massimo 550 elementi in ogni pagina, anche se il numero effettivo può essere minore per alcune pagine, a seconda delle dimensioni del batch di commit successivo nel momento specifico.

Quando vengono introdotti nuovi elementi, `count` viene incrementato e i nuovi oggetti elemento del catalogo vengono visualizzati nella `items` matrice.

Man mano che vengono aggiunti elementi alla pagina, le `commitId` modifiche e `commitTimeStamp` aumentano. Queste due proprietà sono essenzialmente un riepilogo di tutti `commitId` `commitTimeStamp` i valori e nella `items` matrice.

### <a name="catalog-item-object-in-a-page"></a>Oggetto elemento del catalogo in una pagina

Gli oggetti elemento del catalogo disponibili nella proprietà della pagina del catalogo `items` hanno le proprietà seguenti:

Nome            | Type    | Necessario | Note
--------------- | ------- | -------- | -----
@id             | string  | sì      | URL per recuperare l'elemento del catalogo
@type           | string  | sì      | Tipo di elemento del catalogo
commitId        | string  | sì      | ID commit associato a questo elemento del catalogo
commitTimeStamp | string  | sì      | Timestamp di commit di questo elemento del catalogo
NuGet: ID        | string  | sì      | ID del pacchetto a cui è correlata questa foglia
NuGet: versione   | string  | sì      | Versione del pacchetto a cui è correlata questa foglia

Il `@type` valore sarà uno dei due valori seguenti:

1. `nuget:PackageDetails`: corrisponde al `PackageDetails` tipo nel documento foglia del catalogo.
1. `nuget:PackageDelete`: corrisponde al `PackageDelete` tipo nel documento foglia del catalogo.

Per ulteriori informazioni sul significato di ogni tipo, vedere il [tipo di elementi corrispondente](#item-types) di seguito.

### <a name="sample-request"></a>Richiesta di esempio

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Foglia Catalogo

La foglia del catalogo contiene i metadati relativi a una versione e a un ID pacchetto specifici in un determinato momento. Si tratta di un documento recuperato usando il `@id` valore trovato in una pagina di catalogo. L'URL di una foglia del catalogo non può essere prevedibile e deve essere individuato utilizzando solo una pagina di catalogo.

Il documento foglia del catalogo è un oggetto JSON con le proprietà seguenti:

Nome                    | Type                       | Necessario | Note
----------------------- | -------------------------- | -------- | -----
@type                   | Stringa o matrice di stringhe | sì      | Il tipo o i tipi dell'elemento del catalogo
Catalogo: commitid        | string                     | sì      | ID commit associato a questo elemento del catalogo
Catalogo: commitTimeStamp | string                     | sì      | Timestamp di commit di questo elemento del catalogo
id                      | string                     | sì      | ID del pacchetto dell'elemento del catalogo
published               | string                     | sì      | Data di pubblicazione dell'elemento del catalogo del pacchetto
version                 | string                     | sì      | Versione del pacchetto dell'elemento del catalogo

### <a name="item-types"></a>Tipi di elemento

La `@type` proprietà è una stringa o una matrice di stringhe. Per praticità, se il `@type` valore è una stringa, deve essere considerato come una matrice di dimensioni uno. Non tutti i valori possibili per `@type` sono documentati. Tuttavia, ogni elemento del catalogo ha esattamente uno dei due valori di tipo stringa seguenti:

1. `PackageDetails`: rappresenta uno snapshot dei metadati del pacchetto
1. `PackageDelete`: rappresenta un pacchetto eliminato

### <a name="package-details-catalog-items"></a>Elementi del catalogo Dettagli pacchetto

Gli elementi del catalogo con il tipo `PackageDetails` contengono uno snapshot dei metadati del pacchetto per un pacchetto specifico (combinazione di ID e versione). Un elemento del catalogo Dettagli pacchetto viene generato quando un'origine del pacchetto rileva uno degli scenari seguenti:

1. Viene eseguito il **push** di un pacchetto.
1. Viene **elencato** un pacchetto.
1. Un pacchetto non è incluso **nell'elenco**.
1. Un pacchetto viene **propagato**.

Un riflusso del pacchetto è un gesto amministrativo che essenzialmente genera un push fasullo di un pacchetto esistente senza modifiche al pacchetto stesso. In nuget.org viene usato un riflusso dopo la correzione di un bug in uno dei processi in background che utilizzano il catalogo.

I client che utilizzano gli elementi del catalogo non devono tentare di determinare quali di questi scenari hanno prodotto l'elemento del catalogo. Al contrario, il client deve semplicemente aggiornare qualsiasi vista o indice gestito con i metadati contenuti nell'elemento del catalogo. Inoltre, gli elementi del catalogo duplicati o ridondanti devono essere gestiti normalmente (modo idempotente).

Gli elementi del catalogo Dettagli pacchetto hanno le proprietà seguenti, oltre a quelle [incluse in tutte le foglie del catalogo](#catalog-leaf).

Nome                    | Type                       | Necessario | Note
----------------------- | -------------------------- | -------- | -----
authors                 | string                     | no       |
created                 | string                     | no       | Timestamp del momento in cui il pacchetto è stato creato per la prima volta. Proprietà fallback: `published` .
dependencyGroups        | matrice di oggetti           | no       | Dipendenze del pacchetto, raggruppate in base al Framework di destinazione ([stesso formato della risorsa di metadati del pacchetto](registration-base-url-resource.md#package-dependency-group))
deprecazione             | object                     | no       | La deprecazione associata al pacchetto ([stesso formato della risorsa di metadati del pacchetto](registration-base-url-resource.md#package-deprecation))
description             | string                     | no       |
iconUrl                 | string                     | no       |
isPrerelease            | boolean                    | no       | Indica se la versione del pacchetto è provvisoria o meno. Può essere rilevato da `version` .
Linguaggio                | string                     | no       |
licenseUrl              | string                     | no       |
disponibili                  | boolean                    | no       | Indica se il pacchetto è elencato
minClientVersion        | string                     | no       |
packageHash             | string                     | sì      | Hash del pacchetto, codifica con [base 64 standard](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | string                     | sì      |
Pacchetto             | numero intero                    | sì      | Dimensioni del package. nupkg in byte
packageTypes            | matrice di oggetti           | no       | Tipi di pacchetto specificati dall'autore.
projectUrl              | string                     | no       |
releaseNotes            | string                     | no       |
requireLicenseAgreement | boolean                    | no       | Presume `false` se è escluso
riepilogo                 | string                     | no       |
tags                    | matrice di stringhe           | no       |
title                   | string                     | no       |
verbatimVersion         | string                     | no       | La stringa di versione come in origine è stata trovata in. NuSpec

La `version` Proprietà Package è la stringa di versione completa dopo la normalizzazione. Ciò significa che i dati di compilazione di SemVer 2.0.0 possono essere inclusi qui.

Il `created` timestamp è quando il pacchetto è stato ricevuto per la prima volta dall'origine del pacchetto, che in genere è un breve intervallo di tempo prima del timestamp di commit dell'elemento del catalogo.

`packageHashAlgorithm`È una stringa definita dall'implementazione del server che rappresenta l'algoritmo hash utilizzato per produrre `packageHash` . nuget.org usa sempre il `packageHashAlgorithm` valore di `SHA512` .

La `packageTypes` proprietà sarà presente solo se un tipo di pacchetto è stato specificato dall'autore. Se è presente, sarà sempre presente almeno una voce (1). Ogni elemento nella `packageTypes` matrice è un oggetto JSON con le proprietà seguenti:

Nome      | Type    | Necessario | Note
--------- | ------- | -------- | -----
name      | string  | sì      | Nome del tipo di pacchetto.
version    | string  | no       | Versione del tipo di pacchetto. Presente solo se l'autore ha specificato in modo esplicito una versione in NuSpec.

Il `published` timestamp è l'ora dell'ultima elencazione del pacchetto.

> [!Note]
> In nuget.org, il `published` valore viene impostato sull'anno 1900 quando il pacchetto viene riincluso nell'elenco.

#### <a name="sample-request"></a>Richiesta di esempio

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

#### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Elimina pacchetto elementi del catalogo

Gli elementi del catalogo con il tipo `PackageDelete` contengono un set minimo di informazioni che indicano ai client del catalogo che un pacchetto è stato eliminato dall'origine del pacchetto e non è più disponibile per qualsiasi operazione del pacchetto (ad esempio, Restore).

> [!NOTE]
> È possibile che un pacchetto venga eliminato e successivamente ripubblicato utilizzando lo stesso ID e la stessa versione del pacchetto. In nuget.org, si tratta di un caso molto raro in cui si interrompe il presupposto del client ufficiale che l'ID e la versione di un pacchetto implicano un contenuto specifico del pacchetto. Per ulteriori informazioni sull'eliminazione dei pacchetti in nuget.org, vedere [i criteri](../nuget-org/policies/deleting-packages.md).

Gli elementi del catalogo Delete Package non includono proprietà aggiuntive, oltre a quelle [incluse in tutte le foglie del catalogo](#catalog-leaf).

La `version` proprietà è la stringa di versione originale trovata nel package. NuSpec.

La `published` proprietà è l'ora in cui è stato eliminato il pacchetto, che in genere è il tempo breve prima del timestamp di commit dell'elemento del catalogo.

#### <a name="sample-request"></a>Richiesta di esempio

```
GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json
```

#### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Cursore

### <a name="overview"></a>Panoramica

In questa sezione viene descritto un concetto client che, sebbene non sia necessariamente richiesto dal protocollo, deve far parte di qualsiasi implementazione del client di catalogo pratica.

Poiché il catalogo è una struttura di dati di sola aggiunta indicizzata in base al tempo, il client deve archiviare un **cursore** localmente, che rappresenta il punto nel tempo in cui il client ha elaborato gli elementi del catalogo. Si noti che questo valore di cursore non deve mai essere generato utilizzando il clock del computer del client. Al contrario, il valore deve provenire dal valore di un oggetto catalogo `commitTimestamp` .

Ogni volta che il client desidera elaborare nuovi eventi nell'origine del pacchetto, è necessario eseguire una query solo sul catalogo per tutti gli elementi del catalogo con un timestamp di commit maggiore del relativo cursore archiviato. Dopo che il client ha elaborato correttamente tutti i nuovi elementi del catalogo, viene registrato il timestamp di commit più recente degli elementi del catalogo appena elaborato come nuovo valore di cursore.

Con questo approccio, il client può essere sicuro di non perdere mai gli eventi del pacchetto che si sono verificati nell'origine del pacchetto.
Inoltre, il client non deve mai rielaborare gli eventi precedenti prima del timestamp di commit registrato del cursore.

Questo potente concetto di cursori viene usato per molti processi in background di nuget.org e viene usato per tenere aggiornata l'API V3. 

### <a name="initial-value"></a>Valore iniziale

Quando il client del catalogo viene avviato per la prima volta (e pertanto non dispone di alcun valore di cursore), deve utilizzare un valore di cursore predefinito pari a. NET `System.DateTimeOffset.MinValue` o una nozione analoga di timestamp rappresentativi minimi.

### <a name="iterating-over-catalog-items"></a>Iterazione sugli elementi del catalogo

Per eseguire una query per il set successivo di elementi del catalogo da elaborare, il client deve:

1. Recuperare il valore del cursore registrato da un archivio locale.
1. Scaricare e deserializzare l'indice del catalogo.
1. Trovare tutte le pagine del catalogo con un timestamp di commit *maggiore* del cursore.
1. Dichiarare un elenco vuoto di elementi del catalogo da elaborare.
1. Per ogni pagina del catalogo corrispondente al passaggio 3:
   1. Scaricare e deserializzare la pagina del catalogo.
   1. Trova tutti gli elementi del catalogo con un timestamp *di commit maggiore* del cursore.
   1. Aggiungere tutti gli elementi del catalogo corrispondenti all'elenco dichiarato nel passaggio 4.
1. Ordinare l'elenco di elementi del catalogo in base al timestamp del commit.
1. Elaborare ogni elemento del catalogo in sequenza:
   1. Scaricare e deserializzare l'elemento del catalogo.
   1. Reagire in modo appropriato al tipo di elemento del catalogo.
   1. Elaborare il documento dell'elemento del catalogo in modo specifico per il client.
1. Registrare il timestamp di commit dell'ultimo elemento del catalogo come nuovo valore del cursore.

Con questo algoritmo di base, l'implementazione client può creare una panoramica completa di tutti i pacchetti disponibili nell'origine del pacchetto. Il client deve eseguire periodicamente questo algoritmo per tenere sempre conto delle ultime modifiche apportate all'origine del pacchetto.

> [!Note]
> Si tratta dell'algoritmo usato da nuget.org per proteggere i [metadati del pacchetto](registration-base-url-resource.md), il [contenuto del pacchetto](package-base-address-resource.md), la [ricerca](search-query-service-resource.md) e il [completamento automatico](search-autocomplete-service-resource.md) delle risorse.

### <a name="dependent-cursors"></a>Cursori dipendenti

Si supponga che esistano due client di catalogo con una dipendenza intrinseca in cui l'output di un client dipende dall'output di un altro client. 

#### <a name="example"></a>Esempio

In nuget.org, ad esempio, un pacchetto appena pubblicato non dovrebbe essere visualizzato nella risorsa di ricerca prima che venga visualizzato nella risorsa dei metadati del pacchetto. Questo perché l'operazione di ripristino eseguita dal client NuGet ufficiale usa la risorsa di metadati del pacchetto. Se un cliente individua un pacchetto usando il servizio di ricerca, dovrebbe essere in grado di ripristinare correttamente tale pacchetto usando la risorsa di metadati del pacchetto. In altre parole, la risorsa di ricerca dipende dalla risorsa di metadati del pacchetto. Ogni risorsa ha un processo in background del client del catalogo che aggiorna la risorsa. Ogni client dispone di un proprio cursore.

Poiché entrambe le risorse sono compilate dal catalogo, il cursore del client del catalogo che aggiorna la risorsa di ricerca *non deve* superare il cursore del client del catalogo dei metadati del pacchetto.

#### <a name="algorithm"></a>Algoritmo

Per implementare questa restrizione, è sufficiente modificare l'algoritmo precedente in modo che sia:

1. Recuperare il valore del cursore registrato da un archivio locale.
1. Scaricare e deserializzare l'indice del catalogo.
1. Trovare tutte le pagine del catalogo con un timestamp di commit *maggiore* del cursore **minore o uguale al cursore della dipendenza.**
1. Dichiarare un elenco vuoto di elementi del catalogo da elaborare.
1. Per ogni pagina del catalogo corrispondente al passaggio 3:
   1. Scaricare e deserializzare la pagina del catalogo.
   1. Trovare tutti gli elementi del catalogo con un timestamp di commit *maggiore* del cursore **minore o uguale al cursore della dipendenza.**
   1. Aggiungere tutti gli elementi del catalogo corrispondenti all'elenco dichiarato nel passaggio 4.
1. Ordinare l'elenco di elementi del catalogo in base al timestamp del commit.
1. Elaborare ogni elemento del catalogo in sequenza:
   1. Scaricare e deserializzare l'elemento del catalogo.
   1. Reagire in modo appropriato al tipo di elemento del catalogo.
   1. Elaborare il documento dell'elemento del catalogo in modo specifico per il client.
1. Registrare il timestamp di commit dell'ultimo elemento del catalogo come nuovo valore del cursore.

Utilizzando questo algoritmo modificato, è possibile creare un sistema di client di catalogo dipendenti che producono tutti i propri indici, elementi e così via.
