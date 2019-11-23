---
title: Firma di pacchetti NuGet
description: Informazioni su come è possibile usare pacchetti firmati per abilitare la verifica dell'integrità del contenuto.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 1053a18926f63e02f0b1c100e7cc1cd293654ced
ms.sourcegitcommit: e4b0ff4460865db6dc7bc9f20e9f644d98493011
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71307210"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="4ab57-103">Firma di pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="4ab57-103">Signing NuGet Packages</span></span>

<span data-ttu-id="4ab57-104">I pacchetti firmati consentono di eseguire controlli di verifica dell'integrità del contenuto che garantiscono protezione contro eventuali manomissioni del contenuto.</span><span class="sxs-lookup"><span data-stu-id="4ab57-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="4ab57-105">La firma del pacchetto, inoltre, funge da single source of truth riguardo all'origine del pacchetto e ne attesta l'autenticità presso il consumer.</span><span class="sxs-lookup"><span data-stu-id="4ab57-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="4ab57-106">Questa guida presuppone che [sia già stato creato un pacchetto](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="4ab57-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="4ab57-107">Ottenere un certificato di firma del codice</span><span class="sxs-lookup"><span data-stu-id="4ab57-107">Get a code signing certificate</span></span>

<span data-ttu-id="4ab57-108">I certificati validi possono essere ottenuti da un'autorità di certificazione pubblica, ad esempio [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)e così via. L'elenco completo di autorità di certificazione attendibili per Windows può essere ottenuto dalla [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="4ab57-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="4ab57-109">A scopo di test è possibile usare l'autocertificazione.</span><span class="sxs-lookup"><span data-stu-id="4ab57-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="4ab57-110">Tuttavia, i pacchetti firmati con certificati autocertificati non sono accettati da NuGet.org. Altre informazioni sulla [creazione di un certificato di prova](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="4ab57-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="4ab57-111">Esportare il file del certificato</span><span class="sxs-lookup"><span data-stu-id="4ab57-111">Export the certificate file</span></span>

* <span data-ttu-id="4ab57-112">È possibile esportare un certificato esistente in formato DER binario usando Esportazione guidata certificati.</span><span class="sxs-lookup"><span data-stu-id="4ab57-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Esportazione guidata certificati](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="4ab57-114">È anche possibile esportare il certificato usando il [comando Export-Certificate di PowerShell](/powershell/module/pkiclient/export-certificate).</span><span class="sxs-lookup"><span data-stu-id="4ab57-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="4ab57-115">Firmare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="4ab57-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="4ab57-116">Richiede NuGet. exe 4.6.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="4ab57-116">Requires nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="4ab57-117">il supporto di DotNet. exe sarà presto disponibile [#7939](https://github.com/NuGet/Home/issues/7939)</span><span class="sxs-lookup"><span data-stu-id="4ab57-117">dotnet.exe support is coming soon - [#7939](https://github.com/NuGet/Home/issues/7939)</span></span>

<span data-ttu-id="4ab57-118">Firmare il pacchetto usando il comando [sign](../reference/cli-reference/cli-ref-sign.md) di NuGet:</span><span class="sxs-lookup"><span data-stu-id="4ab57-118">Sign the package using [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> <span data-ttu-id="4ab57-119">Il provider di certificati offre spesso anche un URL del server di timestamp che è possibile usare per l'argomento facoltativo `Timestamper` mostrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4ab57-119">The certificate provider often also provides a timestamping server URL which you can use for the `Timestamper` optional argument show above.</span></span> <span data-ttu-id="4ab57-120">Consultare la documentazione e/o rivolgersi al supporto tecnico del provider per ottenere tale URL del servizio.</span><span class="sxs-lookup"><span data-stu-id="4ab57-120">Consult with your provider's documentation and/or support for that service URL.</span></span>

* <span data-ttu-id="4ab57-121">È possibile usare un certificato disponibile nell'archivio certificati o usare un certificato da un file.</span><span class="sxs-lookup"><span data-stu-id="4ab57-121">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="4ab57-122">Vedere Informazioni di riferimento sull'interfaccia della riga di comando per il comando [sign](../reference/cli-reference/cli-ref-sign.md) di NuGet.</span><span class="sxs-lookup"><span data-stu-id="4ab57-122">See CLI reference for [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span></span>
* <span data-ttu-id="4ab57-123">I pacchetti firmati devono includere un timestamp per assicurarsi che la firma rimanga valida dopo la scadenza del certificato di firma.</span><span class="sxs-lookup"><span data-stu-id="4ab57-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="4ab57-124">In caso contrario, l'operazione di firma genera un [avviso](../reference/errors-and-warnings/NU3002.md).</span><span class="sxs-lookup"><span data-stu-id="4ab57-124">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="4ab57-125">Per visualizzare i dettagli della firma di un determinato pacchetto, usare il comando [verify](../reference/cli-reference/cli-ref-verify.md) di NuGet.</span><span class="sxs-lookup"><span data-stu-id="4ab57-125">You can see the signature details of a given package using [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="4ab57-126">Registrare il certificato su NuGet.org</span><span class="sxs-lookup"><span data-stu-id="4ab57-126">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="4ab57-127">Per pubblicare un pacchetto firmato, è necessario prima registrare il certificato con NuGet.org. Il certificato è necessario come file di `.cer` in un formato DER binario.</span><span class="sxs-lookup"><span data-stu-id="4ab57-127">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="4ab57-128">[Eseguire l'accesso](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) a NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="4ab57-128">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="4ab57-129">Passare a `Account settings` oppure a `Manage Organization` **>** `Edit Organziation` se si desidera registrare il certificato con un account aziendale.</span><span class="sxs-lookup"><span data-stu-id="4ab57-129">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="4ab57-130">Espandere la sezione `Certificates` e selezionare `Register new`.</span><span class="sxs-lookup"><span data-stu-id="4ab57-130">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="4ab57-131">Individuare e selezionare il file di certificato esportato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4ab57-131">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="4ab57-132">![Certificati registrati](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="4ab57-132">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="4ab57-133">**Nota**</span><span class="sxs-lookup"><span data-stu-id="4ab57-133">**Note**</span></span>
* <span data-ttu-id="4ab57-134">Un utente può inviare più certificati e lo stesso certificato può essere registrato da più utenti.</span><span class="sxs-lookup"><span data-stu-id="4ab57-134">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="4ab57-135">Una volta che un utente dispone di un certificato registrato, tutti i pacchetti futuri inviati **dovranno obbligatoriamente** essere firmati con uno dei certificati.</span><span class="sxs-lookup"><span data-stu-id="4ab57-135">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="4ab57-136">Vedere [Gestire i requisiti di firma per il pacchetto in NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="4ab57-136">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="4ab57-137">Gli utenti possono anche rimuovere un certificato registrato dall'account.</span><span class="sxs-lookup"><span data-stu-id="4ab57-137">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="4ab57-138">Se un certificato è stato rimosso, i nuovi pacchetti firmati con tale certificato non potranno essere inviati.</span><span class="sxs-lookup"><span data-stu-id="4ab57-138">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="4ab57-139">I pacchetti esistenti non subiscono conseguenze.</span><span class="sxs-lookup"><span data-stu-id="4ab57-139">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="4ab57-140">Pubblicare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="4ab57-140">Publish the package</span></span>

<span data-ttu-id="4ab57-141">A questo punto è possibile pubblicare il pacchetto in NuGet.org. Vedere [pubblicazione di pacchetti](../nuget-org/Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="4ab57-141">You are now ready to publish the package to NuGet.org. See [Publishing packages](../nuget-org/Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="4ab57-142">Creare un certificato di test</span><span class="sxs-lookup"><span data-stu-id="4ab57-142">Create a test certificate</span></span>

<span data-ttu-id="4ab57-143">A scopo di test è possibile usare l'autocertificazione.</span><span class="sxs-lookup"><span data-stu-id="4ab57-143">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="4ab57-144">Per creare un'autocertificazione, usare il [comando New-SelfSignedCertificate di PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="4ab57-144">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate).</span></span>

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

<span data-ttu-id="4ab57-145">Il comando crea un certificato di test e lo rende disponibile nell'archivio certificati personali dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="4ab57-145">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="4ab57-146">Per visualizzare il certificato appena creato, aprire l'archivio certificati eseguendo `certmgr.msc`.</span><span class="sxs-lookup"><span data-stu-id="4ab57-146">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="4ab57-147">NuGet.org non accetta pacchetti firmati con autocertificazione.</span><span class="sxs-lookup"><span data-stu-id="4ab57-147">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="4ab57-148">Gestire i requisiti di firma per il pacchetto in NuGet.org</span><span class="sxs-lookup"><span data-stu-id="4ab57-148">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="4ab57-149">[Eseguire l'accesso](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) a NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="4ab57-149">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="4ab57-150">Passare a `Manage Packages` 
   ![Configurare i firmatari del pacchetto](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="4ab57-150">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="4ab57-151">Se è l'unico proprietario di un pacchetto, l'utente è il firmatario richiesto, ovvero può usare uno qualsiasi dei certificati registrati per firmare e pubblicare i pacchetti in NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="4ab57-151">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="4ab57-152">Se un pacchetto ha più proprietari, per impostazione predefinita, è possibile firmare il pacchetto usando i certificati di "Qualsiasi" proprietario.</span><span class="sxs-lookup"><span data-stu-id="4ab57-152">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="4ab57-153">In qualità di comproprietario del pacchetto, l'utente può indicare se stesso o un altro comproprietario come firmatario richiesto.</span><span class="sxs-lookup"><span data-stu-id="4ab57-153">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="4ab57-154">Se si configura un proprietario che non ha alcun certificato registrato, saranno ammessi i pacchetti non firmati.</span><span class="sxs-lookup"><span data-stu-id="4ab57-154">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="4ab57-155">Analogamente, se l'opzione predefinita "Qualsiasi" è selezionata per un pacchetto in cui un proprietario dispone di un certificato registrato e un altro proprietario non ha alcun certificato registrato, NuGet.org accetterà sia un pacchetto firmato con una firma registrata da uno dei proprietari sia un pacchetto non firmato, dal momento che uno dei proprietari non ha alcun certificato registrato.</span><span class="sxs-lookup"><span data-stu-id="4ab57-155">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="4ab57-156">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="4ab57-156">Related articles</span></span>

- [<span data-ttu-id="4ab57-157">Gestire i limiti di attendibilità dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="4ab57-157">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="4ab57-158">Informazioni di riferimento sui pacchetti firmati</span><span class="sxs-lookup"><span data-stu-id="4ab57-158">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
