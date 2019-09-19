---
title: Contenuto del pacchetto, API NuGet
description: L'indirizzo di base del pacchetto è una semplice interfaccia per il recupero del pacchetto stesso.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 7aea28d6224a89149aa33be035c82a45db3058f0
ms.sourcegitcommit: 1eda83ab537c86cc27316e7bc67f95a358766e63
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/18/2019
ms.locfileid: "71094115"
---
# <a name="package-content"></a><span data-ttu-id="0328e-103">Contenuto del pacchetto</span><span class="sxs-lookup"><span data-stu-id="0328e-103">Package Content</span></span>

<span data-ttu-id="0328e-104">È possibile generare un URL per recuperare il contenuto di un pacchetto arbitrario (il file con estensione nupkg) usando l'API V3.</span><span class="sxs-lookup"><span data-stu-id="0328e-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="0328e-105">La risorsa utilizzata per il recupero del contenuto del pacchetto `PackageBaseAddress` è la risorsa presente nell' [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="0328e-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="0328e-106">Questa risorsa consente inoltre l'individuazione di tutte le versioni di un pacchetto, elencate o riportate in elenco.</span><span class="sxs-lookup"><span data-stu-id="0328e-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="0328e-107">Questa risorsa viene comunemente definita "indirizzo di base del pacchetto" o come "contenitore Flat".</span><span class="sxs-lookup"><span data-stu-id="0328e-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="0328e-108">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="0328e-108">Versioning</span></span>

<span data-ttu-id="0328e-109">Viene utilizzato `@type` il valore seguente:</span><span class="sxs-lookup"><span data-stu-id="0328e-109">The following `@type` value is used:</span></span>

<span data-ttu-id="0328e-110">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="0328e-110">@type value</span></span>              | <span data-ttu-id="0328e-111">Note</span><span class="sxs-lookup"><span data-stu-id="0328e-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="0328e-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="0328e-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="0328e-113">Versione iniziale</span><span class="sxs-lookup"><span data-stu-id="0328e-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="0328e-114">URL di base</span><span class="sxs-lookup"><span data-stu-id="0328e-114">Base URL</span></span>

<span data-ttu-id="0328e-115">L'URL di base per le API seguenti è il valore della `@id` proprietà associata al valore di risorsa `@type` sopra menzionato.</span><span class="sxs-lookup"><span data-stu-id="0328e-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="0328e-116">Nel documento seguente verrà usato l'URL `{@id}` di base segnaposto.</span><span class="sxs-lookup"><span data-stu-id="0328e-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="0328e-117">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="0328e-117">HTTP methods</span></span>

<span data-ttu-id="0328e-118">Tutti gli URL trovati nella risorsa di registrazione supportano i metodi `GET` http `HEAD`e.</span><span class="sxs-lookup"><span data-stu-id="0328e-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="0328e-119">Enumera versioni pacchetto</span><span class="sxs-lookup"><span data-stu-id="0328e-119">Enumerate package versions</span></span>

<span data-ttu-id="0328e-120">Se il client conosce un ID pacchetto e desidera individuare le versioni del pacchetto disponibili nell'origine del pacchetto, il client può costruire un URL stimabile per enumerare tutte le versioni dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="0328e-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="0328e-121">Questo elenco è destinato a essere un "elenco di directory" per l'API del contenuto del pacchetto indicata di seguito.</span><span class="sxs-lookup"><span data-stu-id="0328e-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="0328e-122">Questo elenco contiene le versioni di pacchetto elencate e non in elenco.</span><span class="sxs-lookup"><span data-stu-id="0328e-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="0328e-123">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="0328e-123">Request parameters</span></span>

<span data-ttu-id="0328e-124">Name</span><span class="sxs-lookup"><span data-stu-id="0328e-124">Name</span></span>     | <span data-ttu-id="0328e-125">In</span><span class="sxs-lookup"><span data-stu-id="0328e-125">In</span></span>     | <span data-ttu-id="0328e-126">Type</span><span class="sxs-lookup"><span data-stu-id="0328e-126">Type</span></span>    | <span data-ttu-id="0328e-127">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="0328e-127">Required</span></span> | <span data-ttu-id="0328e-128">Note</span><span class="sxs-lookup"><span data-stu-id="0328e-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="0328e-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="0328e-129">LOWER_ID</span></span> | <span data-ttu-id="0328e-130">URL</span><span class="sxs-lookup"><span data-stu-id="0328e-130">URL</span></span>    | <span data-ttu-id="0328e-131">string</span><span class="sxs-lookup"><span data-stu-id="0328e-131">string</span></span>  | <span data-ttu-id="0328e-132">sì</span><span class="sxs-lookup"><span data-stu-id="0328e-132">yes</span></span>      | <span data-ttu-id="0328e-133">ID del pacchetto, minuscolo</span><span class="sxs-lookup"><span data-stu-id="0328e-133">The package ID, lowercased</span></span>

<span data-ttu-id="0328e-134">Il `LOWER_ID` valore è l'ID pacchetto desiderato in minuscolo usando le regole implementate da. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Metodo NET.</span><span class="sxs-lookup"><span data-stu-id="0328e-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="0328e-135">Risposta</span><span class="sxs-lookup"><span data-stu-id="0328e-135">Response</span></span>

<span data-ttu-id="0328e-136">Se l'origine del pacchetto non dispone di versioni dell'ID pacchetto fornito, viene restituito un codice di stato 404.</span><span class="sxs-lookup"><span data-stu-id="0328e-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="0328e-137">Se l'origine del pacchetto contiene una o più versioni, viene restituito un codice di stato 200.</span><span class="sxs-lookup"><span data-stu-id="0328e-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="0328e-138">Il corpo della risposta è un oggetto JSON con la proprietà seguente:</span><span class="sxs-lookup"><span data-stu-id="0328e-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="0328e-139">Name</span><span class="sxs-lookup"><span data-stu-id="0328e-139">Name</span></span>     | <span data-ttu-id="0328e-140">Type</span><span class="sxs-lookup"><span data-stu-id="0328e-140">Type</span></span>             | <span data-ttu-id="0328e-141">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="0328e-141">Required</span></span> | <span data-ttu-id="0328e-142">Note</span><span class="sxs-lookup"><span data-stu-id="0328e-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="0328e-143">versioni</span><span class="sxs-lookup"><span data-stu-id="0328e-143">versions</span></span> | <span data-ttu-id="0328e-144">Matrice di stringhe</span><span class="sxs-lookup"><span data-stu-id="0328e-144">array of strings</span></span> | <span data-ttu-id="0328e-145">sì</span><span class="sxs-lookup"><span data-stu-id="0328e-145">yes</span></span>      | <span data-ttu-id="0328e-146">Versioni disponibili</span><span class="sxs-lookup"><span data-stu-id="0328e-146">The versions available</span></span>

<span data-ttu-id="0328e-147">Le stringhe nella `versions` matrice sono tutte stringhe di versione di [NuGet normalizzate e normalizzate](../concepts/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="0328e-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="0328e-148">Le stringhe di versione non contengono metadati di compilazione SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="0328e-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="0328e-149">Lo scopo è che le stringhe di versione trovate in questa matrice possano essere usate Verbatim per `LOWER_VERSION` i token trovati negli endpoint seguenti.</span><span class="sxs-lookup"><span data-stu-id="0328e-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="0328e-150">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="0328e-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="0328e-151">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="0328e-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="0328e-152">Scaricare il contenuto del pacchetto (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="0328e-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="0328e-153">Se il client conosce un ID e una versione del pacchetto e vuole scaricare il contenuto del pacchetto, è sufficiente costruire l'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="0328e-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="0328e-154">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="0328e-154">Request parameters</span></span>

<span data-ttu-id="0328e-155">NOME</span><span class="sxs-lookup"><span data-stu-id="0328e-155">Name</span></span>          | <span data-ttu-id="0328e-156">In</span><span class="sxs-lookup"><span data-stu-id="0328e-156">In</span></span>     | <span data-ttu-id="0328e-157">Type</span><span class="sxs-lookup"><span data-stu-id="0328e-157">Type</span></span>   | <span data-ttu-id="0328e-158">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="0328e-158">Required</span></span> | <span data-ttu-id="0328e-159">Note</span><span class="sxs-lookup"><span data-stu-id="0328e-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="0328e-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="0328e-160">LOWER_ID</span></span>      | <span data-ttu-id="0328e-161">URL</span><span class="sxs-lookup"><span data-stu-id="0328e-161">URL</span></span>    | <span data-ttu-id="0328e-162">string</span><span class="sxs-lookup"><span data-stu-id="0328e-162">string</span></span> | <span data-ttu-id="0328e-163">sì</span><span class="sxs-lookup"><span data-stu-id="0328e-163">yes</span></span>      | <span data-ttu-id="0328e-164">ID del pacchetto, minuscolo</span><span class="sxs-lookup"><span data-stu-id="0328e-164">The package ID, lowercase</span></span>
<span data-ttu-id="0328e-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="0328e-165">LOWER_VERSION</span></span> | <span data-ttu-id="0328e-166">URL</span><span class="sxs-lookup"><span data-stu-id="0328e-166">URL</span></span>    | <span data-ttu-id="0328e-167">string</span><span class="sxs-lookup"><span data-stu-id="0328e-167">string</span></span> | <span data-ttu-id="0328e-168">sì</span><span class="sxs-lookup"><span data-stu-id="0328e-168">yes</span></span>      | <span data-ttu-id="0328e-169">Versione del pacchetto, normalizzata e minuscola</span><span class="sxs-lookup"><span data-stu-id="0328e-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="0328e-170">Sia `LOWER_ID` che`LOWER_VERSION` sono minuscole usando le regole implementate da. NET[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="0328e-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="0328e-171">ProcessOnStatus.</span><span class="sxs-lookup"><span data-stu-id="0328e-171">method.</span></span>

<span data-ttu-id="0328e-172">È la versione del pacchetto desiderata normalizzata usando [le regole di normalizzazione](../concepts/package-versioning.md#normalized-version-numbers)della versione di NuGet. `LOWER_VERSION`</span><span class="sxs-lookup"><span data-stu-id="0328e-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="0328e-173">Ciò significa che in questo caso i metadati di compilazione consentiti dalla specifica SemVer 2.0.0 devono essere esclusi.</span><span class="sxs-lookup"><span data-stu-id="0328e-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="0328e-174">Corpo della risposta</span><span class="sxs-lookup"><span data-stu-id="0328e-174">Response body</span></span>

<span data-ttu-id="0328e-175">Se il pacchetto esiste nell'origine del pacchetto, viene restituito un codice di stato 200.</span><span class="sxs-lookup"><span data-stu-id="0328e-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="0328e-176">Il corpo della risposta sarà il contenuto del pacchetto stesso.</span><span class="sxs-lookup"><span data-stu-id="0328e-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="0328e-177">Se il pacchetto non esiste nell'origine del pacchetto, viene restituito un codice di stato 404.</span><span class="sxs-lookup"><span data-stu-id="0328e-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="0328e-178">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="0328e-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="0328e-179">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="0328e-179">Sample response</span></span>

<span data-ttu-id="0328e-180">Flusso binario che rappresenta il file con estensione nupkg per Newtonsoft. JSON 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="0328e-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="0328e-181">Scarica il manifesto del pacchetto (. NuSpec)</span><span class="sxs-lookup"><span data-stu-id="0328e-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="0328e-182">Se il client conosce un ID e una versione del pacchetto e vuole scaricare il manifesto del pacchetto, è sufficiente costruire l'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="0328e-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="0328e-183">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="0328e-183">Request parameters</span></span>

<span data-ttu-id="0328e-184">NOME</span><span class="sxs-lookup"><span data-stu-id="0328e-184">Name</span></span>          | <span data-ttu-id="0328e-185">In</span><span class="sxs-lookup"><span data-stu-id="0328e-185">In</span></span>     | <span data-ttu-id="0328e-186">Type</span><span class="sxs-lookup"><span data-stu-id="0328e-186">Type</span></span>   | <span data-ttu-id="0328e-187">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="0328e-187">Required</span></span> | <span data-ttu-id="0328e-188">Note</span><span class="sxs-lookup"><span data-stu-id="0328e-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="0328e-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="0328e-189">LOWER_ID</span></span>      | <span data-ttu-id="0328e-190">URL</span><span class="sxs-lookup"><span data-stu-id="0328e-190">URL</span></span>    | <span data-ttu-id="0328e-191">string</span><span class="sxs-lookup"><span data-stu-id="0328e-191">string</span></span> | <span data-ttu-id="0328e-192">sì</span><span class="sxs-lookup"><span data-stu-id="0328e-192">yes</span></span>      | <span data-ttu-id="0328e-193">ID del pacchetto, minuscolo</span><span class="sxs-lookup"><span data-stu-id="0328e-193">The package ID, lowercase</span></span>
<span data-ttu-id="0328e-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="0328e-194">LOWER_VERSION</span></span> | <span data-ttu-id="0328e-195">URL</span><span class="sxs-lookup"><span data-stu-id="0328e-195">URL</span></span>    | <span data-ttu-id="0328e-196">string</span><span class="sxs-lookup"><span data-stu-id="0328e-196">string</span></span> | <span data-ttu-id="0328e-197">sì</span><span class="sxs-lookup"><span data-stu-id="0328e-197">yes</span></span>      | <span data-ttu-id="0328e-198">Versione del pacchetto, normalizzata e minuscola</span><span class="sxs-lookup"><span data-stu-id="0328e-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="0328e-199">Sia `LOWER_ID` che`LOWER_VERSION` sono minuscole usando le regole implementate da. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Metodo NET.</span><span class="sxs-lookup"><span data-stu-id="0328e-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="0328e-200">È la versione del pacchetto desiderata normalizzata usando [le regole di normalizzazione](../concepts/package-versioning.md#normalized-version-numbers)della versione di NuGet. `LOWER_VERSION`</span><span class="sxs-lookup"><span data-stu-id="0328e-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="0328e-201">Ciò significa che in questo caso i metadati di compilazione consentiti dalla specifica SemVer 2.0.0 devono essere esclusi.</span><span class="sxs-lookup"><span data-stu-id="0328e-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="0328e-202">Corpo della risposta</span><span class="sxs-lookup"><span data-stu-id="0328e-202">Response body</span></span>

<span data-ttu-id="0328e-203">Se il pacchetto esiste nell'origine del pacchetto, viene restituito un codice di stato 200.</span><span class="sxs-lookup"><span data-stu-id="0328e-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="0328e-204">Il corpo della risposta sarà il manifesto del pacchetto, ovvero il file con estensione NuSpec contenuto nel file. nupkg corrispondente.</span><span class="sxs-lookup"><span data-stu-id="0328e-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="0328e-205">Il file con estensione NuSpec è un documento XML.</span><span class="sxs-lookup"><span data-stu-id="0328e-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="0328e-206">Se il pacchetto non esiste nell'origine del pacchetto, viene restituito un codice di stato 404.</span><span class="sxs-lookup"><span data-stu-id="0328e-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="0328e-207">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="0328e-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="0328e-208">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="0328e-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
