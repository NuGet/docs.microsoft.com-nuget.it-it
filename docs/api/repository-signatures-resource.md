---
title: API NuGet, repository firme | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 3/2/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: La risorsa di firme del repository consente ai client di origini dei pacchetti di annunciare il repository di funzionalità di firma.
keywords: API NuGet repository firme, nuget.org firma dei certificati, la firma del pacchetto nuget.org
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 27c572a482fef791f19b3d32e816a41d8dc40b53
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020558"
---
# <a name="repository-signatures"></a><span data-ttu-id="cb91d-104">Firme di repository</span><span class="sxs-lookup"><span data-stu-id="cb91d-104">Repository signatures</span></span>

<span data-ttu-id="cb91d-105">Se un'origine pacchetto supporta le firme di aggiunta repository per i pacchetti pubblicati, è possibile che un client di determinare i certificati di firma utilizzati per l'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cb91d-105">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="cb91d-106">Questa risorsa consente ai client di rilevare se un repository firmato pacchetto è stato manomesso o ha un certificato di firma imprevisto.</span><span class="sxs-lookup"><span data-stu-id="cb91d-106">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="cb91d-107">La risorsa usata per recuperare informazioni sulla firma questo repository è il `RepositorySignatures` trovare la risorsa nella [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="cb91d-107">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="cb91d-108">NuGet.org inizierà l'annuncio di `RepositorySignatures` risorse in un prossimo futuro.</span><span class="sxs-lookup"><span data-stu-id="cb91d-108">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="cb91d-109">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="cb91d-109">Versioning</span></span>

<span data-ttu-id="cb91d-110">Nell'esempio `@type` valore viene usato:</span><span class="sxs-lookup"><span data-stu-id="cb91d-110">The following `@type` value is used:</span></span>

<span data-ttu-id="cb91d-111">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="cb91d-111">@type value</span></span>                | <span data-ttu-id="cb91d-112">Note</span><span class="sxs-lookup"><span data-stu-id="cb91d-112">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="cb91d-113">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="cb91d-113">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="cb91d-114">La versione iniziale</span><span class="sxs-lookup"><span data-stu-id="cb91d-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="cb91d-115">URL di base</span><span class="sxs-lookup"><span data-stu-id="cb91d-115">Base URL</span></span>

<span data-ttu-id="cb91d-116">URL del punto di ingresso per le API seguenti è il valore della `@id` proprietà associato alla risorsa menzionati in precedenza `@type` valore.</span><span class="sxs-lookup"><span data-stu-id="cb91d-116">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="cb91d-117">In questo argomento Usa l'URL segnaposto `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="cb91d-117">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="cb91d-118">Si noti che a differenza di altre risorse, il `{@id}` l'URL è obbligatorio per essere serviti tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="cb91d-118">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="cb91d-119">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="cb91d-119">HTTP methods</span></span>

