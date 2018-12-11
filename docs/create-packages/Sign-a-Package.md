---
title: Firma di pacchetti NuGet
description: Informazioni su come è possibile usare pacchetti firmati per abilitare la verifica dell'integrità del contenuto.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e8955f9d46bab235c8755d5654814a4291d542d6
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977563"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="cf360-103">Firma di pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="cf360-103">Signing NuGet Packages</span></span>

<span data-ttu-id="cf360-104">I pacchetti firmati consentono di eseguire controlli di verifica dell'integrità del contenuto che garantiscono protezione contro eventuali manomissioni del contenuto.</span><span class="sxs-lookup"><span data-stu-id="cf360-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="cf360-105">La firma del pacchetto, inoltre, funge da single source of truth riguardo all'origine del pacchetto e ne attesta l'autenticità presso il consumer.</span><span class="sxs-lookup"><span data-stu-id="cf360-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="cf360-106">Questa guida presuppone che [sia già stato creato un pacchetto](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="cf360-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="cf360-107">Ottenere un certificato di firma del codice</span><span class="sxs-lookup"><span data-stu-id="cf360-107">Get a code signing certificate</span></span>

<span data-ttu-id="cf360-108">Si possono ottenere certificati validi da autorità di certificazione pubbliche, ad esempio [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) e così via. L'elenco completo delle autorità di certificazione attendibili per Windows è disponibile in [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="cf360-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="cf360-109">A scopo di test è possibile usare l'autocertificazione.</span><span class="sxs-lookup"><span data-stu-id="cf360-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="cf360-110">Tuttavia, i pacchetti firmati utilizzando l'autocertificazione non sono accettati da NuGet.org. Altre informazioni sulla [creazione di un certificato di test](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="cf360-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="cf360-111">Esportare il file del certificato</span><span class="sxs-lookup"><span data-stu-id="cf360-111">Export the certificate file</span></span>

* <span data-ttu-id="cf360-112">È possibile esportare un certificato esistente in formato DER binario usando Esportazione guidata certificati.</span><span class="sxs-lookup"><span data-stu-id="cf360-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Esportazione guidata certificati](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="cf360-114">È anche possibile esportare il certificato usando il [comando Export-Certificate di PowerShell](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="cf360-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="cf360-115">Firmare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="cf360-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="cf360-116">Richiede nuget.exe 4.6.0 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="cf360-116">Requires nuget.exe 4.6.0 or later</span></span>

