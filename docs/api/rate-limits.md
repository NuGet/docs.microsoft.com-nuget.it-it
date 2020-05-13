---
title: Limiti di velocità, API NuGet
description: Le API NuGet avranno limiti di velocità applicati per impedire abusi.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367934"
---
# <a name="rate-limits"></a><span data-ttu-id="92039-103">Limiti di velocità</span><span class="sxs-lookup"><span data-stu-id="92039-103">Rate Limits</span></span>

<span data-ttu-id="92039-104">L'API NuGet.org impone la limitazione della frequenza per impedire abusi.</span><span class="sxs-lookup"><span data-stu-id="92039-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="92039-105">Le richieste che superano il limite di frequenza restituiscono l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="92039-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="92039-106">Oltre alla limitazione delle richieste con limiti di velocità, alcune API applicano anche la quota.</span><span class="sxs-lookup"><span data-stu-id="92039-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="92039-107">Le richieste che superano la quota restituiscono l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="92039-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="92039-108">Le tabelle seguenti elencano i limiti di velocità per l'API NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="92039-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="92039-109">Ricerca di pacchetti</span><span class="sxs-lookup"><span data-stu-id="92039-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="92039-110">Si consiglia di usare le API di [ricerca V3](search-query-service-resource.md) di NuGet. org, perché attualmente non è limitato.</span><span class="sxs-lookup"><span data-stu-id="92039-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="92039-111">Per le API di ricerca V1 e V2, si applicano i limiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="92039-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="92039-112">API</span><span class="sxs-lookup"><span data-stu-id="92039-112">API</span></span> | <span data-ttu-id="92039-113">Tipo limite</span><span class="sxs-lookup"><span data-stu-id="92039-113">Limit Type</span></span> | <span data-ttu-id="92039-114">Valore limite</span><span class="sxs-lookup"><span data-stu-id="92039-114">Limit Value</span></span> | <span data-ttu-id="92039-115">Caso di utilizzo dell'API</span><span class="sxs-lookup"><span data-stu-id="92039-115">API Use Case</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="92039-116">**Ottenere**`/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="92039-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="92039-117">IP</span><span class="sxs-lookup"><span data-stu-id="92039-117">IP</span></span> | <span data-ttu-id="92039-118">1000 al minuto</span><span class="sxs-lookup"><span data-stu-id="92039-118">1000 / minute</span></span> | <span data-ttu-id="92039-119">Eseguire query sui metadati del pacchetto NuGet tramite la raccolta OData V1 `Packages`</span><span class="sxs-lookup"><span data-stu-id="92039-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="92039-120">**Ottenere**`/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="92039-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="92039-121">IP</span><span class="sxs-lookup"><span data-stu-id="92039-121">IP</span></span> | <span data-ttu-id="92039-122">3000 al minuto</span><span class="sxs-lookup"><span data-stu-id="92039-122">3000 / minute</span></span> | <span data-ttu-id="92039-123">Cerca i pacchetti NuGet tramite l'endpoint di ricerca V1</span><span class="sxs-lookup"><span data-stu-id="92039-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="92039-124">**Ottenere**`/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="92039-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="92039-125">IP</span><span class="sxs-lookup"><span data-stu-id="92039-125">IP</span></span> | <span data-ttu-id="92039-126">20000 al minuto</span><span class="sxs-lookup"><span data-stu-id="92039-126">20000 / minute</span></span> | <span data-ttu-id="92039-127">Eseguire query sui metadati del pacchetto NuGet tramite la raccolta OData v2 `Packages`</span><span class="sxs-lookup"><span data-stu-id="92039-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="92039-128">**Ottenere**`/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="92039-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="92039-129">IP</span><span class="sxs-lookup"><span data-stu-id="92039-129">IP</span></span> | <span data-ttu-id="92039-130">100 al minuto</span><span class="sxs-lookup"><span data-stu-id="92039-130">100 / minute</span></span> | <span data-ttu-id="92039-131">Eseguire query sul numero di pacchetti NuGet tramite la raccolta OData v2 `Packages`</span><span class="sxs-lookup"><span data-stu-id="92039-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="92039-132">Push e Unlist di pacchetti</span><span class="sxs-lookup"><span data-stu-id="92039-132">Package Push and Unlist</span></span>

