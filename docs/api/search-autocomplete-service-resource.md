---
title: Completamento automatico, API NuGet
description: Il servizio di completamento automatico di ricerca supporta l'individuazione interattiva di ID e versioni del pacchetto.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488300"
---
# <a name="autocomplete"></a>Completamento automatico

È possibile creare un ID pacchetto e un'esperienza di completamento automatico della versione usando l'API V3. La risorsa utilizzata per eseguire query di completamento automatico è `SearchAutocompleteService` la risorsa presente nell' [indice del servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

Vengono usati `@type` i valori seguenti:

Valore di @type                          | Note
------------------------------------ | -----
SearchAutocompleteService            | Versione iniziale
SearchAutocompleteService/3.0.0-beta | Alias di`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Alias di`SearchAutocompleteService`

## <a name="base-url"></a>URL di base

L'URL di base per le API seguenti è il valore della `@id` proprietà associata a uno dei valori di risorsa `@type` menzionati sopra. Nel documento seguente verrà usato l'URL `{@id}` di base segnaposto.

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL trovati nella risorsa di registrazione supportano i metodi `GET` http `HEAD`e.

## <a name="search-for-package-ids"></a>Ricerca di ID pacchetto

La prima API di completamento automatico supporta la ricerca di una parte di una stringa ID pacchetto. Questo è molto utile quando si vuole fornire una funzionalità di typeahead del pacchetto in un'interfaccia utente integrata con un'origine del pacchetto NuGet.

Un pacchetto solo con versioni non in elenco non verrà visualizzato nei risultati.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametri della richiesta

Name        | In     | Type    | Obbligatoria | Note
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | no       | Stringa da confrontare con gli ID del pacchetto
skip        | URL    | integer | no       | Numero di risultati da ignorare per la paginazione
prendere        | URL    | integer | no       | Numero di risultati da restituire per la paginazione
prerelease  | URL    | boolean | no       | `true`o `false` determinare se includere i [pacchetti in versione non definitiva](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | no       | Una stringa di versione SemVer 1.0.0 

La query `q` di completamento automatico viene analizzata in modo definito dall'implementazione del server. nuget.org supporta l'esecuzione di query per il prefisso dei token ID del pacchetto, che sono parti dell'ID prodotto suddividendo il case originale per Camel e i caratteri simbolo.

Il `skip` valore predefinito del parametro è 0.

Il `take` parametro deve essere un numero intero maggiore di zero. L'implementazione del server può imporre un valore massimo.

Se `prerelease` non viene specificato, i pacchetti di versioni non definitive vengono esclusi.

Il `semVerLevel` parametro di query viene usato per acconsentire esplicitamente ai [pacchetti SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Se questo parametro di query è escluso, verranno restituiti solo gli ID pacchetto con versioni compatibili con SemVer 1.0.0 (con le avvertenze di [controllo delle versioni standard di NuGet](../concepts/package-versioning.md) , ad esempio le stringhe di versione con 4 parti Integer).
Se `semVerLevel=2.0.0` viene specificato, verranno restituiti sia i pacchetti compatibili con SemVer 1.0.0 che SemVer 2.0.0. Per ulteriori informazioni, vedere il [supporto di SemVer 2.0.0 per NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Risposta

La risposta è un documento JSON che contiene `take` i risultati di completamento automatico.

L'oggetto JSON radice presenta le proprietà seguenti:

NOME      | Type             | Obbligatoria | Note
--------- | ---------------- | -------- | -----
totalHits | integer          | sì      | Il numero totale di corrispondenze, che `skip` non riguardano e`take`
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

Name        | In     | Type    | Obbligatoria | Note
----------- | ------ | ------- | -------- | -----
id          | URL    | string  | sì      | ID del pacchetto per cui recuperare le versioni
prerelease  | URL    | boolean | no       | `true`o `false` determinare se includere i [pacchetti in versione non definitiva](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | no       | Una stringa di versione SemVer 2.0.0 

Se `prerelease` non viene specificato, i pacchetti di versioni non definitive vengono esclusi.

Il `semVerLevel` parametro di query viene usato per acconsentire esplicitamente ai pacchetti SemVer 2.0.0. Se questo parametro di query è escluso, verranno restituite solo le versioni SemVer 1.0.0. Se `semVerLevel=2.0.0` viene specificato, verranno restituite sia le versioni SemVer 1.0.0 che SemVer 2.0.0. Per ulteriori informazioni, vedere il [supporto di SemVer 2.0.0 per NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Risposta

La risposta è un documento JSON contenente tutte le versioni dei pacchetti dell'ID pacchetto specificato, filtrando in base ai parametri di query specificati.

L'oggetto JSON radice presenta la proprietà seguente:

Name      | Type             | Obbligatoria | Note
--------- | ---------------- | -------- | -----
data      | matrice di stringhe | sì      | Versioni del pacchetto corrispondenti alla richiesta

Le versioni del pacchetto nella `data` matrice possono contenere i metadati di compilazione SemVer 2.0.0 ( `1.0.0+metadata`ad esempio) `semVerLevel=2.0.0` se è specificato nella stringa di query.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
