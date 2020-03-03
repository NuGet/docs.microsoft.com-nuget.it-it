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
# <a name="nuget-client-sdk"></a><span data-ttu-id="4e188-103">SDK client NuGet</span><span class="sxs-lookup"><span data-stu-id="4e188-103">NuGet Client SDK</span></span>

<span data-ttu-id="4e188-104">*NuGet client SDK* si riferisce a un gruppo di pacchetti NuGet:</span><span class="sxs-lookup"><span data-stu-id="4e188-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="4e188-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) : usato per interagire con i feed NuGet http e basati su file</span><span class="sxs-lookup"><span data-stu-id="4e188-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="4e188-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) : usato per interagire con i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="4e188-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="4e188-107">`NuGet.Protocol` dipende da questo pacchetto</span><span class="sxs-lookup"><span data-stu-id="4e188-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="4e188-108">È possibile trovare il codice sorgente per questi pacchetti nel repository GitHub [NuGet/NuGet. client](https://github.com/NuGet/NuGet.Client) .</span><span class="sxs-lookup"><span data-stu-id="4e188-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="4e188-109">Per la documentazione sul protocollo server NuGet, vedere l'API del [Server NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="4e188-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="4e188-110">Introduzione</span><span class="sxs-lookup"><span data-stu-id="4e188-110">Getting started</span></span>

### <a name="install-the-package"></a><span data-ttu-id="4e188-111">Installare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="4e188-111">Install the package</span></span>

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a><span data-ttu-id="4e188-112">Esempi</span><span class="sxs-lookup"><span data-stu-id="4e188-112">Examples</span></span>

<span data-ttu-id="4e188-113">È possibile trovare questi esempi nel progetto [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="4e188-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="4e188-114">Elencare le versioni del pacchetto</span><span class="sxs-lookup"><span data-stu-id="4e188-114">List package versions</span></span>

<span data-ttu-id="4e188-115">Trovare tutte le versioni di Newtonsoft. JSON usando l' [API del contenuto del pacchetto NuGet V3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="4e188-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="4e188-116">Scarica un pacchetto</span><span class="sxs-lookup"><span data-stu-id="4e188-116">Download a package</span></span>

<span data-ttu-id="4e188-117">Scaricare Newtonsoft. JSON v 12.0.1 usando l' [API del contenuto del pacchetto NuGet V3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="4e188-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="4e188-118">Ottenere i metadati del pacchetto</span><span class="sxs-lookup"><span data-stu-id="4e188-118">Get package metadata</span></span>

<span data-ttu-id="4e188-119">Ottenere i metadati per il pacchetto "Newtonsoft. JSON" usando l' [API dei metadati del pacchetto NuGet V3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="4e188-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="4e188-120">Ricerche nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="4e188-120">Search packages</span></span>

<span data-ttu-id="4e188-121">Cercare i pacchetti "JSON" usando l' [API di ricerca NuGet V3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="4e188-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a><span data-ttu-id="4e188-122">Documentazione di terze parti</span><span class="sxs-lookup"><span data-stu-id="4e188-122">Third-party documentation</span></span>

<span data-ttu-id="4e188-123">È possibile trovare esempi e documentazione per alcune API nella serie di Blog di Dave Glick, pubblicata 2016:</span><span class="sxs-lookup"><span data-stu-id="4e188-123">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="4e188-124">Esplorazione delle librerie NuGet V3, parte 1: introduzione e concetti</span><span class="sxs-lookup"><span data-stu-id="4e188-124">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="4e188-125">Esplorazione delle librerie NuGet V3, parte 2: ricerca di pacchetti</span><span class="sxs-lookup"><span data-stu-id="4e188-125">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="4e188-126">Esplorazione delle librerie NuGet V3, parte 3: installazione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="4e188-126">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="4e188-127">Questi post di Blog sono stati scritti poco dopo il rilascio della versione **3.4.3** dei pacchetti SDK del client NuGet.</span><span class="sxs-lookup"><span data-stu-id="4e188-127">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="4e188-128">Le versioni più recenti dei pacchetti potrebbero non essere compatibili con le informazioni contenute nei post di Blog.</span><span class="sxs-lookup"><span data-stu-id="4e188-128">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="4e188-129">Martin Björkström ha pubblicato un post di Blog per la serie di Blog di Dave Glick, in cui introduce un approccio diverso per l'uso di NuGet client SDK per installare i pacchetti NuGet:</span><span class="sxs-lookup"><span data-stu-id="4e188-129">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="4e188-130">Rivisitando le librerie NuGet V3</span><span class="sxs-lookup"><span data-stu-id="4e188-130">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
