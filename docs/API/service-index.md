---
title: Indice del servizio, NuGet API | Documenti Microsoft
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "L'indice di servizio è il punto di ingresso dell'API HTTP NuGet e vengono elencate le funzionalità del server."
keywords: Punto di ingresso API NuGet, individuazione di endpoint NuGetA PI
ms.reviewer:
- karann
- unnir
ms.openlocfilehash: 8de0bc15edc358d091d84da54b8b67c085f29645
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/08/2018
---
# <a name="service-index"></a><span data-ttu-id="94226-104">Indice del servizio</span><span class="sxs-lookup"><span data-stu-id="94226-104">Service index</span></span>

<span data-ttu-id="94226-105">L'indice di servizio è un documento JSON che è il punto di ingresso per un'origine del pacchetto NuGet e consente a un'implementazione client di individuare le funzionalità dell'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="94226-105">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="94226-106">L'indice di servizio è un oggetto JSON con due proprietà obbligatorie: `version` (la versione dello schema dell'indice del servizio) e `resources` (endpoint o funzionalità di origine del pacchetto).</span><span class="sxs-lookup"><span data-stu-id="94226-106">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="94226-107">indice del servizio di NuGet.org si trova in `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="94226-107">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="94226-108">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="94226-108">Versioning</span></span>

<span data-ttu-id="94226-109">Il `version` valore è una stringa di versione analizzabili SemVer 2.0.0 che indica la versione dello schema dell'indice del servizio.</span><span class="sxs-lookup"><span data-stu-id="94226-109">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="94226-110">L'API richiede che la stringa di versione è un numero di versione principale `3`.</span><span class="sxs-lookup"><span data-stu-id="94226-110">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="94226-111">Al momento non modifiche allo schema di indice del servizio, versione secondaria della stringa di versione verrà aumentato.</span><span class="sxs-lookup"><span data-stu-id="94226-111">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="94226-112">Ogni risorsa in corrispondenza dell'indice del servizio viene creata indipendentemente dalla versione dello schema di indice del servizio.</span><span class="sxs-lookup"><span data-stu-id="94226-112">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="94226-113">La versione dello schema corrente è `3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="94226-113">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="94226-114">Il `3.0.0` è funzionalmente equivalente alla precedente versione `3.0.0-beta.1` versione ma deve essere preferito in quanto più chiaramente comunica lo schema stabile, definito.</span><span class="sxs-lookup"><span data-stu-id="94226-114">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="94226-115">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="94226-115">HTTP methods</span></span>

<span data-ttu-id="94226-116">L'indice di servizio è accessibile tramite i metodi HTTP `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="94226-116">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="94226-117">Risorse</span><span class="sxs-lookup"><span data-stu-id="94226-117">Resources</span></span>

<span data-ttu-id="94226-118">Il `resources` proprietà contiene una matrice di risorse, supportati da questa origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="94226-118">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="94226-119">Risorsa</span><span class="sxs-lookup"><span data-stu-id="94226-119">Resource</span></span>

<span data-ttu-id="94226-120">Una risorsa è un oggetto di `resources` matrice.</span><span class="sxs-lookup"><span data-stu-id="94226-120">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="94226-121">Rappresenta una funzionalità con controllo delle versioni di un'origine pacchetto.</span><span class="sxs-lookup"><span data-stu-id="94226-121">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="94226-122">Una risorsa ha le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="94226-122">A resource has the following properties:</span></span>

<span data-ttu-id="94226-123">nome</span><span class="sxs-lookup"><span data-stu-id="94226-123">Name</span></span>          | <span data-ttu-id="94226-124">Tipo</span><span class="sxs-lookup"><span data-stu-id="94226-124">Type</span></span>   | <span data-ttu-id="94226-125">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="94226-125">Required</span></span> | <span data-ttu-id="94226-126">Note</span><span class="sxs-lookup"><span data-stu-id="94226-126">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="94226-127">stringa</span><span class="sxs-lookup"><span data-stu-id="94226-127">string</span></span> | <span data-ttu-id="94226-128">sì</span><span class="sxs-lookup"><span data-stu-id="94226-128">yes</span></span>      | <span data-ttu-id="94226-129">L'URL della risorsa</span><span class="sxs-lookup"><span data-stu-id="94226-129">The URL to the resource</span></span>
@type         | <span data-ttu-id="94226-130">stringa</span><span class="sxs-lookup"><span data-stu-id="94226-130">string</span></span> | <span data-ttu-id="94226-131">sì</span><span class="sxs-lookup"><span data-stu-id="94226-131">yes</span></span>      | <span data-ttu-id="94226-132">Costante stringa che rappresenta il tipo di risorsa</span><span class="sxs-lookup"><span data-stu-id="94226-132">A string constant representing the resource type</span></span>
<span data-ttu-id="94226-133">commento</span><span class="sxs-lookup"><span data-stu-id="94226-133">comment</span></span>       | <span data-ttu-id="94226-134">stringa</span><span class="sxs-lookup"><span data-stu-id="94226-134">string</span></span> | <span data-ttu-id="94226-135">No</span><span class="sxs-lookup"><span data-stu-id="94226-135">no</span></span>       | <span data-ttu-id="94226-136">Descrizione leggibile della risorsa</span><span class="sxs-lookup"><span data-stu-id="94226-136">A human readable description of the resource</span></span>

<span data-ttu-id="94226-137">Il `@id` è un URL che deve essere assoluto e deve avere lo schema HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="94226-137">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="94226-138">Il `@type` viene utilizzato per identificare il protocollo specifico da utilizzare durante l'interazione con la risorsa.</span><span class="sxs-lookup"><span data-stu-id="94226-138">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="94226-139">Il tipo della risorsa è una stringa opaca ma in genere ha il formato:</span><span class="sxs-lookup"><span data-stu-id="94226-139">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="94226-140">Si prevede che i client a livello di codice il `@type` valori comprendere e cercare nell'indice di un'origine del pacchetto servizio.</span><span class="sxs-lookup"><span data-stu-id="94226-140">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="94226-141">L'esatto `@type` vengono enumerati i valori attualmente in uso nei documenti di riferimento delle singole risorse elencati nel [panoramica dell'API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="94226-141">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="94226-142">Ai fini di questa documentazione, la documentazione relativa alle diverse risorse verrà essenzialmente raggruppata per il `{RESOURCE_NAME}` trovato nell'indice servizio analogo al raggruppamento dallo scenario.</span><span class="sxs-lookup"><span data-stu-id="94226-142">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="94226-143">Non è necessario che ogni risorsa è univoca `@id` o `@type`.</span><span class="sxs-lookup"><span data-stu-id="94226-143">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="94226-144">In questo caso, l'implementazione del client per determinare quale risorsa scegliere da preferire un altro.</span><span class="sxs-lookup"><span data-stu-id="94226-144">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="94226-145">Una possibile implementazione è che le risorse dello stesso o compatibile `@type` può essere usato in uno schema round-robin in caso di errore di server o errore di connessione.</span><span class="sxs-lookup"><span data-stu-id="94226-145">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="94226-146">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="94226-146">Sample request</span></span>

<span data-ttu-id="94226-147">GET https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="94226-147">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="94226-148">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="94226-148">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
