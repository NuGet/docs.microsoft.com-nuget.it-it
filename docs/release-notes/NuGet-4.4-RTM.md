---
title: Note sulla versione per NuGet 4.4 RTM
description: Note sulla versione per NuGet 4.4 RTM, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e controller di dominio.
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 980afffcd4202e019ffa87de5dccf947300a9c13
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901707"
---
# <a name="nuget-44-release-notes"></a><span data-ttu-id="e63ef-103">Note sulla versione per NuGet 4.4</span><span class="sxs-lookup"><span data-stu-id="e63ef-103">NuGet 4.4 Release Notes</span></span>

<span data-ttu-id="e63ef-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) include NuGet 4.4 RTM.</span><span class="sxs-lookup"><span data-stu-id="e63ef-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="summary-whats-new-in-440"></a><span data-ttu-id="e63ef-105">Riepilogo: Novità nella versione 4.4.0</span><span class="sxs-lookup"><span data-stu-id="e63ef-105">Summary: What's New in 4.4.0</span></span>

## <a name="summary-whats-new-in-442"></a><span data-ttu-id="e63ef-106">Riepilogo: Novità nella versione 4.4.2</span><span class="sxs-lookup"><span data-stu-id="e63ef-106">Summary: What's New in 4.4.2</span></span>

* <span data-ttu-id="e63ef-107">Correzione della sicurezza: Le autorizzazioni per i file creati all'interno di ~/.nuget sono troppo [aperte](https://github.com/NuGet/Home/issues/7673) #7673 [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="e63ef-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-443"></a><span data-ttu-id="e63ef-108">Riepilogo: Novità nella versione 4.4.3</span><span class="sxs-lookup"><span data-stu-id="e63ef-108">Summary: What's New in 4.4.3</span></span>

* <span data-ttu-id="e63ef-109">Correzione della sicurezza: i file all'interno dei gruppi di sicurezza di rete possono avere un percorso relativo sopra la directory NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="e63ef-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="e63ef-110">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="e63ef-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="e63ef-111">Problemi relativi a .NET 2.0 Standard con .NET Framework e NuGet</span><span class="sxs-lookup"><span data-stu-id="e63ef-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="e63ef-112">.NET Standard e i relativi strumenti sono stati progettati in modo che i progetti destinati a .NET Framework 4.6.1 possano utilizzare pacchetti e progetti NuGet destinati a .NET Standard 2.0 o versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="e63ef-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="e63ef-113">[Questo documento](https://github.com/dotnet/standard/issues/481) riepiloga i problemi relativi a questo scenario, i piani per risolverli e le soluzioni alternative implementabili allo stato attuale degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="e63ef-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="e63ef-114">Durante l'uso della console di Gestione pacchetti è possibile che il tasto 'INVIO' non funzioni</span><span class="sxs-lookup"><span data-stu-id="e63ef-114">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="e63ef-115">Problema</span><span class="sxs-lookup"><span data-stu-id="e63ef-115">Issue</span></span>

<span data-ttu-id="e63ef-116">A volte, nella console di Gestione pacchetti il tasto INVIO non funziona.</span><span class="sxs-lookup"><span data-stu-id="e63ef-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="e63ef-117">Se si riscontra questo problema, controllare lo stato di avanzamento della correzione e fornire altre informazioni utili sui passaggi per riprodurre la condizione di errore.</span><span class="sxs-lookup"><span data-stu-id="e63ef-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="e63ef-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="e63ef-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="e63ef-119">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="e63ef-119">Workaround</span></span>

<span data-ttu-id="e63ef-120">Riavviare Visual Studio e aprire la console di Gestione pacchetti prima di aprire la soluzione.</span><span class="sxs-lookup"><span data-stu-id="e63ef-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="e63ef-121">In alternativa, provare a eliminare `project.lock.json` e ripetere il ripristino.</span><span class="sxs-lookup"><span data-stu-id="e63ef-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="e63ef-122">Non è possibile visualizzare, aggiungere o aggiornare DotNetCLITools usando Gestione pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="e63ef-122">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="e63ef-123">Problema</span><span class="sxs-lookup"><span data-stu-id="e63ef-123">Issue</span></span>

