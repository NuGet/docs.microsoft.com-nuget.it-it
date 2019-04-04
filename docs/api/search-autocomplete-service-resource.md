---
title: Completamento automatico, API NuGet
description: Il servizio di ricerca autocomplete supporta le versioni e individuazione interattiva di ID di pacchetto.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fdc3ad8aa239a42d8a4c169a757715e856bdcb41
ms.sourcegitcommit: 9f94e00428d83aef4a7a87db679129eff7720c59
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/03/2019
ms.locfileid: "58911049"
---
# <a name="autocomplete"></a><span data-ttu-id="7823a-103">Completamento automatico</span><span class="sxs-lookup"><span data-stu-id="7823a-103">Autocomplete</span></span>

<span data-ttu-id="7823a-104">È possibile creare un pacchetto ID e la versione autocomplete esperienza tramite l'API di V3.</span><span class="sxs-lookup"><span data-stu-id="7823a-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="7823a-105">La risorsa utilizzata per l'esecuzione di query di completamento automatico è il `SearchAutocompleteService` trovare la risorsa nella [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="7823a-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="7823a-106">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="7823a-106">Versioning</span></span>

<span data-ttu-id="7823a-107">Nell'esempio `@type` vengono utilizzati i valori:</span><span class="sxs-lookup"><span data-stu-id="7823a-107">The following `@type` values are used:</span></span>

<span data-ttu-id="7823a-108">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="7823a-108">@type value</span></span>                          | <span data-ttu-id="7823a-109">Note</span><span class="sxs-lookup"><span data-stu-id="7823a-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="7823a-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="7823a-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="7823a-111">La versione iniziale</span><span class="sxs-lookup"><span data-stu-id="7823a-111">The initial release</span></span>
<span data-ttu-id="7823a-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="7823a-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="7823a-113">Alias di</span><span class="sxs-lookup"><span data-stu-id="7823a-113">Alias of</span></span> `SearchAutocompleteService`
<span data-ttu-id="7823a-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="7823a-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="7823a-115">Alias di</span><span class="sxs-lookup"><span data-stu-id="7823a-115">Alias of</span></span> `SearchAutocompleteService`

## <a name="base-url"></a><span data-ttu-id="7823a-116">URL di base</span><span class="sxs-lookup"><span data-stu-id="7823a-116">Base URL</span></span>

<span data-ttu-id="7823a-117">L'URL di base per le API seguente è il valore della `@id` proprietà associati a uno della risorsa menzionati in precedenza `@type` valori.</span><span class="sxs-lookup"><span data-stu-id="7823a-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="7823a-118">Nel documento seguente, il segnaposto URL di base `{@id}` verrà utilizzato.</span><span class="sxs-lookup"><span data-stu-id="7823a-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="7823a-119">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="7823a-119">HTTP Methods</span></span>

<span data-ttu-id="7823a-120">Tutti gli URL disponibili il supporto di risorse di registrazione i metodi HTTP `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="7823a-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="7823a-121">Ricerca per ID pacchetto</span><span class="sxs-lookup"><span data-stu-id="7823a-121">Search for package IDs</span></span>

<span data-ttu-id="7823a-122">L'API di completamento automatico prima supporta la ricerca di parte di una stringa di ID di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="7823a-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="7823a-123">Ciò è ideale quando si desidera fornire una funzionalità di completamento automatico del pacchetto in un'interfaccia utente integrata con un'origine del pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="7823a-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="7823a-124">Un pacchetto con solo le versioni non in elenco non verrà visualizzato nei risultati.</span><span class="sxs-lookup"><span data-stu-id="7823a-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="7823a-125">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="7823a-125">Request parameters</span></span>

<span data-ttu-id="7823a-126">Nome</span><span class="sxs-lookup"><span data-stu-id="7823a-126">Name</span></span>        | <span data-ttu-id="7823a-127">In</span><span class="sxs-lookup"><span data-stu-id="7823a-127">In</span></span>     | <span data-ttu-id="7823a-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="7823a-128">Type</span></span>    | <span data-ttu-id="7823a-129">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="7823a-129">Required</span></span> | <span data-ttu-id="7823a-130">Note</span><span class="sxs-lookup"><span data-stu-id="7823a-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="7823a-131">q</span><span class="sxs-lookup"><span data-stu-id="7823a-131">q</span></span>           | <span data-ttu-id="7823a-132">URL</span><span class="sxs-lookup"><span data-stu-id="7823a-132">URL</span></span>    | <span data-ttu-id="7823a-133">string</span><span class="sxs-lookup"><span data-stu-id="7823a-133">string</span></span>  | <span data-ttu-id="7823a-134">No</span><span class="sxs-lookup"><span data-stu-id="7823a-134">no</span></span>       | <span data-ttu-id="7823a-135">La stringa da confrontare con gli ID pacchetto</span><span class="sxs-lookup"><span data-stu-id="7823a-135">The string to compare against package IDs</span></span>
<span data-ttu-id="7823a-136">skip</span><span class="sxs-lookup"><span data-stu-id="7823a-136">skip</span></span>        | <span data-ttu-id="7823a-137">URL</span><span class="sxs-lookup"><span data-stu-id="7823a-137">URL</span></span>    | <span data-ttu-id="7823a-138">numero intero</span><span class="sxs-lookup"><span data-stu-id="7823a-138">integer</span></span> | <span data-ttu-id="7823a-139">No</span><span class="sxs-lookup"><span data-stu-id="7823a-139">no</span></span>       | <span data-ttu-id="7823a-140">Il numero di risultati da ignorare, per la paginazione</span><span class="sxs-lookup"><span data-stu-id="7823a-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="7823a-141">Take</span><span class="sxs-lookup"><span data-stu-id="7823a-141">take</span></span>        | <span data-ttu-id="7823a-142">URL</span><span class="sxs-lookup"><span data-stu-id="7823a-142">URL</span></span>    | <span data-ttu-id="7823a-143">numero intero</span><span class="sxs-lookup"><span data-stu-id="7823a-143">integer</span></span> | <span data-ttu-id="7823a-144">No</span><span class="sxs-lookup"><span data-stu-id="7823a-144">no</span></span>       | <span data-ttu-id="7823a-145">Il numero di risultati da restituire, per la paginazione</span><span class="sxs-lookup"><span data-stu-id="7823a-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="7823a-146">versione preliminare</span><span class="sxs-lookup"><span data-stu-id="7823a-146">prerelease</span></span>  | <span data-ttu-id="7823a-147">URL</span><span class="sxs-lookup"><span data-stu-id="7823a-147">URL</span></span>    | <span data-ttu-id="7823a-148">boolean</span><span class="sxs-lookup"><span data-stu-id="7823a-148">boolean</span></span> | <span data-ttu-id="7823a-149">No</span><span class="sxs-lookup"><span data-stu-id="7823a-149">no</span></span>       | `true` <span data-ttu-id="7823a-150">oppure `false` che determina se includere [i pacchetti di versioni non definitive](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="7823a-150">or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="7823a-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="7823a-151">semVerLevel</span></span> | <span data-ttu-id="7823a-152">URL</span><span class="sxs-lookup"><span data-stu-id="7823a-152">URL</span></span>    | <span data-ttu-id="7823a-153">string</span><span class="sxs-lookup"><span data-stu-id="7823a-153">string</span></span>  | <span data-ttu-id="7823a-154">No</span><span class="sxs-lookup"><span data-stu-id="7823a-154">no</span></span>       | <span data-ttu-id="7823a-155">Una stringa di versione SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="7823a-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="7823a-156">La query di completamento automatico `q` viene analizzato in modo che è definito dall'implementazione del server.</span><span class="sxs-lookup"><span data-stu-id="7823a-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="7823a-157">NuGet.org supporta l'esecuzione di query per il prefisso del token ID pacchetto, che sono pezzi dell'ID di prodotti dalla suddivisione originale da caratteri le iniziali maiuscole e simboli.</span><span class="sxs-lookup"><span data-stu-id="7823a-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="7823a-158">Il `skip` valori predefiniti dei parametri su 0.</span><span class="sxs-lookup"><span data-stu-id="7823a-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="7823a-159">Il `take` parametro deve essere un numero intero maggiore di zero.</span><span class="sxs-lookup"><span data-stu-id="7823a-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="7823a-160">L'implementazione del server può imporre un valore massimo.</span><span class="sxs-lookup"><span data-stu-id="7823a-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="7823a-161">Se `prerelease` non viene specificato, vengono esclusi i pacchetti in versione non definitiva.</span><span class="sxs-lookup"><span data-stu-id="7823a-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="7823a-162">Il `semVerLevel` parametro di query viene utilizzato per acconsentire [pacchetti di SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="7823a-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="7823a-163">Se questo parametro di query è stata esclusa, verranno restituiti solo gli ID di pacchetto con le versioni compatibili di SemVer 1.0.0 (con il [controllo delle versioni NuGet standard](../reference/package-versioning.md) avvertenze, ad esempio le stringhe di versione con 4 elementi integer).</span><span class="sxs-lookup"><span data-stu-id="7823a-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="7823a-164">Se `semVerLevel=2.0.0` viene fornito, verranno restituiti SemVer 1.0.0 sia pacchetti compatibili di SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="7823a-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="7823a-165">Vedere le [supporto di SemVer 2.0.0 per nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="7823a-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="7823a-166">Risposta</span><span class="sxs-lookup"><span data-stu-id="7823a-166">Response</span></span>

<span data-ttu-id="7823a-167">La risposta è il documento JSON che contiene fino a `take` i risultati di completamento automatico.</span><span class="sxs-lookup"><span data-stu-id="7823a-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="7823a-168">L'oggetto JSON radice ha le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="7823a-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="7823a-169">Nome</span><span class="sxs-lookup"><span data-stu-id="7823a-169">Name</span></span>      | <span data-ttu-id="7823a-170">Tipo</span><span class="sxs-lookup"><span data-stu-id="7823a-170">Type</span></span>             | <span data-ttu-id="7823a-171">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="7823a-171">Required</span></span> | <span data-ttu-id="7823a-172">Note</span><span class="sxs-lookup"><span data-stu-id="7823a-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="7823a-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="7823a-173">totalHits</span></span> | <span data-ttu-id="7823a-174">numero intero</span><span class="sxs-lookup"><span data-stu-id="7823a-174">integer</span></span>          | <span data-ttu-id="7823a-175">sì</span><span class="sxs-lookup"><span data-stu-id="7823a-175">yes</span></span>      | <span data-ttu-id="7823a-176">Il numero complessivo di corrispondenze, ignorando `skip` e</span><span class="sxs-lookup"><span data-stu-id="7823a-176">The total number of matches, disregarding `skip` and</span></span> `take`
<span data-ttu-id="7823a-177">Data</span><span class="sxs-lookup"><span data-stu-id="7823a-177">data</span></span>      | <span data-ttu-id="7823a-178">Matrice di stringhe</span><span class="sxs-lookup"><span data-stu-id="7823a-178">array of strings</span></span> | <span data-ttu-id="7823a-179">sì</span><span class="sxs-lookup"><span data-stu-id="7823a-179">yes</span></span>      | <span data-ttu-id="7823a-180">Il pacchetto ID trovare una corrispondenza con la richiesta</span><span class="sxs-lookup"><span data-stu-id="7823a-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="7823a-181">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="7823a-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="7823a-182">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="7823a-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="7823a-183">Enumera le versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="7823a-183">Enumerate package versions</span></span>

<span data-ttu-id="7823a-184">Dopo che viene rilevato un ID di pacchetto tramite l'API precedente, un client può usare l'API di completamento automatico per enumerare le versioni dei pacchetti per un ID pacchetto specificato.</span><span class="sxs-lookup"><span data-stu-id="7823a-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="7823a-185">Una versione del pacchetto che è incluso nell'elenco non verrà visualizzato nei risultati.</span><span class="sxs-lookup"><span data-stu-id="7823a-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="7823a-186">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="7823a-186">Request parameters</span></span>

<span data-ttu-id="7823a-187">Nome</span><span class="sxs-lookup"><span data-stu-id="7823a-187">Name</span></span>        | <span data-ttu-id="7823a-188">In</span><span class="sxs-lookup"><span data-stu-id="7823a-188">In</span></span>     | <span data-ttu-id="7823a-189">Tipo</span><span class="sxs-lookup"><span data-stu-id="7823a-189">Type</span></span>    | <span data-ttu-id="7823a-190">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="7823a-190">Required</span></span> | <span data-ttu-id="7823a-191">Note</span><span class="sxs-lookup"><span data-stu-id="7823a-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="7823a-192">ID</span><span class="sxs-lookup"><span data-stu-id="7823a-192">id</span></span>          | <span data-ttu-id="7823a-193">URL</span><span class="sxs-lookup"><span data-stu-id="7823a-193">URL</span></span>    | <span data-ttu-id="7823a-194">string</span><span class="sxs-lookup"><span data-stu-id="7823a-194">string</span></span>  | <span data-ttu-id="7823a-195">sì</span><span class="sxs-lookup"><span data-stu-id="7823a-195">yes</span></span>      | <span data-ttu-id="7823a-196">Per recuperare le versioni per l'ID del pacchetto</span><span class="sxs-lookup"><span data-stu-id="7823a-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="7823a-197">versione preliminare</span><span class="sxs-lookup"><span data-stu-id="7823a-197">prerelease</span></span>  | <span data-ttu-id="7823a-198">URL</span><span class="sxs-lookup"><span data-stu-id="7823a-198">URL</span></span>    | <span data-ttu-id="7823a-199">boolean</span><span class="sxs-lookup"><span data-stu-id="7823a-199">boolean</span></span> | <span data-ttu-id="7823a-200">No</span><span class="sxs-lookup"><span data-stu-id="7823a-200">no</span></span>       | `true` <span data-ttu-id="7823a-201">oppure `false` che determina se includere [i pacchetti di versioni non definitive](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="7823a-201">or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="7823a-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="7823a-202">semVerLevel</span></span> | <span data-ttu-id="7823a-203">URL</span><span class="sxs-lookup"><span data-stu-id="7823a-203">URL</span></span>    | <span data-ttu-id="7823a-204">string</span><span class="sxs-lookup"><span data-stu-id="7823a-204">string</span></span>  | <span data-ttu-id="7823a-205">No</span><span class="sxs-lookup"><span data-stu-id="7823a-205">no</span></span>       | <span data-ttu-id="7823a-206">Una stringa di versione di SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="7823a-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="7823a-207">Se `prerelease` non viene specificato, vengono esclusi i pacchetti in versione non definitiva.</span><span class="sxs-lookup"><span data-stu-id="7823a-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="7823a-208">Il `semVerLevel` parametro di query viene utilizzato per acconsentire esplicitamente a pacchetti di SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="7823a-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="7823a-209">Se questo parametro di query è stata esclusa, verranno restituite solo le versioni di SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="7823a-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="7823a-210">Se `semVerLevel=2.0.0` è specificato, verranno restituite sia SemVer 1.0.0 e le versioni di SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="7823a-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="7823a-211">Vedere le [supporto di SemVer 2.0.0 per nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="7823a-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="7823a-212">Risposta</span><span class="sxs-lookup"><span data-stu-id="7823a-212">Response</span></span>

<span data-ttu-id="7823a-213">La risposta è il documento JSON contenente tutte le versioni del pacchetto dell'ID pacchetto fornito, il filtro per i parametri di query specificata.</span><span class="sxs-lookup"><span data-stu-id="7823a-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="7823a-214">L'oggetto JSON radice ha la proprietà seguente:</span><span class="sxs-lookup"><span data-stu-id="7823a-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="7823a-215">Nome</span><span class="sxs-lookup"><span data-stu-id="7823a-215">Name</span></span>      | <span data-ttu-id="7823a-216">Tipo</span><span class="sxs-lookup"><span data-stu-id="7823a-216">Type</span></span>             | <span data-ttu-id="7823a-217">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="7823a-217">Required</span></span> | <span data-ttu-id="7823a-218">Note</span><span class="sxs-lookup"><span data-stu-id="7823a-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="7823a-219">Data</span><span class="sxs-lookup"><span data-stu-id="7823a-219">data</span></span>      | <span data-ttu-id="7823a-220">Matrice di stringhe</span><span class="sxs-lookup"><span data-stu-id="7823a-220">array of strings</span></span> | <span data-ttu-id="7823a-221">sì</span><span class="sxs-lookup"><span data-stu-id="7823a-221">yes</span></span>      | <span data-ttu-id="7823a-222">Le versioni del pacchetto corrispondente alla richiesta</span><span class="sxs-lookup"><span data-stu-id="7823a-222">The package versions matched by the request</span></span>

<span data-ttu-id="7823a-223">Le versioni dei pacchetti nel `data` matrice può contenere i metadati di SemVer 2.0.0 compilazione (ad esempio `1.0.0+metadata`) se il `semVerLevel=2.0.0` viene fornito nella stringa di query.</span><span class="sxs-lookup"><span data-stu-id="7823a-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="7823a-224">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="7823a-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="7823a-225">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="7823a-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
