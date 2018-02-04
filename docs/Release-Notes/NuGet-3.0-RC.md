---
title: Note sulla versione RC di NuGet 3.0 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per NuGet 3.0 RC inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "NuGet 3.0 RC note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4693fd8884283e01d3c0a8ad74e0692c1ca00659
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="585d3-104">Note sulla versione RC di NuGet 3.0</span><span class="sxs-lookup"><span data-stu-id="585d3-104">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="585d3-105">[Note sulla versione Beta di NuGet 3.0](../release-notes/nuget-3.0-beta.md) | [note sulla versione di NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="585d3-105">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="585d3-106">NuGet 3.0 RC il 29 aprile 2015 è stata rilasciata con la versione di Visual Studio 2015 RC.</span><span class="sxs-lookup"><span data-stu-id="585d3-106">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="585d3-107">Questa versione presenta una serie di importanti correzioni di bug, miglioramenti delle prestazioni e gli aggiornamenti per supportare nuovi Framework.</span><span class="sxs-lookup"><span data-stu-id="585d3-107">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="585d3-108">È disponibile solo per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="585d3-108">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="585d3-109">Continua lo stato attivo sulle prestazioni</span><span class="sxs-lookup"><span data-stu-id="585d3-109">Continued Focus on Performance</span></span>

<span data-ttu-id="585d3-110">Stabilità e prestazioni delle query NuGet continuano a essere un argomento che è trattata in.</span><span class="sxs-lookup"><span data-stu-id="585d3-110">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="585d3-111">Con questa versione, è consigliabile iniziare visualizzare le operazioni di ricerca molto rapida NuGet UI e sito Web.</span><span class="sxs-lookup"><span data-stu-id="585d3-111">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="585d3-112">Viene eseguito il monitoraggio il servizio e come utilizzare il servizio in modo da potere continuare a ottimizzare queste operazioni.</span><span class="sxs-lookup"><span data-stu-id="585d3-112">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="585d3-113">Importanti problemi risolti</span><span class="sxs-lookup"><span data-stu-id="585d3-113">Significant Issues Resolved</span></span>

<span data-ttu-id="585d3-114">Per stabilizzare i client NuGet, è risolvere molti problemi come parte di questa versione.</span><span class="sxs-lookup"><span data-stu-id="585d3-114">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="585d3-115">Di seguito è solo un breve elenco di alcuni dei più importanti problemi risolti:</span><span class="sxs-lookup"><span data-stu-id="585d3-115">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="585d3-116">Durante la ridenominazione di framework K per ASP.NET 5, moniker del framework sono stati aggiornati per gestire dnx e dnxcore [collegamento](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="585d3-116">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="585d3-117">Aggiunta di documentazione della Guida dai collegamenti nell'interfaccia utente Visual Studio [collegamento](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="585d3-117">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="585d3-118">Migliore gestione dei riferimenti complessi in `.nuspec` con i riferimenti framework delimitato da virgole [collegamento](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="585d3-118">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="585d3-119">Fissa il supporto per lingue giapponese [collegamento](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="585d3-119">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="585d3-120">Il client aggiornato per consentire l'utilizzo di nuovi endpoint v3 per i progetti di ASP.NET 5 [collegamento](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="585d3-120">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="585d3-121">Cartella di pacchetti di handle aggiornata per una migliore controllo del codice sorgente [collegamento](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="585d3-121">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="585d3-122">Supporto per i pacchetti satellite fissa [collegamento](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="585d3-122">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="585d3-123">Supporto per i file di contenuto specifico del framework corretti [collegamento](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="585d3-123">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="585d3-124">Revisione di presenza di GitHub</span><span class="sxs-lookup"><span data-stu-id="585d3-124">GitHub presence overhaul</span></span>

<span data-ttu-id="585d3-125">È stato apportato alcune modifiche per il nostro [origine repository di codice su GitHub](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="585d3-125">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="585d3-126">Se si dispone di eventuali problemi con il client NuGet di Visual Studio, i comandi di Powershell o la riga di comando eseguibile è possibile accedere a questi problemi e monitorare lo stato di avanzamento nel nostro [elenco di problemi di repository GitHub Home](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="585d3-126">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="585d3-127">Microsoft sta verificando problemi per la raccolta nel nostro [repository GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="585d3-127">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="585d3-128">In futuro</span><span class="sxs-lookup"><span data-stu-id="585d3-128">Stay Tuned</span></span>

<span data-ttu-id="585d3-129">Tenere d'occhio [blog](http://blog.nuget.org) per più lo stato di avanzamento e annunci per NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="585d3-129">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>