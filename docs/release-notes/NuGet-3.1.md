---
title: Note sulla versione 3.1 di NuGet
description: Note sulla versione per NuGet 3.1 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d14455da6f8af4db92f7105ea1b0e88eb9e71600
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820874"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="5030d-103">Note sulla versione 3.1 di NuGet</span><span class="sxs-lookup"><span data-stu-id="5030d-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="5030d-104">[Note sulla versione di NuGet 3.0](../release-notes/nuget-3.0.0.md) | [note sulla versione di NuGet 3.1.1](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="5030d-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="5030d-105">NuGet 3.1 è stata rilasciata 27 luglio 2015 come estensione in dotazione di Universal Windows Platform SDK per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="5030d-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="5030d-106">Questa versione con il SDK della piattaforma Windows messo a disposizione in modo che l'esperienza di sviluppo di Windows può sfruttare il lavoro multipiattaforma NuGet che era stato avviato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5030d-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="5030d-107">Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="5030d-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="5030d-108">È consigliabile gli sviluppatori che dispongono dell'accesso per l'aggiornamento della raccolta di Visual Studio per la versione più recente è disponibile, come sempre attualmente vengono pubblicati gli aggiornamenti con le nuove funzionalità e correzioni di bug.</span><span class="sxs-lookup"><span data-stu-id="5030d-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="5030d-109">Estensione di NuGet di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5030d-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="5030d-110">Problemi e le funzionalità in questa versione sono contrassegnate su GitHub con il [attività cardine "3.1 del supporto transitiva UWP RTM"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) In totale, è stato chiuso 67 problemi nella versione 3.1.</span><span class="sxs-lookup"><span data-stu-id="5030d-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="5030d-111">Nuove funzionalità</span><span class="sxs-lookup"><span data-stu-id="5030d-111">New Features</span></span>

* <span data-ttu-id="5030d-112">`project.json` supporto per il supporto della piattaforma UWP Windows e ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="5030d-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="5030d-113">Installazione del pacchetto transitiva</span><span class="sxs-lookup"><span data-stu-id="5030d-113">Transitive package installation</span></span>

<span data-ttu-id="5030d-114">Descrizione e la definizione di queste funzionalità sono disponibili in un' posizione nella documentazione.</span><span class="sxs-lookup"><span data-stu-id="5030d-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="5030d-115">Deprecato</span><span class="sxs-lookup"><span data-stu-id="5030d-115">Deprecated</span></span>

<span data-ttu-id="5030d-116">Le funzionalità seguenti non sono più disponibili per Visual Studio 2015:</span><span class="sxs-lookup"><span data-stu-id="5030d-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="5030d-117">Pacchetti a livello di soluzione non possono più essere installati</span><span class="sxs-lookup"><span data-stu-id="5030d-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="5030d-118">Le funzionalità seguenti non sono più disponibili per Visual Studio 2015 e i progetti che usano il `project.json` specifica</span><span class="sxs-lookup"><span data-stu-id="5030d-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="5030d-119">`install.ps1` e `uninstall.ps1` -questi script verranno ignorati durante l'installazione del pacchetto, ripristinare, aggiornare e disinstallare</span><span class="sxs-lookup"><span data-stu-id="5030d-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="5030d-120">Trasformazioni di configurazione verranno ignorate</span><span class="sxs-lookup"><span data-stu-id="5030d-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="5030d-121">Il contenuto verrà eseguito, ma non è stato copiato in un progetto.</span><span class="sxs-lookup"><span data-stu-id="5030d-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="5030d-122">Il team sta lavorando per implementare nuovamente questa funzionalità, seguire la discussione e sullo stato di avanzamento in: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="5030d-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="5030d-123">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="5030d-123">Known Issues</span></span>

<span data-ttu-id="5030d-124">Si sono verificati alcuni problemi noti forniti con questa versione.</span><span class="sxs-lookup"><span data-stu-id="5030d-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="5030d-125">Installazione della versione 3.1 con Windows 10 SDK verrà effettuato il downgrade di qualsiasi versione di estensione NuGet che era stato precedentemente installato</span><span class="sxs-lookup"><span data-stu-id="5030d-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="5030d-126">NuGet da riga di comando</span><span class="sxs-lookup"><span data-stu-id="5030d-126">NuGet Command-line</span></span>

<span data-ttu-id="5030d-127">Il file eseguibile da riga di comando di NuGet è stato aggiornato e viene spostato in una nuova posizione distribuibile in modo da versioni precedenti di nuget.exe possono continuare a essere rese disponibili.</span><span class="sxs-lookup"><span data-stu-id="5030d-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="5030d-128">È possibile scaricare la versione 3.1 beta di nuget.exe per Windows, visitare: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="5030d-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="5030d-129">Il nuovo percorso distribuibile risiede nell'host dist.nuget.org, con una struttura di cartelle che segue questo modello:</span><span class="sxs-lookup"><span data-stu-id="5030d-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="5030d-130">Nuove funzionalità</span><span class="sxs-lookup"><span data-stu-id="5030d-130">New Features</span></span>

* <span data-ttu-id="5030d-131">NuGet.exe è possibile ripristinare e installare i pacchetti in progetti che utilizzano un `project.json` file.</span><span class="sxs-lookup"><span data-stu-id="5030d-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="5030d-132">NuGet.exe possono connettersi e utilizzare il protocollo di NuGet v3 a: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="5030d-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="5030d-133">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="5030d-133">Known Issues</span></span> ##

1.    <span data-ttu-id="5030d-134">Non è possibile eseguire pack rispetto a un `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="5030d-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="5030d-135">Non è supportato in Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="5030d-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="5030d-136">Non è localizzato - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="5030d-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="5030d-137">Non è firmato, esattamente come esistenti http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="5030d-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
