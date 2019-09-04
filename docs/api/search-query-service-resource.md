---
title: Ricerca, API NuGet
description: Il servizio di ricerca consente ai client di eseguire query per i pacchetti in base alla parola chiave e di filtrare i risultati in determinati campi del pacchetto.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: be25e9bf72b9115de8ae55f6296195fed3152f10
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235121"
---
# <a name="search"></a>Cerca

È possibile cercare i pacchetti disponibili in un'origine pacchetto usando l'API V3. La risorsa utilizzata per la ricerca è `SearchQueryService` la risorsa trovata nell' [indice del servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

Vengono usati `@type` i valori seguenti:

Valore di @type                   | Note
----------------------------- | -----
SearchQueryService            | Versione iniziale
SearchQueryService/3.0.0-beta | Alias di`SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias di`SearchQueryService`

## <a name="base-url"></a>URL di base

L'URL di base per l'API seguente è il valore della `@id` proprietà associata a uno dei valori di risorsa `@type` menzionati sopra. Nel documento seguente verrà usato l'URL `{@id}` di base segnaposto.

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL trovati nella risorsa di registrazione supportano i metodi `GET` http `HEAD`e.

## <a name="search-for-packages"></a>Cerca pacchetti

L'API di ricerca consente a un client di eseguire una query per una pagina di pacchetti corrispondente a una query di ricerca specificata. L'interpretazione della query di ricerca, ad esempio la suddivisione in token dei termini di ricerca, è determinata dall'implementazione del server, ma l'aspettativa generale è che la query di ricerca viene utilizzata per la corrispondenza tra ID, titoli, descrizioni e tag del pacchetto. È possibile considerare anche altri campi di metadati del pacchetto.

Un pacchetto non in elenco non dovrebbe mai apparire nei risultati della ricerca.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametri della richiesta

NOME        | In     | Type    | Obbligatoria | Note
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | no       | Termini di ricerca da utilizzare per filtrare i pacchetti
skip        | URL    | integer | no       | Numero di risultati da ignorare per la paginazione
prendere        | URL    | integer | no       | Numero di risultati da restituire per la paginazione
prerelease  | URL    | boolean | no       | `true`o `false` determinare se includere i [pacchetti in versione non definitiva](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | no       | Una stringa di versione SemVer 1.0.0 

La query `q` di ricerca viene analizzata in modo definito dall'implementazione del server. nuget.org supporta l'applicazione di filtri [di base a diversi campi](../consume-packages/finding-and-choosing-packages.md#search-syntax). Se non `q` viene specificato alcun oggetto, verranno restituiti tutti i pacchetti entro i limiti imposti da Skip e Take. In questo modo viene abilitata la scheda "Sfoglia" nell'esperienza NuGet di Visual Studio.

Il `skip` valore predefinito del parametro è 0.

Il `take` parametro deve essere un numero intero maggiore di zero. L'implementazione del server può imporre un valore massimo.

Se `prerelease` non viene specificato, i pacchetti di versioni non definitive vengono esclusi.

Il `semVerLevel` parametro di query viene usato per acconsentire esplicitamente ai [pacchetti SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Se questo parametro di query è escluso, verranno restituiti solo i pacchetti con versioni compatibili con SemVer 1.0.0 (con le avvertenze per il [controllo delle versioni di NuGet standard](../concepts/package-versioning.md) , ad esempio le stringhe di versione con 4 parti Integer).
Se `semVerLevel=2.0.0` viene specificato, verranno restituiti sia i pacchetti compatibili con SemVer 1.0.0 che SemVer 2.0.0. Per ulteriori informazioni, vedere il [supporto di SemVer 2.0.0 per NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Risposta

La risposta è un documento JSON contenente fino `take` ai risultati della ricerca. I risultati della ricerca sono raggruppati in base all'ID del pacchetto.

L'oggetto JSON radice presenta le proprietà seguenti:

NOME      | Type             | Obbligatoria | Note
--------- | ---------------- | -------- | -----
totalHits | integer          | sì      | Il numero totale di corrispondenze, che `skip` non riguardano e`take`
data      | matrice di oggetti | sì      | Risultati della ricerca corrispondenti alla richiesta

### <a name="search-result"></a>Risultato della ricerca

Ogni elemento nella `data` matrice è un oggetto JSON costituito da un gruppo di versioni del pacchetto che condividono lo stesso ID pacchetto.
L'oggetto ha le proprietà seguenti:

Name           | Type                       | Obbligatoria | Note
-------------- | -------------------------- | -------- | -----
id             | string                     | sì      | ID del pacchetto corrispondente
version        | string                     | sì      | Stringa di versione SemVer 2.0.0 completa del pacchetto (potrebbe contenere metadati di compilazione)
description    | string                     | no       | 
versioni       | matrice di oggetti           | sì      | Tutte le versioni del pacchetto che corrispondono al `prerelease` parametro
authors        | stringa o matrice di stringhe | no       | 
iconUrl        | string                     | no       | 
licenseUrl     | string                     | no       | 
owners         | stringa o matrice di stringhe | no       | 
projectUrl     | string                     | no       | 
registrazione   | string                     | no       | URL assoluto dell' [indice di registrazione](registration-base-url-resource.md#registration-index) associato
summary        | string                     | no       | 
tags           | stringa o matrice di stringhe | no       | 
title          | string                     | no       | 
totalDownloads | integer                    | no       | Questo valore può essere dedotto dalla somma dei download nella `versions` matrice
verificato       | boolean                    | no       | Valore booleano JSON che indica se il pacchetto è [verificato](../nuget-org/id-prefix-reservation.md)

In nuget.org, un pacchetto verificato è uno che dispone di un ID pacchetto corrispondente a un prefisso ID riservato e di proprietà di uno dei proprietari del prefisso riservato. Per ulteriori informazioni, vedere la [documentazione relativa alla prenotazione del prefisso ID](../reference/id-prefix-reservation.md).

I metadati contenuti nell'oggetto risultato della ricerca sono ricavati dalla versione più recente del pacchetto. Ogni elemento nella `versions` matrice è un oggetto JSON con le proprietà seguenti:

NOME      | Type    | Obbligatoria | Note
--------- | ------- | -------- | -----
@id       | string  | sì      | URL assoluto della [foglia di registrazione](registration-base-url-resource.md#registration-leaf) associata
version   | string  | sì      | Stringa di versione SemVer 2.0.0 completa del pacchetto (potrebbe contenere metadati di compilazione)
Download | integer | sì      | Numero di download per la versione specifica del pacchetto

### <a name="sample-request"></a>Richiesta di esempio

    GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [search-result.json](./_data/search-result.json)]
