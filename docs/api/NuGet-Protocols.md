---
title: Protocolli nuget.org
description: Protocolli nuget.org in evoluzione per interagire con i client NuGet.
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773971"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="9513f-103">Protocolli di nuget.org</span><span class="sxs-lookup"><span data-stu-id="9513f-103">nuget.org protocols</span></span>

<span data-ttu-id="9513f-104">Per interagire con nuget.org, è necessario che i client seguano alcuni protocolli.</span><span class="sxs-lookup"><span data-stu-id="9513f-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="9513f-105">Poiché questi protocolli continuano a evolversi, i client devono identificare la versione del protocollo che usano quando chiamano API nuget.org specifiche.</span><span class="sxs-lookup"><span data-stu-id="9513f-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="9513f-106">Ciò consente a nuget.org di introdurre modifiche in modo non sostanziale per i client precedenti.</span><span class="sxs-lookup"><span data-stu-id="9513f-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="9513f-107">Le API documentate in questa pagina sono specifiche per nuget.org e non è previsto che altre implementazioni di server NuGet introducano queste API.</span><span class="sxs-lookup"><span data-stu-id="9513f-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="9513f-108">Per informazioni sull'API NuGet implementata a livello generale nell'ecosistema NuGet, vedere [Panoramica dell'API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="9513f-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="9513f-109">In questo argomento vengono elencati diversi protocolli come e quando sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="9513f-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="9513f-110">Versione del protocollo NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="9513f-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="9513f-111">Il protocollo 4.1.0 specifica l'uso delle chiavi Verify-scope per interagire con i servizi diversi da nuget.org per convalidare un pacchetto con un account nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9513f-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="9513f-112">Si noti che il `4.1.0` numero di versione è una stringa opaca, ma che coincide con la prima versione del client NuGet ufficiale che supporta questo protocollo.</span><span class="sxs-lookup"><span data-stu-id="9513f-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="9513f-113">La convalida garantisce che le chiavi API create dall'utente vengano utilizzate solo con nuget.org e che la verifica o la convalida da parte di un servizio di terze parti venga gestita tramite le chiavi monouso Verify-scope.</span><span class="sxs-lookup"><span data-stu-id="9513f-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="9513f-114">Queste chiavi Verify-scope possono essere usate per convalidare che il pacchetto appartenga a un determinato utente (account) in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9513f-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="9513f-115">Requisito client</span><span class="sxs-lookup"><span data-stu-id="9513f-115">Client requirement</span></span>

<span data-ttu-id="9513f-116">È necessario che i client passino l'intestazione seguente quando eseguono chiamate API per eseguire il **push** dei pacchetti in NuGet.org:</span><span class="sxs-lookup"><span data-stu-id="9513f-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="9513f-117">Si noti che l' `X-NuGet-Client-Version` intestazione ha una semantica simile, ma è riservata a essere usata solo dal client NuGet ufficiale.</span><span class="sxs-lookup"><span data-stu-id="9513f-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="9513f-118">I client di terze parti devono usare l' `X-NuGet-Protocol-Version` intestazione e il valore.</span><span class="sxs-lookup"><span data-stu-id="9513f-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="9513f-119">Il protocollo di **push** è descritto nella documentazione relativa alla [ `PackagePublish` risorsa](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="9513f-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="9513f-120">Se un client interagisce con i servizi esterni e deve verificare se un pacchetto appartiene a un determinato utente (account), deve usare il protocollo seguente e usare le chiavi Verify-scope e non le chiavi API da nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9513f-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="9513f-121">API per richiedere una chiave Verify-scope</span><span class="sxs-lookup"><span data-stu-id="9513f-121">API to request a verify-scope key</span></span>

<span data-ttu-id="9513f-122">Questa API viene usata per ottenere una chiave Verify-scope per un autore di nuget.org per convalidare un pacchetto di proprietà di loro.</span><span class="sxs-lookup"><span data-stu-id="9513f-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="9513f-123">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="9513f-123">Request parameters</span></span>

<span data-ttu-id="9513f-124">Nome</span><span class="sxs-lookup"><span data-stu-id="9513f-124">Name</span></span>           | <span data-ttu-id="9513f-125">In</span><span class="sxs-lookup"><span data-stu-id="9513f-125">In</span></span>     | <span data-ttu-id="9513f-126">Type</span><span class="sxs-lookup"><span data-stu-id="9513f-126">Type</span></span>   | <span data-ttu-id="9513f-127">Necessario</span><span class="sxs-lookup"><span data-stu-id="9513f-127">Required</span></span> | <span data-ttu-id="9513f-128">Note</span><span class="sxs-lookup"><span data-stu-id="9513f-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="9513f-129">ID</span><span class="sxs-lookup"><span data-stu-id="9513f-129">ID</span></span>             | <span data-ttu-id="9513f-130">URL</span><span class="sxs-lookup"><span data-stu-id="9513f-130">URL</span></span>    | <span data-ttu-id="9513f-131">string</span><span class="sxs-lookup"><span data-stu-id="9513f-131">string</span></span> | <span data-ttu-id="9513f-132">sì</span><span class="sxs-lookup"><span data-stu-id="9513f-132">yes</span></span>      | <span data-ttu-id="9513f-133">Identidier del pacchetto per il quale viene richiesta la chiave di ambito Verify</span><span class="sxs-lookup"><span data-stu-id="9513f-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="9513f-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="9513f-134">VERSION</span></span>        | <span data-ttu-id="9513f-135">URL</span><span class="sxs-lookup"><span data-stu-id="9513f-135">URL</span></span>    | <span data-ttu-id="9513f-136">string</span><span class="sxs-lookup"><span data-stu-id="9513f-136">string</span></span> | <span data-ttu-id="9513f-137">no</span><span class="sxs-lookup"><span data-stu-id="9513f-137">no</span></span>       | <span data-ttu-id="9513f-138">Versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9513f-138">The package version</span></span>
<span data-ttu-id="9513f-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="9513f-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="9513f-140">Intestazione</span><span class="sxs-lookup"><span data-stu-id="9513f-140">Header</span></span> | <span data-ttu-id="9513f-141">string</span><span class="sxs-lookup"><span data-stu-id="9513f-141">string</span></span> | <span data-ttu-id="9513f-142">sì</span><span class="sxs-lookup"><span data-stu-id="9513f-142">yes</span></span>      | <span data-ttu-id="9513f-143">Ad esempio: `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="9513f-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="9513f-144">Risposta</span><span class="sxs-lookup"><span data-stu-id="9513f-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="9513f-145">API per verificare la chiave dell'ambito Verify</span><span class="sxs-lookup"><span data-stu-id="9513f-145">API to verify the verify scope key</span></span>

<span data-ttu-id="9513f-146">Questa API viene usata per convalidare una chiave Verify-scope per il pacchetto di proprietà dell'autore nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9513f-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="9513f-147">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="9513f-147">Request parameters</span></span>

<span data-ttu-id="9513f-148">Nome</span><span class="sxs-lookup"><span data-stu-id="9513f-148">Name</span></span>           | <span data-ttu-id="9513f-149">In</span><span class="sxs-lookup"><span data-stu-id="9513f-149">In</span></span>     | <span data-ttu-id="9513f-150">Type</span><span class="sxs-lookup"><span data-stu-id="9513f-150">Type</span></span>   | <span data-ttu-id="9513f-151">Necessario</span><span class="sxs-lookup"><span data-stu-id="9513f-151">Required</span></span> | <span data-ttu-id="9513f-152">Note</span><span class="sxs-lookup"><span data-stu-id="9513f-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="9513f-153">ID</span><span class="sxs-lookup"><span data-stu-id="9513f-153">ID</span></span>             | <span data-ttu-id="9513f-154">URL</span><span class="sxs-lookup"><span data-stu-id="9513f-154">URL</span></span>    | <span data-ttu-id="9513f-155">string</span><span class="sxs-lookup"><span data-stu-id="9513f-155">string</span></span> | <span data-ttu-id="9513f-156">sì</span><span class="sxs-lookup"><span data-stu-id="9513f-156">yes</span></span>      | <span data-ttu-id="9513f-157">Identificatore del pacchetto per il quale viene richiesta la chiave di ambito Verify</span><span class="sxs-lookup"><span data-stu-id="9513f-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="9513f-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="9513f-158">VERSION</span></span>        | <span data-ttu-id="9513f-159">URL</span><span class="sxs-lookup"><span data-stu-id="9513f-159">URL</span></span>    | <span data-ttu-id="9513f-160">string</span><span class="sxs-lookup"><span data-stu-id="9513f-160">string</span></span> | <span data-ttu-id="9513f-161">no</span><span class="sxs-lookup"><span data-stu-id="9513f-161">no</span></span>       | <span data-ttu-id="9513f-162">Versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="9513f-162">The package version</span></span>
<span data-ttu-id="9513f-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="9513f-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="9513f-164">Intestazione</span><span class="sxs-lookup"><span data-stu-id="9513f-164">Header</span></span> | <span data-ttu-id="9513f-165">string</span><span class="sxs-lookup"><span data-stu-id="9513f-165">string</span></span> | <span data-ttu-id="9513f-166">sì</span><span class="sxs-lookup"><span data-stu-id="9513f-166">yes</span></span>      | <span data-ttu-id="9513f-167">Ad esempio: `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="9513f-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="9513f-168">Questa chiave API dell'ambito di verifica scade entro un giorno o al primo utilizzo, a seconda di quale si verifica per primo.</span><span class="sxs-lookup"><span data-stu-id="9513f-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="9513f-169">Risposta</span><span class="sxs-lookup"><span data-stu-id="9513f-169">Response</span></span>

<span data-ttu-id="9513f-170">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="9513f-170">Status Code</span></span> | <span data-ttu-id="9513f-171">Significato</span><span class="sxs-lookup"><span data-stu-id="9513f-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="9513f-172">200</span><span class="sxs-lookup"><span data-stu-id="9513f-172">200</span></span>         | <span data-ttu-id="9513f-173">La chiave API è valida</span><span class="sxs-lookup"><span data-stu-id="9513f-173">The API key is valid</span></span>
<span data-ttu-id="9513f-174">403</span><span class="sxs-lookup"><span data-stu-id="9513f-174">403</span></span>         | <span data-ttu-id="9513f-175">La chiave API non è valida o non è autorizzata a eseguire il push sul pacchetto</span><span class="sxs-lookup"><span data-stu-id="9513f-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="9513f-176">404</span><span class="sxs-lookup"><span data-stu-id="9513f-176">404</span></span>         | <span data-ttu-id="9513f-177">Il pacchetto a cui `ID` fa riferimento e `VERSION` (facoltativo) non esiste</span><span class="sxs-lookup"><span data-stu-id="9513f-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
