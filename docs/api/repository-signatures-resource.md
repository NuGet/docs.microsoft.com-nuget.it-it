---
title: API NuGet, repository firme | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: La risorsa di firme del repository consente ai client di origini dei pacchetti di annunciare il repository di funzionalità di firma.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 50f309b99d4bf59e14f3e29b6b0421d8c3e8aa5a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547981"
---
# <a name="repository-signatures"></a><span data-ttu-id="bbd22-103">Firme di repository</span><span class="sxs-lookup"><span data-stu-id="bbd22-103">Repository signatures</span></span>

<span data-ttu-id="bbd22-104">Se un'origine pacchetto supporta le firme di aggiunta repository per i pacchetti pubblicati, è possibile che un client di determinare i certificati di firma utilizzati per l'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbd22-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="bbd22-105">Questa risorsa consente ai client di rilevare se un repository firmato pacchetto è stato manomesso o ha un certificato di firma imprevisto.</span><span class="sxs-lookup"><span data-stu-id="bbd22-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="bbd22-106">La risorsa usata per recuperare informazioni sulla firma questo repository è il `RepositorySignatures` trovare la risorsa nella [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="bbd22-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="bbd22-107">NuGet.org inizierà l'annuncio di `RepositorySignatures` risorse in un prossimo futuro.</span><span class="sxs-lookup"><span data-stu-id="bbd22-107">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="bbd22-108">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="bbd22-108">Versioning</span></span>

<span data-ttu-id="bbd22-109">Nell'esempio `@type` valore viene usato:</span><span class="sxs-lookup"><span data-stu-id="bbd22-109">The following `@type` value is used:</span></span>

<span data-ttu-id="bbd22-110">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="bbd22-110">@type value</span></span>                | <span data-ttu-id="bbd22-111">Note</span><span class="sxs-lookup"><span data-stu-id="bbd22-111">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="bbd22-112">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="bbd22-112">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="bbd22-113">La versione iniziale</span><span class="sxs-lookup"><span data-stu-id="bbd22-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="bbd22-114">URL di base</span><span class="sxs-lookup"><span data-stu-id="bbd22-114">Base URL</span></span>

<span data-ttu-id="bbd22-115">URL del punto di ingresso per le API seguenti è il valore della `@id` proprietà associato alla risorsa menzionati in precedenza `@type` valore.</span><span class="sxs-lookup"><span data-stu-id="bbd22-115">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="bbd22-116">In questo argomento Usa l'URL segnaposto `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="bbd22-116">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="bbd22-117">Si noti che a differenza di altre risorse, il `{@id}` l'URL è obbligatorio per essere serviti tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bbd22-117">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="bbd22-118">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="bbd22-118">HTTP methods</span></span>

