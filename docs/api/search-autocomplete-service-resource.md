---
title: Completamento automatico, NuGet API
description: Il servizio di completamento automatico di ricerca supporta le versioni e rilevamento interattivo di ID di pacchetto.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d5e1936c6c5406a1a376c16b2bad5351320dfb4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822136"
---
# <a name="autocomplete"></a>Completamento automatico

È possibile creare un pacchetto ID e la versione autocomplete esperienza tramite l'API V3. La risorsa utilizzata per l'esecuzione di query di completamento automatico è il `SearchAutocompleteService` risorsa trovata nel [indice servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

Nell'esempio `@type` vengono utilizzati i valori:

Valore di @type                          | Note
------------------------------------ | -----
SearchAutocompleteService            | La versione iniziale
SearchAutocompleteService/3.0.0-beta | Alias di `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Alias di `SearchAutocompleteService`

## <a name="base-url"></a>URL di base

L'URL di base per le API seguente è il valore di `@id` proprietà associati a uno della risorsa menzionati in precedenza `@type` valori. Nel documento seguente, il segnaposto URL di base `{@id}` verrà utilizzato.

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL trovati, il supporto di risorsa di registrazione, i metodi HTTP `GET` e `HEAD`.

## <a name="search-for-package-ids"></a>Ricerca per ID pacchetto

Il primo completamento automatico API supporta la ricerca di parte di una stringa di ID di pacchetto. Questo è molto utile quando si desidera fornire una funzionalità typeahead pacchetto in un'interfaccia utente integrata con un'origine del pacchetto NuGet.

Un pacchetto con le versioni non in elenco non verrà visualizzati nei risultati.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametri della richiesta

nome        | In     | Tipo    | Obbligatorio | Note
----------- | ------ | ------- | -------- | -----
q           | URL    | stringa  | No       | La stringa da confrontare con l'ID di pacchetto
skip        | URL    | numero intero | No       | Il numero di risultati da ignorare per l'impaginazione
Take        | URL    | numero intero | No       | Il numero di risultati da restituire, per la paginazione
versione provvisoria  | URL    | boolean | No       | `true` o `false` determinano l'opportunità di includere [pacchetti versione non definitiva](../create-packages/prerelease-packages.md)
semVerLevel | URL    | stringa  | No       | Una stringa di versione SemVer 1.0.0 

La query con completamento automatico `q` viene analizzato in modo che è definito dall'implementazione del server. NuGet.org supporta l'esecuzione di query per il prefisso di token ID di pacchetto, che sono pezzi dell'ID prodotto da [PROD143] e originale da caratteri iniziali di case e simboli.

Il `skip` valori predefiniti dei parametri su 0.

Il `take` parametro deve essere un numero intero maggiore di zero. L'implementazione del server potrebbe avere un valore massimo.

Se `prerelease` non viene fornito, vengono esclusi i pacchetti pre-release.

Il `semVerLevel` parametro di query viene utilizzato per acconsentire esplicitamente a [SemVer 2.0.0 pacchetti](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Se questo parametro di query viene esclusa, verranno restituiti solo gli ID di pacchetto con le versioni compatibili SemVer 1.0.0 (con il [standard controllo delle versioni NuGet](../reference/package-versioning.md) avvertenze, ad esempio le stringhe di versione con 4 elementi di tipo integer).
Se `semVerLevel=2.0.0` viene fornito, verranno restituiti SemVer 1.0.0 sia pacchetti compatibili SemVer 2.0.0. Vedere il [supporto SemVer 2.0.0 per nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) per ulteriori informazioni.

### <a name="response"></a>Risposta

La risposta è il documento JSON che contiene fino a `take` risultati di completamento automatico.

Oggetto JSON radice ha le proprietà seguenti:

nome      | Tipo             | Obbligatorio | Note
--------- | ---------------- | -------- | -----
totalHits | numero intero          | sì      | Il numero complessivo di corrispondenze, non considerando `skip` e `take`
Data      | Matrice di stringhe | sì      | Il pacchetto corrispondente di ID dalla richiesta

### <a name="sample-request"></a>Richiesta di esempio

OTTIENI https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Enumerare le versioni di pacchetto

Dopo che viene rilevato un ID pacchetto tramite l'API precedente, un client può utilizzare l'API di completamento automatico per enumerare le versioni di pacchetto per un ID di pacchetto fornito.

Una versione del pacchetto che è incluso nell'elenco non verrà visualizzato nei risultati.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametri della richiesta

nome        | In     | Tipo    | Obbligatorio | Note
----------- | ------ | ------- | -------- | -----
ID          | URL    | stringa  | sì      | Per recuperare le versioni per l'ID del pacchetto
versione provvisoria  | URL    | boolean | No       | `true` o `false` determinano l'opportunità di includere [pacchetti versione non definitiva](../create-packages/prerelease-packages.md)
semVerLevel | URL    | stringa  | No       | Una stringa di versione SemVer 2.0.0 

Se `prerelease` non viene fornito, vengono esclusi i pacchetti pre-release.

Il `semVerLevel` parametro di query viene utilizzato per acconsentire esplicitamente a pacchetti SemVer 2.0.0. Se questo parametro di query viene esclusa, verranno restituite solo le versioni SemVer 1.0.0. Se `semVerLevel=2.0.0` viene fornito, verranno restituite SemVer 1.0.0 sia versioni SemVer 2.0.0. Vedere il [supporto SemVer 2.0.0 per nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) per ulteriori informazioni.

### <a name="response"></a>Risposta

La risposta è il documento JSON che contiene tutte le versioni di pacchetto dell'ID pacchetto fornito, applicando un filtro per i parametri di query specificata.

Oggetto JSON radice dispone della proprietà seguente:

nome      | Tipo             | Obbligatorio | Note
--------- | ---------------- | -------- | -----
Data      | Matrice di stringhe | sì      | Le versioni del pacchetto corrispondente alla richiesta

Le versioni del pacchetto nel `data` matrice può contenere i metadati di compilazione SemVer 2.0.0 (ad esempio `1.0.0+metadata`) se il `semVerLevel=2.0.0` è stato specificato nella stringa di query.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
