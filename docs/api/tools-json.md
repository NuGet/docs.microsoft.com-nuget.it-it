---
title: tools.json per individuare le versioni di nuget.exe
description: Endpoint per
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773824"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="0f315-103">tools.json per individuare le versioni di nuget.exe</span><span class="sxs-lookup"><span data-stu-id="0f315-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="0f315-104">Attualmente, esistono diversi modi per ottenere la versione più recente di nuget.exe nel computer in modo da poter eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="0f315-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="0f315-105">Ad esempio, è possibile scaricare ed estrarre il [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) pacchetto da NuGet.org. Questa operazione presenta una certa complessità poiché richiede che sia già presente nuget.exe (per `nuget.exe install` ) o che sia necessario decomprimere il file con estensione nupkg usando uno strumento di decompressione di base e trovare il file binario all'interno di.</span><span class="sxs-lookup"><span data-stu-id="0f315-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="0f315-106">Se si dispone già di nuget.exe, è anche possibile utilizzare `nuget.exe update -self` , tuttavia è necessario disporre di una copia di nuget.exe esistente.</span><span class="sxs-lookup"><span data-stu-id="0f315-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="0f315-107">Questo approccio consente inoltre di aggiornare la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="0f315-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="0f315-108">Non consente l'uso di una versione specifica.</span><span class="sxs-lookup"><span data-stu-id="0f315-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="0f315-109">L' `tools.json` endpoint è disponibile sia per risolvere il problema di bootstrap che per consentire il controllo della versione di nuget.exe scaricata.</span><span class="sxs-lookup"><span data-stu-id="0f315-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="0f315-110">Questo può essere usato negli ambienti CI/CD o negli script personalizzati per individuare e scaricare qualsiasi versione rilasciata di nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="0f315-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="0f315-111">L' `tools.json` endpoint può essere recuperato usando una richiesta HTTP non autenticata, ad esempio `Invoke-WebRequest` in PowerShell o `wget` .</span><span class="sxs-lookup"><span data-stu-id="0f315-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="0f315-112">Può essere analizzato usando un deserializzatore JSON e gli URL di download nuget.exe successivi possono anche essere recuperati tramite richieste HTTP non autenticate.</span><span class="sxs-lookup"><span data-stu-id="0f315-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="0f315-113">L'endpoint può essere recuperato utilizzando il `GET` Metodo:</span><span class="sxs-lookup"><span data-stu-id="0f315-113">The endpoint can be fetched using the `GET` method:</span></span>

```
GET https://dist.nuget.org/tools.json
```

