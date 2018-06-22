---
title: Note sulla versione 3.4 RC NuGet
description: Note sulla versione per NuGet 3.4 RC inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e40d685a5256fdfee818f0cc1f1bc352c698f3c2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820820"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="2a711-103">Note sulla versione 3.4 RC NuGet</span><span class="sxs-lookup"><span data-stu-id="2a711-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="2a711-104">[Note sulla versione di NuGet 3.3](../release-notes/nuget-3.3.md) | [note sulla versione di NuGet 3.4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="2a711-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="2a711-105">NuGet 3.4-RC è stato rilasciato il 3 marzo 2016 insieme a Visual Studio 2015 Update 2 RC ed è stata compilata con alcuni principi in mente:</span><span class="sxs-lookup"><span data-stu-id="2a711-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="2a711-106">Supporto multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="2a711-106">Cross-Platform support</span></span>
* <span data-ttu-id="2a711-107">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="2a711-107">Performance improvements</span></span>
* <span data-ttu-id="2a711-108">Piccoli miglioramenti dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="2a711-108">Minor UI improvements</span></span>

<span data-ttu-id="2a711-109">Le funzionalità seguenti sono disponibili in questa RC, con più pianificato per la versione finale 3.4.</span><span class="sxs-lookup"><span data-stu-id="2a711-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="2a711-110">Nuove funzionalità</span><span class="sxs-lookup"><span data-stu-id="2a711-110">New Features</span></span>

* <span data-ttu-id="2a711-111">I client NuGet ora supportano la codifica di contenuto gzip dai repository</span><span class="sxs-lookup"><span data-stu-id="2a711-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="2a711-112">Supporto per PDB dai pacchetti nei progetti xproj</span><span class="sxs-lookup"><span data-stu-id="2a711-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="2a711-113">Supporto per iOS e le azioni di compilazione Android nell'elemento contentFiles</span><span class="sxs-lookup"><span data-stu-id="2a711-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="2a711-114">Supporto per il moniker del framework moniker netstandard e netstandardapp</span><span class="sxs-lookup"><span data-stu-id="2a711-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="2a711-115">Nuove funzionalità dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="2a711-115">New User Interface Features</span></span>

* <span data-ttu-id="2a711-116">Miglioramenti significativi delle prestazioni in particolare nelle schede installato, aggiornamenti e Consolidate</span><span class="sxs-lookup"><span data-stu-id="2a711-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="2a711-117">Installato e le schede degli aggiornamenti sono ora ordinate in ordine alfabetico</span><span class="sxs-lookup"><span data-stu-id="2a711-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="2a711-118">Aggiungere un pulsante di aggiornamento che consente una ricerca da aggiornare</span><span class="sxs-lookup"><span data-stu-id="2a711-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="2a711-119">Aggiornamenti e miglioramenti</span><span class="sxs-lookup"><span data-stu-id="2a711-119">Updates and Improvements</span></span>

* <span data-ttu-id="2a711-120">Pacchetti di cui viene fatto riferimento `project.json` mobile con versione non verrà aggiornata per ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="2a711-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="2a711-121">Al contrario, si aggiornerà solo quando forzato per il ripristino, pulire, ricompilare o modificare `project.json`.</span><span class="sxs-lookup"><span data-stu-id="2a711-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="2a711-122">le origini dei repository NuGet.org non forzate in una configurazione di progetto quando si utilizza l'interfaccia utente di configurazione NuGet.</span><span class="sxs-lookup"><span data-stu-id="2a711-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="2a711-123">NuGet non ripristina i pacchetti in progetti condivisi né scrive un file di blocco.</span><span class="sxs-lookup"><span data-stu-id="2a711-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="2a711-124">Abbiamo migliorati errore di rete e ripetere la gestione di server non è raggiungibile o lento a rispondere.</span><span class="sxs-lookup"><span data-stu-id="2a711-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="2a711-125">I comportamenti di tastiera e mouse vengono aggiornati nell'UI gestione pacchetto di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2a711-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="2a711-126">È ora supportano la versione più recente `project.json` schema DNX.</span><span class="sxs-lookup"><span data-stu-id="2a711-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="2a711-127">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="2a711-127">Known Issues</span></span>

<span data-ttu-id="2a711-128">Continuiamo a tenere traccia dei problemi nella lista di problemi di GitHub che può essere trovato in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="2a711-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>