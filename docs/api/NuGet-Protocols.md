---
title: Protocolli di NuGet.org
description: I protocolli di nuget.org in continua evoluzione per interagire con i client NuGet.
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547273"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="79c60-103">protocolli di NuGet.org</span><span class="sxs-lookup"><span data-stu-id="79c60-103">nuget.org protocols</span></span>

<span data-ttu-id="79c60-104">Per interagire con nuget.org, è necessario seguire alcuni protocolli client.</span><span class="sxs-lookup"><span data-stu-id="79c60-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="79c60-105">Perché mantengano in continua evoluzione di questi protocolli, i client devono identificare la versione del protocollo che usano quando si chiamano le API di nuget.org specifico.</span><span class="sxs-lookup"><span data-stu-id="79c60-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="79c60-106">In questo modo nuget.org per introdurre le modifiche in modo non di rilievo per i client precedenti.</span><span class="sxs-lookup"><span data-stu-id="79c60-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="79c60-107">Le API illustrate in questa pagina sono specifiche di nuget.org e vi è alcuna aspettativa per altre implementazioni di server NuGet per introdurre queste API.</span><span class="sxs-lookup"><span data-stu-id="79c60-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="79c60-108">Per informazioni sull'API NuGet implementato su vasta scala nell'ecosistema NuGet, vedere la [panoramica dell'API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="79c60-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="79c60-109">Questo argomento elenca i vari protocolli come e quando diventano di esistenza.</span><span class="sxs-lookup"><span data-stu-id="79c60-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="79c60-110">Versione del protocollo NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="79c60-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="79c60-111">La 4.1.0 protocollo specifica dell'utilizzo delle chiavi di verifica dell'ambito per interagire con servizi diversi da nuget.org, per convalidare un pacchetto in un account di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="79c60-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="79c60-112">Si noti che il `4.1.0` versione numero è una stringa opaca ma coincide con la prima versione del client NuGet ufficiale che questo protocollo è supportato.</span><span class="sxs-lookup"><span data-stu-id="79c60-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="79c60-113">La convalida garantisce che le chiavi API create dall'utente vengono utilizzate solo con nuget.org e che altri verifica o convalida da un servizio di terze parti viene gestita tramite una chiave di ambito verificare usato una sola volta.</span><span class="sxs-lookup"><span data-stu-id="79c60-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="79c60-114">Queste chiavi verificare ambito sono utilizzabile per verificare che il pacchetto appartiene a un determinato utente (account) in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="79c60-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="79c60-115">Requisiti del client</span><span class="sxs-lookup"><span data-stu-id="79c60-115">Client requirement</span></span>

<span data-ttu-id="79c60-116">I client devono passare l'intestazione seguente quando si effettuano chiamate all'API **push** pacchetti da nuget.org:</span><span class="sxs-lookup"><span data-stu-id="79c60-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

    X-NuGet-Protocol-Version: 4.1.0

<span data-ttu-id="79c60-117">Si noti che il `X-NuGet-Client-Version` intestazione ha una semantica simile ma è riservata per essere utilizzato solo dai client NuGet ufficiale.</span><span class="sxs-lookup"><span data-stu-id="79c60-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="79c60-118">I client di terze parti devono usare il `X-NuGet-Protocol-Version` intestazione e il valore.</span><span class="sxs-lookup"><span data-stu-id="79c60-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="79c60-119">Il **push** protocollo stesso è descritto nella documentazione per il [ `PackagePublish` risorsa](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="79c60-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="79c60-120">Se un client interagisce con servizi esterni e deve verificare se un pacchetto a cui appartiene un determinato utente (account), dovrebbe usare il protocollo seguente e usare le chiavi di verifica-ambito e non le chiavi API da nuget.org.</span><span class="sxs-lookup"><span data-stu-id="79c60-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="79c60-121">Per richiedere una chiave di verifica dell'ambito dell'API</span><span class="sxs-lookup"><span data-stu-id="79c60-121">API to request a verify-scope key</span></span>

<span data-ttu-id="79c60-122">Questa API viene usata per ottenere una chiave di verifica dall'ambito di un autore di nuget.org convalidare un pacchetto di proprietà di quest'ultimo.</span><span class="sxs-lookup"><span data-stu-id="79c60-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="79c60-123">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="79c60-123">Request parameters</span></span>

<span data-ttu-id="79c60-124">nome</span><span class="sxs-lookup"><span data-stu-id="79c60-124">Name</span></span>           | <span data-ttu-id="79c60-125">In</span><span class="sxs-lookup"><span data-stu-id="79c60-125">In</span></span>     | <span data-ttu-id="79c60-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="79c60-126">Type</span></span>   | <span data-ttu-id="79c60-127">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="79c60-127">Required</span></span> | <span data-ttu-id="79c60-128">Note</span><span class="sxs-lookup"><span data-stu-id="79c60-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="79c60-129">Id</span><span class="sxs-lookup"><span data-stu-id="79c60-129">ID</span></span>             | <span data-ttu-id="79c60-130">URL</span><span class="sxs-lookup"><span data-stu-id="79c60-130">URL</span></span>    | <span data-ttu-id="79c60-131">stringa</span><span class="sxs-lookup"><span data-stu-id="79c60-131">string</span></span> | <span data-ttu-id="79c60-132">sì</span><span class="sxs-lookup"><span data-stu-id="79c60-132">yes</span></span>      | <span data-ttu-id="79c60-133">Identidier il pacchetto per il quale viene richiesta la chiave di ambito di verifica</span><span class="sxs-lookup"><span data-stu-id="79c60-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="79c60-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="79c60-134">VERSION</span></span>        | <span data-ttu-id="79c60-135">URL</span><span class="sxs-lookup"><span data-stu-id="79c60-135">URL</span></span>    | <span data-ttu-id="79c60-136">stringa</span><span class="sxs-lookup"><span data-stu-id="79c60-136">string</span></span> | <span data-ttu-id="79c60-137">No</span><span class="sxs-lookup"><span data-stu-id="79c60-137">no</span></span>       | <span data-ttu-id="79c60-138">La versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="79c60-138">The package version</span></span>
<span data-ttu-id="79c60-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="79c60-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="79c60-140">Header</span><span class="sxs-lookup"><span data-stu-id="79c60-140">Header</span></span> | <span data-ttu-id="79c60-141">stringa</span><span class="sxs-lookup"><span data-stu-id="79c60-141">string</span></span> | <span data-ttu-id="79c60-142">sì</span><span class="sxs-lookup"><span data-stu-id="79c60-142">yes</span></span>      | <span data-ttu-id="79c60-143">Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="79c60-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="79c60-144">Risposta</span><span class="sxs-lookup"><span data-stu-id="79c60-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="79c60-145">API per verificare la chiave di verifica ambito</span><span class="sxs-lookup"><span data-stu-id="79c60-145">API to verify the verify scope key</span></span>

<span data-ttu-id="79c60-146">Questa API viene usata per convalidare una chiave di verifica dell'ambito per il pacchetto di proprietà dell'autore di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="79c60-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="79c60-147">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="79c60-147">Request parameters</span></span>

<span data-ttu-id="79c60-148">nome</span><span class="sxs-lookup"><span data-stu-id="79c60-148">Name</span></span>           | <span data-ttu-id="79c60-149">In</span><span class="sxs-lookup"><span data-stu-id="79c60-149">In</span></span>     | <span data-ttu-id="79c60-150">Tipo</span><span class="sxs-lookup"><span data-stu-id="79c60-150">Type</span></span>   | <span data-ttu-id="79c60-151">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="79c60-151">Required</span></span> | <span data-ttu-id="79c60-152">Note</span><span class="sxs-lookup"><span data-stu-id="79c60-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="79c60-153">Id</span><span class="sxs-lookup"><span data-stu-id="79c60-153">ID</span></span>             | <span data-ttu-id="79c60-154">URL</span><span class="sxs-lookup"><span data-stu-id="79c60-154">URL</span></span>    | <span data-ttu-id="79c60-155">stringa</span><span class="sxs-lookup"><span data-stu-id="79c60-155">string</span></span> | <span data-ttu-id="79c60-156">sì</span><span class="sxs-lookup"><span data-stu-id="79c60-156">yes</span></span>      | <span data-ttu-id="79c60-157">L'identificatore del pacchetto per il quale viene richiesta la chiave di ambito di verifica</span><span class="sxs-lookup"><span data-stu-id="79c60-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="79c60-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="79c60-158">VERSION</span></span>        | <span data-ttu-id="79c60-159">URL</span><span class="sxs-lookup"><span data-stu-id="79c60-159">URL</span></span>    | <span data-ttu-id="79c60-160">stringa</span><span class="sxs-lookup"><span data-stu-id="79c60-160">string</span></span> | <span data-ttu-id="79c60-161">No</span><span class="sxs-lookup"><span data-stu-id="79c60-161">no</span></span>       | <span data-ttu-id="79c60-162">La versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="79c60-162">The package version</span></span>
<span data-ttu-id="79c60-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="79c60-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="79c60-164">Header</span><span class="sxs-lookup"><span data-stu-id="79c60-164">Header</span></span> | <span data-ttu-id="79c60-165">stringa</span><span class="sxs-lookup"><span data-stu-id="79c60-165">string</span></span> | <span data-ttu-id="79c60-166">sì</span><span class="sxs-lookup"><span data-stu-id="79c60-166">yes</span></span>      | <span data-ttu-id="79c60-167">Ad esempio, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="79c60-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="79c60-168">Questo tasto di ambito API verifica scade tra ora del giorno o al primo utilizzo, a seconda di quale si verifica per primo.</span><span class="sxs-lookup"><span data-stu-id="79c60-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="79c60-169">Risposta</span><span class="sxs-lookup"><span data-stu-id="79c60-169">Response</span></span>

<span data-ttu-id="79c60-170">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="79c60-170">Status Code</span></span> | <span data-ttu-id="79c60-171">Significato</span><span class="sxs-lookup"><span data-stu-id="79c60-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="79c60-172">200</span><span class="sxs-lookup"><span data-stu-id="79c60-172">200</span></span>         | <span data-ttu-id="79c60-173">La chiave API è valida</span><span class="sxs-lookup"><span data-stu-id="79c60-173">The API key is valid</span></span>
<span data-ttu-id="79c60-174">403</span><span class="sxs-lookup"><span data-stu-id="79c60-174">403</span></span>         | <span data-ttu-id="79c60-175">La chiave API non è valido o non autorizzato a eseguire il push per il pacchetto</span><span class="sxs-lookup"><span data-stu-id="79c60-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="79c60-176">404</span><span class="sxs-lookup"><span data-stu-id="79c60-176">404</span></span>         | <span data-ttu-id="79c60-177">Il pacchetto a cui fa riferimento `ID` e `VERSION` (facoltativo) non esiste</span><span class="sxs-lookup"><span data-stu-id="79c60-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
