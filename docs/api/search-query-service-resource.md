---
title: Ricerca di API NuGet
description: Il servizio di ricerca consente ai client di query per i pacchetti dalla parola chiave e per filtrare i risultati in determinati campi del pacchetto.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d462b289c39c2dd1418304dabcad47d0d4217f82
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426738"
---
# <a name="search"></a>Cerca

È possibile cercare i pacchetti disponibili in un'origine del pacchetto tramite l'API di V3. La risorsa usata per la ricerca è il `SearchQueryService` trovare la risorsa nella [indice del servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

Nell'esempio `@type` vengono utilizzati i valori:

Valore di@type                   | Note
----------------------------- | -----
SearchQueryService            | La versione iniziale
SearchQueryService/3.0.0-beta | Alias di `SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias di `SearchQueryService`

## <a name="base-url"></a>URL di base

L'URL di base per l'API seguente è il valore della `@id` proprietà associati a uno della risorsa menzionati in precedenza `@type` valori. Nel documento seguente, il segnaposto URL di base `{@id}` verrà utilizzato.

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL disponibili il supporto di risorse di registrazione i metodi HTTP `GET` e `HEAD`.

## <a name="search-for-packages"></a>Ricerca di pacchetti

L'API di ricerca consente a un client per eseguire query per una pagina di pacchetti corrispondono a una query di ricerca specificati. L'interpretazione della query di ricerca (ad esempio, la suddivisione in token i termini di ricerca) è determinata dall'implementazione del server, ma l'aspettativa generale è che la query di ricerca viene usata per la corrispondenza degli ID di pacchetto, titoli, descrizioni e tag. Possono essere considerate anche gli altri campi di metadati del pacchetto.

Un package non in elenco dovrebbe essere mai visualizzato nei risultati della ricerca.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametri della richiesta

Nome        | In     | Tipo    | Obbligatorio | Note
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | No       | I termini di ricerca da utilizzare per i pacchetti di filtro
skip        | URL    | numero intero | No       | Il numero di risultati da ignorare, per la paginazione
Take        | URL    | numero intero | No       | Il numero di risultati da restituire, per la paginazione
versione preliminare  | URL    | boolean | No       | `true` oppure `false` che determina se includere [i pacchetti di versioni non definitive](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | No       | Una stringa di versione SemVer 1.0.0 

La query di ricerca `q` viene analizzato in modo che è definito dall'implementazione del server. NuGet.org supporta i filtri di base in un [numerosi campi](../consume-packages/finding-and-choosing-packages.md#search-syntax). Se nessun `q` è specificato, tutti i pacchetti dovrebbero essere restituiti, entro i limiti imposti dal skip e take. In questo modo la scheda "Sfoglia" nell'esperienza di NuGet di Visual Studio.

Il `skip` valori predefiniti dei parametri su 0.

Il `take` parametro deve essere un numero intero maggiore di zero. L'implementazione del server può imporre un valore massimo.

Se `prerelease` non viene specificato, vengono esclusi i pacchetti in versione non definitiva.

Il `semVerLevel` parametro di query viene utilizzato per acconsentire [pacchetti di SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Se questo parametro di query è stata esclusa, verranno restituiti solo i pacchetti con le versioni compatibili di SemVer 1.0.0 (con il [controllo delle versioni NuGet standard](../reference/package-versioning.md) avvertenze, ad esempio le stringhe di versione con 4 elementi integer).
Se `semVerLevel=2.0.0` viene fornito, verranno restituiti SemVer 1.0.0 sia pacchetti compatibili di SemVer 2.0.0. Vedere le [supporto di SemVer 2.0.0 per nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) per altre informazioni.

### <a name="response"></a>Risposta

La risposta è il documento JSON che contiene fino a `take` i risultati della ricerca. I risultati della ricerca sono raggruppati per ID del pacchetto.

L'oggetto JSON radice ha le proprietà seguenti:

Nome      | Tipo             | Obbligatorio | Note
--------- | ---------------- | -------- | -----
totalHits | numero intero          | sì      | Il numero complessivo di corrispondenze, ignorando `skip` e `take`
Data      | Matrice di oggetti | sì      | I risultati della ricerca trovare una corrispondenza con la richiesta

### <a name="search-result"></a>Risultato della ricerca

Ogni elemento di `data` matrice è un oggetto JSON costituito da un gruppo di versioni del pacchetto condividere lo stesso ID di pacchetto.
L'oggetto presenta le proprietà seguenti:

Nome           | Tipo                       | Obbligatorio | Note
-------------- | -------------------------- | -------- | -----
ID             | string                     | sì      | L'ID del pacchetto corrispondente
version        | string                     | sì      | La stringa di versione SemVer 2.0.0 completa del pacchetto (può contenere i metadati di compilazione)
Descrizione    | string                     | No       | 
versioni       | Matrice di oggetti           | sì      | Tutte le versioni dei pacchetti corrispondenti di `prerelease` parametro
authors        | stringa o matrice di stringhe | No       | 
iconUrl        | string                     | No       | 
licenseUrl     | string                     | No       | 
owners         | stringa o matrice di stringhe | No       | 
projectUrl     | string                     | No       | 
registrazione   | string                     | No       | L'URL assoluto associati [indice registrazione](registration-base-url-resource.md#registration-index)
summary        | string                     | No       | 
tag           | stringa o matrice di stringhe | No       | 
title          | string                     | No       | 
totalDownloads | numero intero                    | No       | Questo valore può essere dedotto dalla somma del download nel `versions` matrice
verificato       | boolean                    | No       | Valore booleano JSON, che indica se il pacchetto è [verificato](../nuget-org/id-prefix-reservation.md)

In nuget.org, un pacchetto verificato è quello che ha un ID di pacchetto corrispondente prefisso ID riservato e di proprietà di uno dei proprietari del prefisso riservato. Per altre informazioni, vedere la [documentazione sulla prenotazione del prefisso ID](../reference/id-prefix-reservation.md).

I metadati contenuti nell'oggetto risultato di ricerca da cui proviene la versione più recente del pacchetto. Ogni elemento di `versions` matrice è un oggetto JSON con le proprietà seguenti:

Nome      | Tipo    | Obbligatorio | Note
--------- | ------- | -------- | -----
@id       | string  | sì      | L'URL assoluto associati [foglia di registrazione](registration-base-url-resource.md#registration-leaf)
version   | string  | sì      | La stringa di versione SemVer 2.0.0 completa del pacchetto (può contenere i metadati di compilazione)
Download | numero intero | sì      | Il numero di download per questa versione del pacchetto specifico

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [search-result.json](./_data/search-result.json)]
