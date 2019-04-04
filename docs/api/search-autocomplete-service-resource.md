---
title: Completamento automatico, API NuGet
description: Il servizio di ricerca autocomplete supporta le versioni e individuazione interattiva di ID di pacchetto.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fdc3ad8aa239a42d8a4c169a757715e856bdcb41
ms.sourcegitcommit: 9f94e00428d83aef4a7a87db679129eff7720c59
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/03/2019
ms.locfileid: "58911049"
---
# <a name="autocomplete"></a>Completamento automatico

È possibile creare un pacchetto ID e la versione autocomplete esperienza tramite l'API di V3. La risorsa utilizzata per l'esecuzione di query di completamento automatico è il `SearchAutocompleteService` trovare la risorsa nella [indice del servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

Nell'esempio `@type` vengono utilizzati i valori:

Valore di @type                          | Note
------------------------------------ | -----
SearchAutocompleteService            | La versione iniziale
SearchAutocompleteService/3.0.0-beta | Alias di `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Alias di `SearchAutocompleteService`

## <a name="base-url"></a>URL di base

L'URL di base per le API seguente è il valore della `@id` proprietà associati a uno della risorsa menzionati in precedenza `@type` valori. Nel documento seguente, il segnaposto URL di base `{@id}` verrà utilizzato.

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL disponibili il supporto di risorse di registrazione i metodi HTTP `GET` e `HEAD`.

## <a name="search-for-package-ids"></a>Ricerca per ID pacchetto

L'API di completamento automatico prima supporta la ricerca di parte di una stringa di ID di pacchetto. Ciò è ideale quando si desidera fornire una funzionalità di completamento automatico del pacchetto in un'interfaccia utente integrata con un'origine del pacchetto NuGet.

Un pacchetto con solo le versioni non in elenco non verrà visualizzato nei risultati.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametri della richiesta

Nome        | In     | Tipo    | Obbligatorio | Note
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | No       | La stringa da confrontare con gli ID pacchetto
skip        | URL    | numero intero | No       | Il numero di risultati da ignorare, per la paginazione
Take        | URL    | numero intero | No       | Il numero di risultati da restituire, per la paginazione
versione preliminare  | URL    | boolean | No       | `true` oppure `false` che determina se includere [i pacchetti di versioni non definitive](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | No       | Una stringa di versione SemVer 1.0.0 

La query di completamento automatico `q` viene analizzato in modo che è definito dall'implementazione del server. NuGet.org supporta l'esecuzione di query per il prefisso del token ID pacchetto, che sono pezzi dell'ID di prodotti dalla suddivisione originale da caratteri le iniziali maiuscole e simboli.

Il `skip` valori predefiniti dei parametri su 0.

Il `take` parametro deve essere un numero intero maggiore di zero. L'implementazione del server può imporre un valore massimo.

Se `prerelease` non viene specificato, vengono esclusi i pacchetti in versione non definitiva.

Il `semVerLevel` parametro di query viene utilizzato per acconsentire [pacchetti di SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Se questo parametro di query è stata esclusa, verranno restituiti solo gli ID di pacchetto con le versioni compatibili di SemVer 1.0.0 (con il [controllo delle versioni NuGet standard](../reference/package-versioning.md) avvertenze, ad esempio le stringhe di versione con 4 elementi integer).
Se `semVerLevel=2.0.0` viene fornito, verranno restituiti SemVer 1.0.0 sia pacchetti compatibili di SemVer 2.0.0. Vedere le [supporto di SemVer 2.0.0 per nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) per altre informazioni.

### <a name="response"></a>Risposta

La risposta è il documento JSON che contiene fino a `take` i risultati di completamento automatico.

L'oggetto JSON radice ha le proprietà seguenti:

Nome      | Tipo             | Obbligatorio | Note
--------- | ---------------- | -------- | -----
totalHits | numero intero          | sì      | Il numero complessivo di corrispondenze, ignorando `skip` e `take`
Data      | Matrice di stringhe | sì      | Il pacchetto ID trovare una corrispondenza con la richiesta

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Enumera le versioni dei pacchetti

Dopo che viene rilevato un ID di pacchetto tramite l'API precedente, un client può usare l'API di completamento automatico per enumerare le versioni dei pacchetti per un ID pacchetto specificato.

Una versione del pacchetto che è incluso nell'elenco non verrà visualizzato nei risultati.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametri della richiesta

Nome        | In     | Tipo    | Obbligatorio | Note
----------- | ------ | ------- | -------- | -----
ID          | URL    | string  | sì      | Per recuperare le versioni per l'ID del pacchetto
versione preliminare  | URL    | boolean | No       | `true` oppure `false` che determina se includere [i pacchetti di versioni non definitive](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | No       | Una stringa di versione di SemVer 2.0.0 

Se `prerelease` non viene specificato, vengono esclusi i pacchetti in versione non definitiva.

Il `semVerLevel` parametro di query viene utilizzato per acconsentire esplicitamente a pacchetti di SemVer 2.0.0. Se questo parametro di query è stata esclusa, verranno restituite solo le versioni di SemVer 1.0.0. Se `semVerLevel=2.0.0` è specificato, verranno restituite sia SemVer 1.0.0 e le versioni di SemVer 2.0.0. Vedere le [supporto di SemVer 2.0.0 per nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) per altre informazioni.

### <a name="response"></a>Risposta

La risposta è il documento JSON contenente tutte le versioni del pacchetto dell'ID pacchetto fornito, il filtro per i parametri di query specificata.

L'oggetto JSON radice ha la proprietà seguente:

Nome      | Tipo             | Obbligatorio | Note
--------- | ---------------- | -------- | -----
Data      | Matrice di stringhe | sì      | Le versioni del pacchetto corrispondente alla richiesta

Le versioni dei pacchetti nel `data` matrice può contenere i metadati di SemVer 2.0.0 compilazione (ad esempio `1.0.0+metadata`) se il `semVerLevel=2.0.0` viene fornito nella stringa di query.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
