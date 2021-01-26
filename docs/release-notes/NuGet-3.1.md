---
title: Note sulla versione di NuGet 3,1
description: Note sulla versione per NuGet 3,1, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776531"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="060a3-103">Note sulla versione di NuGet 3,1</span><span class="sxs-lookup"><span data-stu-id="060a3-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="060a3-104">Note sulla versione di [NuGet 3,0](../release-notes/nuget-3.0.0.md)  |  [Note sulla versione di NuGet 3.1.1](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="060a3-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="060a3-105">NuGet 3,1 è stato rilasciato il 27 luglio 2015 come estensione in bundle per piattaforma UWP (Universal Windows Platform) SDK per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="060a3-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="060a3-106">Questa versione è stata distribuita con Windows Platform SDK, in modo che l'esperienza di sviluppo di Windows potesse sfruttare i vantaggi del lavoro multipiattaforma NuGet precedentemente avviato.</span><span class="sxs-lookup"><span data-stu-id="060a3-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="060a3-107">Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="060a3-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="060a3-108">Si consiglia agli sviluppatori che hanno accesso a Visual Studio Gallery di eseguire l'aggiornamento alla versione più recente disponibile, perché vengono sempre pubblicati aggiornamenti con correzioni di bug e nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="060a3-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="060a3-109">Estensione NuGet di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="060a3-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="060a3-110">I problemi e le funzionalità di questa versione sono contrassegnati in GitHub con l' [attività cardine "3,1 RTM UWP supporto transitivo"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  in totale, sono stati chiusi 67 problemi nella versione 3,1.</span><span class="sxs-lookup"><span data-stu-id="060a3-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="060a3-111">Nuove funzioni e caratteristiche</span><span class="sxs-lookup"><span data-stu-id="060a3-111">New Features</span></span>

* <span data-ttu-id="060a3-112">`project.json` supporto per il supporto per Windows UWP e ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="060a3-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="060a3-113">Installazione di pacchetti transitivi</span><span class="sxs-lookup"><span data-stu-id="060a3-113">Transitive package installation</span></span>

<span data-ttu-id="060a3-114">La descrizione e la definizione di queste funzionalità sono disponibili altrove nella documentazione.</span><span class="sxs-lookup"><span data-stu-id="060a3-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="060a3-115">Deprecato</span><span class="sxs-lookup"><span data-stu-id="060a3-115">Deprecated</span></span>

<span data-ttu-id="060a3-116">Le funzionalità seguenti non sono più disponibili per Visual Studio 2015:</span><span class="sxs-lookup"><span data-stu-id="060a3-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="060a3-117">Non è più possibile installare i pacchetti a livello di soluzione</span><span class="sxs-lookup"><span data-stu-id="060a3-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="060a3-118">Le funzionalità seguenti non sono più disponibili per Visual Studio 2015 e i progetti che usano la `project.json` specifica</span><span class="sxs-lookup"><span data-stu-id="060a3-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="060a3-119">`install.ps1` e `uninstall.ps1` -questi script verranno ignorati durante l'installazione, il ripristino, l'aggiornamento e la disinstallazione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="060a3-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="060a3-120">Le trasformazioni di configurazione verranno ignorate</span><span class="sxs-lookup"><span data-stu-id="060a3-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="060a3-121">Il contenuto verrà mantenuto, ma non copiato in un progetto.</span><span class="sxs-lookup"><span data-stu-id="060a3-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="060a3-122">Il team sta lavorando per riimplementare questa funzionalità, seguire la discussione e lo stato di avanzamento in: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="060a3-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="060a3-123">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="060a3-123">Known Issues</span></span>

<span data-ttu-id="060a3-124">In questa versione sono stati introdotti numerosi problemi noti.</span><span class="sxs-lookup"><span data-stu-id="060a3-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="060a3-125">L'installazione della versione 3,1 con Windows 10 SDK effettuerà il downgrade di qualsiasi versione dell'estensione NuGet installata in precedenza</span><span class="sxs-lookup"><span data-stu-id="060a3-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="060a3-126">Riga di comando NuGet</span><span class="sxs-lookup"><span data-stu-id="060a3-126">NuGet Command-line</span></span>

<span data-ttu-id="060a3-127">Il file eseguibile della riga di comando NuGet è stato aggiornato e spostato in un nuovo percorso distribuibile in modo che le versioni cronologiche di nuget.exe possano continuare a essere rese disponibili.</span><span class="sxs-lookup"><span data-stu-id="060a3-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="060a3-128">È possibile scaricare la versione beta 3,1 di nuget.exe per Windows in: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="060a3-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="060a3-129">Il nuovo percorso distribuibile si trova nell'host dist.nuget.org, con una struttura di cartelle che segue questo modello:</span><span class="sxs-lookup"><span data-stu-id="060a3-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a><span data-ttu-id="060a3-130">Nuove funzioni e caratteristiche</span><span class="sxs-lookup"><span data-stu-id="060a3-130">New Features</span></span>

* <span data-ttu-id="060a3-131">nuget.exe possibile ripristinare e installare i pacchetti in progetti che utilizzano un `project.json` file.</span><span class="sxs-lookup"><span data-stu-id="060a3-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="060a3-132">nuget.exe possibile connettersi e utilizzare il protocollo NuGet V3 in: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="060a3-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="060a3-133">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="060a3-133">Known Issues</span></span> ##

1.    <span data-ttu-id="060a3-134">Impossibile eseguire il pacchetto in un `project.json` file- [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="060a3-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="060a3-135">Non è supportato in mono- [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="060a3-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="060a3-136">Non è localizzato- [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="060a3-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="060a3-137">Non è firmato, proprio come il http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073) esistente</span><span class="sxs-lookup"><span data-stu-id="060a3-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
