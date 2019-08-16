---
title: Contenuto del pacchetto, API NuGet
description: L'indirizzo di base del pacchetto è una semplice interfaccia per il recupero del pacchetto stesso.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 5ec6c0e17a3e8b9a3f156a48685bcaafe42c744b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488226"
---
# <a name="package-content"></a><span data-ttu-id="13d12-103">Contenuto del pacchetto</span><span class="sxs-lookup"><span data-stu-id="13d12-103">Package Content</span></span>

<span data-ttu-id="13d12-104">È possibile generare un URL per recuperare il contenuto di un pacchetto arbitrario (il file con estensione nupkg) usando l'API V3.</span><span class="sxs-lookup"><span data-stu-id="13d12-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="13d12-105">La risorsa utilizzata per il recupero del contenuto del pacchetto `PackageBaseAddress` è la risorsa presente nell' [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="13d12-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="13d12-106">Questa risorsa consente inoltre l'individuazione di tutte le versioni di un pacchetto, elencate o riportate in elenco.</span><span class="sxs-lookup"><span data-stu-id="13d12-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="13d12-107">Questa risorsa viene comunemente definita "indirizzo di base del pacchetto" o come "contenitore Flat".</span><span class="sxs-lookup"><span data-stu-id="13d12-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="13d12-108">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="13d12-108">Versioning</span></span>

<span data-ttu-id="13d12-109">Viene utilizzato `@type` il valore seguente:</span><span class="sxs-lookup"><span data-stu-id="13d12-109">The following `@type` value is used:</span></span>

<span data-ttu-id="13d12-110">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="13d12-110">@type value</span></span>              | <span data-ttu-id="13d12-111">Note</span><span class="sxs-lookup"><span data-stu-id="13d12-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="13d12-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="13d12-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="13d12-113">Versione iniziale</span><span class="sxs-lookup"><span data-stu-id="13d12-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="13d12-114">URL di base</span><span class="sxs-lookup"><span data-stu-id="13d12-114">Base URL</span></span>

<span data-ttu-id="13d12-115">L'URL di base per le API seguenti è il valore della `@id` proprietà associata al valore di risorsa `@type` sopra menzionato.</span><span class="sxs-lookup"><span data-stu-id="13d12-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="13d12-116">Nel documento seguente verrà usato l'URL `{@id}` di base segnaposto.</span><span class="sxs-lookup"><span data-stu-id="13d12-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="13d12-117">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="13d12-117">HTTP methods</span></span>

<span data-ttu-id="13d12-118">Tutti gli URL trovati nella risorsa di registrazione supportano i metodi `GET` http `HEAD`e.</span><span class="sxs-lookup"><span data-stu-id="13d12-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="13d12-119">Enumera versioni pacchetto</span><span class="sxs-lookup"><span data-stu-id="13d12-119">Enumerate package versions</span></span>

<span data-ttu-id="13d12-120">Se il client conosce un ID pacchetto e desidera individuare le versioni del pacchetto disponibili nell'origine del pacchetto, il client può costruire un URL stimabile per enumerare tutte le versioni dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="13d12-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="13d12-121">Questo elenco è destinato a essere un "elenco di directory" per l'API del contenuto del pacchetto indicata di seguito.</span><span class="sxs-lookup"><span data-stu-id="13d12-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="13d12-122">Questo elenco contiene le versioni di pacchetto elencate e non in elenco.</span><span class="sxs-lookup"><span data-stu-id="13d12-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="13d12-123">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="13d12-123">Request parameters</span></span>

<span data-ttu-id="13d12-124">Name</span><span class="sxs-lookup"><span data-stu-id="13d12-124">Name</span></span>     | <span data-ttu-id="13d12-125">In</span><span class="sxs-lookup"><span data-stu-id="13d12-125">In</span></span>     | <span data-ttu-id="13d12-126">Type</span><span class="sxs-lookup"><span data-stu-id="13d12-126">Type</span></span>    | <span data-ttu-id="13d12-127">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="13d12-127">Required</span></span> | <span data-ttu-id="13d12-128">Note</span><span class="sxs-lookup"><span data-stu-id="13d12-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="13d12-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="13d12-129">LOWER_ID</span></span> | <span data-ttu-id="13d12-130">URL</span><span class="sxs-lookup"><span data-stu-id="13d12-130">URL</span></span>    | <span data-ttu-id="13d12-131">string</span><span class="sxs-lookup"><span data-stu-id="13d12-131">string</span></span>  | <span data-ttu-id="13d12-132">sì</span><span class="sxs-lookup"><span data-stu-id="13d12-132">yes</span></span>      | <span data-ttu-id="13d12-133">ID del pacchetto, minuscolo</span><span class="sxs-lookup"><span data-stu-id="13d12-133">The package ID, lowercase</span></span>

<span data-ttu-id="13d12-134">Il `LOWER_ID` valore è l'ID pacchetto desiderato in minuscolo usando le regole implementate da. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Metodo NET.</span><span class="sxs-lookup"><span data-stu-id="13d12-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="13d12-135">Risposta</span><span class="sxs-lookup"><span data-stu-id="13d12-135">Response</span></span>

<span data-ttu-id="13d12-136">Se l'origine del pacchetto non dispone di versioni dell'ID pacchetto fornito, viene restituito un codice di stato 404.</span><span class="sxs-lookup"><span data-stu-id="13d12-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="13d12-137">Se l'origine del pacchetto contiene una o più versioni, viene restituito un codice di stato 200.</span><span class="sxs-lookup"><span data-stu-id="13d12-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="13d12-138">Il corpo della risposta è un oggetto JSON con la proprietà seguente:</span><span class="sxs-lookup"><span data-stu-id="13d12-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="13d12-139">NOME</span><span class="sxs-lookup"><span data-stu-id="13d12-139">Name</span></span>     | <span data-ttu-id="13d12-140">Type</span><span class="sxs-lookup"><span data-stu-id="13d12-140">Type</span></span>             | <span data-ttu-id="13d12-141">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="13d12-141">Required</span></span> | <span data-ttu-id="13d12-142">Note</span><span class="sxs-lookup"><span data-stu-id="13d12-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="13d12-143">versioni</span><span class="sxs-lookup"><span data-stu-id="13d12-143">versions</span></span> | <span data-ttu-id="13d12-144">matrice di stringhe</span><span class="sxs-lookup"><span data-stu-id="13d12-144">array of strings</span></span> | <span data-ttu-id="13d12-145">sì</span><span class="sxs-lookup"><span data-stu-id="13d12-145">yes</span></span>      | <span data-ttu-id="13d12-146">ID pacchetto disponibili</span><span class="sxs-lookup"><span data-stu-id="13d12-146">The package IDs available</span></span>

<span data-ttu-id="13d12-147">Le stringhe nella `versions` matrice sono tutte stringhe di versione di [NuGet normalizzate](../concepts/package-versioning.md#normalized-version-numbers)e normalizzate.</span><span class="sxs-lookup"><span data-stu-id="13d12-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="13d12-148">Le stringhe di versione non contengono metadati di compilazione SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="13d12-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="13d12-149">Lo scopo è che le stringhe di versione trovate in questa matrice possano essere usate Verbatim per `LOWER_VERSION` i token trovati negli endpoint seguenti.</span><span class="sxs-lookup"><span data-stu-id="13d12-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="13d12-150">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="13d12-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="13d12-151">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="13d12-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="13d12-152">Scaricare il contenuto del pacchetto (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="13d12-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="13d12-153">Se il client conosce un ID e una versione del pacchetto e vuole scaricare il contenuto del pacchetto, è sufficiente costruire l'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="13d12-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="13d12-154">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="13d12-154">Request parameters</span></span>

<span data-ttu-id="13d12-155">Name</span><span class="sxs-lookup"><span data-stu-id="13d12-155">Name</span></span>          | <span data-ttu-id="13d12-156">In</span><span class="sxs-lookup"><span data-stu-id="13d12-156">In</span></span>     | <span data-ttu-id="13d12-157">Type</span><span class="sxs-lookup"><span data-stu-id="13d12-157">Type</span></span>   | <span data-ttu-id="13d12-158">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="13d12-158">Required</span></span> | <span data-ttu-id="13d12-159">Note</span><span class="sxs-lookup"><span data-stu-id="13d12-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="13d12-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="13d12-160">LOWER_ID</span></span>      | <span data-ttu-id="13d12-161">URL</span><span class="sxs-lookup"><span data-stu-id="13d12-161">URL</span></span>    | <span data-ttu-id="13d12-162">string</span><span class="sxs-lookup"><span data-stu-id="13d12-162">string</span></span> | <span data-ttu-id="13d12-163">sì</span><span class="sxs-lookup"><span data-stu-id="13d12-163">yes</span></span>      | <span data-ttu-id="13d12-164">ID del pacchetto, minuscolo</span><span class="sxs-lookup"><span data-stu-id="13d12-164">The package ID, lowercase</span></span>
<span data-ttu-id="13d12-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="13d12-165">LOWER_VERSION</span></span> | <span data-ttu-id="13d12-166">URL</span><span class="sxs-lookup"><span data-stu-id="13d12-166">URL</span></span>    | <span data-ttu-id="13d12-167">string</span><span class="sxs-lookup"><span data-stu-id="13d12-167">string</span></span> | <span data-ttu-id="13d12-168">sì</span><span class="sxs-lookup"><span data-stu-id="13d12-168">yes</span></span>      | <span data-ttu-id="13d12-169">Versione del pacchetto, normalizzata e minuscola</span><span class="sxs-lookup"><span data-stu-id="13d12-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="13d12-170">Sia `LOWER_ID` che`LOWER_VERSION` sono minuscole usando le regole implementate da. NET[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="13d12-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="13d12-171">ProcessOnStatus.</span><span class="sxs-lookup"><span data-stu-id="13d12-171">method.</span></span>

<span data-ttu-id="13d12-172">È la versione del pacchetto desiderata normalizzata usando [le regole](../concepts/package-versioning.md#normalized-version-numbers)di normalizzazione della versione di NuGet. `LOWER_VERSION`</span><span class="sxs-lookup"><span data-stu-id="13d12-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="13d12-173">Ciò significa che in questo caso i metadati di compilazione consentiti dalla specifica SemVer 2.0.0 devono essere esclusi.</span><span class="sxs-lookup"><span data-stu-id="13d12-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="13d12-174">Corpo della risposta</span><span class="sxs-lookup"><span data-stu-id="13d12-174">Response body</span></span>

<span data-ttu-id="13d12-175">Se il pacchetto esiste nell'origine del pacchetto, viene restituito un codice di stato 200.</span><span class="sxs-lookup"><span data-stu-id="13d12-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="13d12-176">Il corpo della risposta sarà il contenuto del pacchetto stesso.</span><span class="sxs-lookup"><span data-stu-id="13d12-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="13d12-177">Se il pacchetto non esiste nell'origine del pacchetto, viene restituito un codice di stato 404.</span><span class="sxs-lookup"><span data-stu-id="13d12-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="13d12-178">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="13d12-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="13d12-179">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="13d12-179">Sample response</span></span>

<span data-ttu-id="13d12-180">Flusso binario che rappresenta il file con estensione nupkg per Newtonsoft. JSON 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="13d12-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="13d12-181">Scarica il manifesto del pacchetto (. NuSpec)</span><span class="sxs-lookup"><span data-stu-id="13d12-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="13d12-182">Se il client conosce un ID e una versione del pacchetto e vuole scaricare il manifesto del pacchetto, è sufficiente costruire l'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="13d12-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="13d12-183">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="13d12-183">Request parameters</span></span>

<span data-ttu-id="13d12-184">Name</span><span class="sxs-lookup"><span data-stu-id="13d12-184">Name</span></span>          | <span data-ttu-id="13d12-185">In</span><span class="sxs-lookup"><span data-stu-id="13d12-185">In</span></span>     | <span data-ttu-id="13d12-186">Type</span><span class="sxs-lookup"><span data-stu-id="13d12-186">Type</span></span>   | <span data-ttu-id="13d12-187">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="13d12-187">Required</span></span> | <span data-ttu-id="13d12-188">Note</span><span class="sxs-lookup"><span data-stu-id="13d12-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="13d12-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="13d12-189">LOWER_ID</span></span>      | <span data-ttu-id="13d12-190">URL</span><span class="sxs-lookup"><span data-stu-id="13d12-190">URL</span></span>    | <span data-ttu-id="13d12-191">string</span><span class="sxs-lookup"><span data-stu-id="13d12-191">string</span></span> | <span data-ttu-id="13d12-192">sì</span><span class="sxs-lookup"><span data-stu-id="13d12-192">yes</span></span>      | <span data-ttu-id="13d12-193">ID del pacchetto, minuscolo</span><span class="sxs-lookup"><span data-stu-id="13d12-193">The package ID, lowercase</span></span>
<span data-ttu-id="13d12-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="13d12-194">LOWER_VERSION</span></span> | <span data-ttu-id="13d12-195">URL</span><span class="sxs-lookup"><span data-stu-id="13d12-195">URL</span></span>    | <span data-ttu-id="13d12-196">string</span><span class="sxs-lookup"><span data-stu-id="13d12-196">string</span></span> | <span data-ttu-id="13d12-197">sì</span><span class="sxs-lookup"><span data-stu-id="13d12-197">yes</span></span>      | <span data-ttu-id="13d12-198">Versione del pacchetto, normalizzata e minuscola</span><span class="sxs-lookup"><span data-stu-id="13d12-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="13d12-199">Sia `LOWER_ID` che`LOWER_VERSION` sono minuscole usando le regole implementate da. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Metodo NET.</span><span class="sxs-lookup"><span data-stu-id="13d12-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="13d12-200">È la versione del pacchetto desiderata normalizzata usando [le regole](../concepts/package-versioning.md#normalized-version-numbers)di normalizzazione della versione di NuGet. `LOWER_VERSION`</span><span class="sxs-lookup"><span data-stu-id="13d12-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="13d12-201">Ciò significa che in questo caso i metadati di compilazione consentiti dalla specifica SemVer 2.0.0 devono essere esclusi.</span><span class="sxs-lookup"><span data-stu-id="13d12-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="13d12-202">Corpo della risposta</span><span class="sxs-lookup"><span data-stu-id="13d12-202">Response body</span></span>

<span data-ttu-id="13d12-203">Se il pacchetto esiste nell'origine del pacchetto, viene restituito un codice di stato 200.</span><span class="sxs-lookup"><span data-stu-id="13d12-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="13d12-204">Il corpo della risposta sarà il manifesto del pacchetto, ovvero il file con estensione NuSpec contenuto nel file. nupkg corrispondente.</span><span class="sxs-lookup"><span data-stu-id="13d12-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="13d12-205">Il file con estensione NuSpec è un documento XML.</span><span class="sxs-lookup"><span data-stu-id="13d12-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="13d12-206">Se il pacchetto non esiste nell'origine del pacchetto, viene restituito un codice di stato 404.</span><span class="sxs-lookup"><span data-stu-id="13d12-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="13d12-207">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="13d12-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="13d12-208">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="13d12-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
