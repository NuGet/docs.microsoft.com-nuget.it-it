---
title: Completamento automatico, API NuGet
description: Il servizio di completamento automatico di ricerca supporta l'individuazione interattiva di ID e versioni del pacchetto.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488300"
---
# <a name="autocomplete"></a><span data-ttu-id="d800d-103">Completamento automatico</span><span class="sxs-lookup"><span data-stu-id="d800d-103">Autocomplete</span></span>

<span data-ttu-id="d800d-104">È possibile creare un ID pacchetto e un'esperienza di completamento automatico della versione usando l'API V3.</span><span class="sxs-lookup"><span data-stu-id="d800d-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="d800d-105">La risorsa utilizzata per eseguire query di completamento automatico è `SearchAutocompleteService` la risorsa presente nell' [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="d800d-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="d800d-106">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="d800d-106">Versioning</span></span>

<span data-ttu-id="d800d-107">Vengono usati `@type` i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="d800d-107">The following `@type` values are used:</span></span>

<span data-ttu-id="d800d-108">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="d800d-108">@type value</span></span>                          | <span data-ttu-id="d800d-109">Note</span><span class="sxs-lookup"><span data-stu-id="d800d-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="d800d-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="d800d-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="d800d-111">Versione iniziale</span><span class="sxs-lookup"><span data-stu-id="d800d-111">The initial release</span></span>
<span data-ttu-id="d800d-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="d800d-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="d800d-113">Alias di`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="d800d-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="d800d-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="d800d-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="d800d-115">Alias di`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="d800d-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="d800d-116">URL di base</span><span class="sxs-lookup"><span data-stu-id="d800d-116">Base URL</span></span>

<span data-ttu-id="d800d-117">L'URL di base per le API seguenti è il valore della `@id` proprietà associata a uno dei valori di risorsa `@type` menzionati sopra.</span><span class="sxs-lookup"><span data-stu-id="d800d-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="d800d-118">Nel documento seguente verrà usato l'URL `{@id}` di base segnaposto.</span><span class="sxs-lookup"><span data-stu-id="d800d-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d800d-119">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="d800d-119">HTTP Methods</span></span>

<span data-ttu-id="d800d-120">Tutti gli URL trovati nella risorsa di registrazione supportano i metodi `GET` http `HEAD`e.</span><span class="sxs-lookup"><span data-stu-id="d800d-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="d800d-121">Ricerca di ID pacchetto</span><span class="sxs-lookup"><span data-stu-id="d800d-121">Search for package IDs</span></span>

<span data-ttu-id="d800d-122">La prima API di completamento automatico supporta la ricerca di una parte di una stringa ID pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d800d-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="d800d-123">Questo è molto utile quando si vuole fornire una funzionalità di typeahead del pacchetto in un'interfaccia utente integrata con un'origine del pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="d800d-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="d800d-124">Un pacchetto solo con versioni non in elenco non verrà visualizzato nei risultati.</span><span class="sxs-lookup"><span data-stu-id="d800d-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="d800d-125">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="d800d-125">Request parameters</span></span>

