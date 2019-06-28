---
title: Contenuto del pacchetto, NuGet API
description: L'indirizzo di base del pacchetto è una semplice interfaccia per recuperare il pacchetto stesso.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2f0f93e0cee78ea03cbd53194cdc2a10871fd7e1
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426757"
---
# <a name="package-content"></a><span data-ttu-id="dca74-103">Contenuto del pacchetto</span><span class="sxs-lookup"><span data-stu-id="dca74-103">Package Content</span></span>

<span data-ttu-id="dca74-104">È possibile generare un URL per recuperare il contenuto del pacchetto arbitrario (file nupkg) usando l'API di V3.</span><span class="sxs-lookup"><span data-stu-id="dca74-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="dca74-105">La risorsa usata per recuperare il contenuto del pacchetto è il `PackageBaseAddress` trovare la risorsa nella [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="dca74-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="dca74-106">Questa risorsa consente anche l'individuazione di tutte le versioni di un pacchetto, elencati o non in elenco.</span><span class="sxs-lookup"><span data-stu-id="dca74-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="dca74-107">Questa risorsa è noto come entrambi il "pacchetto base address" o il contenitore"flat".</span><span class="sxs-lookup"><span data-stu-id="dca74-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="dca74-108">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="dca74-108">Versioning</span></span>

<span data-ttu-id="dca74-109">Nell'esempio `@type` valore viene usato:</span><span class="sxs-lookup"><span data-stu-id="dca74-109">The following `@type` value is used:</span></span>

<span data-ttu-id="dca74-110">Valore di@type</span><span class="sxs-lookup"><span data-stu-id="dca74-110">@type value</span></span>              | <span data-ttu-id="dca74-111">Note</span><span class="sxs-lookup"><span data-stu-id="dca74-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="dca74-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="dca74-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="dca74-113">La versione iniziale</span><span class="sxs-lookup"><span data-stu-id="dca74-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="dca74-114">URL di base</span><span class="sxs-lookup"><span data-stu-id="dca74-114">Base URL</span></span>

<span data-ttu-id="dca74-115">L'URL di base per le API seguente è il valore della `@id` proprietà associato alla risorsa menzionati in precedenza `@type` valore.</span><span class="sxs-lookup"><span data-stu-id="dca74-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="dca74-116">Nel documento seguente, il segnaposto URL di base `{@id}` verrà utilizzato.</span><span class="sxs-lookup"><span data-stu-id="dca74-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="dca74-117">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="dca74-117">HTTP methods</span></span>