<span data-ttu-id="cb91d-120">Tutti gli URL trovati nei metodi di supporto solo HTTP di repository le firme resource `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="cb91d-120">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="cb91d-121">Indice delle firme del repository</span><span class="sxs-lookup"><span data-stu-id="cb91d-121">Repository signatures index</span></span>

<span data-ttu-id="cb91d-122">L'indice di firme di repository contiene due tipi di informazioni:</span><span class="sxs-lookup"><span data-stu-id="cb91d-122">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="cb91d-123">Se tutti i pacchetti disponibili nell'origine sono firmati da questa origine pacchetto repository.</span><span class="sxs-lookup"><span data-stu-id="cb91d-123">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="cb91d-124">L'elenco dei certificati usati per l'origine del pacchetto per firmare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cb91d-124">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="cb91d-125">Nella maggior parte dei casi, l'elenco dei certificati verrà aggiunto sempre a.</span><span class="sxs-lookup"><span data-stu-id="cb91d-125">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="cb91d-126">I nuovi certificati verranno aggiunto all'elenco quando il certificato di firma precedente è scaduto e l'origine del pacchetto deve iniziare a usare un nuovo certificato di firma.</span><span class="sxs-lookup"><span data-stu-id="cb91d-126">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="cb91d-127">Se un certificato viene rimosso dall'elenco, che significa che tutte le firme dei pacchetti create con il certificato di firma rimosso non è più da considerare valide dal client.</span><span class="sxs-lookup"><span data-stu-id="cb91d-127">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="cb91d-128">In questo caso, la firma del pacchetto, ma non necessariamente il pacchetto, non è valido.</span><span class="sxs-lookup"><span data-stu-id="cb91d-128">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="cb91d-129">Un criterio client può consentire l'installazione del pacchetto come senza segno.</span><span class="sxs-lookup"><span data-stu-id="cb91d-129">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="cb91d-130">Nel caso di revoca del certificato (ad esempio, venga compromessa), l'origine del pacchetto deve firmare nuovamente tutti i pacchetti firmati dal certificato interessato.</span><span class="sxs-lookup"><span data-stu-id="cb91d-130">In the case of certificate revocation (e.g. key compromise), the package source is expected to resign all packages signed by the affected certificate.</span></span> <span data-ttu-id="cb91d-131">Inoltre, l'origine del pacchetto deve rimuovere il certificato interessato dall'elenco di certificati di firma.</span><span class="sxs-lookup"><span data-stu-id="cb91d-131">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="cb91d-132">La richiesta seguente recupera l'indice di firme di repository.</span><span class="sxs-lookup"><span data-stu-id="cb91d-132">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="cb91d-133">L'indice di firma del repository è un documento JSON che contiene un oggetto con le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="cb91d-133">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="cb91d-134">nome</span><span class="sxs-lookup"><span data-stu-id="cb91d-134">Name</span></span>                | <span data-ttu-id="cb91d-135">Tipo</span><span class="sxs-lookup"><span data-stu-id="cb91d-135">Type</span></span>             | <span data-ttu-id="cb91d-136">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="cb91d-136">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="cb91d-137">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="cb91d-137">allRepositorySigned</span></span> | <span data-ttu-id="cb91d-138">boolean</span><span class="sxs-lookup"><span data-stu-id="cb91d-138">boolean</span></span>          | <span data-ttu-id="cb91d-139">sì</span><span class="sxs-lookup"><span data-stu-id="cb91d-139">yes</span></span>
<span data-ttu-id="cb91d-140">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="cb91d-140">signingCertificates</span></span> | <span data-ttu-id="cb91d-141">Matrice di oggetti</span><span class="sxs-lookup"><span data-stu-id="cb91d-141">array of objects</span></span> | <span data-ttu-id="cb91d-142">sì</span><span class="sxs-lookup"><span data-stu-id="cb91d-142">yes</span></span>

<span data-ttu-id="cb91d-143">Il `allRepositorySigned` valore booleano è impostato su false se l'origine del pacchetto ha alcuni pacchetti che non hanno alcuna firma dell'archivio.</span><span class="sxs-lookup"><span data-stu-id="cb91d-143">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="cb91d-144">Se il valore booleano è impostato su true, tutti i pacchetti disponibili in origine deve avere una firma di repository prodotta da uno dei certificati di firma menzionati `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="cb91d-144">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="cb91d-145">Deve essere presente uno o più certificati di firma nel `signingCertificates` matrice se il `allRepositorySigned` valore booleano è impostato su true.</span><span class="sxs-lookup"><span data-stu-id="cb91d-145">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="cb91d-146">Se la matrice è vuota e `allRepositorySigned` è impostato su true, tutti i pacchetti dall'origine devono essere considerati validi, anche se un criterio client consentono ancora il consumo dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cb91d-146">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="cb91d-147">Ogni elemento nella matrice è un oggetto JSON con le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="cb91d-147">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="cb91d-148">nome</span><span class="sxs-lookup"><span data-stu-id="cb91d-148">Name</span></span>         | <span data-ttu-id="cb91d-149">Tipo</span><span class="sxs-lookup"><span data-stu-id="cb91d-149">Type</span></span>   | <span data-ttu-id="cb91d-150">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="cb91d-150">Required</span></span> | <span data-ttu-id="cb91d-151">Note</span><span class="sxs-lookup"><span data-stu-id="cb91d-151">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="cb91d-152">contentUrl</span><span class="sxs-lookup"><span data-stu-id="cb91d-152">contentUrl</span></span>   | <span data-ttu-id="cb91d-153">stringa</span><span class="sxs-lookup"><span data-stu-id="cb91d-153">string</span></span> | <span data-ttu-id="cb91d-154">sì</span><span class="sxs-lookup"><span data-stu-id="cb91d-154">yes</span></span>      | <span data-ttu-id="cb91d-155">URL assoluto per il certificato pubblico con codifica DER</span><span class="sxs-lookup"><span data-stu-id="cb91d-155">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="cb91d-156">impronte digitali</span><span class="sxs-lookup"><span data-stu-id="cb91d-156">fingerprints</span></span> | <span data-ttu-id="cb91d-157">object</span><span class="sxs-lookup"><span data-stu-id="cb91d-157">object</span></span> | <span data-ttu-id="cb91d-158">sì</span><span class="sxs-lookup"><span data-stu-id="cb91d-158">yes</span></span>      |
<span data-ttu-id="cb91d-159">Oggetto</span><span class="sxs-lookup"><span data-stu-id="cb91d-159">subject</span></span>      | <span data-ttu-id="cb91d-160">stringa</span><span class="sxs-lookup"><span data-stu-id="cb91d-160">string</span></span> | <span data-ttu-id="cb91d-161">sì</span><span class="sxs-lookup"><span data-stu-id="cb91d-161">yes</span></span>      | <span data-ttu-id="cb91d-162">Il nome distinto del soggetto del certificato</span><span class="sxs-lookup"><span data-stu-id="cb91d-162">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="cb91d-163">issuer</span><span class="sxs-lookup"><span data-stu-id="cb91d-163">issuer</span></span>       | <span data-ttu-id="cb91d-164">stringa</span><span class="sxs-lookup"><span data-stu-id="cb91d-164">string</span></span> | <span data-ttu-id="cb91d-165">sì</span><span class="sxs-lookup"><span data-stu-id="cb91d-165">yes</span></span>      | <span data-ttu-id="cb91d-166">Il nome distinto dell'emittente del certificato</span><span class="sxs-lookup"><span data-stu-id="cb91d-166">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="cb91d-167">notBefore</span><span class="sxs-lookup"><span data-stu-id="cb91d-167">notBefore</span></span>    | <span data-ttu-id="cb91d-168">stringa</span><span class="sxs-lookup"><span data-stu-id="cb91d-168">string</span></span> | <span data-ttu-id="cb91d-169">sì</span><span class="sxs-lookup"><span data-stu-id="cb91d-169">yes</span></span>      | <span data-ttu-id="cb91d-170">Il timestamp di inizio del periodo di validità del certificato</span><span class="sxs-lookup"><span data-stu-id="cb91d-170">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="cb91d-171">notAfter</span><span class="sxs-lookup"><span data-stu-id="cb91d-171">notAfter</span></span>     | <span data-ttu-id="cb91d-172">stringa</span><span class="sxs-lookup"><span data-stu-id="cb91d-172">string</span></span> | <span data-ttu-id="cb91d-173">sì</span><span class="sxs-lookup"><span data-stu-id="cb91d-173">yes</span></span>      | <span data-ttu-id="cb91d-174">Il timestamp finale del periodo di validità del certificato</span><span class="sxs-lookup"><span data-stu-id="cb91d-174">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="cb91d-175">Si noti che il `contentUrl` deve essere gestito tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="cb91d-175">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="cb91d-176">Questo URL non ha alcun modello di URL specifico e deve essere individuato in modo dinamico utilizzando questo documento di repository le firme dell'indice.</span><span class="sxs-lookup"><span data-stu-id="cb91d-176">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="cb91d-177">Tutte le proprietà in questo oggetto (oltre `contentUrl`) deve essere derivabile dal certificato, vedere `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="cb91d-177">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="cb91d-178">Queste proprietà derivabile sono fornite per praticità per ridurre i round trip.</span><span class="sxs-lookup"><span data-stu-id="cb91d-178">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="cb91d-179">Il `fingerprints` oggetto presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="cb91d-179">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="cb91d-180">nome</span><span class="sxs-lookup"><span data-stu-id="cb91d-180">Name</span></span>                   | <span data-ttu-id="cb91d-181">Tipo</span><span class="sxs-lookup"><span data-stu-id="cb91d-181">Type</span></span>   | <span data-ttu-id="cb91d-182">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="cb91d-182">Required</span></span> | <span data-ttu-id="cb91d-183">Note</span><span class="sxs-lookup"><span data-stu-id="cb91d-183">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="cb91d-184">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="cb91d-184">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="cb91d-185">stringa</span><span class="sxs-lookup"><span data-stu-id="cb91d-185">string</span></span> | <span data-ttu-id="cb91d-186">sì</span><span class="sxs-lookup"><span data-stu-id="cb91d-186">yes</span></span>      | <span data-ttu-id="cb91d-187">L'impronta digitale SHA-256</span><span class="sxs-lookup"><span data-stu-id="cb91d-187">The SHA-256 fingerprint</span></span>

<span data-ttu-id="cb91d-188">Il nome della chiave `2.16.840.1.101.3.4.2.1` è l'OID dell'algoritmo hash SHA-256.</span><span class="sxs-lookup"><span data-stu-id="cb91d-188">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="cb91d-189">Tutti i valori hash devono essere rappresentazioni di stringa di caratteri minuscoli, con codifica esadecimale di digest hash.</span><span class="sxs-lookup"><span data-stu-id="cb91d-189">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="cb91d-190">Richiesta di esempio</span><span class="sxs-lookup"><span data-stu-id="cb91d-190">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="cb91d-191">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="cb91d-191">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
