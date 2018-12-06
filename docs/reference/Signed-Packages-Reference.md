---
title: Pacchetti firmati
description: Requisiti per la firma del pacchetto NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 486bf4032e156168f9b2fef57ccdae0c372b2eff
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977511"
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

## <a name="timestamp-requirements"></a>Requisiti di timestamp

I pacchetti firmati devono includere un timestamp RFC 3161 per assicurare la validità della firma oltre il periodo di validità del certificato di firma del pacchetto. Il certificato usato per firmare il timestamp deve essere valido per il `id-kp-timeStamping` scopo [[RFC 5280 sezione 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Inoltre, il certificato deve avere una pubblica lunghezza della chiave RSA di 2.048 bit o superiore.

Altri dettagli tecnici sono reperibili nel [conoscere le specifiche tecniche di firma del pacchetto](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Requisiti di firma in NuGet.org

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
  
  
## <a name="related-articles"></a>Articoli correlati

- [Firma dei pacchetti NuGet](../create-packages/Sign-a-Package.md)
- [Installazione di pacchetti firmati](../consume-packages/installing-signed-packages.md)
