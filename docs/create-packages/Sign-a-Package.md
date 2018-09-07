---
title: Firma di pacchetti NuGet
description: Informazioni su come è possibile usare pacchetti firmati per abilitare la verifica dell'integrità del contenuto.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: c598461831323ecfcc5da3877df71bd8d69557f6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551978"
---
# <a name="signing-nuget-packages"></a>Firma di pacchetti NuGet

La firma di un pacchetto è un processo per assicurarsi che il pacchetto non sia stato modificato dopo la creazione.

## <a name="prerequisites"></a>Prerequisiti

1. Il pacchetto (file `.nupkg`) da firmare. Vedere [Creazione di un pacchetto](creating-a-package.md).

1. nuget.exe 4.6.0 o versione successiva. Vedere come [installare l'interfaccia della riga di comando di nuget.exe](../install-nuget-client-tools.md#nugetexe-cli).

1. [Un certificato di firma del codice](../reference/signed-packages-reference.md#get-a-code-signing-certificate).

## <a name="sign-a-package"></a>Firmare un pacchetto

Per firmare un pacchetto, usare [nuget sign](../tools/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

Come descritto nelle informazioni di riferimento sui comandi, è possibile usare un certificato disponibile nell'archivio certificati o usare un certificato da un file.

### <a name="common-problems-when-signing-a-package"></a>Problemi comuni durante la firma di un pacchetto

- Il certificato non è valido per la firma del codice. È necessario assicurarsi che il certificato specificato abbia l'utilizzo chiavi avanzato appropriato (EKU 1.3.6.1.5.5.7.3.3).
- Il certificato non soddisfa i requisiti di base, ad esempio l'algoritmo di firma RSA SHA-256 o una chiave pubblica a 2048 bit o superiore.
- Il certificato è scaduto o è stato revocato.
- Il server di timestamp non soddisfa i requisiti del certificato.

> [!Note]
> I pacchetti firmati devono includere un timestamp per assicurarsi che la firma rimanga valida dopo la scadenza del certificato di firma. L'operazione di firma genera un [avviso NU3002](../reference/errors-and-warnings/NU3002.md) se avviene senza un timestamp.

## <a name="verify-a-signed-package"></a>Verificare un pacchetto firmato

Usare [nuget verify](../tools/cli-ref-verify.md) per visualizzare i dettagli di firma di un determinato pacchetto:

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a>Installare un pacchetto firmato

Non sono richieste azioni specifiche per l'installazione di pacchetti firmati. Tuttavia, se il contenuto è stato modificato dopo la firma, l'installazione viene bloccata e genera un [errore NU3008](../reference/errors-and-warnings/NU3008.md).

> [!Warning]
> I pacchetti firmati con certificati non attendibili vengono considerati non firmati e installati senza eventuali avvisi o errori come qualsiasi altro pacchetto non firmato.

## <a name="see-also"></a>Vedere anche

[Informazioni di riferimento sui pacchetti firmati](../reference/Signed-Packages-Reference.md)
