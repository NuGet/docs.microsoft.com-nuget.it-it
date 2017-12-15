---
title: Protocolli di NuGet.org | Documenti Microsoft
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba1d9742-9f1c-42ff-8c30-8e953e23c501
description: I protocolli di nuget.org in continua evoluzione per interagire con i client NuGet.
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 097b7a86d056b692c52d6de76bc2fb99d1b58c6f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="9af15-103">Protocolli di NuGet.org</span><span class="sxs-lookup"><span data-stu-id="9af15-103">nuget.org Protocols</span></span>

<span data-ttu-id="9af15-104">Per interagire con nuget.org, è necessario seguire alcuni protocolli client.</span><span class="sxs-lookup"><span data-stu-id="9af15-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="9af15-105">Poiché questi protocolli mantengono in evoluzione, i client devono identificare la versione del protocollo che usano durante la chiamata API di nuget.org specifico.</span><span class="sxs-lookup"><span data-stu-id="9af15-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="9af15-106">In questo modo nuget.org introdurre modifiche in modo non è importante per i client precedenti.</span><span class="sxs-lookup"><span data-stu-id="9af15-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="9af15-107">Le API illustrate in questa pagina sono specifiche di nuget.org e vi è alcuna aspettativa per altre implementazioni di server NuGet introdurre tali API.</span><span class="sxs-lookup"><span data-stu-id="9af15-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="9af15-108">Per informazioni sull'API NuGet implementato su vasta scala nell'ecosistema NuGet, vedere il [panoramica dell'API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="9af15-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="9af15-109">Questo argomento elenca i vari protocolli come e quando si collegano a esistenza.</span><span class="sxs-lookup"><span data-stu-id="9af15-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="9af15-110">Versione del protocollo NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="9af15-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="9af15-111">Il 4.1.0 protocollo specifica l'utilizzo di chiavi di ambito verificare per interagire con i servizi diversi da nuget.org, per convalidare un pacchetto con un account di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9af15-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="9af15-112">Si noti che il `4.1.0` versione numero è una stringa opaca, ma si verifica in genere coincidano con la prima versione del client NuGet ufficiale che questo protocollo è supportato.</span><span class="sxs-lookup"><span data-stu-id="9af15-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="9af15-113">La convalida garantisce che le chiavi API creati dall'utente vengono utilizzate solo con nuget.org e che altri verifica o convalida da un servizio di terze parti viene gestita tramite una chiave di ambito verificare usato una sola volta.</span><span class="sxs-lookup"><span data-stu-id="9af15-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="9af15-114">Queste chiavi ambito verificare utilizzabile per convalidare che il pacchetto appartiene a un determinato utente (account) in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9af15-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="9af15-115">Requisiti client</span><span class="sxs-lookup"><span data-stu-id="9af15-115">Client requirement</span></span>

<span data-ttu-id="9af15-116">I client devono passare l'intestazione seguente quando si effettuano chiamate API per **push** pacchetti nuget.org:</span><span class="sxs-lookup"><span data-stu-id="9af15-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="9af15-117">Si noti che la pre-esistente `X-NuGet-Client-Version` intestazione ha la stessa funzione, ma ora è deprecata e non deve più essere usato.</span><span class="sxs-lookup"><span data-stu-id="9af15-117">Note that the pre-existing `X-NuGet-Client-Version` header has the same purpose but is now deprecated and should no longer be used.</span></span>

<span data-ttu-id="9af15-118">Il **push** protocollo stesso è descritto nella documentazione per il [ `PackagePublish` risorse](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="9af15-118">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="9af15-119">Se un client interagisce con servizi esterni è necessario per convalidare un pacchetto appartiene a un determinato utente (account), deve utilizzare il protocollo seguente ed utilizzare le chiavi di verifica all'ambito e non le chiavi API di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9af15-119">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="9af15-120">API per richiedere una chiave di verifica dell'ambito</span><span class="sxs-lookup"><span data-stu-id="9af15-120">API to request a verify-scope key</span></span>

<span data-ttu-id="9af15-121">Questa API viene usata per ottenere una chiave di verifica con ambito di un autore di nuget.org convalidare un pacchetto di proprietà di quest'ultimo.</span><span class="sxs-lookup"><span data-stu-id="9af15-121">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="9af15-122">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="9af15-122">Request parameters</span></span>

<span data-ttu-id="9af15-123">Nome</span><span class="sxs-lookup"><span data-stu-id="9af15-123">Name</span></span>           | <span data-ttu-id="9af15-124">In</span><span class="sxs-lookup"><span data-stu-id="9af15-124">In</span></span>     | <span data-ttu-id="9af15-125">Tipo</span><span class="sxs-lookup"><span data-stu-id="9af15-125">Type</span></span>   | <span data-ttu-id="9af15-126">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="9af15-126">Required</span></span> | <span data-ttu-id="9af15-127">Note</span><span class="sxs-lookup"><span data-stu-id="9af15-127">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="9af15-128">Id</span><span class="sxs-lookup"><span data-stu-id="9af15-128">ID</span></span>             | <span data-ttu-id="9af15-129">URL</span><span class="sxs-lookup"><span data-stu-id="9af15-129">URL</span></span>    | <span data-ttu-id="9af15-130">string</span><span class="sxs-lookup"><span data-stu-id="9af15-130">string</span></span> | <span data-ttu-id="9af15-131">sì</span><span class="sxs-lookup"><span data-stu-id="9af15-131">yes</span></span>      | <span data-ttu-id="9af15-132">Identidier il pacchetto per il quale viene richiesta la chiave di verifica ambito</span><span class="sxs-lookup"><span data-stu-id="9af15-132">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="9af15-133">VERSION</span><span class="sxs-lookup"><span data-stu-id="9af15-133">VERSION</span></span>        | <span data-ttu-id="9af15-134">URL</span><span class="sxs-lookup"><span data-stu-id="9af15-134">URL</span></span>    | <span data-ttu-id="9af15-135">string</span><span class="sxs-lookup"><span data-stu-id="9af15-135">string</span></span> | <span data-ttu-id="9af15-136">No</span><span class="sxs-lookup"><span data-stu-id="9af15-136">no</span></span>       | <span data-ttu-id="9af15-137">La versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9af15-137">The package version</span></span>
<span data-ttu-id="9af15-138">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="9af15-138">X-NuGet-ApiKey</span></span> | <span data-ttu-id="9af15-139">Header</span><span class="sxs-lookup"><span data-stu-id="9af15-139">Header</span></span> | <span data-ttu-id="9af15-140">string</span><span class="sxs-lookup"><span data-stu-id="9af15-140">string</span></span> | <span data-ttu-id="9af15-141">sì</span><span class="sxs-lookup"><span data-stu-id="9af15-141">yes</span></span>      | <span data-ttu-id="9af15-142">Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="9af15-142">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="9af15-143">Risposta</span><span class="sxs-lookup"><span data-stu-id="9af15-143">Response</span></span>

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="9af15-144">API per verificare la chiave di verifica ambito</span><span class="sxs-lookup"><span data-stu-id="9af15-144">API to verify the verify scope key</span></span>

<span data-ttu-id="9af15-145">Questa API viene usata per convalidare una chiave di verifica ambito per il pacchetto dall'autore del nuget.org di proprietà.</span><span class="sxs-lookup"><span data-stu-id="9af15-145">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="9af15-146">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="9af15-146">Request parameters</span></span>

<span data-ttu-id="9af15-147">Nome</span><span class="sxs-lookup"><span data-stu-id="9af15-147">Name</span></span>           | <span data-ttu-id="9af15-148">In</span><span class="sxs-lookup"><span data-stu-id="9af15-148">In</span></span>     | <span data-ttu-id="9af15-149">Tipo</span><span class="sxs-lookup"><span data-stu-id="9af15-149">Type</span></span>   | <span data-ttu-id="9af15-150">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="9af15-150">Required</span></span> | <span data-ttu-id="9af15-151">Note</span><span class="sxs-lookup"><span data-stu-id="9af15-151">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="9af15-152">Id</span><span class="sxs-lookup"><span data-stu-id="9af15-152">ID</span></span>             | <span data-ttu-id="9af15-153">URL</span><span class="sxs-lookup"><span data-stu-id="9af15-153">URL</span></span>    | <span data-ttu-id="9af15-154">string</span><span class="sxs-lookup"><span data-stu-id="9af15-154">string</span></span> | <span data-ttu-id="9af15-155">sì</span><span class="sxs-lookup"><span data-stu-id="9af15-155">yes</span></span>      | <span data-ttu-id="9af15-156">L'identificatore del pacchetto per il quale viene richiesta la chiave di verifica ambito</span><span class="sxs-lookup"><span data-stu-id="9af15-156">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="9af15-157">VERSION</span><span class="sxs-lookup"><span data-stu-id="9af15-157">VERSION</span></span>        | <span data-ttu-id="9af15-158">URL</span><span class="sxs-lookup"><span data-stu-id="9af15-158">URL</span></span>    | <span data-ttu-id="9af15-159">string</span><span class="sxs-lookup"><span data-stu-id="9af15-159">string</span></span> | <span data-ttu-id="9af15-160">No</span><span class="sxs-lookup"><span data-stu-id="9af15-160">no</span></span>       | <span data-ttu-id="9af15-161">La versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9af15-161">The package version</span></span>
<span data-ttu-id="9af15-162">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="9af15-162">X-NuGet-ApiKey</span></span> | <span data-ttu-id="9af15-163">Header</span><span class="sxs-lookup"><span data-stu-id="9af15-163">Header</span></span> | <span data-ttu-id="9af15-164">string</span><span class="sxs-lookup"><span data-stu-id="9af15-164">string</span></span> | <span data-ttu-id="9af15-165">sì</span><span class="sxs-lookup"><span data-stu-id="9af15-165">yes</span></span>      | <span data-ttu-id="9af15-166">Ad esempio, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="9af15-166">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="9af15-167">Questa chiave API ambito verifica scadenza ora del giorno o al primo utilizzo, qualunque si verifichi prima.</span><span class="sxs-lookup"><span data-stu-id="9af15-167">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="9af15-168">Risposta</span><span class="sxs-lookup"><span data-stu-id="9af15-168">Response</span></span>

<span data-ttu-id="9af15-169">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="9af15-169">Status Code</span></span> | <span data-ttu-id="9af15-170">Significato</span><span class="sxs-lookup"><span data-stu-id="9af15-170">Meaning</span></span>
----------- | -------
<span data-ttu-id="9af15-171">200</span><span class="sxs-lookup"><span data-stu-id="9af15-171">200</span></span>         | <span data-ttu-id="9af15-172">La chiave API è valida</span><span class="sxs-lookup"><span data-stu-id="9af15-172">The API key is valid</span></span>
<span data-ttu-id="9af15-173">403</span><span class="sxs-lookup"><span data-stu-id="9af15-173">403</span></span>         | <span data-ttu-id="9af15-174">La chiave API non è valido o non autorizzato per effettuare il push per il pacchetto</span><span class="sxs-lookup"><span data-stu-id="9af15-174">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="9af15-175">404</span><span class="sxs-lookup"><span data-stu-id="9af15-175">404</span></span>         | <span data-ttu-id="9af15-176">Il pacchetto a cui fa riferimento a `ID` e `VERSION` (facoltativo) non esiste</span><span class="sxs-lookup"><span data-stu-id="9af15-176">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
