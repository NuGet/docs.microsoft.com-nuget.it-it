---
title: Pacchetti firmati
description: Requisiti per la firma dei pacchetti NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 85fdf7a41cc033d92bbd0326648142aec27a9970
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508800"
---
# <a name="signed-packages"></a>Pacchetti firmati

*NuGet 4.6.0+ e Visual Studio 2017 versione 15.6 e successive*

I pacchetti NuGet possono includere una firma digitale che fornisce protezione dal contenuto manomesso. Questa firma viene prodotta da un certificato X.509 che aggiunge anche le prove di autenticità all'origine effettiva del pacchetto.

I pacchetti firmati offrono la convalida end-to-end più solida. Esistono due tipi diversi di firme NuGet:
- **Firma dell'autore**. Una firma dell'autore garantisce che il pacchetto non sia stato modificato dopo che l'autore ha firmato il pacchetto, indipendentemente dal repository o dal metodo di trasporto recapitato. Inoltre, i pacchetti firmati dall'autore forniscono un meccanismo di autenticazione aggiuntivo per la pipeline di pubblicazione nuget.org perché il certificato di firma deve essere registrato in anticipo. Per altre informazioni, vedere [Registrare i certificati](#signature-requirements-on-nugetorg).
- **Firma del repository**. Le firme del repository  offrono una garanzia di integrità per tutti i pacchetti in un repository, indipendentemente dal fatto che siano firmati o meno dall'autore, anche se tali pacchetti vengono ottenuti da un percorso diverso rispetto al repository originale in cui sono stati firmati.   

Per informazioni dettagliate sulla creazione di un pacchetto firmato dall'autore, vedere [Firma di](../create-packages/Sign-a-package.md) pacchetti e il [comando nuget sign](../reference/cli-reference/cli-ref-sign.md). È possibile verificare le firme dei pacchetti usando i comandi [dotnet nuget verify](/dotnet/core/tools/dotnet-nuget-verify) o [nuget verify.](../reference/cli-reference/cli-ref-verify.md)

> [!Important]
> I pacchetti di firma di creazione sono supportati nuget.exe in Windows al momento. Tuttavia, tutti i pacchetti caricati in nuget.org vengono firmati automaticamente dal repository.

## <a name="certificate-requirements"></a>Requisiti per i certificati

La firma del pacchetto richiede un certificato di firma del codice, che è un tipo speciale di certificato valido per lo scopo `id-kp-codeSigning` [[RFC 5280 sezione 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Inoltre, il certificato deve avere una lunghezza di chiave pubblica RSA di 2048 bit o superiore.

## <a name="timestamp-requirements"></a>Requisiti del timestamp

I pacchetti firmati devono includere un timestamp RFC 3161 per garantire la validità della firma oltre il periodo di validità del certificato di firma del pacchetto. Il certificato usato per firmare il timestamp deve essere valido per `id-kp-timeStamping` lo scopo [ RFC[5280 sezione 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Inoltre, il certificato deve avere una lunghezza di chiave pubblica RSA di 2048 bit o superiore.

Altri dettagli tecnici sono disponibili nelle specifiche tecniche per la [firma del pacchetto](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Requisiti di firma per NuGet.org

nuget.org requisiti aggiuntivi per l'accettazione di un pacchetto firmato:

- La firma primaria deve essere una firma dell'autore.
- La firma primaria deve avere un singolo timestamp valido.
- Certificati X.509 sia per la firma dell'autore che per la firma timestamp:
  - Deve avere una chiave pubblica RSA a 2048 bit o superiore.
  - Deve essere compreso nel periodo di validità per ogni ora UTC corrente al momento della convalida del pacchetto nuget.org.
  - Deve essere concatenato a un'autorità radice attendibile attendibile per impostazione predefinita in Windows. I pacchetti firmati con certificati autoemessi vengono rifiutati.
  - Deve essere valido per lo scopo: 
    - Il certificato di firma dell'autore deve essere valido per la firma del codice.
    - Il certificato timestamp deve essere valido per il timestamp.
  - Non deve essere revocato in fase di firma. Questo potrebbe non essere possibile al momento dell'invio, quindi nuget.org periodicamente controlla lo stato di revoca.
  
  
## <a name="related-articles"></a>Articoli correlati

- [Firma di pacchetti NuGet](../create-packages/Sign-a-Package.md)
- [Verificare i pacchetti firmati usando l'interfaccia della riga di comando dotnet](/dotnet/core/tools/dotnet-nuget-verify)
- [Verificare i pacchetti firmati usando nuget.exe](../reference/cli-reference/cli-ref-verify.md)
- [Gestire i limiti di attendibilità dei pacchetti](../consume-packages/installing-signed-packages.md)
