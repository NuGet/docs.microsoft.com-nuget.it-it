---
title: Note sulla versione di NuGet 5,5
description: Note sulla versione per NuGet 5,5, incluse nuove funzionalità, correzioni di bug e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0fde67dd03c31e986ed89f2f8627608e279ef908
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780106"
---
# <a name="nuget-55-release-notes"></a><span data-ttu-id="b4324-103">Note sulla versione di NuGet 5,5</span><span class="sxs-lookup"><span data-stu-id="b4324-103">NuGet 5.5 Release Notes</span></span>

<span data-ttu-id="b4324-104">Veicoli per la distribuzione di NuGet:</span><span class="sxs-lookup"><span data-stu-id="b4324-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="b4324-105">Versione di NuGet</span><span class="sxs-lookup"><span data-stu-id="b4324-105">NuGet version</span></span> | <span data-ttu-id="b4324-106">Disponibile nella versione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b4324-106">Available in Visual Studio version</span></span>| <span data-ttu-id="b4324-107">Disponibile in .NET SDK</span><span class="sxs-lookup"><span data-stu-id="b4324-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="b4324-108">**5.5.0**</span><span class="sxs-lookup"><span data-stu-id="b4324-108">**5.5.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="b4324-109">Visual Studio 2019 versione 16,5</span><span class="sxs-lookup"><span data-stu-id="b4324-109">Visual Studio 2019 version 16.5</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="b4324-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="b4324-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="b4324-111"><sup>1</sup> Installato con Visual Studio 2019 con carico di lavoro di .NET Core</span><span class="sxs-lookup"><span data-stu-id="b4324-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-55"></a><span data-ttu-id="b4324-112">Riepilogo: novità di 5,5</span><span class="sxs-lookup"><span data-stu-id="b4324-112">Summary: What's New in 5.5</span></span>