<span data-ttu-id="cf360-117">Firmare il pacchetto usando il comando [sign](../tools/cli-ref-sign.md) di NuGet:</span><span class="sxs-lookup"><span data-stu-id="cf360-117">Sign the package using [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateFilePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

* <span data-ttu-id="cf360-118">È possibile usare un certificato disponibile nell'archivio certificati o usare un certificato da un file.</span><span class="sxs-lookup"><span data-stu-id="cf360-118">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="cf360-119">Vedere Informazioni di riferimento sull'interfaccia della riga di comando per il comando [sign](../tools/cli-ref-sign.md) di NuGet.</span><span class="sxs-lookup"><span data-stu-id="cf360-119">See CLI reference for [nuget sign](../tools/cli-ref-sign.md).</span></span>
* <span data-ttu-id="cf360-120">I pacchetti firmati devono includere un timestamp per assicurarsi che la firma rimanga valida dopo la scadenza del certificato di firma.</span><span class="sxs-lookup"><span data-stu-id="cf360-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="cf360-121">In caso contrario, l'operazione di firma genera un [avviso](../reference/errors-and-warnings/NU3002.md).</span><span class="sxs-lookup"><span data-stu-id="cf360-121">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="cf360-122">Per visualizzare i dettagli della firma di un determinato pacchetto, usare il comando [verify](../tools/cli-ref-verify.md) di NuGet.</span><span class="sxs-lookup"><span data-stu-id="cf360-122">You can see the signature details of a given package using [nuget verify](../tools/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="cf360-123">Registrare il certificato su NuGet.org</span><span class="sxs-lookup"><span data-stu-id="cf360-123">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="cf360-124">Per pubblicare un pacchetto firmato, è innanzitutto necessario registrare il certificato su NuGet.org. Il certificato deve essere un file `.cer` in formato DER binario.</span><span class="sxs-lookup"><span data-stu-id="cf360-124">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="cf360-125">[Eseguire l'accesso](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) a NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="cf360-125">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="cf360-126">Passare a `Account settings` oppure a `Manage Organization` **>** `Edit Organziation` se si desidera registrare il certificato con un account aziendale.</span><span class="sxs-lookup"><span data-stu-id="cf360-126">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="cf360-127">Espandere la sezione `Certificates` e selezionare `Register new`.</span><span class="sxs-lookup"><span data-stu-id="cf360-127">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="cf360-128">Individuare e selezionare il file di certificato esportato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="cf360-128">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="cf360-129">![Certificati registrati](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="cf360-129">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="cf360-130">**Nota**</span><span class="sxs-lookup"><span data-stu-id="cf360-130">**Note**</span></span>
* <span data-ttu-id="cf360-131">Un utente può inviare più certificati e lo stesso certificato può essere registrato da più utenti.</span><span class="sxs-lookup"><span data-stu-id="cf360-131">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="cf360-132">Una volta che un utente dispone di un certificato registrato, tutti i pacchetti futuri inviati **dovranno obbligatoriamente** essere firmati con uno dei certificati.</span><span class="sxs-lookup"><span data-stu-id="cf360-132">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="cf360-133">Vedere [Gestire i requisiti di firma per il pacchetto in NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="cf360-133">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="cf360-134">Gli utenti possono anche rimuovere un certificato registrato dall'account.</span><span class="sxs-lookup"><span data-stu-id="cf360-134">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="cf360-135">Se un certificato è stato rimosso, i nuovi pacchetti firmati con tale certificato non potranno essere inviati.</span><span class="sxs-lookup"><span data-stu-id="cf360-135">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="cf360-136">I pacchetti esistenti non subiscono conseguenze.</span><span class="sxs-lookup"><span data-stu-id="cf360-136">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="cf360-137">Pubblicare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="cf360-137">Publish the package</span></span>

<span data-ttu-id="cf360-138">A questo punto si è pronti a pubblicare il pacchetto in NuGet.org. Vedere [Pubblicazione di pacchetti](Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="cf360-138">You are now ready to publish the package to NuGet.org. See [Publishing packages](Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="cf360-139">Creare un certificato di test</span><span class="sxs-lookup"><span data-stu-id="cf360-139">Create a test certificate</span></span>

<span data-ttu-id="cf360-140">A scopo di test è possibile usare l'autocertificazione.</span><span class="sxs-lookup"><span data-stu-id="cf360-140">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="cf360-141">Per creare un'autocertificazione, usare il [comando New-SelfSignedCertificate di PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="cf360-141">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="cf360-142">Il comando crea un certificato di test e lo rende disponibile nell'archivio certificati personali dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="cf360-142">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="cf360-143">Per visualizzare il certificato appena creato, aprire l'archivio certificati eseguendo `certmgr.msc`.</span><span class="sxs-lookup"><span data-stu-id="cf360-143">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="cf360-144">NuGet.org non accetta pacchetti firmati con autocertificazione.</span><span class="sxs-lookup"><span data-stu-id="cf360-144">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="cf360-145">Gestire i requisiti di firma per il pacchetto in NuGet.org</span><span class="sxs-lookup"><span data-stu-id="cf360-145">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="cf360-146">[Eseguire l'accesso](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) a NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="cf360-146">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="cf360-147">Passare a `Manage Packages` 
   ![Configurare i firmatari del pacchetto](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="cf360-147">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="cf360-148">Se è l'unico proprietario di un pacchetto, l'utente è il firmatario richiesto, ovvero può usare uno qualsiasi dei certificati registrati per firmare e pubblicare i pacchetti in NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="cf360-148">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="cf360-149">Se un pacchetto ha più proprietari, per impostazione predefinita, è possibile firmare il pacchetto usando i certificati di "Qualsiasi" proprietario.</span><span class="sxs-lookup"><span data-stu-id="cf360-149">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="cf360-150">In qualità di comproprietario del pacchetto, l'utente può indicare se stesso o un altro comproprietario come firmatario richiesto.</span><span class="sxs-lookup"><span data-stu-id="cf360-150">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="cf360-151">Se si configura un proprietario che non ha alcun certificato registrato, saranno ammessi i pacchetti non firmati.</span><span class="sxs-lookup"><span data-stu-id="cf360-151">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="cf360-152">Analogamente, se l'opzione predefinita "Qualsiasi" è selezionata per un pacchetto in cui un proprietario dispone di un certificato registrato e un altro proprietario non ha alcun certificato registrato, NuGet.org accetterà sia un pacchetto firmato con una firma registrata da uno dei proprietari sia un pacchetto non firmato, dal momento che uno dei proprietari non ha alcun certificato registrato.</span><span class="sxs-lookup"><span data-stu-id="cf360-152">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="cf360-153">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="cf360-153">Related articles</span></span>

- [<span data-ttu-id="cf360-154">Installazione di pacchetti firmati</span><span class="sxs-lookup"><span data-stu-id="cf360-154">Installing signed packages</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="cf360-155">Informazioni di riferimento sui pacchetti firmati</span><span class="sxs-lookup"><span data-stu-id="cf360-155">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
