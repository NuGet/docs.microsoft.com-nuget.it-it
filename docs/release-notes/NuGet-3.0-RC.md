---
title: Note sulla versione RC di NuGet 3.0
description: Note sulla versione per NuGet 3.0 RC inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 28ac49d9e9071d16d20b24808abb0acaab214ffd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819598"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="a5e3e-103">Note sulla versione RC di NuGet 3.0</span><span class="sxs-lookup"><span data-stu-id="a5e3e-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="a5e3e-104">[Note sulla versione Beta di NuGet 3.0](../release-notes/nuget-3.0-beta.md) | [note sulla versione di NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="a5e3e-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="a5e3e-105">NuGet 3.0 RC il 29 aprile 2015 è stata rilasciata con la versione di Visual Studio 2015 RC.</span><span class="sxs-lookup"><span data-stu-id="a5e3e-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="a5e3e-106">Questa versione presenta una serie di importanti correzioni di bug, miglioramenti delle prestazioni e gli aggiornamenti per supportare nuovi Framework.</span><span class="sxs-lookup"><span data-stu-id="a5e3e-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="a5e3e-107">È disponibile solo per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="a5e3e-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="a5e3e-108">Continua lo stato attivo sulle prestazioni</span><span class="sxs-lookup"><span data-stu-id="a5e3e-108">Continued Focus on Performance</span></span>

<span data-ttu-id="a5e3e-109">Stabilità e prestazioni delle query NuGet continuano a essere un argomento che è trattata in.</span><span class="sxs-lookup"><span data-stu-id="a5e3e-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="a5e3e-110">Con questa versione, è consigliabile iniziare visualizzare le operazioni di ricerca molto rapida NuGet UI e sito Web.</span><span class="sxs-lookup"><span data-stu-id="a5e3e-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="a5e3e-111">Viene eseguito il monitoraggio il servizio e come utilizzare il servizio in modo da potere continuare a ottimizzare queste operazioni.</span><span class="sxs-lookup"><span data-stu-id="a5e3e-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="a5e3e-112">Importanti problemi risolti</span><span class="sxs-lookup"><span data-stu-id="a5e3e-112">Significant Issues Resolved</span></span>

<span data-ttu-id="a5e3e-113">Per stabilizzare i client NuGet, è risolvere molti problemi come parte di questa versione.</span><span class="sxs-lookup"><span data-stu-id="a5e3e-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="a5e3e-114">Di seguito è solo un breve elenco di alcuni dei più importanti problemi risolti:</span><span class="sxs-lookup"><span data-stu-id="a5e3e-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="a5e3e-115">Durante la ridenominazione di framework K per ASP.NET 5, moniker del framework sono stati aggiornati per gestire dnx e dnxcore [collegamento](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="a5e3e-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="a5e3e-116">Aggiunta di documentazione della Guida dai collegamenti nell'interfaccia utente di Visual Studio [collegamento](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="a5e3e-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="a5e3e-117">Migliore gestione dei riferimenti complessi in `.nuspec` con i riferimenti framework delimitato da virgole [collegamento](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="a5e3e-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="a5e3e-118">Fissa il supporto per lingue giapponese [collegamento](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="a5e3e-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="a5e3e-119">Il client aggiornato per consentire l'utilizzo di nuovi endpoint v3 per i progetti ASP.NET 5 [collegamento](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="a5e3e-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="a5e3e-120">Cartella di pacchetti handle aggiornata per una migliore controllo del codice sorgente [collegamento](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="a5e3e-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="a5e3e-121">Fissa il supporto per pacchetti satellite [collegamento](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="a5e3e-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="a5e3e-122">Corretto il supporto per i file di contenuto specifico del framework [collegamento](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="a5e3e-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="a5e3e-123">Revisione di presenza di GitHub</span><span class="sxs-lookup"><span data-stu-id="a5e3e-123">GitHub presence overhaul</span></span>

<span data-ttu-id="a5e3e-124">È stato apportato alcune modifiche per il nostro [origine repository di codice su GitHub](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="a5e3e-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="a5e3e-125">Se si dispone di eventuali problemi con il client NuGet di Visual Studio, i comandi di Powershell o la riga di comando eseguibile è possibile accedere a questi problemi e monitorare lo stato di avanzamento nel nostro [elenco di problemi di repository GitHub Home](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="a5e3e-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="a5e3e-126">Microsoft sta verificando problemi per la raccolta nel nostro [repository GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="a5e3e-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="a5e3e-127">In futuro</span><span class="sxs-lookup"><span data-stu-id="a5e3e-127">Stay Tuned</span></span>

<span data-ttu-id="a5e3e-128">Tenere d'occhio [blog](http://blog.nuget.org) per più lo stato di avanzamento e annunci per NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="a5e3e-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>