<span data-ttu-id="0f315-114">Lo [schema JSON](https://json-schema.org/) per l'endpoint è disponibile qui:</span><span class="sxs-lookup"><span data-stu-id="0f315-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a><span data-ttu-id="0f315-115">Risposta</span><span class="sxs-lookup"><span data-stu-id="0f315-115">Response</span></span>

<span data-ttu-id="0f315-116">La risposta è un documento JSON contenente tutte le versioni disponibili di nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="0f315-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="0f315-117">L'oggetto JSON radice presenta la proprietà seguente:</span><span class="sxs-lookup"><span data-stu-id="0f315-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="0f315-118">Nome</span><span class="sxs-lookup"><span data-stu-id="0f315-118">Name</span></span>      | <span data-ttu-id="0f315-119">Type</span><span class="sxs-lookup"><span data-stu-id="0f315-119">Type</span></span>             | <span data-ttu-id="0f315-120">Necessario</span><span class="sxs-lookup"><span data-stu-id="0f315-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="0f315-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="0f315-121">nuget.exe</span></span> | <span data-ttu-id="0f315-122">matrice di oggetti</span><span class="sxs-lookup"><span data-stu-id="0f315-122">array of objects</span></span> | <span data-ttu-id="0f315-123">sì</span><span class="sxs-lookup"><span data-stu-id="0f315-123">yes</span></span>

<span data-ttu-id="0f315-124">Ogni oggetto nella `nuget.exe` matrice presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="0f315-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="0f315-125">Nome</span><span class="sxs-lookup"><span data-stu-id="0f315-125">Name</span></span>     | <span data-ttu-id="0f315-126">Type</span><span class="sxs-lookup"><span data-stu-id="0f315-126">Type</span></span>   | <span data-ttu-id="0f315-127">Necessario</span><span class="sxs-lookup"><span data-stu-id="0f315-127">Required</span></span> | <span data-ttu-id="0f315-128">Note</span><span class="sxs-lookup"><span data-stu-id="0f315-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="0f315-129">version</span><span class="sxs-lookup"><span data-stu-id="0f315-129">version</span></span>  | <span data-ttu-id="0f315-130">string</span><span class="sxs-lookup"><span data-stu-id="0f315-130">string</span></span> | <span data-ttu-id="0f315-131">sì</span><span class="sxs-lookup"><span data-stu-id="0f315-131">yes</span></span>      | <span data-ttu-id="0f315-132">Stringa SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="0f315-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="0f315-133">url</span><span class="sxs-lookup"><span data-stu-id="0f315-133">url</span></span>      | <span data-ttu-id="0f315-134">string</span><span class="sxs-lookup"><span data-stu-id="0f315-134">string</span></span> | <span data-ttu-id="0f315-135">sì</span><span class="sxs-lookup"><span data-stu-id="0f315-135">yes</span></span>      | <span data-ttu-id="0f315-136">URL assoluto per il download di questa versione di nuget.exe</span><span class="sxs-lookup"><span data-stu-id="0f315-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="0f315-137">fase</span><span class="sxs-lookup"><span data-stu-id="0f315-137">stage</span></span>    | <span data-ttu-id="0f315-138">string</span><span class="sxs-lookup"><span data-stu-id="0f315-138">string</span></span> | <span data-ttu-id="0f315-139">sì</span><span class="sxs-lookup"><span data-stu-id="0f315-139">yes</span></span>      | <span data-ttu-id="0f315-140">Stringa enum</span><span class="sxs-lookup"><span data-stu-id="0f315-140">An enum string</span></span>
<span data-ttu-id="0f315-141">caricato</span><span class="sxs-lookup"><span data-stu-id="0f315-141">uploaded</span></span> | <span data-ttu-id="0f315-142">string</span><span class="sxs-lookup"><span data-stu-id="0f315-142">string</span></span> | <span data-ttu-id="0f315-143">sì</span><span class="sxs-lookup"><span data-stu-id="0f315-143">yes</span></span>      | <span data-ttu-id="0f315-144">Timestamp ISO 8601 approssimativo di quando è stata resa disponibile la versione</span><span class="sxs-lookup"><span data-stu-id="0f315-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="0f315-145">Gli elementi nella matrice verranno ordinati in ordine decrescente, SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="0f315-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="0f315-146">Questa garanzia è destinata a ridurre il carico di un client interessato al numero di versione più alto.</span><span class="sxs-lookup"><span data-stu-id="0f315-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="0f315-147">Ciò significa tuttavia che l'elenco non è ordinato in ordine cronologico.</span><span class="sxs-lookup"><span data-stu-id="0f315-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="0f315-148">Se, ad esempio, una versione principale inferiore viene gestita in una data successiva a una versione principale più elevata, la versione servita non verrà visualizzata nella parte superiore dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="0f315-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="0f315-149">Se si vuole che la versione più recente rilasciata da *timestamp*, è sufficiente ordinare la matrice in base alla `uploaded` stringa.</span><span class="sxs-lookup"><span data-stu-id="0f315-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="0f315-150">Questa operazione funziona perché il `uploaded` timestamp è nel formato [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) , che può essere ordinato in ordine cronologico usando un ordinamento lessicografico, ovvero un ordinamento stringa semplice.</span><span class="sxs-lookup"><span data-stu-id="0f315-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="0f315-151">La `stage` proprietà indica il modo in cui la versione dello strumento è stata controllata.</span><span class="sxs-lookup"><span data-stu-id="0f315-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="0f315-152">Fase</span><span class="sxs-lookup"><span data-stu-id="0f315-152">Stage</span></span>              | <span data-ttu-id="0f315-153">Significato</span><span class="sxs-lookup"><span data-stu-id="0f315-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="0f315-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="0f315-154">EarlyAccessPreview</span></span> | <span data-ttu-id="0f315-155">Non ancora visibile nella [pagina Web di download](https://www.nuget.org/downloads) e deve essere convalidato dai partner</span><span class="sxs-lookup"><span data-stu-id="0f315-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="0f315-156">Rilasciata</span><span class="sxs-lookup"><span data-stu-id="0f315-156">Released</span></span>           | <span data-ttu-id="0f315-157">Disponibile nel sito di download, ma non è ancora consigliato per un consumo di ampia diffusione</span><span class="sxs-lookup"><span data-stu-id="0f315-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="0f315-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="0f315-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="0f315-159">Disponibile nel sito di download ed è consigliato per l'utilizzo</span><span class="sxs-lookup"><span data-stu-id="0f315-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="0f315-160">Un approccio semplice per avere la versione più recente consigliata consiste nell'usare la prima versione dell'elenco con il `stage` valore `ReleasedAndBlessed` .</span><span class="sxs-lookup"><span data-stu-id="0f315-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="0f315-161">Questa operazione funziona perché le versioni sono ordinate in base all'ordine di SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="0f315-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="0f315-162">Il `NuGet.CommandLine` pacchetto in NuGet.org viene in genere aggiornato solo con le `ReleasedAndBlessed` versioni.</span><span class="sxs-lookup"><span data-stu-id="0f315-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="0f315-163">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="0f315-163">Sample request</span></span>

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a><span data-ttu-id="0f315-164">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="0f315-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
