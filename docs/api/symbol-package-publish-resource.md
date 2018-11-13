---
title: Eseguire il push dei pacchetti di simboli, API NuGet | Microsoft Docs
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Il servizio di pubblicazione consente ai client di pubblicare nuovi pacchetti di simboli.
keywords: Pacchetto di simboli di API NuGet push
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580414"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="5dcd2-104">Eseguire il push dei pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="5dcd2-104">Push Symbol Packages</span></span>

<span data-ttu-id="5dcd2-105">È possibile push dei pacchetti di simboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) tramite l'API di NuGet V3.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="5dcd2-106">Queste operazioni si basano all'esterno della `SymbolPackagePublish` trovare la risorsa nella [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="5dcd2-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="5dcd2-107">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="5dcd2-107">Versioning</span></span>

<span data-ttu-id="5dcd2-108">Nell'esempio `@type` valore viene usato:</span><span class="sxs-lookup"><span data-stu-id="5dcd2-108">The following `@type` value is used:</span></span>

<span data-ttu-id="5dcd2-109">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="5dcd2-109">@type value</span></span>                 | <span data-ttu-id="5dcd2-110">Note</span><span class="sxs-lookup"><span data-stu-id="5dcd2-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="5dcd2-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="5dcd2-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="5dcd2-112">La versione iniziale</span><span class="sxs-lookup"><span data-stu-id="5dcd2-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="5dcd2-113">URL di base</span><span class="sxs-lookup"><span data-stu-id="5dcd2-113">Base URL</span></span>

<span data-ttu-id="5dcd2-114">L'URL di base per le API seguente è il valore della `@id` proprietà del `SymbolPackagePublish/4.9.0` risorsa nell'origine del pacchetto [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="5dcd2-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="5dcd2-115">Per la documentazione seguente, viene usato l'URL di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="5dcd2-116">Prendere in considerazione `https://www.nuget.org/api/v2/symbolpackage` come segnaposto per il `@id` valore trovato nell'indice del servizio.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="5dcd2-117">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="5dcd2-117">HTTP methods</span></span>

<span data-ttu-id="5dcd2-118">Il `PUT` metodo HTTP supportato da questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="5dcd2-119">Push di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="5dcd2-119">Push a symbol package</span></span>

<span data-ttu-id="5dcd2-120">NuGet.org supporta il push dei nuovo formato di pacchetti di simboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) usando l'API seguente.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="5dcd2-121">Pacchetti di simboli con lo stesso ID e versione possono essere inviati più volte.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="5dcd2-122">Un pacchetto di simboli verrà rifiutato nei casi seguenti.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="5dcd2-123">Un pacchetto con lo stesso ID e versione non esiste.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="5dcd2-124">Un pacchetto di simboli con lo stesso ID e versione è stato eseguito il push, ma non ancora pubblicato.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="5dcd2-125">Il pacchetto di simboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) non è valido (vedere [vincoli di pacchetto di simboli](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="5dcd2-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="5dcd2-126">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="5dcd2-126">Request parameters</span></span>

<span data-ttu-id="5dcd2-127">nome</span><span class="sxs-lookup"><span data-stu-id="5dcd2-127">Name</span></span>           | <span data-ttu-id="5dcd2-128">In</span><span class="sxs-lookup"><span data-stu-id="5dcd2-128">In</span></span>     | <span data-ttu-id="5dcd2-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="5dcd2-129">Type</span></span>   | <span data-ttu-id="5dcd2-130">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="5dcd2-130">Required</span></span> | <span data-ttu-id="5dcd2-131">Note</span><span class="sxs-lookup"><span data-stu-id="5dcd2-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="5dcd2-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="5dcd2-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="5dcd2-133">Intestazione</span><span class="sxs-lookup"><span data-stu-id="5dcd2-133">Header</span></span> | <span data-ttu-id="5dcd2-134">stringa</span><span class="sxs-lookup"><span data-stu-id="5dcd2-134">string</span></span> | <span data-ttu-id="5dcd2-135">sì</span><span class="sxs-lookup"><span data-stu-id="5dcd2-135">yes</span></span>      | <span data-ttu-id="5dcd2-136">Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="5dcd2-137">La chiave API è una stringa opaca ricevuto dall'origine del pacchetto dall'utente e configurato nel client.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="5dcd2-138">Nessun formato determinata stringa è obbligatoria, ma la lunghezza della chiave API non deve superare una dimensione ragionevole per i valori delle intestazioni HTTP.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="5dcd2-139">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="5dcd2-139">Request body</span></span>

<span data-ttu-id="5dcd2-140">Il corpo della richiesta per il push di simbolo è uguale a quello con il corpo della richiesta di una richiesta di push del pacchetto (vedere [push del pacchetto ed eliminare](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="5dcd2-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="5dcd2-141">Risposta</span><span class="sxs-lookup"><span data-stu-id="5dcd2-141">Response</span></span>

<span data-ttu-id="5dcd2-142">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="5dcd2-142">Status Code</span></span> | <span data-ttu-id="5dcd2-143">Significato</span><span class="sxs-lookup"><span data-stu-id="5dcd2-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="5dcd2-144">201</span><span class="sxs-lookup"><span data-stu-id="5dcd2-144">201</span></span>         | <span data-ttu-id="5dcd2-145">Il pacchetto di simboli è stato eseguito il push.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="5dcd2-146">400</span><span class="sxs-lookup"><span data-stu-id="5dcd2-146">400</span></span>         | <span data-ttu-id="5dcd2-147">Il pacchetto di simboli specificato non è valido.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="5dcd2-148">401</span><span class="sxs-lookup"><span data-stu-id="5dcd2-148">401</span></span>         | <span data-ttu-id="5dcd2-149">L'utente non è autorizzato a eseguire questa azione.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="5dcd2-150">404</span><span class="sxs-lookup"><span data-stu-id="5dcd2-150">404</span></span>         | <span data-ttu-id="5dcd2-151">Un pacchetto corrispondente con l'ID e la versione specificata non esiste.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="5dcd2-152">409</span><span class="sxs-lookup"><span data-stu-id="5dcd2-152">409</span></span>         | <span data-ttu-id="5dcd2-153">È stato eseguito il push di un pacchetto di simboli con l'ID e versione specificati, ma non è ancora disponibile.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="5dcd2-154">413</span><span class="sxs-lookup"><span data-stu-id="5dcd2-154">413</span></span>         | <span data-ttu-id="5dcd2-155">Il pacchetto è troppo grande.</span><span class="sxs-lookup"><span data-stu-id="5dcd2-155">The package is too large.</span></span>

