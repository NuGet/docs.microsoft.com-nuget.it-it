---
title: Pacchetti firmati
description: Requisiti per firmare il pacchetto NuGet.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 72fb1a87c13160c53f632d2ef87a12a4e9bc02a3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2018
---
# <a name="signed-packages"></a><span data-ttu-id="f5603-103">Pacchetti firmati</span><span class="sxs-lookup"><span data-stu-id="f5603-103">Signed packages</span></span>

<span data-ttu-id="f5603-104">*NuGet 4.6.0+ e Visual Studio 2017 15,6 e versioni successive*</span><span class="sxs-lookup"><span data-stu-id="f5603-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="f5603-105">Pacchetti NuGet possono includere una firma digitale che fornisce la protezione del contenuto manomessa.</span><span class="sxs-lookup"><span data-stu-id="f5603-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="f5603-106">Questa firma viene generata da un certificato x. 509 che aggiunge anche modelli di prova di autenticità per l'origine del pacchetto effettiva.</span><span class="sxs-lookup"><span data-stu-id="f5603-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="f5603-107">Pacchetti firmati forniscono la convalida end-to-end più attendibili.</span><span class="sxs-lookup"><span data-stu-id="f5603-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="f5603-108">Una firma di autore garantisce che il pacchetto non è stato modificato dopo l'autore la firma del pacchetto, indipendentemente da quale metodo viene recapitato il pacchetto del trasporto repository o cosa.</span><span class="sxs-lookup"><span data-stu-id="f5603-108">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="f5603-109">Inoltre, pacchetti firmati autore forniscono un meccanismo di autenticazione extra per la pipeline di pubblicazione nuget.org poiché il certificato di firma deve essere registrato anticipatamente.</span><span class="sxs-lookup"><span data-stu-id="f5603-109">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="f5603-110">Per altre informazioni, vedere [registra i certificati](#register-certificate-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="f5603-110">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>

<span data-ttu-id="f5603-111">Per informazioni dettagliate sulla creazione di un pacchetto firmato, vedere [firma pacchetti](../create-packages/Sign-a-package.md) e [comando sign nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="f5603-111">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="f5603-112">Firmare il pacchetto è attualmente supportata solo quando si utilizza nuget.exe in Windows.</span><span class="sxs-lookup"><span data-stu-id="f5603-112">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="f5603-113">Verifica dei pacchetti firmati è attualmente supportata solo quando si utilizza nuget.exe o Visual Studio in Windows.</span><span class="sxs-lookup"><span data-stu-id="f5603-113">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="f5603-114">Requisiti del certificato</span><span class="sxs-lookup"><span data-stu-id="f5603-114">Certificate requirements</span></span>

<span data-ttu-id="f5603-115">Firmare il pacchetto richiede un certificato, che è un tipo speciale di certificato valido per la firma del codice di `id-kp-codeSigning` scopo [[RFC 5280 sezione 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="f5603-115">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="f5603-116">Inoltre, il certificato deve avere una pubblica lunghezza della chiave RSA 2048 bit o superiore.</span><span class="sxs-lookup"><span data-stu-id="f5603-116">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="f5603-117">Ottenere un certificato di firma codice</span><span class="sxs-lookup"><span data-stu-id="f5603-117">Get a code signing certificate</span></span>

<span data-ttu-id="f5603-118">I certificati validi possono essere ottenuti da un'autorità di certificazione pubblica, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="f5603-118">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="f5603-119">Symantec</span><span class="sxs-lookup"><span data-stu-id="f5603-119">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="f5603-120">DigiCert</span><span class="sxs-lookup"><span data-stu-id="f5603-120">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="f5603-121">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="f5603-121">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="f5603-122">Accesso globale</span><span class="sxs-lookup"><span data-stu-id="f5603-122">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="f5603-123">Comodo</span><span class="sxs-lookup"><span data-stu-id="f5603-123">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="f5603-124">Certum</span><span class="sxs-lookup"><span data-stu-id="f5603-124">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="f5603-125">L'elenco completo delle autorità di certificazione attendibile per Windows può essere ottenuto da [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="f5603-125">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="f5603-126">Creare un certificato di prova</span><span class="sxs-lookup"><span data-stu-id="f5603-126">Create a test certificate</span></span>

<span data-ttu-id="f5603-127">È possibile utilizzare i certificati autocertificati a scopo di test.</span><span class="sxs-lookup"><span data-stu-id="f5603-127">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="f5603-128">Per creare un'autocertificazione, usare il [comando di PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="f5603-128">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="f5603-129">Questo comando crea un certificato di test disponibile nell'archivio certificati personali dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="f5603-129">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="f5603-130">È possibile aprire l'archivio certificati eseguendo `certmgr.msc` per visualizzare il certificato appena creato.</span><span class="sxs-lookup"><span data-stu-id="f5603-130">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="f5603-131">NuGet.org non accetta i pacchetti firmati con i certificati autocertificati.</span><span class="sxs-lookup"><span data-stu-id="f5603-131">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="f5603-132">Requisiti di timestamp</span><span class="sxs-lookup"><span data-stu-id="f5603-132">Timestamp requirements</span></span>

<span data-ttu-id="f5603-133">Pacchetti firmati devono includere un timestamp RFC 3161 per garantire la validità della firma oltre il periodo di validità del certificato di firma dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f5603-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="f5603-134">Il certificato utilizzato per firmare il timestamp deve essere valido per il `id-kp-timeStamping` scopo [[RFC 5280 sezione 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="f5603-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="f5603-135">Inoltre, il certificato deve avere una pubblica lunghezza della chiave RSA 2048 bit o superiore.</span><span class="sxs-lookup"><span data-stu-id="f5603-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="f5603-136">Altri dettagli tecnici, vedere il [specifiche tecniche di firma del pacchetto](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="f5603-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="f5603-137">Requisiti per la firma in nuget.org</span><span class="sxs-lookup"><span data-stu-id="f5603-137">Signature requirements on nuget.org</span></span>

<span data-ttu-id="f5603-138">NuGet.org prevede requisiti aggiuntivi per l'accettazione di un pacchetto con segno:</span><span class="sxs-lookup"><span data-stu-id="f5603-138">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="f5603-139">La firma primaria deve essere una firma dell'autore.</span><span class="sxs-lookup"><span data-stu-id="f5603-139">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="f5603-140">La firma primaria deve avere un solo timestamp valido.</span><span class="sxs-lookup"><span data-stu-id="f5603-140">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="f5603-141">I certificati X.509 per la firma di autore e la relativa firma timestamp:</span><span class="sxs-lookup"><span data-stu-id="f5603-141">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="f5603-142">Deve avere una chiave pubblica RSA 2048 bit o superiore.</span><span class="sxs-lookup"><span data-stu-id="f5603-142">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="f5603-143">Deve essere entro il relativo periodo di validità per ogni ora UTC corrente in fase di convalida del pacchetto in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f5603-143">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="f5603-144">Deve essere concatenato a un'autorità radice attendibile è considerato attendibile per impostazione predefinita in Windows.</span><span class="sxs-lookup"><span data-stu-id="f5603-144">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="f5603-145">Pacchetti firmati con i certificati autocertificati vengono rifiutati.</span><span class="sxs-lookup"><span data-stu-id="f5603-145">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="f5603-146">Deve essere valido per il suo scopo:</span><span class="sxs-lookup"><span data-stu-id="f5603-146">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="f5603-147">L'autore del certificato di firma deve essere valido per la firma del codice.</span><span class="sxs-lookup"><span data-stu-id="f5603-147">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="f5603-148">Il certificato di timestamp deve essere valido per l'aggiunta di timestamp.</span><span class="sxs-lookup"><span data-stu-id="f5603-148">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="f5603-149">Non deve essere revocato al momento della firma.</span><span class="sxs-lookup"><span data-stu-id="f5603-149">Must not be revoked at signing time.</span></span> <span data-ttu-id="f5603-150">(Potrebbe non trattarsi conosciuto in fase di invio, quindi nuget.org controlla periodicamente nuovamente lo stato di revoca).</span><span class="sxs-lookup"><span data-stu-id="f5603-150">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="f5603-151">Registrazione certificato in nuget.org</span><span class="sxs-lookup"><span data-stu-id="f5603-151">Register certificate on nuget.org</span></span>

<span data-ttu-id="f5603-152">Per inviare un pacchetto con segno, è innanzitutto necessario registrare il certificato con nuget.org. È necessario il certificato come un `.cer` file in un formato DER binario.</span><span class="sxs-lookup"><span data-stu-id="f5603-152">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="f5603-153">È possibile esportare un certificato esistente in un formato binario DER utilizzando Esportazione guidata certificati.</span><span class="sxs-lookup"><span data-stu-id="f5603-153">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![Esportazione guidata certificati](media/CertificateExportWizard.png)

<span data-ttu-id="f5603-155">Gli utenti avanzati possono esportare il certificato usando il [comando Export-Certificate PowerShell](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="f5603-155">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="f5603-156">Per registrare il certificato con nuget.org, passare a `Certificates` sezione `Account settings` pagina (o pagina di impostazioni dell'organizzazione) e selezionare `Register new certificate`.</span><span class="sxs-lookup"><span data-stu-id="f5603-156">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![Certificati registrati](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="f5603-158">Un utente può inviare che più certificati e lo stesso certificato possono essere registrati da più utenti.</span><span class="sxs-lookup"><span data-stu-id="f5603-158">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="f5603-159">Una volta che un utente dispone di un certificato registrato, tutti gli invii di pacchetto future **necessario** essere firmate con uno dei certificati.</span><span class="sxs-lookup"><span data-stu-id="f5603-159">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="f5603-160">Gli utenti possono inoltre rimuovere un certificato registrato dall'account.</span><span class="sxs-lookup"><span data-stu-id="f5603-160">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="f5603-161">Dopo la rimozione di un certificato, pacchetti firmati con tale certificato non riuscire in invio.</span><span class="sxs-lookup"><span data-stu-id="f5603-161">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="f5603-162">I pacchetti esistenti non sono interessati.</span><span class="sxs-lookup"><span data-stu-id="f5603-162">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="f5603-163">Configurare i requisiti di firma dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="f5603-163">Configure package signing requirements</span></span>

<span data-ttu-id="f5603-164">Se si è l'unico proprietario di un pacchetto, si è il firmatario richiesto.</span><span class="sxs-lookup"><span data-stu-id="f5603-164">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="f5603-165">Vale a dire, è possibile utilizzare uno dei certificati registrati per firmare i pacchetti e inviare a nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f5603-165">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="f5603-166">Se un pacchetto include più proprietari, per impostazione predefinita, i certificati del proprietario "Any" possono essere usati per firmare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f5603-166">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="f5603-167">Come Comproprietario del pacchetto, è possibile eseguire l'override "Any" con se stessi o altri Comproprietario sia il firmatario richiesto.</span><span class="sxs-lookup"><span data-stu-id="f5603-167">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="f5603-168">Se si apporta un proprietario non ha registrato alcun certificato, saranno consentiti pacchetti non firmati.</span><span class="sxs-lookup"><span data-stu-id="f5603-168">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="f5603-169">Analogamente, se il valore predefinito "Any" opzione è selezionata per un pacchetto in un solo proprietario disponga di un certificato registrato e un altro proprietario non ha registrato alcun certificato, quindi nuget.org accetta un pacchetto con segno con una firma registrata da uno dei proprietari o senza segno (perché uno dei proprietari non è registrato alcun certificato) del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f5603-169">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![Configurare firmatari pacchetto](media/configure-package-signers.png)