<span data-ttu-id="dca74-118">Tutti gli URL disponibili il supporto di risorse di registrazione i metodi HTTP `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="dca74-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="dca74-119">Enumera le versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="dca74-119">Enumerate package versions</span></span>

<span data-ttu-id="dca74-120">Se il client riconosce un ID pacchetto e vuole scoprire quali versioni dei pacchetti il pacchetto di origine è disponibile, il client può costruire un URL prevedibile per enumerare tutte le versioni del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="dca74-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="dca74-121">Questo elenco deve essere un "elenco di directory" per l'API di pacchetto contenuto indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="dca74-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="dca74-122">Questo elenco contiene entrambe le versioni dei pacchetti elencati e non in elenco.</span><span class="sxs-lookup"><span data-stu-id="dca74-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="dca74-123">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="dca74-123">Request parameters</span></span>

<span data-ttu-id="dca74-124">Nome</span><span class="sxs-lookup"><span data-stu-id="dca74-124">Name</span></span>     | <span data-ttu-id="dca74-125">In</span><span class="sxs-lookup"><span data-stu-id="dca74-125">In</span></span>     | <span data-ttu-id="dca74-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="dca74-126">Type</span></span>    | <span data-ttu-id="dca74-127">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="dca74-127">Required</span></span> | <span data-ttu-id="dca74-128">Note</span><span class="sxs-lookup"><span data-stu-id="dca74-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="dca74-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="dca74-129">LOWER_ID</span></span> | <span data-ttu-id="dca74-130">URL</span><span class="sxs-lookup"><span data-stu-id="dca74-130">URL</span></span>    | <span data-ttu-id="dca74-131">string</span><span class="sxs-lookup"><span data-stu-id="dca74-131">string</span></span>  | <span data-ttu-id="dca74-132">sì</span><span class="sxs-lookup"><span data-stu-id="dca74-132">yes</span></span>      | <span data-ttu-id="dca74-133">L'ID del pacchetto, lettere minuscole</span><span class="sxs-lookup"><span data-stu-id="dca74-133">The package ID, lowercase</span></span>

<span data-ttu-id="dca74-134">Il `LOWER_ID` valore è l'ID pacchetto desiderato minuscola usando le regole implementate da. Di NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) (metodo).</span><span class="sxs-lookup"><span data-stu-id="dca74-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="dca74-135">Risposta</span><span class="sxs-lookup"><span data-stu-id="dca74-135">Response</span></span>

<span data-ttu-id="dca74-136">Se l'origine del pacchetto non ci è versioni dell'ID del pacchetto fornito, viene restituito un codice di 404 stato.</span><span class="sxs-lookup"><span data-stu-id="dca74-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="dca74-137">Se l'origine del pacchetto ha una o più versioni, viene restituito un codice di 200 stato.</span><span class="sxs-lookup"><span data-stu-id="dca74-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="dca74-138">Il corpo della risposta è un oggetto JSON con la proprietà seguente:</span><span class="sxs-lookup"><span data-stu-id="dca74-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="dca74-139">Nome</span><span class="sxs-lookup"><span data-stu-id="dca74-139">Name</span></span>     | <span data-ttu-id="dca74-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="dca74-140">Type</span></span>             | <span data-ttu-id="dca74-141">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="dca74-141">Required</span></span> | <span data-ttu-id="dca74-142">Note</span><span class="sxs-lookup"><span data-stu-id="dca74-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="dca74-143">versioni</span><span class="sxs-lookup"><span data-stu-id="dca74-143">versions</span></span> | <span data-ttu-id="dca74-144">Matrice di stringhe</span><span class="sxs-lookup"><span data-stu-id="dca74-144">array of strings</span></span> | <span data-ttu-id="dca74-145">sì</span><span class="sxs-lookup"><span data-stu-id="dca74-145">yes</span></span>      | <span data-ttu-id="dca74-146">L'ID pacchetto</span><span class="sxs-lookup"><span data-stu-id="dca74-146">The package IDs available</span></span>

<span data-ttu-id="dca74-147">Le stringhe nel `versions` matrice tutte minuscole, [normalizzato le stringhe di versione di NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="dca74-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="dca74-148">Le stringhe di versione non contengono i metadati di compilazione di SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="dca74-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="dca74-149">L'intento è che le stringhe di versione disponibili in questa matrice possono essere usate come verbatim per il `LOWER_VERSION` token trovato nell'endpoint seguenti.</span><span class="sxs-lookup"><span data-stu-id="dca74-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="dca74-150">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="dca74-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="dca74-151">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="dca74-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="dca74-152">Scarica contenuto pacchetto (con estensione nupkg)</span><span class="sxs-lookup"><span data-stu-id="dca74-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="dca74-153">Se il client sa un ID pacchetto e versione e si vuole scaricare il contenuto del pacchetto, è sufficiente creare l'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="dca74-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="dca74-154">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="dca74-154">Request parameters</span></span>

<span data-ttu-id="dca74-155">Nome</span><span class="sxs-lookup"><span data-stu-id="dca74-155">Name</span></span>          | <span data-ttu-id="dca74-156">In</span><span class="sxs-lookup"><span data-stu-id="dca74-156">In</span></span>     | <span data-ttu-id="dca74-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="dca74-157">Type</span></span>   | <span data-ttu-id="dca74-158">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="dca74-158">Required</span></span> | <span data-ttu-id="dca74-159">Note</span><span class="sxs-lookup"><span data-stu-id="dca74-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="dca74-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="dca74-160">LOWER_ID</span></span>      | <span data-ttu-id="dca74-161">URL</span><span class="sxs-lookup"><span data-stu-id="dca74-161">URL</span></span>    | <span data-ttu-id="dca74-162">string</span><span class="sxs-lookup"><span data-stu-id="dca74-162">string</span></span> | <span data-ttu-id="dca74-163">sì</span><span class="sxs-lookup"><span data-stu-id="dca74-163">yes</span></span>      | <span data-ttu-id="dca74-164">L'ID del pacchetto, lettere minuscole</span><span class="sxs-lookup"><span data-stu-id="dca74-164">The package ID, lowercase</span></span>
<span data-ttu-id="dca74-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="dca74-165">LOWER_VERSION</span></span> | <span data-ttu-id="dca74-166">URL</span><span class="sxs-lookup"><span data-stu-id="dca74-166">URL</span></span>    | <span data-ttu-id="dca74-167">string</span><span class="sxs-lookup"><span data-stu-id="dca74-167">string</span></span> | <span data-ttu-id="dca74-168">sì</span><span class="sxs-lookup"><span data-stu-id="dca74-168">yes</span></span>      | <span data-ttu-id="dca74-169">La versione del pacchetto, normalizzate e minuscola</span><span class="sxs-lookup"><span data-stu-id="dca74-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="dca74-170">Entrambe `LOWER_ID` e `LOWER_VERSION` sono minuscole usando le regole implementate da. Di NET [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="dca74-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="dca74-171">ProcessOnStatus.</span><span class="sxs-lookup"><span data-stu-id="dca74-171">method.</span></span>

<span data-ttu-id="dca74-172">Il `LOWER_VERSION` è la versione del pacchetto desiderato normalizzata mediante una versione di NuGet [regole di normalizzazione](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="dca74-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="dca74-173">Ciò significa che i metadati di compilazione che sono consentito dalla specifica di SemVer 2.0.0 devono essere escluse in questo caso.</span><span class="sxs-lookup"><span data-stu-id="dca74-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="dca74-174">Corpo della risposta</span><span class="sxs-lookup"><span data-stu-id="dca74-174">Response body</span></span>

<span data-ttu-id="dca74-175">Se il pacchetto esiste nell'origine del pacchetto, viene restituito un codice di 200 stato.</span><span class="sxs-lookup"><span data-stu-id="dca74-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="dca74-176">Il corpo della risposta sarà contenuto il pacchetto stesso.</span><span class="sxs-lookup"><span data-stu-id="dca74-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="dca74-177">Se il pacchetto non esiste nell'origine pacchetto, viene restituito un codice di 404 stato.</span><span class="sxs-lookup"><span data-stu-id="dca74-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="dca74-178">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="dca74-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="dca74-179">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="dca74-179">Sample response</span></span>

<span data-ttu-id="dca74-180">Il flusso di dati binari è il pacchetto. nupkg per newtonsoft. JSON 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="dca74-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="dca74-181">Scaricare il manifesto di pacchetto (con estensione nuspec)</span><span class="sxs-lookup"><span data-stu-id="dca74-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="dca74-182">Se il client sa un ID pacchetto e versione e si vuole scaricare il manifesto del pacchetto, è sufficiente creare l'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="dca74-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="dca74-183">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="dca74-183">Request parameters</span></span>

<span data-ttu-id="dca74-184">Nome</span><span class="sxs-lookup"><span data-stu-id="dca74-184">Name</span></span>          | <span data-ttu-id="dca74-185">In</span><span class="sxs-lookup"><span data-stu-id="dca74-185">In</span></span>     | <span data-ttu-id="dca74-186">Tipo</span><span class="sxs-lookup"><span data-stu-id="dca74-186">Type</span></span>   | <span data-ttu-id="dca74-187">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="dca74-187">Required</span></span> | <span data-ttu-id="dca74-188">Note</span><span class="sxs-lookup"><span data-stu-id="dca74-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="dca74-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="dca74-189">LOWER_ID</span></span>      | <span data-ttu-id="dca74-190">URL</span><span class="sxs-lookup"><span data-stu-id="dca74-190">URL</span></span>    | <span data-ttu-id="dca74-191">string</span><span class="sxs-lookup"><span data-stu-id="dca74-191">string</span></span> | <span data-ttu-id="dca74-192">sì</span><span class="sxs-lookup"><span data-stu-id="dca74-192">yes</span></span>      | <span data-ttu-id="dca74-193">L'ID del pacchetto, lettere minuscole</span><span class="sxs-lookup"><span data-stu-id="dca74-193">The package ID, lowercase</span></span>
<span data-ttu-id="dca74-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="dca74-194">LOWER_VERSION</span></span> | <span data-ttu-id="dca74-195">URL</span><span class="sxs-lookup"><span data-stu-id="dca74-195">URL</span></span>    | <span data-ttu-id="dca74-196">string</span><span class="sxs-lookup"><span data-stu-id="dca74-196">string</span></span> | <span data-ttu-id="dca74-197">sì</span><span class="sxs-lookup"><span data-stu-id="dca74-197">yes</span></span>      | <span data-ttu-id="dca74-198">La versione del pacchetto, normalizzate e minuscola</span><span class="sxs-lookup"><span data-stu-id="dca74-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="dca74-199">Entrambe `LOWER_ID` e `LOWER_VERSION` sono minuscole usando le regole implementate da. Di NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) (metodo).</span><span class="sxs-lookup"><span data-stu-id="dca74-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="dca74-200">Il `LOWER_VERSION` è la versione del pacchetto desiderato normalizzata mediante una versione di NuGet [regole di normalizzazione](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="dca74-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="dca74-201">Ciò significa che i metadati di compilazione che sono consentito dalla specifica di SemVer 2.0.0 devono essere escluse in questo caso.</span><span class="sxs-lookup"><span data-stu-id="dca74-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="dca74-202">Corpo della risposta</span><span class="sxs-lookup"><span data-stu-id="dca74-202">Response body</span></span>

<span data-ttu-id="dca74-203">Se il pacchetto esiste nell'origine del pacchetto, viene restituito un codice di 200 stato.</span><span class="sxs-lookup"><span data-stu-id="dca74-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="dca74-204">Il corpo della risposta sarà il manifesto di pacchetto, ovvero il file con estensione nuspec contenuti nel pacchetto. nupkg corrispondente.</span><span class="sxs-lookup"><span data-stu-id="dca74-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="dca74-205">Il file con estensione nuspec è un documento XML.</span><span class="sxs-lookup"><span data-stu-id="dca74-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="dca74-206">Se il pacchetto non esiste nell'origine pacchetto, viene restituito un codice di 404 stato.</span><span class="sxs-lookup"><span data-stu-id="dca74-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="dca74-207">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="dca74-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="dca74-208">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="dca74-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
