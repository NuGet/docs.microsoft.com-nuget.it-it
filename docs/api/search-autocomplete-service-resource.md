---
title: Completamento automatico, API NuGet
description: Il servizio di completamento automatico di ricerca supporta l'individuazione interattiva di ID e versioni del pacchetto.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: f574849bf99cd4da4eefd55c3dd5a0648042f0c1
ms.sourcegitcommit: 7e9c0630335ef9ec1e200e2ee9065f702e52a8ec
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/24/2020
ms.locfileid: "85292293"
---
# <a name="autocomplete"></a>Completamento automatico

È possibile creare un ID pacchetto e un'esperienza di completamento automatico della versione usando l'API V3. La risorsa utilizzata per eseguire query di completamento automatico è la `SearchAutocompleteService` risorsa presente nell' [indice del servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

`@type`Vengono usati i valori seguenti:

Valore della proprietà @type                          | Note
------------------------------------ | -----
SearchAutocompleteService            | Versione iniziale
SearchAutocompleteService/3.0.0-beta | Alias di`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-RC   | Alias di`SearchAutocompleteService`
SearchAutocompleteService/3.5.0      | Include il supporto per il `packageType` parametro di query

### <a name="searchautocompleteservice350"></a>SearchAutocompleteService/3.5.0
Questa versione introduce il supporto per il `packageType` parametro di query, consentendo il filtraggio in base ai tipi di pacchetti definiti dall'autore. È completamente compatibile con le query in `SearchAutocompleteService` .

## <a name="base-url"></a>URL di base

L'URL di base per le API seguenti è il valore della `@id` proprietà associata a uno dei valori di risorsa menzionati sopra `@type` . Nel documento seguente verrà usato l'URL di base segnaposto `{@id}` .

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL trovati nella risorsa di registrazione supportano i metodi HTTP `GET` e `HEAD` .

## <a name="search-for-package-ids"></a>Ricerca di ID pacchetto

La prima API di completamento automatico supporta la ricerca di una parte di una stringa ID pacchetto. Questo è molto utile quando si vuole fornire una funzionalità di typeahead del pacchetto in un'interfaccia utente integrata con un'origine del pacchetto NuGet.

Un pacchetto solo con versioni non in elenco non verrà visualizzato nei risultati.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}

### <a name="request-parameters"></a>Parametri della richiesta

Nome        | In     | Type    | Necessario | Note
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | no       | Stringa da confrontare con gli ID del pacchetto
skip        | URL    | integer | no       | Numero di risultati da ignorare per la paginazione
take        | URL    | integer | no       | Numero di risultati da restituire per la paginazione
prerelease  | URL    | boolean | no       | `true`o `false` determinare se includere i [pacchetti in versione non definitiva](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | no       | Una stringa di versione SemVer 1.0.0 
packageType | URL    | string  | no       | Tipo di pacchetto da utilizzare per filtrare i pacchetti (aggiunti in `SearchAutocompleteService/3.5.0` )

La query di completamento automatico `q` viene analizzata in modo definito dall'implementazione del server. nuget.org supporta l'esecuzione di query per il prefisso dei token ID del pacchetto, che sono parti dell'ID prodotto suddividendo il case originale per Camel e i caratteri simbolo.

Il `skip` valore predefinito del parametro è 0.

Il `take` parametro deve essere un numero intero maggiore di zero. L'implementazione del server può imporre un valore massimo.

Se `prerelease` non viene specificato, i pacchetti di versioni non definitive vengono esclusi.

Il `semVerLevel` parametro di query viene usato per acconsentire esplicitamente ai [pacchetti SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Se questo parametro di query è escluso, verranno restituiti solo gli ID pacchetto con versioni compatibili con SemVer 1.0.0 (con le avvertenze di [controllo delle versioni standard di NuGet](../concepts/package-versioning.md) , ad esempio le stringhe di versione con 4 parti Integer).
Se `semVerLevel=2.0.0` viene specificato, verranno restituiti sia i pacchetti compatibili con SemVer 1.0.0 che SemVer 2.0.0. Per ulteriori informazioni, vedere il [supporto di SemVer 2.0.0 per NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

Il `packageType` parametro viene utilizzato per filtrare ulteriormente i risultati di completamento automatico solo per i pacchetti che hanno almeno un tipo di pacchetto corrispondente al nome del tipo di pacchetto.
Se il tipo di pacchetto specificato non è un tipo di pacchetto valido come definito dal [documento del tipo di pacchetto](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), verrà restituito un risultato vuoto.
Se il tipo di pacchetto fornito è vuoto, non verrà applicato alcun filtro. In altre parole, il passaggio di nessun valore al `packageType` parametro si comporterà come se il parametro non venisse passato.

### <a name="response"></a>Risposta

La risposta è un documento JSON che contiene i `take` risultati di completamento automatico.

L'oggetto JSON radice presenta le proprietà seguenti:

Nome      | Type             | Necessario | Note
--------- | ---------------- | -------- | -----
totalHits | integer          | sì      | Il numero totale di corrispondenze, che non riguardano `skip` e`take`
data      | matrice di stringhe | sì      | ID del pacchetto corrispondenti alla richiesta

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Enumera versioni pacchetto

Una volta individuato l'ID di un pacchetto usando l'API precedente, un client può usare l'API di completamento automatico per enumerare le versioni del pacchetto per un ID pacchetto specificato.

Una versione del pacchetto non in elenco non verrà visualizzata nei risultati.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametri della richiesta

Nome        | In     | Type    | Necessario | Note
----------- | ------ | ------- | -------- | -----
id          | URL    | string  | sì      | ID del pacchetto per cui recuperare le versioni
prerelease  | URL    | boolean | no       | `true`o `false` determinare se includere i [pacchetti in versione non definitiva](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | no       | Una stringa di versione SemVer 2.0.0 

Se `prerelease` non viene specificato, i pacchetti di versioni non definitive vengono esclusi.

Il `semVerLevel` parametro di query viene usato per acconsentire esplicitamente ai pacchetti SemVer 2.0.0. Se questo parametro di query è escluso, verranno restituite solo le versioni SemVer 1.0.0. Se `semVerLevel=2.0.0` viene specificato, verranno restituite sia le versioni SemVer 1.0.0 che SemVer 2.0.0. Per ulteriori informazioni, vedere il [supporto di SemVer 2.0.0 per NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Risposta

La risposta è un documento JSON contenente tutte le versioni dei pacchetti dell'ID pacchetto specificato, filtrando in base ai parametri di query specificati.

L'oggetto JSON radice presenta la proprietà seguente:

Nome      | Type             | Necessario | Note
--------- | ---------------- | -------- | -----
data      | matrice di stringhe | sì      | Versioni del pacchetto corrispondenti alla richiesta

Le versioni del pacchetto nella `data` matrice possono contenere i metadati di compilazione SemVer 2.0.0 (ad esempio `1.0.0+metadata` ) se `semVerLevel=2.0.0` è specificato nella stringa di query.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