<span data-ttu-id="e63ef-124">Gestione pacchetti NuGet non visualizza e non consente l'aggiunta e/o l'aggiornamento di DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="e63ef-124">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="e63ef-125">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="e63ef-125">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="e63ef-126">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="e63ef-126">Workaround</span></span>

<span data-ttu-id="e63ef-127">È necessario modificare manualmente DotNetCLIToolReferences nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="e63ef-127">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="e63ef-128">La ridestinazione della versione framework di destinazione può portare a informazioni Intellisense incomplete</span><span class="sxs-lookup"><span data-stu-id="e63ef-128">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="e63ef-129">Problema</span><span class="sxs-lookup"><span data-stu-id="e63ef-129">Issue</span></span>

<span data-ttu-id="e63ef-130">Se in Visual Studio si ridefinisce la destinazione della versione framework di destinazione, le informazioni Intellisense possono risultare incomplete.</span><span class="sxs-lookup"><span data-stu-id="e63ef-130">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="e63ef-131">Questo accade quando si usa PackageReferences come formato di gestione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="e63ef-131">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="e63ef-132">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="e63ef-132">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="e63ef-133">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="e63ef-133">Workaround</span></span>

<span data-ttu-id="e63ef-134">Eseguire un ripristino manuale.</span><span class="sxs-lookup"><span data-stu-id="e63ef-134">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="e63ef-135">Un pacchetto in un progetto .NET Core contenente un assembly con una firma non valida, può causare un ciclo infinito di ripristino</span><span class="sxs-lookup"><span data-stu-id="e63ef-135">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="e63ef-136">Problema</span><span class="sxs-lookup"><span data-stu-id="e63ef-136">Issue</span></span>

