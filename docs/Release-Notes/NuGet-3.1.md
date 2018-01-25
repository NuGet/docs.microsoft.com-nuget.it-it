---
title: Note sulla versione 3.1 NuGet | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per NuGet 3.1 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "3.1 NuGet note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a7aa43b8701b3bbef8f6ebce9a5d636ee1bc6abe
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="3ab94-104">Note sulla versione 3.1 di NuGet</span><span class="sxs-lookup"><span data-stu-id="3ab94-104">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="3ab94-105">[Note sulla versione di NuGet 3.0](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 note](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="3ab94-105">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="3ab94-106">NuGet 3.1 è stata rilasciata 27 luglio 2015 come estensione in dotazione di Universal Windows Platform SDK per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="3ab94-106">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="3ab94-107">Questa versione con il SDK della piattaforma Windows messo a disposizione in modo che l'esperienza di sviluppo di Windows può sfruttare il lavoro multipiattaforma NuGet che era stato avviato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3ab94-107">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="3ab94-108">Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="3ab94-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="3ab94-109">È consigliabile gli sviluppatori che dispongono dell'accesso per l'aggiornamento della raccolta di Visual Studio per la versione più recente è disponibile, come sempre attualmente vengono pubblicati gli aggiornamenti con le nuove funzionalità e correzioni di bug.</span><span class="sxs-lookup"><span data-stu-id="3ab94-109">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="3ab94-110">Estensione di NuGet di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3ab94-110">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="3ab94-111">Problemi e le funzionalità in questa versione sono contrassegnate su GitHub con il [attività cardine "3.1 del supporto transitiva UWP RTM"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) In totale, è stato chiuso 67 problemi nella versione 3.1.</span><span class="sxs-lookup"><span data-stu-id="3ab94-111">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="3ab94-112">Nuove funzionalità</span><span class="sxs-lookup"><span data-stu-id="3ab94-112">New Features</span></span>

* <span data-ttu-id="3ab94-113">`project.json`supporto per il supporto della piattaforma UWP Windows e ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="3ab94-113">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="3ab94-114">Installazione del pacchetto transitiva</span><span class="sxs-lookup"><span data-stu-id="3ab94-114">Transitive package installation</span></span>

<span data-ttu-id="3ab94-115">Descrizione e la definizione di queste funzionalità sono disponibili in un' posizione nella documentazione.</span><span class="sxs-lookup"><span data-stu-id="3ab94-115">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="3ab94-116">Deprecato</span><span class="sxs-lookup"><span data-stu-id="3ab94-116">Deprecated</span></span>

<span data-ttu-id="3ab94-117">Le funzionalità seguenti non sono più disponibili per Visual Studio 2015:</span><span class="sxs-lookup"><span data-stu-id="3ab94-117">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="3ab94-118">Pacchetti a livello di soluzione non possono più essere installati</span><span class="sxs-lookup"><span data-stu-id="3ab94-118">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="3ab94-119">Le funzionalità seguenti non sono più disponibili per Visual Studio 2015 e i progetti che usano il `project.json` specifica</span><span class="sxs-lookup"><span data-stu-id="3ab94-119">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="3ab94-120">`install.ps1`e `uninstall.ps1` -questi script verranno ignorati durante l'installazione del pacchetto, ripristinare, aggiornare e disinstallare</span><span class="sxs-lookup"><span data-stu-id="3ab94-120">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="3ab94-121">Trasformazioni di configurazione verranno ignorate</span><span class="sxs-lookup"><span data-stu-id="3ab94-121">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="3ab94-122">Il contenuto verrà eseguito, ma non è stato copiato in un progetto.</span><span class="sxs-lookup"><span data-stu-id="3ab94-122">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="3ab94-123">Il team sta lavorando per implementare nuovamente questa funzionalità, seguire la discussione e sullo stato di avanzamento in: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="3ab94-123">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="3ab94-124">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="3ab94-124">Known Issues</span></span>

<span data-ttu-id="3ab94-125">Si sono verificati alcuni problemi noti forniti con questa versione.</span><span class="sxs-lookup"><span data-stu-id="3ab94-125">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="3ab94-126">Installazione della versione 3.1 con Windows 10 SDK verrà effettuato il downgrade di qualsiasi versione di estensione NuGet che era stato precedentemente installato</span><span class="sxs-lookup"><span data-stu-id="3ab94-126">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="3ab94-127">NuGet da riga di comando</span><span class="sxs-lookup"><span data-stu-id="3ab94-127">NuGet Command-line</span></span>

<span data-ttu-id="3ab94-128">Il file eseguibile da riga di comando di NuGet è stato aggiornato e viene spostato in una nuova posizione distribuibile in modo da versioni precedenti di nuget.exe possono continuare a essere rese disponibili.</span><span class="sxs-lookup"><span data-stu-id="3ab94-128">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="3ab94-129">È possibile scaricare la versione 3.1 beta di nuget.exe per Windows all'indirizzo: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="3ab94-129">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="3ab94-130">Il nuovo percorso distribuibile risiede nell'host dist.nuget.org, con una struttura di cartelle che segue questo modello:</span><span class="sxs-lookup"><span data-stu-id="3ab94-130">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="3ab94-131">Nuove funzionalità</span><span class="sxs-lookup"><span data-stu-id="3ab94-131">New Features</span></span>

* <span data-ttu-id="3ab94-132">NuGet.exe è possibile ripristinare e installare i pacchetti in progetti che utilizzano un `project.json` file.</span><span class="sxs-lookup"><span data-stu-id="3ab94-132">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="3ab94-133">NuGet.exe possono connettersi e utilizzare il protocollo di NuGet v3 a: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="3ab94-133">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="3ab94-134">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="3ab94-134">Known Issues</span></span> ##

1.    <span data-ttu-id="3ab94-135">Non è possibile eseguire contro un `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="3ab94-135">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="3ab94-136">Non è supportato in Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="3ab94-136">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="3ab94-137">Non è localizzato - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="3ab94-137">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="3ab94-138">Non è firmato, esattamente come http://nuget.org/nuget.exe esistente - [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="3ab94-138">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
