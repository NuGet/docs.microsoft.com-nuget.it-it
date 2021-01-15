---
title: Pacchetti firmati
description: Requisiti per la firma dei pacchetti NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: ac9efadc1d29bec86ca9b7821d5587e0171613aa
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235711"
---
# <a name="signed-packages"></a>Pacchetti firmati

*NuGet 4.6.0 + e Visual Studio 2017 versione 15,6 e successive*

I pacchetti NuGet possono includere una firma digitale che fornisce la protezione contro il contenuto manomesso. Questa firma viene prodotta da un certificato X. 509 che aggiunge anche prove di autenticità all'origine effettiva del pacchetto.

I pacchetti firmati forniscono la convalida end-to-end più avanzata. Esistono due tipi diversi di firme NuGet:
- **Firma dell'autore**. Una firma di autore garantisce che il pacchetto non sia stato modificato dopo che l'autore ha firmato il pacchetto, indipendentemente dal repository o dal metodo di trasporto fornito dal pacchetto. Inoltre, i pacchetti firmati dall'autore forniscono un meccanismo di autenticazione aggiuntivo alla pipeline di pubblicazione nuget.org, perché il certificato di firma deve essere registrato in anticipo. Per ulteriori informazioni, vedere [Register Certificates](#signature-requirements-on-nugetorg).
- **Firma del repository**. Le firme del repository forniscono una garanzia di integrità per **tutti i** pacchetti in un repository, indipendentemente dal fatto che siano firmati o meno dall'autore, anche se i pacchetti vengono ottenuti da un percorso diverso rispetto al repository originale in cui sono stati firmati.   

Per informazioni dettagliate sulla creazione di un pacchetto firmato autore, vedere [signing Packages](../create-packages/Sign-a-package.md) e il [comando NuGet Sign](../reference/cli-reference/cli-ref-sign.md). È possibile verificare le firme dei pacchetti usando i comandi [DotNet NuGet Verify](/dotnet/core/tools/dotnet-nuget-verify.md) o [NuGet Verify](../reference/cli-reference/cli-ref-verify.md) .

> [!Important]
> I pacchetti per la firma di autore sono supportati solo da nuget.exe in Windows al momento. Tuttavia, tutti i pacchetti caricati in nuget.org vengono automaticamente firmati.

## <a name="certificate-requirements"></a>Requisiti per i certificati

Per la firma del pacchetto è necessario un certificato di firma del codice, che è un tipo speciale di certificato valido per lo `id-kp-codeSigning` scopo [[RFC 5280 Section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Inoltre, il certificato deve avere una lunghezza di chiave pubblica RSA di 2048 bit o superiore.

## <a name="timestamp-requirements"></a>Requisiti timestamp

I pacchetti firmati devono includere un timestamp RFC 3161 per garantire la validità della firma oltre il periodo di validità del certificato di firma del pacchetto. Il certificato utilizzato per firmare il timestamp deve essere valido per lo `id-kp-timeStamping` scopo [[RFC 5280 Section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Inoltre, il certificato deve avere una lunghezza di chiave pubblica RSA di 2048 bit o superiore.

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
- [Verificare pacchetti firmati tramite l'interfaccia della riga di comando DotNet](/dotnet/core/tools/dotnet-nuget-verify.md)
- [Verificare i pacchetti firmati tramite nuget.exe](../reference/cli-reference/cli-ref-verify.md)
- [Gestire i limiti di attendibilità dei pacchetti](../consume-packages/installing-signed-packages.md)
