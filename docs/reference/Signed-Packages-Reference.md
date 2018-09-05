---
title: Pacchetti firmati
description: Requisiti per la firma del pacchetto NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c36db9486ad787f19430c75fc38a2e9dd8ba6e37
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550421"
---
# <a name="signed-packages"></a><span data-ttu-id="111ae-103">Pacchetti firmati</span><span class="sxs-lookup"><span data-stu-id="111ae-103">Signed packages</span></span>

<span data-ttu-id="111ae-104">*4.6.0+ NuGet e Visual Studio 2017 versione 15.6 e versioni successive*</span><span class="sxs-lookup"><span data-stu-id="111ae-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="111ae-105">I pacchetti NuGet possono includere una firma digitale che offre protezione contro i contenuti manomessi.</span><span class="sxs-lookup"><span data-stu-id="111ae-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="111ae-106">Questa firma viene generata da un certificato X.509 che aggiunge inoltre prove autenticità per l'origine del pacchetto effettiva.</span><span class="sxs-lookup"><span data-stu-id="111ae-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="111ae-107">I pacchetti firmati forniscono la convalida end-to-end più attendibili.</span><span class="sxs-lookup"><span data-stu-id="111ae-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="111ae-108">Esistono due diversi tipi di firme di NuGet:</span><span class="sxs-lookup"><span data-stu-id="111ae-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="111ae-109">**Creare una firma**.</span><span class="sxs-lookup"><span data-stu-id="111ae-109">**Author Signature**.</span></span> <span data-ttu-id="111ae-110">Una firma di autore garantisce che il pacchetto non è stato modificato dopo l'autore firma il pacchetto, non importa da quale metodo viene recapitato il pacchetto del trasporto repository o un'azione.</span><span class="sxs-lookup"><span data-stu-id="111ae-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="111ae-111">Inoltre, pacchetti firmati dall'autore forniscono un meccanismo di autenticazione extra per la pipeline di pubblicazione di nuget.org perché il certificato di firma deve essere registrato anticipatamente.</span><span class="sxs-lookup"><span data-stu-id="111ae-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="111ae-112">Per altre informazioni, vedere [registrare i certificati](#register-certificate-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="111ae-112">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>
- <span data-ttu-id="111ae-113">**Firma repository**.</span><span class="sxs-lookup"><span data-stu-id="111ae-113">**Repository Signature**.</span></span> <span data-ttu-id="111ae-114">Le firme di repository forniscono una garanzia di integrità per **tutti** in un repository di pacchetti che siano autore firmato o No, anche se tali pacchetti sono ottenuti da una posizione diversa nel repository originale dove si trovavano eseguito l'accesso.</span><span class="sxs-lookup"><span data-stu-id="111ae-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="111ae-115">Per informazioni dettagliate sulla creazione di un pacchetto firmato autore, vedere [firma dei pacchetti](../create-packages/Sign-a-package.md) e il [comando nuget sign](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="111ae-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="111ae-116">La firma del pacchetto è attualmente supportata solo quando si usa nuget.exe in Windows.</span><span class="sxs-lookup"><span data-stu-id="111ae-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="111ae-117">Verifica dei pacchetti firmati è attualmente supportata solo quando si usa nuget.exe o Visual Studio in Windows.</span><span class="sxs-lookup"><span data-stu-id="111ae-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="111ae-118">Requisiti del certificato</span><span class="sxs-lookup"><span data-stu-id="111ae-118">Certificate requirements</span></span>

