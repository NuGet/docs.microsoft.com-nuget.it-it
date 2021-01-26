---
title: Firme del repository, API NuGet | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: La risorsa firme del repository consente alle origini dei pacchetti client di annunciare le funzionalità di firma del repository.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775338"
---
# <a name="repository-signatures"></a><span data-ttu-id="2af41-103">Firme di repository</span><span class="sxs-lookup"><span data-stu-id="2af41-103">Repository signatures</span></span>

<span data-ttu-id="2af41-104">Se un'origine del pacchetto supporta l'aggiunta di firme di repository ai pacchetti pubblicati, è possibile che un client determini i certificati di firma utilizzati dall'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2af41-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="2af41-105">Questa risorsa consente ai client di rilevare se un pacchetto firmato del repository è stato alterato o ha un certificato di firma imprevisto.</span><span class="sxs-lookup"><span data-stu-id="2af41-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="2af41-106">La risorsa usata per recuperare le informazioni sulla firma del repository è la `RepositorySignatures` risorsa trovata nell' [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="2af41-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="2af41-107">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="2af41-107">Versioning</span></span>

<span data-ttu-id="2af41-108">`@type`Viene utilizzato il valore seguente:</span><span class="sxs-lookup"><span data-stu-id="2af41-108">The following `@type` value is used:</span></span>

<span data-ttu-id="2af41-109">Valore della proprietà @type</span><span class="sxs-lookup"><span data-stu-id="2af41-109">@type value</span></span>                | <span data-ttu-id="2af41-110">Note</span><span class="sxs-lookup"><span data-stu-id="2af41-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="2af41-111">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="2af41-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="2af41-112">Versione iniziale</span><span class="sxs-lookup"><span data-stu-id="2af41-112">The initial release</span></span>
<span data-ttu-id="2af41-113">RepositorySignatures/4.9.0</span><span class="sxs-lookup"><span data-stu-id="2af41-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="2af41-114">Supportato da NuGet v 4.9 + client</span><span class="sxs-lookup"><span data-stu-id="2af41-114">Supported by NuGet v4.9+ clients</span></span>
<span data-ttu-id="2af41-115">RepositorySignatures/5.0.0</span><span class="sxs-lookup"><span data-stu-id="2af41-115">RepositorySignatures/5.0.0</span></span> | <span data-ttu-id="2af41-116">Consente l'abilitazione di `allRepositorySigned` .</span><span class="sxs-lookup"><span data-stu-id="2af41-116">Allows enabling `allRepositorySigned`.</span></span> <span data-ttu-id="2af41-117">Supportato da NuGet v 5.0 + client</span><span class="sxs-lookup"><span data-stu-id="2af41-117">Supported by NuGet v5.0+ clients</span></span>

## <a name="base-url"></a><span data-ttu-id="2af41-118">URL di base</span><span class="sxs-lookup"><span data-stu-id="2af41-118">Base URL</span></span>

<span data-ttu-id="2af41-119">L'URL del punto di ingresso per le API seguenti è il valore della `@id` proprietà associata al valore di risorsa sopra menzionato `@type` .</span><span class="sxs-lookup"><span data-stu-id="2af41-119">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="2af41-120">In questo argomento viene utilizzato l'URL segnaposto `{@id}` .</span><span class="sxs-lookup"><span data-stu-id="2af41-120">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="2af41-121">Si noti che, a differenza di altre risorse, `{@id}` è necessario che l'URL venga servito tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2af41-121">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="2af41-122">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="2af41-122">HTTP methods</span></span>

<span data-ttu-id="2af41-123">Tutti gli URL presenti nella risorsa delle firme del repository supportano solo i metodi HTTP `GET` e `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="2af41-123">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="2af41-124">Indice delle firme del repository</span><span class="sxs-lookup"><span data-stu-id="2af41-124">Repository signatures index</span></span>

<span data-ttu-id="2af41-125">L'indice delle firme del repository contiene due tipi di informazioni:</span><span class="sxs-lookup"><span data-stu-id="2af41-125">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="2af41-126">Indica se tutti i pacchetti trovati nell'origine sono repository firmati da questa origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2af41-126">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="2af41-127">Elenco di certificati utilizzati dall'origine del pacchetto per la firma dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="2af41-127">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="2af41-128">Nella maggior parte dei casi, l'elenco dei certificati verrà aggiunto solo a.</span><span class="sxs-lookup"><span data-stu-id="2af41-128">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="2af41-129">I nuovi certificati vengono aggiunti all'elenco quando il certificato di firma precedente è scaduto e l'origine del pacchetto deve iniziare a usare un nuovo certificato di firma.</span><span class="sxs-lookup"><span data-stu-id="2af41-129">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="2af41-130">Se un certificato viene rimosso dall'elenco, significa che tutte le firme dei pacchetti create con il certificato di firma rimosso non devono più essere considerate valide dal client.</span><span class="sxs-lookup"><span data-stu-id="2af41-130">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="2af41-131">In questo caso, la firma del pacchetto, ma non necessariamente il pacchetto, non è valida.</span><span class="sxs-lookup"><span data-stu-id="2af41-131">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="2af41-132">Un criterio client può consentire l'installazione del pacchetto come senza segno.</span><span class="sxs-lookup"><span data-stu-id="2af41-132">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="2af41-133">Nel caso di revoca del certificato (ad esempio, compromissione della chiave), è previsto che l'origine del pacchetto firmi nuovamente tutti i pacchetti firmati dal certificato interessato.</span><span class="sxs-lookup"><span data-stu-id="2af41-133">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="2af41-134">Inoltre, l'origine del pacchetto deve rimuovere il certificato interessato dall'elenco dei certificati di firma.</span><span class="sxs-lookup"><span data-stu-id="2af41-134">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="2af41-135">La richiesta seguente recupera l'indice delle firme del repository.</span><span class="sxs-lookup"><span data-stu-id="2af41-135">The following request fetches the repository signatures index.</span></span>

```
GET {@id}
```

<span data-ttu-id="2af41-136">L'indice della firma del repository è un documento JSON che contiene un oggetto con le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="2af41-136">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="2af41-137">Nome</span><span class="sxs-lookup"><span data-stu-id="2af41-137">Name</span></span>                | <span data-ttu-id="2af41-138">Type</span><span class="sxs-lookup"><span data-stu-id="2af41-138">Type</span></span>             | <span data-ttu-id="2af41-139">Necessario</span><span class="sxs-lookup"><span data-stu-id="2af41-139">Required</span></span> | <span data-ttu-id="2af41-140">Note</span><span class="sxs-lookup"><span data-stu-id="2af41-140">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="2af41-141">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="2af41-141">allRepositorySigned</span></span> | <span data-ttu-id="2af41-142">boolean</span><span class="sxs-lookup"><span data-stu-id="2af41-142">boolean</span></span>          | <span data-ttu-id="2af41-143">sì</span><span class="sxs-lookup"><span data-stu-id="2af41-143">yes</span></span>      | <span data-ttu-id="2af41-144">Deve trovarsi `false` sulle risorse 4.7.0 e 4.9.0</span><span class="sxs-lookup"><span data-stu-id="2af41-144">Must be `false` on 4.7.0 and 4.9.0 resources</span></span>
<span data-ttu-id="2af41-145">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="2af41-145">signingCertificates</span></span> | <span data-ttu-id="2af41-146">matrice di oggetti</span><span class="sxs-lookup"><span data-stu-id="2af41-146">array of objects</span></span> | <span data-ttu-id="2af41-147">sì</span><span class="sxs-lookup"><span data-stu-id="2af41-147">yes</span></span>      | 

<span data-ttu-id="2af41-148">Il `allRepositorySigned` valore booleano è impostato su false se l'origine del pacchetto include alcuni pacchetti senza firma del repository.</span><span class="sxs-lookup"><span data-stu-id="2af41-148">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="2af41-149">Se il valore booleano è impostato su true, tutti i pacchetti disponibili nell'origine devono disporre di una firma del repository prodotta da uno dei certificati di firma indicati in `signingCertificates` .</span><span class="sxs-lookup"><span data-stu-id="2af41-149">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="2af41-150">Il `allRepositorySigned` valore booleano deve essere false nelle risorse 4.7.0 e 4.9.0.</span><span class="sxs-lookup"><span data-stu-id="2af41-150">The `allRepositorySigned` boolean must be false on the 4.7.0 and 4.9.0 resources.</span></span> <span data-ttu-id="2af41-151">I client NuGet v 4.7, v 4.8 e v 4.9 non possono installare pacchetti da origini che hanno `allRepositorySigned` impostato su true.</span><span class="sxs-lookup"><span data-stu-id="2af41-151">NuGet v4.7, v4.8, and v4.9 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="2af41-152">`signingCertificates`Se il `allRepositorySigned` valore booleano è impostato su true, nella matrice devono essere presenti uno o più certificati di firma.</span><span class="sxs-lookup"><span data-stu-id="2af41-152">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="2af41-153">Se la matrice è vuota e `allRepositorySigned` è impostata su true, tutti i pacchetti dell'origine devono essere considerati non validi, sebbene i criteri client possano comunque consentire l'utilizzo di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="2af41-153">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="2af41-154">Ogni elemento in questa matrice è un oggetto JSON con le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="2af41-154">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="2af41-155">Nome</span><span class="sxs-lookup"><span data-stu-id="2af41-155">Name</span></span>         | <span data-ttu-id="2af41-156">Type</span><span class="sxs-lookup"><span data-stu-id="2af41-156">Type</span></span>   | <span data-ttu-id="2af41-157">Necessario</span><span class="sxs-lookup"><span data-stu-id="2af41-157">Required</span></span> | <span data-ttu-id="2af41-158">Note</span><span class="sxs-lookup"><span data-stu-id="2af41-158">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="2af41-159">contentUrl</span><span class="sxs-lookup"><span data-stu-id="2af41-159">contentUrl</span></span>   | <span data-ttu-id="2af41-160">string</span><span class="sxs-lookup"><span data-stu-id="2af41-160">string</span></span> | <span data-ttu-id="2af41-161">sì</span><span class="sxs-lookup"><span data-stu-id="2af41-161">yes</span></span>      | <span data-ttu-id="2af41-162">URL assoluto del certificato pubblico con codifica DER</span><span class="sxs-lookup"><span data-stu-id="2af41-162">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="2af41-163">impronte digitali</span><span class="sxs-lookup"><span data-stu-id="2af41-163">fingerprints</span></span> | <span data-ttu-id="2af41-164">object</span><span class="sxs-lookup"><span data-stu-id="2af41-164">object</span></span> | <span data-ttu-id="2af41-165">sì</span><span class="sxs-lookup"><span data-stu-id="2af41-165">yes</span></span>      |
<span data-ttu-id="2af41-166">subject</span><span class="sxs-lookup"><span data-stu-id="2af41-166">subject</span></span>      | <span data-ttu-id="2af41-167">string</span><span class="sxs-lookup"><span data-stu-id="2af41-167">string</span></span> | <span data-ttu-id="2af41-168">sì</span><span class="sxs-lookup"><span data-stu-id="2af41-168">yes</span></span>      | <span data-ttu-id="2af41-169">Nome distinto del soggetto del certificato</span><span class="sxs-lookup"><span data-stu-id="2af41-169">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="2af41-170">autorità di certificazione</span><span class="sxs-lookup"><span data-stu-id="2af41-170">issuer</span></span>       | <span data-ttu-id="2af41-171">string</span><span class="sxs-lookup"><span data-stu-id="2af41-171">string</span></span> | <span data-ttu-id="2af41-172">sì</span><span class="sxs-lookup"><span data-stu-id="2af41-172">yes</span></span>      | <span data-ttu-id="2af41-173">Nome distinto dell'emittente del certificato.</span><span class="sxs-lookup"><span data-stu-id="2af41-173">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="2af41-174">notBefore</span><span class="sxs-lookup"><span data-stu-id="2af41-174">notBefore</span></span>    | <span data-ttu-id="2af41-175">string</span><span class="sxs-lookup"><span data-stu-id="2af41-175">string</span></span> | <span data-ttu-id="2af41-176">sì</span><span class="sxs-lookup"><span data-stu-id="2af41-176">yes</span></span>      | <span data-ttu-id="2af41-177">Timestamp iniziale del periodo di validità del certificato</span><span class="sxs-lookup"><span data-stu-id="2af41-177">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="2af41-178">notAfter</span><span class="sxs-lookup"><span data-stu-id="2af41-178">notAfter</span></span>     | <span data-ttu-id="2af41-179">string</span><span class="sxs-lookup"><span data-stu-id="2af41-179">string</span></span> | <span data-ttu-id="2af41-180">sì</span><span class="sxs-lookup"><span data-stu-id="2af41-180">yes</span></span>      | <span data-ttu-id="2af41-181">Timestamp finale del periodo di validità del certificato</span><span class="sxs-lookup"><span data-stu-id="2af41-181">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="2af41-182">Si noti che `contentUrl` è necessario che sia servito tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2af41-182">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="2af41-183">Questo URL non ha un modello di URL specifico e deve essere individuato in modo dinamico usando questo documento di indice delle firme del repository.</span><span class="sxs-lookup"><span data-stu-id="2af41-183">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="2af41-184">Tutte le proprietà di questo oggetto (a parte `contentUrl` ) devono essere derivabili dal certificato trovato in `contentUrl` .</span><span class="sxs-lookup"><span data-stu-id="2af41-184">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="2af41-185">Queste proprietà derivabili vengono fornite come praticità per ridurre al minimo i round trip.</span><span class="sxs-lookup"><span data-stu-id="2af41-185">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="2af41-186">Di seguito sono elencate le proprietà dell'oggetto `fingerprints`:</span><span class="sxs-lookup"><span data-stu-id="2af41-186">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="2af41-187">Nome</span><span class="sxs-lookup"><span data-stu-id="2af41-187">Name</span></span>                   | <span data-ttu-id="2af41-188">Type</span><span class="sxs-lookup"><span data-stu-id="2af41-188">Type</span></span>   | <span data-ttu-id="2af41-189">Necessario</span><span class="sxs-lookup"><span data-stu-id="2af41-189">Required</span></span> | <span data-ttu-id="2af41-190">Note</span><span class="sxs-lookup"><span data-stu-id="2af41-190">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="2af41-191">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="2af41-191">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="2af41-192">string</span><span class="sxs-lookup"><span data-stu-id="2af41-192">string</span></span> | <span data-ttu-id="2af41-193">sì</span><span class="sxs-lookup"><span data-stu-id="2af41-193">yes</span></span>      | <span data-ttu-id="2af41-194">Impronta digitale SHA-256</span><span class="sxs-lookup"><span data-stu-id="2af41-194">The SHA-256 fingerprint</span></span>

<span data-ttu-id="2af41-195">Il nome della chiave `2.16.840.1.101.3.4.2.1` è l'OID dell'algoritmo hash SHA-256.</span><span class="sxs-lookup"><span data-stu-id="2af41-195">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="2af41-196">Tutti i valori hash devono essere rappresentazioni di stringa con codifica esadecimale minuscole del digest hash.</span><span class="sxs-lookup"><span data-stu-id="2af41-196">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="2af41-197">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="2af41-197">Sample request</span></span>

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a><span data-ttu-id="2af41-198">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="2af41-198">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
