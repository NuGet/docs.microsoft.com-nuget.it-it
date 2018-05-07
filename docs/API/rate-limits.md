---
title: Limiti, NuGet API di velocità
description: APIs NuGet verranno sono applicati i limiti di velocità per evitare abusi.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: e236d685a700d0f47480336cece8edfd44c28863
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2018
---
# <a name="rate-limits"></a><span data-ttu-id="c9909-103">Limiti di velocità</span><span class="sxs-lookup"><span data-stu-id="c9909-103">Rate Limits</span></span>

<span data-ttu-id="c9909-104">L'API di NuGet.org impone limiti di velocità per evitare di evitare eventuali abusi.</span><span class="sxs-lookup"><span data-stu-id="c9909-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="c9909-105">Le richieste che superano il limite di velocità restituiranno l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="c9909-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="c9909-106">Le tabelle seguenti elencano i limiti di velocità per l'API di NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c9909-106">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="c9909-107">Ricerca di pacchetto</span><span class="sxs-lookup"><span data-stu-id="c9909-107">Package search</span></span>

> [!Note]
> <span data-ttu-id="c9909-108">Si consiglia di usare di NuGet.org [V3 API](https://docs.microsoft.com/nuget/api/search-query-service-resource) per la ricerca ad alte prestazioni e non hanno alcun limite attualmente.</span><span class="sxs-lookup"><span data-stu-id="c9909-108">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="c9909-109">Per le versioni V1 e V2 le API di ricerca, applicano i limiti followins:</span><span class="sxs-lookup"><span data-stu-id="c9909-109">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="c9909-110">API</span><span class="sxs-lookup"><span data-stu-id="c9909-110">API</span></span> | <span data-ttu-id="c9909-111">Tipo di limite</span><span class="sxs-lookup"><span data-stu-id="c9909-111">Limit Type</span></span> | <span data-ttu-id="c9909-112">Valore del limite</span><span class="sxs-lookup"><span data-stu-id="c9909-112">Limit Value</span></span> | <span data-ttu-id="c9909-113">API usecase</span><span class="sxs-lookup"><span data-stu-id="c9909-113">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="c9909-114">**OTTIENI** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="c9909-114">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="c9909-115">IP</span><span class="sxs-lookup"><span data-stu-id="c9909-115">IP</span></span> | <span data-ttu-id="c9909-116">1000 / minuto</span><span class="sxs-lookup"><span data-stu-id="c9909-116">1000 / minute</span></span> | <span data-ttu-id="c9909-117">Eseguire una query dei metadati del pacchetto NuGet tramite OData v1 `Packages` raccolta</span><span class="sxs-lookup"><span data-stu-id="c9909-117">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="c9909-118">**OTTIENI** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="c9909-118">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="c9909-119">IP</span><span class="sxs-lookup"><span data-stu-id="c9909-119">IP</span></span> | <span data-ttu-id="c9909-120">3000 / minuto</span><span class="sxs-lookup"><span data-stu-id="c9909-120">3000 / minute</span></span> | <span data-ttu-id="c9909-121">Ricerca per i pacchetti NuGet tramite l'endpoint di ricerca v1</span><span class="sxs-lookup"><span data-stu-id="c9909-121">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="c9909-122">**OTTIENI** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="c9909-122">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="c9909-123">IP</span><span class="sxs-lookup"><span data-stu-id="c9909-123">IP</span></span> | <span data-ttu-id="c9909-124">20000 / minuto</span><span class="sxs-lookup"><span data-stu-id="c9909-124">20000 / minute</span></span> | <span data-ttu-id="c9909-125">Eseguire una query dei metadati del pacchetto NuGet tramite v2 OData `Packages` raccolta</span><span class="sxs-lookup"><span data-stu-id="c9909-125">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="c9909-126">**OTTIENI** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="c9909-126">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="c9909-127">IP</span><span class="sxs-lookup"><span data-stu-id="c9909-127">IP</span></span> | <span data-ttu-id="c9909-128">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="c9909-128">100 / minute</span></span> | <span data-ttu-id="c9909-129">Eseguire una query conteggio pacchetto NuGet tramite v2 OData `Packages` raccolta</span><span class="sxs-lookup"><span data-stu-id="c9909-129">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="c9909-130">Pacchetto Push ed esclusione</span><span class="sxs-lookup"><span data-stu-id="c9909-130">Package Push and Unlist</span></span>

| <span data-ttu-id="c9909-131">API</span><span class="sxs-lookup"><span data-stu-id="c9909-131">API</span></span> | <span data-ttu-id="c9909-132">Tipo di limite</span><span class="sxs-lookup"><span data-stu-id="c9909-132">Limit Type</span></span> | <span data-ttu-id="c9909-133">Valore del limite</span><span class="sxs-lookup"><span data-stu-id="c9909-133">Limit Value</span></span> | <span data-ttu-id="c9909-134">API usecase</span><span class="sxs-lookup"><span data-stu-id="c9909-134">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="c9909-135">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="c9909-135">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="c9909-136">Chiave API</span><span class="sxs-lookup"><span data-stu-id="c9909-136">API Key</span></span> | <span data-ttu-id="c9909-137">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="c9909-137">100 / minute</span></span> | <span data-ttu-id="c9909-138">Caricare un nuovo pacchetto NuGet (versione) tramite l'endpoint di push v2</span><span class="sxs-lookup"><span data-stu-id="c9909-138">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="c9909-139">**ELIMINARE** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="c9909-139">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="c9909-140">Chiave API</span><span class="sxs-lookup"><span data-stu-id="c9909-140">API Key</span></span> | <span data-ttu-id="c9909-141">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="c9909-141">100 / minute</span></span> | <span data-ttu-id="c9909-142">Esclusione di un pacchetto NuGet (versione) tramite l'endpoint v2</span><span class="sxs-lookup"><span data-stu-id="c9909-142">Unlist a NuGet package (version) via v2 endpoint</span></span> 
