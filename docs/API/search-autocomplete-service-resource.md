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
ms.assetid: ead5cf7a-e51e-4cbb-8798-58226f4c853f
description: Il servizio di completamento automatico di ricerca supporta le versioni e rilevamento interattivo di ID di pacchetto.
keywords: API di completamento automatico NuGet, ID del pacchetto NuGet ricerca, ID di pacchetto sottostringa
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 313ceb630947b46c34b98e14044ecf121b725087
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="autocomplete"></a><span data-ttu-id="cc8a6-104">Completamento automatico</span><span class="sxs-lookup"><span data-stu-id="cc8a6-104">Autocomplete</span></span>

<span data-ttu-id="cc8a6-105">È possibile creare un pacchetto ID e la versione autocomplete esperienza tramite l'API V3.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-105">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="cc8a6-106">La risorsa utilizzata per l'esecuzione di query di completamento automatico è il `SearchAutocompleteService` risorsa trovata nel [indice servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="cc8a6-106">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="cc8a6-107">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="cc8a6-107">Versioning</span></span>

<span data-ttu-id="cc8a6-108">Nell'esempio `@type` vengono utilizzati i valori:</span><span class="sxs-lookup"><span data-stu-id="cc8a6-108">The following `@type` values are used:</span></span>

<span data-ttu-id="cc8a6-109">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="cc8a6-109">@type value</span></span>                          | <span data-ttu-id="cc8a6-110">Note</span><span class="sxs-lookup"><span data-stu-id="cc8a6-110">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="cc8a6-111">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="cc8a6-111">SearchAutocompleteService</span></span>            | <span data-ttu-id="cc8a6-112">La versione iniziale</span><span class="sxs-lookup"><span data-stu-id="cc8a6-112">The initial release</span></span>
<span data-ttu-id="cc8a6-113">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="cc8a6-113">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="cc8a6-114">Alias di`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="cc8a6-114">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="cc8a6-115">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="cc8a6-115">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="cc8a6-116">Alias di`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="cc8a6-116">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="cc8a6-117">URL di base</span><span class="sxs-lookup"><span data-stu-id="cc8a6-117">Base URL</span></span>

<span data-ttu-id="cc8a6-118">L'URL di base per le API seguente è il valore di `@id` proprietà associati a uno della risorsa menzionati in precedenza `@type` valori.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-118">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="cc8a6-119">Nel documento seguente, il segnaposto URL di base `{@id}` verrà utilizzato.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="cc8a6-120">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="cc8a6-120">HTTP Methods</span></span>

<span data-ttu-id="cc8a6-121">Tutti gli URL trovati, il supporto di risorsa di registrazione, i metodi HTTP `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="cc8a6-122">Ricerca per ID pacchetto</span><span class="sxs-lookup"><span data-stu-id="cc8a6-122">Search for package IDs</span></span>

<span data-ttu-id="cc8a6-123">Il primo completamento automatico API supporta la ricerca di parte di una stringa di ID di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-123">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="cc8a6-124">Questo è molto utile quando si desidera fornire una funzionalità typeahead pacchetto in un'interfaccia utente integrata con un'origine del pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-124">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="cc8a6-125">Un pacchetto con le versioni non in elenco non verrà visualizzati nei risultati.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-125">A package with only unlisted versions will not appear in the results.</span></span>

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="cc8a6-126">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="cc8a6-126">Request parameters</span></span>

<span data-ttu-id="cc8a6-127">Nome</span><span class="sxs-lookup"><span data-stu-id="cc8a6-127">Name</span></span>        | <span data-ttu-id="cc8a6-128">In</span><span class="sxs-lookup"><span data-stu-id="cc8a6-128">In</span></span>     | <span data-ttu-id="cc8a6-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="cc8a6-129">Type</span></span>    | <span data-ttu-id="cc8a6-130">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="cc8a6-130">Required</span></span> | <span data-ttu-id="cc8a6-131">Note</span><span class="sxs-lookup"><span data-stu-id="cc8a6-131">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="cc8a6-132">q</span><span class="sxs-lookup"><span data-stu-id="cc8a6-132">q</span></span>           | <span data-ttu-id="cc8a6-133">URL</span><span class="sxs-lookup"><span data-stu-id="cc8a6-133">URL</span></span>    | <span data-ttu-id="cc8a6-134">string</span><span class="sxs-lookup"><span data-stu-id="cc8a6-134">string</span></span>  | <span data-ttu-id="cc8a6-135">No</span><span class="sxs-lookup"><span data-stu-id="cc8a6-135">no</span></span>       | <span data-ttu-id="cc8a6-136">La stringa da confrontare con l'ID di pacchetto</span><span class="sxs-lookup"><span data-stu-id="cc8a6-136">The string to compare against package IDs</span></span>
<span data-ttu-id="cc8a6-137">skip</span><span class="sxs-lookup"><span data-stu-id="cc8a6-137">skip</span></span>        | <span data-ttu-id="cc8a6-138">URL</span><span class="sxs-lookup"><span data-stu-id="cc8a6-138">URL</span></span>    | <span data-ttu-id="cc8a6-139">numero intero</span><span class="sxs-lookup"><span data-stu-id="cc8a6-139">integer</span></span> | <span data-ttu-id="cc8a6-140">No</span><span class="sxs-lookup"><span data-stu-id="cc8a6-140">no</span></span>       | <span data-ttu-id="cc8a6-141">Il numero di risultati da ignorare per l'impaginazione</span><span class="sxs-lookup"><span data-stu-id="cc8a6-141">The number of results to skip, for pagination</span></span>
<span data-ttu-id="cc8a6-142">Take</span><span class="sxs-lookup"><span data-stu-id="cc8a6-142">take</span></span>        | <span data-ttu-id="cc8a6-143">URL</span><span class="sxs-lookup"><span data-stu-id="cc8a6-143">URL</span></span>    | <span data-ttu-id="cc8a6-144">numero intero</span><span class="sxs-lookup"><span data-stu-id="cc8a6-144">integer</span></span> | <span data-ttu-id="cc8a6-145">No</span><span class="sxs-lookup"><span data-stu-id="cc8a6-145">no</span></span>       | <span data-ttu-id="cc8a6-146">Il numero di risultati da restituire, per la paginazione</span><span class="sxs-lookup"><span data-stu-id="cc8a6-146">The number of results to return, for pagination</span></span>
<span data-ttu-id="cc8a6-147">versione provvisoria</span><span class="sxs-lookup"><span data-stu-id="cc8a6-147">prerelease</span></span>  | <span data-ttu-id="cc8a6-148">URL</span><span class="sxs-lookup"><span data-stu-id="cc8a6-148">URL</span></span>    | <span data-ttu-id="cc8a6-149">boolean</span><span class="sxs-lookup"><span data-stu-id="cc8a6-149">boolean</span></span> | <span data-ttu-id="cc8a6-150">No</span><span class="sxs-lookup"><span data-stu-id="cc8a6-150">no</span></span>       | <span data-ttu-id="cc8a6-151">`true`o `false` stabilire se includere [pacchetti pre-release](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="cc8a6-151">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="cc8a6-152">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="cc8a6-152">semVerLevel</span></span> | <span data-ttu-id="cc8a6-153">URL</span><span class="sxs-lookup"><span data-stu-id="cc8a6-153">URL</span></span>    | <span data-ttu-id="cc8a6-154">string</span><span class="sxs-lookup"><span data-stu-id="cc8a6-154">string</span></span>  | <span data-ttu-id="cc8a6-155">No</span><span class="sxs-lookup"><span data-stu-id="cc8a6-155">no</span></span>       | <span data-ttu-id="cc8a6-156">Una stringa di versione SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="cc8a6-156">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="cc8a6-157">La query con completamento automatico `q` viene analizzato in modo che è definito dall'implementazione del server.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-157">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="cc8a6-158">NuGet.org supporta l'esecuzione di query per il prefisso di token ID di pacchetto, che sono pezzi dell'ID prodotto da [PROD143] e originale da caratteri iniziali di case e simboli.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-158">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="cc8a6-159">Il `skip` valori predefiniti dei parametri su 0.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-159">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="cc8a6-160">Il `take` parametro deve essere un numero intero maggiore di zero.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-160">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="cc8a6-161">L'implementazione del server potrebbe avere un valore massimo.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-161">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="cc8a6-162">Se `prerelease` non viene fornito, vengono esclusi i pacchetti pre-release.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-162">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="cc8a6-163">Il `semVerLevel` parametro di query viene utilizzato per acconsentire esplicitamente a [SemVer 2.0.0 pacchetti](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="cc8a6-163">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="cc8a6-164">Se questo parametro di query viene esclusa, verranno restituiti solo gli ID di pacchetto con le versioni compatibili SemVer 1.0.0 (con il [standard controllo delle versioni NuGet](../reference/package-versioning.md) avvertenze, ad esempio le stringhe di versione con 4 elementi di tipo integer).</span><span class="sxs-lookup"><span data-stu-id="cc8a6-164">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="cc8a6-165">Se `semVerLevel=2.0.0` viene fornito, verranno restituiti SemVer 1.0.0 sia pacchetti compatibili SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-165">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="cc8a6-166">Vedere il [supporto SemVer 2.0.0 per nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-166">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="cc8a6-167">Risposta</span><span class="sxs-lookup"><span data-stu-id="cc8a6-167">Response</span></span>

<span data-ttu-id="cc8a6-168">La risposta è il documento JSON che contiene fino a `take` risultati di completamento automatico.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-168">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="cc8a6-169">Oggetto JSON radice ha le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc8a6-169">The root JSON object has the following properties:</span></span>

<span data-ttu-id="cc8a6-170">Nome</span><span class="sxs-lookup"><span data-stu-id="cc8a6-170">Name</span></span>      | <span data-ttu-id="cc8a6-171">Tipo</span><span class="sxs-lookup"><span data-stu-id="cc8a6-171">Type</span></span>             | <span data-ttu-id="cc8a6-172">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="cc8a6-172">Required</span></span> | <span data-ttu-id="cc8a6-173">Note</span><span class="sxs-lookup"><span data-stu-id="cc8a6-173">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="cc8a6-174">totalHits</span><span class="sxs-lookup"><span data-stu-id="cc8a6-174">totalHits</span></span> | <span data-ttu-id="cc8a6-175">numero intero</span><span class="sxs-lookup"><span data-stu-id="cc8a6-175">integer</span></span>          | <span data-ttu-id="cc8a6-176">sì</span><span class="sxs-lookup"><span data-stu-id="cc8a6-176">yes</span></span>      | <span data-ttu-id="cc8a6-177">Il numero complessivo di corrispondenze, ignorando `skip` e`take`</span><span class="sxs-lookup"><span data-stu-id="cc8a6-177">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="cc8a6-178">Data</span><span class="sxs-lookup"><span data-stu-id="cc8a6-178">data</span></span>      | <span data-ttu-id="cc8a6-179">Matrice di stringhe</span><span class="sxs-lookup"><span data-stu-id="cc8a6-179">array of strings</span></span> | <span data-ttu-id="cc8a6-180">sì</span><span class="sxs-lookup"><span data-stu-id="cc8a6-180">yes</span></span>      | <span data-ttu-id="cc8a6-181">Il pacchetto corrispondente di ID dalla richiesta</span><span class="sxs-lookup"><span data-stu-id="cc8a6-181">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="cc8a6-182">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="cc8a6-182">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="cc8a6-183">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="cc8a6-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="cc8a6-184">Enumerare le versioni di pacchetto</span><span class="sxs-lookup"><span data-stu-id="cc8a6-184">Enumerate package versions</span></span>

<span data-ttu-id="cc8a6-185">Dopo che viene rilevato un ID pacchetto tramite l'API precedente, un client può utilizzare l'API di completamento automatico per enumerare le versioni di pacchetto per un ID di pacchetto fornito.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="cc8a6-186">Una versione del pacchetto che è incluso nell'elenco non verrà visualizzato nei risultati.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-186">A package version that is unlisted will not appear in the results.</span></span>

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="cc8a6-187">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="cc8a6-187">Request parameters</span></span>

<span data-ttu-id="cc8a6-188">Nome</span><span class="sxs-lookup"><span data-stu-id="cc8a6-188">Name</span></span>        | <span data-ttu-id="cc8a6-189">In</span><span class="sxs-lookup"><span data-stu-id="cc8a6-189">In</span></span>     | <span data-ttu-id="cc8a6-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="cc8a6-190">Type</span></span>    | <span data-ttu-id="cc8a6-191">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="cc8a6-191">Required</span></span> | <span data-ttu-id="cc8a6-192">Note</span><span class="sxs-lookup"><span data-stu-id="cc8a6-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="cc8a6-193">ID</span><span class="sxs-lookup"><span data-stu-id="cc8a6-193">id</span></span>          | <span data-ttu-id="cc8a6-194">URL</span><span class="sxs-lookup"><span data-stu-id="cc8a6-194">URL</span></span>    | <span data-ttu-id="cc8a6-195">string</span><span class="sxs-lookup"><span data-stu-id="cc8a6-195">string</span></span>  | <span data-ttu-id="cc8a6-196">sì</span><span class="sxs-lookup"><span data-stu-id="cc8a6-196">yes</span></span>      | <span data-ttu-id="cc8a6-197">Per recuperare le versioni per l'ID del pacchetto</span><span class="sxs-lookup"><span data-stu-id="cc8a6-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="cc8a6-198">versione provvisoria</span><span class="sxs-lookup"><span data-stu-id="cc8a6-198">prerelease</span></span>  | <span data-ttu-id="cc8a6-199">URL</span><span class="sxs-lookup"><span data-stu-id="cc8a6-199">URL</span></span>    | <span data-ttu-id="cc8a6-200">boolean</span><span class="sxs-lookup"><span data-stu-id="cc8a6-200">boolean</span></span> | <span data-ttu-id="cc8a6-201">No</span><span class="sxs-lookup"><span data-stu-id="cc8a6-201">no</span></span>       | <span data-ttu-id="cc8a6-202">`true`o `false` stabilire se includere [pacchetti pre-release](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="cc8a6-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="cc8a6-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="cc8a6-203">semVerLevel</span></span> | <span data-ttu-id="cc8a6-204">URL</span><span class="sxs-lookup"><span data-stu-id="cc8a6-204">URL</span></span>    | <span data-ttu-id="cc8a6-205">string</span><span class="sxs-lookup"><span data-stu-id="cc8a6-205">string</span></span>  | <span data-ttu-id="cc8a6-206">No</span><span class="sxs-lookup"><span data-stu-id="cc8a6-206">no</span></span>       | <span data-ttu-id="cc8a6-207">Una stringa di versione SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="cc8a6-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="cc8a6-208">Se `prerelease` non viene fornito, vengono esclusi i pacchetti pre-release.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="cc8a6-209">Il `semVerLevel` parametro di query viene utilizzato per acconsentire esplicitamente a pacchetti SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="cc8a6-210">Se questo parametro di query viene esclusa, verranno restituite solo le versioni SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="cc8a6-211">Se `semVerLevel=2.0.0` viene fornito, verranno restituite SemVer 1.0.0 sia versioni SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="cc8a6-212">Vedere il [supporto SemVer 2.0.0 per nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="cc8a6-213">Risposta</span><span class="sxs-lookup"><span data-stu-id="cc8a6-213">Response</span></span>

<span data-ttu-id="cc8a6-214">La risposta è il documento JSON che contiene tutte le versioni di pacchetto dell'ID pacchetto fornito, applicando un filtro per i parametri di query specificata.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="cc8a6-215">Oggetto JSON radice dispone della proprietà seguente:</span><span class="sxs-lookup"><span data-stu-id="cc8a6-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="cc8a6-216">Nome</span><span class="sxs-lookup"><span data-stu-id="cc8a6-216">Name</span></span>      | <span data-ttu-id="cc8a6-217">Tipo</span><span class="sxs-lookup"><span data-stu-id="cc8a6-217">Type</span></span>             | <span data-ttu-id="cc8a6-218">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="cc8a6-218">Required</span></span> | <span data-ttu-id="cc8a6-219">Note</span><span class="sxs-lookup"><span data-stu-id="cc8a6-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="cc8a6-220">Data</span><span class="sxs-lookup"><span data-stu-id="cc8a6-220">data</span></span>      | <span data-ttu-id="cc8a6-221">Matrice di stringhe</span><span class="sxs-lookup"><span data-stu-id="cc8a6-221">array of strings</span></span> | <span data-ttu-id="cc8a6-222">sì</span><span class="sxs-lookup"><span data-stu-id="cc8a6-222">yes</span></span>      | <span data-ttu-id="cc8a6-223">Le versioni del pacchetto corrispondente alla richiesta</span><span class="sxs-lookup"><span data-stu-id="cc8a6-223">The package versions matched by the request</span></span>

<span data-ttu-id="cc8a6-224">Le versioni del pacchetto nel `data` matrice può contenere i metadati di compilazione SemVer 2.0.0 (ad esempio `1.0.0+metadata`) se il `semVerLevel=2.0.0` è stato specificato nella stringa di query.</span><span class="sxs-lookup"><span data-stu-id="cc8a6-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="cc8a6-225">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="cc8a6-225">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="cc8a6-226">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="cc8a6-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
