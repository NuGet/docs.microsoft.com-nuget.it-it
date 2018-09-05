---
title: Note sulla versione 3.4-RC di NuGet
description: Note sulla versione per NuGet 3.4 RC, tra cui i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546754"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="c41a8-103">Note sulla versione 3.4-RC di NuGet</span><span class="sxs-lookup"><span data-stu-id="c41a8-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="c41a8-104">[Note sulla versione di NuGet 3.3](../release-notes/nuget-3.3.md) | [note sulla versione di NuGet 3.4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="c41a8-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="c41a8-105">NuGet 3.4-RC è stato rilasciato il 3 marzo 2016 insieme a Visual Studio 2015 Update 2 RC e sia stato generato con alcuni principi in mente:</span><span class="sxs-lookup"><span data-stu-id="c41a8-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="c41a8-106">Supporto multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="c41a8-106">Cross-Platform support</span></span>
* <span data-ttu-id="c41a8-107">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="c41a8-107">Performance improvements</span></span>
* <span data-ttu-id="c41a8-108">Miglioramenti dell'interfaccia utente secondari</span><span class="sxs-lookup"><span data-stu-id="c41a8-108">Minor UI improvements</span></span>

<span data-ttu-id="c41a8-109">Le funzionalità seguenti sono disponibili in RC, con più previsto per la versione finale 3.4.</span><span class="sxs-lookup"><span data-stu-id="c41a8-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="c41a8-110">Nuove funzionalità</span><span class="sxs-lookup"><span data-stu-id="c41a8-110">New Features</span></span>

* <span data-ttu-id="c41a8-111">I client NuGet supportano ora codifica di contenuto gzip dai repository</span><span class="sxs-lookup"><span data-stu-id="c41a8-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="c41a8-112">Supporto per i file PDB dai pacchetti nei progetti xproj</span><span class="sxs-lookup"><span data-stu-id="c41a8-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="c41a8-113">Supporto per iOS e le azioni di compilazione Android nell'elemento contentFiles</span><span class="sxs-lookup"><span data-stu-id="c41a8-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="c41a8-114">Supporto per i moniker netstandard e netstandardapp di framework</span><span class="sxs-lookup"><span data-stu-id="c41a8-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="c41a8-115">Nuove funzionalità dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="c41a8-115">New User Interface Features</span></span>

* <span data-ttu-id="c41a8-116">Miglioramenti significativi delle prestazioni in particolare nelle schede installato, gli aggiornamenti e consolida</span><span class="sxs-lookup"><span data-stu-id="c41a8-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="c41a8-117">Installazione e le schede degli aggiornamenti sono ora ordinate in ordine alfabetico</span><span class="sxs-lookup"><span data-stu-id="c41a8-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="c41a8-118">Aggiungere un pulsante di aggiornamento che consente una ricerca da aggiornare</span><span class="sxs-lookup"><span data-stu-id="c41a8-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="c41a8-119">Aggiornamenti e miglioramenti</span><span class="sxs-lookup"><span data-stu-id="c41a8-119">Updates and Improvements</span></span>

* <span data-ttu-id="c41a8-120">I pacchetti a cui fa riferimento `project.json` mobile con versione non verrà aggiornata per ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="c41a8-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="c41a8-121">Al contrario, si aggiornerà solo quando era necessario ripristinare, pulire, ricompilare o modificare `project.json`.</span><span class="sxs-lookup"><span data-stu-id="c41a8-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="c41a8-122">origini di repository NuGet.org non sono forzate non è più in una configurazione di progetto quando si usa l'interfaccia utente di configurazione NuGet.</span><span class="sxs-lookup"><span data-stu-id="c41a8-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="c41a8-123">Non è più NuGet Ripristina i pacchetti in progetti condivisi né scrive un file di blocco.</span><span class="sxs-lookup"><span data-stu-id="c41a8-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="c41a8-124">È stata migliorata l'errore di rete e ripetere la gestione per il server non è raggiungibile o rallentare di risposta.</span><span class="sxs-lookup"><span data-stu-id="c41a8-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="c41a8-125">I comportamenti di tastiera e mouse sono stati migliorati nella UI di gestione pacchetti Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c41a8-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="c41a8-126">Supportiamo ora la versione più recente `project.json` dello schema in DNX.</span><span class="sxs-lookup"><span data-stu-id="c41a8-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="c41a8-127">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="c41a8-127">Known Issues</span></span>

<span data-ttu-id="c41a8-128">Continuiamo a tenere traccia dei problemi nel nostro elenco di problemi di GitHub che può trovarsi in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="c41a8-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>