<span data-ttu-id="e63ef-137">A volte, quando si usa un pacchetto contenente un assembly con una firma non valida o quando la versione del pacchetto è impostata con tick 'DateTime', è possibile che il processo di ripristino automatico del pacchetto entri in un ciclo infinito (dotnet/project-system#1457).</span><span class="sxs-lookup"><span data-stu-id="e63ef-137">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="e63ef-138">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="e63ef-138">Workaround</span></span>

<span data-ttu-id="e63ef-139">Al momento non sono disponibili soluzioni alternative.</span><span class="sxs-lookup"><span data-stu-id="e63ef-139">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="e63ef-140">Problemi risolti nell'intervallo di tempo NuGet 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="e63ef-140">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="e63ef-141">[Note sulla versione per NuGet 4.3 RTM](../release-notes/nuget-4.3-RTM.md) - Vengono elencati tutti i problemi risolti per NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="e63ef-141">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="e63ef-142">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="e63ef-142">Features</span></span>

- <span data-ttu-id="e63ef-143">Supporto per il caricamento leggero delle soluzioni nella console di Gestione pacchetti e nell'interfaccia utente di Gestione pacchetti NuGet - [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="e63ef-143">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="e63ef-144">La destinazione pack di MSBuild deve avere un hook pubblico per l'esecuzione delle destinazioni dell'utente prima di se stessa - [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="e63ef-144">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="e63ef-145">Funzionalità: Aggiunta dell'opzione dependencyVersion al comando nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="e63ef-145">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="e63ef-146">uap10.0.TODO.0 deve essere mappato a .NET Standard 2.0 per NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="e63ef-146">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="e63ef-147">Supporto di Visual Studio Build Tools SKU con msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="e63ef-147">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="e63ef-148">Durante il ripristino viene generato un errore se il supporto di .NET 4.6.1 il per .NET Standard 2.0 è richiesto ma non è installato - [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="e63ef-148">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="e63ef-149">Interfaccia utente client per la prenotazione del prefisso dell'ID del pacchetto [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="e63ef-149">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="e63ef-150">Distribuire componenti NuGet localizzati per supportare la localizzazione di dotnet.exe - [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="e63ef-150">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="e63ef-151">Bug</span><span class="sxs-lookup"><span data-stu-id="e63ef-151">Bugs</span></span>

- <span data-ttu-id="e63ef-152">Combinazioni di maiuscole/minuscole diverse nel percorso del progetto possono causare la perdita di riferimenti PackageReference durante il ripristino - [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="e63ef-152">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="e63ef-153">Spostare i codici di errore con numeri di avviso nell'intervallo degli errori - [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="e63ef-153">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="e63ef-154">Errore fuorviante quando la versione di .NET Standard non è notoriamente compatibile con il framework di destinazione - [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="e63ef-154">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="e63ef-155">File di test con testo di licenza confuso: [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="e63ef-155">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="e63ef-156">Intestazioni di licenza mancanti in modelli di test EndToEnd - [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="e63ef-156">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="e63ef-157">Per il ripristino di packages.config gli errori vengono visualizzati come NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="e63ef-157">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="e63ef-158">Per nuget.exe install è necessario DisableParallelProcessing su Mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="e63ef-158">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="e63ef-159">nuget.exe install disabilita in modo non corretto la memorizzazione nella cache - [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="e63ef-159">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="e63ef-160">VS: quando si esegue il comando restore per packages.config quando il ripristino è disabilitato viene visualizzato un messaggio non corretto - [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="e63ef-160">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="e63ef-161">VS: quando si esegue il comando restore quando il ripristino è disabilitato viene visualizzato un messaggio confuso - [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="e63ef-161">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="e63ef-162">GetRestoreDotnetCliToolsTask non riesce quando mancano i metadati della versione - [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="e63ef-162">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="e63ef-163">dotnet</span><span class="sxs-lookup"><span data-stu-id="e63ef-163">dotnet</span></span>
  - <span data-ttu-id="e63ef-164">dotnetcore add package può cancellare le righe vuote da un csproj - [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="e63ef-164">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="e63ef-165">Per i nomi di origine delle impostazioni delle credenziali in NuGet.config viene fatta distinzione tra maiuscole e minuscole - [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="e63ef-165">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="e63ef-166">In seguito all'abilitazione di GeneratePackageOnBuild viene eliminata l'intera cronologia di pacchetti - [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="e63ef-166">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="e63ef-167">Il ripristino non consentirà di ripristinare i pacchetti mono.cecil o semver, ma tutti gli altri pacchetti vengono ripristinati.</span><span class="sxs-lookup"><span data-stu-id="e63ef-167">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="e63ef-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="e63ef-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="e63ef-169">Errori e avvisi - errore grave quando un'origine non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="e63ef-169">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="e63ef-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="e63ef-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="e63ef-171">[Coerenza della progettazione] Attualmente, il testo dello stato di installazione di NuGet non viene visualizzato in modo corretto con il tema scuro.</span><span class="sxs-lookup"><span data-stu-id="e63ef-171">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="e63ef-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="e63ef-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="e63ef-173">L'aggiornamento dei pacchetti a livello di soluzione esegue l'aggiornamento/installazione per tutti i progetti - [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="e63ef-173">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="e63ef-174">dotnet</span><span class="sxs-lookup"><span data-stu-id="e63ef-174">dotnet</span></span>
  - <span data-ttu-id="e63ef-175">dotnetcore pack si comporta diversamente con TargetFramework o TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="e63ef-175">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="e63ef-176">Le DLL incluse nella cartella Tools generano avvisi - [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="e63ef-176">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="e63ef-177">NuGet.ContentModel utilizza troppa memoria per le operazioni su stringhe - [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="e63ef-177">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="e63ef-178">RuntimeEnvironmentHelper.IsLinux restituisce true per OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="e63ef-178">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="e63ef-179">'dotnet pack' posiziona nuspec in obj invece che in obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="e63ef-179">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="e63ef-180">Nuget: aggiornamento dei pacchetti estremamente lento - [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="e63ef-180">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="e63ef-181">CPS non sincronizzato per il ripristino con soluzioni grandi senza il ripristino leggero delle soluzioni attivato - [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="e63ef-181">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="e63ef-182">SemVer 2.0 - nuget pack con la versione specificata ignora i metadati (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="e63ef-182">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="e63ef-183">Nuget.exe (3.+): l'installazione di un pacchetto con numero di versione e flag ExcludeVersion non aggiorna il pacchetto alla versione più recente - [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="e63ef-183">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="e63ef-184">Il ripristino di project.json dovrebbe generare un avviso quando i pacchetti di livello superiore violano i vincoli - [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="e63ef-184">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="e63ef-185">-ConfigFile non imposta la configurazione personalizzata per il comando install - [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="e63ef-185">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="e63ef-186">L'installazione di nuget.exe non rispetta l'opzione '-DisableParallelProcessing' - [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="e63ef-186">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="e63ef-187">Origini disabilitate usate comunque da DotNet.exe o msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="e63ef-187">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="e63ef-188">Correzione dei blocchi nello scenario di caricamento leggero delle soluzioni - [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="e63ef-188">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="e63ef-189">DCR</span><span class="sxs-lookup"><span data-stu-id="e63ef-189">DCRs</span></span>

- <span data-ttu-id="e63ef-190">Supporto di TargetFramework per nuget.exe install - [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="e63ef-190">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="e63ef-191">Aggiungere stringhe diverse per l'agente utente per l'attività MSBuild (.NET Core o Desktop) - [5709 #](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="e63ef-191">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="e63ef-192">PackagePathResolver.GetPackageDirectoryName deve essere virtuale - [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="e63ef-192">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="e63ef-193">[Coerenza della progettazione] Messaggio non chiaro durante l'aggiunta di un pacchetto NuGet - [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="e63ef-193">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="e63ef-194">[Avvisi ed errori] NoWarn non viene trasferito in modo transitivo attraverso riferimenti P2P - [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="e63ef-194">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="e63ef-195">Caricamento leggero delle soluzioni: core comune per interfaccia utente di Gestione pacchetti, console di Gestione pacchetti e interfacce IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="e63ef-195">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="e63ef-196">Caricamento leggero delle soluzioni: supporto - Console di Gestione pacchetti - [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="e63ef-196">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="e63ef-197">Aggiunta del supporto di una destinazione di MSBuild pre-ripristino attivata da Visual Studio - [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="e63ef-197">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="e63ef-198">Aggiunta di una destinazione pubblica a NuGet.targets a cui è possibile fare riferimento tramite BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="e63ef-198">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="e63ef-199">La destinazione Pack non consente di creare correttamente file di contenuto con le azioni di compilazione - [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="e63ef-199">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="e63ef-200">RestoreOperationLogger.Do blocca thread del pool di thread - [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="e63ef-200">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="e63ef-201">Docs</span><span class="sxs-lookup"><span data-stu-id="e63ef-201">Docs</span></span>

- <span data-ttu-id="e63ef-202">Documentazione per i flag DependencyVersion e Framework del comando Install - [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="e63ef-202">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="e63ef-203">Aggiornamento della documentazione per gli avvisi e gli errori NuGet - [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="e63ef-203">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="e63ef-204">Collegamenti ai problemi di GitHub risolti nella versione 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="e63ef-204">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="e63ef-205">Elenco di problemi 1</span><span class="sxs-lookup"><span data-stu-id="e63ef-205">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="e63ef-206">Elenco di problemi 2</span><span class="sxs-lookup"><span data-stu-id="e63ef-206">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="e63ef-207">Elenco di problemi 3</span><span class="sxs-lookup"><span data-stu-id="e63ef-207">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
