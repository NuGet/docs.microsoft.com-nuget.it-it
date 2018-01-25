---
title: Note sulla versione 3.4 RC NuGet | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per NuGet 3.4 RC inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "NuGet 3.4 RC note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 749068683d6e2a3fd9dd29c69d9ff50137acdd46
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="7845f-104">Note sulla versione 3.4 RC NuGet</span><span class="sxs-lookup"><span data-stu-id="7845f-104">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="7845f-105">[Note sulla versione di NuGet 3.3](../release-notes/nuget-3.3.md) | [note sulla versione di NuGet 3.4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="7845f-105">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="7845f-106">NuGet 3.4-RC è stato rilasciato il 3 marzo 2016 insieme a Visual Studio 2015 Update 2 RC ed è stata compilata con alcuni principi in mente:</span><span class="sxs-lookup"><span data-stu-id="7845f-106">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="7845f-107">Supporto multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="7845f-107">Cross-Platform support</span></span>
* <span data-ttu-id="7845f-108">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="7845f-108">Performance improvements</span></span>
* <span data-ttu-id="7845f-109">Piccoli miglioramenti dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="7845f-109">Minor UI improvements</span></span>

<span data-ttu-id="7845f-110">Le funzionalità seguenti sono disponibili in questa RC, con più pianificato per la versione finale 3.4.</span><span class="sxs-lookup"><span data-stu-id="7845f-110">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="7845f-111">Nuove funzionalità</span><span class="sxs-lookup"><span data-stu-id="7845f-111">New Features</span></span>

* <span data-ttu-id="7845f-112">I client NuGet ora supportano la codifica di contenuto gzip dai repository</span><span class="sxs-lookup"><span data-stu-id="7845f-112">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="7845f-113">Supporto per PDB dai pacchetti nei progetti xproj</span><span class="sxs-lookup"><span data-stu-id="7845f-113">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="7845f-114">Supporto per iOS e le azioni di compilazione Android nell'elemento contentFiles</span><span class="sxs-lookup"><span data-stu-id="7845f-114">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="7845f-115">Supporto per il moniker del framework moniker netstandard e netstandardapp</span><span class="sxs-lookup"><span data-stu-id="7845f-115">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="7845f-116">Nuove funzionalità dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="7845f-116">New User Interface Features</span></span>

* <span data-ttu-id="7845f-117">Miglioramenti significativi delle prestazioni in particolare nelle schede installato, aggiornamenti e Consolidate</span><span class="sxs-lookup"><span data-stu-id="7845f-117">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="7845f-118">Installato e le schede degli aggiornamenti sono ora ordinate in ordine alfabetico</span><span class="sxs-lookup"><span data-stu-id="7845f-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="7845f-119">Aggiungere un pulsante di aggiornamento che consente una ricerca da aggiornare</span><span class="sxs-lookup"><span data-stu-id="7845f-119">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="7845f-120">Aggiornamenti e miglioramenti</span><span class="sxs-lookup"><span data-stu-id="7845f-120">Updates and Improvements</span></span>

* <span data-ttu-id="7845f-121">Pacchetti di cui viene fatto riferimento `project.json` mobile con versione non verrà aggiornata per ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="7845f-121">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="7845f-122">Al contrario, si aggiornerà solo quando forzato per il ripristino, pulire, ricompilare o modificare `project.json`.</span><span class="sxs-lookup"><span data-stu-id="7845f-122">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="7845f-123">le origini dei repository NuGet.org non forzate in una configurazione di progetto quando si utilizza l'interfaccia utente di configurazione NuGet.</span><span class="sxs-lookup"><span data-stu-id="7845f-123">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="7845f-124">NuGet non ripristina i pacchetti in progetti condivisi né scrive un file di blocco.</span><span class="sxs-lookup"><span data-stu-id="7845f-124">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="7845f-125">Abbiamo migliorati errore di rete e ripetere la gestione di server non è raggiungibile o lento a rispondere.</span><span class="sxs-lookup"><span data-stu-id="7845f-125">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="7845f-126">I comportamenti di tastiera e mouse vengono aggiornati nell'UI gestione pacchetto di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7845f-126">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="7845f-127">È ora supportano la versione più recente `project.json` schema DNX.</span><span class="sxs-lookup"><span data-stu-id="7845f-127">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="7845f-128">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="7845f-128">Known Issues</span></span>

<span data-ttu-id="7845f-129">Continuiamo a tenere traccia dei problemi nell'elenco di problemi di GitHub in cui è reperibile in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="7845f-129">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>