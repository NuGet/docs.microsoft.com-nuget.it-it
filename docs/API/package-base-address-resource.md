---
title: Pacchetto di contenuto, NuGet API | Documenti Microsoft
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
description: "L'indirizzo di base del pacchetto è un'interfaccia semplice per recuperare il pacchetto stesso."
keywords: NuGet flat contenitore, l'indirizzo di base del pacchetto NuGet, NuGet nupkg API, versioni del pacchetto NuGet API, API NuGet pacchetti non in elenco, API NuGet download nuspec
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c2e631dc0bba95ac849430d77142f27ef591f741
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2018
---
# <a name="package-content"></a><span data-ttu-id="87f35-104">Contenuto del pacchetto</span><span class="sxs-lookup"><span data-stu-id="87f35-104">Package Content</span></span>

<span data-ttu-id="87f35-105">È possibile generare un URL per recuperare il contenuto del pacchetto non autorizzato (il file .nupkg) tramite l'API V3.</span><span class="sxs-lookup"><span data-stu-id="87f35-105">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="87f35-106">La risorsa utilizzata per il recupero di contenuto del pacchetto è il `PackageBaseAddress` risorse, vedere il [indice servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="87f35-106">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="87f35-107">Questa risorsa consente inoltre l'individuazione di tutte le versioni di un pacchetto, elencato o non in elenco.</span><span class="sxs-lookup"><span data-stu-id="87f35-107">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="87f35-108">Questa risorsa è noto come un "pacchetto indirizzo di base" o "container flat".</span><span class="sxs-lookup"><span data-stu-id="87f35-108">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="87f35-109">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="87f35-109">Versioning</span></span>

<span data-ttu-id="87f35-110">Le operazioni seguenti `@type` valore viene utilizzato:</span><span class="sxs-lookup"><span data-stu-id="87f35-110">The following `@type` value is used:</span></span>

<span data-ttu-id="87f35-111">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="87f35-111">@type value</span></span>              | <span data-ttu-id="87f35-112">Note</span><span class="sxs-lookup"><span data-stu-id="87f35-112">Notes</span></span>
------------------------ | -----
<span data-ttu-id="87f35-113">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="87f35-113">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="87f35-114">La versione iniziale</span><span class="sxs-lookup"><span data-stu-id="87f35-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="87f35-115">URL di base</span><span class="sxs-lookup"><span data-stu-id="87f35-115">Base URL</span></span>

<span data-ttu-id="87f35-116">L'URL di base per le API seguente è il valore di `@id` proprietà associato alla risorsa menzionati in precedenza `@type` valore.</span><span class="sxs-lookup"><span data-stu-id="87f35-116">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="87f35-117">Nel documento seguente, il segnaposto URL di base `{@id}` verrà utilizzato.</span><span class="sxs-lookup"><span data-stu-id="87f35-117">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="87f35-118">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="87f35-118">HTTP methods</span></span>

