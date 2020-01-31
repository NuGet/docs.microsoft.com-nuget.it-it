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
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813195"
---
# <a name="rate-limits"></a><span data-ttu-id="aec2e-103">Limiti di velocità</span><span class="sxs-lookup"><span data-stu-id="aec2e-103">Rate Limits</span></span>

<span data-ttu-id="aec2e-104">L'API NuGet.org impone la limitazione della frequenza per impedire abusi.</span><span class="sxs-lookup"><span data-stu-id="aec2e-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="aec2e-105">Le richieste che superano il limite di frequenza restituiscono l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="aec2e-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="aec2e-106">Oltre alla limitazione delle richieste con limiti di velocità, alcune API applicano anche la quota.</span><span class="sxs-lookup"><span data-stu-id="aec2e-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="aec2e-107">Le richieste che superano la quota restituiscono l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="aec2e-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="aec2e-108">Le tabelle seguenti elencano i limiti di velocità per l'API NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="aec2e-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="aec2e-109">Ricerca di pacchetti</span><span class="sxs-lookup"><span data-stu-id="aec2e-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="aec2e-110">Si consiglia di usare le API di [ricerca V3](search-query-service-resource.md) di NuGet. org, perché attualmente non è limitato.</span><span class="sxs-lookup"><span data-stu-id="aec2e-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="aec2e-111">Per le API di ricerca V1 e V2, si applicano i limiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aec2e-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="aec2e-112">API</span><span class="sxs-lookup"><span data-stu-id="aec2e-112">API</span></span> | <span data-ttu-id="aec2e-113">Tipo limite</span><span class="sxs-lookup"><span data-stu-id="aec2e-113">Limit Type</span></span> | <span data-ttu-id="aec2e-114">Valore limite</span><span class="sxs-lookup"><span data-stu-id="aec2e-114">Limit Value</span></span> | <span data-ttu-id="aec2e-115">API useCase</span><span class="sxs-lookup"><span data-stu-id="aec2e-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="aec2e-116">**Ottenere** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="aec2e-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="aec2e-117">IP</span><span class="sxs-lookup"><span data-stu-id="aec2e-117">IP</span></span> | <span data-ttu-id="aec2e-118">1000 al minuto</span><span class="sxs-lookup"><span data-stu-id="aec2e-118">1000 / minute</span></span> | <span data-ttu-id="aec2e-119">Eseguire query sui metadati del pacchetto NuGet tramite la raccolta di `Packages` OData V1</span><span class="sxs-lookup"><span data-stu-id="aec2e-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="aec2e-120">**Ottenere** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="aec2e-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="aec2e-121">IP</span><span class="sxs-lookup"><span data-stu-id="aec2e-121">IP</span></span> | <span data-ttu-id="aec2e-122">3000 al minuto</span><span class="sxs-lookup"><span data-stu-id="aec2e-122">3000 / minute</span></span> | <span data-ttu-id="aec2e-123">Cerca i pacchetti NuGet tramite l'endpoint di ricerca V1</span><span class="sxs-lookup"><span data-stu-id="aec2e-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="aec2e-124">**Ottenere** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="aec2e-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="aec2e-125">IP</span><span class="sxs-lookup"><span data-stu-id="aec2e-125">IP</span></span> | <span data-ttu-id="aec2e-126">20000 al minuto</span><span class="sxs-lookup"><span data-stu-id="aec2e-126">20000 / minute</span></span> | <span data-ttu-id="aec2e-127">Eseguire query sui metadati del pacchetto NuGet tramite la raccolta `Packages` OData V2</span><span class="sxs-lookup"><span data-stu-id="aec2e-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="aec2e-128">**Ottenere** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="aec2e-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="aec2e-129">IP</span><span class="sxs-lookup"><span data-stu-id="aec2e-129">IP</span></span> | <span data-ttu-id="aec2e-130">100 al minuto</span><span class="sxs-lookup"><span data-stu-id="aec2e-130">100 / minute</span></span> | <span data-ttu-id="aec2e-131">Eseguire query sul numero di pacchetti NuGet tramite la raccolta `Packages` OData V2</span><span class="sxs-lookup"><span data-stu-id="aec2e-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="aec2e-132">Push e Unlist di pacchetti</span><span class="sxs-lookup"><span data-stu-id="aec2e-132">Package Push and Unlist</span></span>

| <span data-ttu-id="aec2e-133">API</span><span class="sxs-lookup"><span data-stu-id="aec2e-133">API</span></span> | <span data-ttu-id="aec2e-134">Tipo limite</span><span class="sxs-lookup"><span data-stu-id="aec2e-134">Limit Type</span></span> | <span data-ttu-id="aec2e-135">Valore limite</span><span class="sxs-lookup"><span data-stu-id="aec2e-135">Limit Value</span></span> | <span data-ttu-id="aec2e-136">API useCase</span><span class="sxs-lookup"><span data-stu-id="aec2e-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="aec2e-137">**Inserisci** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="aec2e-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="aec2e-138">Chiave API</span><span class="sxs-lookup"><span data-stu-id="aec2e-138">API Key</span></span> | <span data-ttu-id="aec2e-139">350/ora</span><span class="sxs-lookup"><span data-stu-id="aec2e-139">350 / hour</span></span> | <span data-ttu-id="aec2e-140">Caricare un nuovo pacchetto NuGet (versione) tramite l'endpoint di push V2</span><span class="sxs-lookup"><span data-stu-id="aec2e-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="aec2e-141">**Elimina** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="aec2e-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="aec2e-142">Chiave API</span><span class="sxs-lookup"><span data-stu-id="aec2e-142">API Key</span></span> | <span data-ttu-id="aec2e-143">250/ora</span><span class="sxs-lookup"><span data-stu-id="aec2e-143">250 / hour</span></span> | <span data-ttu-id="aec2e-144">Non elencare un pacchetto NuGet (versione) tramite l'endpoint V2</span><span class="sxs-lookup"><span data-stu-id="aec2e-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
