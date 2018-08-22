---
title: per individuare le versioni nuget.exe Tools.JSON
description: L'endpoint per
author: jver
ms.author: jver
manager: skofman
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d11e79cd9109e1760189e848e35ff322be026a4d
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2018
ms.locfileid: "40248355"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="789d8-103">per individuare le versioni nuget.exe Tools.JSON</span><span class="sxs-lookup"><span data-stu-id="789d8-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="789d8-104">Attualmente, esistono alcuni modi per ottenere la versione più recente di nuget.exe nel computer in modo gestibile tramite script.</span><span class="sxs-lookup"><span data-stu-id="789d8-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="789d8-105">Ad esempio, è possibile scaricare ed estrarre il [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) pacchetti da nuget.org. Questo ha un livello di complessità perché sia richiede che sia già stato nuget.exe (per `nuget.exe install`) o è necessario decomprimere il pacchetto. nupkg usando uno strumento di decompressione di base e trovare binario interno.</span><span class="sxs-lookup"><span data-stu-id="789d8-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="789d8-106">Se hai già nuget.exe, è anche possibile usare `nuget.exe update -self`, ma anche è necessario disporre di una copia esistente di nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="789d8-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="789d8-107">Questo approccio anche si aggiorna alla versione più recente.</span><span class="sxs-lookup"><span data-stu-id="789d8-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="789d8-108">Non consente l'uso di una versione specifica.</span><span class="sxs-lookup"><span data-stu-id="789d8-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="789d8-109">Il `tools.json` endpoint è disponibile per entrambi è stato risolto l'avvio automatico e di offrire il controllo della versione di nuget.exe scaricato.</span><span class="sxs-lookup"><span data-stu-id="789d8-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="789d8-110">Ciò è utilizzabile negli ambienti CI/CD o script personalizzati per individuare e scaricare qualsiasi versione rilasciata di nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="789d8-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="789d8-111">Il `tools.json` endpoint possono essere recuperate tramite una richiesta HTTP non autenticata (ad esempio `Invoke-WebRequest` in PowerShell o `wget`).</span><span class="sxs-lookup"><span data-stu-id="789d8-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="789d8-112">Può essere analizzata usando un deserializzatore JSON né autenticate di download successivi nuget.exe che URL può anche essere recuperati tramite richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="789d8-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="789d8-113">L'endpoint può essere recuperato usando la `GET` metodo:</span><span class="sxs-lookup"><span data-stu-id="789d8-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="789d8-114">Il [dello schema JSON](http://json-schema.org/) per l'endpoint è disponibile qui:</span><span class="sxs-lookup"><span data-stu-id="789d8-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="789d8-115">Risposta</span><span class="sxs-lookup"><span data-stu-id="789d8-115">Response</span></span>

<span data-ttu-id="789d8-116">La risposta è un documento JSON contenente tutte le versioni disponibili di nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="789d8-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="789d8-117">L'oggetto JSON radice ha la proprietà seguente:</span><span class="sxs-lookup"><span data-stu-id="789d8-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="789d8-118">nome</span><span class="sxs-lookup"><span data-stu-id="789d8-118">Name</span></span>      | <span data-ttu-id="789d8-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="789d8-119">Type</span></span>             | <span data-ttu-id="789d8-120">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="789d8-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="789d8-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="789d8-121">nuget.exe</span></span> | <span data-ttu-id="789d8-122">Matrice di oggetti</span><span class="sxs-lookup"><span data-stu-id="789d8-122">array of objects</span></span> | <span data-ttu-id="789d8-123">sì</span><span class="sxs-lookup"><span data-stu-id="789d8-123">yes</span></span>

