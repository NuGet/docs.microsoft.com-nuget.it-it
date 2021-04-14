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
# <a name="nuget-client-sdk"></a><span data-ttu-id="be4e6-103">NuGet Client SDK</span><span class="sxs-lookup"><span data-stu-id="be4e6-103">NuGet Client SDK</span></span>

<span data-ttu-id="be4e6-104">NuGet *Client SDK fa* riferimento a un gruppo di pacchetti NuGet:</span><span class="sxs-lookup"><span data-stu-id="be4e6-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="be4e6-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Usato per interagire con HTTP e feed NuGet basati su file</span><span class="sxs-lookup"><span data-stu-id="be4e6-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="be4e6-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Usato per interagire con i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="be4e6-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="be4e6-107">`NuGet.Protocol` dipende da questo pacchetto</span><span class="sxs-lookup"><span data-stu-id="be4e6-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="be4e6-108">È possibile trovare il codice sorgente per questi pacchetti nel repository GitHub [NuGet/NuGet.Client.](https://github.com/NuGet/NuGet.Client)</span><span class="sxs-lookup"><span data-stu-id="be4e6-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>
<span data-ttu-id="be4e6-109">È possibile trovare il codice sorgente per questi esempi nel [progetto NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) in GitHub.</span><span class="sxs-lookup"><span data-stu-id="be4e6-109">You can find the source code for these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) project on GitHub.</span></span>

