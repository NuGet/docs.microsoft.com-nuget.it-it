---
title: NuGet Client SDK
description: L'API è in continua evoluzione e non ancora documentato, ma gli esempi sono disponibili nel blog di Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 97ed3ec7d41d2847c0521af69373a1871eb585dd
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324682"
---
# <a name="nuget-client-sdk"></a>NuGet Client SDK

> [!Note]
> Non deve essere confusa con la [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)

Il *NuGet Client SDK* fa riferimento a un gruppo di librerie .NET incentrati [NuGet](https://www.nuget.org/packages/NuGet.Client), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), e [NuGet. Protocol](https://www.nuget.org/packages/NuGet.Protocol). Questi pacchetti sostituiscono la precedente [togliere](https://www.nuget.org/packages/NuGet.Core/) libreria.

Microsoft sta lavorando con una superficie di attacco stabile che è possibile documentare a breve.

## <a name="source-code"></a>Codice sorgente

Il codice sorgente viene pubblicato in GitHub nel progetto [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).

## <a name="third-party-documentation"></a>Documentazione di terze parti

È possibile trovare esempi e documentazione per alcune delle API della serie di blog seguente da Dave Glick, pubblicato 2016:

- [Esplorare le librerie di NuGet v3, parte 1: Introduzione e concetti](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Esplorare le librerie di NuGet v3, parte 2: La ricerca di pacchetti](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Esplorare le librerie di NuGet v3, parte 3: L'installazione dei pacchetti](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Questi post di blog scritti subito dopo il **3.4.3** versione di NuGet sono stati rilasciati pacchetti SDK client.
> Le versioni più recenti dei pacchetti possono essere incompatibili con le informazioni contenute nei post di blog.

Martin Björkström ha un post di blog di follow-up per serie di blog di Dave Glick dove presenta un approccio diverso usando il SDK del Client NuGet per l'installazione di pacchetti NuGet:

- [Rivedere le librerie di NuGet v3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