<span data-ttu-id="bbd22-119">Tutti gli URL trovati nei metodi di supporto solo HTTP di repository le firme resource `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="bbd22-119">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="bbd22-120">Indice delle firme del repository</span><span class="sxs-lookup"><span data-stu-id="bbd22-120">Repository signatures index</span></span>

<span data-ttu-id="bbd22-121">L'indice di firme di repository contiene due tipi di informazioni:</span><span class="sxs-lookup"><span data-stu-id="bbd22-121">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="bbd22-122">Se tutti i pacchetti disponibili nell'origine sono firmati da questa origine pacchetto repository.</span><span class="sxs-lookup"><span data-stu-id="bbd22-122">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="bbd22-123">L'elenco dei certificati usati per l'origine del pacchetto per firmare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="bbd22-123">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="bbd22-124">Nella maggior parte dei casi, l'elenco dei certificati verrà aggiunto sempre a.</span><span class="sxs-lookup"><span data-stu-id="bbd22-124">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="bbd22-125">I nuovi certificati verranno aggiunto all'elenco quando il certificato di firma precedente è scaduto e l'origine del pacchetto deve iniziare a usare un nuovo certificato di firma.</span><span class="sxs-lookup"><span data-stu-id="bbd22-125">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="bbd22-126">Se un certificato viene rimosso dall'elenco, che significa che tutte le firme dei pacchetti create con il certificato di firma rimosso non è più da considerare valide dal client.</span><span class="sxs-lookup"><span data-stu-id="bbd22-126">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="bbd22-127">In questo caso, la firma del pacchetto, ma non necessariamente il pacchetto, non è valido.</span><span class="sxs-lookup"><span data-stu-id="bbd22-127">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="bbd22-128">Un criterio client può consentire l'installazione del pacchetto come senza segno.</span><span class="sxs-lookup"><span data-stu-id="bbd22-128">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="bbd22-129">Nel caso di revoca del certificato (ad esempio, venga compromessa), l'origine del pacchetto deve firmare di nuovo tutti i pacchetti firmati dal certificato interessato.</span><span class="sxs-lookup"><span data-stu-id="bbd22-129">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="bbd22-130">Inoltre, l'origine del pacchetto deve rimuovere il certificato interessato dall'elenco di certificati di firma.</span><span class="sxs-lookup"><span data-stu-id="bbd22-130">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="bbd22-131">La richiesta seguente recupera l'indice di firme di repository.</span><span class="sxs-lookup"><span data-stu-id="bbd22-131">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="bbd22-132">L'indice di firma del repository è un documento JSON che contiene un oggetto con le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="bbd22-132">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="bbd22-133">nome</span><span class="sxs-lookup"><span data-stu-id="bbd22-133">Name</span></span>                | <span data-ttu-id="bbd22-134">Tipo</span><span class="sxs-lookup"><span data-stu-id="bbd22-134">Type</span></span>             | <span data-ttu-id="bbd22-135">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="bbd22-135">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="bbd22-136">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="bbd22-136">allRepositorySigned</span></span> | <span data-ttu-id="bbd22-137">boolean</span><span class="sxs-lookup"><span data-stu-id="bbd22-137">boolean</span></span>          | <span data-ttu-id="bbd22-138">sì</span><span class="sxs-lookup"><span data-stu-id="bbd22-138">yes</span></span>
<span data-ttu-id="bbd22-139">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="bbd22-139">signingCertificates</span></span> | <span data-ttu-id="bbd22-140">Matrice di oggetti</span><span class="sxs-lookup"><span data-stu-id="bbd22-140">array of objects</span></span> | <span data-ttu-id="bbd22-141">sì</span><span class="sxs-lookup"><span data-stu-id="bbd22-141">yes</span></span>

<span data-ttu-id="bbd22-142">Il `allRepositorySigned` valore booleano è impostato su false se l'origine del pacchetto ha alcuni pacchetti che non hanno alcuna firma dell'archivio.</span><span class="sxs-lookup"><span data-stu-id="bbd22-142">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="bbd22-143">Se il valore booleano è impostato su true, tutti i pacchetti disponibili in origine deve avere una firma di repository prodotta da uno dei certificati di firma menzionati `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="bbd22-143">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="bbd22-144">Deve essere presente uno o più certificati di firma nel `signingCertificates` matrice se il `allRepositorySigned` valore booleano è impostato su true.</span><span class="sxs-lookup"><span data-stu-id="bbd22-144">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="bbd22-145">Se la matrice è vuota e `allRepositorySigned` è impostato su true, tutti i pacchetti dall'origine devono essere considerati validi, anche se un criterio client consentono ancora il consumo dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="bbd22-145">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="bbd22-146">Ogni elemento nella matrice è un oggetto JSON con le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="bbd22-146">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="bbd22-147">nome</span><span class="sxs-lookup"><span data-stu-id="bbd22-147">Name</span></span>         | <span data-ttu-id="bbd22-148">Tipo</span><span class="sxs-lookup"><span data-stu-id="bbd22-148">Type</span></span>   | <span data-ttu-id="bbd22-149">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="bbd22-149">Required</span></span> | <span data-ttu-id="bbd22-150">Note</span><span class="sxs-lookup"><span data-stu-id="bbd22-150">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="bbd22-151">contentUrl</span><span class="sxs-lookup"><span data-stu-id="bbd22-151">contentUrl</span></span>   | <span data-ttu-id="bbd22-152">stringa</span><span class="sxs-lookup"><span data-stu-id="bbd22-152">string</span></span> | <span data-ttu-id="bbd22-153">sì</span><span class="sxs-lookup"><span data-stu-id="bbd22-153">yes</span></span>      | <span data-ttu-id="bbd22-154">URL assoluto per il certificato pubblico con codifica DER</span><span class="sxs-lookup"><span data-stu-id="bbd22-154">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="bbd22-155">impronte digitali</span><span class="sxs-lookup"><span data-stu-id="bbd22-155">fingerprints</span></span> | <span data-ttu-id="bbd22-156">object</span><span class="sxs-lookup"><span data-stu-id="bbd22-156">object</span></span> | <span data-ttu-id="bbd22-157">sì</span><span class="sxs-lookup"><span data-stu-id="bbd22-157">yes</span></span>      |
<span data-ttu-id="bbd22-158">Oggetto</span><span class="sxs-lookup"><span data-stu-id="bbd22-158">subject</span></span>      | <span data-ttu-id="bbd22-159">stringa</span><span class="sxs-lookup"><span data-stu-id="bbd22-159">string</span></span> | <span data-ttu-id="bbd22-160">sì</span><span class="sxs-lookup"><span data-stu-id="bbd22-160">yes</span></span>      | <span data-ttu-id="bbd22-161">Il nome distinto del soggetto del certificato</span><span class="sxs-lookup"><span data-stu-id="bbd22-161">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="bbd22-162">issuer</span><span class="sxs-lookup"><span data-stu-id="bbd22-162">issuer</span></span>       | <span data-ttu-id="bbd22-163">stringa</span><span class="sxs-lookup"><span data-stu-id="bbd22-163">string</span></span> | <span data-ttu-id="bbd22-164">sì</span><span class="sxs-lookup"><span data-stu-id="bbd22-164">yes</span></span>      | <span data-ttu-id="bbd22-165">Il nome distinto dell'emittente del certificato</span><span class="sxs-lookup"><span data-stu-id="bbd22-165">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="bbd22-166">notBefore</span><span class="sxs-lookup"><span data-stu-id="bbd22-166">notBefore</span></span>    | <span data-ttu-id="bbd22-167">stringa</span><span class="sxs-lookup"><span data-stu-id="bbd22-167">string</span></span> | <span data-ttu-id="bbd22-168">sì</span><span class="sxs-lookup"><span data-stu-id="bbd22-168">yes</span></span>      | <span data-ttu-id="bbd22-169">Il timestamp di inizio del periodo di validità del certificato</span><span class="sxs-lookup"><span data-stu-id="bbd22-169">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="bbd22-170">notAfter</span><span class="sxs-lookup"><span data-stu-id="bbd22-170">notAfter</span></span>     | <span data-ttu-id="bbd22-171">stringa</span><span class="sxs-lookup"><span data-stu-id="bbd22-171">string</span></span> | <span data-ttu-id="bbd22-172">sì</span><span class="sxs-lookup"><span data-stu-id="bbd22-172">yes</span></span>      | <span data-ttu-id="bbd22-173">Il timestamp finale del periodo di validità del certificato</span><span class="sxs-lookup"><span data-stu-id="bbd22-173">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="bbd22-174">Si noti che il `contentUrl` deve essere gestito tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bbd22-174">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="bbd22-175">Questo URL non ha alcun modello di URL specifico e deve essere individuato in modo dinamico utilizzando questo documento di repository le firme dell'indice.</span><span class="sxs-lookup"><span data-stu-id="bbd22-175">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="bbd22-176">Tutte le proprietà in questo oggetto (oltre `contentUrl`) deve essere derivabile dal certificato, vedere `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="bbd22-176">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="bbd22-177">Queste proprietà derivabile sono fornite per praticità per ridurre i round trip.</span><span class="sxs-lookup"><span data-stu-id="bbd22-177">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="bbd22-178">Il `fingerprints` oggetto presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="bbd22-178">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="bbd22-179">nome</span><span class="sxs-lookup"><span data-stu-id="bbd22-179">Name</span></span>                   | <span data-ttu-id="bbd22-180">Tipo</span><span class="sxs-lookup"><span data-stu-id="bbd22-180">Type</span></span>   | <span data-ttu-id="bbd22-181">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="bbd22-181">Required</span></span> | <span data-ttu-id="bbd22-182">Note</span><span class="sxs-lookup"><span data-stu-id="bbd22-182">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="bbd22-183">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="bbd22-183">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="bbd22-184">stringa</span><span class="sxs-lookup"><span data-stu-id="bbd22-184">string</span></span> | <span data-ttu-id="bbd22-185">sì</span><span class="sxs-lookup"><span data-stu-id="bbd22-185">yes</span></span>      | <span data-ttu-id="bbd22-186">L'impronta digitale SHA-256</span><span class="sxs-lookup"><span data-stu-id="bbd22-186">The SHA-256 fingerprint</span></span>

<span data-ttu-id="bbd22-187">Il nome della chiave `2.16.840.1.101.3.4.2.1` è l'OID dell'algoritmo hash SHA-256.</span><span class="sxs-lookup"><span data-stu-id="bbd22-187">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="bbd22-188">Tutti i valori hash devono essere rappresentazioni di stringa di caratteri minuscoli, con codifica esadecimale di digest hash.</span><span class="sxs-lookup"><span data-stu-id="bbd22-188">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="bbd22-189">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="bbd22-189">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="bbd22-190">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="bbd22-190">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
