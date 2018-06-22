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
ms.openlocfilehash: c5d3cf68ac6a96a6c14eb5e652bcf72698b6a8e8
ms.sourcegitcommit: 8f0bb8bb9cb91d27d660963ed9b0f32642f420fe
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/17/2018
ms.locfileid: "34225944"
---
# <a name="rate-limits"></a><span data-ttu-id="59986-103">Limiti di velocità</span><span class="sxs-lookup"><span data-stu-id="59986-103">Rate Limits</span></span>

<span data-ttu-id="59986-104">L'API di NuGet.org impone limiti di velocità per evitare di evitare eventuali abusi.</span><span class="sxs-lookup"><span data-stu-id="59986-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="59986-105">Le richieste che superano il limite di velocità restituiranno l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="59986-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="59986-106">Le tabelle seguenti elencano i limiti di velocità per l'API di NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="59986-106">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="59986-107">Ricerca di pacchetto</span><span class="sxs-lookup"><span data-stu-id="59986-107">Package search</span></span>

> [!Note]
> <span data-ttu-id="59986-108">Si consiglia di usare di NuGet.org [V3 API](https://docs.microsoft.com/nuget/api/search-query-service-resource) per la ricerca ad alte prestazioni e non hanno alcun limite attualmente.</span><span class="sxs-lookup"><span data-stu-id="59986-108">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="59986-109">Per le versioni V1 e V2 le API di ricerca, applicano i limiti followins:</span><span class="sxs-lookup"><span data-stu-id="59986-109">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="59986-110">API</span><span class="sxs-lookup"><span data-stu-id="59986-110">API</span></span> | <span data-ttu-id="59986-111">Tipo di limite</span><span class="sxs-lookup"><span data-stu-id="59986-111">Limit Type</span></span> | <span data-ttu-id="59986-112">Valore del limite</span><span class="sxs-lookup"><span data-stu-id="59986-112">Limit Value</span></span> | <span data-ttu-id="59986-113">API usecase</span><span class="sxs-lookup"><span data-stu-id="59986-113">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="59986-114">**OTTIENI** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="59986-114">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="59986-115">IP</span><span class="sxs-lookup"><span data-stu-id="59986-115">IP</span></span> | <span data-ttu-id="59986-116">1000 / minuto</span><span class="sxs-lookup"><span data-stu-id="59986-116">1000 / minute</span></span> | <span data-ttu-id="59986-117">Eseguire una query dei metadati del pacchetto NuGet tramite OData v1 `Packages` raccolta</span><span class="sxs-lookup"><span data-stu-id="59986-117">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="59986-118">**OTTIENI** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="59986-118">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="59986-119">IP</span><span class="sxs-lookup"><span data-stu-id="59986-119">IP</span></span> | <span data-ttu-id="59986-120">3000 / minuto</span><span class="sxs-lookup"><span data-stu-id="59986-120">3000 / minute</span></span> | <span data-ttu-id="59986-121">Ricerca per i pacchetti NuGet tramite l'endpoint di ricerca v1</span><span class="sxs-lookup"><span data-stu-id="59986-121">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="59986-122">**OTTIENI** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="59986-122">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="59986-123">IP</span><span class="sxs-lookup"><span data-stu-id="59986-123">IP</span></span> | <span data-ttu-id="59986-124">20000 / minuto</span><span class="sxs-lookup"><span data-stu-id="59986-124">20000 / minute</span></span> | <span data-ttu-id="59986-125">Eseguire una query dei metadati del pacchetto NuGet tramite v2 OData `Packages` raccolta</span><span class="sxs-lookup"><span data-stu-id="59986-125">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="59986-126">**OTTIENI** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="59986-126">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="59986-127">IP</span><span class="sxs-lookup"><span data-stu-id="59986-127">IP</span></span> | <span data-ttu-id="59986-128">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="59986-128">100 / minute</span></span> | <span data-ttu-id="59986-129">Eseguire una query conteggio pacchetto NuGet tramite v2 OData `Packages` raccolta</span><span class="sxs-lookup"><span data-stu-id="59986-129">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="59986-130">Pacchetto Push ed esclusione</span><span class="sxs-lookup"><span data-stu-id="59986-130">Package Push and Unlist</span></span>

| <span data-ttu-id="59986-131">API</span><span class="sxs-lookup"><span data-stu-id="59986-131">API</span></span> | <span data-ttu-id="59986-132">Tipo di limite</span><span class="sxs-lookup"><span data-stu-id="59986-132">Limit Type</span></span> | <span data-ttu-id="59986-133">Valore del limite</span><span class="sxs-lookup"><span data-stu-id="59986-133">Limit Value</span></span> | <span data-ttu-id="59986-134">API usecase</span><span class="sxs-lookup"><span data-stu-id="59986-134">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="59986-135">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="59986-135">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="59986-136">Chiave API</span><span class="sxs-lookup"><span data-stu-id="59986-136">API Key</span></span> | <span data-ttu-id="59986-137">250 / ora</span><span class="sxs-lookup"><span data-stu-id="59986-137">250 / hour</span></span> | <span data-ttu-id="59986-138">Caricare un nuovo pacchetto NuGet (versione) tramite l'endpoint di push v2</span><span class="sxs-lookup"><span data-stu-id="59986-138">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="59986-139">**ELIMINARE** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="59986-139">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="59986-140">Chiave API</span><span class="sxs-lookup"><span data-stu-id="59986-140">API Key</span></span> | <span data-ttu-id="59986-141">250 / ora</span><span class="sxs-lookup"><span data-stu-id="59986-141">250 / hour</span></span> | <span data-ttu-id="59986-142">Esclusione di un pacchetto NuGet (versione) tramite l'endpoint v2</span><span class="sxs-lookup"><span data-stu-id="59986-142">Unlist a NuGet package (version) via v2 endpoint</span></span> 
