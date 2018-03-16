---
title: Note sulla versione per NuGet 4.0 RC | Microsoft Docs
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Note sulla versione per NuGet 4.0 RTM incluse informazioni su problemi noti, correzioni di bug e DCR.
keywords: "Note sulla versione per NuGet 4.0 RTM, correzioni di bug, problemi noti, funzionalità aggiunte, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d1ab89f0decb64a64d04dc293e5273b577e8398b
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-40-rtm-release-notes"></a><span data-ttu-id="3375b-104">Note sulla versione per NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="3375b-104">NuGet 4.0 RTM Release Notes</span></span>

<span data-ttu-id="3375b-105">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) include NuGet 4.0, che aggiunge il supporto per .NET Core, oltre a varie correzioni per la qualità e miglioramenti delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="3375b-105">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="3375b-106">Questa versione offre anche diversi miglioramenti come il supporto di PackageReference, i comandi NuGet come destinazioni di MSBuild, il ripristino dei pacchetti in background e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="3375b-106">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="3375b-107">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="3375b-107">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="3375b-108">Il ripristino di NuGet può avere esito negativo quando in una soluzione sono presenti più progetti che fanno riferimento a un altro progetto</span><span class="sxs-lookup"><span data-stu-id="3375b-108">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="3375b-109">Problema</span><span class="sxs-lookup"><span data-stu-id="3375b-109">Issue</span></span>

<span data-ttu-id="3375b-110">Il ripristino di NuGet può avere esito negativo se, in una soluzione, sono presenti riferimenti allo stesso progetto con una diversa combinazione di maiuscole e minuscole o con percorsi relativi differenti.</span><span class="sxs-lookup"><span data-stu-id="3375b-110">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="3375b-111">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="3375b-111">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="3375b-112">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="3375b-112">Workaround</span></span>

<span data-ttu-id="3375b-113">Correggere la combinazione di maiuscole e minuscole o i percorsi relativi in modo che siano identici per tutti i riferimenti al progetto.</span><span class="sxs-lookup"><span data-stu-id="3375b-113">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="3375b-114">Durante l'uso della console di Gestione pacchetti è possibile che il tasto 'INVIO' non funzioni</span><span class="sxs-lookup"><span data-stu-id="3375b-114">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="3375b-115">Problema</span><span class="sxs-lookup"><span data-stu-id="3375b-115">Issue</span></span>

<span data-ttu-id="3375b-116">A volte, nella console di Gestione pacchetti il tasto INVIO non funziona.</span><span class="sxs-lookup"><span data-stu-id="3375b-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="3375b-117">Se si riscontra questo problema, controllare lo stato di avanzamento della correzione e fornire altre informazioni utili sui passaggi per riprodurre la condizione di errore.</span><span class="sxs-lookup"><span data-stu-id="3375b-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="3375b-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="3375b-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="3375b-119">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="3375b-119">Workaround</span></span>

<span data-ttu-id="3375b-120">Riavviare Visual Studio e aprire la console di Gestione pacchetti prima di aprire la soluzione.</span><span class="sxs-lookup"><span data-stu-id="3375b-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="3375b-121">In alternativa, provare a eliminare `project.lock.json` e ripetere il ripristino.</span><span class="sxs-lookup"><span data-stu-id="3375b-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="3375b-122">Nei progetti .NET Core, quando si usa un pacchetto contenente un assembly con una firma non valida, si verifica un ciclo infinito di ripristino</span><span class="sxs-lookup"><span data-stu-id="3375b-122">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>

#### <a name="issue"></a><span data-ttu-id="3375b-123">Problema</span><span class="sxs-lookup"><span data-stu-id="3375b-123">Issue</span></span>

<span data-ttu-id="3375b-124">In alcune occasioni, quando si usa un pacchetto contenente un assembly con una firma non valida o quando la versione del pacchetto è impostata con il titolo 'DateTime', è possibile che il processo di ripristino automatico del pacchetto entri in un ciclo infinito.</span><span class="sxs-lookup"><span data-stu-id="3375b-124">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="3375b-125">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="3375b-125">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="3375b-126">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="3375b-126">Workaround</span></span>

<span data-ttu-id="3375b-127">Attualmente non esiste alcuna soluzione.</span><span class="sxs-lookup"><span data-stu-id="3375b-127">There is no workaround at this time.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="3375b-128">Non è possibile visualizzare, aggiungere o aggiornare DotNetCLITools usando Gestione pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="3375b-128">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="3375b-129">Problema</span><span class="sxs-lookup"><span data-stu-id="3375b-129">Issue</span></span>