| <span data-ttu-id="92039-133">API</span><span class="sxs-lookup"><span data-stu-id="92039-133">API</span></span> | <span data-ttu-id="92039-134">Tipo limite</span><span class="sxs-lookup"><span data-stu-id="92039-134">Limit Type</span></span> | <span data-ttu-id="92039-135">Valore limite</span><span class="sxs-lookup"><span data-stu-id="92039-135">Limit Value</span></span> | <span data-ttu-id="92039-136">Caso di utilizzo dell'API</span><span class="sxs-lookup"><span data-stu-id="92039-136">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="92039-137">**Inserisci**`/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="92039-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="92039-138">API key</span><span class="sxs-lookup"><span data-stu-id="92039-138">API Key</span></span> | <span data-ttu-id="92039-139">350/ora</span><span class="sxs-lookup"><span data-stu-id="92039-139">350 / hour</span></span> | <span data-ttu-id="92039-140">Caricare un nuovo pacchetto NuGet (versione) tramite l'endpoint di push V2</span><span class="sxs-lookup"><span data-stu-id="92039-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="92039-141">**Elimina**`/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="92039-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="92039-142">API key</span><span class="sxs-lookup"><span data-stu-id="92039-142">API Key</span></span> | <span data-ttu-id="92039-143">250/ora</span><span class="sxs-lookup"><span data-stu-id="92039-143">250 / hour</span></span> | <span data-ttu-id="92039-144">Non elencare un pacchetto NuGet (versione) tramite l'endpoint V2</span><span class="sxs-lookup"><span data-stu-id="92039-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 

## <a name="nugetorg-website-page-views"></a><span data-ttu-id="92039-145">Visualizzazioni delle pagine del sito Web nuget.org</span><span class="sxs-lookup"><span data-stu-id="92039-145">nuget.org website page views</span></span>

<span data-ttu-id="92039-146">Se si accede alle pagine Web di nuget.org a livello di codice, è consigliabile esaminare le [API V3](overview.md)documentate.</span><span class="sxs-lookup"><span data-stu-id="92039-146">If you are accessing the nuget.org web pages programmatically, consider investigating our documented [V3 APIs](overview.md).</span></span> <span data-ttu-id="92039-147">Questi endpoint consentono un accesso più semplice ai metadati e al contenuto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="92039-147">These endpoints allow for simpler access to package metadata and content.</span></span> <span data-ttu-id="92039-148">L'API V3 offre una maggiore disponibilità e offre prestazioni migliori rispetto all'accesso alle pagine Web della raccolta NuGet, progettate per l'interazione con il Web browser.</span><span class="sxs-lookup"><span data-stu-id="92039-148">The V3 API has better availability and has higher performance than accessing the NuGet Gallery web pages, which are designed for web browser interaction.</span></span>

| <span data-ttu-id="92039-149">API</span><span class="sxs-lookup"><span data-stu-id="92039-149">API</span></span> | <span data-ttu-id="92039-150">Tipo limite</span><span class="sxs-lookup"><span data-stu-id="92039-150">Limit Type</span></span> | <span data-ttu-id="92039-151">Valore limite</span><span class="sxs-lookup"><span data-stu-id="92039-151">Limit Value</span></span> | <span data-ttu-id="92039-152">Caso di utilizzo dell'API</span><span class="sxs-lookup"><span data-stu-id="92039-152">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="92039-153">**Ottenere**`/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="92039-153">**GET** `/package/{id}/{version}`</span></span> | <span data-ttu-id="92039-154">IP</span><span class="sxs-lookup"><span data-stu-id="92039-154">IP</span></span> | <span data-ttu-id="92039-155">50 al minuto</span><span class="sxs-lookup"><span data-stu-id="92039-155">50 / minute</span></span> | <span data-ttu-id="92039-156">Visualizza la pagina dei dettagli del pacchetto (versione).</span><span class="sxs-lookup"><span data-stu-id="92039-156">Display package (version) details page.</span></span> 
