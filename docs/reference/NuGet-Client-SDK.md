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
# <a name="nuget-client-sdk"></a><span data-ttu-id="f8e15-103">NuGet Client SDK</span><span class="sxs-lookup"><span data-stu-id="f8e15-103">NuGet Client SDK</span></span>

<span data-ttu-id="f8e15-104">*NuGet client SDK* si riferisce a un gruppo di pacchetti NuGet:</span><span class="sxs-lookup"><span data-stu-id="f8e15-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="f8e15-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -Usato per interagire con i feed NuGet HTTP e basati su file</span><span class="sxs-lookup"><span data-stu-id="f8e15-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="f8e15-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) : Usato per interagire con i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="f8e15-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="f8e15-107">`NuGet.Protocol` dipende da questo pacchetto</span><span class="sxs-lookup"><span data-stu-id="f8e15-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="f8e15-108">È possibile trovare il codice sorgente per questi pacchetti nel repository GitHub [NuGet/NuGet. client](https://github.com/NuGet/NuGet.Client) .</span><span class="sxs-lookup"><span data-stu-id="f8e15-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="f8e15-109">Per la documentazione sul protocollo server NuGet, vedere l'API del [Server NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="f8e15-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="f8e15-110">Introduzione</span><span class="sxs-lookup"><span data-stu-id="f8e15-110">Getting started</span></span>

### <a name="install-the-packages"></a><span data-ttu-id="f8e15-111">Installare i pacchetti</span><span class="sxs-lookup"><span data-stu-id="f8e15-111">Install the packages</span></span>

```ps1
dotnet add package NuGet.Protocol  # interact with HTTP and folder-based NuGet package feeds, includes NuGet.Packaging

dotnet add package NuGet.Packaging # interact with .nupkg and .nuspec files from a stream
```

## <a name="examples"></a><span data-ttu-id="f8e15-112">Esempi</span><span class="sxs-lookup"><span data-stu-id="f8e15-112">Examples</span></span>

<span data-ttu-id="f8e15-113">È possibile trovare questi esempi nel progetto [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="f8e15-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="f8e15-114">Elencare le versioni del pacchetto</span><span class="sxs-lookup"><span data-stu-id="f8e15-114">List package versions</span></span>

<span data-ttu-id="f8e15-115">Trovare tutte le versioni di Newtonsoft.Jsusando l' [API del contenuto del pacchetto NuGet V3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="f8e15-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="f8e15-116">Scarica un pacchetto</span><span class="sxs-lookup"><span data-stu-id="f8e15-116">Download a package</span></span>

<span data-ttu-id="f8e15-117">Scaricare Newtonsoft.Jsin v 12.0.1 usando l' [API del contenuto del pacchetto NuGet V3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="f8e15-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="f8e15-118">Ottenere i metadati del pacchetto</span><span class="sxs-lookup"><span data-stu-id="f8e15-118">Get package metadata</span></span>

<span data-ttu-id="f8e15-119">Ottenere i metadati per il pacchetto "Newtonsoft.Json" usando l' [API dei metadati del pacchetto NuGet V3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="f8e15-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="f8e15-120">Ricerche nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="f8e15-120">Search packages</span></span>

<span data-ttu-id="f8e15-121">Cercare i pacchetti "JSON" usando l' [API di ricerca NuGet V3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="f8e15-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="create-a-package"></a><span data-ttu-id="f8e15-122">Creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="f8e15-122">Create a package</span></span>

<span data-ttu-id="f8e15-123">Creare un pacchetto, impostare i metadati e aggiungere le dipendenze usando [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="f8e15-123">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8e15-124">Si consiglia vivamente di creare pacchetti NuGet usando gli strumenti di NuGet ufficiali e **senza** usare questa API di basso livello.</span><span class="sxs-lookup"><span data-stu-id="f8e15-124">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="f8e15-125">Esistono diverse caratteristiche importanti per un pacchetto ben formato e la versione più recente degli strumenti consente di incorporare queste procedure consigliate.</span><span class="sxs-lookup"><span data-stu-id="f8e15-125">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="f8e15-126">Per altre informazioni sulla creazione di pacchetti NuGet, vedere la panoramica del [flusso di lavoro di creazione dei pacchetti](../create-packages/overview-and-workflow.md) e la documentazione per gli strumenti di Pack ufficiali, ad esempio [usando l'interfaccia della](../create-packages/creating-a-package-dotnet-cli.md)riga di comando di DotNet.</span><span class="sxs-lookup"><span data-stu-id="f8e15-126">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="f8e15-127">Leggi un pacchetto</span><span class="sxs-lookup"><span data-stu-id="f8e15-127">Read a package</span></span>

<span data-ttu-id="f8e15-128">Leggere un pacchetto da un flusso di file usando [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="f8e15-128">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="f8e15-129">Documentazione di terze parti</span><span class="sxs-lookup"><span data-stu-id="f8e15-129">Third-party documentation</span></span>

<span data-ttu-id="f8e15-130">È possibile trovare esempi e documentazione per alcune API nella serie di Blog di Dave Glick, pubblicata 2016:</span><span class="sxs-lookup"><span data-stu-id="f8e15-130">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="f8e15-131">Esplorazione delle librerie NuGet V3, parte 1: introduzione e concetti</span><span class="sxs-lookup"><span data-stu-id="f8e15-131">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="f8e15-132">Esplorazione delle librerie NuGet V3, parte 2: ricerca di pacchetti</span><span class="sxs-lookup"><span data-stu-id="f8e15-132">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="f8e15-133">Esplorazione delle librerie NuGet V3, parte 3: installazione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="f8e15-133">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="f8e15-134">Questi post di Blog sono stati scritti poco dopo il rilascio della versione **3.4.3** dei pacchetti SDK del client NuGet.</span><span class="sxs-lookup"><span data-stu-id="f8e15-134">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="f8e15-135">Le versioni più recenti dei pacchetti potrebbero non essere compatibili con le informazioni contenute nei post di Blog.</span><span class="sxs-lookup"><span data-stu-id="f8e15-135">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="f8e15-136">Martin Björkström ha pubblicato un post di Blog per la serie di Blog di Dave Glick, in cui introduce un approccio diverso per l'uso di NuGet client SDK per installare i pacchetti NuGet:</span><span class="sxs-lookup"><span data-stu-id="f8e15-136">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="f8e15-137">Rivisitando le librerie NuGet V3</span><span class="sxs-lookup"><span data-stu-id="f8e15-137">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
