---
title: Indice del servizio, API NuGet
description: L'indice del servizio è il punto di ingresso dell'API HTTP NuGet e vengono elencate le funzionalità del server.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1dcfb87690b728280b494d4434f9c1d7ee7a7e74
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324721"
---
# <a name="service-index"></a>Indice del servizio

L'indice del servizio è un documento JSON che rappresenta il punto di ingresso per un'origine del pacchetto NuGet e consente un'implementazione del client individuare le funzionalità dell'origine del pacchetto. L'indice del servizio è un oggetto JSON con due proprietà obbligatorie: `version` (la versione dello schema dell'indice del servizio) e `resources` (gli endpoint o le funzionalità dell'origine del pacchetto).

indice del servizio di NuGet.org è disponibile all'indirizzo `https://api.nuget.org/v3/index.json`.

## <a name="versioning"></a>Controllo delle versioni

Il `version` valore è una stringa di versione analizzabili SemVer 2.0.0, che indica la versione dello schema dell'indice del servizio. L'API di utilizzo, è necessario che la stringa di versione abbia un numero di versione principale `3`. Quando vengono apportate modifiche non di rilievo allo schema di indice del servizio, versione secondaria della stringa di versione verrà aumentato.

Ogni risorsa l'indice del servizio è con controllo delle versioni in modo indipendente dalla versione dello schema dell'indice del servizio.

La versione dello schema corrente è `3.0.0`. Il `3.0.0` versione è funzionalmente equivalente al precedente `3.0.0-beta.1` versione ma dovrebbe essere preferito in quanto comunica in modo più chiaro lo schema stabile, definito.

## <a name="http-methods"></a>Metodi HTTP

L'indice del servizio è accessibile tramite i metodi HTTP `GET` e `HEAD`.

## <a name="resources"></a>Risorse

Il `resources` proprietà contiene una matrice di risorse supportati da questa origine pacchetto.

### <a name="resource"></a>Risorsa

Una risorsa è un oggetto di `resources` matrice. Rappresenta una funzionalità con controllo delle versioni di un'origine del pacchetto. Una risorsa ha le proprietà seguenti:

nome          | Tipo   | Obbligatorio | Note
------------- | ------ | -------- | -----
@id           | stringa | sì      | L'URL della risorsa
@type         | stringa | sì      | Costante stringa che rappresenta il tipo di risorsa
commento       | stringa | No       | Descrizione leggibile della risorsa

Il `@id` è un URL che deve essere assoluto e deve avere lo schema HTTP o HTTPS.

Il `@type` viene usato per identificare il protocollo specifico da usare quando si interagisce con la risorsa. Il tipo della risorsa è una stringa opaca, ma in genere ha il formato:

    {RESOURCE_NAME}/{RESOURCE_VERSION}

I client è previsto a livello di codice il `@type` valori che comprendere e cercarli in indice del servizio di origine del pacchetto. L'esatto `@type` vengono enumerati i valori attualmente in uso nei documenti di riferimento delle singole risorse elencati nel [Cenni preliminari sull'API](overview.md#resources-and-schema).

Ai fini di questa documentazione, la documentazione relativa a diverse risorse verrà essenzialmente raggruppata per il `{RESOURCE_NAME}` trovato nell'indice servizio analogo al raggruppamento dallo scenario. 

Non è necessario che ogni risorsa dispone di un valore univoco `@id` o `@type`. È responsabilità dell'implementazione client per determinare quale risorsa scegliere da preferire rispetto a un altro. Una possibile implementazione è che le risorse con lo stesso o compatibile `@type` può essere usato in modo round robin in caso di errore di server o di errore di connessione.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3/index.json

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [service-index.json](./_data/service-index.json)]
