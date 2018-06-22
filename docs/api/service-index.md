---
title: Indice del servizio, NuGet API
description: L'indice di servizio è il punto di ingresso dell'API HTTP NuGet e vengono elencate le funzionalità del server.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 84e623e8480e4d17edad2ec3b2da6dcb6e53d21b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822094"
---
# <a name="service-index"></a>Indice del servizio

L'indice di servizio è un documento JSON che è il punto di ingresso per un'origine del pacchetto NuGet e consente a un'implementazione client di individuare le funzionalità dell'origine del pacchetto. L'indice di servizio è un oggetto JSON con due proprietà obbligatorie: `version` (la versione dello schema dell'indice del servizio) e `resources` (endpoint o funzionalità di origine del pacchetto).

indice del servizio di NuGet.org si trova in `https://api.nuget.org/v3/index.json`.

## <a name="versioning"></a>Controllo delle versioni

Il `version` valore è una stringa di versione analizzabili SemVer 2.0.0 che indica la versione dello schema dell'indice del servizio. L'API richiede che la stringa di versione è un numero di versione principale `3`. Al momento non modifiche allo schema di indice del servizio, versione secondaria della stringa di versione verrà aumentato.

Ogni risorsa in corrispondenza dell'indice del servizio viene creata indipendentemente dalla versione dello schema di indice del servizio.

La versione dello schema corrente è `3.0.0`. Il `3.0.0` è funzionalmente equivalente alla precedente versione `3.0.0-beta.1` versione ma deve essere preferito in quanto più chiaramente comunica lo schema stabile, definito.

## <a name="http-methods"></a>Metodi HTTP

L'indice di servizio è accessibile tramite i metodi HTTP `GET` e `HEAD`.

## <a name="resources"></a>Risorse

Il `resources` proprietà contiene una matrice di risorse, supportati da questa origine del pacchetto.

### <a name="resource"></a>Risorsa

Una risorsa è un oggetto di `resources` matrice. Rappresenta una funzionalità con controllo delle versioni di un'origine pacchetto. Una risorsa ha le proprietà seguenti:

nome          | Tipo   | Obbligatorio | Note
------------- | ------ | -------- | -----
@id           | stringa | sì      | L'URL della risorsa
@type         | stringa | sì      | Costante stringa che rappresenta il tipo di risorsa
commento       | stringa | No       | Descrizione leggibile della risorsa

Il `@id` è un URL che deve essere assoluto e deve avere lo schema HTTP o HTTPS.

Il `@type` viene utilizzato per identificare il protocollo specifico da utilizzare durante l'interazione con la risorsa. Il tipo della risorsa è una stringa opaca ma in genere ha il formato:

    {RESOURCE_NAME}/{RESOURCE_VERSION}

Si prevede che i client a livello di codice il `@type` valori comprendere e cercare nell'indice di un'origine del pacchetto servizio. L'esatto `@type` vengono enumerati i valori attualmente in uso nei documenti di riferimento delle singole risorse elencati nel [panoramica dell'API](overview.md#resources-and-schema).

Ai fini di questa documentazione, la documentazione relativa alle diverse risorse verrà essenzialmente raggruppata per il `{RESOURCE_NAME}` trovato nell'indice servizio analogo al raggruppamento dallo scenario. 

Non è necessario che ogni risorsa è univoca `@id` o `@type`. In questo caso, l'implementazione del client per determinare quale risorsa scegliere da preferire un altro. Una possibile implementazione è che le risorse dello stesso o compatibile `@type` può essere usato in uno schema round-robin in caso di errore di server o errore di connessione.

### <a name="sample-request"></a>Richiesta di esempio

OTTIENI https://api.nuget.org/v3/index.json

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [service-index.json](./_data/service-index.json)]
