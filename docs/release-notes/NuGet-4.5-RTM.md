---
title: Note sulla versione per NuGet 4.5 RTM
description: Note sulla versione per NuGet 4.5 RTM incluse informazioni su problemi noti, correzioni di bug e DCR.
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 321aedb471bc6f86e9c03878093b199267e31195
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432504"
---
# <a name="nuget-45-release-notes"></a><span data-ttu-id="91752-103">Note sulla versione per NuGet 4.5</span><span class="sxs-lookup"><span data-stu-id="91752-103">NuGet 4.5 Release Notes</span></span>

<span data-ttu-id="91752-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) include [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="91752-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-450"></a><span data-ttu-id="91752-105">Riepilogo: Novità nella versione 4.5.0</span><span class="sxs-lookup"><span data-stu-id="91752-105">Summary: What's New in 4.5.0</span></span>

## <a name="summary-whats-new-in-452"></a><span data-ttu-id="91752-106">Riepilogo: Novità nella versione 4.5.2</span><span class="sxs-lookup"><span data-stu-id="91752-106">Summary: What's New in 4.5.2</span></span>

* <span data-ttu-id="91752-107">Correzione della sicurezza: le autorizzazioni per i file creati all'interno di ~/.nuget sono troppo aperte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="91752-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-453"></a><span data-ttu-id="91752-108">Riepilogo: Novità nella versione 4.5.3</span><span class="sxs-lookup"><span data-stu-id="91752-108">Summary: What's New in 4.5.3</span></span>

* <span data-ttu-id="91752-109">Correzione della sicurezza: i file all'interno di pacchetti NuGet possono avere un percorso relativo sopra la directory NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="91752-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="91752-110">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="91752-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="91752-111">Problemi relativi a .NET 2.0 Standard con .NET Framework e NuGet</span><span class="sxs-lookup"><span data-stu-id="91752-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="91752-112">.NET Standard e i relativi strumenti sono stati progettati in modo che i progetti destinati a .NET Framework 4.6.1 possano utilizzare pacchetti e progetti NuGet destinati a .NET Standard 2.0 o versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="91752-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="91752-113">[Questo documento](https://github.com/dotnet/standard/issues/481) riepiloga i problemi relativi a questo scenario, i piani per risolverli e le soluzioni alternative implementabili allo stato attuale degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="91752-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="91752-114">Non è possibile visualizzare, aggiungere o aggiornare DotNetCLITools usando Gestione pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="91752-114">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="91752-115">Problema</span><span class="sxs-lookup"><span data-stu-id="91752-115">Issue</span></span>

<span data-ttu-id="91752-116">Gestione pacchetti NuGet non visualizza e non consente l'aggiunta e/o l'aggiornamento di DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="91752-116">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="91752-117">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="91752-117">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="91752-118">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="91752-118">Workaround</span></span>

<span data-ttu-id="91752-119">È necessario modificare manualmente DotNetCLIToolReferences nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="91752-119">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="91752-120">La ridestinazione della versione framework di destinazione può portare a informazioni Intellisense incomplete</span><span class="sxs-lookup"><span data-stu-id="91752-120">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="91752-121">Problema</span><span class="sxs-lookup"><span data-stu-id="91752-121">Issue</span></span>

<span data-ttu-id="91752-122">Se in Visual Studio si ridefinisce la destinazione della versione framework di destinazione, le informazioni Intellisense possono risultare incomplete.</span><span class="sxs-lookup"><span data-stu-id="91752-122">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="91752-123">Questo accade quando si usa PackageReferences come formato di gestione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="91752-123">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="91752-124">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="91752-124">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="91752-125">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="91752-125">Workaround</span></span>

<span data-ttu-id="91752-126">Eseguire un ripristino manuale.</span><span class="sxs-lookup"><span data-stu-id="91752-126">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="91752-127">Un pacchetto in un progetto .NET Core contenente un assembly con una firma non valida, può causare un ciclo infinito di ripristino</span><span class="sxs-lookup"><span data-stu-id="91752-127">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="91752-128">Problema</span><span class="sxs-lookup"><span data-stu-id="91752-128">Issue</span></span>

<span data-ttu-id="91752-129">A volte, quando si usa un pacchetto contenente un assembly con una firma non valida o quando la versione del pacchetto è impostata con tick 'DateTime', è possibile che il processo di ripristino automatico del pacchetto entri in un ciclo infinito [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span><span class="sxs-lookup"><span data-stu-id="91752-129">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="91752-130">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="91752-130">Workaround</span></span>

<span data-ttu-id="91752-131">Attualmente non esiste alcuna soluzione.</span><span class="sxs-lookup"><span data-stu-id="91752-131">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="91752-132">Problemi risolti nell'intervallo di tempo NuGet 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="91752-132">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="91752-133">Per i problemi risolti in NuGet 4.4 RTM, vedere le [Note sulla versione per NuGet 4.4 RTM](../release-notes/nuget-4.4-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="91752-133">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="91752-134">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="91752-134">Features</span></span>

- <span data-ttu-id="91752-135">Disabilitare il push automatico del pacchetto di simboli - [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="91752-135">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="91752-136">Bug</span><span class="sxs-lookup"><span data-stu-id="91752-136">Bugs</span></span>

- <span data-ttu-id="91752-137">[Regressione] in 15.5p1: Portable0.0 viene ignorato - [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="91752-137">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="91752-138">Asset dai pacchetti mancanti dopo il ripristino - [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="91752-138">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="91752-139">I provider di credenziali plug-in non funzionano con gli URI contenenti spazi - [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="91752-139">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="91752-140">Se il ripristino del pacchetto non riesce, l'errore deve comparire nell'output anche quando è attivo il livello di dettaglio minimo - [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="91752-140">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="91752-141">dotnet</span><span class="sxs-lookup"><span data-stu-id="91752-141">dotnet</span></span>
  - <span data-ttu-id="91752-142">dotnetcore restore a livello di soluzione non segue ProjectReference con ReferenceOutputAssembly impostato su false, con conseguenti errori di compilazione casuali - [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="91752-142">dotnetcore restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="91752-143">Il completamento automatico nella console di Gestione pacchetti non funziona correttamente con i metodi di oggetto - [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="91752-143">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="91752-144">Il ripristino di nuget.exe non funziona con il set di strumenti di Visual Studio 2015 - [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="91752-144">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="91752-145">Prestazioni: la creazione di istanze della console di Gestione pacchetti è onerosa in VS2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="91752-145">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="91752-146">Recupero di informazioni sulle dipendenze lento su connessione lenta - [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="91752-146">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="91752-147">uninstall-package con -RemoveDependencies avrà esito negativo se più pacchetti condividono una dipendenza in comune - [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="91752-147">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="91752-148">Finalizzare NuGet.Core.nupkg per la pubblicazione - [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="91752-148">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="91752-149">NuGet pack risolve l'ID di dipendenza dal nome di directory quando si usa -IncludeProjectReferences per csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="91752-149">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="91752-150">L'inizializzatore di tipo per 'NuGet.ProxyCache' ha generato un'eccezione - [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="91752-150">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="91752-151">Problema di prestazioni di nuget restore con kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="91752-151">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="91752-152">Il client dell'interfaccia utente non visualizza errori o avvisi quando la ricerca non è sincronizzata con i BLOB di registrazione - [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="91752-152">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="91752-153">Get-Packages-Updates genera una query non corretta - [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="91752-153">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="91752-154">Collegamenti ai problemi di GitHub risolti nella versione 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="91752-154">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="91752-155">Elenco dei problemi</span><span class="sxs-lookup"><span data-stu-id="91752-155">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