<span data-ttu-id="d800d-126">Name</span><span class="sxs-lookup"><span data-stu-id="d800d-126">Name</span></span>        | <span data-ttu-id="d800d-127">In</span><span class="sxs-lookup"><span data-stu-id="d800d-127">In</span></span>     | <span data-ttu-id="d800d-128">Type</span><span class="sxs-lookup"><span data-stu-id="d800d-128">Type</span></span>    | <span data-ttu-id="d800d-129">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="d800d-129">Required</span></span> | <span data-ttu-id="d800d-130">Note</span><span class="sxs-lookup"><span data-stu-id="d800d-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="d800d-131">q</span><span class="sxs-lookup"><span data-stu-id="d800d-131">q</span></span>           | <span data-ttu-id="d800d-132">URL</span><span class="sxs-lookup"><span data-stu-id="d800d-132">URL</span></span>    | <span data-ttu-id="d800d-133">string</span><span class="sxs-lookup"><span data-stu-id="d800d-133">string</span></span>  | <span data-ttu-id="d800d-134">no</span><span class="sxs-lookup"><span data-stu-id="d800d-134">no</span></span>       | <span data-ttu-id="d800d-135">Stringa da confrontare con gli ID del pacchetto</span><span class="sxs-lookup"><span data-stu-id="d800d-135">The string to compare against package IDs</span></span>
<span data-ttu-id="d800d-136">skip</span><span class="sxs-lookup"><span data-stu-id="d800d-136">skip</span></span>        | <span data-ttu-id="d800d-137">URL</span><span class="sxs-lookup"><span data-stu-id="d800d-137">URL</span></span>    | <span data-ttu-id="d800d-138">integer</span><span class="sxs-lookup"><span data-stu-id="d800d-138">integer</span></span> | <span data-ttu-id="d800d-139">no</span><span class="sxs-lookup"><span data-stu-id="d800d-139">no</span></span>       | <span data-ttu-id="d800d-140">Numero di risultati da ignorare per la paginazione</span><span class="sxs-lookup"><span data-stu-id="d800d-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="d800d-141">prendere</span><span class="sxs-lookup"><span data-stu-id="d800d-141">take</span></span>        | <span data-ttu-id="d800d-142">URL</span><span class="sxs-lookup"><span data-stu-id="d800d-142">URL</span></span>    | <span data-ttu-id="d800d-143">integer</span><span class="sxs-lookup"><span data-stu-id="d800d-143">integer</span></span> | <span data-ttu-id="d800d-144">no</span><span class="sxs-lookup"><span data-stu-id="d800d-144">no</span></span>       | <span data-ttu-id="d800d-145">Numero di risultati da restituire per la paginazione</span><span class="sxs-lookup"><span data-stu-id="d800d-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="d800d-146">prerelease</span><span class="sxs-lookup"><span data-stu-id="d800d-146">prerelease</span></span>  | <span data-ttu-id="d800d-147">URL</span><span class="sxs-lookup"><span data-stu-id="d800d-147">URL</span></span>    | <span data-ttu-id="d800d-148">boolean</span><span class="sxs-lookup"><span data-stu-id="d800d-148">boolean</span></span> | <span data-ttu-id="d800d-149">no</span><span class="sxs-lookup"><span data-stu-id="d800d-149">no</span></span>       | <span data-ttu-id="d800d-150">`true`o `false` determinare se includere i [pacchetti in versione non definitiva](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d800d-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="d800d-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="d800d-151">semVerLevel</span></span> | <span data-ttu-id="d800d-152">URL</span><span class="sxs-lookup"><span data-stu-id="d800d-152">URL</span></span>    | <span data-ttu-id="d800d-153">string</span><span class="sxs-lookup"><span data-stu-id="d800d-153">string</span></span>  | <span data-ttu-id="d800d-154">no</span><span class="sxs-lookup"><span data-stu-id="d800d-154">no</span></span>       | <span data-ttu-id="d800d-155">Una stringa di versione SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="d800d-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="d800d-156">La query `q` di completamento automatico viene analizzata in modo definito dall'implementazione del server.</span><span class="sxs-lookup"><span data-stu-id="d800d-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="d800d-157">nuget.org supporta l'esecuzione di query per il prefisso dei token ID del pacchetto, che sono parti dell'ID prodotto suddividendo il case originale per Camel e i caratteri simbolo.</span><span class="sxs-lookup"><span data-stu-id="d800d-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="d800d-158">Il `skip` valore predefinito del parametro è 0.</span><span class="sxs-lookup"><span data-stu-id="d800d-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="d800d-159">Il `take` parametro deve essere un numero intero maggiore di zero.</span><span class="sxs-lookup"><span data-stu-id="d800d-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="d800d-160">L'implementazione del server può imporre un valore massimo.</span><span class="sxs-lookup"><span data-stu-id="d800d-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="d800d-161">Se `prerelease` non viene specificato, i pacchetti di versioni non definitive vengono esclusi.</span><span class="sxs-lookup"><span data-stu-id="d800d-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="d800d-162">Il `semVerLevel` parametro di query viene usato per acconsentire esplicitamente ai [pacchetti SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="d800d-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="d800d-163">Se questo parametro di query è escluso, verranno restituiti solo gli ID pacchetto con versioni compatibili con SemVer 1.0.0 (con le avvertenze di [controllo delle versioni standard di NuGet](../concepts/package-versioning.md) , ad esempio le stringhe di versione con 4 parti Integer).</span><span class="sxs-lookup"><span data-stu-id="d800d-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="d800d-164">Se `semVerLevel=2.0.0` viene specificato, verranno restituiti sia i pacchetti compatibili con SemVer 1.0.0 che SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d800d-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="d800d-165">Per ulteriori informazioni, vedere il [supporto di SemVer 2.0.0 per NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .</span><span class="sxs-lookup"><span data-stu-id="d800d-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="d800d-166">Risposta</span><span class="sxs-lookup"><span data-stu-id="d800d-166">Response</span></span>

<span data-ttu-id="d800d-167">La risposta è un documento JSON che contiene `take` i risultati di completamento automatico.</span><span class="sxs-lookup"><span data-stu-id="d800d-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="d800d-168">L'oggetto JSON radice presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="d800d-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="d800d-169">NOME</span><span class="sxs-lookup"><span data-stu-id="d800d-169">Name</span></span>      | <span data-ttu-id="d800d-170">Type</span><span class="sxs-lookup"><span data-stu-id="d800d-170">Type</span></span>             | <span data-ttu-id="d800d-171">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="d800d-171">Required</span></span> | <span data-ttu-id="d800d-172">Note</span><span class="sxs-lookup"><span data-stu-id="d800d-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="d800d-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="d800d-173">totalHits</span></span> | <span data-ttu-id="d800d-174">integer</span><span class="sxs-lookup"><span data-stu-id="d800d-174">integer</span></span>          | <span data-ttu-id="d800d-175">sì</span><span class="sxs-lookup"><span data-stu-id="d800d-175">yes</span></span>      | <span data-ttu-id="d800d-176">Il numero totale di corrispondenze, che `skip` non riguardano e`take`</span><span class="sxs-lookup"><span data-stu-id="d800d-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="d800d-177">data</span><span class="sxs-lookup"><span data-stu-id="d800d-177">data</span></span>      | <span data-ttu-id="d800d-178">matrice di stringhe</span><span class="sxs-lookup"><span data-stu-id="d800d-178">array of strings</span></span> | <span data-ttu-id="d800d-179">sì</span><span class="sxs-lookup"><span data-stu-id="d800d-179">yes</span></span>      | <span data-ttu-id="d800d-180">ID del pacchetto corrispondenti alla richiesta</span><span class="sxs-lookup"><span data-stu-id="d800d-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="d800d-181">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="d800d-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="d800d-182">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="d800d-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="d800d-183">Enumera versioni pacchetto</span><span class="sxs-lookup"><span data-stu-id="d800d-183">Enumerate package versions</span></span>

<span data-ttu-id="d800d-184">Una volta individuato l'ID di un pacchetto usando l'API precedente, un client può usare l'API di completamento automatico per enumerare le versioni del pacchetto per un ID pacchetto specificato.</span><span class="sxs-lookup"><span data-stu-id="d800d-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="d800d-185">Una versione del pacchetto non in elenco non verrà visualizzata nei risultati.</span><span class="sxs-lookup"><span data-stu-id="d800d-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="d800d-186">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="d800d-186">Request parameters</span></span>

<span data-ttu-id="d800d-187">Name</span><span class="sxs-lookup"><span data-stu-id="d800d-187">Name</span></span>        | <span data-ttu-id="d800d-188">In</span><span class="sxs-lookup"><span data-stu-id="d800d-188">In</span></span>     | <span data-ttu-id="d800d-189">Type</span><span class="sxs-lookup"><span data-stu-id="d800d-189">Type</span></span>    | <span data-ttu-id="d800d-190">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="d800d-190">Required</span></span> | <span data-ttu-id="d800d-191">Note</span><span class="sxs-lookup"><span data-stu-id="d800d-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="d800d-192">id</span><span class="sxs-lookup"><span data-stu-id="d800d-192">id</span></span>          | <span data-ttu-id="d800d-193">URL</span><span class="sxs-lookup"><span data-stu-id="d800d-193">URL</span></span>    | <span data-ttu-id="d800d-194">string</span><span class="sxs-lookup"><span data-stu-id="d800d-194">string</span></span>  | <span data-ttu-id="d800d-195">sì</span><span class="sxs-lookup"><span data-stu-id="d800d-195">yes</span></span>      | <span data-ttu-id="d800d-196">ID del pacchetto per cui recuperare le versioni</span><span class="sxs-lookup"><span data-stu-id="d800d-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="d800d-197">prerelease</span><span class="sxs-lookup"><span data-stu-id="d800d-197">prerelease</span></span>  | <span data-ttu-id="d800d-198">URL</span><span class="sxs-lookup"><span data-stu-id="d800d-198">URL</span></span>    | <span data-ttu-id="d800d-199">boolean</span><span class="sxs-lookup"><span data-stu-id="d800d-199">boolean</span></span> | <span data-ttu-id="d800d-200">no</span><span class="sxs-lookup"><span data-stu-id="d800d-200">no</span></span>       | <span data-ttu-id="d800d-201">`true`o `false` determinare se includere i [pacchetti in versione non definitiva](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d800d-201">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="d800d-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="d800d-202">semVerLevel</span></span> | <span data-ttu-id="d800d-203">URL</span><span class="sxs-lookup"><span data-stu-id="d800d-203">URL</span></span>    | <span data-ttu-id="d800d-204">string</span><span class="sxs-lookup"><span data-stu-id="d800d-204">string</span></span>  | <span data-ttu-id="d800d-205">no</span><span class="sxs-lookup"><span data-stu-id="d800d-205">no</span></span>       | <span data-ttu-id="d800d-206">Una stringa di versione SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="d800d-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="d800d-207">Se `prerelease` non viene specificato, i pacchetti di versioni non definitive vengono esclusi.</span><span class="sxs-lookup"><span data-stu-id="d800d-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="d800d-208">Il `semVerLevel` parametro di query viene usato per acconsentire esplicitamente ai pacchetti SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d800d-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="d800d-209">Se questo parametro di query è escluso, verranno restituite solo le versioni SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="d800d-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="d800d-210">Se `semVerLevel=2.0.0` viene specificato, verranno restituite sia le versioni SemVer 1.0.0 che SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d800d-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="d800d-211">Per ulteriori informazioni, vedere il [supporto di SemVer 2.0.0 per NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .</span><span class="sxs-lookup"><span data-stu-id="d800d-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="d800d-212">Risposta</span><span class="sxs-lookup"><span data-stu-id="d800d-212">Response</span></span>

<span data-ttu-id="d800d-213">La risposta è un documento JSON contenente tutte le versioni dei pacchetti dell'ID pacchetto specificato, filtrando in base ai parametri di query specificati.</span><span class="sxs-lookup"><span data-stu-id="d800d-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="d800d-214">L'oggetto JSON radice presenta la proprietà seguente:</span><span class="sxs-lookup"><span data-stu-id="d800d-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="d800d-215">Name</span><span class="sxs-lookup"><span data-stu-id="d800d-215">Name</span></span>      | <span data-ttu-id="d800d-216">Type</span><span class="sxs-lookup"><span data-stu-id="d800d-216">Type</span></span>             | <span data-ttu-id="d800d-217">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="d800d-217">Required</span></span> | <span data-ttu-id="d800d-218">Note</span><span class="sxs-lookup"><span data-stu-id="d800d-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="d800d-219">data</span><span class="sxs-lookup"><span data-stu-id="d800d-219">data</span></span>      | <span data-ttu-id="d800d-220">matrice di stringhe</span><span class="sxs-lookup"><span data-stu-id="d800d-220">array of strings</span></span> | <span data-ttu-id="d800d-221">sì</span><span class="sxs-lookup"><span data-stu-id="d800d-221">yes</span></span>      | <span data-ttu-id="d800d-222">Versioni del pacchetto corrispondenti alla richiesta</span><span class="sxs-lookup"><span data-stu-id="d800d-222">The package versions matched by the request</span></span>

<span data-ttu-id="d800d-223">Le versioni del pacchetto nella `data` matrice possono contenere i metadati di compilazione SemVer 2.0.0 ( `1.0.0+metadata`ad esempio) `semVerLevel=2.0.0` se è specificato nella stringa di query.</span><span class="sxs-lookup"><span data-stu-id="d800d-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d800d-224">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="d800d-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="d800d-225">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="d800d-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
