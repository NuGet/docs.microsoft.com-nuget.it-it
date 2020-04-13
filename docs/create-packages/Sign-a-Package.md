---
title: Firma di pacchetti NuGet
description: Informazioni su come è possibile usare pacchetti firmati per abilitare la verifica dell'integrità del contenuto.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 00fe1d5fa81132b5d6826203a0d26e56aa8d4755
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429003"
---
# <a name="signing-nuget-packages"></a>Firma di pacchetti NuGet

I pacchetti firmati consentono di eseguire controlli di verifica dell'integrità del contenuto che garantiscono protezione contro eventuali manomissioni del contenuto. La firma del pacchetto, inoltre, funge da single source of truth riguardo all'origine del pacchetto e ne attesta l'autenticità presso il consumer. Questa guida presuppone che [sia già stato creato un pacchetto](creating-a-package.md).

## <a name="get-a-code-signing-certificate"></a>Ottenere un certificato di firma del codice

Certificati validi possono essere ottenuti da un'autorità di certificazione pubblica, ad esempio [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)e così via. L'elenco completo delle autorità di certificazione attendibili da Windows può essere ottenuto da [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners).

A scopo di test è possibile usare l'autocertificazione. Tuttavia, i pacchetti firmati utilizzando certificati auto-emessi non sono accettati da NuGet.org. Altre informazioni sulla creazione di un certificato di [provaLearn](#create-a-test-certificate) more about creating a test certificate

## <a name="export-the-certificate-file"></a>Esportare il file del certificato

* È possibile esportare un certificato esistente in formato DER binario usando Esportazione guidata certificati.

  ![Esportazione guidata certificati](../reference/media/CertificateExportWizard.png)

* È anche possibile esportare il certificato usando il [comando Export-Certificate di PowerShell](/powershell/module/pkiclient/export-certificate).

## <a name="sign-the-package"></a>Firmare il pacchetto

> [!note]
> Richiede nuget.exe 4.6.0 o versione successiva. Il supporto dotnet.exe è in arrivo - [#7939](https://github.com/NuGet/Home/issues/7939)

Firmare il pacchetto usando il comando [sign](../reference/cli-reference/cli-ref-sign.md) di NuGet:

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> Il provider di certificati offre spesso anche un URL del server di timestamp che è possibile usare per l'argomento facoltativo `Timestamper` mostrato in precedenza. Consultare la documentazione e/o rivolgersi al supporto tecnico del provider per ottenere tale URL del servizio.

* È possibile usare un certificato disponibile nell'archivio certificati o usare un certificato da un file. Vedere Informazioni di riferimento sull'interfaccia della riga di comando per il comando [sign](../reference/cli-reference/cli-ref-sign.md) di NuGet.
* I pacchetti firmati devono includere un timestamp per assicurarsi che la firma rimanga valida dopo la scadenza del certificato di firma. In caso contrario, l'operazione di firma genera un [avviso](../reference/errors-and-warnings/NU3002.md).
* Per visualizzare i dettagli della firma di un determinato pacchetto, usare il comando [verify](../reference/cli-reference/cli-ref-verify.md) di NuGet.

## <a name="register-the-certificate-on-nugetorg"></a>Registrare il certificato su NuGet.org

Per pubblicare un pacchetto firmato, è innanzitutto necessario registrare il certificato con NuGet.org. È necessario il `.cer` certificato come file in un formato DER binario.

1. [Eseguire l'accesso](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) a NuGet.org.
1. Passare a `Account settings` oppure a `Manage Organization` **>** `Edit Organziation` se si desidera registrare il certificato con un account aziendale.
1. Espandere la sezione `Certificates` e selezionare `Register new`.
1. Individuare e selezionare il file di certificato esportato in precedenza.
  ![Certificati registrati](../reference/media/registered-certs.png)

**Nota**
* Un utente può inviare più certificati e lo stesso certificato può essere registrato da più utenti.
* Una volta che un utente dispone di un certificato registrato, tutti i pacchetti futuri inviati **dovranno obbligatoriamente** essere firmati con uno dei certificati. Vedere [Gestire i requisiti di firma per il pacchetto in NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)
* Gli utenti possono anche rimuovere un certificato registrato dall'account. Se un certificato è stato rimosso, i nuovi pacchetti firmati con tale certificato non potranno essere inviati. I pacchetti esistenti non subiscono conseguenze.

## <a name="publish-the-package"></a>Pubblicare il pacchetto

È ora possibile pubblicare il pacchetto per NuGet.org. Consultate [Pubblicazione di pacchetti](../nuget-org/Publish-a-package.md).

## <a name="create-a-test-certificate"></a>Creare un certificato di test

A scopo di test è possibile usare l'autocertificazione. Per creare un'autocertificazione, usare il [comando New-SelfSignedCertificate di PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate).

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

Il comando crea un certificato di test e lo rende disponibile nell'archivio certificati personali dell'utente corrente. Per visualizzare il certificato appena creato, aprire l'archivio certificati eseguendo `certmgr.msc`.

> [!Warning]
> NuGet.org non accetta pacchetti firmati con autocertificazione.

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>Gestire i requisiti di firma per il pacchetto in NuGet.org
1. [Eseguire l'accesso](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) a NuGet.org.

1. Passare a `Manage Packages` 
   ![Configurare i firmatari del pacchetto](../reference/media/configure-package-signers.png)

* Se è l'unico proprietario di un pacchetto, l'utente è il firmatario richiesto, ovvero può usare uno qualsiasi dei certificati registrati per firmare e pubblicare i pacchetti in NuGet.org.

* Se un pacchetto ha più proprietari, per impostazione predefinita, è possibile firmare il pacchetto usando i certificati di "Qualsiasi" proprietario. In qualità di comproprietario del pacchetto, l'utente può indicare se stesso o un altro comproprietario come firmatario richiesto. Se si configura un proprietario che non ha alcun certificato registrato, saranno ammessi i pacchetti non firmati. 

* Analogamente, se l'opzione predefinita "Qualsiasi" è selezionata per un pacchetto in cui un proprietario dispone di un certificato registrato e un altro proprietario non ha alcun certificato registrato, NuGet.org accetterà sia un pacchetto firmato con una firma registrata da uno dei proprietari sia un pacchetto non firmato, dal momento che uno dei proprietari non ha alcun certificato registrato.

## <a name="related-articles"></a>Articoli correlati

- [Gestire i limiti di attendibilità dei pacchetti](../consume-packages/installing-signed-packages.md)
- [Informazioni di riferimento sui pacchetti firmati](../reference/Signed-Packages-Reference.md)