<span data-ttu-id="111ae-119">Firmare il pacchetto richiede un codice di firma del certificato, ovvero un tipo speciale di certificato valido per il `id-kp-codeSigning` scopo [[RFC 5280 sezione 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="111ae-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="111ae-120">Inoltre, il certificato deve avere una pubblica lunghezza della chiave RSA di 2.048 bit o superiore.</span><span class="sxs-lookup"><span data-stu-id="111ae-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="111ae-121">Ottenere un certificato di firma codice</span><span class="sxs-lookup"><span data-stu-id="111ae-121">Get a code signing certificate</span></span>

<span data-ttu-id="111ae-122">I certificati validi possono essere ottenuti da un'autorità di certificazione pubblica, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="111ae-122">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="111ae-123">Symantec</span><span class="sxs-lookup"><span data-stu-id="111ae-123">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="111ae-124">DigiCert</span><span class="sxs-lookup"><span data-stu-id="111ae-124">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="111ae-125">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="111ae-125">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="111ae-126">Accesso globale</span><span class="sxs-lookup"><span data-stu-id="111ae-126">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="111ae-127">Comodo</span><span class="sxs-lookup"><span data-stu-id="111ae-127">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="111ae-128">Certum</span><span class="sxs-lookup"><span data-stu-id="111ae-128">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="111ae-129">L'elenco completo delle autorità di certificazione attendibile per Windows può essere ottenuto da [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="111ae-129">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="111ae-130">Creare un certificato di test</span><span class="sxs-lookup"><span data-stu-id="111ae-130">Create a test certificate</span></span>

<span data-ttu-id="111ae-131">È possibile usare i certificati autocertificati a scopo di test.</span><span class="sxs-lookup"><span data-stu-id="111ae-131">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="111ae-132">Per creare un certificato autocertificato, usare il [comandi di PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="111ae-132">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="111ae-133">Questo comando crea un certificato di test disponibile nell'archivio certificati personali dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="111ae-133">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="111ae-134">È possibile aprire l'archivio certificati eseguendo `certmgr.msc` per visualizzare il certificato appena creato.</span><span class="sxs-lookup"><span data-stu-id="111ae-134">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="111ae-135">NuGet.org non accetta i pacchetti firmati con i certificati autocertificati.</span><span class="sxs-lookup"><span data-stu-id="111ae-135">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="111ae-136">Requisiti di timestamp</span><span class="sxs-lookup"><span data-stu-id="111ae-136">Timestamp requirements</span></span>

<span data-ttu-id="111ae-137">I pacchetti firmati devono includere un timestamp RFC 3161 per assicurare la validità della firma oltre il periodo di validità del certificato di firma del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="111ae-137">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="111ae-138">Il certificato usato per firmare il timestamp deve essere valido per il `id-kp-timeStamping` scopo [[RFC 5280 sezione 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="111ae-138">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="111ae-139">Inoltre, il certificato deve avere una pubblica lunghezza della chiave RSA di 2.048 bit o superiore.</span><span class="sxs-lookup"><span data-stu-id="111ae-139">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="111ae-140">Altri dettagli tecnici sono reperibili nel [conoscere le specifiche tecniche di firma del pacchetto](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="111ae-140">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="111ae-141">Requisiti di firma in nuget.org</span><span class="sxs-lookup"><span data-stu-id="111ae-141">Signature requirements on nuget.org</span></span>

<span data-ttu-id="111ae-142">NuGet.org prevede requisiti aggiuntivi per l'accettazione di un pacchetto firmato:</span><span class="sxs-lookup"><span data-stu-id="111ae-142">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="111ae-143">La firma primaria deve essere una firma di autore.</span><span class="sxs-lookup"><span data-stu-id="111ae-143">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="111ae-144">La firma primaria deve avere un solo timestamp valido.</span><span class="sxs-lookup"><span data-stu-id="111ae-144">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="111ae-145">I certificati X.509 per la firma dell'autore e la firma del timestamp:</span><span class="sxs-lookup"><span data-stu-id="111ae-145">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="111ae-146">Deve avere una chiave pubblica RSA 2048 bit o superiore.</span><span class="sxs-lookup"><span data-stu-id="111ae-146">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="111ae-147">Deve essere entro il relativo periodo di validità per ogni ora UTC corrente in fase di convalida del pacchetto in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="111ae-147">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="111ae-148">Deve essere concatenato a un'autorità radice attendibile è considerato attendibile per impostazione predefinita in Windows.</span><span class="sxs-lookup"><span data-stu-id="111ae-148">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="111ae-149">I pacchetti firmati con i certificati autocertificati vengono rifiutati.</span><span class="sxs-lookup"><span data-stu-id="111ae-149">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="111ae-150">Deve essere valido per il suo scopo:</span><span class="sxs-lookup"><span data-stu-id="111ae-150">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="111ae-151">L'autore del certificato di firma deve essere valido per la firma del codice.</span><span class="sxs-lookup"><span data-stu-id="111ae-151">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="111ae-152">Il certificato di timestamp deve essere valido per l'aggiunta di timestamp.</span><span class="sxs-lookup"><span data-stu-id="111ae-152">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="111ae-153">Non deve essere revocato al momento della firma.</span><span class="sxs-lookup"><span data-stu-id="111ae-153">Must not be revoked at signing time.</span></span> <span data-ttu-id="111ae-154">(Ciò potrebbe non essere conosciuto al momento dell'invio, in modo da nuget.org a controlli periodicamente lo stato di revoca).</span><span class="sxs-lookup"><span data-stu-id="111ae-154">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="111ae-155">Registrare il certificato in nuget.org</span><span class="sxs-lookup"><span data-stu-id="111ae-155">Register certificate on nuget.org</span></span>

<span data-ttu-id="111ae-156">Per inviare un pacchetto firmato, è innanzitutto necessario registrare il certificato con nuget.org. È necessario il certificato come una `.cer` file in un formato DER binario.</span><span class="sxs-lookup"><span data-stu-id="111ae-156">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="111ae-157">È possibile esportare un certificato esistente in un formato DER binario usando l'esportazione guidata certificati.</span><span class="sxs-lookup"><span data-stu-id="111ae-157">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![Esportazione guidata certificati](media/CertificateExportWizard.png)

<span data-ttu-id="111ae-159">Gli utenti avanzati possono esportare il certificato usando il [comando Export-Certificate PowerShell](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="111ae-159">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="111ae-160">Per registrare il certificato con nuget.org, passare a `Certificates` nella sezione `Account settings` pagina (o pagina di impostazioni dell'organizzazione) e selezionare `Register new certificate`.</span><span class="sxs-lookup"><span data-stu-id="111ae-160">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![Certificati registrati](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="111ae-162">Un utente può inviare che più certificati e lo stesso certificato può essere registrati da più utenti.</span><span class="sxs-lookup"><span data-stu-id="111ae-162">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="111ae-163">Una volta che un utente dispone di un certificato registrato, tutti gli invii di pacchetto futuri **necessario** siano firmate con uno dei certificati.</span><span class="sxs-lookup"><span data-stu-id="111ae-163">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="111ae-164">Gli utenti possono inoltre rimuovere un certificato registrato dall'account.</span><span class="sxs-lookup"><span data-stu-id="111ae-164">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="111ae-165">Dopo la rimozione di un certificato, i pacchetti firmati con tale certificato non riuscire in invio.</span><span class="sxs-lookup"><span data-stu-id="111ae-165">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="111ae-166">I pacchetti esistenti non sono interessati.</span><span class="sxs-lookup"><span data-stu-id="111ae-166">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="111ae-167">Configurare i requisiti di firma del pacchetto</span><span class="sxs-lookup"><span data-stu-id="111ae-167">Configure package signing requirements</span></span>

<span data-ttu-id="111ae-168">Se sei l'unico proprietario di un pacchetto, si è il firmatario richiesto.</span><span class="sxs-lookup"><span data-stu-id="111ae-168">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="111ae-169">Vale a dire, è possibile utilizzare uno dei certificati registrati per firmare i pacchetti e inviare in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="111ae-169">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="111ae-170">Se un pacchetto include più proprietari, per impostazione predefinita, i certificati del proprietario della "Any" possono essere usati per firmare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="111ae-170">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="111ae-171">Come co-proprietario del pacchetto, è possibile eseguire l'override "Any" con se stessi o altri Comproprietario sia il firmatario richiesto.</span><span class="sxs-lookup"><span data-stu-id="111ae-171">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="111ae-172">Se si apporta un proprietario non ha alcun certificato registrato, quindi i pacchetti non firmati potrà essere.</span><span class="sxs-lookup"><span data-stu-id="111ae-172">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="111ae-173">Analogamente, se il valore predefinito "Any" opzione è selezionata per un pacchetto in cui un solo proprietario dispone di un certificato registrato e un altro proprietario non ha alcun certificato registrato, quindi nuget.org accetta entrambi un pacchetto firmato con una firma registrata da uno dei proprietari o unsigned (perché uno dei proprietari non è disponibile alcun certificato registrato) del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="111ae-173">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![Configurare i firmatari pacchetto](media/configure-package-signers.png)