<span data-ttu-id="87f35-119">Tutti gli URL trovati, il supporto di risorsa di registrazione, i metodi HTTP `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="87f35-119">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="87f35-120">Enumerare le versioni di pacchetto</span><span class="sxs-lookup"><span data-stu-id="87f35-120">Enumerate package versions</span></span>

<span data-ttu-id="87f35-121">Se il client conosce un ID pacchetto e desidera individuare quali versioni del pacchetto il pacchetto di origine è disponibile, il client può costruire un URL prevedibile per enumerare tutte le versioni di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="87f35-121">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="87f35-122">Questo elenco deve essere un "elenco di directory" per l'API di contenuto del pacchetto riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="87f35-122">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="87f35-123">Questo elenco contiene entrambe le versioni di pacchetto elencate e non in elenco.</span><span class="sxs-lookup"><span data-stu-id="87f35-123">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="87f35-124">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="87f35-124">Request parameters</span></span>

<span data-ttu-id="87f35-125">nome</span><span class="sxs-lookup"><span data-stu-id="87f35-125">Name</span></span>     | <span data-ttu-id="87f35-126">In</span><span class="sxs-lookup"><span data-stu-id="87f35-126">In</span></span>     | <span data-ttu-id="87f35-127">Tipo</span><span class="sxs-lookup"><span data-stu-id="87f35-127">Type</span></span>    | <span data-ttu-id="87f35-128">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="87f35-128">Required</span></span> | <span data-ttu-id="87f35-129">Note</span><span class="sxs-lookup"><span data-stu-id="87f35-129">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="87f35-130">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="87f35-130">LOWER_ID</span></span> | <span data-ttu-id="87f35-131">URL</span><span class="sxs-lookup"><span data-stu-id="87f35-131">URL</span></span>    | <span data-ttu-id="87f35-132">stringa</span><span class="sxs-lookup"><span data-stu-id="87f35-132">string</span></span>  | <span data-ttu-id="87f35-133">sì</span><span class="sxs-lookup"><span data-stu-id="87f35-133">yes</span></span>      | <span data-ttu-id="87f35-134">L'ID del pacchetto, lettere minuscole</span><span class="sxs-lookup"><span data-stu-id="87f35-134">The package ID, lowercase</span></span>

<span data-ttu-id="87f35-135">Il `LOWER_ID` valore è l'ID del pacchetto desiderato minuscola usando le regole implementate da. Del NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metodo.</span><span class="sxs-lookup"><span data-stu-id="87f35-135">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="87f35-136">Risposta</span><span class="sxs-lookup"><span data-stu-id="87f35-136">Response</span></span>

<span data-ttu-id="87f35-137">Se l'origine del pacchetto non dispone di alcuna versione dell'ID pacchetto fornito, viene restituito un codice di 404 stato.</span><span class="sxs-lookup"><span data-stu-id="87f35-137">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="87f35-138">Se l'origine del pacchetto ha una o più versioni, viene restituito un codice di 200 stato.</span><span class="sxs-lookup"><span data-stu-id="87f35-138">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="87f35-139">Il corpo della risposta è un oggetto JSON con la seguente proprietà:</span><span class="sxs-lookup"><span data-stu-id="87f35-139">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="87f35-140">nome</span><span class="sxs-lookup"><span data-stu-id="87f35-140">Name</span></span>     | <span data-ttu-id="87f35-141">Tipo</span><span class="sxs-lookup"><span data-stu-id="87f35-141">Type</span></span>             | <span data-ttu-id="87f35-142">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="87f35-142">Required</span></span> | <span data-ttu-id="87f35-143">Note</span><span class="sxs-lookup"><span data-stu-id="87f35-143">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="87f35-144">versioni</span><span class="sxs-lookup"><span data-stu-id="87f35-144">versions</span></span> | <span data-ttu-id="87f35-145">Matrice di stringhe</span><span class="sxs-lookup"><span data-stu-id="87f35-145">array of strings</span></span> | <span data-ttu-id="87f35-146">sì</span><span class="sxs-lookup"><span data-stu-id="87f35-146">yes</span></span>      | <span data-ttu-id="87f35-147">L'ID pacchetto</span><span class="sxs-lookup"><span data-stu-id="87f35-147">The package IDs available</span></span>

<span data-ttu-id="87f35-148">Le stringhe di `versions` matrice tutti minuscola, [normalizzare le stringhe di versione NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="87f35-148">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="87f35-149">Le stringhe di versione non contengono i metadati di compilazione SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="87f35-149">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="87f35-150">Lo scopo è che le stringhe di versione trovate in questa matrice consente alla lettera per il `LOWER_VERSION` token, vedere i seguenti endpoint.</span><span class="sxs-lookup"><span data-stu-id="87f35-150">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="87f35-151">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="87f35-151">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="87f35-152">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="87f35-152">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="87f35-153">Scaricare il contenuto del pacchetto (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="87f35-153">Download package content (.nupkg)</span></span>

<span data-ttu-id="87f35-154">Se il client conosce un ID pacchetto e una versione e desidera scaricare il contenuto del pacchetto, è necessario solo costruire l'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="87f35-154">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="87f35-155">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="87f35-155">Request parameters</span></span>

<span data-ttu-id="87f35-156">nome</span><span class="sxs-lookup"><span data-stu-id="87f35-156">Name</span></span>          | <span data-ttu-id="87f35-157">In</span><span class="sxs-lookup"><span data-stu-id="87f35-157">In</span></span>     | <span data-ttu-id="87f35-158">Tipo</span><span class="sxs-lookup"><span data-stu-id="87f35-158">Type</span></span>   | <span data-ttu-id="87f35-159">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="87f35-159">Required</span></span> | <span data-ttu-id="87f35-160">Note</span><span class="sxs-lookup"><span data-stu-id="87f35-160">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="87f35-161">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="87f35-161">LOWER_ID</span></span>      | <span data-ttu-id="87f35-162">URL</span><span class="sxs-lookup"><span data-stu-id="87f35-162">URL</span></span>    | <span data-ttu-id="87f35-163">stringa</span><span class="sxs-lookup"><span data-stu-id="87f35-163">string</span></span> | <span data-ttu-id="87f35-164">sì</span><span class="sxs-lookup"><span data-stu-id="87f35-164">yes</span></span>      | <span data-ttu-id="87f35-165">L'ID del pacchetto, lettere minuscole</span><span class="sxs-lookup"><span data-stu-id="87f35-165">The package ID, lowercase</span></span>
<span data-ttu-id="87f35-166">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="87f35-166">LOWER_VERSION</span></span> | <span data-ttu-id="87f35-167">URL</span><span class="sxs-lookup"><span data-stu-id="87f35-167">URL</span></span>    | <span data-ttu-id="87f35-168">stringa</span><span class="sxs-lookup"><span data-stu-id="87f35-168">string</span></span> | <span data-ttu-id="87f35-169">sì</span><span class="sxs-lookup"><span data-stu-id="87f35-169">yes</span></span>      | <span data-ttu-id="87f35-170">La versione del pacchetto, normalizzato e minuscola</span><span class="sxs-lookup"><span data-stu-id="87f35-170">The package version, normalized and lowercased</span></span>

<span data-ttu-id="87f35-171">Entrambi `LOWER_ID` e `LOWER_VERSION` sono minuscole usando le regole implementate da. Del NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metodo.</span><span class="sxs-lookup"><span data-stu-id="87f35-171">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="87f35-172">Il `LOWER_VERSION` è la versione del pacchetto desiderato normalizzata usando la versione NuGet [le regole di normalizzazione](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="87f35-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="87f35-173">Ciò significa che i metadati di compilazione consentiti dalla specifica SemVer 2.0.0 devono essere escluso in questo caso.</span><span class="sxs-lookup"><span data-stu-id="87f35-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="87f35-174">Corpo della risposta</span><span class="sxs-lookup"><span data-stu-id="87f35-174">Response body</span></span>

<span data-ttu-id="87f35-175">Se il pacchetto esiste nell'origine del pacchetto, viene restituito un codice di 200 stato.</span><span class="sxs-lookup"><span data-stu-id="87f35-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="87f35-176">Il corpo della risposta sarà il contenuto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="87f35-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="87f35-177">Se il pacchetto non esiste nell'origine pacchetto, viene restituito un codice di 404 stato.</span><span class="sxs-lookup"><span data-stu-id="87f35-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="87f35-178">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="87f35-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="87f35-179">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="87f35-179">Sample response</span></span>

<span data-ttu-id="87f35-180">Il flusso binario che è il .nupkg per 9.0.1 di newtonsoft. JSON.</span><span class="sxs-lookup"><span data-stu-id="87f35-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="87f35-181">Scaricare il manifesto di pacchetto (. nuspec)</span><span class="sxs-lookup"><span data-stu-id="87f35-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="87f35-182">Se il client conosce un ID pacchetto e una versione e desidera scaricare il manifesto di pacchetto, è necessario solo costruire l'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="87f35-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="87f35-183">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="87f35-183">Request parameters</span></span>

<span data-ttu-id="87f35-184">nome</span><span class="sxs-lookup"><span data-stu-id="87f35-184">Name</span></span>          | <span data-ttu-id="87f35-185">In</span><span class="sxs-lookup"><span data-stu-id="87f35-185">In</span></span>     | <span data-ttu-id="87f35-186">Tipo</span><span class="sxs-lookup"><span data-stu-id="87f35-186">Type</span></span>    | <span data-ttu-id="87f35-187">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="87f35-187">Required</span></span> | <span data-ttu-id="87f35-188">Note</span><span class="sxs-lookup"><span data-stu-id="87f35-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="87f35-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="87f35-189">LOWER_ID</span></span>      | <span data-ttu-id="87f35-190">URL</span><span class="sxs-lookup"><span data-stu-id="87f35-190">URL</span></span>    | <span data-ttu-id="87f35-191">stringa</span><span class="sxs-lookup"><span data-stu-id="87f35-191">string</span></span>  | <span data-ttu-id="87f35-192">sì</span><span class="sxs-lookup"><span data-stu-id="87f35-192">yes</span></span>      | <span data-ttu-id="87f35-193">L'ID del pacchetto, lettere minuscole</span><span class="sxs-lookup"><span data-stu-id="87f35-193">The package ID, lowercase</span></span>
<span data-ttu-id="87f35-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="87f35-194">LOWER_VERSION</span></span> | <span data-ttu-id="87f35-195">URL</span><span class="sxs-lookup"><span data-stu-id="87f35-195">URL</span></span>    | <span data-ttu-id="87f35-196">numero intero</span><span class="sxs-lookup"><span data-stu-id="87f35-196">integer</span></span> | <span data-ttu-id="87f35-197">sì</span><span class="sxs-lookup"><span data-stu-id="87f35-197">yes</span></span>      | <span data-ttu-id="87f35-198">La versione del pacchetto, normalizzato e minuscola</span><span class="sxs-lookup"><span data-stu-id="87f35-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="87f35-199">Entrambi `LOWER_ID` e `LOWER_VERSION` sono minuscole usando le regole implementate da. Del NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metodo.</span><span class="sxs-lookup"><span data-stu-id="87f35-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="87f35-200">Il `LOWER_VERSION` è la versione del pacchetto desiderato normalizzata usando la versione NuGet [le regole di normalizzazione](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="87f35-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="87f35-201">Ciò significa che i metadati di compilazione consentiti dalla specifica SemVer 2.0.0 devono essere escluso in questo caso.</span><span class="sxs-lookup"><span data-stu-id="87f35-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="87f35-202">Corpo della risposta</span><span class="sxs-lookup"><span data-stu-id="87f35-202">Response body</span></span>

<span data-ttu-id="87f35-203">Se il pacchetto esiste nell'origine del pacchetto, viene restituito un codice di 200 stato.</span><span class="sxs-lookup"><span data-stu-id="87f35-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="87f35-204">Il corpo della risposta sarà il manifesto del pacchetto, ovvero il. nuspec nel .nupkg corrispondente.</span><span class="sxs-lookup"><span data-stu-id="87f35-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="87f35-205">I. nuspec è un documento XML.</span><span class="sxs-lookup"><span data-stu-id="87f35-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="87f35-206">Se il pacchetto non esiste nell'origine pacchetto, viene restituito un codice di 404 stato.</span><span class="sxs-lookup"><span data-stu-id="87f35-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="87f35-207">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="87f35-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="87f35-208">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="87f35-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
