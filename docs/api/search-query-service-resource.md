---
title: Ricerca, API NuGet
description: Il servizio di ricerca consente ai client di eseguire query per i pacchetti in base alla parola chiave e di filtrare i risultati in determinati campi del pacchetto.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 86c9d07cf90b84fffd09b04847d41772dd633b98
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237874"
---
# <a name="search"></a>Cerca

È possibile cercare i pacchetti disponibili in un'origine pacchetto usando l'API V3. La risorsa utilizzata per la ricerca è la `SearchQueryService` risorsa trovata nell' [indice del servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

`@type`Vengono usati i valori seguenti:

Valore della proprietà @type                   | Note
----------------------------- | -----
SearchQueryService            | Versione iniziale
SearchQueryService/3.0.0-beta | Alias di `SearchQueryService`
SearchQueryService/3.0.0-RC   | Alias di `SearchQueryService`
SearchQueryService/3.5.0      | Include il supporto per il `packageType` parametro di query

### <a name="searchqueryservice350"></a>SearchQueryService/3.5.0
Questa versione introduce il supporto per il `packageType` parametro di query e la `packageTypes` proprietà Response, consentendo il filtraggio in base ai tipi di pacchetti definiti dall'autore. È completamente compatibile con le query in `SearchQueryService` .

## <a name="base-url"></a>URL di base

L'URL di base per l'API seguente è il valore della `@id` proprietà associata a uno dei valori di risorsa menzionati sopra `@type` . Nel documento seguente verrà usato l'URL di base segnaposto `{@id}` .

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL trovati nella risorsa di registrazione supportano i metodi HTTP `GET` e `HEAD` .

## <a name="search-for-packages"></a>Cerca pacchetti

L'API di ricerca consente a un client di eseguire una query per una pagina di pacchetti corrispondente a una query di ricerca specificata. L'interpretazione della query di ricerca, ad esempio la suddivisione in token dei termini di ricerca, è determinata dall'implementazione del server, ma l'aspettativa generale è che la query di ricerca viene utilizzata per la corrispondenza tra ID, titoli, descrizioni e tag del pacchetto. È possibile considerare anche altri campi di metadati del pacchetto.

Un pacchetto non in elenco non dovrebbe mai apparire nei risultati della ricerca.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}

### <a name="request-parameters"></a>Parametri della richiesta

