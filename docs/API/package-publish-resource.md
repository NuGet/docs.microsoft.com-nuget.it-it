---
title: Eseguire il push ed eliminare, NuGet API
description: Il servizio di pubblicazione consente ai client di pubblicare nuovi pacchetti e l'esclusione o eliminare i pacchetti esistenti.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 911c8238624f806b1fbb5c7938d02b6bdfbd8614
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="00800-103">Push ed eliminare</span><span class="sxs-lookup"><span data-stu-id="00800-103">Push and Delete</span></span>

<span data-ttu-id="00800-104">È possibile eseguire il push, eliminare o esclusione, a seconda dell'implementazione di server e rimettere pacchetti utilizzando l'API di NuGet V3.</span><span class="sxs-lookup"><span data-stu-id="00800-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="00800-105">Queste operazioni sono basate sul `PackagePublish` risorse, vedere il [indice servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="00800-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="00800-106">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="00800-106">Versioning</span></span>

<span data-ttu-id="00800-107">Le operazioni seguenti `@type` valore viene utilizzato:</span><span class="sxs-lookup"><span data-stu-id="00800-107">The following `@type` value is used:</span></span>

<span data-ttu-id="00800-108">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="00800-108">@type value</span></span>          | <span data-ttu-id="00800-109">Note</span><span class="sxs-lookup"><span data-stu-id="00800-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="00800-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="00800-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="00800-111">La versione iniziale</span><span class="sxs-lookup"><span data-stu-id="00800-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="00800-112">URL di base</span><span class="sxs-lookup"><span data-stu-id="00800-112">Base URL</span></span>

