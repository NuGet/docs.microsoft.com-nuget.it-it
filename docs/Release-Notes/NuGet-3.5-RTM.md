---
title: Note sulla versione Beta di NuGet 3.5 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 082a96b9-607b-4225-864d-e1cea537f591
description: "Note sulla versione per NuGet 3.5 incluso dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "3.5 NuGet note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0a0f039d2529e1d41bbc0c7f9ac3f76f51f96ce5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
#<a name="nuget-35-release-notes"></a><span data-ttu-id="123a0-104">Note sulla versione 3.5 di NuGet</span><span class="sxs-lookup"><span data-stu-id="123a0-104">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="123a0-105">[Note sulla versione 3.5 RC NuGet](../release-notes/nuget-3.5-RC.md) | [note sulla versione RC NuGet 4.0](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="123a0-105">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="123a0-106">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="123a0-106">Bug Fixes</span></span>

* <span data-ttu-id="123a0-107">Service Pack non utilizza MSBuild 14.1 su mono - [&#3550;](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="123a0-107">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="123a0-108">Scheda di aggiornamento non consente di selezionare la versione più recente versione installata corrente seleziona - invece di aggiornare [&#3498;](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="123a0-108">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="123a0-109">Correzione di arresto anomalo dopo l'autenticazione una privata v2 feed MyGet e facendo clic su "Show x più risultati"- [&#3469;](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="123a0-109">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="123a0-110">Messaggi di log sembrano essere in ordine inverso per l'interfaccia utente - [&#3446;](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="123a0-110">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="123a0-111">V3.4.4 - ripristino Nuget genera un'eccezione "il formato del percorso specificato non è supportato -" [&#3442;](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="123a0-111">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="123a0-112">NuGet cmdLine 3.6 beta non rispetta - Prop Configuration = Release - [&#3432;](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="123a0-112">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="123a0-113">Installare NuGet IKVM lento nel progetto di grandi dimensioni - [&#3428;](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="123a0-113">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="123a0-114">Update - Self tiene in aggiornarsi - NuGet.exe [&#3395;](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="123a0-114">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="123a0-115">installazione e ripristino 3.5 da condivisione UNC offre prestazioni regressione da 3.4.4 - [&#3355;](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="123a0-115">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="123a0-116">Errore durante l'installazione di Moq dalla gestione dei pacchetti dell'interfaccia utente per un progetto net451 - [&#3349;](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="123a0-116">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="123a0-117">Installazione della scheda a livello di soluzione non mostra la versione del pacchetto - [&#3339;](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="123a0-117">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="123a0-118">xproj `project.json` aggiornamento dalla scheda installato perde lo stato - [&#3303;](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="123a0-118">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="123a0-119">Pacchetto NuGet in `.csproj` Ignora elemento file vuoti in `.nuspec` file - [&#3257;](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="123a0-119">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="123a0-120">Progetti di siti Web ospitati in IIS non dovrebbero causare ripristino esito negativo - [&#3235;](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="123a0-120">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="123a0-121">Credenziali non recuperate da NuGet. config quando endpoint v3 reindirizza a v2 - [&#3179;](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="123a0-121">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="123a0-122">Pacchetto NuGet non riesce a risolvere l'assembly durante il recupero dei metadati dell'assembly portabile - [&#3128;](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="123a0-122">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="123a0-123">Impossibile trovare NuGet `msbuild.exe` su Mono - [&#3085;](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="123a0-123">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="123a0-124">NuGet.exe pack non consente un tag di pre-release che inizia con numeri - [&#1743;](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="123a0-124">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="123a0-125">installazione del pacchetto NuGet non riesce in VS2015E - [&#1298;](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="123a0-125">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="123a0-126">attributo allowedversions valido Filtra non lavorativi a livello di soluzione - [&#333;](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="123a0-126">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="123a0-127">Ripristino non riesce in modo casuale con un elemento con la stessa chiave è già stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="123a0-127">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="123a0-128"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="123a0-128"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="123a0-129">Non è possibile installare Nuget.Common in `.csproj`  -  [&#2635;](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="123a0-129">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="123a0-130">Quando si utilizza l'interfaccia utente per la ricerca di un'origine V2, FindPackagesById viene chiamato due volte per ogni ID - [&#2517;](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="123a0-130">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="123a0-131">Pacchetti non possono dipendere da progetti - [&#2490;](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="123a0-131">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="123a0-132">NuGet.exe pack - Exclude è documentato ma non supportato - [&#2284;](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="123a0-132">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="123a0-133">I messaggi di problemi con l'errore quando la sezione 'contentFiles' di `.nuspec` non è valido - [&#1686;](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="123a0-133">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="123a0-134">Push invia sempre l'intero pacchetto due volte con autenticato origini pacchetto - [&#1501;](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="123a0-134">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="123a0-135">È stata fornita alcuna informazione quando la chiamata a nuget.exe *. csproj update durante il progetto non dispone di un `packages.config`  -  [&#1496;](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="123a0-135">No information was given when calling nuget.exe update *.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="123a0-136">`packages.config`Restore non tenterà sui codici di stato 5xx da origini V2 - [&#1217;](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="123a0-136">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="123a0-137">Coppia di punti nel file src in `.nuspec` non funziona - [&#2947;](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="123a0-137">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="123a0-138">È necessario ignorare i feed con crittografia - ripristino CoreCLR [&#2942;](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="123a0-138">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="123a0-139">NuGet.exe push gestione 403 - richiesta in modo non corretto di credenziali - [&#2910;](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="123a0-139">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="123a0-140">Gestione pacchetti NuGet aggiornamento rimuove il `project.json`  -  [&#2888;](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="123a0-140">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="123a0-141">NuGet.PackageManagement.VisualStudio tenta di caricare "NuGet.TeamFoundationServer14", ma che il nome DLL modificato in "NuGet.TeamFoundationServer" - [&#2857;](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="123a0-141">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="123a0-142">Pacchetto di gestione dell'interfaccia utente non viene visualizzato appena aggiornata versione - [&#2828;](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="123a0-142">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="123a0-143">pacchetto di aggiornamento sta tentando di utilizzare packageid, versione anziché package.version - [&#2771;](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="123a0-143">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="123a0-144">NuGet restore csproj deve errore se il progetto non usa nuget (`packages.config` o `project.json`)- [&#2766;](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="123a0-144">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="123a0-145">Errore di TFS "[file] non venga rilevato nell'area di lavoro o non si dispone dell'autorizzazione per accedervi" durante l'aggiornamento o la disinstallazione quando soluzione/progetto è associato al controllo del codice sorgente TFS - [&#2739;](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="123a0-145">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="123a0-146">pacchetto di aggiornamento non ottiene le dipendenze per i pacchetti non-destinazione - [&#2724;](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="123a0-146">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="123a0-147">Non è possibile impostare il livello di dettaglio i log per le azioni dell'interfaccia utente di gestione del pacchetto Nuget - [&#2705;](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="123a0-147">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="123a0-148">la configurazione NuGet non è valida - VS 2015 VSIX (v3.4.3) - [&#2667;](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="123a0-148">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="123a0-149">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) non funziona - [&#2653;](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="123a0-149">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="123a0-150">ottenere valore non può essere null in fase di compilazione - pacchetto NuGet versione 3.4.3 versione - [&#2648;](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="123a0-150">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="123a0-151">ripristino non utilizza credenziali archiviate da NuGet. config per i feed di VSTS - [&#2647;](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="123a0-151">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="123a0-152">[dotnet ripristino] - configfile è relativo alla directory di progetto anziché il comando dir cmd - [&#2639;](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="123a0-152">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="123a0-153">Le allocazioni eccessive nel codice di confronto versione - [&#2632;](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="123a0-153">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="123a0-154">Più istanze di nuget.exe sta tentando di installare lo stesso pacchetto in paralleli fa sì che un'operazione di scrittura double - [&#2628;](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="123a0-154">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="123a0-155">Informazioni sulle dipendenze non è stato memorizzato nella cache per le operazioni multiprogetto - [&#2619;](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="123a0-155">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="123a0-156">Installare e aggiornare i pacchetti di download senza verificare la cartella pacchetti innanzitutto - [&#2618;](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="123a0-156">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="123a0-157">Se l'elenco di origine del pacchetto è vuoto, non è possibile aggiungere l'origine del pacchetto tramite l'interfaccia utente (NuGet 3.4.x)- [&#2617;](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="123a0-157">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="123a0-158">Fuorviante errore durante il tentativo di installare il pacchetto che dipende dalla fase di progettazione aspetti - [&#2594;](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="123a0-158">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="123a0-159">Installa un pacchetto dalla console PackageManager con l'impostazione "All" tenta prima origine - [&#2557;](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="123a0-159">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="123a0-160">Versione beta più recente non decompressione ModernHttpClient - [&#2518;](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="123a0-160">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="123a0-161">Arresto anomalo di VS2015 all'avvio con NuGet self-compilato 3.4.1 - [&#2419;](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="123a0-161">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="123a0-162">Comando di aggiornamento potrebbe essere più dettagliato se i richiede che sia necessaria.... - [&#2418;](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="123a0-162">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="123a0-163">VSIX compilato localmente la compilazione di CI deve essere la stessa DLL e file.</span><span class="sxs-lookup"><span data-stu-id="123a0-163">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="123a0-164"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="123a0-164"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="123a0-165">Risolvere gli avvisi di downgrade di NuGet nella compilazione - [&#2396;](https://github.com/NuGet/Home/issues/2396)</span><span class="sxs-lookup"><span data-stu-id="123a0-165">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="123a0-166">Impossibile autenticare l'origine del pacchetto (3 volte) è bloccato per sempre - [&#2362;](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="123a0-166">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="123a0-167">Contenuto del pacchetto non verrà ripristinato correttamente quando si installa un pacchetto da nuget 3.3 + feed con l'argomento - NoCache quando il pacchetto contiene `.nupkg` file - [&#2354;](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="123a0-167">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="123a0-168">Installazione di NuGet con tutte le origini del pacchetto, ma pacchetto mancante dall'1 origine, non viene completata - [&#2322;](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="123a0-168">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="123a0-169">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [&#2285;](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="123a0-169">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="123a0-170">Installare blocchi se una singola origine si verifica un errore di autorizzazione - [&#2034;](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="123a0-170">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="123a0-171">`.nuspec`versione intervallo deve eseguire l'override di versione - IncludeReferencedProjects - [&#1983;](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="123a0-171">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="123a0-172">Pacchetto di aggiornamento rallentare super - "il tentativo di raccogliere informazioni sulle dipendenze" - [&#1909;](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="123a0-172">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="123a0-173">Creare un pacchetto NuGet punta a downgrade quando batch l'aggiornamento delle relative dipendenze - [&#1903;](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="123a0-173">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="123a0-174">aggiornamento di NuGet.exe elimina il nome sicuro dell'assembly e l'attributo privata.</span><span class="sxs-lookup"><span data-stu-id="123a0-174">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="123a0-175"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="123a0-175"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="123a0-176">Percorso relativo del file per "DefaultPushSource" - [&#1746;](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="123a0-176">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="123a0-177">Migliorare i messaggi di errore di sistema di risoluzione - [&#1373;](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="123a0-177">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="123a0-178">pacchetto di aggiornamento v3 non riesce con pacchetti non nell'origine specificata - [&#1013;](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="123a0-178">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="123a0-179">Utilizzando i percorsi relativi per le origini pacchetto risulta problematico per utilizzare - [&#865;](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="123a0-179">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="123a0-180">Manca una dipendenza nel file NUPKG generato dal progetto se dipendenza indiretta esiste già con un requisito di versione inferiore - [&#759;](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="123a0-180">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="123a0-181">Eliminazione di un progetto chiude una finestra dell'interfaccia utente corrispondente, ma la ridenominazione di un progetto non comporta la ridenominazione la finestra dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="123a0-181">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="123a0-182">Si noti che è in ascolto PMC ridenominazione del progetto e di eventi nei progetti remove - [&#670;](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="123a0-182">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="123a0-183">[Willow carico di lavoro Web] Creazione Razor v3 WSP si blocca - [&#3241;](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="123a0-183">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="123a0-184">Installazione o il ripristino di un particolare pacchetto ha esito negativo con "Pacchetto contiene più file nuspec."</span><span class="sxs-lookup"><span data-stu-id="123a0-184">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="123a0-185"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="123a0-185"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="123a0-186">Minuscolo ID & `packages.config` scenari - [&#3209;](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="123a0-186">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="123a0-187">[-beta2 3.5] Ripristino del pacchetto non riesce a ripristinare i pacchetti "legacy" - [&#3208;](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="123a0-187">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="123a0-188">pacchetto NuGet aggiunge in modo forzato file con estensione tt alla cartella del contenuto indipendentemente - [&#3203;](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="123a0-188">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="123a0-189">pacchetto di aggiornamento dell'app web ASP.NET genera l'avviso relativo al file: origine - [&#3194;](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="123a0-189">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="123a0-190">NuGet pack csproj (con `project.json`) si blocca se sono non presenti packOptions e proprietario nel file JSON - [&#3180;](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="123a0-190">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="123a0-191">pacchetto NuGet per `project.json` ignora i tag packOptions come riepilogo, gli autori e proprietari e così via - [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="123a0-191">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="123a0-192">NullReferenceException tramite NuGet.Packaging.PhysicalPackageFile.GetStream - [&#3160;](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="123a0-192">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="123a0-193">Pacchetto NuGet ignora le dipendenze nell'output `.nuspec` per `project.json`  -  [&#3145;](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="123a0-193">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="123a0-194">Aggiornamento di più pacchetti con rollback lascia il progetto in uno stato danneggiato - [&#3139;](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="123a0-194">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="123a0-195">ContentFiles in presenza non vengono aggiunti per i progetti di moniker netstandard - [&#3118;](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="123a0-195">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="123a0-196">Impossibile creare pacchetto libreria per .net Standard correttamente - [&#3108;](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="123a0-196">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="123a0-197">File -> Nuovo progetto -> ha esito negativo al progetto libreria di classi (portabile) VS2015 e Dev15 - [&#3094;](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="123a0-197">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="123a0-198">Errore di NuGet - 1.0.0-* non è una stringa di versione valida - [&#3070;](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="123a0-198">nuGet error - 1.0.0-* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="123a0-199">Find-Package ha esito negativo per la visualizzazione, ma il funzionamento di Install-Package - [&#3068;](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="123a0-199">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="123a0-200">Errore quando "Install-Package jquery.validation" in dev15 - [&#3061;](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="123a0-200">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="123a0-201">passa al percorso di destinazione non valida - pacchetto NuGet di xproj [&#3060;](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="123a0-201">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="123a0-202">Quando è installato Visual Studio 2015 update 3 in un Visual Studio che usa NuGet si verifica l'errore di versione 3.5.0 - [&#3053;](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="123a0-202">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="123a0-203">"Bloccata da Packages" in `project.json` (UWP, dette anche compilazione integrato) progetto - [&#3046;](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="123a0-203">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="123a0-204">aggiornare dotnet cli installato dallo script di compilazione per preview2-003121, la compilazione di preview2 ufficiale.</span><span class="sxs-lookup"><span data-stu-id="123a0-204">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="123a0-205"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="123a0-205"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="123a0-206">Pacchetto interfaccia utente di gestione: non visualizza una nuova versione dopo aver aggiornato un pacchetto- [&#3041;](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="123a0-206">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="123a0-207">-ApiKey nella riga di comando di eliminazione non viene in lettura/inviata 3.5.0-beta - [&#3037;](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="123a0-207">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="123a0-208">Stringa non corretto: una versione stabile di un pacchetto non deve avere in una versione non definitiva dipendenza.</span><span class="sxs-lookup"><span data-stu-id="123a0-208">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="123a0-209"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="123a0-209"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="123a0-210">Cache OptimizedZipPackage lascia le cartelle vuote - [&#3029;](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="123a0-210">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="123a0-211">Creazione di get progetto PCL (net46 e windows 10) NullRef eccezione.</span><span class="sxs-lookup"><span data-stu-id="123a0-211">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="123a0-212"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="123a0-212"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="123a0-213">Aggiornamento di NuGet deve fornire un messaggio informativo quando una versione successiva è limitata dal vincolo di attributo allowedversions valido - [&#3013;](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="123a0-213">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="123a0-214">Problemi di ripristino NuGet v3 - [&#2891;](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="123a0-214">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="123a0-215">Plug-in credenziali chiuso con errore -1 / errore di download del pacchetto quando si utilizzano provider di credenziali con più origini - [&#2885;](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="123a0-215">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="123a0-216">`project.json`ripristino NuGet comporta la ricompilazione quando non modificato - [&#2817;](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="123a0-216">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="123a0-217">Pacchetti di simboli non devono mai essere utilizzato nell'installazione o aggiornamento - [&#2807;](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="123a0-217">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="123a0-218">Visual Studio non supporta le variabili di ambiente in repositoryPath (nuget.exe non) - [&#2763;](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="123a0-218">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="123a0-219">Etichetta di UIElement senza etichetta nel Package Manager UI per l'accessibilità - [&#2745;](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="123a0-219">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="123a0-220">Framework portabili con profili sillabati vengono rifiutate.</span><span class="sxs-lookup"><span data-stu-id="123a0-220">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="123a0-221"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="123a0-221"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="123a0-222">Gestione pacchetti NuGet deve mettere in evidenza tale elenco di opzioni in dettaglio non è valida per i pacchetti `project.json`  -  [&#2665;](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="123a0-222">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="123a0-223">NuGet.exe push/delete non utilizzano la chiave API - [&#2627;](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="123a0-223">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="123a0-224">Rimuovere la proprietà bloccata dal file di blocco - [&#2379;](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="123a0-224">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="123a0-225">NuGet 3.3.0 aggiornamento ha esito negativo con '... un vincolo aggiuntivo definito nel file Packages. config impedisce questa operazione.'</span><span class="sxs-lookup"><span data-stu-id="123a0-225">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="123a0-226"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="123a0-226"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="123a0-227">L'installazione del pacchetto da un'origine locale che non esiste genera un messaggio fittizio - [&#1674;](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="123a0-227">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="123a0-228">"Aggiornamento disponibile" filtro consente di visualizzare gli aggiornamenti che violano il vincolo di versione - [&#1094;](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="123a0-228">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="123a0-229">Impossibile aggiornare i pacchetti nativi - [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="123a0-229">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="123a0-230">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="123a0-230">Features</span></span>

* <span data-ttu-id="123a0-231">Supporta l'impostazione CopyLocal su false nei riferimenti aggiunti da NuGet - [&#329;](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="123a0-231">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="123a0-232">il supporto per MSBuild 15 - NuGet.exe [&#1937;](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="123a0-232">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="123a0-233">Supporto per Pack.`csproj`</span><span class="sxs-lookup"><span data-stu-id="123a0-233">Pack support for .`csproj`</span></span><span data-ttu-id="123a0-234"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="123a0-234"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="123a0-235">Disabilitare l'intervento dell'utente quando sono presenti azioni dell'utente in esecuzione- [&#1440;](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="123a0-235">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="123a0-236">NuGet è necessario aggiungere il supporto per `runtimes/{rid}/nativeassets/{txm}/`  -  [&#2782;](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="123a0-236">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="123a0-237">Compatibilità di framework mancante in NuGet aggiungere 2. x (che sono già in 3. x) - [&#2720;](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="123a0-237">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="123a0-238">Supporto per le cartelle pacchetto fallback - [&#2899;](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="123a0-238">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="123a0-239">Progettare e implementare una nozione di tipo di pacchetto per supportare i pacchetti strumento - [&#2476;](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="123a0-239">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="123a0-240">Aggiungere un'API per ottenere il percorso della cartella di pacchetti globale - [&#2403;](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="123a0-240">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="123a0-241">Abilitare SemVer 2.0.0 Pack - [&#3356;](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="123a0-241">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="123a0-242">DCR</span><span class="sxs-lookup"><span data-stu-id="123a0-242">DCRs</span></span>

* <span data-ttu-id="123a0-243">NuGet.exe push: parametro di timeout non funziona - [&#2785;](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="123a0-243">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="123a0-244">Testo della descrizione del pacchetto deve essere selezionabile - [&#1769;](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="123a0-244">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="123a0-245">Abilitare nuget.exe per produrre `.props` e `.targets` file per `.nuproj` progetti [&#2711;](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="123a0-245">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="123a0-246">Aggiungere l'API da confrontare con importazioni - Framework di estendibilità [&#2633;](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="123a0-246">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="123a0-247">Nascondere le opzioni di dipendenza quando si utilizza `project.json`  -  [&#2486;](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="123a0-247">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="123a0-248">Stampa l'intestazione di versione nuget.exe in output dettagliato - [&#1887;](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="123a0-248">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="123a0-249">NuGet è necessario informare gli utenti che l'aggiornamento o l'installazione in un tfm dotnet basato su PCL potrebbe provocare problemi - [&#3138;](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="123a0-249">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="123a0-250">Installazione/aggiornamento non valido per il progetto con tfm Avvisa = "dotnet" - [&#3137;](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="123a0-250">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="123a0-251">Risolvere i problemi di prestazioni con ReShaper e NuGet per l'aggiornamento - [&#3044;](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="123a0-251">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="123a0-252">Aggiungere il supporto netcoreapp11 e netstandard17 - [&#2998;](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="123a0-252">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="123a0-253">Attributo AssemblyMetadata sfruttare per `.nuspec` token sostituzioni - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="123a0-253">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