Nome        | In     | Type    | Obbligatoria | Note
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | no       | Termini di ricerca da utilizzare per filtrare i pacchetti
skip        | URL    | integer | no       | Numero di risultati da ignorare per la paginazione
take        | URL    | integer | no       | Numero di risultati da restituire per la paginazione
prerelease  | URL    | boolean | no       | `true` o `false` determinare se includere i [pacchetti in versione non definitiva](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | no       | Una stringa di versione SemVer 1.0.0 
packageType | URL    | string  | no       | Tipo di pacchetto da utilizzare per filtrare i pacchetti (aggiunti in `SearchQueryService/3.5.0` )

La query di ricerca `q` viene analizzata in modo definito dall'implementazione del server. nuget.org supporta l'applicazione di filtri [di base a diversi campi](../consume-packages/finding-and-choosing-packages.md#search-syntax). Se non `q` viene specificato alcun oggetto, verranno restituiti tutti i pacchetti entro i limiti imposti da Skip e Take. In questo modo viene abilitata la scheda "Sfoglia" nell'esperienza NuGet di Visual Studio.

Il `skip` valore predefinito del parametro è 0.

Il `take` parametro deve essere un numero intero maggiore di zero. L'implementazione del server può imporre un valore massimo.

Se `prerelease` non viene specificato, i pacchetti di versioni non definitive vengono esclusi.

Il `semVerLevel` parametro di query viene usato per acconsentire esplicitamente ai [pacchetti SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Se questo parametro di query è escluso, verranno restituiti solo i pacchetti con versioni compatibili con SemVer 1.0.0 (con le avvertenze per il [controllo delle versioni di NuGet standard](../concepts/package-versioning.md) , ad esempio le stringhe di versione con 4 parti Integer).
Se `semVerLevel=2.0.0` viene specificato, verranno restituiti sia i pacchetti compatibili con SemVer 1.0.0 che SemVer 2.0.0. Per ulteriori informazioni, vedere il [supporto di SemVer 2.0.0 per NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

Il `packageType` parametro viene utilizzato per filtrare ulteriormente i risultati della ricerca solo per i pacchetti che hanno almeno un tipo di pacchetto corrispondente al nome del tipo di pacchetto.
Se il tipo di pacchetto specificato non è un tipo di pacchetto valido come definito dal [documento del tipo di pacchetto](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), verrà restituito un risultato vuoto.
Se il tipo di pacchetto fornito è vuoto, non verrà applicato alcun filtro. In altre parole, il passaggio di nessun valore al parametro packageType si comporterà come se il parametro non venisse passato.

### <a name="response"></a>Risposta

La risposta è un documento JSON contenente fino ai `take` Risultati della ricerca. I risultati della ricerca sono raggruppati in base all'ID del pacchetto.

L'oggetto JSON radice presenta le proprietà seguenti:

Nome      | Type             | Obbligatoria | Note
--------- | ---------------- | -------- | -----
totalHits | integer          | yes      | Il numero totale di corrispondenze, che non riguardano `skip` e `take`
Data      | matrice di oggetti | yes      | Risultati della ricerca corrispondenti alla richiesta

### <a name="search-result"></a>Risultato della ricerca

Ogni elemento nella `data` matrice è un oggetto JSON costituito da un gruppo di versioni del pacchetto che condividono lo stesso ID pacchetto.
L'oggetto ha le proprietà seguenti:

Nome           | Type                       | Obbligatoria | Note
-------------- | -------------------------- | -------- | -----
id             | string                     | yes      | ID del pacchetto corrispondente
version        | string                     | yes      | Stringa di versione SemVer 2.0.0 completa del pacchetto (potrebbe contenere metadati di compilazione)
description    | string                     | no       | 
versions       | matrice di oggetti           | yes      | Tutte le versioni del pacchetto che corrispondono al `prerelease` parametro
authors        | Stringa o matrice di stringhe | no       | 
iconUrl        | string                     | no       | 
licenseUrl     | string                     | no       | 
owners         | Stringa o matrice di stringhe | no       | 
projectUrl     | string                     | no       | 
registrazione   | string                     | no       | URL assoluto dell' [indice di registrazione](registration-base-url-resource.md#registration-index) associato
riepilogo        | string                     | no       | 
tags           | Stringa o matrice di stringhe | no       | 
title          | string                     | no       | 
totalDownloads | integer                    | no       | Questo valore può essere dedotto dalla somma dei download nella `versions` matrice
verificato       | boolean                    | no       | Valore booleano JSON che indica se il pacchetto è [verificato](../nuget-org/id-prefix-reservation.md)
packageTypes   | matrice di oggetti           | yes      | Tipi di pacchetto definiti dall'autore del pacchetto (aggiunti in `SearchQueryService/3.5.0` )

In nuget.org, un pacchetto verificato è uno che dispone di un ID pacchetto corrispondente a un prefisso ID riservato e di proprietà di uno dei proprietari del prefisso riservato. Per ulteriori informazioni, vedere la [documentazione relativa alla prenotazione del prefisso ID](../nuget-org/id-prefix-reservation.md).

I metadati contenuti nell'oggetto risultato della ricerca sono ricavati dalla versione più recente del pacchetto. Ogni elemento nella `versions` matrice è un oggetto JSON con le proprietà seguenti:

Nome      | Type    | Obbligatoria | Note
--------- | ------- | -------- | -----
@id       | string  | yes      | URL assoluto della [foglia di registrazione](registration-base-url-resource.md#registration-leaf) associata
version   | string  | yes      | Stringa di versione SemVer 2.0.0 completa del pacchetto (potrebbe contenere metadati di compilazione)
Download | integer | yes      | Numero di download per la versione specifica del pacchetto

La `packageTypes` matrice è sempre costituita da almeno un elemento (1). Il tipo di pacchetto per un determinato ID pacchetto è considerato i tipi di pacchetto definiti dalla versione più recente del pacchetto rispetto agli altri parametri di ricerca. Ogni elemento nella `packageTypes` matrice è un oggetto JSON con le proprietà seguenti:

Nome      | Type    | Obbligatoria | Note
--------- | ------- | -------- | -----
name      | string  | yes      | Nome del tipo di pacchetto.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [search-result.json](./_data/search-result.json)]