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
# <a name="signed-packages"></a>Pacchetti firmati

*NuGet 4.6.0+ e Visual Studio 2017 15,6 e versioni successive*

Pacchetti NuGet possono includere una firma digitale che fornisce la protezione del contenuto manomessa. Questa firma viene generata da un certificato x. 509 che aggiunge anche modelli di prova di autenticità per l'origine del pacchetto effettiva.

Pacchetti firmati forniscono la convalida end-to-end più attendibili. Una firma di autore garantisce che il pacchetto non è stato modificato dopo l'autore la firma del pacchetto, indipendentemente da quale metodo viene recapitato il pacchetto del trasporto repository o cosa.

Inoltre, pacchetti firmati autore forniscono un meccanismo di autenticazione extra per la pipeline di pubblicazione nuget.org poiché il certificato di firma deve essere registrato anticipatamente. Per altre informazioni, vedere [registra i certificati](#register-certificate-on-nugetorg).

Per informazioni dettagliate sulla creazione di un pacchetto firmato, vedere [firma pacchetti](../create-packages/Sign-a-package.md) e [comando sign nuget](../tools/cli-ref-sign.md).

> [!Important]
> Firmare il pacchetto è attualmente supportata solo quando si utilizza nuget.exe in Windows. Verifica dei pacchetti firmati è attualmente supportata solo quando si utilizza nuget.exe o Visual Studio in Windows.

## <a name="certificate-requirements"></a>Requisiti del certificato

Firmare il pacchetto richiede un certificato, che è un tipo speciale di certificato valido per la firma del codice di `id-kp-codeSigning` scopo [[RFC 5280 sezione 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Inoltre, il certificato deve avere una pubblica lunghezza della chiave RSA 2048 bit o superiore.

## <a name="get-a-code-signing-certificate"></a>Ottenere un certificato di firma codice

I certificati validi possono essere ottenuti da un'autorità di certificazione pubblica, ad esempio:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Accesso globale](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

L'elenco completo delle autorità di certificazione attendibile per Windows può essere ottenuto da [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Creare un certificato di prova

È possibile utilizzare i certificati autocertificati a scopo di test. Per creare un'autocertificazione, usare il [comando di PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate.md).

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

Questo comando crea un certificato di test disponibile nell'archivio certificati personali dell'utente corrente. È possibile aprire l'archivio certificati eseguendo `certmgr.msc` per visualizzare il certificato appena creato.

> [!Warning]
> NuGet.org non accetta i pacchetti firmati con i certificati autocertificati.

## <a name="timestamp-requirements"></a>Requisiti di timestamp

Pacchetti firmati devono includere un timestamp RFC 3161 per garantire la validità della firma oltre il periodo di validità del certificato di firma dei pacchetti. Il certificato utilizzato per firmare il timestamp deve essere valido per il `id-kp-timeStamping` scopo [[RFC 5280 sezione 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Inoltre, il certificato deve avere una pubblica lunghezza della chiave RSA 2048 bit o superiore.

Altri dettagli tecnici, vedere il [specifiche tecniche di firma del pacchetto](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Requisiti per la firma in nuget.org

NuGet.org prevede requisiti aggiuntivi per l'accettazione di un pacchetto con segno:

- La firma primaria deve essere una firma dell'autore.
- La firma primaria deve avere un solo timestamp valido.
- I certificati X.509 per la firma di autore e la relativa firma timestamp:
  - Deve avere una chiave pubblica RSA 2048 bit o superiore.
  - Deve essere entro il relativo periodo di validità per ogni ora UTC corrente in fase di convalida del pacchetto in nuget.org.
  - Deve essere concatenato a un'autorità radice attendibile è considerato attendibile per impostazione predefinita in Windows. Pacchetti firmati con i certificati autocertificati vengono rifiutati.
  - Deve essere valido per il suo scopo: 
    - L'autore del certificato di firma deve essere valido per la firma del codice.
    - Il certificato di timestamp deve essere valido per l'aggiunta di timestamp.
  - Non deve essere revocato al momento della firma. (Potrebbe non trattarsi conosciuto in fase di invio, quindi nuget.org controlla periodicamente nuovamente lo stato di revoca).

## <a name="register-certificate-on-nugetorg"></a>Registrazione certificato in nuget.org

Per inviare un pacchetto con segno, è innanzitutto necessario registrare il certificato con nuget.org. È necessario il certificato come un `.cer` file in un formato DER binario. È possibile esportare un certificato esistente in un formato binario DER utilizzando Esportazione guidata certificati.

![Esportazione guidata certificati](media/CertificateExportWizard.png)

Gli utenti avanzati possono esportare il certificato usando il [comando Export-Certificate PowerShell](/powershell/module/pkiclient/export-certificate.md).

Per registrare il certificato con nuget.org, passare a `Certificates` sezione `Account settings` pagina (o pagina di impostazioni dell'organizzazione) e selezionare `Register new certificate`.

![Certificati registrati](media/registered-certs.png)

> [!Tip]
> Un utente può inviare che più certificati e lo stesso certificato possono essere registrati da più utenti.

Una volta che un utente dispone di un certificato registrato, tutti gli invii di pacchetto future **necessario** essere firmate con uno dei certificati.

Gli utenti possono inoltre rimuovere un certificato registrato dall'account. Dopo la rimozione di un certificato, pacchetti firmati con tale certificato non riuscire in invio. I pacchetti esistenti non sono interessati.

## <a name="configure-package-signing-requirements"></a>Configurare i requisiti di firma dei pacchetti

Se si è l'unico proprietario di un pacchetto, si è il firmatario richiesto. Vale a dire, è possibile utilizzare uno dei certificati registrati per firmare i pacchetti e inviare a nuget.org.

Se un pacchetto include più proprietari, per impostazione predefinita, i certificati del proprietario "Any" possono essere usati per firmare il pacchetto. Come Comproprietario del pacchetto, è possibile eseguire l'override "Any" con se stessi o altri Comproprietario sia il firmatario richiesto. Se si apporta un proprietario non ha registrato alcun certificato, saranno consentiti pacchetti non firmati. 

Analogamente, se il valore predefinito "Any" opzione è selezionata per un pacchetto in un solo proprietario disponga di un certificato registrato e un altro proprietario non ha registrato alcun certificato, quindi nuget.org accetta un pacchetto con segno con una firma registrata da uno dei proprietari o senza segno (perché uno dei proprietari non è registrato alcun certificato) del pacchetto.

![Configurare firmatari pacchetto](media/configure-package-signers.png)
