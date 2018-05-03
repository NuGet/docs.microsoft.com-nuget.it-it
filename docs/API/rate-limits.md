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
ms.openlocfilehash: 3aaebef8fff670759c6484a5a8f90a2f4dd58c66
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="rate-limits"></a><span data-ttu-id="484d7-103">Limiti di velocità</span><span class="sxs-lookup"><span data-stu-id="484d7-103">Rate Limits</span></span>

<span data-ttu-id="484d7-104">L'API di NuGet.org impone limiti di velocità per evitare di evitare eventuali abusi.</span><span class="sxs-lookup"><span data-stu-id="484d7-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="484d7-105">Le richieste che superano il limite di velocità restituiranno l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="484d7-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="484d7-106">Le tabelle seguenti elencano i limiti di velocità per l'API di NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="484d7-106">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="484d7-107">Ricerca di pacchetto</span><span class="sxs-lookup"><span data-stu-id="484d7-107">Package search</span></span>

> [!Note]
> <span data-ttu-id="484d7-108">Si consiglia di usare di NuGet.org [V3 API](https://docs.microsoft.com/nuget/api/search-query-service-resource) per la ricerca ad alte prestazioni e non hanno alcun limite attualmente.</span><span class="sxs-lookup"><span data-stu-id="484d7-108">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="484d7-109">Per le versioni V1 e V2 le API di ricerca, applicano i limiti followins:</span><span class="sxs-lookup"><span data-stu-id="484d7-109">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="484d7-110">API</span><span class="sxs-lookup"><span data-stu-id="484d7-110">API</span></span> | <span data-ttu-id="484d7-111">Tipo di limite</span><span class="sxs-lookup"><span data-stu-id="484d7-111">Limit Type</span></span> | <span data-ttu-id="484d7-112">Valore del limite</span><span class="sxs-lookup"><span data-stu-id="484d7-112">Limit Value</span></span> | <span data-ttu-id="484d7-113">API usecase</span><span class="sxs-lookup"><span data-stu-id="484d7-113">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="484d7-114">**OTTIENI** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="484d7-114">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="484d7-115">IP</span><span class="sxs-lookup"><span data-stu-id="484d7-115">IP</span></span> | <span data-ttu-id="484d7-116">1000 / minuto</span><span class="sxs-lookup"><span data-stu-id="484d7-116">1000 / minute</span></span> | <span data-ttu-id="484d7-117">Eseguire una query dei metadati del pacchetto NuGet tramite OData v1 `Packages` raccolta</span><span class="sxs-lookup"><span data-stu-id="484d7-117">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="484d7-118">**OTTIENI** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="484d7-118">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="484d7-119">IP</span><span class="sxs-lookup"><span data-stu-id="484d7-119">IP</span></span> | <span data-ttu-id="484d7-120">3000 / minuto</span><span class="sxs-lookup"><span data-stu-id="484d7-120">3000 / minute</span></span> | <span data-ttu-id="484d7-121">Ricerca per i pacchetti NuGet tramite l'endpoint di ricerca v1</span><span class="sxs-lookup"><span data-stu-id="484d7-121">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="484d7-122">**OTTIENI** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="484d7-122">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="484d7-123">IP</span><span class="sxs-lookup"><span data-stu-id="484d7-123">IP</span></span> | <span data-ttu-id="484d7-124">20000 / minuto</span><span class="sxs-lookup"><span data-stu-id="484d7-124">20000 / minute</span></span> | <span data-ttu-id="484d7-125">Eseguire una query dei metadati del pacchetto NuGet tramite v2 OData `Packages` raccolta</span><span class="sxs-lookup"><span data-stu-id="484d7-125">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="484d7-126">**OTTIENI** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="484d7-126">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="484d7-127">IP</span><span class="sxs-lookup"><span data-stu-id="484d7-127">IP</span></span> | <span data-ttu-id="484d7-128">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="484d7-128">100 / minute</span></span> | <span data-ttu-id="484d7-129">Eseguire una query conteggio pacchetto NuGet tramite v2 OData `Packages` raccolta</span><span class="sxs-lookup"><span data-stu-id="484d7-129">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="484d7-130">Pacchetto Push ed esclusione</span><span class="sxs-lookup"><span data-stu-id="484d7-130">Package Push and Unlist</span></span>

| <span data-ttu-id="484d7-131">API</span><span class="sxs-lookup"><span data-stu-id="484d7-131">API</span></span> | <span data-ttu-id="484d7-132">Tipo di limite</span><span class="sxs-lookup"><span data-stu-id="484d7-132">Limit Type</span></span> | <span data-ttu-id="484d7-133">Valore del limite</span><span class="sxs-lookup"><span data-stu-id="484d7-133">Limit Value</span></span> | <span data-ttu-id="484d7-134">APU usecase</span><span class="sxs-lookup"><span data-stu-id="484d7-134">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="484d7-135">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="484d7-135">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="484d7-136">Chiave API</span><span class="sxs-lookup"><span data-stu-id="484d7-136">API Key</span></span> | <span data-ttu-id="484d7-137">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="484d7-137">100 / minute</span></span> | <span data-ttu-id="484d7-138">Caricare un nuovo pacchetto NuGet (versione) tramite l'endpoint di push v2</span><span class="sxs-lookup"><span data-stu-id="484d7-138">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="484d7-139">**ELIMINARE** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="484d7-139">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="484d7-140">Chiave API</span><span class="sxs-lookup"><span data-stu-id="484d7-140">API Key</span></span> | <span data-ttu-id="484d7-141">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="484d7-141">100 / minute</span></span> | <span data-ttu-id="484d7-142">Esclusione di un pacchetto NuGet (versione) tramite l'endpoint v2</span><span class="sxs-lookup"><span data-stu-id="484d7-142">Unlist a NuGet package (version) via v2 endpoint</span></span> 
