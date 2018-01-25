---
title: Completamento automatico, NuGet API | Documenti Microsoft
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Il servizio di completamento automatico di ricerca supporta le versioni e rilevamento interattivo di ID di pacchetto.
keywords: API di completamento automatico NuGet, ID del pacchetto NuGet ricerca, ID di pacchetto sottostringa
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7c984ca61799293d7832851b80cf3fefc4734288
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="autocomplete"></a><span data-ttu-id="8b18f-104">Completamento automatico</span><span class="sxs-lookup"><span data-stu-id="8b18f-104">Autocomplete</span></span>

<span data-ttu-id="8b18f-105">È possibile creare un pacchetto ID e la versione autocomplete esperienza tramite l'API V3.</span><span class="sxs-lookup"><span data-stu-id="8b18f-105">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="8b18f-106">La risorsa utilizzata per l'esecuzione di query di completamento automatico è il `SearchAutocompleteService` risorsa trovata nel [indice servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="8b18f-106">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="8b18f-107">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="8b18f-107">Versioning</span></span>

<span data-ttu-id="8b18f-108">Nell'esempio `@type` vengono utilizzati i valori:</span><span class="sxs-lookup"><span data-stu-id="8b18f-108">The following `@type` values are used:</span></span>

<span data-ttu-id="8b18f-109">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="8b18f-109">@type value</span></span>                          | <span data-ttu-id="8b18f-110">Note</span><span class="sxs-lookup"><span data-stu-id="8b18f-110">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="8b18f-111">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="8b18f-111">SearchAutocompleteService</span></span>            | <span data-ttu-id="8b18f-112">La versione iniziale</span><span class="sxs-lookup"><span data-stu-id="8b18f-112">The initial release</span></span>
<span data-ttu-id="8b18f-113">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="8b18f-113">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="8b18f-114">Alias di`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="8b18f-114">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="8b18f-115">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="8b18f-115">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="8b18f-116">Alias di`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="8b18f-116">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="8b18f-117">URL di base</span><span class="sxs-lookup"><span data-stu-id="8b18f-117">Base URL</span></span>

<span data-ttu-id="8b18f-118">L'URL di base per le API seguente è il valore di `@id` proprietà associati a uno della risorsa menzionati in precedenza `@type` valori.</span><span class="sxs-lookup"><span data-stu-id="8b18f-118">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="8b18f-119">Nel documento seguente, il segnaposto URL di base `{@id}` verrà utilizzato.</span><span class="sxs-lookup"><span data-stu-id="8b18f-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="8b18f-120">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="8b18f-120">HTTP Methods</span></span>

<span data-ttu-id="8b18f-121">Tutti gli URL trovati, il supporto di risorsa di registrazione, i metodi HTTP `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="8b18f-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="8b18f-122">Ricerca per ID pacchetto</span><span class="sxs-lookup"><span data-stu-id="8b18f-122">Search for package IDs</span></span>

<span data-ttu-id="8b18f-123">Il primo completamento automatico API supporta la ricerca di parte di una stringa di ID di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="8b18f-123">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="8b18f-124">Questo è molto utile quando si desidera fornire una funzionalità typeahead pacchetto in un'interfaccia utente integrata con un'origine del pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="8b18f-124">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="8b18f-125">Un pacchetto con le versioni non in elenco non verrà visualizzati nei risultati.</span><span class="sxs-lookup"><span data-stu-id="8b18f-125">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="8b18f-126">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="8b18f-126">Request parameters</span></span>

<span data-ttu-id="8b18f-127">nome</span><span class="sxs-lookup"><span data-stu-id="8b18f-127">Name</span></span>        | <span data-ttu-id="8b18f-128">In</span><span class="sxs-lookup"><span data-stu-id="8b18f-128">In</span></span>     | <span data-ttu-id="8b18f-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="8b18f-129">Type</span></span>    | <span data-ttu-id="8b18f-130">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b18f-130">Required</span></span> | <span data-ttu-id="8b18f-131">Note</span><span class="sxs-lookup"><span data-stu-id="8b18f-131">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="8b18f-132">q</span><span class="sxs-lookup"><span data-stu-id="8b18f-132">q</span></span>           | <span data-ttu-id="8b18f-133">URL</span><span class="sxs-lookup"><span data-stu-id="8b18f-133">URL</span></span>    | <span data-ttu-id="8b18f-134">stringa</span><span class="sxs-lookup"><span data-stu-id="8b18f-134">string</span></span>  | <span data-ttu-id="8b18f-135">No</span><span class="sxs-lookup"><span data-stu-id="8b18f-135">no</span></span>       | <span data-ttu-id="8b18f-136">La stringa da confrontare con l'ID di pacchetto</span><span class="sxs-lookup"><span data-stu-id="8b18f-136">The string to compare against package IDs</span></span>
<span data-ttu-id="8b18f-137">skip</span><span class="sxs-lookup"><span data-stu-id="8b18f-137">skip</span></span>        | <span data-ttu-id="8b18f-138">URL</span><span class="sxs-lookup"><span data-stu-id="8b18f-138">URL</span></span>    | <span data-ttu-id="8b18f-139">numero intero</span><span class="sxs-lookup"><span data-stu-id="8b18f-139">integer</span></span> | <span data-ttu-id="8b18f-140">No</span><span class="sxs-lookup"><span data-stu-id="8b18f-140">no</span></span>       | <span data-ttu-id="8b18f-141">Il numero di risultati da ignorare per l'impaginazione</span><span class="sxs-lookup"><span data-stu-id="8b18f-141">The number of results to skip, for pagination</span></span>
<span data-ttu-id="8b18f-142">Take</span><span class="sxs-lookup"><span data-stu-id="8b18f-142">take</span></span>        | <span data-ttu-id="8b18f-143">URL</span><span class="sxs-lookup"><span data-stu-id="8b18f-143">URL</span></span>    | <span data-ttu-id="8b18f-144">numero intero</span><span class="sxs-lookup"><span data-stu-id="8b18f-144">integer</span></span> | <span data-ttu-id="8b18f-145">No</span><span class="sxs-lookup"><span data-stu-id="8b18f-145">no</span></span>       | <span data-ttu-id="8b18f-146">Il numero di risultati da restituire, per la paginazione</span><span class="sxs-lookup"><span data-stu-id="8b18f-146">The number of results to return, for pagination</span></span>
<span data-ttu-id="8b18f-147">versione provvisoria</span><span class="sxs-lookup"><span data-stu-id="8b18f-147">prerelease</span></span>  | <span data-ttu-id="8b18f-148">URL</span><span class="sxs-lookup"><span data-stu-id="8b18f-148">URL</span></span>    | <span data-ttu-id="8b18f-149">boolean</span><span class="sxs-lookup"><span data-stu-id="8b18f-149">boolean</span></span> | <span data-ttu-id="8b18f-150">No</span><span class="sxs-lookup"><span data-stu-id="8b18f-150">no</span></span>       | <span data-ttu-id="8b18f-151">`true`o `false` stabilire se includere [pacchetti pre-release](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="8b18f-151">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="8b18f-152">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="8b18f-152">semVerLevel</span></span> | <span data-ttu-id="8b18f-153">URL</span><span class="sxs-lookup"><span data-stu-id="8b18f-153">URL</span></span>    | <span data-ttu-id="8b18f-154">stringa</span><span class="sxs-lookup"><span data-stu-id="8b18f-154">string</span></span>  | <span data-ttu-id="8b18f-155">No</span><span class="sxs-lookup"><span data-stu-id="8b18f-155">no</span></span>       | <span data-ttu-id="8b18f-156">Una stringa di versione SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="8b18f-156">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="8b18f-157">La query con completamento automatico `q` viene analizzato in modo che è definito dall'implementazione del server.</span><span class="sxs-lookup"><span data-stu-id="8b18f-157">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="8b18f-158">NuGet.org supporta l'esecuzione di query per il prefisso di token ID di pacchetto, che sono pezzi dell'ID prodotto da [PROD143] e originale da caratteri iniziali di case e simboli.</span><span class="sxs-lookup"><span data-stu-id="8b18f-158">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="8b18f-159">Il `skip` valori predefiniti dei parametri su 0.</span><span class="sxs-lookup"><span data-stu-id="8b18f-159">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="8b18f-160">Il `take` parametro deve essere un numero intero maggiore di zero.</span><span class="sxs-lookup"><span data-stu-id="8b18f-160">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="8b18f-161">L'implementazione del server potrebbe avere un valore massimo.</span><span class="sxs-lookup"><span data-stu-id="8b18f-161">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="8b18f-162">Se `prerelease` non viene fornito, vengono esclusi i pacchetti pre-release.</span><span class="sxs-lookup"><span data-stu-id="8b18f-162">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="8b18f-163">Il `semVerLevel` parametro di query viene utilizzato per acconsentire esplicitamente a [SemVer 2.0.0 pacchetti](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="8b18f-163">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="8b18f-164">Se questo parametro di query viene esclusa, verranno restituiti solo gli ID di pacchetto con le versioni compatibili SemVer 1.0.0 (con il [standard controllo delle versioni NuGet](../reference/package-versioning.md) avvertenze, ad esempio le stringhe di versione con 4 elementi di tipo integer).</span><span class="sxs-lookup"><span data-stu-id="8b18f-164">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="8b18f-165">Se `semVerLevel=2.0.0` viene fornito, verranno restituiti SemVer 1.0.0 sia pacchetti compatibili SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="8b18f-165">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="8b18f-166">Vedere il [supporto SemVer 2.0.0 per nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="8b18f-166">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="8b18f-167">Risposta</span><span class="sxs-lookup"><span data-stu-id="8b18f-167">Response</span></span>

<span data-ttu-id="8b18f-168">La risposta è il documento JSON che contiene fino a `take` risultati di completamento automatico.</span><span class="sxs-lookup"><span data-stu-id="8b18f-168">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="8b18f-169">Oggetto JSON radice ha le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b18f-169">The root JSON object has the following properties:</span></span>

<span data-ttu-id="8b18f-170">nome</span><span class="sxs-lookup"><span data-stu-id="8b18f-170">Name</span></span>      | <span data-ttu-id="8b18f-171">Tipo</span><span class="sxs-lookup"><span data-stu-id="8b18f-171">Type</span></span>             | <span data-ttu-id="8b18f-172">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b18f-172">Required</span></span> | <span data-ttu-id="8b18f-173">Note</span><span class="sxs-lookup"><span data-stu-id="8b18f-173">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="8b18f-174">totalHits</span><span class="sxs-lookup"><span data-stu-id="8b18f-174">totalHits</span></span> | <span data-ttu-id="8b18f-175">numero intero</span><span class="sxs-lookup"><span data-stu-id="8b18f-175">integer</span></span>          | <span data-ttu-id="8b18f-176">sì</span><span class="sxs-lookup"><span data-stu-id="8b18f-176">yes</span></span>      | <span data-ttu-id="8b18f-177">Il numero complessivo di corrispondenze, ignorando `skip` e`take`</span><span class="sxs-lookup"><span data-stu-id="8b18f-177">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="8b18f-178">Data</span><span class="sxs-lookup"><span data-stu-id="8b18f-178">data</span></span>      | <span data-ttu-id="8b18f-179">Matrice di stringhe</span><span class="sxs-lookup"><span data-stu-id="8b18f-179">array of strings</span></span> | <span data-ttu-id="8b18f-180">sì</span><span class="sxs-lookup"><span data-stu-id="8b18f-180">yes</span></span>      | <span data-ttu-id="8b18f-181">Il pacchetto corrispondente di ID dalla richiesta</span><span class="sxs-lookup"><span data-stu-id="8b18f-181">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="8b18f-182">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="8b18f-182">Sample request</span></span>

<span data-ttu-id="8b18f-183">OTTENERE https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="8b18f-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="8b18f-184">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="8b18f-184">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="8b18f-185">Enumerare le versioni di pacchetto</span><span class="sxs-lookup"><span data-stu-id="8b18f-185">Enumerate package versions</span></span>

<span data-ttu-id="8b18f-186">Dopo che viene rilevato un ID pacchetto tramite l'API precedente, un client può utilizzare l'API di completamento automatico per enumerare le versioni di pacchetto per un ID di pacchetto fornito.</span><span class="sxs-lookup"><span data-stu-id="8b18f-186">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="8b18f-187">Una versione del pacchetto che è incluso nell'elenco non verrà visualizzato nei risultati.</span><span class="sxs-lookup"><span data-stu-id="8b18f-187">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="8b18f-188">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="8b18f-188">Request parameters</span></span>

<span data-ttu-id="8b18f-189">nome</span><span class="sxs-lookup"><span data-stu-id="8b18f-189">Name</span></span>        | <span data-ttu-id="8b18f-190">In</span><span class="sxs-lookup"><span data-stu-id="8b18f-190">In</span></span>     | <span data-ttu-id="8b18f-191">Tipo</span><span class="sxs-lookup"><span data-stu-id="8b18f-191">Type</span></span>    | <span data-ttu-id="8b18f-192">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b18f-192">Required</span></span> | <span data-ttu-id="8b18f-193">Note</span><span class="sxs-lookup"><span data-stu-id="8b18f-193">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="8b18f-194">ID</span><span class="sxs-lookup"><span data-stu-id="8b18f-194">id</span></span>          | <span data-ttu-id="8b18f-195">URL</span><span class="sxs-lookup"><span data-stu-id="8b18f-195">URL</span></span>    | <span data-ttu-id="8b18f-196">stringa</span><span class="sxs-lookup"><span data-stu-id="8b18f-196">string</span></span>  | <span data-ttu-id="8b18f-197">sì</span><span class="sxs-lookup"><span data-stu-id="8b18f-197">yes</span></span>      | <span data-ttu-id="8b18f-198">Per recuperare le versioni per l'ID del pacchetto</span><span class="sxs-lookup"><span data-stu-id="8b18f-198">The package ID to fetch versions for</span></span>
<span data-ttu-id="8b18f-199">versione provvisoria</span><span class="sxs-lookup"><span data-stu-id="8b18f-199">prerelease</span></span>  | <span data-ttu-id="8b18f-200">URL</span><span class="sxs-lookup"><span data-stu-id="8b18f-200">URL</span></span>    | <span data-ttu-id="8b18f-201">boolean</span><span class="sxs-lookup"><span data-stu-id="8b18f-201">boolean</span></span> | <span data-ttu-id="8b18f-202">No</span><span class="sxs-lookup"><span data-stu-id="8b18f-202">no</span></span>       | <span data-ttu-id="8b18f-203">`true`o `false` stabilire se includere [pacchetti pre-release](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="8b18f-203">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="8b18f-204">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="8b18f-204">semVerLevel</span></span> | <span data-ttu-id="8b18f-205">URL</span><span class="sxs-lookup"><span data-stu-id="8b18f-205">URL</span></span>    | <span data-ttu-id="8b18f-206">stringa</span><span class="sxs-lookup"><span data-stu-id="8b18f-206">string</span></span>  | <span data-ttu-id="8b18f-207">No</span><span class="sxs-lookup"><span data-stu-id="8b18f-207">no</span></span>       | <span data-ttu-id="8b18f-208">Una stringa di versione SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="8b18f-208">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="8b18f-209">Se `prerelease` non viene fornito, vengono esclusi i pacchetti pre-release.</span><span class="sxs-lookup"><span data-stu-id="8b18f-209">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="8b18f-210">Il `semVerLevel` parametro di query viene utilizzato per acconsentire esplicitamente a pacchetti SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="8b18f-210">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="8b18f-211">Se questo parametro di query viene esclusa, verranno restituite solo le versioni SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="8b18f-211">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="8b18f-212">Se `semVerLevel=2.0.0` viene fornito, verranno restituite SemVer 1.0.0 sia versioni SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="8b18f-212">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="8b18f-213">Vedere il [supporto SemVer 2.0.0 per nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="8b18f-213">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="8b18f-214">Risposta</span><span class="sxs-lookup"><span data-stu-id="8b18f-214">Response</span></span>

<span data-ttu-id="8b18f-215">La risposta è il documento JSON che contiene tutte le versioni di pacchetto dell'ID pacchetto fornito, applicando un filtro per i parametri di query specificata.</span><span class="sxs-lookup"><span data-stu-id="8b18f-215">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="8b18f-216">Oggetto JSON radice dispone della proprietà seguente:</span><span class="sxs-lookup"><span data-stu-id="8b18f-216">The root JSON object has the following property:</span></span>

<span data-ttu-id="8b18f-217">nome</span><span class="sxs-lookup"><span data-stu-id="8b18f-217">Name</span></span>      | <span data-ttu-id="8b18f-218">Tipo</span><span class="sxs-lookup"><span data-stu-id="8b18f-218">Type</span></span>             | <span data-ttu-id="8b18f-219">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8b18f-219">Required</span></span> | <span data-ttu-id="8b18f-220">Note</span><span class="sxs-lookup"><span data-stu-id="8b18f-220">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="8b18f-221">Data</span><span class="sxs-lookup"><span data-stu-id="8b18f-221">data</span></span>      | <span data-ttu-id="8b18f-222">Matrice di stringhe</span><span class="sxs-lookup"><span data-stu-id="8b18f-222">array of strings</span></span> | <span data-ttu-id="8b18f-223">sì</span><span class="sxs-lookup"><span data-stu-id="8b18f-223">yes</span></span>      | <span data-ttu-id="8b18f-224">Le versioni del pacchetto corrispondente alla richiesta</span><span class="sxs-lookup"><span data-stu-id="8b18f-224">The package versions matched by the request</span></span>

<span data-ttu-id="8b18f-225">Le versioni del pacchetto nel `data` matrice può contenere i metadati di compilazione SemVer 2.0.0 (ad esempio `1.0.0+metadata`) se il `semVerLevel=2.0.0` è stato specificato nella stringa di query.</span><span class="sxs-lookup"><span data-stu-id="8b18f-225">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="8b18f-226">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="8b18f-226">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="8b18f-227">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="8b18f-227">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
