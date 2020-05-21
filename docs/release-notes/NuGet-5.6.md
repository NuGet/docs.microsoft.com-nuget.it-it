---
title: Note sulla versione di NuGet 5,6
description: Note sulla versione per NuGet 5,6, incluse nuove funzionalità, correzioni di bug e DCR.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727821"
---
# <a name="nuget-56-release-notes"></a><span data-ttu-id="848fc-103">Note sulla versione di NuGet 5,6</span><span class="sxs-lookup"><span data-stu-id="848fc-103">NuGet 5.6 Release Notes</span></span>

<span data-ttu-id="848fc-104">Veicoli per la distribuzione di NuGet:</span><span class="sxs-lookup"><span data-stu-id="848fc-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="848fc-105">Versione di NuGet</span><span class="sxs-lookup"><span data-stu-id="848fc-105">NuGet version</span></span> | <span data-ttu-id="848fc-106">Disponibile nella versione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="848fc-106">Available in Visual Studio version</span></span>| <span data-ttu-id="848fc-107">Disponibile in .NET SDK</span><span class="sxs-lookup"><span data-stu-id="848fc-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="848fc-108">**5.6.0**</span><span class="sxs-lookup"><span data-stu-id="848fc-108">**5.6.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="848fc-109">Visual Studio 2019 versione 16,6</span><span class="sxs-lookup"><span data-stu-id="848fc-109">Visual Studio 2019 version 16.6</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="848fc-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="848fc-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="848fc-111"><sup>1</sup> Installato con Visual Studio 2019 con carico di lavoro di .NET Core</span><span class="sxs-lookup"><span data-stu-id="848fc-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-56"></a><span data-ttu-id="848fc-112">Riepilogo: novità di 5,6</span><span class="sxs-lookup"><span data-stu-id="848fc-112">Summary: What's New in 5.6</span></span>

* <span data-ttu-id="848fc-113">Supporta i pacchetti di versioni non definitive con versioni mobili.</span><span class="sxs-lookup"><span data-stu-id="848fc-113">Support prerelease packages with floating versions.</span></span> <span data-ttu-id="848fc-114">`Version="*-*"`, `Version="1.*-*"` e float analogo alle versioni più recenti, incluse le versioni provvisorie, entro l'intervallo specificato- [#912](https://github.com/NuGet/Home/issues/912)</span><span class="sxs-lookup"><span data-stu-id="848fc-114">`Version="*-*"`, `Version="1.*-*"`, and similar float to latest versions, including prerelease versions, within specified range  - [#912](https://github.com/NuGet/Home/issues/912)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="848fc-115">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="848fc-115">Issues fixed in this release</span></span>

<span data-ttu-id="848fc-116">**Bug**</span><span class="sxs-lookup"><span data-stu-id="848fc-116">**Bugs:**</span></span>