<span data-ttu-id="789d8-124">Ogni oggetto di `nuget.exe` matrice presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="789d8-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="789d8-125">nome</span><span class="sxs-lookup"><span data-stu-id="789d8-125">Name</span></span>     | <span data-ttu-id="789d8-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="789d8-126">Type</span></span>   | <span data-ttu-id="789d8-127">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="789d8-127">Required</span></span> | <span data-ttu-id="789d8-128">Note</span><span class="sxs-lookup"><span data-stu-id="789d8-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="789d8-129">version</span><span class="sxs-lookup"><span data-stu-id="789d8-129">version</span></span>  | <span data-ttu-id="789d8-130">stringa</span><span class="sxs-lookup"><span data-stu-id="789d8-130">string</span></span> | <span data-ttu-id="789d8-131">sì</span><span class="sxs-lookup"><span data-stu-id="789d8-131">yes</span></span>      | <span data-ttu-id="789d8-132">Una stringa di SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="789d8-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="789d8-133">url</span><span class="sxs-lookup"><span data-stu-id="789d8-133">url</span></span>      | <span data-ttu-id="789d8-134">stringa</span><span class="sxs-lookup"><span data-stu-id="789d8-134">string</span></span> | <span data-ttu-id="789d8-135">sì</span><span class="sxs-lookup"><span data-stu-id="789d8-135">yes</span></span>      | <span data-ttu-id="789d8-136">Un URL assoluto per il download di questa versione di nuget.exe</span><span class="sxs-lookup"><span data-stu-id="789d8-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="789d8-137">Fase</span><span class="sxs-lookup"><span data-stu-id="789d8-137">stage</span></span>    | <span data-ttu-id="789d8-138">stringa</span><span class="sxs-lookup"><span data-stu-id="789d8-138">string</span></span> | <span data-ttu-id="789d8-139">sì</span><span class="sxs-lookup"><span data-stu-id="789d8-139">yes</span></span>      | <span data-ttu-id="789d8-140">Una stringa di enum</span><span class="sxs-lookup"><span data-stu-id="789d8-140">An enum string</span></span>
<span data-ttu-id="789d8-141">caricato</span><span class="sxs-lookup"><span data-stu-id="789d8-141">uploaded</span></span> | <span data-ttu-id="789d8-142">stringa</span><span class="sxs-lookup"><span data-stu-id="789d8-142">string</span></span> | <span data-ttu-id="789d8-143">sì</span><span class="sxs-lookup"><span data-stu-id="789d8-143">yes</span></span>      | <span data-ttu-id="789d8-144">Un timestamp di quando è stata resa disponibile la versione approssimativo</span><span class="sxs-lookup"><span data-stu-id="789d8-144">An approximate timestamp of when the version was made available</span></span>

<span data-ttu-id="789d8-145">Gli elementi della matrice verranno ordinati in senso decrescente, SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="789d8-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="789d8-146">Questa garanzia è progettata per semplificare il carico di lavoro in un client cerca la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="789d8-146">This guarantee is meant to ease the burden on a client looking for the latest version.</span></span> 

<span data-ttu-id="789d8-147">Il `stage` proprietà indica la modalità vettect questa versione dello strumento.</span><span class="sxs-lookup"><span data-stu-id="789d8-147">The `stage` property indicates how vettect this version of the tool is.</span></span> 

<span data-ttu-id="789d8-148">Fase</span><span class="sxs-lookup"><span data-stu-id="789d8-148">Stage</span></span>              | <span data-ttu-id="789d8-149">Significato</span><span class="sxs-lookup"><span data-stu-id="789d8-149">Meaning</span></span>
------------------ | ------
<span data-ttu-id="789d8-150">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="789d8-150">EarlyAccessPreview</span></span> | <span data-ttu-id="789d8-151">Non è ancora visibile sulla [pagina web di download](https://www.nuget.org/downloads) e deve essere convalidato dai partner</span><span class="sxs-lookup"><span data-stu-id="789d8-151">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="789d8-152">Rilasciata</span><span class="sxs-lookup"><span data-stu-id="789d8-152">Released</span></span>           | <span data-ttu-id="789d8-153">Disponibile nel sito di download, ma non è ancora consigliato per l'utilizzo di diffusa</span><span class="sxs-lookup"><span data-stu-id="789d8-153">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="789d8-154">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="789d8-154">ReleasedAndBlessed</span></span> | <span data-ttu-id="789d8-155">Disponibile nel sito di download ed è consigliata per l'utilizzo</span><span class="sxs-lookup"><span data-stu-id="789d8-155">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="789d8-156">Un approccio semplice per avere la versione più recente, versione consigliata deve eseguire la prima versione nell'elenco che contiene il `stage` pari a `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="789d8-156">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span>

<span data-ttu-id="789d8-157">Il `NuGet.CommandLine` pacchetto in nuget.org in genere viene aggiornata solo con `ReleasedAndBlessed` versioni.</span><span class="sxs-lookup"><span data-stu-id="789d8-157">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="789d8-158">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="789d8-158">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="789d8-159">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="789d8-159">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]