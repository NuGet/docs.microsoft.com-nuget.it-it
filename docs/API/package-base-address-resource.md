---
title: Contenuto del pacchetto, NuGet API
description: L'indirizzo di base del pacchetto è un'interfaccia semplice per recuperare il pacchetto stesso.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a6ac40368f30d33f35d4ca0b6cc18ce4bd6efee5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="package-content"></a><span data-ttu-id="2addc-103">Contenuto del pacchetto</span><span class="sxs-lookup"><span data-stu-id="2addc-103">Package Content</span></span>

<span data-ttu-id="2addc-104">È possibile generare un URL per recuperare il contenuto del pacchetto non autorizzato (il file .nupkg) tramite l'API V3.</span><span class="sxs-lookup"><span data-stu-id="2addc-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="2addc-105">La risorsa utilizzata per il recupero di contenuto del pacchetto è il `PackageBaseAddress` risorse, vedere il [indice servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="2addc-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="2addc-106">Questa risorsa consente inoltre l'individuazione di tutte le versioni di un pacchetto, elencato o non in elenco.</span><span class="sxs-lookup"><span data-stu-id="2addc-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="2addc-107">Questa risorsa è noto come un "pacchetto indirizzo di base" o "container flat".</span><span class="sxs-lookup"><span data-stu-id="2addc-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="2addc-108">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="2addc-108">Versioning</span></span>

<span data-ttu-id="2addc-109">Le operazioni seguenti `@type` valore viene utilizzato:</span><span class="sxs-lookup"><span data-stu-id="2addc-109">The following `@type` value is used:</span></span>

<span data-ttu-id="2addc-110">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="2addc-110">@type value</span></span>              | <span data-ttu-id="2addc-111">Note</span><span class="sxs-lookup"><span data-stu-id="2addc-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="2addc-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="2addc-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="2addc-113">La versione iniziale</span><span class="sxs-lookup"><span data-stu-id="2addc-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="2addc-114">URL di base</span><span class="sxs-lookup"><span data-stu-id="2addc-114">Base URL</span></span>

<span data-ttu-id="2addc-115">L'URL di base per le API seguente è il valore di `@id` proprietà associato alla risorsa menzionati in precedenza `@type` valore.</span><span class="sxs-lookup"><span data-stu-id="2addc-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="2addc-116">Nel documento seguente, il segnaposto URL di base `{@id}` verrà utilizzato.</span><span class="sxs-lookup"><span data-stu-id="2addc-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="2addc-117">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="2addc-117">HTTP methods</span></span>

