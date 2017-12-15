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
ms.openlocfilehash: 1fa3c0e1698a11208d9ef29fdf26a4980cb60cf5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="push-and-delete"></a><span data-ttu-id="98c51-104">Push ed eliminare</span><span class="sxs-lookup"><span data-stu-id="98c51-104">Push and Delete</span></span>

<span data-ttu-id="98c51-105">È possibile eseguire il push ed eliminare (o esclusione, a seconda dell'implementazione di server) dei pacchetti tramite l'API di NuGet V3.</span><span class="sxs-lookup"><span data-stu-id="98c51-105">It is possible to push and delete (or unlist, depending on the server implementation) packages using the NuGet V3 API.</span></span>
<span data-ttu-id="98c51-106">Entrambe le operazioni sono basate sul `PackagePublish` risorse, vedere il [indice servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="98c51-106">Both operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="98c51-107">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="98c51-107">Versioning</span></span>

<span data-ttu-id="98c51-108">Le operazioni seguenti `@type` valore viene utilizzato:</span><span class="sxs-lookup"><span data-stu-id="98c51-108">The following `@type` value is used:</span></span>

<span data-ttu-id="98c51-109">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="98c51-109">@type value</span></span>          | <span data-ttu-id="98c51-110">Note</span><span class="sxs-lookup"><span data-stu-id="98c51-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="98c51-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="98c51-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="98c51-112">La versione iniziale</span><span class="sxs-lookup"><span data-stu-id="98c51-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="98c51-113">URL di base</span><span class="sxs-lookup"><span data-stu-id="98c51-113">Base URL</span></span>

<span data-ttu-id="98c51-114">L'URL di base per le API seguente è il valore della `@id` proprietà del `PackagePublish/2.0.0` risorse nell'origine del pacchetto [indice servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="98c51-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="98c51-115">Per la documentazione riportata di seguito, viene utilizzato l'URL di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="98c51-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="98c51-116">Prendere in considerazione `https://www.nuget.org/api/v2/package` come segnaposto per il `@id` valore trovato in corrispondenza dell'indice del servizio.</span><span class="sxs-lookup"><span data-stu-id="98c51-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="98c51-117">Si noti che questo URL punti nello stesso percorso dell'endpoint di push V2 legacy, poiché il protocollo è gli stessi.</span><span class="sxs-lookup"><span data-stu-id="98c51-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="98c51-118">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="98c51-118">HTTP methods</span></span>

<span data-ttu-id="98c51-119">Il `PUT` e `DELETE` metodi HTTP supportati da questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="98c51-119">The `PUT` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="98c51-120">Per i metodi supportati per ogni endpoint, vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="98c51-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="98c51-121">Push di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="98c51-121">Push a package</span></span>

<span data-ttu-id="98c51-122">NuGet.org supporta l'inserimento di nuovi pacchetti utilizzando l'API seguente.</span><span class="sxs-lookup"><span data-stu-id="98c51-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="98c51-123">Se il pacchetto con la versione e l'ID specificato esiste già, nuget.org rifiuterà il push.</span><span class="sxs-lookup"><span data-stu-id="98c51-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="98c51-124">Altre origini pacchetto supportino la sostituzione di un pacchetto esistente.</span><span class="sxs-lookup"><span data-stu-id="98c51-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="98c51-125">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="98c51-125">Request parameters</span></span>

<span data-ttu-id="98c51-126">Nome</span><span class="sxs-lookup"><span data-stu-id="98c51-126">Name</span></span>           | <span data-ttu-id="98c51-127">In</span><span class="sxs-lookup"><span data-stu-id="98c51-127">In</span></span>     | <span data-ttu-id="98c51-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="98c51-128">Type</span></span>   | <span data-ttu-id="98c51-129">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="98c51-129">Required</span></span> | <span data-ttu-id="98c51-130">Note</span><span class="sxs-lookup"><span data-stu-id="98c51-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="98c51-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="98c51-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="98c51-132">Header</span><span class="sxs-lookup"><span data-stu-id="98c51-132">Header</span></span> | <span data-ttu-id="98c51-133">string</span><span class="sxs-lookup"><span data-stu-id="98c51-133">string</span></span> | <span data-ttu-id="98c51-134">sì</span><span class="sxs-lookup"><span data-stu-id="98c51-134">yes</span></span>      | <span data-ttu-id="98c51-135">Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="98c51-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="98c51-136">La chiave API è una stringa opaca disponibili dall'origine del pacchetto per l'utente e configurato nel client.</span><span class="sxs-lookup"><span data-stu-id="98c51-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="98c51-137">Nessun formato determinata stringa è obbligatoria, ma la lunghezza della chiave API non deve superare dimensioni per i valori dell'intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="98c51-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="98c51-138">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="98c51-138">Request body</span></span>

<span data-ttu-id="98c51-139">Il corpo della richiesta deve essere nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="98c51-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="98c51-140">Dati del form multipart</span><span class="sxs-lookup"><span data-stu-id="98c51-140">Multipart form data</span></span>

<span data-ttu-id="98c51-141">L'intestazione della richiesta `Content-Type` è `multipart/form-data` e i byte non elaborati del .nupkg viene inserito il primo elemento nel corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="98c51-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="98c51-142">Gli elementi successivi in più parti corpo vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="98c51-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="98c51-143">Il nome del file o qualsiasi altra intestazione degli elementi in più parti vengono ignorata.</span><span class="sxs-lookup"><span data-stu-id="98c51-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="98c51-144">Risposta</span><span class="sxs-lookup"><span data-stu-id="98c51-144">Response</span></span>

<span data-ttu-id="98c51-145">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="98c51-145">Status Code</span></span> | <span data-ttu-id="98c51-146">Significato</span><span class="sxs-lookup"><span data-stu-id="98c51-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="98c51-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="98c51-147">201, 202</span></span>    | <span data-ttu-id="98c51-148">Il pacchetto è stato inserito correttamente</span><span class="sxs-lookup"><span data-stu-id="98c51-148">The package was successfully pushed</span></span>
<span data-ttu-id="98c51-149">400</span><span class="sxs-lookup"><span data-stu-id="98c51-149">400</span></span>         | <span data-ttu-id="98c51-150">Il pacchetto fornito non è valido</span><span class="sxs-lookup"><span data-stu-id="98c51-150">The provided package is invalid</span></span>
<span data-ttu-id="98c51-151">409</span><span class="sxs-lookup"><span data-stu-id="98c51-151">409</span></span>         | <span data-ttu-id="98c51-152">Un pacchetto con la versione e l'ID specificato esiste già</span><span class="sxs-lookup"><span data-stu-id="98c51-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="98c51-153">Le implementazioni server variare il codice di stato di esito positivo restituito quando un pacchetto viene inserito correttamente.</span><span class="sxs-lookup"><span data-stu-id="98c51-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="98c51-154">Eliminare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="98c51-154">Delete a package</span></span>

<span data-ttu-id="98c51-155">NuGet.org interpreta la richiesta di eliminazione del pacchetto come un'esclusione"di".</span><span class="sxs-lookup"><span data-stu-id="98c51-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="98c51-156">Ciò significa che il pacchetto è ancora disponibile per i consumer esistenti del pacchetto, ma il pacchetto non viene più visualizzata nei risultati della ricerca o nell'interfaccia web.</span><span class="sxs-lookup"><span data-stu-id="98c51-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="98c51-157">Per ulteriori informazioni su questa esercitazione, vedere il [pacchetti eliminati](../policies/deleting-packages.md) criteri.</span><span class="sxs-lookup"><span data-stu-id="98c51-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="98c51-158">Altre implementazioni di server sono disponibili per interpretare il segnale come un'eliminazione di disco rigido, eliminare temporaneamente o esclusione.</span><span class="sxs-lookup"><span data-stu-id="98c51-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="98c51-159">Ad esempio, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (un'implementazione di server supportano solo l'API V2 precedente) supporta la gestione di questa richiesta come un unlist o una disco rigida delete basata su un'opzione di configurazione.</span><span class="sxs-lookup"><span data-stu-id="98c51-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="98c51-160">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="98c51-160">Request parameters</span></span>

<span data-ttu-id="98c51-161">Nome</span><span class="sxs-lookup"><span data-stu-id="98c51-161">Name</span></span>           | <span data-ttu-id="98c51-162">In</span><span class="sxs-lookup"><span data-stu-id="98c51-162">In</span></span>     | <span data-ttu-id="98c51-163">Tipo</span><span class="sxs-lookup"><span data-stu-id="98c51-163">Type</span></span>   | <span data-ttu-id="98c51-164">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="98c51-164">Required</span></span> | <span data-ttu-id="98c51-165">Note</span><span class="sxs-lookup"><span data-stu-id="98c51-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="98c51-166">Id</span><span class="sxs-lookup"><span data-stu-id="98c51-166">ID</span></span>             | <span data-ttu-id="98c51-167">URL</span><span class="sxs-lookup"><span data-stu-id="98c51-167">URL</span></span>    | <span data-ttu-id="98c51-168">string</span><span class="sxs-lookup"><span data-stu-id="98c51-168">string</span></span> | <span data-ttu-id="98c51-169">sì</span><span class="sxs-lookup"><span data-stu-id="98c51-169">yes</span></span>      | <span data-ttu-id="98c51-170">L'ID del pacchetto da eliminare</span><span class="sxs-lookup"><span data-stu-id="98c51-170">The ID of the package to delete</span></span>
<span data-ttu-id="98c51-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="98c51-171">VERSION</span></span>        | <span data-ttu-id="98c51-172">URL</span><span class="sxs-lookup"><span data-stu-id="98c51-172">URL</span></span>    | <span data-ttu-id="98c51-173">string</span><span class="sxs-lookup"><span data-stu-id="98c51-173">string</span></span> | <span data-ttu-id="98c51-174">sì</span><span class="sxs-lookup"><span data-stu-id="98c51-174">yes</span></span>      | <span data-ttu-id="98c51-175">La versione del pacchetto da eliminare</span><span class="sxs-lookup"><span data-stu-id="98c51-175">The version of the package to delete</span></span>
<span data-ttu-id="98c51-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="98c51-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="98c51-177">Header</span><span class="sxs-lookup"><span data-stu-id="98c51-177">Header</span></span> | <span data-ttu-id="98c51-178">string</span><span class="sxs-lookup"><span data-stu-id="98c51-178">string</span></span> | <span data-ttu-id="98c51-179">sì</span><span class="sxs-lookup"><span data-stu-id="98c51-179">yes</span></span>      | <span data-ttu-id="98c51-180">Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="98c51-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="98c51-181">Risposta</span><span class="sxs-lookup"><span data-stu-id="98c51-181">Response</span></span>

<span data-ttu-id="98c51-182">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="98c51-182">Status Code</span></span> | <span data-ttu-id="98c51-183">Significato</span><span class="sxs-lookup"><span data-stu-id="98c51-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="98c51-184">204</span><span class="sxs-lookup"><span data-stu-id="98c51-184">204</span></span>         | <span data-ttu-id="98c51-185">Il pacchetto è stato eliminato</span><span class="sxs-lookup"><span data-stu-id="98c51-185">The package was deleted</span></span>
<span data-ttu-id="98c51-186">404</span><span class="sxs-lookup"><span data-stu-id="98c51-186">404</span></span>         | <span data-ttu-id="98c51-187">Nessun pacchetto con l'oggetto fornito `ID` e `VERSION` esiste</span><span class="sxs-lookup"><span data-stu-id="98c51-187">No package with the provided `ID` and `VERSION` exists</span></span>