<span data-ttu-id="3375b-130">Gestione pacchetti NuGet non visualizza e non consente l'aggiunta e/o l'aggiornamento di DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="3375b-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="3375b-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="3375b-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="3375b-132">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="3375b-132">Workaround</span></span>

<span data-ttu-id="3375b-133">È necessario modificare manualmente DotNetCLIToolReferences nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="3375b-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="3375b-134">Quando si imposta la proprietà PackageId per i progetti, il ripristino di NuGet ha esito negativo</span><span class="sxs-lookup"><span data-stu-id="3375b-134">NuGet restore will fail when you set PackageId property for projects</span></span>

#### <a name="issue"></a><span data-ttu-id="3375b-135">Problema</span><span class="sxs-lookup"><span data-stu-id="3375b-135">Issue</span></span>

<span data-ttu-id="3375b-136">Per i progetti .NET Core, il ripristino di NuGet in Visual Studio non rispetta la proprietà PackageId.</span><span class="sxs-lookup"><span data-stu-id="3375b-136">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="3375b-137">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="3375b-137">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="3375b-138">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="3375b-138">Workaround</span></span>

<span data-ttu-id="3375b-139">Eseguire il ripristino dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="3375b-139">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="3375b-140">Se nel progetto non è presente la cartella 'obj', è possibile che il ripristino abbia esito negativo</span><span class="sxs-lookup"><span data-stu-id="3375b-140">When your project does not have 'obj' folder, package restore may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="3375b-141">Problema</span><span class="sxs-lookup"><span data-stu-id="3375b-141">Issue</span></span>

<span data-ttu-id="3375b-142">Se la cartella 'obj' è stata eliminata, Visual Studio non è in grado di ripristinare PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="3375b-142">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="3375b-143">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="3375b-143">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="3375b-144">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="3375b-144">Workaround</span></span>

<span data-ttu-id="3375b-145">Creare manualmente la cartella 'obj'. Il ripristino dovrebbe avere esito positivo.</span><span class="sxs-lookup"><span data-stu-id="3375b-145">Create 'obj' folder manually and the restore should work.</span></span>

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="3375b-146">L'aggiornamento manuale dei pacchetti usando Aggiorna pacchetto nella console può avere esito negativo</span><span class="sxs-lookup"><span data-stu-id="3375b-146">Manually updating packages using Update-Package in console may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="3375b-147">Problema</span><span class="sxs-lookup"><span data-stu-id="3375b-147">Issue</span></span>

<span data-ttu-id="3375b-148">L'aggiornamento manuale nella console mediante Aggiorna pacchetto funziona una sola volta per i progetti PackageReferences appena convertiti.</span><span class="sxs-lookup"><span data-stu-id="3375b-148">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="3375b-149">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="3375b-149">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="3375b-150">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="3375b-150">Workaround</span></span>

<span data-ttu-id="3375b-151">Attualmente non esiste alcuna soluzione.</span><span class="sxs-lookup"><span data-stu-id="3375b-151">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="3375b-152">La ridestinazione della versione framework di destinazione può portare a informazioni Intellisense incomplete</span><span class="sxs-lookup"><span data-stu-id="3375b-152">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="3375b-153">Problema</span><span class="sxs-lookup"><span data-stu-id="3375b-153">Issue</span></span>

<span data-ttu-id="3375b-154">Se in Visual Studio si ridefinisce la destinazione della versione framework di destinazione, le informazioni Intellisense possono risultare incomplete.</span><span class="sxs-lookup"><span data-stu-id="3375b-154">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="3375b-155">Questo accade quando si usa PackageReferences come formato di gestione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="3375b-155">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="3375b-156">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="3375b-156">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="3375b-157">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="3375b-157">Workaround</span></span>

<span data-ttu-id="3375b-158">Eseguire un ripristino manuale.</span><span class="sxs-lookup"><span data-stu-id="3375b-158">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="3375b-159">msbuild /t:restore può avere esito negativo quando un progetto destinato a .NET461 fa riferimento a un altro progetto destinato a .NETStandard</span><span class="sxs-lookup"><span data-stu-id="3375b-159">msbuild /t:restore fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="3375b-160">Problema</span><span class="sxs-lookup"><span data-stu-id="3375b-160">Issue</span></span>

