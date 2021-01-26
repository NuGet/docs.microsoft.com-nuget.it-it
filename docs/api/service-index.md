---
title: Indice del servizio, API NuGet
description: L'indice del servizio è il punto di ingresso dell'API HTTP NuGet ed enumera le funzionalità del server.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775363"
---
# <a name="service-index"></a>Indice dei servizi

L'indice del servizio è un documento JSON che rappresenta il punto di ingresso per un'origine del pacchetto NuGet e consente a un'implementazione client di individuare le funzionalità dell'origine del pacchetto. L'indice del servizio è un oggetto JSON con due proprietà obbligatorie: `version` (la versione dello schema dell'indice del servizio) e `resources`  (gli endpoint o le funzionalità dell'origine del pacchetto).

l'indice del servizio NuGet. org si trova in `https://api.nuget.org/v3/index.json` .

## <a name="versioning"></a>Controllo delle versioni

Il `version` valore è una stringa di versione analizzabile SemVer 2.0.0 che indica la versione dello schema dell'indice del servizio. L'API impone che la stringa di versione abbia un numero di versione principale di `3` . Quando vengono apportate modifiche non di rilievo allo schema dell'indice del servizio, viene aumentata la versione secondaria della stringa di versione.

Ogni risorsa nell'indice del servizio viene sottoversione indipendentemente dalla versione dello schema dell'indice del servizio.

La versione corrente dello schema è `3.0.0` . La `3.0.0` versione è funzionalmente equivalente alla `3.0.0-beta.1` versione precedente, ma deve essere preferita perché comunica più chiaramente lo schema stabile e definito.

## <a name="http-methods"></a>Metodi HTTP

L'indice del servizio è accessibile tramite metodi HTTP `GET` e `HEAD` .

## <a name="resources"></a>Risorse

La `resources` proprietà contiene una matrice di risorse supportate dall'origine del pacchetto.

### <a name="resource"></a>Risorsa

Una risorsa è un oggetto nella `resources` matrice. Rappresenta una funzionalità con versione di un'origine del pacchetto. Una risorsa presenta le proprietà seguenti:

Nome          | Type   | Necessario | Note
------------- | ------ | -------- | -----
@id           | string | sì      | URL della risorsa
@type         | string | sì      | Costante di stringa che rappresenta il tipo di risorsa
comment       | string | no       | Descrizione leggibile della risorsa

`@id`È un URL che deve essere assoluto e deve avere lo schema http o HTTPS.

`@type`Viene usato per identificare il protocollo specifico da usare quando si interagisce con la risorsa. Il tipo della risorsa è una stringa opaca, ma in genere presenta il formato seguente:

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

Si prevede che i client `@type` consentano di codificare in modo rigido i valori che conoscono e li cercano nell'indice del servizio di un'origine del pacchetto. I `@type` valori esatti attualmente in uso vengono enumerati nei singoli documenti di riferimento delle risorse elencati nella [Panoramica dell'API](overview.md#resources-and-schema).

Ai fini di questa documentazione, la documentazione relativa alle diverse risorse verrà essenzialmente raggruppata in base all'oggetto `{RESOURCE_NAME}` rilevato nell'indice del servizio, che è analogo al raggruppamento in base allo scenario. 

Non è necessario che ogni risorsa abbia un o univoco `@id` `@type` . Spetta all'implementazione client determinare la risorsa da preferire rispetto a un'altra. Una possibile implementazione è che le risorse dello stesso o compatibili `@type` possono essere utilizzate in modo round robin in caso di errore di connessione o errore del server.

### <a name="sample-request"></a>Richiesta di esempio

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [service-index.json](./_data/service-index.json)]
