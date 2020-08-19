---
title: NuGet Client SDK
description: L'API è in continua evoluzione e non è ancora documentata, ma gli esempi sono disponibili nel Blog di Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 39a4de4071eec70c88a2add158f2a3a734f7d7b7
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622928"
---
# <a name="nuget-client-sdk"></a>NuGet Client SDK

*NuGet client SDK* si riferisce a un gruppo di pacchetti NuGet:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -Usato per interagire con i feed NuGet HTTP e basati su file
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) : Usato per interagire con i pacchetti NuGet. `NuGet.Protocol` dipende da questo pacchetto

È possibile trovare il codice sorgente per questi pacchetti nel repository GitHub [NuGet/NuGet. client](https://github.com/NuGet/NuGet.Client) .

> [!Note]
> Per la documentazione sul protocollo server NuGet, vedere l'API del [Server NuGet](~/api/overview.md).

## <a name="getting-started"></a>Introduzione

### <a name="install-the-packages"></a>Installare i pacchetti

```ps1
dotnet add package NuGet.Protocol  # interact with HTTP and folder-based NuGet package feeds, includes NuGet.Packaging

dotnet add package NuGet.Packaging # interact with .nupkg and .nuspec files from a stream
```

## <a name="examples"></a>Esempi

È possibile trovare questi esempi nel progetto [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) su GitHub.

### <a name="list-package-versions"></a>Elencare le versioni del pacchetto

Trovare tutte le versioni di Newtonsoft.Jsusando l' [API del contenuto del pacchetto NuGet V3](../api/package-base-address-resource.md#enumerate-package-versions):

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Scarica un pacchetto

Scaricare Newtonsoft.Jsin v 12.0.1 usando l' [API del contenuto del pacchetto NuGet V3](../api/package-base-address-resource.md):

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Ottenere i metadati del pacchetto

Ottenere i metadati per il pacchetto "Newtonsoft.Json" usando l' [API dei metadati del pacchetto NuGet V3](../api/registration-base-url-resource.md):

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Ricerche nei pacchetti

Cercare i pacchetti "JSON" usando l' [API di ricerca NuGet V3](../api/search-query-service-resource.md):

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="create-a-package"></a>Creare un pacchetto

Creare un pacchetto, impostare i metadati e aggiungere le dipendenze usando [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

> [!IMPORTANT]
> Si consiglia vivamente di creare pacchetti NuGet usando gli strumenti di NuGet ufficiali e **senza** usare questa API di basso livello. Esistono diverse caratteristiche importanti per un pacchetto ben formato e la versione più recente degli strumenti consente di incorporare queste procedure consigliate.
> 
> Per altre informazioni sulla creazione di pacchetti NuGet, vedere la panoramica del [flusso di lavoro di creazione dei pacchetti](../create-packages/overview-and-workflow.md) e la documentazione per gli strumenti di Pack ufficiali, ad esempio [usando l'interfaccia della](../create-packages/creating-a-package-dotnet-cli.md)riga di comando di DotNet.

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a>Leggi un pacchetto

Leggere un pacchetto da un flusso di file usando [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

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
