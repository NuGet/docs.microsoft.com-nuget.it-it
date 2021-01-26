---
title: Push ed eliminazione, API NuGet
description: Il servizio Publish consente ai client di pubblicare nuovi pacchetti ed eliminare dall'elenco o eliminare i pacchetti esistenti.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773919"
---
# <a name="push-and-delete"></a><span data-ttu-id="aaaf1-103">Push ed eliminazione</span><span class="sxs-lookup"><span data-stu-id="aaaf1-103">Push and Delete</span></span>

<span data-ttu-id="aaaf1-104">È possibile eseguire il push, eliminare o rimuovere l'elenco in base all'implementazione del server e rielencare i pacchetti usando l'API NuGet V3.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="aaaf1-105">Queste operazioni sono basate sulla `PackagePublish` risorsa presente nell' [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="aaaf1-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="aaaf1-106">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="aaaf1-106">Versioning</span></span>

<span data-ttu-id="aaaf1-107">`@type`Viene utilizzato il valore seguente:</span><span class="sxs-lookup"><span data-stu-id="aaaf1-107">The following `@type` value is used:</span></span>

<span data-ttu-id="aaaf1-108">Valore della proprietà @type</span><span class="sxs-lookup"><span data-stu-id="aaaf1-108">@type value</span></span>          | <span data-ttu-id="aaaf1-109">Note</span><span class="sxs-lookup"><span data-stu-id="aaaf1-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="aaaf1-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="aaaf1-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="aaaf1-111">Versione iniziale</span><span class="sxs-lookup"><span data-stu-id="aaaf1-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="aaaf1-112">URL di base</span><span class="sxs-lookup"><span data-stu-id="aaaf1-112">Base URL</span></span>

<span data-ttu-id="aaaf1-113">L'URL di base per le API seguenti è il valore della `@id` proprietà della `PackagePublish/2.0.0` risorsa nell' [indice del servizio](service-index.md)dell'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="aaaf1-114">Per la documentazione riportata di seguito, viene usato l'URL di NuGet. org.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="aaaf1-115">Considerare `https://www.nuget.org/api/v2/package` come un segnaposto per il `@id` valore trovato nell'indice del servizio.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="aaaf1-116">Si noti che questo URL punta alla stessa posizione dell'endpoint di push V2 legacy poiché il protocollo è lo stesso.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="aaaf1-117">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="aaaf1-117">HTTP methods</span></span>

<span data-ttu-id="aaaf1-118">I `PUT` `POST` metodi, e `DELETE` http sono supportati da questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="aaaf1-119">Per i metodi supportati in ogni endpoint, vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="aaaf1-120">Eseguire il push di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="aaaf1-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="aaaf1-121">nuget.org presenta [requisiti aggiuntivi](NuGet-Protocols.md) per l'interazione con l'endpoint di push.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="aaaf1-122">nuget.org supporta il push di nuovi pacchetti usando l'API seguente.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="aaaf1-123">Se il pacchetto con l'ID e la versione specificati esiste già, nuget.org rifiuterà il push.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="aaaf1-124">Altre origini di pacchetti possono supportare la sostituzione di un pacchetto esistente.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="aaaf1-125">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="aaaf1-125">Request parameters</span></span>

<span data-ttu-id="aaaf1-126">Nome</span><span class="sxs-lookup"><span data-stu-id="aaaf1-126">Name</span></span>           | <span data-ttu-id="aaaf1-127">In</span><span class="sxs-lookup"><span data-stu-id="aaaf1-127">In</span></span>     | <span data-ttu-id="aaaf1-128">Type</span><span class="sxs-lookup"><span data-stu-id="aaaf1-128">Type</span></span>   | <span data-ttu-id="aaaf1-129">Necessario</span><span class="sxs-lookup"><span data-stu-id="aaaf1-129">Required</span></span> | <span data-ttu-id="aaaf1-130">Note</span><span class="sxs-lookup"><span data-stu-id="aaaf1-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="aaaf1-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="aaaf1-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="aaaf1-132">Intestazione</span><span class="sxs-lookup"><span data-stu-id="aaaf1-132">Header</span></span> | <span data-ttu-id="aaaf1-133">string</span><span class="sxs-lookup"><span data-stu-id="aaaf1-133">string</span></span> | <span data-ttu-id="aaaf1-134">sì</span><span class="sxs-lookup"><span data-stu-id="aaaf1-134">yes</span></span>      | <span data-ttu-id="aaaf1-135">Ad esempio: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="aaaf1-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="aaaf1-136">La chiave API è una stringa opaca ottenuta dall'origine del pacchetto dall'utente e configurata nel client.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="aaaf1-137">Non è richiesto alcun formato stringa particolare, ma la lunghezza della chiave API non deve superare una dimensione ragionevole per i valori dell'intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="aaaf1-138">Testo della richiesta</span><span class="sxs-lookup"><span data-stu-id="aaaf1-138">Request body</span></span>

<span data-ttu-id="aaaf1-139">Il corpo della richiesta deve avere il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="aaaf1-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="aaaf1-140">Dati in formato multipart</span><span class="sxs-lookup"><span data-stu-id="aaaf1-140">Multipart form data</span></span>

<span data-ttu-id="aaaf1-141">L'intestazione della richiesta `Content-Type` è `multipart/form-data` e il primo elemento nel corpo della richiesta è costituito dai byte non elaborati del nupkg di cui viene eseguito il push.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="aaaf1-142">Gli elementi successivi nel corpo multipart vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="aaaf1-143">Il nome del file o qualsiasi altra intestazione degli elementi multipart viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="aaaf1-144">Risposta</span><span class="sxs-lookup"><span data-stu-id="aaaf1-144">Response</span></span>

<span data-ttu-id="aaaf1-145">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="aaaf1-145">Status Code</span></span> | <span data-ttu-id="aaaf1-146">Significato</span><span class="sxs-lookup"><span data-stu-id="aaaf1-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="aaaf1-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="aaaf1-147">201, 202</span></span>    | <span data-ttu-id="aaaf1-148">Push del pacchetto completato</span><span class="sxs-lookup"><span data-stu-id="aaaf1-148">The package was successfully pushed</span></span>
<span data-ttu-id="aaaf1-149">400</span><span class="sxs-lookup"><span data-stu-id="aaaf1-149">400</span></span>         | <span data-ttu-id="aaaf1-150">Il pacchetto specificato non è valido</span><span class="sxs-lookup"><span data-stu-id="aaaf1-150">The provided package is invalid</span></span>
<span data-ttu-id="aaaf1-151">409</span><span class="sxs-lookup"><span data-stu-id="aaaf1-151">409</span></span>         | <span data-ttu-id="aaaf1-152">Esiste già un pacchetto con l'ID e la versione specificati</span><span class="sxs-lookup"><span data-stu-id="aaaf1-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="aaaf1-153">Le implementazioni del server variano in base al codice di stato di esito positivo restituito quando viene eseguito il push di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="aaaf1-154">Eliminare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="aaaf1-154">Delete a package</span></span>

<span data-ttu-id="aaaf1-155">nuget.org interpreta la richiesta di eliminazione del pacchetto come "Unlist".</span><span class="sxs-lookup"><span data-stu-id="aaaf1-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="aaaf1-156">Questo significa che il pacchetto è ancora disponibile per i consumer esistenti del pacchetto, ma il pacchetto non viene più visualizzato nei risultati della ricerca o nell'interfaccia Web.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="aaaf1-157">Per ulteriori informazioni su questa procedura, vedere i criteri dei [pacchetti eliminati](../nuget-org/policies/deleting-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="aaaf1-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="aaaf1-158">Altre implementazioni del server sono gratuite per interpretare questo segnale come eliminazione, eliminazione temporanea o annullamento dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="aaaf1-159">Ad esempio, [NuGet. Server](https://www.nuget.org/packages/NuGet.Server) (un'implementazione del server che supporta solo la versione precedente dell'API v2) supporta la gestione della richiesta come Unlist o DELETE rigido in base a un'opzione di configurazione.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="aaaf1-160">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="aaaf1-160">Request parameters</span></span>

<span data-ttu-id="aaaf1-161">Nome</span><span class="sxs-lookup"><span data-stu-id="aaaf1-161">Name</span></span>           | <span data-ttu-id="aaaf1-162">In</span><span class="sxs-lookup"><span data-stu-id="aaaf1-162">In</span></span>     | <span data-ttu-id="aaaf1-163">Type</span><span class="sxs-lookup"><span data-stu-id="aaaf1-163">Type</span></span>   | <span data-ttu-id="aaaf1-164">Necessario</span><span class="sxs-lookup"><span data-stu-id="aaaf1-164">Required</span></span> | <span data-ttu-id="aaaf1-165">Note</span><span class="sxs-lookup"><span data-stu-id="aaaf1-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="aaaf1-166">ID</span><span class="sxs-lookup"><span data-stu-id="aaaf1-166">ID</span></span>             | <span data-ttu-id="aaaf1-167">URL</span><span class="sxs-lookup"><span data-stu-id="aaaf1-167">URL</span></span>    | <span data-ttu-id="aaaf1-168">string</span><span class="sxs-lookup"><span data-stu-id="aaaf1-168">string</span></span> | <span data-ttu-id="aaaf1-169">sì</span><span class="sxs-lookup"><span data-stu-id="aaaf1-169">yes</span></span>      | <span data-ttu-id="aaaf1-170">ID del pacchetto da eliminare</span><span class="sxs-lookup"><span data-stu-id="aaaf1-170">The ID of the package to delete</span></span>
<span data-ttu-id="aaaf1-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="aaaf1-171">VERSION</span></span>        | <span data-ttu-id="aaaf1-172">URL</span><span class="sxs-lookup"><span data-stu-id="aaaf1-172">URL</span></span>    | <span data-ttu-id="aaaf1-173">string</span><span class="sxs-lookup"><span data-stu-id="aaaf1-173">string</span></span> | <span data-ttu-id="aaaf1-174">sì</span><span class="sxs-lookup"><span data-stu-id="aaaf1-174">yes</span></span>      | <span data-ttu-id="aaaf1-175">Versione del pacchetto da eliminare</span><span class="sxs-lookup"><span data-stu-id="aaaf1-175">The version of the package to delete</span></span>
<span data-ttu-id="aaaf1-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="aaaf1-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="aaaf1-177">Intestazione</span><span class="sxs-lookup"><span data-stu-id="aaaf1-177">Header</span></span> | <span data-ttu-id="aaaf1-178">string</span><span class="sxs-lookup"><span data-stu-id="aaaf1-178">string</span></span> | <span data-ttu-id="aaaf1-179">sì</span><span class="sxs-lookup"><span data-stu-id="aaaf1-179">yes</span></span>      | <span data-ttu-id="aaaf1-180">Ad esempio: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="aaaf1-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="aaaf1-181">Risposta</span><span class="sxs-lookup"><span data-stu-id="aaaf1-181">Response</span></span>

<span data-ttu-id="aaaf1-182">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="aaaf1-182">Status Code</span></span> | <span data-ttu-id="aaaf1-183">Significato</span><span class="sxs-lookup"><span data-stu-id="aaaf1-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="aaaf1-184">204</span><span class="sxs-lookup"><span data-stu-id="aaaf1-184">204</span></span>         | <span data-ttu-id="aaaf1-185">Il pacchetto è stato eliminato</span><span class="sxs-lookup"><span data-stu-id="aaaf1-185">The package was deleted</span></span>
<span data-ttu-id="aaaf1-186">404</span><span class="sxs-lookup"><span data-stu-id="aaaf1-186">404</span></span>         | <span data-ttu-id="aaaf1-187">Nessun pacchetto con l'oggetto fornito `ID` ed `VERSION` esiste</span><span class="sxs-lookup"><span data-stu-id="aaaf1-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="aaaf1-188">Rielencare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="aaaf1-188">Relist a package</span></span>

<span data-ttu-id="aaaf1-189">Se un pacchetto non è incluso nell'elenco, è possibile renderlo ancora una volta visibile nei risultati della ricerca usando l'endpoint "relist".</span><span class="sxs-lookup"><span data-stu-id="aaaf1-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="aaaf1-190">Questo endpoint ha la stessa forma dell' [endpoint Delete (Unlist)](#delete-a-package) , ma usa il `POST` metodo HTTP anziché il `DELETE` metodo.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="aaaf1-191">Se il pacchetto è già elencato, la richiesta ha ancora esito positivo.</span><span class="sxs-lookup"><span data-stu-id="aaaf1-191">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="aaaf1-192">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="aaaf1-192">Request parameters</span></span>

<span data-ttu-id="aaaf1-193">Nome</span><span class="sxs-lookup"><span data-stu-id="aaaf1-193">Name</span></span>           | <span data-ttu-id="aaaf1-194">In</span><span class="sxs-lookup"><span data-stu-id="aaaf1-194">In</span></span>     | <span data-ttu-id="aaaf1-195">Type</span><span class="sxs-lookup"><span data-stu-id="aaaf1-195">Type</span></span>   | <span data-ttu-id="aaaf1-196">Necessario</span><span class="sxs-lookup"><span data-stu-id="aaaf1-196">Required</span></span> | <span data-ttu-id="aaaf1-197">Note</span><span class="sxs-lookup"><span data-stu-id="aaaf1-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="aaaf1-198">ID</span><span class="sxs-lookup"><span data-stu-id="aaaf1-198">ID</span></span>             | <span data-ttu-id="aaaf1-199">URL</span><span class="sxs-lookup"><span data-stu-id="aaaf1-199">URL</span></span>    | <span data-ttu-id="aaaf1-200">string</span><span class="sxs-lookup"><span data-stu-id="aaaf1-200">string</span></span> | <span data-ttu-id="aaaf1-201">sì</span><span class="sxs-lookup"><span data-stu-id="aaaf1-201">yes</span></span>      | <span data-ttu-id="aaaf1-202">ID del pacchetto da rielencare</span><span class="sxs-lookup"><span data-stu-id="aaaf1-202">The ID of the package to relist</span></span>
<span data-ttu-id="aaaf1-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="aaaf1-203">VERSION</span></span>        | <span data-ttu-id="aaaf1-204">URL</span><span class="sxs-lookup"><span data-stu-id="aaaf1-204">URL</span></span>    | <span data-ttu-id="aaaf1-205">string</span><span class="sxs-lookup"><span data-stu-id="aaaf1-205">string</span></span> | <span data-ttu-id="aaaf1-206">sì</span><span class="sxs-lookup"><span data-stu-id="aaaf1-206">yes</span></span>      | <span data-ttu-id="aaaf1-207">Versione del pacchetto da rielencare</span><span class="sxs-lookup"><span data-stu-id="aaaf1-207">The version of the package to relist</span></span>
<span data-ttu-id="aaaf1-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="aaaf1-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="aaaf1-209">Intestazione</span><span class="sxs-lookup"><span data-stu-id="aaaf1-209">Header</span></span> | <span data-ttu-id="aaaf1-210">string</span><span class="sxs-lookup"><span data-stu-id="aaaf1-210">string</span></span> | <span data-ttu-id="aaaf1-211">sì</span><span class="sxs-lookup"><span data-stu-id="aaaf1-211">yes</span></span>      | <span data-ttu-id="aaaf1-212">Ad esempio: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="aaaf1-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="aaaf1-213">Risposta</span><span class="sxs-lookup"><span data-stu-id="aaaf1-213">Response</span></span>

<span data-ttu-id="aaaf1-214">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="aaaf1-214">Status Code</span></span> | <span data-ttu-id="aaaf1-215">Significato</span><span class="sxs-lookup"><span data-stu-id="aaaf1-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="aaaf1-216">200</span><span class="sxs-lookup"><span data-stu-id="aaaf1-216">200</span></span>         | <span data-ttu-id="aaaf1-217">Il pacchetto è ora elencato</span><span class="sxs-lookup"><span data-stu-id="aaaf1-217">The package is now listed</span></span>
<span data-ttu-id="aaaf1-218">404</span><span class="sxs-lookup"><span data-stu-id="aaaf1-218">404</span></span>         | <span data-ttu-id="aaaf1-219">Nessun pacchetto con l'oggetto fornito `ID` ed `VERSION` esiste</span><span class="sxs-lookup"><span data-stu-id="aaaf1-219">No package with the provided `ID` and `VERSION` exists</span></span>
