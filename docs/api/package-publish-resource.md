---
title: Push ed eliminazione, API NuGet
description: Il servizio di pubblicazione consente ai client di pubblicare nuovi pacchetti e rimuovere dall'elenco o Elimina i pacchetti esistenti.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: ad66d8e0ffda13aaef744104c213863b0e111e0e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547521"
---
# <a name="push-and-delete"></a><span data-ttu-id="60b16-103">Push ed eliminazione</span><span class="sxs-lookup"><span data-stu-id="60b16-103">Push and Delete</span></span>

<span data-ttu-id="60b16-104">È possibile eseguire il push, eliminare o rimuovere dall'elenco, a seconda dell'implementazione di server e includere di nuovo nell'elenco dei pacchetti tramite l'API di NuGet V3.</span><span class="sxs-lookup"><span data-stu-id="60b16-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="60b16-105">Queste operazioni si basano all'esterno della `PackagePublish` trovare la risorsa nella [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="60b16-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="60b16-106">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="60b16-106">Versioning</span></span>

<span data-ttu-id="60b16-107">Nell'esempio `@type` valore viene usato:</span><span class="sxs-lookup"><span data-stu-id="60b16-107">The following `@type` value is used:</span></span>

<span data-ttu-id="60b16-108">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="60b16-108">@type value</span></span>          | <span data-ttu-id="60b16-109">Note</span><span class="sxs-lookup"><span data-stu-id="60b16-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="60b16-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="60b16-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="60b16-111">La versione iniziale</span><span class="sxs-lookup"><span data-stu-id="60b16-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="60b16-112">URL di base</span><span class="sxs-lookup"><span data-stu-id="60b16-112">Base URL</span></span>

