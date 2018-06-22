---
title: Completamento automatico, NuGet API
description: Il servizio di completamento automatico di ricerca supporta le versioni e rilevamento interattivo di ID di pacchetto.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d5e1936c6c5406a1a376c16b2bad5351320dfb4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822136"
---
# <a name="autocomplete"></a><span data-ttu-id="cde93-103">Completamento automatico</span><span class="sxs-lookup"><span data-stu-id="cde93-103">Autocomplete</span></span>

<span data-ttu-id="cde93-104">È possibile creare un pacchetto ID e la versione autocomplete esperienza tramite l'API V3.</span><span class="sxs-lookup"><span data-stu-id="cde93-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="cde93-105">La risorsa utilizzata per l'esecuzione di query di completamento automatico è il `SearchAutocompleteService` risorsa trovata nel [indice servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="cde93-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="cde93-106">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="cde93-106">Versioning</span></span>

<span data-ttu-id="cde93-107">Nell'esempio `@type` vengono utilizzati i valori:</span><span class="sxs-lookup"><span data-stu-id="cde93-107">The following `@type` values are used:</span></span>

<span data-ttu-id="cde93-108">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="cde93-108">@type value</span></span>                          | <span data-ttu-id="cde93-109">Note</span><span class="sxs-lookup"><span data-stu-id="cde93-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="cde93-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="cde93-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="cde93-111">La versione iniziale</span><span class="sxs-lookup"><span data-stu-id="cde93-111">The initial release</span></span>
<span data-ttu-id="cde93-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="cde93-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="cde93-113">Alias di `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="cde93-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="cde93-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="cde93-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="cde93-115">Alias di `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="cde93-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="cde93-116">URL di base</span><span class="sxs-lookup"><span data-stu-id="cde93-116">Base URL</span></span>

<span data-ttu-id="cde93-117">L'URL di base per le API seguente è il valore di `@id` proprietà associati a uno della risorsa menzionati in precedenza `@type` valori.</span><span class="sxs-lookup"><span data-stu-id="cde93-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="cde93-118">Nel documento seguente, il segnaposto URL di base `{@id}` verrà utilizzato.</span><span class="sxs-lookup"><span data-stu-id="cde93-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="cde93-119">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="cde93-119">HTTP Methods</span></span>

<span data-ttu-id="cde93-120">Tutti gli URL trovati, il supporto di risorsa di registrazione, i metodi HTTP `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="cde93-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="cde93-121">Ricerca per ID pacchetto</span><span class="sxs-lookup"><span data-stu-id="cde93-121">Search for package IDs</span></span>

<span data-ttu-id="cde93-122">Il primo completamento automatico API supporta la ricerca di parte di una stringa di ID di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cde93-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="cde93-123">Questo è molto utile quando si desidera fornire una funzionalità typeahead pacchetto in un'interfaccia utente integrata con un'origine del pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="cde93-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="cde93-124">Un pacchetto con le versioni non in elenco non verrà visualizzati nei risultati.</span><span class="sxs-lookup"><span data-stu-id="cde93-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="cde93-125">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="cde93-125">Request parameters</span></span>

<span data-ttu-id="cde93-126">nome</span><span class="sxs-lookup"><span data-stu-id="cde93-126">Name</span></span>        | <span data-ttu-id="cde93-127">In</span><span class="sxs-lookup"><span data-stu-id="cde93-127">In</span></span>     | <span data-ttu-id="cde93-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="cde93-128">Type</span></span>    | <span data-ttu-id="cde93-129">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="cde93-129">Required</span></span> | <span data-ttu-id="cde93-130">Note</span><span class="sxs-lookup"><span data-stu-id="cde93-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="cde93-131">q</span><span class="sxs-lookup"><span data-stu-id="cde93-131">q</span></span>           | <span data-ttu-id="cde93-132">URL</span><span class="sxs-lookup"><span data-stu-id="cde93-132">URL</span></span>    | <span data-ttu-id="cde93-133">stringa</span><span class="sxs-lookup"><span data-stu-id="cde93-133">string</span></span>  | <span data-ttu-id="cde93-134">No</span><span class="sxs-lookup"><span data-stu-id="cde93-134">no</span></span>       | <span data-ttu-id="cde93-135">La stringa da confrontare con l'ID di pacchetto</span><span class="sxs-lookup"><span data-stu-id="cde93-135">The string to compare against package IDs</span></span>
<span data-ttu-id="cde93-136">skip</span><span class="sxs-lookup"><span data-stu-id="cde93-136">skip</span></span>        | <span data-ttu-id="cde93-137">URL</span><span class="sxs-lookup"><span data-stu-id="cde93-137">URL</span></span>    | <span data-ttu-id="cde93-138">numero intero</span><span class="sxs-lookup"><span data-stu-id="cde93-138">integer</span></span> | <span data-ttu-id="cde93-139">No</span><span class="sxs-lookup"><span data-stu-id="cde93-139">no</span></span>       | <span data-ttu-id="cde93-140">Il numero di risultati da ignorare per l'impaginazione</span><span class="sxs-lookup"><span data-stu-id="cde93-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="cde93-141">Take</span><span class="sxs-lookup"><span data-stu-id="cde93-141">take</span></span>        | <span data-ttu-id="cde93-142">URL</span><span class="sxs-lookup"><span data-stu-id="cde93-142">URL</span></span>    | <span data-ttu-id="cde93-143">numero intero</span><span class="sxs-lookup"><span data-stu-id="cde93-143">integer</span></span> | <span data-ttu-id="cde93-144">No</span><span class="sxs-lookup"><span data-stu-id="cde93-144">no</span></span>       | <span data-ttu-id="cde93-145">Il numero di risultati da restituire, per la paginazione</span><span class="sxs-lookup"><span data-stu-id="cde93-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="cde93-146">versione provvisoria</span><span class="sxs-lookup"><span data-stu-id="cde93-146">prerelease</span></span>  | <span data-ttu-id="cde93-147">URL</span><span class="sxs-lookup"><span data-stu-id="cde93-147">URL</span></span>    | <span data-ttu-id="cde93-148">boolean</span><span class="sxs-lookup"><span data-stu-id="cde93-148">boolean</span></span> | <span data-ttu-id="cde93-149">No</span><span class="sxs-lookup"><span data-stu-id="cde93-149">no</span></span>       | <span data-ttu-id="cde93-150">`true` o `false` determinano l'opportunità di includere [pacchetti versione non definitiva](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="cde93-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="cde93-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="cde93-151">semVerLevel</span></span> | <span data-ttu-id="cde93-152">URL</span><span class="sxs-lookup"><span data-stu-id="cde93-152">URL</span></span>    | <span data-ttu-id="cde93-153">stringa</span><span class="sxs-lookup"><span data-stu-id="cde93-153">string</span></span>  | <span data-ttu-id="cde93-154">No</span><span class="sxs-lookup"><span data-stu-id="cde93-154">no</span></span>       | <span data-ttu-id="cde93-155">Una stringa di versione SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="cde93-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="cde93-156">La query con completamento automatico `q` viene analizzato in modo che è definito dall'implementazione del server.</span><span class="sxs-lookup"><span data-stu-id="cde93-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="cde93-157">NuGet.org supporta l'esecuzione di query per il prefisso di token ID di pacchetto, che sono pezzi dell'ID prodotto da [PROD143] e originale da caratteri iniziali di case e simboli.</span><span class="sxs-lookup"><span data-stu-id="cde93-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="cde93-158">Il `skip` valori predefiniti dei parametri su 0.</span><span class="sxs-lookup"><span data-stu-id="cde93-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="cde93-159">Il `take` parametro deve essere un numero intero maggiore di zero.</span><span class="sxs-lookup"><span data-stu-id="cde93-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="cde93-160">L'implementazione del server potrebbe avere un valore massimo.</span><span class="sxs-lookup"><span data-stu-id="cde93-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="cde93-161">Se `prerelease` non viene fornito, vengono esclusi i pacchetti pre-release.</span><span class="sxs-lookup"><span data-stu-id="cde93-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="cde93-162">Il `semVerLevel` parametro di query viene utilizzato per acconsentire esplicitamente a [SemVer 2.0.0 pacchetti](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="cde93-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="cde93-163">Se questo parametro di query viene esclusa, verranno restituiti solo gli ID di pacchetto con le versioni compatibili SemVer 1.0.0 (con il [standard controllo delle versioni NuGet](../reference/package-versioning.md) avvertenze, ad esempio le stringhe di versione con 4 elementi di tipo integer).</span><span class="sxs-lookup"><span data-stu-id="cde93-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="cde93-164">Se `semVerLevel=2.0.0` viene fornito, verranno restituiti SemVer 1.0.0 sia pacchetti compatibili SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="cde93-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="cde93-165">Vedere il [supporto SemVer 2.0.0 per nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="cde93-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="cde93-166">Risposta</span><span class="sxs-lookup"><span data-stu-id="cde93-166">Response</span></span>

<span data-ttu-id="cde93-167">La risposta è il documento JSON che contiene fino a `take` risultati di completamento automatico.</span><span class="sxs-lookup"><span data-stu-id="cde93-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="cde93-168">Oggetto JSON radice ha le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="cde93-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="cde93-169">nome</span><span class="sxs-lookup"><span data-stu-id="cde93-169">Name</span></span>      | <span data-ttu-id="cde93-170">Tipo</span><span class="sxs-lookup"><span data-stu-id="cde93-170">Type</span></span>             | <span data-ttu-id="cde93-171">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="cde93-171">Required</span></span> | <span data-ttu-id="cde93-172">Note</span><span class="sxs-lookup"><span data-stu-id="cde93-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="cde93-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="cde93-173">totalHits</span></span> | <span data-ttu-id="cde93-174">numero intero</span><span class="sxs-lookup"><span data-stu-id="cde93-174">integer</span></span>          | <span data-ttu-id="cde93-175">sì</span><span class="sxs-lookup"><span data-stu-id="cde93-175">yes</span></span>      | <span data-ttu-id="cde93-176">Il numero complessivo di corrispondenze, non considerando `skip` e `take`</span><span class="sxs-lookup"><span data-stu-id="cde93-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="cde93-177">Data</span><span class="sxs-lookup"><span data-stu-id="cde93-177">data</span></span>      | <span data-ttu-id="cde93-178">Matrice di stringhe</span><span class="sxs-lookup"><span data-stu-id="cde93-178">array of strings</span></span> | <span data-ttu-id="cde93-179">sì</span><span class="sxs-lookup"><span data-stu-id="cde93-179">yes</span></span>      | <span data-ttu-id="cde93-180">Il pacchetto corrispondente di ID dalla richiesta</span><span class="sxs-lookup"><span data-stu-id="cde93-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="cde93-181">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="cde93-181">Sample request</span></span>

<span data-ttu-id="cde93-182">OTTIENI https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="cde93-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="cde93-183">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="cde93-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="cde93-184">Enumerare le versioni di pacchetto</span><span class="sxs-lookup"><span data-stu-id="cde93-184">Enumerate package versions</span></span>

<span data-ttu-id="cde93-185">Dopo che viene rilevato un ID pacchetto tramite l'API precedente, un client può utilizzare l'API di completamento automatico per enumerare le versioni di pacchetto per un ID di pacchetto fornito.</span><span class="sxs-lookup"><span data-stu-id="cde93-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="cde93-186">Una versione del pacchetto che è incluso nell'elenco non verrà visualizzato nei risultati.</span><span class="sxs-lookup"><span data-stu-id="cde93-186">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="cde93-187">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="cde93-187">Request parameters</span></span>

<span data-ttu-id="cde93-188">nome</span><span class="sxs-lookup"><span data-stu-id="cde93-188">Name</span></span>        | <span data-ttu-id="cde93-189">In</span><span class="sxs-lookup"><span data-stu-id="cde93-189">In</span></span>     | <span data-ttu-id="cde93-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="cde93-190">Type</span></span>    | <span data-ttu-id="cde93-191">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="cde93-191">Required</span></span> | <span data-ttu-id="cde93-192">Note</span><span class="sxs-lookup"><span data-stu-id="cde93-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="cde93-193">ID</span><span class="sxs-lookup"><span data-stu-id="cde93-193">id</span></span>          | <span data-ttu-id="cde93-194">URL</span><span class="sxs-lookup"><span data-stu-id="cde93-194">URL</span></span>    | <span data-ttu-id="cde93-195">stringa</span><span class="sxs-lookup"><span data-stu-id="cde93-195">string</span></span>  | <span data-ttu-id="cde93-196">sì</span><span class="sxs-lookup"><span data-stu-id="cde93-196">yes</span></span>      | <span data-ttu-id="cde93-197">Per recuperare le versioni per l'ID del pacchetto</span><span class="sxs-lookup"><span data-stu-id="cde93-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="cde93-198">versione provvisoria</span><span class="sxs-lookup"><span data-stu-id="cde93-198">prerelease</span></span>  | <span data-ttu-id="cde93-199">URL</span><span class="sxs-lookup"><span data-stu-id="cde93-199">URL</span></span>    | <span data-ttu-id="cde93-200">boolean</span><span class="sxs-lookup"><span data-stu-id="cde93-200">boolean</span></span> | <span data-ttu-id="cde93-201">No</span><span class="sxs-lookup"><span data-stu-id="cde93-201">no</span></span>       | <span data-ttu-id="cde93-202">`true` o `false` determinano l'opportunità di includere [pacchetti versione non definitiva](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="cde93-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="cde93-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="cde93-203">semVerLevel</span></span> | <span data-ttu-id="cde93-204">URL</span><span class="sxs-lookup"><span data-stu-id="cde93-204">URL</span></span>    | <span data-ttu-id="cde93-205">stringa</span><span class="sxs-lookup"><span data-stu-id="cde93-205">string</span></span>  | <span data-ttu-id="cde93-206">No</span><span class="sxs-lookup"><span data-stu-id="cde93-206">no</span></span>       | <span data-ttu-id="cde93-207">Una stringa di versione SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="cde93-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="cde93-208">Se `prerelease` non viene fornito, vengono esclusi i pacchetti pre-release.</span><span class="sxs-lookup"><span data-stu-id="cde93-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="cde93-209">Il `semVerLevel` parametro di query viene utilizzato per acconsentire esplicitamente a pacchetti SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="cde93-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="cde93-210">Se questo parametro di query viene esclusa, verranno restituite solo le versioni SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="cde93-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="cde93-211">Se `semVerLevel=2.0.0` viene fornito, verranno restituite SemVer 1.0.0 sia versioni SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="cde93-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="cde93-212">Vedere il [supporto SemVer 2.0.0 per nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="cde93-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="cde93-213">Risposta</span><span class="sxs-lookup"><span data-stu-id="cde93-213">Response</span></span>

<span data-ttu-id="cde93-214">La risposta è il documento JSON che contiene tutte le versioni di pacchetto dell'ID pacchetto fornito, applicando un filtro per i parametri di query specificata.</span><span class="sxs-lookup"><span data-stu-id="cde93-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="cde93-215">Oggetto JSON radice dispone della proprietà seguente:</span><span class="sxs-lookup"><span data-stu-id="cde93-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="cde93-216">nome</span><span class="sxs-lookup"><span data-stu-id="cde93-216">Name</span></span>      | <span data-ttu-id="cde93-217">Tipo</span><span class="sxs-lookup"><span data-stu-id="cde93-217">Type</span></span>             | <span data-ttu-id="cde93-218">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="cde93-218">Required</span></span> | <span data-ttu-id="cde93-219">Note</span><span class="sxs-lookup"><span data-stu-id="cde93-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="cde93-220">Data</span><span class="sxs-lookup"><span data-stu-id="cde93-220">data</span></span>      | <span data-ttu-id="cde93-221">Matrice di stringhe</span><span class="sxs-lookup"><span data-stu-id="cde93-221">array of strings</span></span> | <span data-ttu-id="cde93-222">sì</span><span class="sxs-lookup"><span data-stu-id="cde93-222">yes</span></span>      | <span data-ttu-id="cde93-223">Le versioni del pacchetto corrispondente alla richiesta</span><span class="sxs-lookup"><span data-stu-id="cde93-223">The package versions matched by the request</span></span>

<span data-ttu-id="cde93-224">Le versioni del pacchetto nel `data` matrice può contenere i metadati di compilazione SemVer 2.0.0 (ad esempio `1.0.0+metadata`) se il `semVerLevel=2.0.0` è stato specificato nella stringa di query.</span><span class="sxs-lookup"><span data-stu-id="cde93-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="cde93-225">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="cde93-225">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="cde93-226">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="cde93-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