> [!Note]
> <span data-ttu-id="be4e6-110">Per la documentazione sul protocollo server NuGet, vedere [l'API del server NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="be4e6-110">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="nugetprotocol"></a><span data-ttu-id="be4e6-111">NuGet.Protocol</span><span class="sxs-lookup"><span data-stu-id="be4e6-111">NuGet.Protocol</span></span>

<span data-ttu-id="be4e6-112">Installare il pacchetto per interagire con HTTP e feed di pacchetti `NuGet.Protocol` NuGet basati su cartelle:</span><span class="sxs-lookup"><span data-stu-id="be4e6-112">Install the `NuGet.Protocol` package to interact with HTTP and folder-based NuGet package feeds:</span></span>

```ps1
dotnet add package NuGet.Protocol
```

> [!Tip]
> <span data-ttu-id="be4e6-113">`Repository.Factory` è definito nello spazio `NuGet.Protocol.Core.Types` dei nomi e il metodo è un metodo di estensione definito nello spazio dei nomi `GetCoreV3` `NuGet.Protocol` .</span><span class="sxs-lookup"><span data-stu-id="be4e6-113">`Repository.Factory` is defined in the `NuGet.Protocol.Core.Types` namespace, and the `GetCoreV3` method is an extension method defined in the `NuGet.Protocol` namespace.</span></span> <span data-ttu-id="be4e6-114">Sarà quindi necessario aggiungere istruzioni `using` per entrambi gli spazi dei nomi.</span><span class="sxs-lookup"><span data-stu-id="be4e6-114">Therefore, you will need to add `using` statements for both namespaces.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="be4e6-115">Elencare le versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="be4e6-115">List package versions</span></span>

<span data-ttu-id="be4e6-116">Trovare tutte le versioni di Newtonsoft.Jssull'uso [dell'API NuGet V3 Package Content:](../api/package-base-address-resource.md#enumerate-package-versions)</span><span class="sxs-lookup"><span data-stu-id="be4e6-116">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="be4e6-117">Scaricare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="be4e6-117">Download a package</span></span>

<span data-ttu-id="be4e6-118">Scaricare Newtonsoft.Jsversione 12.0.1 usando [l'API NuGet V3 Package Content:](../api/package-base-address-resource.md)</span><span class="sxs-lookup"><span data-stu-id="be4e6-118">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="be4e6-119">Ottenere i metadati del pacchetto</span><span class="sxs-lookup"><span data-stu-id="be4e6-119">Get package metadata</span></span>

<span data-ttu-id="be4e6-120">Ottenere i metadati per il pacchetto "Newtonsoft.Js" usando l'API dei metadati del pacchetto [NuGet V3:](../api/registration-base-url-resource.md)</span><span class="sxs-lookup"><span data-stu-id="be4e6-120">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="be4e6-121">Ricerche nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="be4e6-121">Search packages</span></span>

<span data-ttu-id="be4e6-122">Cercare i pacchetti "json" usando [l'API di ricerca NuGet V3:](../api/search-query-service-resource.md)</span><span class="sxs-lookup"><span data-stu-id="be4e6-122">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a><span data-ttu-id="be4e6-123">Eseguire il push di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="be4e6-123">Push a package</span></span>

<span data-ttu-id="be4e6-124">Eseguire il push di un pacchetto [usando l'API NuGet V3 Push ed Delete:](../api/package-publish-resource.md)</span><span class="sxs-lookup"><span data-stu-id="be4e6-124">Push a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a><span data-ttu-id="be4e6-125">Eliminare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="be4e6-125">Delete a package</span></span>

<span data-ttu-id="be4e6-126">Eliminare un pacchetto usando [l'API NuGet V3 Push and Delete](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="be4e6-126">Delete a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

> [!Note]
> <span data-ttu-id="be4e6-127">I server NuGet sono liberi di interpretare una richiesta di eliminazione del pacchetto come "eliminazione hard", "eliminazione software" o "unlist".</span><span class="sxs-lookup"><span data-stu-id="be4e6-127">NuGet servers are free to interpret a package delete request as a "hard delete", "soft delete", or "unlist".</span></span>
> <span data-ttu-id="be4e6-128">Ad esempio, nuget.org interpreta la richiesta di eliminazione del pacchetto come "unlist".</span><span class="sxs-lookup"><span data-stu-id="be4e6-128">For example, nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="be4e6-129">Per altre informazioni su questa procedura, vedere il criterio [Eliminazione di](../nuget-org/policies/deleting-packages.md) pacchetti.</span><span class="sxs-lookup"><span data-stu-id="be4e6-129">For more information about this practice, see the [Deleting Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span>

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a><span data-ttu-id="be4e6-130">Usare feed autenticati</span><span class="sxs-lookup"><span data-stu-id="be4e6-130">Work with authenticated feeds</span></span>

<span data-ttu-id="be4e6-131">Usare [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) per usare i feed autenticati.</span><span class="sxs-lookup"><span data-stu-id="be4e6-131">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) to work with authenticated feeds.</span></span>

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a><span data-ttu-id="be4e6-132">NuGet.Packaging</span><span class="sxs-lookup"><span data-stu-id="be4e6-132">NuGet.Packaging</span></span>

<span data-ttu-id="be4e6-133">Installare il `NuGet.Packaging` pacchetto per interagire con i file e da un `.nupkg` `.nuspec` flusso:</span><span class="sxs-lookup"><span data-stu-id="be4e6-133">Install the `NuGet.Packaging` package to interact with `.nupkg` and `.nuspec` files from a stream:</span></span>

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a><span data-ttu-id="be4e6-134">Creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="be4e6-134">Create a package</span></span>

<span data-ttu-id="be4e6-135">Creare un pacchetto, impostare i metadati e aggiungere dipendenze usando [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="be4e6-135">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="be4e6-136">È consigliabile creare pacchetti NuGet usando gli strumenti NuGet ufficiali e non **usando** questa API di basso livello.</span><span class="sxs-lookup"><span data-stu-id="be4e6-136">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="be4e6-137">Esistono diverse caratteristiche importanti per un pacchetto ben formato e la versione più recente degli strumenti consente di incorporare queste procedure consigliate.</span><span class="sxs-lookup"><span data-stu-id="be4e6-137">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="be4e6-138">Per altre informazioni sulla creazione di pacchetti [](../create-packages/overview-and-workflow.md) NuGet, vedere la panoramica del flusso di lavoro di creazione del pacchetto e la documentazione per gli strumenti ufficiali dei pacchetti ( ad esempio, tramite l'interfaccia della riga di [comando dotnet](../create-packages/creating-a-package-dotnet-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="be4e6-138">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="be4e6-139">Leggere un pacchetto</span><span class="sxs-lookup"><span data-stu-id="be4e6-139">Read a package</span></span>

<span data-ttu-id="be4e6-140">Leggere un pacchetto da un flusso di file usando [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="be4e6-140">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="be4e6-141">Documentazione di terze parti</span><span class="sxs-lookup"><span data-stu-id="be4e6-141">Third-party documentation</span></span>

<span data-ttu-id="be4e6-142">Esempi e documentazione per alcune API sono disponibili nella serie di blog seguente di Dave Glick, pubblicata nel 2016:</span><span class="sxs-lookup"><span data-stu-id="be4e6-142">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="be4e6-143">Esplorazione delle librerie NuGet v3, parte 1: Introduzione e concetti</span><span class="sxs-lookup"><span data-stu-id="be4e6-143">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="be4e6-144">Esplorazione delle librerie NuGet v3, parte 2: Ricerca di pacchetti</span><span class="sxs-lookup"><span data-stu-id="be4e6-144">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="be4e6-145">Esplorazione delle librerie NuGet v3, parte 3: Installazione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="be4e6-145">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="be4e6-146">Questi post di blog sono stati scritti poco dopo il rilascio della versione **3.4.3** dei pacchetti SDK del client NuGet.</span><span class="sxs-lookup"><span data-stu-id="be4e6-146">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="be4e6-147">Le versioni più recenti dei pacchetti potrebbero non essere compatibili con le informazioni contenute nei post di blog.</span><span class="sxs-lookup"><span data-stu-id="be4e6-147">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="be4e6-148">Martin Björkström ha fatto un post di blog di follow-up alla serie di blog di Dave Glick in cui introduce un approccio diverso all'uso di NuGet Client SDK per installare i pacchetti NuGet:</span><span class="sxs-lookup"><span data-stu-id="be4e6-148">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="be4e6-149">Revisione delle librerie NuGet v3</span><span class="sxs-lookup"><span data-stu-id="be4e6-149">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
