---
title: NuGet Client SDK
description: L'API è in evoluzione e non è ancora documentata, ma gli esempi sono disponibili nel blog di Dave Glick.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 6417c971dc13cf9ed05dcec4e4156af94c0ea058
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387387"
---
# <a name="nuget-client-sdk"></a>NuGet Client SDK

NuGet *Client SDK fa* riferimento a un gruppo di pacchetti NuGet:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Usato per interagire con HTTP e feed NuGet basati su file
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Usato per interagire con i pacchetti NuGet. `NuGet.Protocol` dipende da questo pacchetto

È possibile trovare il codice sorgente per questi pacchetti nel repository GitHub [NuGet/NuGet.Client.](https://github.com/NuGet/NuGet.Client)
È possibile trovare il codice sorgente per questi esempi nel [progetto NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) in GitHub.

> [!Note]
> Per la documentazione sul protocollo server NuGet, vedere [l'API del server NuGet](~/api/overview.md).

## <a name="nugetprotocol"></a>NuGet.Protocol

Installare il pacchetto per interagire con HTTP e feed di pacchetti `NuGet.Protocol` NuGet basati su cartelle:

```ps1
dotnet add package NuGet.Protocol
```

> [!Tip]
> `Repository.Factory` è definito nello spazio `NuGet.Protocol.Core.Types` dei nomi e il metodo è un metodo di estensione definito nello spazio dei nomi `GetCoreV3` `NuGet.Protocol` . Sarà quindi necessario aggiungere istruzioni `using` per entrambi gli spazi dei nomi.

### <a name="list-package-versions"></a>Elencare le versioni dei pacchetti

Trovare tutte le versioni di Newtonsoft.Jssull'uso [dell'API NuGet V3 Package Content:](../api/package-base-address-resource.md#enumerate-package-versions)

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Scaricare un pacchetto

Scaricare Newtonsoft.Jsversione 12.0.1 usando [l'API NuGet V3 Package Content:](../api/package-base-address-resource.md)

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Ottenere i metadati del pacchetto

Ottenere i metadati per il pacchetto "Newtonsoft.Js" usando l'API dei metadati del pacchetto [NuGet V3:](../api/registration-base-url-resource.md)

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Ricerche nei pacchetti

Cercare i pacchetti "json" usando [l'API di ricerca NuGet V3:](../api/search-query-service-resource.md)

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a>Eseguire il push di un pacchetto

Eseguire il push di un pacchetto [usando l'API NuGet V3 Push ed Delete:](../api/package-publish-resource.md)

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a>Eliminare un pacchetto

Eliminare un pacchetto usando [l'API NuGet V3 Push and Delete](../api/package-publish-resource.md):

> [!Note]
> I server NuGet sono liberi di interpretare una richiesta di eliminazione del pacchetto come "eliminazione hard", "eliminazione software" o "unlist".
> Ad esempio, nuget.org interpreta la richiesta di eliminazione del pacchetto come "unlist". Per altre informazioni su questa procedura, vedere il criterio [Eliminazione di](../nuget-org/policies/deleting-packages.md) pacchetti.

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a>Usare feed autenticati

Usare [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) per usare i feed autenticati.

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a>NuGet.Packaging

Installare il `NuGet.Packaging` pacchetto per interagire con i file e da un `.nupkg` `.nuspec` flusso:

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a>Creare un pacchetto

Creare un pacchetto, impostare i metadati e aggiungere dipendenze usando [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

> [!IMPORTANT]
> È consigliabile creare pacchetti NuGet usando gli strumenti NuGet ufficiali e non **usando** questa API di basso livello. Esistono diverse caratteristiche importanti per un pacchetto ben formato e la versione più recente degli strumenti consente di incorporare queste procedure consigliate.
> 
> Per altre informazioni sulla creazione di pacchetti [](../create-packages/overview-and-workflow.md) NuGet, vedere la panoramica del flusso di lavoro di creazione del pacchetto e la documentazione per gli strumenti ufficiali dei pacchetti ( ad esempio, tramite l'interfaccia della riga di [comando dotnet](../create-packages/creating-a-package-dotnet-cli.md)).

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a>Leggere un pacchetto

Leggere un pacchetto da un flusso di file usando [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a>Documentazione di terze parti

Esempi e documentazione per alcune API sono disponibili nella serie di blog seguente di Dave Glick, pubblicata nel 2016:

- [Esplorazione delle librerie NuGet v3, parte 1: Introduzione e concetti](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Esplorazione delle librerie NuGet v3, parte 2: Ricerca di pacchetti](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Esplorazione delle librerie NuGet v3, parte 3: Installazione di pacchetti](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Questi post di blog sono stati scritti poco dopo il rilascio della versione **3.4.3** dei pacchetti SDK del client NuGet.
> Le versioni più recenti dei pacchetti potrebbero non essere compatibili con le informazioni contenute nei post di blog.

Martin Björkström ha fatto un post di blog di follow-up alla serie di blog di Dave Glick in cui introduce un approccio diverso all'uso di NuGet Client SDK per installare i pacchetti NuGet:

- [Revisione delle librerie NuGet v3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
