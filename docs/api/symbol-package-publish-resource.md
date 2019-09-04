---
title: Pacchetti di simboli push, API NuGet | Microsoft Docs
author: cristinamanum
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Il servizio Publish consente ai client di pubblicare nuovi pacchetti di simboli.
keywords: Pacchetto di simboli push dell'API NuGet
ms.reviewer: karann
ms.openlocfilehash: 27e557bf15ce31152243a409eddc4112eeb6c38b
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235112"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="9f686-104">Pacchetti di simboli push</span><span class="sxs-lookup"><span data-stu-id="9f686-104">Push Symbol Packages</span></span>

<span data-ttu-id="9f686-105">È possibile eseguire il push dei pacchetti di simboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) usando l'API NuGet V3.</span><span class="sxs-lookup"><span data-stu-id="9f686-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="9f686-106">Queste operazioni sono basate `SymbolPackagePublish` sulla risorsa presente nell'indice del [servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="9f686-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="9f686-107">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="9f686-107">Versioning</span></span>

<span data-ttu-id="9f686-108">Viene utilizzato `@type` il valore seguente:</span><span class="sxs-lookup"><span data-stu-id="9f686-108">The following `@type` value is used:</span></span>

<span data-ttu-id="9f686-109">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="9f686-109">@type value</span></span>                 | <span data-ttu-id="9f686-110">Note</span><span class="sxs-lookup"><span data-stu-id="9f686-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="9f686-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="9f686-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="9f686-112">Versione iniziale</span><span class="sxs-lookup"><span data-stu-id="9f686-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="9f686-113">URL di base</span><span class="sxs-lookup"><span data-stu-id="9f686-113">Base URL</span></span>

<span data-ttu-id="9f686-114">L'URL di base per le API seguenti è il valore della `@id` proprietà `SymbolPackagePublish/4.9.0` della risorsa nell' [indice del servizio](service-index.md)dell'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9f686-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="9f686-115">Per la documentazione riportata di seguito, viene usato l'URL di NuGet. org.</span><span class="sxs-lookup"><span data-stu-id="9f686-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="9f686-116">Considerare `https://www.nuget.org/api/v2/symbolpackage` come un segnaposto per `@id` il valore trovato nell'indice del servizio.</span><span class="sxs-lookup"><span data-stu-id="9f686-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="9f686-117">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="9f686-117">HTTP methods</span></span>

<span data-ttu-id="9f686-118">Il `PUT` metodo HTTP è supportato da questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="9f686-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="9f686-119">Eseguire il push di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="9f686-119">Push a symbol package</span></span>

<span data-ttu-id="9f686-120">nuget.org supporta il push del nuovo formato dei pacchetti di simboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) usando l'API seguente.</span><span class="sxs-lookup"><span data-stu-id="9f686-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="9f686-121">I pacchetti di simboli con lo stesso ID e la stessa versione possono essere inviati più volte.</span><span class="sxs-lookup"><span data-stu-id="9f686-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="9f686-122">Un pacchetto di simboli verrà rifiutato nei casi seguenti.</span><span class="sxs-lookup"><span data-stu-id="9f686-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="9f686-123">Non esiste un pacchetto con lo stesso ID e la stessa versione.</span><span class="sxs-lookup"><span data-stu-id="9f686-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="9f686-124">È stato eseguito il push di un pacchetto di simboli con lo stesso ID e la stessa versione ma non è ancora pubblicato.</span><span class="sxs-lookup"><span data-stu-id="9f686-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="9f686-125">Il pacchetto di simboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) non è valido (vedere [vincoli dei pacchetti di simboli](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="9f686-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="9f686-126">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="9f686-126">Request parameters</span></span>

<span data-ttu-id="9f686-127">Name</span><span class="sxs-lookup"><span data-stu-id="9f686-127">Name</span></span>           | <span data-ttu-id="9f686-128">In</span><span class="sxs-lookup"><span data-stu-id="9f686-128">In</span></span>     | <span data-ttu-id="9f686-129">Type</span><span class="sxs-lookup"><span data-stu-id="9f686-129">Type</span></span>   | <span data-ttu-id="9f686-130">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="9f686-130">Required</span></span> | <span data-ttu-id="9f686-131">Note</span><span class="sxs-lookup"><span data-stu-id="9f686-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="9f686-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="9f686-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="9f686-133">Intestazione</span><span class="sxs-lookup"><span data-stu-id="9f686-133">Header</span></span> | <span data-ttu-id="9f686-134">string</span><span class="sxs-lookup"><span data-stu-id="9f686-134">string</span></span> | <span data-ttu-id="9f686-135">sì</span><span class="sxs-lookup"><span data-stu-id="9f686-135">yes</span></span>      | <span data-ttu-id="9f686-136">Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="9f686-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="9f686-137">La chiave API è una stringa opaca ottenuta dall'origine del pacchetto dall'utente e configurata nel client.</span><span class="sxs-lookup"><span data-stu-id="9f686-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="9f686-138">Non è richiesto alcun formato stringa particolare, ma la lunghezza della chiave API non deve superare una dimensione ragionevole per i valori dell'intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="9f686-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="9f686-139">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="9f686-139">Request body</span></span>

<span data-ttu-id="9f686-140">Il corpo della richiesta per il push dei simboli è uguale al corpo della richiesta di una richiesta di push del pacchetto (vedere [push e eliminazione di pacchetti](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="9f686-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="9f686-141">Risposta</span><span class="sxs-lookup"><span data-stu-id="9f686-141">Response</span></span>

<span data-ttu-id="9f686-142">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="9f686-142">Status Code</span></span> | <span data-ttu-id="9f686-143">Significato</span><span class="sxs-lookup"><span data-stu-id="9f686-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="9f686-144">201</span><span class="sxs-lookup"><span data-stu-id="9f686-144">201</span></span>         | <span data-ttu-id="9f686-145">Push del pacchetto di simboli completato.</span><span class="sxs-lookup"><span data-stu-id="9f686-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="9f686-146">400</span><span class="sxs-lookup"><span data-stu-id="9f686-146">400</span></span>         | <span data-ttu-id="9f686-147">Il pacchetto di simboli specificato non è valido.</span><span class="sxs-lookup"><span data-stu-id="9f686-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="9f686-148">401</span><span class="sxs-lookup"><span data-stu-id="9f686-148">401</span></span>         | <span data-ttu-id="9f686-149">L'utente non è autorizzato a eseguire questa azione.</span><span class="sxs-lookup"><span data-stu-id="9f686-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="9f686-150">404</span><span class="sxs-lookup"><span data-stu-id="9f686-150">404</span></span>         | <span data-ttu-id="9f686-151">Non esiste un pacchetto corrispondente con l'ID e la versione specificati.</span><span class="sxs-lookup"><span data-stu-id="9f686-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="9f686-152">409</span><span class="sxs-lookup"><span data-stu-id="9f686-152">409</span></span>         | <span data-ttu-id="9f686-153">È stato eseguito il push di un pacchetto di simboli con l'ID e la versione specificati, che tuttavia non è ancora disponibile.</span><span class="sxs-lookup"><span data-stu-id="9f686-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="9f686-154">413</span><span class="sxs-lookup"><span data-stu-id="9f686-154">413</span></span>         | <span data-ttu-id="9f686-155">Il pacchetto è troppo grande.</span><span class="sxs-lookup"><span data-stu-id="9f686-155">The package is too large.</span></span>

