---
title: Pacchetti firmati
description: Requisiti per la firma dei pacchetti NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 7384e8b30cb2ec5fe53ea0fe485858bc1f7b3c43
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428681"
---
# <a name="signed-packages"></a>Pacchetti firmati

*NuGet 4.6.0 + e Visual Studio 2017 versione 15,6 e successive*

I pacchetti NuGet possono includere una firma digitale che fornisce la protezione contro il contenuto manomesso. Questa firma viene prodotta da un certificato X. 509 che aggiunge anche prove di autenticità all'origine effettiva del pacchetto.

I pacchetti firmati forniscono la convalida end-to-end più avanzata. Esistono due tipi diversi di firme NuGet:
- **Firma dell'autore**. Una firma di autore garantisce che il pacchetto non sia stato modificato dopo che l'autore ha firmato il pacchetto, indipendentemente dal repository o dal metodo di trasporto fornito dal pacchetto. Inoltre, i pacchetti firmati dall'autore forniscono un meccanismo di autenticazione aggiuntivo alla pipeline di pubblicazione nuget.org, perché il certificato di firma deve essere registrato in anticipo. Per ulteriori informazioni, vedere [Register Certificates](#signature-requirements-on-nugetorg).
- **Firma del repository**. Le firme del repository forniscono una garanzia di integrità per **tutti i** pacchetti in un repository, indipendentemente dal fatto che siano firmati o meno dall'autore, anche se i pacchetti vengono ottenuti da un percorso diverso rispetto al repository originale in cui sono stati firmati.   

Per informazioni dettagliate sulla creazione di un pacchetto firmato autore, vedere [signing Packages](../create-packages/Sign-a-package.md) e il [comando NuGet Sign](../reference/cli-reference/cli-ref-sign.md).

> [!Important]
> La firma del pacchetto è attualmente supportata solo quando si usa NuGet. exe in Windows. [La verifica dei pacchetti firmati è attualmente supportata solo quando si usa NuGet. exe](../reference/cli-reference/cli-ref-verify.md) o Visual Studio in Windows.

## <a name="certificate-requirements"></a>Requisiti per i certificati

Per la firma del pacchetto è necessario un certificato di firma del codice, che è un tipo speciale di certificato valido per lo scopo `id-kp-codeSigning` [[RFC 5280 Section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Inoltre, il certificato deve avere una lunghezza di chiave pubblica RSA di 2048 bit o superiore.

## <a name="timestamp-requirements"></a>Requisiti timestamp

I pacchetti firmati devono includere un timestamp RFC 3161 per garantire la validità della firma oltre il periodo di validità del certificato di firma del pacchetto. Il certificato utilizzato per firmare il timestamp deve essere valido per lo scopo `id-kp-timeStamping` [[RFC 5280 Section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Inoltre, il certificato deve avere una lunghezza di chiave pubblica RSA di 2048 bit o superiore.

Ulteriori dettagli tecnici sono disponibili nelle [specifiche tecniche di firma del pacchetto](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Requisiti di firma su NuGet.org

nuget.org dispone di requisiti aggiuntivi per l'accettazione di un pacchetto firmato:

- La firma primaria deve essere una firma dell'autore.
- La firma primaria deve avere un singolo timestamp valido.
- I certificati X. 509 per la firma dell'autore e la relativa firma timestamp:
  - Deve avere una chiave pubblica RSA 2048 bit o superiore.
  - Deve essere entro il periodo di validità per l'ora UTC corrente al momento della convalida del pacchetto in nuget.org.
  - Deve essere concatenato a un'autorità radice attendibile considerata attendibile per impostazione predefinita in Windows. I pacchetti firmati con certificati autofirmati vengono rifiutati.
  - Deve essere valido per lo scopo: 
    - Il certificato di firma dell'autore deve essere valido per la firma del codice.
    - Il certificato timestamp deve essere valido per il timestamp.
  - Non deve essere revocato al momento della firma. Questo potrebbe non essere noto al momento dell'invio, quindi nuget.org verifica periodicamente lo stato di revoca.
  
  
## <a name="related-articles"></a>Articoli correlati

- [Firma di pacchetti NuGet](../create-packages/Sign-a-Package.md)
- [Gestire i limiti di attendibilità dei pacchetti](../consume-packages/installing-signed-packages.md)
