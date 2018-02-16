---
title: Panoramica dell'hosting dei feed NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Panoramica delle opzioni per l'hosting dei feed o delle raccolte di pacchetti NuGet localmente o in remoto.
keywords: Feed NuGet, raccolta NuGet, feed di pacchetti personalizzati, NuGet.Server
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 738190e20603046d075faa3f50402601890583c1
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="hosting-your-own-nuget-feeds"></a><span data-ttu-id="80aea-104">Hosting dei feed NuGet</span><span class="sxs-lookup"><span data-stu-id="80aea-104">Hosting your own NuGet feeds</span></span>

<span data-ttu-id="80aea-105">Invece di rendere i pacchetti pubblicamente disponibili, potrebbe essere necessario rilasciarli solo per un pubblico limitato, ad esempio un'organizzazione o un gruppo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="80aea-105">Instead of making packages publicly available, you might want to release packages to only a limited audience, such as your organization or workgroup.</span></span> <span data-ttu-id="80aea-106">Inoltre, per alcune aziende potrebbe essere necessario limitare le librerie di terze parti utilizzabili dagli sviluppatori, vincolandoli ad attingere a un'origine pacchetto limitata anziché a nuget.org.</span><span class="sxs-lookup"><span data-stu-id="80aea-106">In addition, some companies may want to restrict which third-party libraries their developers may use, and thus direct those developers to draw from a limited package source rather than nuget.org.</span></span>

<span data-ttu-id="80aea-107">Per tutti questi scopi, NuGet supporta l'impostazione di origini pacchetto private secondo le modalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="80aea-107">For all such purposes, NuGet supports setting up private package sources in the following ways:</span></span>

- <span data-ttu-id="80aea-108">Feed locale: i pacchetti vengono semplicemente inseriti in una condivisione file di rete appropriata, preferibilmente usando `nuget init` e `nuget add` per creare una struttura di cartelle gerarchica (NuGet 3.3+).</span><span class="sxs-lookup"><span data-stu-id="80aea-108">Local feed: Packages are simply placed on a suitable network file share, ideally using `nuget init` and `nuget add` to create a hierarchical folder structure (NuGet 3.3+).</span></span> <span data-ttu-id="80aea-109">Per maggiori dettagli, vedere [Feed locali](../hosting-packages/local-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="80aea-109">For details, see [Local Feeds](../hosting-packages/local-feeds.md).</span></span>
- <span data-ttu-id="80aea-110">NuGet.Server: i pacchetti vengono resi disponibili tramite un server HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="80aea-110">NuGet.Server: Packages are made available through a local HTTP server.</span></span> <span data-ttu-id="80aea-111">Per maggiori dettagli, vedere [NuGet.Server](../hosting-packages/nuget-server.md).</span><span class="sxs-lookup"><span data-stu-id="80aea-111">For details, see [NuGet.Server](../hosting-packages/nuget-server.md).</span></span>
- <span data-ttu-id="80aea-112">Raccolta NuGet: i pacchetti sono ospitati in un server Internet tramite il [progetto della raccolta NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span><span class="sxs-lookup"><span data-stu-id="80aea-112">NuGet Gallery: Packages are hosted on an Internet server using the [NuGet Gallery Project](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span></span> <span data-ttu-id="80aea-113">La raccolta NuGet fornisce la gestione degli utenti e funzionalità quali un'interfaccia utente Web completa che consente la ricerca e l'esplorazione dei pacchetti dall'interno del browser, analogamente a nuget.org.</span><span class="sxs-lookup"><span data-stu-id="80aea-113">NuGet Gallery provides user management and features such as an extensive web UI that allows searching and exploring packages from within the browser, similar to nuget.org.</span></span>

<span data-ttu-id="80aea-114">Sono inoltre disponibili diversi altri prodotti di hosting NuGet che supportano feed privati remoti, tra cui:</span><span class="sxs-lookup"><span data-stu-id="80aea-114">There are also several other NuGet hosting products that support remote private feeds, including the following:</span></span>

- <span data-ttu-id="80aea-115">[Gestione pacchetti di Visual Studio Team Services](https://www.visualstudio.com/docs/package/nuget/publish), anche disponibile in Team Foundation Server 2017 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="80aea-115">[Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), which is also available on Team Foundation Server 2017 and later.</span></span>
- [<span data-ttu-id="80aea-116">MyGet</span><span class="sxs-lookup"><span data-stu-id="80aea-116">MyGet</span></span>](http://myget.org)
- <span data-ttu-id="80aea-117">[ProGet](http://inedo.com/proget) di Inedo</span><span class="sxs-lookup"><span data-stu-id="80aea-117">[ProGet](http://inedo.com/proget) from Inedo</span></span>
- <span data-ttu-id="80aea-118">[NuGet Server](http://nugetserver.net/), un progetto di community di Inedo</span><span class="sxs-lookup"><span data-stu-id="80aea-118">[NuGet Server](http://nugetserver.net/), a community project from Inedo</span></span>
- <span data-ttu-id="80aea-119">[NuGet Server (Open Source)](http://nuget-server.net), un'implementazione open source simile a NuGet Server di Inedo</span><span class="sxs-lookup"><span data-stu-id="80aea-119">[NuGet Server (Open Source)](http://nuget-server.net), an open-source implementation similar to Inedo's NuGet Server</span></span>
- <span data-ttu-id="80aea-120">[Artifactory](https://www.jfrog.com/artifactory/) di JFrog</span><span class="sxs-lookup"><span data-stu-id="80aea-120">[Artifactory](https://www.jfrog.com/artifactory/) from JFrog.</span></span>
- <span data-ttu-id="80aea-121">[Nexus](http://www.sonatype.org/nexus/) di Sonatype</span><span class="sxs-lookup"><span data-stu-id="80aea-121">[Nexus](http://www.sonatype.org/nexus/) from Sonatype.</span></span>
- <span data-ttu-id="80aea-122">[TeamCity](https://www.jetbrains.com/teamcity/) di JetBrains</span><span class="sxs-lookup"><span data-stu-id="80aea-122">[TeamCity](https://www.jetbrains.com/teamcity/) from JetBrains.</span></span>

<span data-ttu-id="80aea-123">Indipendentemente dalla modalità di hosting, i pacchetti diventano accessibili una volta aggiunti all'elenco delle origini disponibili in `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="80aea-123">Regardless of how packages are hosted, you access them by adding them to the list of available sources in `NuGet.Config`.</span></span> <span data-ttu-id="80aea-124">Questa operazione può essere eseguita in Visual Studio come descritto nella sezione [Package Sources](../tools/package-manager-ui.md#package-sources) (Origini dei pacchetti) o dalla riga di comando tramite [`nuget sources`](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="80aea-124">This can be done in Visual Studio as described in [Package Sources](../tools/package-manager-ui.md#package-sources), or from the command line using [`nuget sources`](../tools/cli-ref-sources.md).</span></span> <span data-ttu-id="80aea-125">Il percorso di un'origine può essere un nome di percorso di una cartella locale, un nome di rete o un URL.</span><span class="sxs-lookup"><span data-stu-id="80aea-125">The path to a source can be a local folder pathname, a network name, or a URL.</span></span>
