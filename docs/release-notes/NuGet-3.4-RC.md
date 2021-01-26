---
title: Note sulla versione di NuGet 3,4-RC
description: Note sulla versione per NuGet 3,4 RC, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780236"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="f0778-103">Note sulla versione di NuGet 3,4-RC</span><span class="sxs-lookup"><span data-stu-id="f0778-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="f0778-104">Note sulla versione di [NuGet 3,3](../release-notes/nuget-3.3.md)  |  [Note sulla versione di NuGet 3,4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="f0778-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="f0778-105">NuGet 3,4-RC è stato rilasciato il 3 marzo 2016 insieme a Visual Studio 2015 Update 2 RC ed è stato creato con alcuni principi in mente:</span><span class="sxs-lookup"><span data-stu-id="f0778-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="f0778-106">Supporto multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="f0778-106">Cross-Platform support</span></span>
* <span data-ttu-id="f0778-107">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="f0778-107">Performance improvements</span></span>
* <span data-ttu-id="f0778-108">Miglioramenti dell'interfaccia utente secondaria</span><span class="sxs-lookup"><span data-stu-id="f0778-108">Minor UI improvements</span></span>

<span data-ttu-id="f0778-109">Le funzionalità seguenti sono disponibili in questa versione RC, con più pianificate per la versione finale 3,4.</span><span class="sxs-lookup"><span data-stu-id="f0778-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="f0778-110">Nuove funzioni e caratteristiche</span><span class="sxs-lookup"><span data-stu-id="f0778-110">New Features</span></span>

* <span data-ttu-id="f0778-111">I client NuGet supportano ora la codifica di contenuto gzip dai repository</span><span class="sxs-lookup"><span data-stu-id="f0778-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="f0778-112">Supporto per PDB dai pacchetti nei progetti xproj</span><span class="sxs-lookup"><span data-stu-id="f0778-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="f0778-113">Supporto per le azioni di compilazione iOS e Android nell'elemento contentFiles</span><span class="sxs-lookup"><span data-stu-id="f0778-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="f0778-114">Supporto per i moniker del Framework netstandard e netstandardapp</span><span class="sxs-lookup"><span data-stu-id="f0778-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="f0778-115">Nuove funzionalità dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="f0778-115">New User Interface Features</span></span>

* <span data-ttu-id="f0778-116">Miglioramenti significativi delle prestazioni in particolare sulle schede installate, aggiornate e consolidate</span><span class="sxs-lookup"><span data-stu-id="f0778-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="f0778-117">Le schede installato e aggiornamenti sono ora ordinate in ordine alfabetico</span><span class="sxs-lookup"><span data-stu-id="f0778-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="f0778-118">È stato aggiunto un pulsante di aggiornamento che consente di aggiornare una ricerca</span><span class="sxs-lookup"><span data-stu-id="f0778-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="f0778-119">Aggiornamenti e miglioramenti</span><span class="sxs-lookup"><span data-stu-id="f0778-119">Updates and Improvements</span></span>

* <span data-ttu-id="f0778-120">I pacchetti a cui viene fatto riferimento in `project.json` che hanno una versione mobile non vengono aggiornati in ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="f0778-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="f0778-121">Verranno invece aggiornati solo quando è necessario eseguire il ripristino, la pulizia, la ricompilazione o la modifica `project.json` .</span><span class="sxs-lookup"><span data-stu-id="f0778-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="f0778-122">le origini del repository nuget.org non sono più forzate in una configurazione di progetto quando si usa l'interfaccia utente di configurazione di NuGet.</span><span class="sxs-lookup"><span data-stu-id="f0778-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="f0778-123">NuGet non ripristina più i pacchetti nei progetti condivisi né scrive un file di blocco.</span><span class="sxs-lookup"><span data-stu-id="f0778-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="f0778-124">Si è verificato un errore di rete migliorato ed è stato effettuato un nuovo tentativo di gestione per server non raggiungibili o lenti a risposta.</span><span class="sxs-lookup"><span data-stu-id="f0778-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="f0778-125">I comportamenti della tastiera e del mouse sono stati migliorati nell'interfaccia utente di gestione pacchetti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f0778-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="f0778-126">È ora supportato lo schema più recente `project.json` in DNX.</span><span class="sxs-lookup"><span data-stu-id="f0778-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="f0778-127">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="f0778-127">Known Issues</span></span>

<span data-ttu-id="f0778-128">Continuiamo a tenere traccia dei problemi nell'elenco dei problemi di GitHub disponibili all'indirizzo: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="f0778-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>