* <span data-ttu-id="848fc-117">`nuget push *.nupkg`ha esito negativo se snupkg non esiste- [#8148](https://github.com/NuGet/Home/issues/8148)</span><span class="sxs-lookup"><span data-stu-id="848fc-117">`nuget push *.nupkg` fails when snupkg does not exist - [#8148](https://github.com/NuGet/Home/issues/8148)</span></span>

* <span data-ttu-id="848fc-118">Pack e diversi altri percorsi di codice non riescono a dipendere dalle impostazioni locali.</span><span class="sxs-lookup"><span data-stu-id="848fc-118">Pack, and several other code paths, fail dependent on locale.</span></span> <span data-ttu-id="848fc-119">Usare RegexOptions. CultureInvariant- [#8246](https://github.com/NuGet/Home/issues/8246)</span><span class="sxs-lookup"><span data-stu-id="848fc-119">Use RegexOptions.CultureInvariant - [#8246](https://github.com/NuGet/Home/issues/8246)</span></span>

* <span data-ttu-id="848fc-120">Prestazioni: le specifiche DG per gli scenari di progetto scaricati non devono essere scritte nei ripristini di anteprima [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="848fc-120">Perf: DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="848fc-121">Ripristino: migliorare le prestazioni memorizzando nella cache le specifiche del grafico delle dipendenze della soluzione- [#9201](https://github.com/NuGet/Home/issues/9201)</span><span class="sxs-lookup"><span data-stu-id="848fc-121">Restore: Improve performance by caching solution dependency graph spec - [#9201](https://github.com/NuGet/Home/issues/9201)</span></span>

* <span data-ttu-id="848fc-122">L'interfaccia utente PM non funziona per i progetti di stile SDK dopo l'installazione di un pacchetto con la console PM- [#9203](https://github.com/NuGet/Home/issues/9203)</span><span class="sxs-lookup"><span data-stu-id="848fc-122">PM UI doesn't work for SDK style projects after installing a package with PM Console - [#9203](https://github.com/NuGet/Home/issues/9203)</span></span>

* <span data-ttu-id="848fc-123">Non è possibile visualizzare l'icona incorporata nell'interfaccia utente di PM con il feed di pacchetti locale, a seconda di/vs [#9225](https://github.com/NuGet/Home/issues/9225)</span><span class="sxs-lookup"><span data-stu-id="848fc-123">Embedded icon can’t be shown in PM UI with local package feed - depending on / vs \ - [#9225](https://github.com/NuGet/Home/issues/9225)</span></span>

* <span data-ttu-id="848fc-124">NuGetVersion. TryParseStrict () deve restituire false se l'analisi non riesce. [#9255](https://github.com/NuGet/Home/issues/9255)</span><span class="sxs-lookup"><span data-stu-id="848fc-124">NuGetVersion.TryParseStrict() should return false if it fails to parse - [#9255](https://github.com/NuGet/Home/issues/9255)</span></span>

* <span data-ttu-id="848fc-125">`nuget.exe push`Guida per `-source` , deve suggerire l'uso del nome di origine, non dell'URL di origine- [#9265](https://github.com/NuGet/Home/issues/9265)</span><span class="sxs-lookup"><span data-stu-id="848fc-125">`nuget.exe push` help for `-source`, should suggest usage of source name, not source URL - [#9265](https://github.com/NuGet/Home/issues/9265)</span></span>

* <span data-ttu-id="848fc-126">`dotnet nuget add package SourceUri`Crea il nome di origine del pacchetto predefinito non valido- [#9277](https://github.com/NuGet/Home/issues/9277)</span><span class="sxs-lookup"><span data-stu-id="848fc-126">`dotnet nuget add package SourceUri`  creates bad default package source name - [#9277](https://github.com/NuGet/Home/issues/9277)</span></span>

* <span data-ttu-id="848fc-127">La lettura dello schermo non annuncia "ricerca..." messaggio durante il cambio di schede- [#9307](https://github.com/NuGet/Home/issues/9307)</span><span class="sxs-lookup"><span data-stu-id="848fc-127">Screen reader doesn't announce "Searching..." message when switching tabs - [#9307](https://github.com/NuGet/Home/issues/9307)</span></span>

* <span data-ttu-id="848fc-128">Accessibilità: stato attivo-colore rettangolo non accessibile per le schede dell'interfaccia utente nel tema scuro- [#9336](https://github.com/NuGet/Home/issues/9336)</span><span class="sxs-lookup"><span data-stu-id="848fc-128">Accessibility: Focus-rectangle color is not accessible PM UI tabs in dark theme - [#9336](https://github.com/NuGet/Home/issues/9336)</span></span>

* <span data-ttu-id="848fc-129">il ripristino di NuGet. exe 5,5 non riesce con MSBuild 14 o versioni precedenti [#9458](https://github.com/NuGet/Home/issues/9458)</span><span class="sxs-lookup"><span data-stu-id="848fc-129">nuget.exe 5.5 fails to restore with MSBuild 14 or below - [#9458](https://github.com/NuGet/Home/issues/9458)</span></span>

* <span data-ttu-id="848fc-130">Non registrare i millisecondi per i messaggi di ripristino- [#8977](https://github.com/NuGet/Home/issues/8977)</span><span class="sxs-lookup"><span data-stu-id="848fc-130">Don't log millisecond times in restore messages - [#8977](https://github.com/NuGet/Home/issues/8977)</span></span>

* <span data-ttu-id="848fc-131">Make IOutputConsole Async- [#9268](https://github.com/NuGet/Home/issues/9268)</span><span class="sxs-lookup"><span data-stu-id="848fc-131">Make IOutputConsole async - [#9268](https://github.com/NuGet/Home/issues/9268)</span></span>

* <span data-ttu-id="848fc-132">La selezione della versione di MSBuild non funziona in alcune culture non in lingua inglese, [#9322](https://github.com/NuGet/Home/issues/9322)</span><span class="sxs-lookup"><span data-stu-id="848fc-132">MSBuild version picking works poorly on some non-english cultures - [#9322](https://github.com/NuGet/Home/issues/9322)</span></span>

* <span data-ttu-id="848fc-133">Formato predefinito mancante `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)</span><span class="sxs-lookup"><span data-stu-id="848fc-133">Missing format default on `dotnet nuget list source` - [#9337](https://github.com/NuGet/Home/issues/9337)</span></span>

* <span data-ttu-id="848fc-134">Prestazioni: RestoreOperationLogger con affinità di thread non necessaria- [#9288](https://github.com/NuGet/Home/issues/9288)</span><span class="sxs-lookup"><span data-stu-id="848fc-134">Perf: RestoreOperationLogger has unnecessary thread affinity - [#9288](https://github.com/NuGet/Home/issues/9288)</span></span>

* <span data-ttu-id="848fc-135">Creazione automatica di documenti per i `dotnet nuget` comandi- [#9146](https://github.com/NuGet/Home/issues/9146)</span><span class="sxs-lookup"><span data-stu-id="848fc-135">Automated creation of docs for `dotnet nuget` commands - [#9146](https://github.com/NuGet/Home/issues/9146)</span></span>

* <span data-ttu-id="848fc-136">Il livello di dettaglio predefinito non deve segnalare il ripristino NOOP di ogni progetto- [#8792](https://github.com/NuGet/Home/issues/8792)</span><span class="sxs-lookup"><span data-stu-id="848fc-136">Default verbosity should not report each project's noop restore - [#8792](https://github.com/NuGet/Home/issues/8792)</span></span>

* <span data-ttu-id="848fc-137">`-DependencyVersion`Parametro di supporto per `NuGet.exe update` , simile a install command- [#7694](https://github.com/NuGet/Home/issues/7694)</span><span class="sxs-lookup"><span data-stu-id="848fc-137">Support `-DependencyVersion` parameter for `NuGet.exe update`, similar to install command - [#7694](https://github.com/NuGet/Home/issues/7694)</span></span>


<span data-ttu-id="848fc-138">**DCR**</span><span class="sxs-lookup"><span data-stu-id="848fc-138">**DCRs:**</span></span>

* <span data-ttu-id="848fc-139">Aggiungere il supporto iniziale per il Framework di destinazione NET 5.0- [#9584](https://github.com/NuGet/Home/issues/9584)</span><span class="sxs-lookup"><span data-stu-id="848fc-139">Add initial support for net5.0 target framework - [#9584](https://github.com/NuGet/Home/issues/9584)</span></span>

* <span data-ttu-id="848fc-140">Ordinare i pacchetti in base all'ID nella scheda aggiornamenti dell'interfaccia utente di PM- [#9278](https://github.com/NuGet/Home/issues/9278)</span><span class="sxs-lookup"><span data-stu-id="848fc-140">Sort packages by ID in the Updates tab of the PM UI - [#9278](https://github.com/NuGet/Home/issues/9278)</span></span>


<span data-ttu-id="848fc-141">**[Elenco di tutti i problemi risolti in questa versione-5,6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span><span class="sxs-lookup"><span data-stu-id="848fc-141">**[List of all issues fixed in this release - 5.6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span></span>
