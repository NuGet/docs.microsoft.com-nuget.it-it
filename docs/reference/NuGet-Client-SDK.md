---
title: SDK client NuGet
description: L'API è in continua evoluzione e non è ancora documentata, ma gli esempi sono disponibili nel Blog di Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: a5c542379318f24ee35ccf25651d0e8de91253ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231240"
---
# <a name="nuget-client-sdk"></a>SDK client NuGet

*NuGet client SDK* si riferisce a un gruppo di pacchetti NuGet:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) : usato per interagire con i feed NuGet http e basati su file
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) : usato per interagire con i pacchetti NuGet. `NuGet.Protocol` dipende da questo pacchetto

È possibile trovare il codice sorgente per questi pacchetti nel repository GitHub [NuGet/NuGet. client](https://github.com/NuGet/NuGet.Client) .

> [!Note]
> Per la documentazione sul protocollo server NuGet, vedere l'API del [Server NuGet](~/api/overview.md).

## <a name="getting-started"></a>Introduzione

### <a name="install-the-package"></a>Installare il pacchetto

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a>Esempi

È possibile trovare questi esempi nel progetto [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) su GitHub.

### <a name="list-package-versions"></a>Elencare le versioni del pacchetto

Trovare tutte le versioni di Newtonsoft. JSON usando l' [API del contenuto del pacchetto NuGet V3](../api/package-base-address-resource.md#enumerate-package-versions):

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Scarica un pacchetto

Scaricare Newtonsoft. JSON v 12.0.1 usando l' [API del contenuto del pacchetto NuGet V3](../api/package-base-address-resource.md):

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Ottenere i metadati del pacchetto

Ottenere i metadati per il pacchetto "Newtonsoft. JSON" usando l' [API dei metadati del pacchetto NuGet V3](../api/registration-base-url-resource.md):

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Ricerche nei pacchetti

Cercare i pacchetti "JSON" usando l' [API di ricerca NuGet V3](../api/search-query-service-resource.md):

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a>Documentazione di terze parti

È possibile trovare esempi e documentazione per alcune API nella serie di Blog di Dave Glick, pubblicata 2016:

- [Esplorazione delle librerie NuGet V3, parte 1: introduzione e concetti](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Esplorazione delle librerie NuGet V3, parte 2: ricerca di pacchetti](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Esplorazione delle librerie NuGet V3, parte 3: installazione dei pacchetti](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Questi post di Blog sono stati scritti poco dopo il rilascio della versione **3.4.3** dei pacchetti SDK del client NuGet.
> Le versioni più recenti dei pacchetti potrebbero non essere compatibili con le informazioni contenute nei post di Blog.

Martin Björkström ha pubblicato un post di Blog per la serie di Blog di Dave Glick, in cui introduce un approccio diverso per l'uso di NuGet client SDK per installare i pacchetti NuGet:

- [Rivisitando le librerie NuGet V3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
