---
title: Note sulla versione per NuGet 4.0 RC
description: Note sulla versione per NuGet 4.0 RC incluse informazioni su problemi noti, correzioni di bug e DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 8124b11d0489a2c72ffcfdde28e8528c1da1f677
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-40-rc-release-notes"></a><span data-ttu-id="a94f5-103">Note sulla versione per NuGet 4.0 RC</span><span class="sxs-lookup"><span data-stu-id="a94f5-103">NuGet 4.0 RC Release Notes</span></span>

[<span data-ttu-id="a94f5-104">Note sulla versione per NuGet 3.5 RTM</span><span class="sxs-lookup"><span data-stu-id="a94f5-104">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="a94f5-105">[NuGet 4.0 RC per Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) è una versione incentrata sull'aggiunta del supporto per gli scenari principali di .NET Core, sul fornire risposte ai commenti e suggerimenti principali dei clienti e sul miglioramento delle prestazioni in svariati scenari.</span><span class="sxs-lookup"><span data-stu-id="a94f5-105">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="a94f5-106">Questa versione offre diversi miglioramenti come il supporto di PackageReference, i comandi NuGet come destinazioni di MSBuild, il ripristino dei pacchetti in background e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="a94f5-106">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="a94f5-107">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="a94f5-107">Bug Fixes</span></span>

- <span data-ttu-id="a94f5-108">Modifiche del comportamento in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span><span class="sxs-lookup"><span data-stu-id="a94f5-108">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

- <span data-ttu-id="a94f5-109">Errore di nuget.exe restore in computer solo VS "15" - [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="a94f5-109">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

- <span data-ttu-id="a94f5-110">Il comando per la creazione di un nuovo progetto .NETCore dovrebbe bloccare la compilazione durante il ripristino - [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="a94f5-110">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

- <span data-ttu-id="a94f5-111">Con un'app Web ASP.NET Core migrata da VS2015 a VS "15" non è possibile eseguire il ripristino.</span><span class="sxs-lookup"><span data-stu-id="a94f5-111">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="a94f5-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="a94f5-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

- <span data-ttu-id="a94f5-113">[Errore di test] Impossibile disinstallare 'jQuery Validation' del pacchetto con l'interfaccia utente di Gestione pacchetti - [#3755](https://github.com/NuGet/Home/issues/3755)</span><span class="sxs-lookup"><span data-stu-id="a94f5-113">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

- <span data-ttu-id="a94f5-114">Quando si installa un pacchetto nel file `project.json` UWP, dovrebbero essere ripristinati anche i progetti padre - [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="a94f5-114">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

- <span data-ttu-id="a94f5-115">Modificare le destinazioni NuGet per registrare le origini di pacchetti con livello di dettaglio alto invece di normale - [#3719](https://github.com/NuGet/Home/issues/3719)</span><span class="sxs-lookup"><span data-stu-id="a94f5-115">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

- <span data-ttu-id="a94f5-116">dotnet</span><span class="sxs-lookup"><span data-stu-id="a94f5-116">dotnet</span></span>
  - <span data-ttu-id="a94f5-117">dotnetcore pack3 dovrebbe includere la documentazione XML per impostazione predefinita - [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="a94f5-117">dotnetcore pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

- <span data-ttu-id="a94f5-118">L'aggiornamento in batch non riesce dall'interfaccia utente quando l'origine senza il pacchetto è la prima e si seleziona l'opzione Tutte le origini - [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="a94f5-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

- <span data-ttu-id="a94f5-119">Il comando nuget pack non include tutti i file - [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="a94f5-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

- <span data-ttu-id="a94f5-120">Problema di memoria insufficiente - [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="a94f5-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

- <span data-ttu-id="a94f5-121">La sezione ProjectFileDependencyGroups del file di asset dovrebbe usare i nomi di libreria per i progetti - [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="a94f5-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

- <span data-ttu-id="a94f5-122">"dotnet restore" e ricorsione delle directory - [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="a94f5-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

- <span data-ttu-id="a94f5-123">Ripristino: 3 errori vengono registrati come avvisi anziché errori - [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="a94f5-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

- <span data-ttu-id="a94f5-124">Problema di TFS: "[file] non è stato trovato nell'area di lavoro o non si dispone delle autorizzazioni per accedervi." - [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="a94f5-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

- <span data-ttu-id="a94f5-125">Se si digita "nuget <packagename>" nella casella di ricerca di avvio veloce di VS viene mantenuto il prefisso "nuget " - [#2719](https://github.com/NuGet/Home/issues/2719)</span><span class="sxs-lookup"><span data-stu-id="a94f5-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

- <span data-ttu-id="a94f5-126">System.Xml.XmlException: Elemento radice non riconosciuto nella parte Core Properties.</span><span class="sxs-lookup"><span data-stu-id="a94f5-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="a94f5-127">Riga 2, posizione 2.</span><span class="sxs-lookup"><span data-stu-id="a94f5-127">Line 2, position 2.</span></span><span data-ttu-id="a94f5-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="a94f5-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

- <span data-ttu-id="a94f5-129">`.nuspec` con caratteri di escape per &lt; o &gt; nei campi di testo non viene più compilato - [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="a94f5-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

- <span data-ttu-id="a94f5-130">nuget.exe delete non richiede le credenziali (modalità non interattiva) - [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="a94f5-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

- <span data-ttu-id="a94f5-131">nuget.exe delete genera un avviso per la chiave API per le origini locali, anche se non ha senso - [#2625](https://github.com/NuGet/Home/issues/2625)</span><span class="sxs-lookup"><span data-stu-id="a94f5-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

- <span data-ttu-id="a94f5-132">Esperienza insoddisfacente per l'errore durante l'installazione del pacchetto EF -pre - [#2566](https://github.com/NuGet/Home/issues/2566)</span><span class="sxs-lookup"><span data-stu-id="a94f5-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

- <span data-ttu-id="a94f5-133">Arresto anomalo di Visual Studio durante il tentativo di modifica della selezione in Gestione pacchetti - [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="a94f5-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

- <span data-ttu-id="a94f5-134">dotnet</span><span class="sxs-lookup"><span data-stu-id="a94f5-134">dotnet</span></span>
  - <span data-ttu-id="a94f5-135">dotnetcore restore esegue ricerche di ID con distinzione tra maiuscole e minuscole nei repository locali con elenco semplice quando si usano le versioni mobili - [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="a94f5-135">dotnetcore restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

- <span data-ttu-id="a94f5-136">nuget.exe delete non funziona per il feed V2 - [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="a94f5-136">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

- <span data-ttu-id="a94f5-137">Per il timeout di nuget.exe push è necessario un messaggio di errore migliore - [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="a94f5-137">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

- <span data-ttu-id="a94f5-138">Il ripristino dello strumento senza le direttive imports appropriate ha esito negativo senza messaggi.</span><span class="sxs-lookup"><span data-stu-id="a94f5-138">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="a94f5-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="a94f5-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

- <span data-ttu-id="a94f5-140">NuGet richiede di immettere le credenziali in presenza di un feed privato anche in caso di installazione da nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span><span class="sxs-lookup"><span data-stu-id="a94f5-140">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

- <span data-ttu-id="a94f5-141">Il pacchetto ApplicationInsights 2.0 è elencato ma non esiste ancora - [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="a94f5-141">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

- <span data-ttu-id="a94f5-142">UIDelay nel ramo VS "15" preview 5 - [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="a94f5-142">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

- <span data-ttu-id="a94f5-143">Il primo evento OnBuild non viene gestito per il ripristino durante la compilazione per UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span><span class="sxs-lookup"><span data-stu-id="a94f5-143">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

- <span data-ttu-id="a94f5-144">PowerShell5 non consente l'installazione di EntityFramework?</span><span class="sxs-lookup"><span data-stu-id="a94f5-144">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="a94f5-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="a94f5-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

- <span data-ttu-id="a94f5-146">Aggiungere l'origine alla registrazione dettagliata (da valutare per 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="a94f5-146">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

- <span data-ttu-id="a94f5-147">Parametro NoCache non rispettato nella versione 3.4+ di NuGet - [#3074](https://github.com/NuGet/Home/issues/3074)</span><span class="sxs-lookup"><span data-stu-id="a94f5-147">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

- <span data-ttu-id="a94f5-148">Quando il caricamento di un provider di credenziali non riesce in Visual Studio, non interrompere NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="a94f5-148">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>

## <a name="features"></a><span data-ttu-id="a94f5-149">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="a94f5-149">Features</span></span>

- <span data-ttu-id="a94f5-150">Configurare CI per l'esecuzione x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span><span class="sxs-lookup"><span data-stu-id="a94f5-150">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

- <span data-ttu-id="a94f5-151">Ripristino automatico 3/3: nessun blocco dall'interfaccia utente - [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="a94f5-151">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

- <span data-ttu-id="a94f5-152">Ripristino automatico 2/3: ripristino in background in caso di nomina - [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="a94f5-152">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

- <span data-ttu-id="a94f5-153">Ripristinare i riferimenti al progetto in modo che corrispondano al comportamento di compilazione (ricorsione) - [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="a94f5-153">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

- <span data-ttu-id="a94f5-154">Supporto DPL in Visual Studio "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span><span class="sxs-lookup"><span data-stu-id="a94f5-154">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

- <span data-ttu-id="a94f5-155">Spostare il file di impostazioni in Programmi - [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="a94f5-155">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

- <span data-ttu-id="a94f5-156">Per le proprietà e le destinazioni di ripristino generate è necessaria la partecipazione a crosstargeting - [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="a94f5-156">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

- <span data-ttu-id="a94f5-157">Supporto di PackageTargetFallback (in precedenza imports) per il ripristino NuGet - [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="a94f5-157">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

- <span data-ttu-id="a94f5-158">Implementazione di ToolsRef - [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="a94f5-158">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

- <span data-ttu-id="a94f5-159">Restore3 per un RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span><span class="sxs-lookup"><span data-stu-id="a94f5-159">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

- <span data-ttu-id="a94f5-160">Supporto nell'interfaccia utente di NuGet di aggiunta/rimozione/aggiornamento dei riferimenti ai pacchetti - [#3457](https://github.com/NuGet/Home/issues/3457)</span><span class="sxs-lookup"><span data-stu-id="a94f5-160">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

- <span data-ttu-id="a94f5-161">Ripristino automatico 1/3: implementazione dell'API per nominare tramite memorizzazione nella cache delle informazioni di ripristino del progetto - [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="a94f5-161">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

- <span data-ttu-id="a94f5-162">[0] Attività e destinazioni di ripristino NuGet - [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="a94f5-162">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

- <span data-ttu-id="a94f5-163">[1] Abilitare il ripristino a livello di soluzione in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span><span class="sxs-lookup"><span data-stu-id="a94f5-163">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

- <span data-ttu-id="a94f5-164">Supporto dell'estendibilità pubblica del provider di credenziali in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="a94f5-164">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

- <span data-ttu-id="a94f5-165">Esecuzione ricorsiva di nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="a94f5-165">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

- <span data-ttu-id="a94f5-166">Non è possibile caricare Microsoft.TeamFoundation.Client in dev15, è necessario aggiornare Microsoft.TeamFoundation.Client alla versione 15.0 per VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span><span class="sxs-lookup"><span data-stu-id="a94f5-166">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

- <span data-ttu-id="a94f5-167">Non è possibile installare il pacchetto di C++ nel progetto UWP C++ in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span><span class="sxs-lookup"><span data-stu-id="a94f5-167">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

- <span data-ttu-id="a94f5-168">Nupkg deve supportare la cartella \buildCrossTargeting\ e importare `.targets` / `.props` per il "crosstargeting" dell'ambito MSBuild.</span><span class="sxs-lookup"><span data-stu-id="a94f5-168">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="a94f5-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="a94f5-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

- <span data-ttu-id="a94f5-170">Progettazione di ToolsReference - [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="a94f5-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

- <span data-ttu-id="a94f5-171">Correggere l'interfaccia utente di NuGet per supportare il ripristino con PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span><span class="sxs-lookup"><span data-stu-id="a94f5-171">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

- <span data-ttu-id="a94f5-172">Aggiunta del pulsante per cancellare la cache nelle impostazioni di Gestione pacchetti in VS - [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="a94f5-172">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="a94f5-173">DCR</span><span class="sxs-lookup"><span data-stu-id="a94f5-173">DCRs</span></span>

- <span data-ttu-id="a94f5-174">Il ripristino della soluzione dovrebbe essere bloccato quando è in corso un ripristino automatico.</span><span class="sxs-lookup"><span data-stu-id="a94f5-174">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="a94f5-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="a94f5-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

- <span data-ttu-id="a94f5-176">L'installazione di NetCore dall'interfaccia utente di Gestione pacchetti NuGet viene eseguita in tutti i moniker TFM, invece che solo in quelli supportati dal pacchetto - [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="a94f5-176">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

- <span data-ttu-id="a94f5-177">L'API di denominazione per il ripristino deve supportare anche DotNetCliToolsReferences.</span><span class="sxs-lookup"><span data-stu-id="a94f5-177">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="a94f5-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="a94f5-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

- <span data-ttu-id="a94f5-179">Contrassegnare VSIX "15" come systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span><span class="sxs-lookup"><span data-stu-id="a94f5-179">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

- <span data-ttu-id="a94f5-180">Eseguire la migrazione dai riferimenti a MS.VS.Services.Client a MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="a94f5-180">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

- <span data-ttu-id="a94f5-181">Il comando restore deve rispettare $(RestoreLegacyPackagesDirectory) a livello di progetto - [#3618](https://github.com/NuGet/Home/issues/3618)</span><span class="sxs-lookup"><span data-stu-id="a94f5-181">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

- <span data-ttu-id="a94f5-182">Per il ripristino in un progetto con singolo TargetFramework non devono essere definite condizioni per le proprietà - [#3588](https://github.com/NuGet/Home/issues/3588)</span><span class="sxs-lookup"><span data-stu-id="a94f5-182">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

- <span data-ttu-id="a94f5-183">dotnet</span><span class="sxs-lookup"><span data-stu-id="a94f5-183">dotnet</span></span>
  - <span data-ttu-id="a94f5-184">dotnetcore restore3 foo.csproj deve seguire le dipendenze e anche ripristinarle.</span><span class="sxs-lookup"><span data-stu-id="a94f5-184">dotnetcore restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="a94f5-185">Come la compilazione.</span><span class="sxs-lookup"><span data-stu-id="a94f5-185">Like build.</span></span><span data-ttu-id="a94f5-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="a94f5-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

- <span data-ttu-id="a94f5-187">"type": "platform" Dipendenze rappresentate come "type":"package" in file di blocco - [#2695](https://github.com/NuGet/Home/issues/2695)</span><span class="sxs-lookup"><span data-stu-id="a94f5-187">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

- <span data-ttu-id="a94f5-188">La modalità dettagliata di nuget.exe deve mostrare l'URL di download - [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="a94f5-188">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

- <span data-ttu-id="a94f5-189">Spostare NuGet xplat in Microsoft.NetCore.App e netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="a94f5-189">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

- <span data-ttu-id="a94f5-190">Push - dovrebbe essere possibile eseguire l'override del server di simboli quando di esegue il push dalla riga di comando - [#2348](https://github.com/NuGet/Home/issues/2348)</span><span class="sxs-lookup"><span data-stu-id="a94f5-190">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

- <span data-ttu-id="a94f5-191">Consolidare il codice per la ricerca del percorso dei pacchetti globale - [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="a94f5-191">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

- <span data-ttu-id="a94f5-192">È necessario un nome migliore rispetto a suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span><span class="sxs-lookup"><span data-stu-id="a94f5-192">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

- <span data-ttu-id="a94f5-193">Determinare il nome della dipendenza `project.json` da usare per i progetti MSBuild - [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="a94f5-193">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

- <span data-ttu-id="a94f5-194">Aggiungere il supporto di SemVer 2.0.0 a NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span><span class="sxs-lookup"><span data-stu-id="a94f5-194">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

- <span data-ttu-id="a94f5-195">Consentire ai pacchetti NuGet con dipendenza transitiva con `.targets` di essere disponibili in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="a94f5-195">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

- <span data-ttu-id="a94f5-196">Il ripristino NuGet da riga di comando è molto più lento rispetto a Visual Studio - [#3330](https://github.com/NuGet/Home/issues/3330)</span><span class="sxs-lookup"><span data-stu-id="a94f5-196">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

- <span data-ttu-id="a94f5-197">Impostare il confronto di versione e ID dei pacchetti in modo da non fare distinzione tra maiuscole e minuscole - [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="a94f5-197">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

- <span data-ttu-id="a94f5-198">L'opzione NoCache non funziona per operazioni di ripristino/installazione basate su `packages.config` (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="a94f5-198">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

- <span data-ttu-id="a94f5-199">Per le risorse FindPackageByIdResource sono necessari un contesto di cache e un logger predefiniti - [#1357](https://github.com/NuGet/Home/issues/1357)</span><span class="sxs-lookup"><span data-stu-id="a94f5-199">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