<span data-ttu-id="00800-113">L'URL di base per le API seguente è il valore della `@id` proprietà del `PackagePublish/2.0.0` risorse nell'origine del pacchetto [indice servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="00800-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="00800-114">Per la documentazione riportata di seguito, viene utilizzato l'URL di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="00800-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="00800-115">Prendere in considerazione `https://www.nuget.org/api/v2/package` come segnaposto per il `@id` valore trovato in corrispondenza dell'indice del servizio.</span><span class="sxs-lookup"><span data-stu-id="00800-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="00800-116">Si noti che questo URL punti nello stesso percorso dell'endpoint di push V2 legacy, poiché il protocollo è gli stessi.</span><span class="sxs-lookup"><span data-stu-id="00800-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="00800-117">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="00800-117">HTTP methods</span></span>

<span data-ttu-id="00800-118">Il `PUT`, `POST` e `DELETE` metodi HTTP supportati da questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="00800-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="00800-119">Per i metodi supportati per ogni endpoint, vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="00800-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="00800-120">Push di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="00800-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="00800-121">ha NuGet.org [requisiti aggiuntivi](NuGet-Protocols.md) per l'interazione con l'endpoint di push.</span><span class="sxs-lookup"><span data-stu-id="00800-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="00800-122">NuGet.org supporta l'inserimento di nuovi pacchetti utilizzando l'API seguente.</span><span class="sxs-lookup"><span data-stu-id="00800-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="00800-123">Se il pacchetto con la versione e l'ID specificato esiste già, nuget.org rifiuterà il push.</span><span class="sxs-lookup"><span data-stu-id="00800-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="00800-124">Altre origini pacchetto supportino la sostituzione di un pacchetto esistente.</span><span class="sxs-lookup"><span data-stu-id="00800-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="00800-125">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="00800-125">Request parameters</span></span>

<span data-ttu-id="00800-126">nome</span><span class="sxs-lookup"><span data-stu-id="00800-126">Name</span></span>           | <span data-ttu-id="00800-127">In</span><span class="sxs-lookup"><span data-stu-id="00800-127">In</span></span>     | <span data-ttu-id="00800-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="00800-128">Type</span></span>   | <span data-ttu-id="00800-129">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="00800-129">Required</span></span> | <span data-ttu-id="00800-130">Note</span><span class="sxs-lookup"><span data-stu-id="00800-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="00800-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="00800-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="00800-132">Header</span><span class="sxs-lookup"><span data-stu-id="00800-132">Header</span></span> | <span data-ttu-id="00800-133">stringa</span><span class="sxs-lookup"><span data-stu-id="00800-133">string</span></span> | <span data-ttu-id="00800-134">sì</span><span class="sxs-lookup"><span data-stu-id="00800-134">yes</span></span>      | <span data-ttu-id="00800-135">Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="00800-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="00800-136">La chiave API è una stringa opaca disponibili dall'origine del pacchetto per l'utente e configurato nel client.</span><span class="sxs-lookup"><span data-stu-id="00800-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="00800-137">Nessun formato determinata stringa è obbligatoria, ma la lunghezza della chiave API non deve superare dimensioni per i valori dell'intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="00800-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="00800-138">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="00800-138">Request body</span></span>

<span data-ttu-id="00800-139">Il corpo della richiesta deve essere nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="00800-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="00800-140">Dati del form multipart</span><span class="sxs-lookup"><span data-stu-id="00800-140">Multipart form data</span></span>

<span data-ttu-id="00800-141">L'intestazione della richiesta `Content-Type` è `multipart/form-data` e i byte non elaborati del .nupkg viene inserito il primo elemento nel corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="00800-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="00800-142">Gli elementi successivi in più parti corpo vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="00800-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="00800-143">Il nome del file o qualsiasi altra intestazione degli elementi in più parti vengono ignorata.</span><span class="sxs-lookup"><span data-stu-id="00800-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="00800-144">Risposta</span><span class="sxs-lookup"><span data-stu-id="00800-144">Response</span></span>

<span data-ttu-id="00800-145">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="00800-145">Status Code</span></span> | <span data-ttu-id="00800-146">Significato</span><span class="sxs-lookup"><span data-stu-id="00800-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="00800-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="00800-147">201, 202</span></span>    | <span data-ttu-id="00800-148">Il pacchetto è stato inserito correttamente</span><span class="sxs-lookup"><span data-stu-id="00800-148">The package was successfully pushed</span></span>
<span data-ttu-id="00800-149">400</span><span class="sxs-lookup"><span data-stu-id="00800-149">400</span></span>         | <span data-ttu-id="00800-150">Il pacchetto fornito non è valido</span><span class="sxs-lookup"><span data-stu-id="00800-150">The provided package is invalid</span></span>
<span data-ttu-id="00800-151">409</span><span class="sxs-lookup"><span data-stu-id="00800-151">409</span></span>         | <span data-ttu-id="00800-152">Un pacchetto con la versione e l'ID specificato esiste già</span><span class="sxs-lookup"><span data-stu-id="00800-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="00800-153">Le implementazioni server variare il codice di stato di esito positivo restituito quando un pacchetto viene inserito correttamente.</span><span class="sxs-lookup"><span data-stu-id="00800-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="00800-154">Eliminare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="00800-154">Delete a package</span></span>

<span data-ttu-id="00800-155">NuGet.org interpreta la richiesta di eliminazione del pacchetto come un'esclusione"di".</span><span class="sxs-lookup"><span data-stu-id="00800-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="00800-156">Ciò significa che il pacchetto è ancora disponibile per i consumer esistenti del pacchetto, ma il pacchetto non viene più visualizzata nei risultati della ricerca o nell'interfaccia web.</span><span class="sxs-lookup"><span data-stu-id="00800-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="00800-157">Per ulteriori informazioni su questa esercitazione, vedere il [pacchetti eliminati](../policies/deleting-packages.md) criteri.</span><span class="sxs-lookup"><span data-stu-id="00800-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="00800-158">Altre implementazioni di server sono disponibili per interpretare il segnale come un'eliminazione di disco rigido, eliminare temporaneamente o esclusione.</span><span class="sxs-lookup"><span data-stu-id="00800-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="00800-159">Ad esempio, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (un'implementazione di server supportano solo l'API V2 precedente) supporta la gestione di questa richiesta come un unlist o una disco rigida delete basata su un'opzione di configurazione.</span><span class="sxs-lookup"><span data-stu-id="00800-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="00800-160">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="00800-160">Request parameters</span></span>

<span data-ttu-id="00800-161">nome</span><span class="sxs-lookup"><span data-stu-id="00800-161">Name</span></span>           | <span data-ttu-id="00800-162">In</span><span class="sxs-lookup"><span data-stu-id="00800-162">In</span></span>     | <span data-ttu-id="00800-163">Tipo</span><span class="sxs-lookup"><span data-stu-id="00800-163">Type</span></span>   | <span data-ttu-id="00800-164">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="00800-164">Required</span></span> | <span data-ttu-id="00800-165">Note</span><span class="sxs-lookup"><span data-stu-id="00800-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="00800-166">Id</span><span class="sxs-lookup"><span data-stu-id="00800-166">ID</span></span>             | <span data-ttu-id="00800-167">URL</span><span class="sxs-lookup"><span data-stu-id="00800-167">URL</span></span>    | <span data-ttu-id="00800-168">stringa</span><span class="sxs-lookup"><span data-stu-id="00800-168">string</span></span> | <span data-ttu-id="00800-169">sì</span><span class="sxs-lookup"><span data-stu-id="00800-169">yes</span></span>      | <span data-ttu-id="00800-170">L'ID del pacchetto da eliminare</span><span class="sxs-lookup"><span data-stu-id="00800-170">The ID of the package to delete</span></span>
<span data-ttu-id="00800-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="00800-171">VERSION</span></span>        | <span data-ttu-id="00800-172">URL</span><span class="sxs-lookup"><span data-stu-id="00800-172">URL</span></span>    | <span data-ttu-id="00800-173">stringa</span><span class="sxs-lookup"><span data-stu-id="00800-173">string</span></span> | <span data-ttu-id="00800-174">sì</span><span class="sxs-lookup"><span data-stu-id="00800-174">yes</span></span>      | <span data-ttu-id="00800-175">La versione del pacchetto da eliminare</span><span class="sxs-lookup"><span data-stu-id="00800-175">The version of the package to delete</span></span>
<span data-ttu-id="00800-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="00800-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="00800-177">Header</span><span class="sxs-lookup"><span data-stu-id="00800-177">Header</span></span> | <span data-ttu-id="00800-178">stringa</span><span class="sxs-lookup"><span data-stu-id="00800-178">string</span></span> | <span data-ttu-id="00800-179">sì</span><span class="sxs-lookup"><span data-stu-id="00800-179">yes</span></span>      | <span data-ttu-id="00800-180">Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="00800-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="00800-181">Risposta</span><span class="sxs-lookup"><span data-stu-id="00800-181">Response</span></span>

<span data-ttu-id="00800-182">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="00800-182">Status Code</span></span> | <span data-ttu-id="00800-183">Significato</span><span class="sxs-lookup"><span data-stu-id="00800-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="00800-184">204</span><span class="sxs-lookup"><span data-stu-id="00800-184">204</span></span>         | <span data-ttu-id="00800-185">Il pacchetto è stato eliminato</span><span class="sxs-lookup"><span data-stu-id="00800-185">The package was deleted</span></span>
<span data-ttu-id="00800-186">404</span><span class="sxs-lookup"><span data-stu-id="00800-186">404</span></span>         | <span data-ttu-id="00800-187">Nessun pacchetto con l'oggetto fornito `ID` e `VERSION` esiste</span><span class="sxs-lookup"><span data-stu-id="00800-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="00800-188">Rimettere un pacchetto</span><span class="sxs-lookup"><span data-stu-id="00800-188">Relist a package</span></span>

<span data-ttu-id="00800-189">Se un pacchetto è incluso nell'elenco, è possibile rendere nuovamente visibili nei risultati della ricerca utilizzando l'endpoint "rimettere in vendita" che il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="00800-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="00800-190">Questo endpoint è la stessa forma di [eliminare (esclusione) endpoint](#delete-a-package) ma utilizza il `POST` metodo HTTP invece del `DELETE` metodo.</span><span class="sxs-lookup"><span data-stu-id="00800-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="00800-191">Se il pacchetto è già presente, viene comunque completato correttamente la richiesta.</span><span class="sxs-lookup"><span data-stu-id="00800-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="00800-192">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="00800-192">Request parameters</span></span>

<span data-ttu-id="00800-193">nome</span><span class="sxs-lookup"><span data-stu-id="00800-193">Name</span></span>           | <span data-ttu-id="00800-194">In</span><span class="sxs-lookup"><span data-stu-id="00800-194">In</span></span>     | <span data-ttu-id="00800-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="00800-195">Type</span></span>   | <span data-ttu-id="00800-196">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="00800-196">Required</span></span> | <span data-ttu-id="00800-197">Note</span><span class="sxs-lookup"><span data-stu-id="00800-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="00800-198">Id</span><span class="sxs-lookup"><span data-stu-id="00800-198">ID</span></span>             | <span data-ttu-id="00800-199">URL</span><span class="sxs-lookup"><span data-stu-id="00800-199">URL</span></span>    | <span data-ttu-id="00800-200">stringa</span><span class="sxs-lookup"><span data-stu-id="00800-200">string</span></span> | <span data-ttu-id="00800-201">sì</span><span class="sxs-lookup"><span data-stu-id="00800-201">yes</span></span>      | <span data-ttu-id="00800-202">L'ID del pacchetto rimettere in</span><span class="sxs-lookup"><span data-stu-id="00800-202">The ID of the package to relist</span></span>
<span data-ttu-id="00800-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="00800-203">VERSION</span></span>        | <span data-ttu-id="00800-204">URL</span><span class="sxs-lookup"><span data-stu-id="00800-204">URL</span></span>    | <span data-ttu-id="00800-205">stringa</span><span class="sxs-lookup"><span data-stu-id="00800-205">string</span></span> | <span data-ttu-id="00800-206">sì</span><span class="sxs-lookup"><span data-stu-id="00800-206">yes</span></span>      | <span data-ttu-id="00800-207">La versione del pacchetto rimettere in</span><span class="sxs-lookup"><span data-stu-id="00800-207">The version of the package to relist</span></span>
<span data-ttu-id="00800-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="00800-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="00800-209">Header</span><span class="sxs-lookup"><span data-stu-id="00800-209">Header</span></span> | <span data-ttu-id="00800-210">stringa</span><span class="sxs-lookup"><span data-stu-id="00800-210">string</span></span> | <span data-ttu-id="00800-211">sì</span><span class="sxs-lookup"><span data-stu-id="00800-211">yes</span></span>      | <span data-ttu-id="00800-212">Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="00800-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="00800-213">Risposta</span><span class="sxs-lookup"><span data-stu-id="00800-213">Response</span></span>

<span data-ttu-id="00800-214">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="00800-214">Status Code</span></span> | <span data-ttu-id="00800-215">Significato</span><span class="sxs-lookup"><span data-stu-id="00800-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="00800-216">200</span><span class="sxs-lookup"><span data-stu-id="00800-216">200</span></span>         | <span data-ttu-id="00800-217">Il pacchetto è ora elencato</span><span class="sxs-lookup"><span data-stu-id="00800-217">The package is now listed</span></span>
<span data-ttu-id="00800-218">404</span><span class="sxs-lookup"><span data-stu-id="00800-218">404</span></span>         | <span data-ttu-id="00800-219">Nessun pacchetto con l'oggetto fornito `ID` e `VERSION` esiste</span><span class="sxs-lookup"><span data-stu-id="00800-219">No package with the provided `ID` and `VERSION` exists</span></span>
