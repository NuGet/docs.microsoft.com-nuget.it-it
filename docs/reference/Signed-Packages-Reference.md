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
# <a name="signed-packages"></a>Pacchetti firmati

*4.6.0+ NuGet e Visual Studio 2017 versione 15.6 e versioni successive*

I pacchetti NuGet possono includere una firma digitale che offre protezione contro i contenuti manomessi. Questa firma viene generata da un certificato X.509 che aggiunge inoltre prove autenticità per l'origine del pacchetto effettiva.

I pacchetti firmati forniscono la convalida end-to-end più attendibili. Esistono due diversi tipi di firme di NuGet:
- **Creare una firma**. Una firma di autore garantisce che il pacchetto non è stato modificato dopo l'autore firma il pacchetto, non importa da quale metodo viene recapitato il pacchetto del trasporto repository o un'azione. Inoltre, pacchetti firmati dall'autore forniscono un meccanismo di autenticazione extra per la pipeline di pubblicazione di nuget.org perché il certificato di firma deve essere registrato anticipatamente. Per altre informazioni, vedere [registrare i certificati](#register-certificate-on-nugetorg).
- **Firma repository**. Le firme di repository forniscono una garanzia di integrità per **tutti** in un repository di pacchetti che siano autore firmato o No, anche se tali pacchetti sono ottenuti da una posizione diversa nel repository originale dove si trovavano eseguito l'accesso.   

Per informazioni dettagliate sulla creazione di un pacchetto firmato autore, vedere [firma dei pacchetti](../create-packages/Sign-a-package.md) e il [comando nuget sign](../tools/cli-ref-sign.md).

> [!Important]
> La firma del pacchetto è attualmente supportata solo quando si usa nuget.exe in Windows. Verifica dei pacchetti firmati è attualmente supportata solo quando si usa nuget.exe o Visual Studio in Windows.

## <a name="certificate-requirements"></a>Requisiti del certificato

Firmare il pacchetto richiede un codice di firma del certificato, ovvero un tipo speciale di certificato valido per il `id-kp-codeSigning` scopo [[RFC 5280 sezione 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Inoltre, il certificato deve avere una pubblica lunghezza della chiave RSA di 2.048 bit o superiore.

## <a name="get-a-code-signing-certificate"></a>Ottenere un certificato di firma codice

I certificati validi possono essere ottenuti da un'autorità di certificazione pubblica, ad esempio:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Accesso globale](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

L'elenco completo delle autorità di certificazione attendibile per Windows può essere ottenuto da [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Creare un certificato di test

È possibile usare i certificati autocertificati a scopo di test. Per creare un certificato autocertificato, usare il [comandi di PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate.md).

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

I pacchetti firmati devono includere un timestamp RFC 3161 per assicurare la validità della firma oltre il periodo di validità del certificato di firma del pacchetto. Il certificato usato per firmare il timestamp deve essere valido per il `id-kp-timeStamping` scopo [[RFC 5280 sezione 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Inoltre, il certificato deve avere una pubblica lunghezza della chiave RSA di 2.048 bit o superiore.

Altri dettagli tecnici sono reperibili nel [conoscere le specifiche tecniche di firma del pacchetto](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Requisiti di firma in nuget.org

NuGet.org prevede requisiti aggiuntivi per l'accettazione di un pacchetto firmato:

- La firma primaria deve essere una firma di autore.
- La firma primaria deve avere un solo timestamp valido.
- I certificati X.509 per la firma dell'autore e la firma del timestamp:
  - Deve avere una chiave pubblica RSA 2048 bit o superiore.
  - Deve essere entro il relativo periodo di validità per ogni ora UTC corrente in fase di convalida del pacchetto in nuget.org.
  - Deve essere concatenato a un'autorità radice attendibile è considerato attendibile per impostazione predefinita in Windows. I pacchetti firmati con i certificati autocertificati vengono rifiutati.
  - Deve essere valido per il suo scopo: 
    - L'autore del certificato di firma deve essere valido per la firma del codice.
    - Il certificato di timestamp deve essere valido per l'aggiunta di timestamp.
  - Non deve essere revocato al momento della firma. (Ciò potrebbe non essere conosciuto al momento dell'invio, in modo da nuget.org a controlli periodicamente lo stato di revoca).

## <a name="register-certificate-on-nugetorg"></a>Registrare il certificato in nuget.org

Per inviare un pacchetto firmato, è innanzitutto necessario registrare il certificato con nuget.org. È necessario il certificato come una `.cer` file in un formato DER binario. È possibile esportare un certificato esistente in un formato DER binario usando l'esportazione guidata certificati.

![Esportazione guidata certificati](media/CertificateExportWizard.png)

Gli utenti avanzati possono esportare il certificato usando il [comando Export-Certificate PowerShell](/powershell/module/pkiclient/export-certificate.md).

Per registrare il certificato con nuget.org, passare a `Certificates` nella sezione `Account settings` pagina (o pagina di impostazioni dell'organizzazione) e selezionare `Register new certificate`.

![Certificati registrati](media/registered-certs.png)

> [!Tip]
> Un utente può inviare che più certificati e lo stesso certificato può essere registrati da più utenti.

Una volta che un utente dispone di un certificato registrato, tutti gli invii di pacchetto futuri **necessario** siano firmate con uno dei certificati.

Gli utenti possono inoltre rimuovere un certificato registrato dall'account. Dopo la rimozione di un certificato, i pacchetti firmati con tale certificato non riuscire in invio. I pacchetti esistenti non sono interessati.

## <a name="configure-package-signing-requirements"></a>Configurare i requisiti di firma del pacchetto

Se sei l'unico proprietario di un pacchetto, si è il firmatario richiesto. Vale a dire, è possibile utilizzare uno dei certificati registrati per firmare i pacchetti e inviare in nuget.org.

Se un pacchetto include più proprietari, per impostazione predefinita, i certificati del proprietario della "Any" possono essere usati per firmare il pacchetto. Come co-proprietario del pacchetto, è possibile eseguire l'override "Any" con se stessi o altri Comproprietario sia il firmatario richiesto. Se si apporta un proprietario non ha alcun certificato registrato, quindi i pacchetti non firmati potrà essere. 

Analogamente, se il valore predefinito "Any" opzione è selezionata per un pacchetto in cui un solo proprietario dispone di un certificato registrato e un altro proprietario non ha alcun certificato registrato, quindi nuget.org accetta entrambi un pacchetto firmato con una firma registrata da uno dei proprietari o unsigned (perché uno dei proprietari non è disponibile alcun certificato registrato) del pacchetto.

![Configurare i firmatari pacchetto](media/configure-package-signers.png)
