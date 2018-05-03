---
title: Firmato riferimento i pacchetti NuGet
description: Requisiti per firmare il pacchetto NuGet.
author: rido-min
ms.author: rido-min
manager: unnir
ms.date: 04/24/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 751a8ff14bdc3a647985da4f908ad1a0fd0def9a
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2018
---
# <a name="signed-packages"></a><span data-ttu-id="1b795-103">Pacchetti firmati</span><span class="sxs-lookup"><span data-stu-id="1b795-103">Signed packages</span></span>

<span data-ttu-id="1b795-104">*NuGet 4.6.0+ e Visual Studio 2017 15,6 e versioni successive*</span><span class="sxs-lookup"><span data-stu-id="1b795-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="1b795-105">Pacchetti NuGet possono includere una firma digitale che fornisce la protezione del contenuto manomessa.</span><span class="sxs-lookup"><span data-stu-id="1b795-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="1b795-106">Questa firma viene generata da un certificato x. 509 che aggiunge anche modelli di prova di autenticità per l'origine del pacchetto effettiva.</span><span class="sxs-lookup"><span data-stu-id="1b795-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="1b795-107">Pacchetti firmati forniscono la convalida end-to-end più attendibili.</span><span class="sxs-lookup"><span data-stu-id="1b795-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="1b795-108">Una firma di autore garantisce che il pacchetto non è stato modificato dopo l'autore la firma del pacchetto, indipendentemente da quale metodo viene recapitato il pacchetto del trasporto repository o cosa.</span><span class="sxs-lookup"><span data-stu-id="1b795-108">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="1b795-109">I consumer che necessitano di un ambiente bloccato possono richiedere pacchetti firmati con un certificato specifico dell'autore.</span><span class="sxs-lookup"><span data-stu-id="1b795-109">Consumers who demand a locked-down environment can require packages signed with a specific author certificate.</span></span>

<span data-ttu-id="1b795-110">Inoltre, pacchetti firmati autore forniscono un meccanismo di autenticazione extra per la pipeline di pubblicazione nuget.org poiché il certificato di firma deve essere registrato anticipatamente.</span><span class="sxs-lookup"><span data-stu-id="1b795-110">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span>

<span data-ttu-id="1b795-111">Per informazioni dettagliate sulla creazione di un pacchetto firmato, vedere [firma pacchetti](../create-packages/Sign-a-package.md) e [comando sign nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="1b795-111">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="1b795-112">NuGet.org non accetta attualmente dei pacchetti firmati.</span><span class="sxs-lookup"><span data-stu-id="1b795-112">nuget.org does not presently accept signed packages.</span></span> <span data-ttu-id="1b795-113">È possibile firmare pacchetti per la pubblicazione in feed personalizzati.</span><span class="sxs-lookup"><span data-stu-id="1b795-113">You can sign packages for publishing to custom feeds.</span></span>

> [!Important]
> <span data-ttu-id="1b795-114">Firmare il pacchetto è attualmente supportata solo quando si utilizza nuget.exe in Windows.</span><span class="sxs-lookup"><span data-stu-id="1b795-114">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="1b795-115">Verifica dei pacchetti firmati è attualmente supportata solo quando si utilizza nuget.exe o Visual Studio in Windows.</span><span class="sxs-lookup"><span data-stu-id="1b795-115">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="1b795-116">Requisiti del certificato</span><span class="sxs-lookup"><span data-stu-id="1b795-116">Certificate requirements</span></span>

<span data-ttu-id="1b795-117">Firmare il pacchetto richiede un certificato, che è un tipo speciale di certificato valido per la firma del codice di `id-kp-codeSigning` scopo [[RFC 5280 sezione 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="1b795-117">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="1b795-118">Inoltre, il certificato deve avere una pubblica lunghezza della chiave RSA 2048 bit o superiore.</span><span class="sxs-lookup"><span data-stu-id="1b795-118">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="1b795-119">Ottenere un certificato di firma codice</span><span class="sxs-lookup"><span data-stu-id="1b795-119">Get a code signing certificate</span></span>

<span data-ttu-id="1b795-120">I certificati validi possono essere ottenuti da autorità di certificazione pubblica come:</span><span class="sxs-lookup"><span data-stu-id="1b795-120">Valid certificates may be obtained from public certificate authorities like:</span></span>

- [<span data-ttu-id="1b795-121">Symantec</span><span class="sxs-lookup"><span data-stu-id="1b795-121">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="1b795-122">DigiCert</span><span class="sxs-lookup"><span data-stu-id="1b795-122">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="1b795-123">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="1b795-123">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="1b795-124">Accesso globale</span><span class="sxs-lookup"><span data-stu-id="1b795-124">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="1b795-125">Comodo</span><span class="sxs-lookup"><span data-stu-id="1b795-125">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="1b795-126">Certum</span><span class="sxs-lookup"><span data-stu-id="1b795-126">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="1b795-127">L'elenco completo delle autorità di certificazione attendibile per Windows può essere ottenuto da [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="1b795-127">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="1b795-128">Creare un certificato di prova</span><span class="sxs-lookup"><span data-stu-id="1b795-128">Create a test certificate</span></span>

<span data-ttu-id="1b795-129">È possibile utilizzare i certificati autocertificati a scopo di test.</span><span class="sxs-lookup"><span data-stu-id="1b795-129">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="1b795-130">Per creare un'autocertificazione, utilizzare il [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) comando di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b795-130">To create a self-issued certificate, use the [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell command.</span></span>

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

<span data-ttu-id="1b795-131">Questo comando crea un certificato di test disponibile nell'archivio certificati personali dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="1b795-131">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="1b795-132">È possibile aprire l'archivio certificati eseguendo `certmgr.msc` per visualizzare il certificato appena creato.</span><span class="sxs-lookup"><span data-stu-id="1b795-132">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="1b795-133">Requisiti di timestamp</span><span class="sxs-lookup"><span data-stu-id="1b795-133">Timestamp requirements</span></span>

<span data-ttu-id="1b795-134">Pacchetti firmati devono includere un timestamp RFC 3161 per garantire la validità della firma oltre il periodo di validità del certificato di firma dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1b795-134">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="1b795-135">Il certificato utilizzato per firmare il timestamp deve essere valido per il `id-kp-timeStamping` scopo [[RFC 5280 sezione 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="1b795-135">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="1b795-136">Inoltre, il certificato deve avere una pubblica lunghezza della chiave RSA 2048 bit o superiore.</span><span class="sxs-lookup"><span data-stu-id="1b795-136">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="1b795-137">Altri dettagli tecnici, vedere il [specifiche tecniche di firma del pacchetto](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="1b795-137">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>
