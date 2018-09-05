---
title: Limiti, API NuGet di velocità
description: I limiti di velocità per impedirne l'uso improprio verrà applicata APIs di NuGet.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548677"
---
# <a name="rate-limits"></a><span data-ttu-id="99ec6-103">Limiti di velocità</span><span class="sxs-lookup"><span data-stu-id="99ec6-103">Rate Limits</span></span>

<span data-ttu-id="99ec6-104">L'API di NuGet.org consente di applicare la limitazione della frequenza per impedirne l'uso improprio.</span><span class="sxs-lookup"><span data-stu-id="99ec6-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="99ec6-105">Le richieste che superano il limite di frequenza restituiranno l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="99ec6-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="99ec6-106">Oltre a utilizzando i limiti di velocità di limitazione delle richieste, alcune API applicano anche quota.</span><span class="sxs-lookup"><span data-stu-id="99ec6-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="99ec6-107">Le richieste che superano la quota di restituiranno l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="99ec6-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="99ec6-108">Le tabelle seguenti elencano i limiti di velocità per l'API di NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="99ec6-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="99ec6-109">Ricerca di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="99ec6-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="99ec6-110">È consigliabile usare di NuGet.org [V3 API](https://docs.microsoft.com/nuget/api/search-query-service-resource) per la ricerca ad alte prestazioni e non siano presenti limitare attualmente.</span><span class="sxs-lookup"><span data-stu-id="99ec6-110">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="99ec6-111">Per versioni V1 e V2 API di ricerca, si applicano i limiti followins:</span><span class="sxs-lookup"><span data-stu-id="99ec6-111">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="99ec6-112">API</span><span class="sxs-lookup"><span data-stu-id="99ec6-112">API</span></span> | <span data-ttu-id="99ec6-113">Tipo di limite</span><span class="sxs-lookup"><span data-stu-id="99ec6-113">Limit Type</span></span> | <span data-ttu-id="99ec6-114">Valore del limite</span><span class="sxs-lookup"><span data-stu-id="99ec6-114">Limit Value</span></span> | <span data-ttu-id="99ec6-115">API usecase</span><span class="sxs-lookup"><span data-stu-id="99ec6-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="99ec6-116">**OTTIENI** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="99ec6-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="99ec6-117">IP</span><span class="sxs-lookup"><span data-stu-id="99ec6-117">IP</span></span> | <span data-ttu-id="99ec6-118">1000 al minuto</span><span class="sxs-lookup"><span data-stu-id="99ec6-118">1000 / minute</span></span> | <span data-ttu-id="99ec6-119">Eseguire query sui metadati del pacchetto NuGet tramite OData v1 `Packages` raccolta</span><span class="sxs-lookup"><span data-stu-id="99ec6-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="99ec6-120">**OTTIENI** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="99ec6-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="99ec6-121">IP</span><span class="sxs-lookup"><span data-stu-id="99ec6-121">IP</span></span> | <span data-ttu-id="99ec6-122">3000 / minuto</span><span class="sxs-lookup"><span data-stu-id="99ec6-122">3000 / minute</span></span> | <span data-ttu-id="99ec6-123">Cercare i pacchetti NuGet tramite l'endpoint ricerca v1</span><span class="sxs-lookup"><span data-stu-id="99ec6-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="99ec6-124">**OTTIENI** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="99ec6-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="99ec6-125">IP</span><span class="sxs-lookup"><span data-stu-id="99ec6-125">IP</span></span> | <span data-ttu-id="99ec6-126">20000 al minuto</span><span class="sxs-lookup"><span data-stu-id="99ec6-126">20000 / minute</span></span> | <span data-ttu-id="99ec6-127">Eseguire query sui metadati del pacchetto NuGet tramite OData v2 `Packages` raccolta</span><span class="sxs-lookup"><span data-stu-id="99ec6-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="99ec6-128">**OTTIENI** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="99ec6-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="99ec6-129">IP</span><span class="sxs-lookup"><span data-stu-id="99ec6-129">IP</span></span> | <span data-ttu-id="99ec6-130">100 al minuto</span><span class="sxs-lookup"><span data-stu-id="99ec6-130">100 / minute</span></span> | <span data-ttu-id="99ec6-131">Numero di pacchetti NuGet tramite OData v2 di query `Packages` raccolta</span><span class="sxs-lookup"><span data-stu-id="99ec6-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="99ec6-132">Pacchetto di effettuare il Push e rimuovere dall'elenco</span><span class="sxs-lookup"><span data-stu-id="99ec6-132">Package Push and Unlist</span></span>

| <span data-ttu-id="99ec6-133">API</span><span class="sxs-lookup"><span data-stu-id="99ec6-133">API</span></span> | <span data-ttu-id="99ec6-134">Tipo di limite</span><span class="sxs-lookup"><span data-stu-id="99ec6-134">Limit Type</span></span> | <span data-ttu-id="99ec6-135">Valore del limite</span><span class="sxs-lookup"><span data-stu-id="99ec6-135">Limit Value</span></span> | <span data-ttu-id="99ec6-136">API usecase</span><span class="sxs-lookup"><span data-stu-id="99ec6-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="99ec6-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="99ec6-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="99ec6-138">Chiave API</span><span class="sxs-lookup"><span data-stu-id="99ec6-138">API Key</span></span> | <span data-ttu-id="99ec6-139">250 / ora</span><span class="sxs-lookup"><span data-stu-id="99ec6-139">250 / hour</span></span> | <span data-ttu-id="99ec6-140">Caricare un nuovo pacchetto NuGet (versione) tramite l'endpoint v2 push</span><span class="sxs-lookup"><span data-stu-id="99ec6-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="99ec6-141">**DELETE** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="99ec6-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="99ec6-142">Chiave API</span><span class="sxs-lookup"><span data-stu-id="99ec6-142">API Key</span></span> | <span data-ttu-id="99ec6-143">250 / ora</span><span class="sxs-lookup"><span data-stu-id="99ec6-143">250 / hour</span></span> | <span data-ttu-id="99ec6-144">Rimuovere un pacchetto NuGet (versione) tramite l'endpoint v2</span><span class="sxs-lookup"><span data-stu-id="99ec6-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
