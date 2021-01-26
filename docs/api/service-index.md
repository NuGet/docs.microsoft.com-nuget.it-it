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
# <a name="service-index"></a><span data-ttu-id="9f171-103">Indice dei servizi</span><span class="sxs-lookup"><span data-stu-id="9f171-103">Service index</span></span>

<span data-ttu-id="9f171-104">L'indice del servizio è un documento JSON che rappresenta il punto di ingresso per un'origine del pacchetto NuGet e consente a un'implementazione client di individuare le funzionalità dell'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9f171-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="9f171-105">L'indice del servizio è un oggetto JSON con due proprietà obbligatorie: `version` (la versione dello schema dell'indice del servizio) e `resources`  (gli endpoint o le funzionalità dell'origine del pacchetto).</span><span class="sxs-lookup"><span data-stu-id="9f171-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="9f171-106">l'indice del servizio NuGet. org si trova in `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="9f171-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="9f171-107">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="9f171-107">Versioning</span></span>

<span data-ttu-id="9f171-108">Il `version` valore è una stringa di versione analizzabile SemVer 2.0.0 che indica la versione dello schema dell'indice del servizio.</span><span class="sxs-lookup"><span data-stu-id="9f171-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="9f171-109">L'API impone che la stringa di versione abbia un numero di versione principale di `3` .</span><span class="sxs-lookup"><span data-stu-id="9f171-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="9f171-110">Quando vengono apportate modifiche non di rilievo allo schema dell'indice del servizio, viene aumentata la versione secondaria della stringa di versione.</span><span class="sxs-lookup"><span data-stu-id="9f171-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="9f171-111">Ogni risorsa nell'indice del servizio viene sottoversione indipendentemente dalla versione dello schema dell'indice del servizio.</span><span class="sxs-lookup"><span data-stu-id="9f171-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="9f171-112">La versione corrente dello schema è `3.0.0` .</span><span class="sxs-lookup"><span data-stu-id="9f171-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="9f171-113">La `3.0.0` versione è funzionalmente equivalente alla `3.0.0-beta.1` versione precedente, ma deve essere preferita perché comunica più chiaramente lo schema stabile e definito.</span><span class="sxs-lookup"><span data-stu-id="9f171-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="9f171-114">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="9f171-114">HTTP methods</span></span>

<span data-ttu-id="9f171-115">L'indice del servizio è accessibile tramite metodi HTTP `GET` e `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="9f171-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="9f171-116">Risorse</span><span class="sxs-lookup"><span data-stu-id="9f171-116">Resources</span></span>

<span data-ttu-id="9f171-117">La `resources` proprietà contiene una matrice di risorse supportate dall'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9f171-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="9f171-118">Risorsa</span><span class="sxs-lookup"><span data-stu-id="9f171-118">Resource</span></span>

<span data-ttu-id="9f171-119">Una risorsa è un oggetto nella `resources` matrice.</span><span class="sxs-lookup"><span data-stu-id="9f171-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="9f171-120">Rappresenta una funzionalità con versione di un'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9f171-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="9f171-121">Una risorsa presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="9f171-121">A resource has the following properties:</span></span>

<span data-ttu-id="9f171-122">Nome</span><span class="sxs-lookup"><span data-stu-id="9f171-122">Name</span></span>          | <span data-ttu-id="9f171-123">Type</span><span class="sxs-lookup"><span data-stu-id="9f171-123">Type</span></span>   | <span data-ttu-id="9f171-124">Necessario</span><span class="sxs-lookup"><span data-stu-id="9f171-124">Required</span></span> | <span data-ttu-id="9f171-125">Note</span><span class="sxs-lookup"><span data-stu-id="9f171-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="9f171-126">string</span><span class="sxs-lookup"><span data-stu-id="9f171-126">string</span></span> | <span data-ttu-id="9f171-127">sì</span><span class="sxs-lookup"><span data-stu-id="9f171-127">yes</span></span>      | <span data-ttu-id="9f171-128">URL della risorsa</span><span class="sxs-lookup"><span data-stu-id="9f171-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="9f171-129">string</span><span class="sxs-lookup"><span data-stu-id="9f171-129">string</span></span> | <span data-ttu-id="9f171-130">sì</span><span class="sxs-lookup"><span data-stu-id="9f171-130">yes</span></span>      | <span data-ttu-id="9f171-131">Costante di stringa che rappresenta il tipo di risorsa</span><span class="sxs-lookup"><span data-stu-id="9f171-131">A string constant representing the resource type</span></span>
<span data-ttu-id="9f171-132">comment</span><span class="sxs-lookup"><span data-stu-id="9f171-132">comment</span></span>       | <span data-ttu-id="9f171-133">string</span><span class="sxs-lookup"><span data-stu-id="9f171-133">string</span></span> | <span data-ttu-id="9f171-134">no</span><span class="sxs-lookup"><span data-stu-id="9f171-134">no</span></span>       | <span data-ttu-id="9f171-135">Descrizione leggibile della risorsa</span><span class="sxs-lookup"><span data-stu-id="9f171-135">A human readable description of the resource</span></span>

<span data-ttu-id="9f171-136">`@id`È un URL che deve essere assoluto e deve avere lo schema http o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9f171-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="9f171-137">`@type`Viene usato per identificare il protocollo specifico da usare quando si interagisce con la risorsa.</span><span class="sxs-lookup"><span data-stu-id="9f171-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="9f171-138">Il tipo della risorsa è una stringa opaca, ma in genere presenta il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="9f171-138">The type of the resource is an opaque string but generally has the format:</span></span>

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

<span data-ttu-id="9f171-139">Si prevede che i client `@type` consentano di codificare in modo rigido i valori che conoscono e li cercano nell'indice del servizio di un'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9f171-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="9f171-140">I `@type` valori esatti attualmente in uso vengono enumerati nei singoli documenti di riferimento delle risorse elencati nella [Panoramica dell'API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="9f171-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="9f171-141">Ai fini di questa documentazione, la documentazione relativa alle diverse risorse verrà essenzialmente raggruppata in base all'oggetto `{RESOURCE_NAME}` rilevato nell'indice del servizio, che è analogo al raggruppamento in base allo scenario.</span><span class="sxs-lookup"><span data-stu-id="9f171-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="9f171-142">Non è necessario che ogni risorsa abbia un o univoco `@id` `@type` .</span><span class="sxs-lookup"><span data-stu-id="9f171-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="9f171-143">Spetta all'implementazione client determinare la risorsa da preferire rispetto a un'altra.</span><span class="sxs-lookup"><span data-stu-id="9f171-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="9f171-144">Una possibile implementazione è che le risorse dello stesso o compatibili `@type` possono essere utilizzate in modo round robin in caso di errore di connessione o errore del server.</span><span class="sxs-lookup"><span data-stu-id="9f171-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="9f171-145">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="9f171-145">Sample request</span></span>

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a><span data-ttu-id="9f171-146">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="9f171-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
