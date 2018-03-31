---
title: Limiti di velocità | Documenti Microsoft
author:
- cmanu
- anangaur
ms.author:
- cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: APIs NuGet verranno sono applicati i limiti di velocità per evitare abusi.
keywords: Limitazione di velocità NuGet API,
ms.reviewer:
- skofman
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f7891d5e4c008219d9f4808f223f3e5e7ae06ced
ms.sourcegitcommit: fa40be739d093a37d5f7072b62ebdb4f595f4110
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2018
---
# <a name="rate-limits"></a><span data-ttu-id="504c5-104">Limiti di velocità</span><span class="sxs-lookup"><span data-stu-id="504c5-104">Rate Limits</span></span>

<span data-ttu-id="504c5-105">L'API di NuGet.org impone limiti di velocità per evitare di evitare eventuali abusi.</span><span class="sxs-lookup"><span data-stu-id="504c5-105">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="504c5-106">Le richieste che superano il limite di velocità restituiranno l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="504c5-106">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="504c5-107">Le tabelle seguenti elencano i limiti di velocità per l'API di NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="504c5-107">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="504c5-108">Ricerca di pacchetto</span><span class="sxs-lookup"><span data-stu-id="504c5-108">Package search</span></span>

> [!Note]
> <span data-ttu-id="504c5-109">Si consiglia di usare di NuGet.org [V3 API](https://docs.microsoft.com/nuget/api/search-query-service-resource) per la ricerca ad alte prestazioni e non hanno alcun limite attualmente.</span><span class="sxs-lookup"><span data-stu-id="504c5-109">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="504c5-110">Per le versioni V1 e V2 le API di ricerca, applicano i limiti followins:</span><span class="sxs-lookup"><span data-stu-id="504c5-110">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="504c5-111">API</span><span class="sxs-lookup"><span data-stu-id="504c5-111">API</span></span> | <span data-ttu-id="504c5-112">Tipo di limite</span><span class="sxs-lookup"><span data-stu-id="504c5-112">Limit Type</span></span> | <span data-ttu-id="504c5-113">Valore del limite</span><span class="sxs-lookup"><span data-stu-id="504c5-113">Limit Value</span></span> | <span data-ttu-id="504c5-114">API usecase</span><span class="sxs-lookup"><span data-stu-id="504c5-114">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="504c5-115">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="504c5-115">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="504c5-116">IP</span><span class="sxs-lookup"><span data-stu-id="504c5-116">IP</span></span> | <span data-ttu-id="504c5-117">1000 / minuto</span><span class="sxs-lookup"><span data-stu-id="504c5-117">1000 / minute</span></span> | <span data-ttu-id="504c5-118">Eseguire una query dei metadati del pacchetto NuGet tramite OData v1 `Packages` raccolta</span><span class="sxs-lookup"><span data-stu-id="504c5-118">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="504c5-119">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="504c5-119">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="504c5-120">IP</span><span class="sxs-lookup"><span data-stu-id="504c5-120">IP</span></span> | <span data-ttu-id="504c5-121">3000 / minuto</span><span class="sxs-lookup"><span data-stu-id="504c5-121">3000 / minute</span></span> | <span data-ttu-id="504c5-122">Ricerca per i pacchetti NuGet tramite l'endpoint di ricerca v1</span><span class="sxs-lookup"><span data-stu-id="504c5-122">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="504c5-123">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="504c5-123">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="504c5-124">IP</span><span class="sxs-lookup"><span data-stu-id="504c5-124">IP</span></span> | <span data-ttu-id="504c5-125">20000 / minuto</span><span class="sxs-lookup"><span data-stu-id="504c5-125">20000 / minute</span></span> | <span data-ttu-id="504c5-126">Eseguire una query dei metadati del pacchetto NuGet tramite v2 OData `Packages` raccolta</span><span class="sxs-lookup"><span data-stu-id="504c5-126">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="504c5-127">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="504c5-127">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="504c5-128">IP</span><span class="sxs-lookup"><span data-stu-id="504c5-128">IP</span></span> | <span data-ttu-id="504c5-129">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="504c5-129">100 / minute</span></span> | <span data-ttu-id="504c5-130">Eseguire una query conteggio pacchetto NuGet tramite v2 OData `Packages` raccolta</span><span class="sxs-lookup"><span data-stu-id="504c5-130">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="504c5-131">Pacchetto Push ed esclusione</span><span class="sxs-lookup"><span data-stu-id="504c5-131">Package Push and Unlist</span></span>

| <span data-ttu-id="504c5-132">API</span><span class="sxs-lookup"><span data-stu-id="504c5-132">API</span></span> | <span data-ttu-id="504c5-133">Tipo di limite</span><span class="sxs-lookup"><span data-stu-id="504c5-133">Limit Type</span></span> | <span data-ttu-id="504c5-134">Valore del limite</span><span class="sxs-lookup"><span data-stu-id="504c5-134">Limit Value</span></span> | <span data-ttu-id="504c5-135">APU usecase</span><span class="sxs-lookup"><span data-stu-id="504c5-135">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="504c5-136">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="504c5-136">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="504c5-137">Chiave API</span><span class="sxs-lookup"><span data-stu-id="504c5-137">API Key</span></span> | <span data-ttu-id="504c5-138">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="504c5-138">100 / minute</span></span> | <span data-ttu-id="504c5-139">Caricare un nuovo pacchetto NuGet (versione) tramite l'endpoint di push v2</span><span class="sxs-lookup"><span data-stu-id="504c5-139">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="504c5-140">**ELIMINARE** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="504c5-140">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="504c5-141">Chiave API</span><span class="sxs-lookup"><span data-stu-id="504c5-141">API Key</span></span> | <span data-ttu-id="504c5-142">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="504c5-142">100 / minute</span></span> | <span data-ttu-id="504c5-143">Esclusione di un pacchetto NuGet (versione) tramite l'endpoint v2</span><span class="sxs-lookup"><span data-stu-id="504c5-143">Unlist a NuGet package (version) via v2 endpoint</span></span> 
