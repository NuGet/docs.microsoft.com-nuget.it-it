---
title: Push e Delete, NuGet API | Documenti Microsoft
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
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: Il servizio di pubblicazione consente ai client di pubblicare nuovi pacchetti e l'esclusione o eliminare i pacchetti esistenti.
keywords: Pacchetto NuGet API push API NuGet eliminare pacchetto, API NuGet esclusione di pacchetto, pacchetto di caricamento API NuGet, API NuGet creare pacchetto
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 87970a701c63bce2b74c619069ec1d231ea77ab5
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="1a26f-104">Push ed eliminare</span><span class="sxs-lookup"><span data-stu-id="1a26f-104">Push and Delete</span></span>

<span data-ttu-id="1a26f-105">È possibile eseguire il push, eliminare o esclusione, a seconda dell'implementazione di server e rimettere pacchetti utilizzando l'API di NuGet V3.</span><span class="sxs-lookup"><span data-stu-id="1a26f-105">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="1a26f-106">Queste operazioni sono basate sul `PackagePublish` risorse, vedere il [indice servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="1a26f-106">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="1a26f-107">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="1a26f-107">Versioning</span></span>

<span data-ttu-id="1a26f-108">Le operazioni seguenti `@type` valore viene utilizzato:</span><span class="sxs-lookup"><span data-stu-id="1a26f-108">The following `@type` value is used:</span></span>

<span data-ttu-id="1a26f-109">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="1a26f-109">@type value</span></span>          | <span data-ttu-id="1a26f-110">Note</span><span class="sxs-lookup"><span data-stu-id="1a26f-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="1a26f-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="1a26f-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="1a26f-112">La versione iniziale</span><span class="sxs-lookup"><span data-stu-id="1a26f-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="1a26f-113">URL di base</span><span class="sxs-lookup"><span data-stu-id="1a26f-113">Base URL</span></span>

<span data-ttu-id="1a26f-114">L'URL di base per le API seguente è il valore della `@id` proprietà del `PackagePublish/2.0.0` risorse nell'origine del pacchetto [indice servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="1a26f-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="1a26f-115">Per la documentazione riportata di seguito, viene utilizzato l'URL di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1a26f-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="1a26f-116">Prendere in considerazione `https://www.nuget.org/api/v2/package` come segnaposto per il `@id` valore trovato in corrispondenza dell'indice del servizio.</span><span class="sxs-lookup"><span data-stu-id="1a26f-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="1a26f-117">Si noti che questo URL punti nello stesso percorso dell'endpoint di push V2 legacy, poiché il protocollo è gli stessi.</span><span class="sxs-lookup"><span data-stu-id="1a26f-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="1a26f-118">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="1a26f-118">HTTP methods</span></span>

<span data-ttu-id="1a26f-119">Il `PUT`, `POST` e `DELETE` metodi HTTP supportati da questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="1a26f-119">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="1a26f-120">Per i metodi supportati per ogni endpoint, vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="1a26f-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="1a26f-121">Push di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="1a26f-121">Push a package</span></span>

> [!Note]
> <span data-ttu-id="1a26f-122">ha NuGet.org [requisiti aggiuntivi](NuGet-Protocols.md) per l'interazione con l'endpoint di push.</span><span class="sxs-lookup"><span data-stu-id="1a26f-122">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="1a26f-123">NuGet.org supporta l'inserimento di nuovi pacchetti utilizzando l'API seguente.</span><span class="sxs-lookup"><span data-stu-id="1a26f-123">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="1a26f-124">Se il pacchetto con la versione e l'ID specificato esiste già, nuget.org rifiuterà il push.</span><span class="sxs-lookup"><span data-stu-id="1a26f-124">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="1a26f-125">Altre origini pacchetto supportino la sostituzione di un pacchetto esistente.</span><span class="sxs-lookup"><span data-stu-id="1a26f-125">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="1a26f-126">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="1a26f-126">Request parameters</span></span>

<span data-ttu-id="1a26f-127">nome</span><span class="sxs-lookup"><span data-stu-id="1a26f-127">Name</span></span>           | <span data-ttu-id="1a26f-128">In</span><span class="sxs-lookup"><span data-stu-id="1a26f-128">In</span></span>     | <span data-ttu-id="1a26f-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a26f-129">Type</span></span>   | <span data-ttu-id="1a26f-130">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1a26f-130">Required</span></span> | <span data-ttu-id="1a26f-131">Note</span><span class="sxs-lookup"><span data-stu-id="1a26f-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="1a26f-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="1a26f-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="1a26f-133">Header</span><span class="sxs-lookup"><span data-stu-id="1a26f-133">Header</span></span> | <span data-ttu-id="1a26f-134">stringa</span><span class="sxs-lookup"><span data-stu-id="1a26f-134">string</span></span> | <span data-ttu-id="1a26f-135">sì</span><span class="sxs-lookup"><span data-stu-id="1a26f-135">yes</span></span>      | <span data-ttu-id="1a26f-136">Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="1a26f-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="1a26f-137">La chiave API è una stringa opaca disponibili dall'origine del pacchetto per l'utente e configurato nel client.</span><span class="sxs-lookup"><span data-stu-id="1a26f-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="1a26f-138">Nessun formato determinata stringa è obbligatoria, ma la lunghezza della chiave API non deve superare dimensioni per i valori dell'intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="1a26f-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="1a26f-139">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="1a26f-139">Request body</span></span>

<span data-ttu-id="1a26f-140">Il corpo della richiesta deve essere nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="1a26f-140">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="1a26f-141">Dati del form multipart</span><span class="sxs-lookup"><span data-stu-id="1a26f-141">Multipart form data</span></span>

<span data-ttu-id="1a26f-142">L'intestazione della richiesta `Content-Type` è `multipart/form-data` e i byte non elaborati del .nupkg viene inserito il primo elemento nel corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="1a26f-142">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="1a26f-143">Gli elementi successivi in più parti corpo vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="1a26f-143">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="1a26f-144">Il nome del file o qualsiasi altra intestazione degli elementi in più parti vengono ignorata.</span><span class="sxs-lookup"><span data-stu-id="1a26f-144">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="1a26f-145">Risposta</span><span class="sxs-lookup"><span data-stu-id="1a26f-145">Response</span></span>

<span data-ttu-id="1a26f-146">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="1a26f-146">Status Code</span></span> | <span data-ttu-id="1a26f-147">Significato</span><span class="sxs-lookup"><span data-stu-id="1a26f-147">Meaning</span></span>
----------- | -------
<span data-ttu-id="1a26f-148">201, 202</span><span class="sxs-lookup"><span data-stu-id="1a26f-148">201, 202</span></span>    | <span data-ttu-id="1a26f-149">Il pacchetto è stato inserito correttamente</span><span class="sxs-lookup"><span data-stu-id="1a26f-149">The package was successfully pushed</span></span>
<span data-ttu-id="1a26f-150">400</span><span class="sxs-lookup"><span data-stu-id="1a26f-150">400</span></span>         | <span data-ttu-id="1a26f-151">Il pacchetto fornito non è valido</span><span class="sxs-lookup"><span data-stu-id="1a26f-151">The provided package is invalid</span></span>
<span data-ttu-id="1a26f-152">409</span><span class="sxs-lookup"><span data-stu-id="1a26f-152">409</span></span>         | <span data-ttu-id="1a26f-153">Un pacchetto con la versione e l'ID specificato esiste già</span><span class="sxs-lookup"><span data-stu-id="1a26f-153">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="1a26f-154">Le implementazioni server variare il codice di stato di esito positivo restituito quando un pacchetto viene inserito correttamente.</span><span class="sxs-lookup"><span data-stu-id="1a26f-154">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="1a26f-155">Eliminare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="1a26f-155">Delete a package</span></span>

<span data-ttu-id="1a26f-156">NuGet.org interpreta la richiesta di eliminazione del pacchetto come un'esclusione"di".</span><span class="sxs-lookup"><span data-stu-id="1a26f-156">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="1a26f-157">Ciò significa che il pacchetto è ancora disponibile per i consumer esistenti del pacchetto, ma il pacchetto non viene più visualizzata nei risultati della ricerca o nell'interfaccia web.</span><span class="sxs-lookup"><span data-stu-id="1a26f-157">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="1a26f-158">Per ulteriori informazioni su questa esercitazione, vedere il [pacchetti eliminati](../policies/deleting-packages.md) criteri.</span><span class="sxs-lookup"><span data-stu-id="1a26f-158">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="1a26f-159">Altre implementazioni di server sono disponibili per interpretare il segnale come un'eliminazione di disco rigido, eliminare temporaneamente o esclusione.</span><span class="sxs-lookup"><span data-stu-id="1a26f-159">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="1a26f-160">Ad esempio, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (un'implementazione di server supportano solo l'API V2 precedente) supporta la gestione di questa richiesta come un unlist o una disco rigida delete basata su un'opzione di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1a26f-160">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="1a26f-161">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="1a26f-161">Request parameters</span></span>

<span data-ttu-id="1a26f-162">nome</span><span class="sxs-lookup"><span data-stu-id="1a26f-162">Name</span></span>           | <span data-ttu-id="1a26f-163">In</span><span class="sxs-lookup"><span data-stu-id="1a26f-163">In</span></span>     | <span data-ttu-id="1a26f-164">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a26f-164">Type</span></span>   | <span data-ttu-id="1a26f-165">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1a26f-165">Required</span></span> | <span data-ttu-id="1a26f-166">Note</span><span class="sxs-lookup"><span data-stu-id="1a26f-166">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="1a26f-167">Id</span><span class="sxs-lookup"><span data-stu-id="1a26f-167">ID</span></span>             | <span data-ttu-id="1a26f-168">URL</span><span class="sxs-lookup"><span data-stu-id="1a26f-168">URL</span></span>    | <span data-ttu-id="1a26f-169">stringa</span><span class="sxs-lookup"><span data-stu-id="1a26f-169">string</span></span> | <span data-ttu-id="1a26f-170">sì</span><span class="sxs-lookup"><span data-stu-id="1a26f-170">yes</span></span>      | <span data-ttu-id="1a26f-171">L'ID del pacchetto da eliminare</span><span class="sxs-lookup"><span data-stu-id="1a26f-171">The ID of the package to delete</span></span>
<span data-ttu-id="1a26f-172">VERSION</span><span class="sxs-lookup"><span data-stu-id="1a26f-172">VERSION</span></span>        | <span data-ttu-id="1a26f-173">URL</span><span class="sxs-lookup"><span data-stu-id="1a26f-173">URL</span></span>    | <span data-ttu-id="1a26f-174">stringa</span><span class="sxs-lookup"><span data-stu-id="1a26f-174">string</span></span> | <span data-ttu-id="1a26f-175">sì</span><span class="sxs-lookup"><span data-stu-id="1a26f-175">yes</span></span>      | <span data-ttu-id="1a26f-176">La versione del pacchetto da eliminare</span><span class="sxs-lookup"><span data-stu-id="1a26f-176">The version of the package to delete</span></span>
<span data-ttu-id="1a26f-177">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="1a26f-177">X-NuGet-ApiKey</span></span> | <span data-ttu-id="1a26f-178">Header</span><span class="sxs-lookup"><span data-stu-id="1a26f-178">Header</span></span> | <span data-ttu-id="1a26f-179">stringa</span><span class="sxs-lookup"><span data-stu-id="1a26f-179">string</span></span> | <span data-ttu-id="1a26f-180">sì</span><span class="sxs-lookup"><span data-stu-id="1a26f-180">yes</span></span>      | <span data-ttu-id="1a26f-181">Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="1a26f-181">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="1a26f-182">Risposta</span><span class="sxs-lookup"><span data-stu-id="1a26f-182">Response</span></span>

<span data-ttu-id="1a26f-183">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="1a26f-183">Status Code</span></span> | <span data-ttu-id="1a26f-184">Significato</span><span class="sxs-lookup"><span data-stu-id="1a26f-184">Meaning</span></span>
----------- | -------
<span data-ttu-id="1a26f-185">204</span><span class="sxs-lookup"><span data-stu-id="1a26f-185">204</span></span>         | <span data-ttu-id="1a26f-186">Il pacchetto è stato eliminato</span><span class="sxs-lookup"><span data-stu-id="1a26f-186">The package was deleted</span></span>
<span data-ttu-id="1a26f-187">404</span><span class="sxs-lookup"><span data-stu-id="1a26f-187">404</span></span>         | <span data-ttu-id="1a26f-188">Nessun pacchetto con l'oggetto fornito `ID` e `VERSION` esiste</span><span class="sxs-lookup"><span data-stu-id="1a26f-188">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="1a26f-189">Rimettere un pacchetto</span><span class="sxs-lookup"><span data-stu-id="1a26f-189">Relist a package</span></span>

<span data-ttu-id="1a26f-190">Se un pacchetto è incluso nell'elenco, è possibile rendere nuovamente visibili nei risultati della ricerca utilizzando l'endpoint "rimettere in vendita" che il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1a26f-190">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="1a26f-191">Questo endpoint è la stessa forma di [eliminare (esclusione) endpoint](#delete-a-package) ma utilizza il `POST` metodo HTTP invece del `DELETE` metodo.</span><span class="sxs-lookup"><span data-stu-id="1a26f-191">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="1a26f-192">Se il pacchetto è già presente, viene comunque completato correttamente la richiesta.</span><span class="sxs-lookup"><span data-stu-id="1a26f-192">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="1a26f-193">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="1a26f-193">Request parameters</span></span>

<span data-ttu-id="1a26f-194">nome</span><span class="sxs-lookup"><span data-stu-id="1a26f-194">Name</span></span>           | <span data-ttu-id="1a26f-195">In</span><span class="sxs-lookup"><span data-stu-id="1a26f-195">In</span></span>     | <span data-ttu-id="1a26f-196">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a26f-196">Type</span></span>   | <span data-ttu-id="1a26f-197">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1a26f-197">Required</span></span> | <span data-ttu-id="1a26f-198">Note</span><span class="sxs-lookup"><span data-stu-id="1a26f-198">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="1a26f-199">Id</span><span class="sxs-lookup"><span data-stu-id="1a26f-199">ID</span></span>             | <span data-ttu-id="1a26f-200">URL</span><span class="sxs-lookup"><span data-stu-id="1a26f-200">URL</span></span>    | <span data-ttu-id="1a26f-201">stringa</span><span class="sxs-lookup"><span data-stu-id="1a26f-201">string</span></span> | <span data-ttu-id="1a26f-202">sì</span><span class="sxs-lookup"><span data-stu-id="1a26f-202">yes</span></span>      | <span data-ttu-id="1a26f-203">L'ID del pacchetto rimettere in</span><span class="sxs-lookup"><span data-stu-id="1a26f-203">The ID of the package to relist</span></span>
<span data-ttu-id="1a26f-204">VERSION</span><span class="sxs-lookup"><span data-stu-id="1a26f-204">VERSION</span></span>        | <span data-ttu-id="1a26f-205">URL</span><span class="sxs-lookup"><span data-stu-id="1a26f-205">URL</span></span>    | <span data-ttu-id="1a26f-206">stringa</span><span class="sxs-lookup"><span data-stu-id="1a26f-206">string</span></span> | <span data-ttu-id="1a26f-207">sì</span><span class="sxs-lookup"><span data-stu-id="1a26f-207">yes</span></span>      | <span data-ttu-id="1a26f-208">La versione del pacchetto rimettere in</span><span class="sxs-lookup"><span data-stu-id="1a26f-208">The version of the package to relist</span></span>
<span data-ttu-id="1a26f-209">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="1a26f-209">X-NuGet-ApiKey</span></span> | <span data-ttu-id="1a26f-210">Header</span><span class="sxs-lookup"><span data-stu-id="1a26f-210">Header</span></span> | <span data-ttu-id="1a26f-211">stringa</span><span class="sxs-lookup"><span data-stu-id="1a26f-211">string</span></span> | <span data-ttu-id="1a26f-212">sì</span><span class="sxs-lookup"><span data-stu-id="1a26f-212">yes</span></span>      | <span data-ttu-id="1a26f-213">Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="1a26f-213">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="1a26f-214">Risposta</span><span class="sxs-lookup"><span data-stu-id="1a26f-214">Response</span></span>

<span data-ttu-id="1a26f-215">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="1a26f-215">Status Code</span></span> | <span data-ttu-id="1a26f-216">Significato</span><span class="sxs-lookup"><span data-stu-id="1a26f-216">Meaning</span></span>
----------- | -------
<span data-ttu-id="1a26f-217">204</span><span class="sxs-lookup"><span data-stu-id="1a26f-217">204</span></span>         | <span data-ttu-id="1a26f-218">Il pacchetto è ora elencato</span><span class="sxs-lookup"><span data-stu-id="1a26f-218">The package is now listed</span></span>
<span data-ttu-id="1a26f-219">404</span><span class="sxs-lookup"><span data-stu-id="1a26f-219">404</span></span>         | <span data-ttu-id="1a26f-220">Nessun pacchetto con l'oggetto fornito `ID` e `VERSION` esiste</span><span class="sxs-lookup"><span data-stu-id="1a26f-220">No package with the provided `ID` and `VERSION` exists</span></span>
