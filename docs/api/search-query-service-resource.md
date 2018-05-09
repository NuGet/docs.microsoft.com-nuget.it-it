---
title: Ricerca, NuGet API
description: Il servizio di ricerca consente ai client di query per i pacchetti dalla parola chiave e per i risultati del filtro su determinati campi pacchetto.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 76600ee916305ee01ddfb675c83c184e980c5a42
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="search"></a>Cerca

È possibile cercare i pacchetti disponibili su un'origine del pacchetto tramite l'API V3. La risorsa utilizzata per la ricerca di `SearchQueryService` risorsa trovata nel [indice servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

Nell'esempio `@type` vengono utilizzati i valori:

Valore di @type                   | Note
----------------------------- | -----
SearchQueryService            | La versione iniziale
SearchQueryService/3.0.0-beta | Alias di `SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias di `SearchQueryService`

## <a name="base-url"></a>URL di base

L'URL di base per l'API seguente è il valore di `@id` proprietà associati a uno della risorsa menzionati in precedenza `@type` valori. Nel documento seguente, il segnaposto URL di base `{@id}` verrà utilizzato.

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL trovati, il supporto di risorsa di registrazione, i metodi HTTP `GET` e `HEAD`.

## <a name="search-for-packages"></a>Ricerca per i pacchetti

L'API di ricerca consente al client per eseguire query per una pagina di pacchetti corrispondenti a una query di ricerca specificato. L'interpretazione della query di ricerca (ad esempio, la suddivisione in token i termini di ricerca) è determinata dall'implementazione del server, ma l'aspettativa generale è che la query di ricerca viene utilizzata per l'ID di pacchetto, titoli, descrizioni e tag corrispondenti. Possono anche essere considerate altri campi di metadati del pacchetto.

Un pacchetto non in elenco devono essere mai presenti nei risultati della ricerca.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametri della richiesta

nome        | In     | Tipo    | Obbligatorio | Note
----------- | ------ | ------- | -------- | -----
q           | URL    | stringa  | No       | I termini di ricerca da utilizzare per i pacchetti di filtro
skip        | URL    | numero intero | No       | Il numero di risultati da ignorare per l'impaginazione
Take        | URL    | numero intero | No       | Il numero di risultati da restituire, per la paginazione
versione provvisoria  | URL    | boolean | No       | `true` o `false` determinano l'opportunità di includere [pacchetti versione non definitiva](../create-packages/prerelease-packages.md)
semVerLevel | URL    | stringa  | No       | Una stringa di versione SemVer 1.0.0 

La query di ricerca `q` viene analizzato in modo che è definito dall'implementazione del server. NuGet.org supporta i filtri di base su un [diversi campi di](../consume-packages/finding-and-choosing-packages.md#search-syntax). Se non `q` viene fornito, devono essere restituiti tutti i pacchetti, entro i limiti imposti da skip e take. In questo modo la scheda "Sfoglia" nell'esperienza NuGet di Visual Studio.

Il `skip` valori predefiniti dei parametri su 0.

Il `take` parametro deve essere un numero intero maggiore di zero. L'implementazione del server potrebbe avere un valore massimo.

Se `prerelease` non viene fornito, vengono esclusi i pacchetti pre-release.

Il `semVerLevel` parametro di query viene utilizzato per acconsentire esplicitamente a [SemVer 2.0.0 pacchetti](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Se questo parametro di query viene esclusa, verranno restituiti solo i pacchetti con le versioni compatibili SemVer 1.0.0 (con il [standard controllo delle versioni NuGet](../reference/package-versioning.md) avvertenze, ad esempio le stringhe di versione con 4 elementi di tipo integer).
Se `semVerLevel=2.0.0` viene fornito, verranno restituiti SemVer 1.0.0 sia pacchetti compatibili SemVer 2.0.0. Vedere il [supporto SemVer 2.0.0 per nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) per ulteriori informazioni.

### <a name="response"></a>Risposta

La risposta è il documento JSON che contiene fino a `take` i risultati della ricerca. I risultati della ricerca sono raggruppati per ID del pacchetto.

Oggetto JSON radice ha le proprietà seguenti:

nome      | Tipo             | Obbligatorio | Note
--------- | ---------------- | -------- | -----
totalHits | numero intero          | sì      | Il numero complessivo di corrispondenze, non considerando `skip` e `take`
Data      | Matrice di oggetti | sì      | I risultati della ricerca corrispondenti a richiesta

### <a name="search-result"></a>risultato della ricerca

Ogni elemento di `data` matrice è un oggetto JSON costituito da un gruppo di versioni del pacchetto condividere lo stesso ID di pacchetto.
L'oggetto ha le proprietà seguenti:

nome           | Tipo                       | Obbligatorio | Note
-------------- | -------------------------- | -------- | -----
ID             | stringa                     | sì      | L'ID del pacchetto corrispondente
version        | stringa                     | sì      | La stringa di versione SemVer 2.0.0 completa del pacchetto (può contenere i metadati di compilazione)
Descrizione    | stringa                     | No       | 
versioni       | Matrice di oggetti           | sì      | Tutte le versioni del pacchetto corrispondente il `prerelease` parametro
authors        | stringa o matrice di stringhe | No       | 
iconUrl        | stringa                     | No       | 
licenseUrl     | stringa                     | No       | 
owners         | stringa o matrice di stringhe | No       | 
projectUrl     | stringa                     | No       | 
registrazione   | stringa                     | No       | L'URL assoluto all'oggetto associato [indice registrazione](registration-base-url-resource.md#registration-index)
summary        | stringa                     | No       | 
tag           | stringa o matrice di stringhe | No       | 
title          | stringa                     | No       | 
totalDownloads | numero intero                    | No       | Questo valore può essere dedotto per la somma di download di `versions` matrice
Verificato       | boolean                    | No       | Valore booleano JSON che indica se il pacchetto è [verificato](../reference/id-prefix-reservation.md)

In nuget.org, un pacchetto verificato è quello che ha un ID di pacchetto corrispondente prefisso ID riservato e proprietà di uno dei proprietari di spazio dei nomi riservato. Per ulteriori informazioni, vedere il [documentazione sulla prenotazione di prefisso ID](../reference/id-prefix-reservation.md).

I metadati contenuti nell'oggetto risultato di ricerca da cui proviene la versione più recente del pacchetto. Ogni elemento di `versions` matrice è un oggetto JSON con le proprietà seguenti:

nome      | Tipo    | Obbligatorio | Note
--------- | ------- | -------- | -----
@id       | stringa  | sì      | L'URL assoluto all'oggetto associato [foglia di registrazione](registration-base-url-resource.md#registration-leaf)
version   | stringa  | sì      | La stringa di versione SemVer 2.0.0 completa del pacchetto (può contenere i metadati di compilazione)
Scarica | numero intero | sì      | Il numero di download per questa versione del pacchetto specifico

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [search-result.json](./_data/search-result.json)]