* <span data-ttu-id="b4324-113">Esperienza migliorata per l'accessibilità e la lettura dello schermo per l'interfaccia utente di gestione pacchetti NuGet in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b4324-113">Improved accessibility and screen reader experience for the NuGet package manager UI in Visual Studio</span></span>
    * <span data-ttu-id="b4324-114">Problemi di accessibilità nelle esperienze di lettura schermo, altText mancanti e nome accessibile per la casella di testo installata e così via,- [#9059](https://github.com/NuGet/Home/issues/9059)</span><span class="sxs-lookup"><span data-stu-id="b4324-114">Accessibility issues in Screen Reader experiences, missing altText and accessible name for Installed textbox, etc., - [#9059](https://github.com/NuGet/Home/issues/9059)</span></span>
    * <span data-ttu-id="b4324-115">Problemi di accessibilità nelle esperienze di lettura schermo nell'elenco dei pacchetti- [#9077](https://github.com/NuGet/Home/issues/9077)</span><span class="sxs-lookup"><span data-stu-id="b4324-115">Accessibility issues in Screen Reader experiences in Packages List - [#9077](https://github.com/NuGet/Home/issues/9077)</span></span>
    * <span data-ttu-id="b4324-116">Problemi di accessibilità nelle esperienze di lettura schermo correlate alle schede "Sfoglia", "Install", "Update"- [#9078](https://github.com/NuGet/Home/issues/9078)</span><span class="sxs-lookup"><span data-stu-id="b4324-116">Accessibility issues in Screen Reader experiences related to "browse","install","update" Tabs - [#9078](https://github.com/NuGet/Home/issues/9078)</span></span>
    * <span data-ttu-id="b4324-117">Assistente vocale non annuncia l'etichetta di collegamento "blank", "No dependencies", "NuGet. org", "MIT" [#9157](https://github.com/NuGet/Home/issues/9157)</span><span class="sxs-lookup"><span data-stu-id="b4324-117">Narrator does not announce "Blank","No Dependencies","nuget.org","MIT" link label [#9157](https://github.com/NuGet/Home/issues/9157)</span></span>

* <span data-ttu-id="b4324-118">Supporto per la visualizzazione di icone autosufficienti nell'interfaccia utente di gestione pacchetti di Visual Studio per i pacchetti ospitati nei feed locali- [#8189](https://github.com/NuGet/Home/issues/8189)</span><span class="sxs-lookup"><span data-stu-id="b4324-118">Support for surfacing self-contained icons in Visual Studio package manager UI for packages hosted on local feeds - [#8189](https://github.com/NuGet/Home/issues/8189)</span></span>

* <span data-ttu-id="b4324-119">Miglioramento significativo delle prestazioni di ripristino senza op mediante `RestoreUseStaticGraphEvaluation` la quale è possibile velocizzare le valutazioni chiamando API Graph statiche di MSBuild- [8791](https://github.com/NuGet/Home/issues/8791)</span><span class="sxs-lookup"><span data-stu-id="b4324-119">Significantly improved no-op restore performance using `RestoreUseStaticGraphEvaluation` which speeds up evaluations by calling MSBuild Static Graph APIs - [8791](https://github.com/NuGet/Home/issues/8791)</span></span>

* <span data-ttu-id="b4324-120">Miglioramento dell'affidabilità dotnet.exe con i plug-in di autenticazione multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="b4324-120">Improved dotnet.exe reliability with cross-platform authentication plugins</span></span>
    * <span data-ttu-id="b4324-121">dotnet restore non riuscito con TaskCanceledException- [#7842](https://github.com/NuGet/Home/issues/7842)</span><span class="sxs-lookup"><span data-stu-id="b4324-121">dotnet restore failing with TaskCanceledException - [#7842](https://github.com/NuGet/Home/issues/7842)</span></span>
    * <span data-ttu-id="b4324-122">Plug-in: "un'attività è stata annullata". problema con l'autenticazione ADO a causa di questo.</span><span class="sxs-lookup"><span data-stu-id="b4324-122">Plugin:  "A task was cancelled" - problem with ADO authentication due to this.</span></span><span data-ttu-id="b4324-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span><span class="sxs-lookup"><span data-stu-id="b4324-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span></span>

* <span data-ttu-id="b4324-124">Aggiungi `dotnet nuget <add|remove|update|disable|enable|list> source` [#4126](https://github.com/NuGet/Home/issues/4126) comando</span><span class="sxs-lookup"><span data-stu-id="b4324-124">add `dotnet nuget <add|remove|update|disable|enable|list> source` command - [#4126](https://github.com/NuGet/Home/issues/4126)</span></span>

* <span data-ttu-id="b4324-125">Eseguire il `--skip-duplicate`  push per l'uso di DotNet NuGet push- [#8778](https://github.com/NuGet/Home/issues/8778)</span><span class="sxs-lookup"><span data-stu-id="b4324-125">Suport for `--skip-duplicate`  using dotnet nuget push - [#8778](https://github.com/NuGet/Home/issues/8778)</span></span>

* <span data-ttu-id="b4324-126">Supporto `packages.config` con MSBuild/Restore- [#8506](https://github.com/NuGet/Home/issues/8506)</span><span class="sxs-lookup"><span data-stu-id="b4324-126">Support `packages.config` with msbuild /restore - [#8506](https://github.com/NuGet/Home/issues/8506)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="b4324-127">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="b4324-127">Issues fixed in this release</span></span>

<span data-ttu-id="b4324-128">**Bug**</span><span class="sxs-lookup"><span data-stu-id="b4324-128">**Bugs**</span></span>

* <span data-ttu-id="b4324-129">Rielaborare Self-Updater con le API V3- [#4197](https://github.com/NuGet/Home/issues/4197)</span><span class="sxs-lookup"><span data-stu-id="b4324-129">Rework Self-Updater with V3 Apis - [#4197](https://github.com/NuGet/Home/issues/4197)</span></span>

* <span data-ttu-id="b4324-130">Versione di dipendenza del pacchetto errata se la versione della dipendenza del pacchetto è impostata su' \*'- [#6697](https://github.com/NuGet/Home/issues/6697)</span><span class="sxs-lookup"><span data-stu-id="b4324-130">Wrong package dependency version If package dependency version is set to '\*' - [#6697](https://github.com/NuGet/Home/issues/6697)</span></span>

* <span data-ttu-id="b4324-131">Il messaggio di errore ErrorUnsafePackageEntry non punta all'origine del problema [#7505](https://github.com/NuGet/Home/issues/7505)</span><span class="sxs-lookup"><span data-stu-id="b4324-131">ErrorUnsafePackageEntry error message is not pointing to source of problem - [#7505](https://github.com/NuGet/Home/issues/7505)</span></span>

* <span data-ttu-id="b4324-132">Il file di blocco non è rispettato negli scenari "\*": [#8073](https://github.com/NuGet/Home/issues/8073)</span><span class="sxs-lookup"><span data-stu-id="b4324-132">Lock file is not honored in "\*" scenarios  - [#8073](https://github.com/NuGet/Home/issues/8073)</span></span>

* <span data-ttu-id="b4324-133">NuGet.exe non si risolve nella versione più recente di un pacchetto quando si usa \* in PackageReference (MSBuild/DotNet/VS Restore do)- [#8432](https://github.com/NuGet/Home/issues/8432)</span><span class="sxs-lookup"><span data-stu-id="b4324-133">NuGet.exe does not resolve to the latest version of a package when using \* in PackageReference (MSBuild/Dotnet/VS restore do) - [#8432](https://github.com/NuGet/Home/issues/8432)</span></span>

* <span data-ttu-id="b4324-134">pacchetto di elenco DotNet con il progetto WPF con più destinazioni- [#8463](https://github.com/NuGet/Home/issues/8463)</span><span class="sxs-lookup"><span data-stu-id="b4324-134">dotnet list package with multi targeting WPF project - [#8463](https://github.com/NuGet/Home/issues/8463)</span></span>

* <span data-ttu-id="b4324-135">Migliorare ConcurrencyUtilities (ridurre l'utilizzo della CPU)- [#8653](https://github.com/NuGet/Home/issues/8653)</span><span class="sxs-lookup"><span data-stu-id="b4324-135">Improve ConcurrencyUtilities (reduce CPU usage) - [#8653](https://github.com/NuGet/Home/issues/8653)</span></span>

* <span data-ttu-id="b4324-136">Le specifiche DG per gli scenari di progetto scaricati non devono essere scritte nei ripristini di anteprima [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="b4324-136">DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="b4324-137">I pacchetti NuGet di Visual Studio (RestoreManagerPackage) devono essere caricati automaticamente sugli eventi di compilazione della soluzione- [#8796](https://github.com/NuGet/Home/issues/8796)</span><span class="sxs-lookup"><span data-stu-id="b4324-137">The Visual Studio NuGet packages (RestoreManagerPackage) needs to auto load on solution build events - [#8796](https://github.com/NuGet/Home/issues/8796)</span></span>

* <span data-ttu-id="b4324-138">Deadlock in VSSettings init- [#8842](https://github.com/NuGet/Home/issues/8842)</span><span class="sxs-lookup"><span data-stu-id="b4324-138">Deadlock in VSSettings init - [#8842](https://github.com/NuGet/Home/issues/8842)</span></span>

* <span data-ttu-id="b4324-139">La casella degli strumenti VisualStudio non viene popolata da un pacchetto NuGet se un progetto viene inserito in una cartella della soluzione [#8868](https://github.com/NuGet/Home/issues/8868)</span><span class="sxs-lookup"><span data-stu-id="b4324-139">VisualStudio ToolBox is not populated from a NuGet package if a project is placed in a solution folder - [#8868](https://github.com/NuGet/Home/issues/8868)</span></span>

* <span data-ttu-id="b4324-140">Visual Studio: il ripristino della soluzione ha esito negativo a causa della [#8881](https://github.com/NuGet/Home/issues/8881) race condition</span><span class="sxs-lookup"><span data-stu-id="b4324-140">VS:  solution restore perpetually fails due to race condition - [#8881](https://github.com/NuGet/Home/issues/8881)</span></span>

* <span data-ttu-id="b4324-141">Costante "Loading.." nella scheda installata e "ricerca</span><span class="sxs-lookup"><span data-stu-id="b4324-141">Constant "loading.." on installed tab, and "searching</span></span> <term><span data-ttu-id="b4324-142">.. "nella scheda aggiornamenti- [#8890](https://github.com/NuGet/Home/issues/8890)</span><span class="sxs-lookup"><span data-stu-id="b4324-142">.." on updates tab - [#8890](https://github.com/NuGet/Home/issues/8890)</span></span>

* <span data-ttu-id="b4324-143">Icone incorporate mancanti nell'interfaccia utente di Visual Studio dopo la scadenza della cache- [#9069](https://github.com/NuGet/Home/issues/9069)</span><span class="sxs-lookup"><span data-stu-id="b4324-143">Missing Embedded Icons in VS PM UI after cache expires - [#9069](https://github.com/NuGet/Home/issues/9069)</span></span>

* <span data-ttu-id="b4324-144">Avvio interfaccia utente FireAndForget- [#9112](https://github.com/NuGet/Home/issues/9112)</span><span class="sxs-lookup"><span data-stu-id="b4324-144">FireAndForget PM UI startup - [#9112](https://github.com/NuGet/Home/issues/9112)</span></span>

* <span data-ttu-id="b4324-145">Restore: l'implementazione di IncludeExcludeFiles. Equals (...) non è corretta- [#9167](https://github.com/NuGet/Home/issues/9167)</span><span class="sxs-lookup"><span data-stu-id="b4324-145">Restore: IncludeExcludeFiles.Equals(...) implementation is incorrect - [#9167](https://github.com/NuGet/Home/issues/9167)</span></span>

* <span data-ttu-id="b4324-146">Restore: PackageSpec. Clone () crea un clone diverso- [#9211](https://github.com/NuGet/Home/issues/9211)</span><span class="sxs-lookup"><span data-stu-id="b4324-146">Restore: PackageSpec.Clone() creates unequal clone - [#9211](https://github.com/NuGet/Home/issues/9211)</span></span>

* <span data-ttu-id="b4324-147">Elenco errori visualizzato anche se "Mostra sempre Elenco errori se la compilazione termina con errori" non è selezionata- [#8190](https://github.com/NuGet/Home/issues/8190)</span><span class="sxs-lookup"><span data-stu-id="b4324-147">Error list shown although "Always show Error List if build finishes with errors" is not checked - [#8190](https://github.com/NuGet/Home/issues/8190)</span></span>

* <span data-ttu-id="b4324-148">Il ripristino statico del grafo non deve superare SolutionPath- [#9061](https://github.com/NuGet/Home/issues/9061) vuoti</span><span class="sxs-lookup"><span data-stu-id="b4324-148">Static Graph restore should not pass empty SolutionPath - [#9061](https://github.com/NuGet/Home/issues/9061)</span></span>

* <span data-ttu-id="b4324-149">Ripristino: chiusura calcolata per ogni progetto 4 volte- [#9042](https://github.com/NuGet/Home/issues/9042)</span><span class="sxs-lookup"><span data-stu-id="b4324-149">Restore: closure computed for each project 4 times - [#9042](https://github.com/NuGet/Home/issues/9042)</span></span>

* <span data-ttu-id="b4324-150">Restore: DependencyGraphSpec. Load (...) non necessita di JObject- [#9040](https://github.com/NuGet/Home/issues/9040)</span><span class="sxs-lookup"><span data-stu-id="b4324-150">Restore: DependencyGraphSpec.Load(...) does not need JObject - [#9040](https://github.com/NuGet/Home/issues/9040)</span></span>

* <span data-ttu-id="b4324-151">Restore: stringhe di grandi dimensioni create nell'heap degli oggetti grandi (LOH)- [#9031](https://github.com/NuGet/Home/issues/9031)</span><span class="sxs-lookup"><span data-stu-id="b4324-151">Restore: large strings created on large object heap (LOH) - [#9031](https://github.com/NuGet/Home/issues/9031)</span></span>

* <span data-ttu-id="b4324-152">nuget.exe personalizzati sul mono più recente potrebbero interrompersi a causa del sistema di risoluzione dell'SDK di MSBuild- [8848](https://github.com/NuGet/Home/issues/8848)</span><span class="sxs-lookup"><span data-stu-id="b4324-152">Custom nuget.exe on newer mono might break due to the MSBuild SDK Resolver - [8848](https://github.com/NuGet/Home/issues/8848)</span></span>

* <span data-ttu-id="b4324-153">il ripristino non riesce quando nuget.dgspec.jssu è "usato da un altro processo"- [8692](https://github.com/NuGet/Home/issues/8692)</span><span class="sxs-lookup"><span data-stu-id="b4324-153">restore fails when nuget.dgspec.json is "used by another process" - [8692](https://github.com/NuGet/Home/issues/8692)</span></span>

<span data-ttu-id="b4324-154">**DCR**</span><span class="sxs-lookup"><span data-stu-id="b4324-154">**DCRs**</span></span>

* <span data-ttu-id="b4324-155">La logica in _GetRestoreProjectStyle deve trovarsi in un'attività- [#8804](https://github.com/NuGet/Home/issues/8804)</span><span class="sxs-lookup"><span data-stu-id="b4324-155">Logic in _GetRestoreProjectStyle should be in a task - [#8804](https://github.com/NuGet/Home/issues/8804)</span></span>

* <span data-ttu-id="b4324-156">Aggiungere le informazioni di deprecazione per impostazione predefinita nella scheda installato- [#8541](https://github.com/NuGet/Home/issues/8541)</span><span class="sxs-lookup"><span data-stu-id="b4324-156">Add deprecation information by default on the installed tab - [#8541](https://github.com/NuGet/Home/issues/8541)</span></span>

<span data-ttu-id="b4324-157">**[Elenco di tutti i problemi risolti in questa versione-5,5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span><span class="sxs-lookup"><span data-stu-id="b4324-157">**[List of all issues fixed in this release - 5.5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span></span>