<span data-ttu-id="2addc-118">Tutti gli URL trovati, il supporto di risorsa di registrazione, i metodi HTTP `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="2addc-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="2addc-119">Enumerare le versioni di pacchetto</span><span class="sxs-lookup"><span data-stu-id="2addc-119">Enumerate package versions</span></span>

<span data-ttu-id="2addc-120">Se il client conosce un ID pacchetto e desidera individuare quali versioni del pacchetto il pacchetto di origine è disponibile, il client può costruire un URL prevedibile per enumerare tutte le versioni di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2addc-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="2addc-121">Questo elenco deve essere un "elenco di directory" per l'API di contenuto del pacchetto riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="2addc-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="2addc-122">Questo elenco contiene entrambe le versioni di pacchetto elencate e non in elenco.</span><span class="sxs-lookup"><span data-stu-id="2addc-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="2addc-123">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="2addc-123">Request parameters</span></span>

<span data-ttu-id="2addc-124">nome</span><span class="sxs-lookup"><span data-stu-id="2addc-124">Name</span></span>     | <span data-ttu-id="2addc-125">In</span><span class="sxs-lookup"><span data-stu-id="2addc-125">In</span></span>     | <span data-ttu-id="2addc-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="2addc-126">Type</span></span>    | <span data-ttu-id="2addc-127">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2addc-127">Required</span></span> | <span data-ttu-id="2addc-128">Note</span><span class="sxs-lookup"><span data-stu-id="2addc-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="2addc-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="2addc-129">LOWER_ID</span></span> | <span data-ttu-id="2addc-130">URL</span><span class="sxs-lookup"><span data-stu-id="2addc-130">URL</span></span>    | <span data-ttu-id="2addc-131">stringa</span><span class="sxs-lookup"><span data-stu-id="2addc-131">string</span></span>  | <span data-ttu-id="2addc-132">sì</span><span class="sxs-lookup"><span data-stu-id="2addc-132">yes</span></span>      | <span data-ttu-id="2addc-133">L'ID del pacchetto, lettere minuscole</span><span class="sxs-lookup"><span data-stu-id="2addc-133">The package ID, lowercase</span></span>

<span data-ttu-id="2addc-134">Il `LOWER_ID` valore è l'ID del pacchetto desiderato minuscola usando le regole implementate da. Del NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metodo.</span><span class="sxs-lookup"><span data-stu-id="2addc-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="2addc-135">Risposta</span><span class="sxs-lookup"><span data-stu-id="2addc-135">Response</span></span>

<span data-ttu-id="2addc-136">Se l'origine del pacchetto non dispone di alcuna versione dell'ID pacchetto fornito, viene restituito un codice di 404 stato.</span><span class="sxs-lookup"><span data-stu-id="2addc-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="2addc-137">Se l'origine del pacchetto ha una o più versioni, viene restituito un codice di 200 stato.</span><span class="sxs-lookup"><span data-stu-id="2addc-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="2addc-138">Il corpo della risposta è un oggetto JSON con la seguente proprietà:</span><span class="sxs-lookup"><span data-stu-id="2addc-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="2addc-139">nome</span><span class="sxs-lookup"><span data-stu-id="2addc-139">Name</span></span>     | <span data-ttu-id="2addc-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="2addc-140">Type</span></span>             | <span data-ttu-id="2addc-141">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2addc-141">Required</span></span> | <span data-ttu-id="2addc-142">Note</span><span class="sxs-lookup"><span data-stu-id="2addc-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="2addc-143">versioni</span><span class="sxs-lookup"><span data-stu-id="2addc-143">versions</span></span> | <span data-ttu-id="2addc-144">Matrice di stringhe</span><span class="sxs-lookup"><span data-stu-id="2addc-144">array of strings</span></span> | <span data-ttu-id="2addc-145">sì</span><span class="sxs-lookup"><span data-stu-id="2addc-145">yes</span></span>      | <span data-ttu-id="2addc-146">L'ID pacchetto</span><span class="sxs-lookup"><span data-stu-id="2addc-146">The package IDs available</span></span>

<span data-ttu-id="2addc-147">Le stringhe di `versions` matrice tutti minuscola, [normalizzare le stringhe di versione NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="2addc-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="2addc-148">Le stringhe di versione non contengono i metadati di compilazione SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="2addc-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="2addc-149">Lo scopo è che le stringhe di versione trovate in questa matrice consente alla lettera per il `LOWER_VERSION` token, vedere i seguenti endpoint.</span><span class="sxs-lookup"><span data-stu-id="2addc-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="2addc-150">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="2addc-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="2addc-151">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="2addc-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="2addc-152">Scaricare il contenuto del pacchetto (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="2addc-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="2addc-153">Se il client conosce un ID pacchetto e una versione e desidera scaricare il contenuto del pacchetto, è necessario solo costruire l'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="2addc-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="2addc-154">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="2addc-154">Request parameters</span></span>

<span data-ttu-id="2addc-155">nome</span><span class="sxs-lookup"><span data-stu-id="2addc-155">Name</span></span>          | <span data-ttu-id="2addc-156">In</span><span class="sxs-lookup"><span data-stu-id="2addc-156">In</span></span>     | <span data-ttu-id="2addc-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="2addc-157">Type</span></span>   | <span data-ttu-id="2addc-158">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2addc-158">Required</span></span> | <span data-ttu-id="2addc-159">Note</span><span class="sxs-lookup"><span data-stu-id="2addc-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="2addc-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="2addc-160">LOWER_ID</span></span>      | <span data-ttu-id="2addc-161">URL</span><span class="sxs-lookup"><span data-stu-id="2addc-161">URL</span></span>    | <span data-ttu-id="2addc-162">stringa</span><span class="sxs-lookup"><span data-stu-id="2addc-162">string</span></span> | <span data-ttu-id="2addc-163">sì</span><span class="sxs-lookup"><span data-stu-id="2addc-163">yes</span></span>      | <span data-ttu-id="2addc-164">L'ID del pacchetto, lettere minuscole</span><span class="sxs-lookup"><span data-stu-id="2addc-164">The package ID, lowercase</span></span>
<span data-ttu-id="2addc-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="2addc-165">LOWER_VERSION</span></span> | <span data-ttu-id="2addc-166">URL</span><span class="sxs-lookup"><span data-stu-id="2addc-166">URL</span></span>    | <span data-ttu-id="2addc-167">stringa</span><span class="sxs-lookup"><span data-stu-id="2addc-167">string</span></span> | <span data-ttu-id="2addc-168">sì</span><span class="sxs-lookup"><span data-stu-id="2addc-168">yes</span></span>      | <span data-ttu-id="2addc-169">La versione del pacchetto, normalizzato e minuscola</span><span class="sxs-lookup"><span data-stu-id="2addc-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="2addc-170">Entrambi `LOWER_ID` e `LOWER_VERSION` sono minuscole usando le regole implementate da. Del NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metodo.</span><span class="sxs-lookup"><span data-stu-id="2addc-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="2addc-171">Il `LOWER_VERSION` è la versione del pacchetto desiderato normalizzata usando la versione NuGet [le regole di normalizzazione](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="2addc-171">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="2addc-172">Ciò significa che i metadati di compilazione consentiti dalla specifica SemVer 2.0.0 devono essere escluso in questo caso.</span><span class="sxs-lookup"><span data-stu-id="2addc-172">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="2addc-173">Corpo della risposta</span><span class="sxs-lookup"><span data-stu-id="2addc-173">Response body</span></span>

<span data-ttu-id="2addc-174">Se il pacchetto esiste nell'origine del pacchetto, viene restituito un codice di 200 stato.</span><span class="sxs-lookup"><span data-stu-id="2addc-174">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="2addc-175">Il corpo della risposta sarà il contenuto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2addc-175">The response body will be the package content itself.</span></span>

<span data-ttu-id="2addc-176">Se il pacchetto non esiste nell'origine pacchetto, viene restituito un codice di 404 stato.</span><span class="sxs-lookup"><span data-stu-id="2addc-176">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="2addc-177">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="2addc-177">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="2addc-178">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="2addc-178">Sample response</span></span>

<span data-ttu-id="2addc-179">Il flusso binario che è il .nupkg per 9.0.1 di newtonsoft. JSON.</span><span class="sxs-lookup"><span data-stu-id="2addc-179">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="2addc-180">Scaricare il manifesto di pacchetto (. nuspec)</span><span class="sxs-lookup"><span data-stu-id="2addc-180">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="2addc-181">Se il client conosce un ID pacchetto e una versione e desidera scaricare il manifesto di pacchetto, è necessario solo costruire l'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="2addc-181">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="2addc-182">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="2addc-182">Request parameters</span></span>

<span data-ttu-id="2addc-183">nome</span><span class="sxs-lookup"><span data-stu-id="2addc-183">Name</span></span>          | <span data-ttu-id="2addc-184">In</span><span class="sxs-lookup"><span data-stu-id="2addc-184">In</span></span>     | <span data-ttu-id="2addc-185">Tipo</span><span class="sxs-lookup"><span data-stu-id="2addc-185">Type</span></span>    | <span data-ttu-id="2addc-186">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2addc-186">Required</span></span> | <span data-ttu-id="2addc-187">Note</span><span class="sxs-lookup"><span data-stu-id="2addc-187">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="2addc-188">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="2addc-188">LOWER_ID</span></span>      | <span data-ttu-id="2addc-189">URL</span><span class="sxs-lookup"><span data-stu-id="2addc-189">URL</span></span>    | <span data-ttu-id="2addc-190">stringa</span><span class="sxs-lookup"><span data-stu-id="2addc-190">string</span></span>  | <span data-ttu-id="2addc-191">sì</span><span class="sxs-lookup"><span data-stu-id="2addc-191">yes</span></span>      | <span data-ttu-id="2addc-192">L'ID del pacchetto, lettere minuscole</span><span class="sxs-lookup"><span data-stu-id="2addc-192">The package ID, lowercase</span></span>
<span data-ttu-id="2addc-193">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="2addc-193">LOWER_VERSION</span></span> | <span data-ttu-id="2addc-194">URL</span><span class="sxs-lookup"><span data-stu-id="2addc-194">URL</span></span>    | <span data-ttu-id="2addc-195">numero intero</span><span class="sxs-lookup"><span data-stu-id="2addc-195">integer</span></span> | <span data-ttu-id="2addc-196">sì</span><span class="sxs-lookup"><span data-stu-id="2addc-196">yes</span></span>      | <span data-ttu-id="2addc-197">La versione del pacchetto, normalizzato e minuscola</span><span class="sxs-lookup"><span data-stu-id="2addc-197">The package version, normalized and lowercased</span></span>

<span data-ttu-id="2addc-198">Entrambi `LOWER_ID` e `LOWER_VERSION` sono minuscole usando le regole implementate da. Del NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metodo.</span><span class="sxs-lookup"><span data-stu-id="2addc-198">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="2addc-199">Il `LOWER_VERSION` è la versione del pacchetto desiderato normalizzata usando la versione NuGet [le regole di normalizzazione](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="2addc-199">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="2addc-200">Ciò significa che i metadati di compilazione consentiti dalla specifica SemVer 2.0.0 devono essere escluso in questo caso.</span><span class="sxs-lookup"><span data-stu-id="2addc-200">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="2addc-201">Corpo della risposta</span><span class="sxs-lookup"><span data-stu-id="2addc-201">Response body</span></span>

<span data-ttu-id="2addc-202">Se il pacchetto esiste nell'origine del pacchetto, viene restituito un codice di 200 stato.</span><span class="sxs-lookup"><span data-stu-id="2addc-202">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="2addc-203">Il corpo della risposta sarà il manifesto del pacchetto, ovvero il. nuspec nel .nupkg corrispondente.</span><span class="sxs-lookup"><span data-stu-id="2addc-203">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="2addc-204">I. nuspec è un documento XML.</span><span class="sxs-lookup"><span data-stu-id="2addc-204">The .nuspec is an XML document.</span></span>

<span data-ttu-id="2addc-205">Se il pacchetto non esiste nell'origine pacchetto, viene restituito un codice di 404 stato.</span><span class="sxs-lookup"><span data-stu-id="2addc-205">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="2addc-206">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="2addc-206">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="2addc-207">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="2addc-207">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
