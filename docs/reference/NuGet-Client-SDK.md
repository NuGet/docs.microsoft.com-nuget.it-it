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
# <a name="nuget-client-sdk"></a><span data-ttu-id="97d1a-103">NuGet Client SDK</span><span class="sxs-lookup"><span data-stu-id="97d1a-103">NuGet Client SDK</span></span>

> [!Note]
> <span data-ttu-id="97d1a-104">Non deve essere confusa con la [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span><span class="sxs-lookup"><span data-stu-id="97d1a-104">Not to be confused with the [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span></span>

<span data-ttu-id="97d1a-105">Il *NuGet Client SDK* fa riferimento a un gruppo di librerie .NET incentrati [NuGet](https://www.nuget.org/packages/NuGet.Client), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), e [NuGet. Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="97d1a-105">The *NuGet Client SDK* refers to a group of .NET libraries centered around [NuGet.Client](https://www.nuget.org/packages/NuGet.Client), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="97d1a-106">Questi pacchetti sostituiscono la precedente [togliere](https://www.nuget.org/packages/NuGet.Core/) libreria.</span><span class="sxs-lookup"><span data-stu-id="97d1a-106">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

<span data-ttu-id="97d1a-107">Microsoft sta lavorando con una superficie di attacco stabile che è possibile documentare a breve.</span><span class="sxs-lookup"><span data-stu-id="97d1a-107">We are working on having a stable surface area that we can document soon.</span></span>

## <a name="source-code"></a><span data-ttu-id="97d1a-108">Codice sorgente</span><span class="sxs-lookup"><span data-stu-id="97d1a-108">Source code</span></span>

<span data-ttu-id="97d1a-109">Il codice sorgente viene pubblicato in GitHub nel progetto [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span><span class="sxs-lookup"><span data-stu-id="97d1a-109">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="97d1a-110">Documentazione di terze parti</span><span class="sxs-lookup"><span data-stu-id="97d1a-110">Third-party documentation</span></span>

<span data-ttu-id="97d1a-111">È possibile trovare esempi e documentazione per alcune delle API della serie di blog seguente da Dave Glick, pubblicato 2016:</span><span class="sxs-lookup"><span data-stu-id="97d1a-111">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="97d1a-112">Esplorare le librerie di NuGet v3, parte 1: Introduzione e concetti</span><span class="sxs-lookup"><span data-stu-id="97d1a-112">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="97d1a-113">Esplorare le librerie di NuGet v3, parte 2: La ricerca di pacchetti</span><span class="sxs-lookup"><span data-stu-id="97d1a-113">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="97d1a-114">Esplorare le librerie di NuGet v3, parte 3: L'installazione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="97d1a-114">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="97d1a-115">Questi post di blog scritti subito dopo il **3.4.3** versione di NuGet sono stati rilasciati pacchetti SDK client.</span><span class="sxs-lookup"><span data-stu-id="97d1a-115">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="97d1a-116">Le versioni più recenti dei pacchetti possono essere incompatibili con le informazioni contenute nei post di blog.</span><span class="sxs-lookup"><span data-stu-id="97d1a-116">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="97d1a-117">Martin Björkström ha un post di blog di follow-up per serie di blog di Dave Glick dove presenta un approccio diverso usando il SDK del Client NuGet per l'installazione di pacchetti NuGet:</span><span class="sxs-lookup"><span data-stu-id="97d1a-117">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="97d1a-118">Rivedere le librerie di NuGet v3</span><span class="sxs-lookup"><span data-stu-id="97d1a-118">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