<span data-ttu-id="60b16-113">L'URL di base per le API seguente è il valore della `@id` proprietà del `PackagePublish/2.0.0` risorsa nell'origine del pacchetto [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="60b16-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="60b16-114">Per la documentazione seguente, viene usato l'URL di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="60b16-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="60b16-115">Prendere in considerazione `https://www.nuget.org/api/v2/package` come segnaposto per il `@id` valore trovato nell'indice del servizio.</span><span class="sxs-lookup"><span data-stu-id="60b16-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="60b16-116">Si noti che questo URL punta a nello stesso percorso degli endpoint precedenti V2 push, poiché il protocollo è gli stessi.</span><span class="sxs-lookup"><span data-stu-id="60b16-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="60b16-117">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="60b16-117">HTTP methods</span></span>

<span data-ttu-id="60b16-118">Il `PUT`, `POST` e `DELETE` metodi HTTP supportati da questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="60b16-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="60b16-119">Per i metodi che sono supportati in ogni endpoint, vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="60b16-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="60b16-120">Push di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="60b16-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="60b16-121">dispone di NuGet.org [requisiti aggiuntivi](NuGet-Protocols.md) per l'interazione con l'endpoint di push.</span><span class="sxs-lookup"><span data-stu-id="60b16-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="60b16-122">NuGet.org supporta il push dei nuovi pacchetti tramite l'API seguente.</span><span class="sxs-lookup"><span data-stu-id="60b16-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="60b16-123">Se il pacchetto con l'ID e versione specificati esiste già, nuget.org rifiuterà il push.</span><span class="sxs-lookup"><span data-stu-id="60b16-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="60b16-124">Altre origini di pacchetti possono supportare la sostituzione di un pacchetto esistente.</span><span class="sxs-lookup"><span data-stu-id="60b16-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="60b16-125">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="60b16-125">Request parameters</span></span>

<span data-ttu-id="60b16-126">nome</span><span class="sxs-lookup"><span data-stu-id="60b16-126">Name</span></span>           | <span data-ttu-id="60b16-127">In</span><span class="sxs-lookup"><span data-stu-id="60b16-127">In</span></span>     | <span data-ttu-id="60b16-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="60b16-128">Type</span></span>   | <span data-ttu-id="60b16-129">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="60b16-129">Required</span></span> | <span data-ttu-id="60b16-130">Note</span><span class="sxs-lookup"><span data-stu-id="60b16-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="60b16-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="60b16-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="60b16-132">Header</span><span class="sxs-lookup"><span data-stu-id="60b16-132">Header</span></span> | <span data-ttu-id="60b16-133">stringa</span><span class="sxs-lookup"><span data-stu-id="60b16-133">string</span></span> | <span data-ttu-id="60b16-134">sì</span><span class="sxs-lookup"><span data-stu-id="60b16-134">yes</span></span>      | <span data-ttu-id="60b16-135">Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="60b16-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="60b16-136">La chiave API è una stringa opaca ricevuto dall'origine del pacchetto dall'utente e configurato nel client.</span><span class="sxs-lookup"><span data-stu-id="60b16-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="60b16-137">Nessun formato determinata stringa è obbligatoria, ma la lunghezza della chiave API non deve superare una dimensione ragionevole per i valori delle intestazioni HTTP.</span><span class="sxs-lookup"><span data-stu-id="60b16-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="60b16-138">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="60b16-138">Request body</span></span>

<span data-ttu-id="60b16-139">Il corpo della richiesta deve essere nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="60b16-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="60b16-140">Dati del form multipart</span><span class="sxs-lookup"><span data-stu-id="60b16-140">Multipart form data</span></span>

<span data-ttu-id="60b16-141">L'intestazione della richiesta `Content-Type` è `multipart/form-data` e il primo elemento nel corpo della richiesta è i byte non elaborati del pacchetto. nupkg esserne eseguito il push.</span><span class="sxs-lookup"><span data-stu-id="60b16-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="60b16-142">Gli elementi successivi in più parti corpo vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="60b16-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="60b16-143">Il nome del file o qualsiasi altra intestazione degli elementi composti da più parti verranno ignorata.</span><span class="sxs-lookup"><span data-stu-id="60b16-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="60b16-144">Risposta</span><span class="sxs-lookup"><span data-stu-id="60b16-144">Response</span></span>

<span data-ttu-id="60b16-145">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="60b16-145">Status Code</span></span> | <span data-ttu-id="60b16-146">Significato</span><span class="sxs-lookup"><span data-stu-id="60b16-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="60b16-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="60b16-147">201, 202</span></span>    | <span data-ttu-id="60b16-148">Il pacchetto è stato eseguito il push</span><span class="sxs-lookup"><span data-stu-id="60b16-148">The package was successfully pushed</span></span>
<span data-ttu-id="60b16-149">400</span><span class="sxs-lookup"><span data-stu-id="60b16-149">400</span></span>         | <span data-ttu-id="60b16-150">Il pacchetto fornito non è valido</span><span class="sxs-lookup"><span data-stu-id="60b16-150">The provided package is invalid</span></span>
<span data-ttu-id="60b16-151">409</span><span class="sxs-lookup"><span data-stu-id="60b16-151">409</span></span>         | <span data-ttu-id="60b16-152">Un pacchetto con l'ID e versione specificati esiste già</span><span class="sxs-lookup"><span data-stu-id="60b16-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="60b16-153">Le implementazioni di server variano il codice di stato riuscito restituito quando un pacchetto viene eseguito il push.</span><span class="sxs-lookup"><span data-stu-id="60b16-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="60b16-154">Eliminare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="60b16-154">Delete a package</span></span>

<span data-ttu-id="60b16-155">NuGet.org interpreta la richiesta di eliminazione del pacchetto come un' "Rimuovi dall'elenco".</span><span class="sxs-lookup"><span data-stu-id="60b16-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="60b16-156">Ciò significa che il pacchetto è ancora disponibile per i consumer esistenti del pacchetto, ma il pacchetto non viene più visualizzata nei risultati della ricerca o nell'interfaccia web.</span><span class="sxs-lookup"><span data-stu-id="60b16-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="60b16-157">Per altre informazioni su questa procedura, vedere la [i pacchetti eliminati](../policies/deleting-packages.md) criteri.</span><span class="sxs-lookup"><span data-stu-id="60b16-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="60b16-158">Altre implementazioni di server sono liberi di interpretare questo segnale come un'eliminazione di disco rigido, tipo "soft" eliminare o rimuovere dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="60b16-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="60b16-159">Ad esempio, [NuGet. server](https://www.nuget.org/packages/NuGet.Server) (un'implementazione del server che supportano solo l'API V2 meno recente) supporta la gestione di questa richiesta come una rimozione dall'elenco o una disco rigida delete basata su un'opzione di configurazione.</span><span class="sxs-lookup"><span data-stu-id="60b16-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="60b16-160">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="60b16-160">Request parameters</span></span>

<span data-ttu-id="60b16-161">nome</span><span class="sxs-lookup"><span data-stu-id="60b16-161">Name</span></span>           | <span data-ttu-id="60b16-162">In</span><span class="sxs-lookup"><span data-stu-id="60b16-162">In</span></span>     | <span data-ttu-id="60b16-163">Tipo</span><span class="sxs-lookup"><span data-stu-id="60b16-163">Type</span></span>   | <span data-ttu-id="60b16-164">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="60b16-164">Required</span></span> | <span data-ttu-id="60b16-165">Note</span><span class="sxs-lookup"><span data-stu-id="60b16-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="60b16-166">Id</span><span class="sxs-lookup"><span data-stu-id="60b16-166">ID</span></span>             | <span data-ttu-id="60b16-167">URL</span><span class="sxs-lookup"><span data-stu-id="60b16-167">URL</span></span>    | <span data-ttu-id="60b16-168">stringa</span><span class="sxs-lookup"><span data-stu-id="60b16-168">string</span></span> | <span data-ttu-id="60b16-169">sì</span><span class="sxs-lookup"><span data-stu-id="60b16-169">yes</span></span>      | <span data-ttu-id="60b16-170">L'ID del pacchetto da eliminare</span><span class="sxs-lookup"><span data-stu-id="60b16-170">The ID of the package to delete</span></span>
<span data-ttu-id="60b16-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="60b16-171">VERSION</span></span>        | <span data-ttu-id="60b16-172">URL</span><span class="sxs-lookup"><span data-stu-id="60b16-172">URL</span></span>    | <span data-ttu-id="60b16-173">stringa</span><span class="sxs-lookup"><span data-stu-id="60b16-173">string</span></span> | <span data-ttu-id="60b16-174">sì</span><span class="sxs-lookup"><span data-stu-id="60b16-174">yes</span></span>      | <span data-ttu-id="60b16-175">La versione del pacchetto da eliminare</span><span class="sxs-lookup"><span data-stu-id="60b16-175">The version of the package to delete</span></span>
<span data-ttu-id="60b16-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="60b16-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="60b16-177">Header</span><span class="sxs-lookup"><span data-stu-id="60b16-177">Header</span></span> | <span data-ttu-id="60b16-178">stringa</span><span class="sxs-lookup"><span data-stu-id="60b16-178">string</span></span> | <span data-ttu-id="60b16-179">sì</span><span class="sxs-lookup"><span data-stu-id="60b16-179">yes</span></span>      | <span data-ttu-id="60b16-180">Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="60b16-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="60b16-181">Risposta</span><span class="sxs-lookup"><span data-stu-id="60b16-181">Response</span></span>

<span data-ttu-id="60b16-182">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="60b16-182">Status Code</span></span> | <span data-ttu-id="60b16-183">Significato</span><span class="sxs-lookup"><span data-stu-id="60b16-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="60b16-184">204</span><span class="sxs-lookup"><span data-stu-id="60b16-184">204</span></span>         | <span data-ttu-id="60b16-185">Il pacchetto è stato eliminato</span><span class="sxs-lookup"><span data-stu-id="60b16-185">The package was deleted</span></span>
<span data-ttu-id="60b16-186">404</span><span class="sxs-lookup"><span data-stu-id="60b16-186">404</span></span>         | <span data-ttu-id="60b16-187">Nessun pacchetto con l'oggetto fornito `ID` e `VERSION` esiste</span><span class="sxs-lookup"><span data-stu-id="60b16-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="60b16-188">Includere di nuovo nell'elenco un pacchetto</span><span class="sxs-lookup"><span data-stu-id="60b16-188">Relist a package</span></span>

<span data-ttu-id="60b16-189">Se un pacchetto è incluso nell'elenco, è possibile rendere nuovamente visibile nei risultati della ricerca usando l'endpoint "rimessa" che il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="60b16-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="60b16-190">Questo endpoint è la stessa forma il [eliminare (rimuovere dall'elenco) endpoint](#delete-a-package) , ma usa le `POST` invece del metodo HTTP il `DELETE` (metodo).</span><span class="sxs-lookup"><span data-stu-id="60b16-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="60b16-191">Se il pacchetto è già presente, viene comunque completato correttamente la richiesta.</span><span class="sxs-lookup"><span data-stu-id="60b16-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="60b16-192">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="60b16-192">Request parameters</span></span>

<span data-ttu-id="60b16-193">nome</span><span class="sxs-lookup"><span data-stu-id="60b16-193">Name</span></span>           | <span data-ttu-id="60b16-194">In</span><span class="sxs-lookup"><span data-stu-id="60b16-194">In</span></span>     | <span data-ttu-id="60b16-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="60b16-195">Type</span></span>   | <span data-ttu-id="60b16-196">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="60b16-196">Required</span></span> | <span data-ttu-id="60b16-197">Note</span><span class="sxs-lookup"><span data-stu-id="60b16-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="60b16-198">Id</span><span class="sxs-lookup"><span data-stu-id="60b16-198">ID</span></span>             | <span data-ttu-id="60b16-199">URL</span><span class="sxs-lookup"><span data-stu-id="60b16-199">URL</span></span>    | <span data-ttu-id="60b16-200">stringa</span><span class="sxs-lookup"><span data-stu-id="60b16-200">string</span></span> | <span data-ttu-id="60b16-201">sì</span><span class="sxs-lookup"><span data-stu-id="60b16-201">yes</span></span>      | <span data-ttu-id="60b16-202">L'ID del pacchetto rimettere in</span><span class="sxs-lookup"><span data-stu-id="60b16-202">The ID of the package to relist</span></span>
<span data-ttu-id="60b16-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="60b16-203">VERSION</span></span>        | <span data-ttu-id="60b16-204">URL</span><span class="sxs-lookup"><span data-stu-id="60b16-204">URL</span></span>    | <span data-ttu-id="60b16-205">stringa</span><span class="sxs-lookup"><span data-stu-id="60b16-205">string</span></span> | <span data-ttu-id="60b16-206">sì</span><span class="sxs-lookup"><span data-stu-id="60b16-206">yes</span></span>      | <span data-ttu-id="60b16-207">La versione del pacchetto rimettere in</span><span class="sxs-lookup"><span data-stu-id="60b16-207">The version of the package to relist</span></span>
<span data-ttu-id="60b16-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="60b16-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="60b16-209">Header</span><span class="sxs-lookup"><span data-stu-id="60b16-209">Header</span></span> | <span data-ttu-id="60b16-210">stringa</span><span class="sxs-lookup"><span data-stu-id="60b16-210">string</span></span> | <span data-ttu-id="60b16-211">sì</span><span class="sxs-lookup"><span data-stu-id="60b16-211">yes</span></span>      | <span data-ttu-id="60b16-212">Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="60b16-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="60b16-213">Risposta</span><span class="sxs-lookup"><span data-stu-id="60b16-213">Response</span></span>

<span data-ttu-id="60b16-214">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="60b16-214">Status Code</span></span> | <span data-ttu-id="60b16-215">Significato</span><span class="sxs-lookup"><span data-stu-id="60b16-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="60b16-216">200</span><span class="sxs-lookup"><span data-stu-id="60b16-216">200</span></span>         | <span data-ttu-id="60b16-217">Il pacchetto è ora elencato</span><span class="sxs-lookup"><span data-stu-id="60b16-217">The package is now listed</span></span>
<span data-ttu-id="60b16-218">404</span><span class="sxs-lookup"><span data-stu-id="60b16-218">404</span></span>         | <span data-ttu-id="60b16-219">Nessun pacchetto con l'oggetto fornito `ID` e `VERSION` esiste</span><span class="sxs-lookup"><span data-stu-id="60b16-219">No package with the provided `ID` and `VERSION` exists</span></span>
