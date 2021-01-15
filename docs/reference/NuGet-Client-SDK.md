---
title: NuGet Client SDK
description: L'API è in continua evoluzione e non è ancora documentata, ma gli esempi sono disponibili nel Blog di Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 0eca8478b4d6509dbc1407560d2c86069c7575dd
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235737"
---
# <a name="nuget-client-sdk"></a>NuGet Client SDK

*NuGet client SDK* si riferisce a un gruppo di pacchetti NuGet:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -Usato per interagire con i feed NuGet HTTP e basati su file
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) : Usato per interagire con i pacchetti NuGet. `NuGet.Protocol` dipende da questo pacchetto

È possibile trovare il codice sorgente per questi pacchetti nel repository GitHub [NuGet/NuGet. client](https://github.com/NuGet/NuGet.Client) .
È possibile trovare il codice sorgente per questi esempi nel progetto [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) su GitHub.

> [!Note]
> Per la documentazione sul protocollo server NuGet, vedere l'API del [Server NuGet](~/api/overview.md).

## <a name="nugetprotocol"></a>NuGet. Protocol

Installare il `NuGet.Protocol` pacchetto per interagire con i feed di pacchetti NuGet basati su cartelle e http:

```ps1
dotnet add package NuGet.Protocol
```

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

### <a name="push-a-package"></a>Eseguire il push di un pacchetto

Eseguire il push di un pacchetto usando l' [API di push ed eliminazione NuGet V3](../api/package-publish-resource.md):

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a>Eliminare un pacchetto

Eliminare un pacchetto usando l' [API di push ed eliminazione NuGet V3](../api/package-publish-resource.md):

> [!Note]
> I server NuGet sono liberi di interpretare una richiesta di eliminazione del pacchetto come "eliminazione hardware", "eliminazione temporanea" o "Unlist".
> Nuget.org, ad esempio, interpreta la richiesta di eliminazione del pacchetto come "Unlist". Per ulteriori informazioni su questa procedura, vedere il criterio [eliminazione dei pacchetti](../nuget-org/policies/deleting-packages.md) .

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a>Usare i feed autenticati

Usare [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) per lavorare con i feed autenticati.

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a>NuGet. Packaging

Installare il `NuGet.Packaging` pacchetto per interagire con `.nupkg` `.nuspec` i file e da un flusso:

```ps1
dotnet add package NuGet.Packaging
```

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
