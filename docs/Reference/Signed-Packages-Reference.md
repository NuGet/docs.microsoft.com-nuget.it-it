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
# <a name="signed-packages"></a>Pacchetti firmati

*NuGet 4.6.0+ e Visual Studio 2017 15,6 e versioni successive*

Pacchetti NuGet possono includere una firma digitale che fornisce la protezione del contenuto manomessa. Questa firma viene generata da un certificato x. 509 che aggiunge anche modelli di prova di autenticità per l'origine del pacchetto effettiva.

Pacchetti firmati forniscono la convalida end-to-end più attendibili. Una firma di autore garantisce che il pacchetto non è stato modificato dopo l'autore la firma del pacchetto, indipendentemente da quale metodo viene recapitato il pacchetto del trasporto repository o cosa.

I consumer che necessitano di un ambiente bloccato possono richiedere pacchetti firmati con un certificato specifico dell'autore.

Inoltre, pacchetti firmati autore forniscono un meccanismo di autenticazione extra per la pipeline di pubblicazione nuget.org poiché il certificato di firma deve essere registrato anticipatamente.

Per informazioni dettagliate sulla creazione di un pacchetto firmato, vedere [firma pacchetti](../create-packages/Sign-a-package.md) e [comando sign nuget](../tools/cli-ref-sign.md).

> [!Important]
> NuGet.org non accetta attualmente dei pacchetti firmati. È possibile firmare pacchetti per la pubblicazione nel feed personalizzati.

## <a name="certificate-requirements"></a>Requisiti del certificato

Firmare il pacchetto richiede un certificato, che è un tipo speciale di certificato valido per la firma del codice di `id-kp-codeSigning` scopo [[RFC 5280 sezione 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Inoltre, il certificato deve avere una pubblica lunghezza della chiave RSA 2048 bit o superiore.

## <a name="get-a-code-signing-certificate"></a>Ottenere un certificato di firma codice

I certificati validi possono essere ottenuti da autorità di certificazione pubblica come:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Accesso globale](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

L'elenco completo delle autorità di certificazione attendibile per Windows può essere ottenuto da [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Creare un certificato di prova

È possibile utilizzare i certificati autocertificati a scopo di test. Per creare un'autocertificazione, utilizzare il [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) comando di PowerShell.

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

## <a name="timestamp-requirements"></a>Requisiti di timestamp

Pacchetti firmati devono includere un timestamp RFC 3161 per garantire la validità della firma oltre il periodo di validità del certificato di firma dei pacchetti. Il certificato utilizzato per firmare il timestamp deve essere valido per il `id-kp-timeStamping` scopo [[RFC 5280 sezione 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Inoltre, il certificato deve avere una pubblica lunghezza della chiave RSA 2048 bit o superiore.

Altri dettagli tecnici, vedere il [specifiche tecniche di firma del pacchetto](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).