<span data-ttu-id="3375b-161">msbuild /t:restore può avere esito negativo quando un progetto basato su PackageReferenece e destinato a .NET461 fa riferimento a un altro progetto basato su PackageReferenece e destinato a .NETStandard.</span><span class="sxs-lookup"><span data-stu-id="3375b-161">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="3375b-162">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="3375b-162">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="3375b-163">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="3375b-163">Workaround</span></span>

<span data-ttu-id="3375b-164">Attualmente non esiste alcuna soluzione.</span><span class="sxs-lookup"><span data-stu-id="3375b-164">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="3375b-165">Problemi risolti nell'intervallo di tempo NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="3375b-165">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="3375b-166">[Note sulla versione per NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md) - Vengono elencati tutti i problemi risolti per NuGet 4.0 RC</span><span class="sxs-lookup"><span data-stu-id="3375b-166">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

### <a name="features"></a><span data-ttu-id="3375b-167">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="3375b-167">Features</span></span>

- <span data-ttu-id="3375b-168">Stringhe da localizzare in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span><span class="sxs-lookup"><span data-stu-id="3375b-168">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

- <span data-ttu-id="3375b-169">Nuget forza il caricamento dei progetti di applicazione Web in modalità di caricamento leggero delle soluzioni - [#4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="3375b-169">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

- <span data-ttu-id="3375b-170">PackageReference con riferimenti automatici deve supportare il blocco delle modifiche di versione nell'interfaccia utente per i pacchetti installati da SDK - [#4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="3375b-170">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

- <span data-ttu-id="3375b-171">Comunicare correttamente il valore di PackageSpec.Version per qualsiasi dipendenza di progetto (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="3375b-171">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

- <span data-ttu-id="3375b-172">Supporto per la rimozione di riferimenti in `.csproj` dalla riga di comando - [#4101](https://github.com/NuGet/Home/issues/4101)</span><span class="sxs-lookup"><span data-stu-id="3375b-172">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

- <span data-ttu-id="3375b-173">Supporto del ripristino per i progetti PackageReference (normali e xplat) e il caricamento leggero delle soluzioni - [#4003](https://github.com/NuGet/Home/issues/4003)</span><span class="sxs-lookup"><span data-stu-id="3375b-173">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

- <span data-ttu-id="3375b-174">Supporto per l'aggiunta di riferimenti in `.csproj` dalla riga di comando - [#3751](https://github.com/NuGet/Home/issues/3751)</span><span class="sxs-lookup"><span data-stu-id="3375b-174">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

- <span data-ttu-id="3375b-175">Supporto del ripristino NuGet per il caricamento leggero delle soluzioni per `packages.config` o `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span><span class="sxs-lookup"><span data-stu-id="3375b-175">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

- <span data-ttu-id="3375b-176">Supporto di contentFiles nel file target generato da nuget - [#3683](https://github.com/NuGet/Home/issues/3683)</span><span class="sxs-lookup"><span data-stu-id="3375b-176">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

- <span data-ttu-id="3375b-177">Stabilire CI Mono per la convalida di nuget.exe su Mac con MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span><span class="sxs-lookup"><span data-stu-id="3375b-177">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

- <span data-ttu-id="3375b-178">Togliere NuGet dalle dipendenze v2 di NuGet.Core - [#3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="3375b-178">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>

### <a name="bugs"></a><span data-ttu-id="3375b-179">Bug</span><span class="sxs-lookup"><span data-stu-id="3375b-179">Bugs</span></span>

- <span data-ttu-id="3375b-180">Il ripristino di NuGet in Visual Studio non rispetta la proprietà PackageId dei progetti - [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="3375b-180">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

- <span data-ttu-id="3375b-181">Errore NuGet ProjectSystemCache durante l'aggiunta di un pacchetto nel pacchetto VSIX - [#4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="3375b-181">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

- <span data-ttu-id="3375b-182">Il comando pack genera eccezioni se si usa IncludeSource in un progetto con più moniker TFM - [#4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="3375b-182">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

- <span data-ttu-id="3375b-183">Arresti anomali di VS 2017 RC3 durante l'aggiornamento dalla gestione dei pacchetti per la soluzione - [#4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="3375b-183">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

- <span data-ttu-id="3375b-184">Impossibile disinstallare un pacchetto appena installato - [#4435](https://github.com/NuGet/Home/issues/4435)</span><span class="sxs-lookup"><span data-stu-id="3375b-184">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

- <span data-ttu-id="3375b-185">Durante la migrazione a PackageRef, le soluzioni ibride hanno un comportamento strano per il ripristino - [#4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="3375b-185">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

- <span data-ttu-id="3375b-186">L'avvio di una compilazione poco dopo aver avviato un'operazione NuGet (install, update, restore), può causare il blocco di VS - [#4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="3375b-186">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

- <span data-ttu-id="3375b-187">Blocco dell'interfaccia utente - Deadlock durante l'inizializzazione di NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span><span class="sxs-lookup"><span data-stu-id="3375b-187">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

- <span data-ttu-id="3375b-188">Il comando add package deve aggiungere la versione come attributo anziché come elemento - [#4325](https://github.com/NuGet/Home/issues/4325)</span><span class="sxs-lookup"><span data-stu-id="3375b-188">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

- <span data-ttu-id="3375b-189">Dotnet restore foo.sln -- non riesce quando le configurazioni nella soluzione causano progetti duplicati (ma configurazioni diverse) nel grafico di ripristino - [#4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="3375b-189">Dotnet Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

- <span data-ttu-id="3375b-190">Pacchetti di solo contenuto - [#3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="3375b-190">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

- <span data-ttu-id="3375b-191">Per impostazione predefinita rifiuto esplicito dell'opzione per il selettore del formato del pacchetto - [#4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="3375b-191">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

- <span data-ttu-id="3375b-192">Prestazioni: CreateUAP_CSharp_VS.01.1.Create regressione progetto Duration_TotalElapsedTime di 3.153.570 ms (149,1%).</span><span class="sxs-lookup"><span data-stu-id="3375b-192">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="3375b-193">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="3375b-193">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

- <span data-ttu-id="3375b-194">Prestazioni: ManagedLangs_CS_DDRIT.0300.Rebuild regressione soluzione Duration_TotalElapsedTime di 1,5 sec.</span><span class="sxs-lookup"><span data-stu-id="3375b-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="3375b-195">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="3375b-195">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

- <span data-ttu-id="3375b-196">Errore di denominazione in progetti con più moniker TFM - [#4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="3375b-196">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

- <span data-ttu-id="3375b-197">Prestazioni: WebForms_DDRIT.1200.Close regressione soluzione VM_ImagesInMemory_Total_devenv di 3.000 conteggi (0,5%).</span><span class="sxs-lookup"><span data-stu-id="3375b-197">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="3375b-198">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="3375b-198">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

- <span data-ttu-id="3375b-199">vsfeedback - Avvisi di pack con destinazione netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span><span class="sxs-lookup"><span data-stu-id="3375b-199">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

- <span data-ttu-id="3375b-200">PathTooLongException quando si tenta di aggiungere un pacchetto NuGet a un'applicazione Web ASP.NET Core vuota - [#4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="3375b-200">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

- <span data-ttu-id="3375b-201">Esecuzione troppo frequente di pack -- dotnet pack non riesce con l'errore È presente una dipendenza circolare nel grafico di dipendenze che utilizza la destinazione "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="3375b-201">Pack runs too often -- dotnet pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

- <span data-ttu-id="3375b-202">Esecuzione troppo frequente di pack - La generazione del pacchetto NuGet non include tutte le configurazioni  - [#4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="3375b-202">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

- <span data-ttu-id="3375b-203">NullReferenceException durante l'aggiunta di nuget con packageref in un progetto C++ - [#4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="3375b-203">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

- <span data-ttu-id="3375b-204">Accessibilità: Assistente vocale non indica la casella di controllo per selezionare i progetti in cui installare il pacchetto - [#4366](https://github.com/NuGet/Home/issues/4366)</span><span class="sxs-lookup"><span data-stu-id="3375b-204">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

- <span data-ttu-id="3375b-205">NuGet VS17 non riesce sporadicamente a connettersi a feed VSO/VSTS - Bug VS 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="3375b-205">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

- <span data-ttu-id="3375b-206">L'output di contentFiles va nella posizione sbagliata se PackagePath specifica il percorso come "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="3375b-206">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

- <span data-ttu-id="3375b-207">La destinazione della generazione del pacchetto aggiunge la proprietà PackageVersion con VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="3375b-207">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

- <span data-ttu-id="3375b-208">La specifica del percorso del pacchetto non funziona con dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="3375b-208">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

- <span data-ttu-id="3375b-209">NuGet genera vari avvisi per importazioni duplicate durante il ripristino - [#4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="3375b-209">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

- <span data-ttu-id="3375b-210">La finestra di dialogo per scegliere il formato di Gestione pacchetti NuGet non ha un aspetto corretto con il tema scuro - [#4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="3375b-210">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

- <span data-ttu-id="3375b-211">Arresto anomalo di Visual Studio durante il ripristino - [#4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="3375b-211">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

- <span data-ttu-id="3375b-212">Deadlock di Visual Studio se si aggiunge un moniker TFM in targetframeworks, si salva e quindi si compila.</span><span class="sxs-lookup"><span data-stu-id="3375b-212">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="3375b-213">10% delle volte - [#4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="3375b-213">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

- <span data-ttu-id="3375b-214">nuget pack non restituisce un messaggio di completamento dell'operazione per la creazione corretta del pacchetto di un progetto - [#4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="3375b-214">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

- <span data-ttu-id="3375b-215">Errore di PackTask perché impossibile trovare System.IO.Compression 4.1 - [#4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="3375b-215">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

- <span data-ttu-id="3375b-216">Esecuzione troppo frequente di pack - PackTask ha spesso esito negativo con conflitti di accesso al file - [#4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="3375b-216">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

- <span data-ttu-id="3375b-217">NuGet apre la finestra di output durante il ripristino in background - [#4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="3375b-217">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

- <span data-ttu-id="3375b-218">Eliminare ServiceProvider in quanto modello di codifica pericoloso (che può causare blocchi) - [#4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="3375b-218">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

- <span data-ttu-id="3375b-219">Prestazioni/blocco interfaccia utente - Migliorare le letture DownloadTimeoutStream - [#4266](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="3375b-219">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

- <span data-ttu-id="3375b-220">Deadlock di Visual Studio se si tenta di chiudere un progetto prima del completamento del ripristino di NuGet - [#4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="3375b-220">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

- <span data-ttu-id="3375b-221">Problemi relativi a PackTask e alla creazione di `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span><span class="sxs-lookup"><span data-stu-id="3375b-221">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

- <span data-ttu-id="3375b-222">[vsfeedback] Impossibile risolvere pacchetti nuget per un nuovo progetto (è necessario riavviare Visual Studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="3375b-222">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

- <span data-ttu-id="3375b-223">[vsfeedback] L'elenco a discesa "Versione" che mostra le versioni dei pacchetti disponibili non è ben sincronizzato con il pacchetto NuGet selezionato...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="3375b-223">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

- <span data-ttu-id="3375b-224">Nuget.Client deve usare CPS JoinableTaskFactory per le interazioni con CPS per evitare deadlock - [#4185](https://github.com/NuGet/Home/issues/4185)</span><span class="sxs-lookup"><span data-stu-id="3375b-224">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

- <span data-ttu-id="3375b-225">NuGet 3.5.0 non estrae il file `.targets` dal pacchetto - [#4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="3375b-225">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

- <span data-ttu-id="3375b-226">dotnet pack non supporta title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span><span class="sxs-lookup"><span data-stu-id="3375b-226">dotnet pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

- <span data-ttu-id="3375b-227">Install-Package genera una finestra di dialogo di errore in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="3375b-227">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

- <span data-ttu-id="3375b-228">L'aggiornamento di un pacchetto per il progetto .NET Core sembra non funzionare, perché l'interfaccia utente non ottiene l'aggiornamento di CPS dal nominato.</span><span class="sxs-lookup"><span data-stu-id="3375b-228">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="3375b-229"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="3375b-229"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

- <span data-ttu-id="3375b-230">Migliorare l'avviso di riferimento non risolto - [#3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="3375b-230">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

- <span data-ttu-id="3375b-231">dotnet pack - ProjectReference perde le informazioni sulla versione - [#3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="3375b-231">dotnet pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

- <span data-ttu-id="3375b-232">Regressioni del tempo totale trascorso per creare un progetto di app UWP e ricompilare - [#3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="3375b-232">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

- <span data-ttu-id="3375b-233">Viene visualizzato un messaggio di ripristino completato anche dopo un errore durante il ripristino.</span><span class="sxs-lookup"><span data-stu-id="3375b-233">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="3375b-234"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="3375b-234"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

- <span data-ttu-id="3375b-235">Ripubblicare Nuget.CommandLine 3.4.4 in Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span><span class="sxs-lookup"><span data-stu-id="3375b-235">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

- <span data-ttu-id="3375b-236">Durante la migrazione i progetti passano da `project.json` a `.csproj` --- Il ripristino non riesce - [#4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="3375b-236">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

- <span data-ttu-id="3375b-237">Ripristino non riuscito per un nuovo progetto di test xUnit  - [#4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="3375b-237">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

- <span data-ttu-id="3375b-238">I progetti Core possono bloccarsi, blocco dell'interfaccia utente all'apertura - [#4269](https://github.com/NuGet/Home/issues/4269)</span><span class="sxs-lookup"><span data-stu-id="3375b-238">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

- <span data-ttu-id="3375b-239">Correggere il file targets per le attività di compilazione - [#4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="3375b-239">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

- <span data-ttu-id="3375b-240">L'elenco degli errori deve includere un errore dopo la compilazione di una soluzione che scarica il progetto di riferimento - [#4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="3375b-240">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

- <span data-ttu-id="3375b-241">MSB4057: la destinazione "_GenerateRestoreGraphProjectEntry" non è presente nel progetto.</span><span class="sxs-lookup"><span data-stu-id="3375b-241">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="3375b-242"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="3375b-242"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

- <span data-ttu-id="3375b-243">vsfeedback: arresto anomalo dell'interfaccia utente di Gestione pacchetti NuGet per la soluzione quando si selezionano tutti i progetti - [#4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="3375b-243">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

- <span data-ttu-id="3375b-244">Errore di nuget.exe msbuildpath in presenza di una barra finale - [#4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="3375b-244">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

- <span data-ttu-id="3375b-245">vsfeedback: NuGet restore genera vari avvisi di riferimenti al progetto per il progetto LinqToTwitter - [#4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="3375b-245">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

- <span data-ttu-id="3375b-246">La creazione del pacchetto da `.csproj` non include l'attributo minClientVersion - [#4135](https://github.com/NuGet/Home/issues/4135)</span><span class="sxs-lookup"><span data-stu-id="3375b-246">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

- <span data-ttu-id="3375b-247">NuGet.Build.Tasks.Pack.dll fornito in ritardo con firma in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="3375b-247">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

- <span data-ttu-id="3375b-248">VSFeedback: il ripristino non riesce per un progetto di VS 2015 generato con CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="3375b-248">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

- <span data-ttu-id="3375b-249">VSFeedback: gli errori di ripristino possono nascondere i messaggi di errore più completi generati dalla compilazione - [#4113](https://github.com/NuGet/Home/issues/4113)</span><span class="sxs-lookup"><span data-stu-id="3375b-249">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

- <span data-ttu-id="3375b-250">[VSFeedback] Errore durante il ripristino dei pacchetti NuGet per il progetto di sito Web: Il valore non può essere null.</span><span class="sxs-lookup"><span data-stu-id="3375b-250">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="3375b-251"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="3375b-251"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

- <span data-ttu-id="3375b-252">La migrazione genera un'eccezione di riferimento a oggetto in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span><span class="sxs-lookup"><span data-stu-id="3375b-252">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

- <span data-ttu-id="3375b-253">dotnet pack deve includere nel pacchetto strumenti con le versioni usate per la compilazione del pacchetto - [#4063](https://github.com/NuGet/Home/issues/4063)</span><span class="sxs-lookup"><span data-stu-id="3375b-253">dotnet pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

- <span data-ttu-id="3375b-254">Il nuovo ripristino in background scrive millisecondi nella barra di stato ma per il ripristino sono richiesti secondi - [#4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="3375b-254">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

- <span data-ttu-id="3375b-255">Errore di ortografia nel messaggio di errore sulla risoluzione di tutti i riferimenti al progetto - [#4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="3375b-255">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

- <span data-ttu-id="3375b-256">Abilitare i flussi di lavoro PCM negli scenari di riferimento ai pacchetti - [#4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="3375b-256">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

- <span data-ttu-id="3375b-257">Impossibile trovare i pacchetti installati nell'interfaccia utente di Gestione pacchetti - [#4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="3375b-257">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

- <span data-ttu-id="3375b-258">Errore di dotnet pack quando PackagePath è vuoto - [#3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="3375b-258">dotnet pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

- <span data-ttu-id="3375b-259">L'attività di ripristino ha esito negativo in uno scenario multiutente - [#3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="3375b-259">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

- <span data-ttu-id="3375b-260">Impossibile modificare il tipo di contenuto quando si crea un pacchetto con l'attività nuget pack - [#3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="3375b-260">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

- <span data-ttu-id="3375b-261">La copia predefinita di ContentFiles non è corretta per MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span><span class="sxs-lookup"><span data-stu-id="3375b-261">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

- <span data-ttu-id="3375b-262">Il ripristino di pacchetti con installazione registra due volte il messaggio di ripristino dei pacchetti - [#3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="3375b-262">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

- <span data-ttu-id="3375b-263">Rimuovere i confini - Il ripristino della sezione "runtimes" deve essere applicato solo al progetto corrente - [#3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="3375b-263">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

- <span data-ttu-id="3375b-264">L'attività pack posiziona i file di contenuto sia in 'content/' che in 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="3375b-264">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

- <span data-ttu-id="3375b-265">dotnet pack3 aggiunge elementi di divisione per i tag - [#3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="3375b-265">dotnet pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

- <span data-ttu-id="3375b-266">dotnet pack: la creazione di un pacchetto di progetti con riferimenti ai pacchetti causa un avviso di importazione duplicata - [#3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="3375b-266">dotnet pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

- <span data-ttu-id="3375b-267">La registrazione del ripristino in VS non sempre viene visualizzata - [#3633](https://github.com/NuGet/Home/issues/3633)</span><span class="sxs-lookup"><span data-stu-id="3375b-267">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

- <span data-ttu-id="3375b-268">Il testo della Guida di nuget locals menziona ancora la cache dei pacchetti - [#3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="3375b-268">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

- <span data-ttu-id="3375b-269">Restore3 associa PackageReferences a TargetFrameworks.</span><span class="sxs-lookup"><span data-stu-id="3375b-269">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="3375b-270"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="3375b-270"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

- <span data-ttu-id="3375b-271">Nuget sceglie una versione imprevista di MSBuild nel prompt dei comandi per gli sviluppatori in VS "15" Preview 4</span><span class="sxs-lookup"><span data-stu-id="3375b-271">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="3375b-272">- [#3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="3375b-272">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

- <span data-ttu-id="3375b-273">Scrivere i file di destinazioni/proprietà per il ripristino non riuscito - [#3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="3375b-273">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

- <span data-ttu-id="3375b-274">NuGet durante il ripristino non rispetta lo stesso shim di compatibilità di MSBuild durante l'esecuzione nel prompt dei comandi di VS 15 - [#3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="3375b-274">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

- <span data-ttu-id="3375b-275">Riabilitare PackFromProjectWithDevelopmentDependencySet per VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span><span class="sxs-lookup"><span data-stu-id="3375b-275">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

- <span data-ttu-id="3375b-276">Problemi di Blend con NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="3375b-276">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

- <span data-ttu-id="3375b-277">Integrare la versione 4.0.0.2067 nei repository CLI e SDK per includerla in RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="3375b-277">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

- <span data-ttu-id="3375b-278">VS si blocca quando si crea una nuova app console Core, si chiude la soluzione, di apre la soluzione e si chiude la soluzione  - [#4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="3375b-278">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

- <span data-ttu-id="3375b-279">Blocco durante l'apertura di un progetto in d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span><span class="sxs-lookup"><span data-stu-id="3375b-279">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

- <span data-ttu-id="3375b-280">Correggere il messaggio della Guida/documentazione di dotnet/nuget.exe locals - [#3919](https://github.com/NuGet/Home/issues/3919)</span><span class="sxs-lookup"><span data-stu-id="3375b-280">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

- <span data-ttu-id="3375b-281">Esaminare PackTask per i problemi con gli spazi vuoti iniziali o finali - [#3906](https://github.com/NuGet/Home/issues/3906)</span><span class="sxs-lookup"><span data-stu-id="3375b-281">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

- <span data-ttu-id="3375b-282">dotnet pack crea il pacchetto da obj e non da bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="3375b-282">dotnet pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

- <span data-ttu-id="3375b-283">dotnet pack sembra impostare sempre la versione di ProjectReference su 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span><span class="sxs-lookup"><span data-stu-id="3375b-283">dotnet pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

- <span data-ttu-id="3375b-284">dotnet pack non riesce con riferimenti a progetti e <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span><span class="sxs-lookup"><span data-stu-id="3375b-284">dotnet pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

- <span data-ttu-id="3375b-285">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span><span class="sxs-lookup"><span data-stu-id="3375b-285">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

- <span data-ttu-id="3375b-286">Tagliare lo spazio vuoto dalle proprietà di MSBuild - [#3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="3375b-286">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

- <span data-ttu-id="3375b-287">Consolidare i due eventi di progetto generati al caricamento del progetto - [#3759](https://github.com/NuGet/Home/issues/3759)</span><span class="sxs-lookup"><span data-stu-id="3375b-287">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

- <span data-ttu-id="3375b-288">Versione non corretta per le librerie P2P nel file `project.assets.json` - [#3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="3375b-288">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

- <span data-ttu-id="3375b-289">Arresto anomalo del ripristino a causa di feed che non risponde e pacchetto non disponibile - [#3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="3375b-289">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

- <span data-ttu-id="3375b-290">nuget.exe potrebbe bloccarsi in presenza di una grande quantità di errori nell'output di MSBuild - [#3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="3375b-290">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

- <span data-ttu-id="3375b-291">Il ripristino in fase di compilazione per Blend non riesce la prima volta, ma riesce la seconda (scenario VS corretto) - [#2121](https://github.com/NuGet/Home/issues/2121)</span><span class="sxs-lookup"><span data-stu-id="3375b-291">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

### <a name="dcrs"></a><span data-ttu-id="3375b-292">DCR</span><span class="sxs-lookup"><span data-stu-id="3375b-292">DCRs</span></span>

- <span data-ttu-id="3375b-293">Eseguire la migrazione di VSIX da VSIX v2 a VSIX v3 - [#4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="3375b-293">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

- <span data-ttu-id="3375b-294">NuGet deve disporre di un meccanismo per ottenere il percorso del file di blocco in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span><span class="sxs-lookup"><span data-stu-id="3375b-294">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

- <span data-ttu-id="3375b-295">Aggiungere gli asset di compilazione al controllo di compatibilità dei moniker TFM e al file di asset - [#3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="3375b-295">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

- <span data-ttu-id="3375b-296">Definire un nuovo "Pack" ProjectCapability nelle destinazioni della creazione del pacchetto per abilitare le funzionalità correlate al pacchetto - [#4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="3375b-296">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

- <span data-ttu-id="3375b-297">Eseguire pack come destinazione di post compilazione usando una condizione basata sulla proprietà di MSBuild "GeneratePackageOnBuild" - [#4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="3375b-297">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

- <span data-ttu-id="3375b-298">Usare la proprietà NuGet RestoreProjectStyle per creare un progetto NuGet specifico - [#4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="3375b-298">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

- <span data-ttu-id="3375b-299">Adattare il ripristino per la modifica dei riferimenti a progetti transitivi - [#4076](https://github.com/NuGet/Home/issues/4076)</span><span class="sxs-lookup"><span data-stu-id="3375b-299">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

- <span data-ttu-id="3375b-300">Aggiungere le proprietà NuGet nel file di destinazione per i progetti non UWP - [#4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="3375b-300">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

- <span data-ttu-id="3375b-301">Supporto di TargetPlatformVersion UWP - [#3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="3375b-301">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

- <span data-ttu-id="3375b-302">Comunicare i metadati dei riferimenti a progetti al sistema di progetto NuGet - [#3922](https://github.com/NuGet/Home/issues/3922)</span><span class="sxs-lookup"><span data-stu-id="3375b-302">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

- <span data-ttu-id="3375b-303">Aggiungere l'interfaccia utente per la modalità di creazione di pacchetti - [#3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="3375b-303">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

- <span data-ttu-id="3375b-304">Per il file `.csproj` legacy è necessario impostare NugetTargetMoniker e RuntimeIdentifiers in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span><span class="sxs-lookup"><span data-stu-id="3375b-304">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

- <span data-ttu-id="3375b-305">L'installazione del pacchetto può sovrapporsi al ripristino automatico - [#3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="3375b-305">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

- <span data-ttu-id="3375b-306">Lo stato dei comandi del menu di scelta rapida non viene controllato fino al caricamento di VSPackage - [#3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="3375b-306">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

- <span data-ttu-id="3375b-307">Per il ripristino di soluzione e il ripristino di compilazione vengono ancora visualizzate finestre di dialogo - [#3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="3375b-307">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

- <span data-ttu-id="3375b-308">Isolare la versione di VSSDK nella compilazione di soluzione NuGet.Clients - [#3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="3375b-308">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="3375b-309">Collegamento ai problemi di GitHub risolti nella versione RTM</span><span class="sxs-lookup"><span data-stu-id="3375b-309">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="3375b-310">Elenco di problemi 1</span><span class="sxs-lookup"><span data-stu-id="3375b-310">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RTM")  
[<span data-ttu-id="3375b-311">Elenco di problemi 2</span><span class="sxs-lookup"><span data-stu-id="3375b-311">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC4")  
[<span data-ttu-id="3375b-312">Elenco di problemi 3</span><span class="sxs-lookup"><span data-stu-id="3375b-312">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC3")  
[<span data-ttu-id="3375b-313">Elenco di problemi 4</span><span class="sxs-lookup"><span data-stu-id="3375b-313">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC2")  
[<span data-ttu-id="3375b-314">Elenco di problemi 5</span><span class="sxs-lookup"><span data-stu-id="3375b-314">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC")
