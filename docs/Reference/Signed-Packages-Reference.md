---
title: Riferimento a pacchetti firmati | Documenti Microsoft
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Descrizione pacchetti di funzionalità di firma."
keywords: Accesso pacchetto NuGet, firma certificato
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4763b0dde0153f9e8ea840d5e788b5a3d96b9bd8
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/08/2018
---
# <a name="signed-packages"></a><span data-ttu-id="70d51-104">Pacchetti firmati</span><span class="sxs-lookup"><span data-stu-id="70d51-104">Signed packages</span></span>

<span data-ttu-id="70d51-105">*NuGet 4.6.0+ e Visual Studio 2017 15,6 e versioni successive*</span><span class="sxs-lookup"><span data-stu-id="70d51-105">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="70d51-106">Pacchetti NuGet possono includere una firma digitale che fornisce la protezione del contenuto manomessa.</span><span class="sxs-lookup"><span data-stu-id="70d51-106">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="70d51-107">Questa firma viene generata da un certificato x. 509 che aggiunge anche modelli di prova di autenticità per l'origine del pacchetto effettiva.</span><span class="sxs-lookup"><span data-stu-id="70d51-107">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="70d51-108">Pacchetti firmati forniscono la convalida end-to-end più attendibili.</span><span class="sxs-lookup"><span data-stu-id="70d51-108">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="70d51-109">Una firma di autore garantisce che il pacchetto non è stato modificato dopo l'autore la firma del pacchetto, indipendentemente da quale metodo viene recapitato il pacchetto del trasporto repository o cosa.</span><span class="sxs-lookup"><span data-stu-id="70d51-109">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="70d51-110">I consumer che necessitano di un ambiente bloccato possono richiedere pacchetti firmati con un certificato specifico dell'autore.</span><span class="sxs-lookup"><span data-stu-id="70d51-110">Consumers who demand a locked-down environment can require packages signed with an specific author certificate.</span></span>

<span data-ttu-id="70d51-111">Inoltre, pacchetti firmati autore forniscono un meccanismo di autenticazione extra per la pipeline di pubblicazione nuget.org poiché il certificato di firma deve essere registrato anticipatamente.</span><span class="sxs-lookup"><span data-stu-id="70d51-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span>

<span data-ttu-id="70d51-112">Per informazioni dettagliate sulla creazione di un pacchetto firmato, vedere [firma pacchetti](../create-packages/Sign-a-package.md) e [comando sign nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="70d51-112">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="70d51-113">NuGet.org non accetta attualmente dei pacchetti firmati.</span><span class="sxs-lookup"><span data-stu-id="70d51-113">nuget.org does not presently accept signed packages.</span></span> <span data-ttu-id="70d51-114">È possibile firmare pacchetti per la pubblicazione nel feed personalizzati.</span><span class="sxs-lookup"><span data-stu-id="70d51-114">You can sign packages for publishing to custom feeds.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="70d51-115">Requisiti del certificato</span><span class="sxs-lookup"><span data-stu-id="70d51-115">Certificate requirements</span></span>

<span data-ttu-id="70d51-116">Firmare il pacchetto richiede un certificato, che è un tipo speciale di certificato valido per la firma del codice di `id-kp-codeSigning` scopo [[RFC 5280 sezione 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="70d51-116">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="70d51-117">Inoltre, il certificato deve avere una pubblica lunghezza della chiave RSA 2048 bit o superiore.</span><span class="sxs-lookup"><span data-stu-id="70d51-117">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="70d51-118">Ottenere un certificato di firma codice</span><span class="sxs-lookup"><span data-stu-id="70d51-118">Get a code signing certificate</span></span>

<span data-ttu-id="70d51-119">I certificati validi possono essere ottenuti da autorità di certificazione pubblica come:</span><span class="sxs-lookup"><span data-stu-id="70d51-119">Valid certificates may be obtained from public certificate authorities like:</span></span>

- [<span data-ttu-id="70d51-120">Symantec</span><span class="sxs-lookup"><span data-stu-id="70d51-120">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="70d51-121">DigiCert</span><span class="sxs-lookup"><span data-stu-id="70d51-121">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="70d51-122">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="70d51-122">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="70d51-123">Accesso globale</span><span class="sxs-lookup"><span data-stu-id="70d51-123">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="70d51-124">Comodo</span><span class="sxs-lookup"><span data-stu-id="70d51-124">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="70d51-125">Certum</span><span class="sxs-lookup"><span data-stu-id="70d51-125">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="70d51-126">L'elenco completo delle autorità di certificazione attendibile per Windows può essere ottenuto da [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="70d51-126">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="70d51-127">Creare un certificato di prova</span><span class="sxs-lookup"><span data-stu-id="70d51-127">Create a test certificate</span></span>

<span data-ttu-id="70d51-128">È possibile utilizzare i certificati autocertificati a scopo di test.</span><span class="sxs-lookup"><span data-stu-id="70d51-128">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="70d51-129">Per creare un'autocertificazione, utilizzare il [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) comando di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="70d51-129">To create a self-issued certificate, use the [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell command.</span></span>

```ps
New-SelfSignedCertificate -Subject "CN=NuGet Test Developer, OU=Use for testing purposes ONLY" `
                          -FriendlyName "NuGetTestDeveloper" `
                          -Type CodeSigning `
                          -KeyUsage DigitalSignature `
                          -KeyLength 2048 `
                          -KeyAlgorithm RSA `
                          -HashAlgorithm SHA256 `
                          -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
                          -CertStoreLocation "Cert:\CurrentUser\My" 
```

<span data-ttu-id="70d51-130">Questo comando crea un certificato di test disponibile nell'archivio certificati personali dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="70d51-130">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="70d51-131">È possibile aprire l'archivio certificati eseguendo `certmgr.msc` per visualizzare il certificato appena creato.</span><span class="sxs-lookup"><span data-stu-id="70d51-131">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="70d51-132">Requisiti di timestamp</span><span class="sxs-lookup"><span data-stu-id="70d51-132">Timestamp requirements</span></span>

<span data-ttu-id="70d51-133">Pacchetti firmati devono includere un timestamp RFC 3161 per garantire la validità della firma oltre il periodo di validità del certificato di firma dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="70d51-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="70d51-134">Il certificato utilizzato per firmare il timestamp deve essere valido per il `id-kp-timeStamping` scopo [[RFC 5280 sezione 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="70d51-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="70d51-135">Inoltre, il certificato deve avere una pubblica lunghezza della chiave RSA 2048 bit o superiore.</span><span class="sxs-lookup"><span data-stu-id="70d51-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="70d51-136">Altri dettagli tecnici, vedere il [specifiche tecniche di firma del pacchetto](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="70d51-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>
