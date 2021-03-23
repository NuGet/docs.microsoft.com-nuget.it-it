---
title: NuGet Client SDK
description: L'API è in continua evoluzione e non è ancora documentata, ma gli esempi sono disponibili nel Blog di Dave Glick.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: f9e08d37b30dfea83fd9b61f168c1e20f530ff9f
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859408"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="39622-103">NuGet Client SDK</span><span class="sxs-lookup"><span data-stu-id="39622-103">NuGet Client SDK</span></span>

<span data-ttu-id="39622-104">*NuGet client SDK* si riferisce a un gruppo di pacchetti NuGet:</span><span class="sxs-lookup"><span data-stu-id="39622-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="39622-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -Usato per interagire con i feed NuGet HTTP e basati su file</span><span class="sxs-lookup"><span data-stu-id="39622-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="39622-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) : Usato per interagire con i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="39622-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="39622-107">`NuGet.Protocol` dipende da questo pacchetto</span><span class="sxs-lookup"><span data-stu-id="39622-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="39622-108">È possibile trovare il codice sorgente per questi pacchetti nel repository GitHub [NuGet/NuGet. client](https://github.com/NuGet/NuGet.Client) .</span><span class="sxs-lookup"><span data-stu-id="39622-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>
<span data-ttu-id="39622-109">È possibile trovare il codice sorgente per questi esempi nel progetto [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="39622-109">You can find the source code for these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) project on GitHub.</span></span>

> [!Note]
> <span data-ttu-id="39622-110">Per la documentazione sul protocollo server NuGet, vedere l'API del [Server NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="39622-110">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="nugetprotocol"></a><span data-ttu-id="39622-111">NuGet. Protocol</span><span class="sxs-lookup"><span data-stu-id="39622-111">NuGet.Protocol</span></span>

<span data-ttu-id="39622-112">Installare il `NuGet.Protocol` pacchetto per interagire con i feed di pacchetti NuGet basati su cartelle e http:</span><span class="sxs-lookup"><span data-stu-id="39622-112">Install the `NuGet.Protocol` package to interact with HTTP and folder-based NuGet package feeds:</span></span>

```ps1
dotnet add package NuGet.Protocol
```

### <a name="list-package-versions"></a><span data-ttu-id="39622-113">Elencare le versioni del pacchetto</span><span class="sxs-lookup"><span data-stu-id="39622-113">List package versions</span></span>

<span data-ttu-id="39622-114">Trovare tutte le versioni di Newtonsoft.Jsusando l' [API del contenuto del pacchetto NuGet V3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="39622-114">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="39622-115">Scarica un pacchetto</span><span class="sxs-lookup"><span data-stu-id="39622-115">Download a package</span></span>

<span data-ttu-id="39622-116">Scaricare Newtonsoft.Jsin v 12.0.1 usando l' [API del contenuto del pacchetto NuGet V3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="39622-116">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="39622-117">Ottenere i metadati del pacchetto</span><span class="sxs-lookup"><span data-stu-id="39622-117">Get package metadata</span></span>

<span data-ttu-id="39622-118">Ottenere i metadati per il pacchetto "Newtonsoft.Json" usando l' [API dei metadati del pacchetto NuGet V3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="39622-118">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="39622-119">Ricerche nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="39622-119">Search packages</span></span>

<span data-ttu-id="39622-120">Cercare i pacchetti "JSON" usando l' [API di ricerca NuGet V3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="39622-120">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a><span data-ttu-id="39622-121">Eseguire il push di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="39622-121">Push a package</span></span>

<span data-ttu-id="39622-122">Eseguire il push di un pacchetto usando l' [API di push ed eliminazione NuGet V3](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="39622-122">Push a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a><span data-ttu-id="39622-123">Eliminare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="39622-123">Delete a package</span></span>

<span data-ttu-id="39622-124">Eliminare un pacchetto usando l' [API di push ed eliminazione NuGet V3](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="39622-124">Delete a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

> [!Note]
> <span data-ttu-id="39622-125">I server NuGet sono liberi di interpretare una richiesta di eliminazione del pacchetto come "eliminazione hardware", "eliminazione temporanea" o "Unlist".</span><span class="sxs-lookup"><span data-stu-id="39622-125">NuGet servers are free to interpret a package delete request as a "hard delete", "soft delete", or "unlist".</span></span>
> <span data-ttu-id="39622-126">Nuget.org, ad esempio, interpreta la richiesta di eliminazione del pacchetto come "Unlist".</span><span class="sxs-lookup"><span data-stu-id="39622-126">For example, nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="39622-127">Per ulteriori informazioni su questa procedura, vedere il criterio [eliminazione dei pacchetti](../nuget-org/policies/deleting-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="39622-127">For more information about this practice, see the [Deleting Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span>

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a><span data-ttu-id="39622-128">Usare i feed autenticati</span><span class="sxs-lookup"><span data-stu-id="39622-128">Work with authenticated feeds</span></span>

<span data-ttu-id="39622-129">Usare [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) per lavorare con i feed autenticati.</span><span class="sxs-lookup"><span data-stu-id="39622-129">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) to work with authenticated feeds.</span></span>

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a><span data-ttu-id="39622-130">NuGet. Packaging</span><span class="sxs-lookup"><span data-stu-id="39622-130">NuGet.Packaging</span></span>

<span data-ttu-id="39622-131">Installare il `NuGet.Packaging` pacchetto per interagire con `.nupkg` `.nuspec` i file e da un flusso:</span><span class="sxs-lookup"><span data-stu-id="39622-131">Install the `NuGet.Packaging` package to interact with `.nupkg` and `.nuspec` files from a stream:</span></span>

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a><span data-ttu-id="39622-132">Creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="39622-132">Create a package</span></span>

<span data-ttu-id="39622-133">Creare un pacchetto, impostare i metadati e aggiungere le dipendenze usando [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="39622-133">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39622-134">Si consiglia vivamente di creare pacchetti NuGet usando gli strumenti di NuGet ufficiali e **senza** usare questa API di basso livello.</span><span class="sxs-lookup"><span data-stu-id="39622-134">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="39622-135">Esistono diverse caratteristiche importanti per un pacchetto ben formato e la versione più recente degli strumenti consente di incorporare queste procedure consigliate.</span><span class="sxs-lookup"><span data-stu-id="39622-135">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="39622-136">Per altre informazioni sulla creazione di pacchetti NuGet, vedere la panoramica del [flusso di lavoro di creazione dei pacchetti](../create-packages/overview-and-workflow.md) e la documentazione per gli strumenti di Pack ufficiali, ad esempio [usando l'interfaccia della](../create-packages/creating-a-package-dotnet-cli.md)riga di comando di DotNet.</span><span class="sxs-lookup"><span data-stu-id="39622-136">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="39622-137">Leggi un pacchetto</span><span class="sxs-lookup"><span data-stu-id="39622-137">Read a package</span></span>

<span data-ttu-id="39622-138">Leggere un pacchetto da un flusso di file usando [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="39622-138">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="39622-139">Documentazione di terze parti</span><span class="sxs-lookup"><span data-stu-id="39622-139">Third-party documentation</span></span>

<span data-ttu-id="39622-140">È possibile trovare esempi e documentazione per alcune API nella serie di Blog di Dave Glick, pubblicata 2016:</span><span class="sxs-lookup"><span data-stu-id="39622-140">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="39622-141">Esplorazione delle librerie NuGet V3, parte 1: introduzione e concetti</span><span class="sxs-lookup"><span data-stu-id="39622-141">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="39622-142">Esplorazione delle librerie NuGet V3, parte 2: ricerca di pacchetti</span><span class="sxs-lookup"><span data-stu-id="39622-142">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="39622-143">Esplorazione delle librerie NuGet V3, parte 3: installazione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="39622-143">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="39622-144">Questi post di Blog sono stati scritti poco dopo il rilascio della versione **3.4.3** dei pacchetti SDK del client NuGet.</span><span class="sxs-lookup"><span data-stu-id="39622-144">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="39622-145">Le versioni più recenti dei pacchetti potrebbero non essere compatibili con le informazioni contenute nei post di Blog.</span><span class="sxs-lookup"><span data-stu-id="39622-145">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="39622-146">Martin Björkström ha pubblicato un post di Blog per la serie di Blog di Dave Glick, in cui introduce un approccio diverso per l'uso di NuGet client SDK per installare i pacchetti NuGet:</span><span class="sxs-lookup"><span data-stu-id="39622-146">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="39622-147">Rivisitando le librerie NuGet V3</span><span class="sxs-lookup"><span data-stu-id="39622-147">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
