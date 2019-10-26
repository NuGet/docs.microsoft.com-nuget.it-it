---
title: SDK client NuGet
description: L'API è in continua evoluzione e non è ancora documentata, ma gli esempi sono disponibili nel Blog di Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 873bde467a39653b818b49173d53bc983e99d1b9
ms.sourcegitcommit: f9645fc5f49c18978e12a292a3f832e162e069d5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2019
ms.locfileid: "72924609"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="11b29-103">SDK client NuGet</span><span class="sxs-lookup"><span data-stu-id="11b29-103">NuGet Client SDK</span></span>

<span data-ttu-id="11b29-104">*NuGet client SDK* si riferisce a un gruppo di pacchetti NuGet incentrati su [NuGet. Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet. Packaging](https://www.nuget.org/packages/NuGet.Packaging)e [NuGet. Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="11b29-104">The *NuGet Client SDK* refers to a group of NuGet packages centered around [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="11b29-105">Questi pacchetti sostituiscono la libreria [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/) precedente.</span><span class="sxs-lookup"><span data-stu-id="11b29-105">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

> [!Note]
>  <span data-ttu-id="11b29-106">Per la documentazione sul protocollo server NuGet, vedere l'API del [Server NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="11b29-106">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="source-code"></a><span data-ttu-id="11b29-107">Codice sorgente</span><span class="sxs-lookup"><span data-stu-id="11b29-107">Source code</span></span>

<span data-ttu-id="11b29-108">Il codice sorgente è pubblicato in GitHub nel progetto [NuGet/NuGet. client](https://github.com/NuGet/NuGet.Client).</span><span class="sxs-lookup"><span data-stu-id="11b29-108">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="11b29-109">Documentazione di terze parti</span><span class="sxs-lookup"><span data-stu-id="11b29-109">Third-party documentation</span></span>

<span data-ttu-id="11b29-110">È possibile trovare esempi e documentazione per alcune API nella serie di Blog di Dave Glick, pubblicata 2016:</span><span class="sxs-lookup"><span data-stu-id="11b29-110">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="11b29-111">Esplorazione delle librerie NuGet V3, parte 1: introduzione e concetti</span><span class="sxs-lookup"><span data-stu-id="11b29-111">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="11b29-112">Esplorazione delle librerie NuGet V3, parte 2: ricerca di pacchetti</span><span class="sxs-lookup"><span data-stu-id="11b29-112">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="11b29-113">Esplorazione delle librerie NuGet V3, parte 3: installazione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="11b29-113">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="11b29-114">Questi post di Blog sono stati scritti poco dopo il rilascio della versione **3.4.3** dei pacchetti SDK del client NuGet.</span><span class="sxs-lookup"><span data-stu-id="11b29-114">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="11b29-115">Le versioni più recenti dei pacchetti potrebbero non essere compatibili con le informazioni contenute nei post di Blog.</span><span class="sxs-lookup"><span data-stu-id="11b29-115">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="11b29-116">Martin Björkström ha fatto un post di Blog di seguito alla serie di Blog di Dave Glick, in cui è stato introdotto un approccio diverso per l'uso di NuGet client SDK per l'installazione dei pacchetti NuGet:</span><span class="sxs-lookup"><span data-stu-id="11b29-116">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="11b29-117">Rivisitando le librerie NuGet V3</span><span class="sxs-lookup"><span data-stu-id="11b29-117">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
