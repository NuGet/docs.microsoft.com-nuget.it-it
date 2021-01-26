---
title: Note sulla versione per NuGet 3.5 RTM
description: Note sulla versione per NuGet 3,5, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776346"
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="49332-103">Note sulla versione di NuGet 3,5</span><span class="sxs-lookup"><span data-stu-id="49332-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="49332-104">Note sulla versione [di NuGet 3,5-RC](../release-notes/nuget-3.5-RC.md)  |  [Note sulla versione di NuGet 4,0 RC](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="49332-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="49332-105">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="49332-105">Bug Fixes</span></span>

* <span data-ttu-id="49332-106">Pack non usa MSBuild 14,1 in mono- [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="49332-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="49332-107">Aggiornamento scheda non selezionare la versione disponibile più recente da aggiornare invece selezionare versione installata corrente- [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="49332-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="49332-108">Correzione dell'arresto anomalo dopo l'autenticazione di un feed MyGet privato V2 e facendo clic su "Mostra altri x risultati"- [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="49332-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="49332-109">I messaggi di log sembrano essere in ordine inverso per l'interfaccia utente- [#3446](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="49332-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="49332-110">v 3.4.4-il ripristino di NuGet genera "il formato del percorso specificato non è supportato"- [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="49332-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="49332-111">NuGet cmdLine 3,6 beta non rispetta-prop Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="49332-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="49332-112">Installazione lenta di NuGet IKVM in un progetto di grandi dimensioni- [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="49332-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="49332-113">Aggiornamento nuget.exe-self mantiene l'aggiornamento autonomo- [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="49332-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="49332-114">3,5 l'installazione o il ripristino dalla condivisione UNC presenta una regressione delle prestazioni da 3.4.4- [#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="49332-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="49332-115">Errore durante l'installazione di MOQ dall'interfaccia utente di gestione pacchetti per un progetto net451- [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="49332-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="49332-116">La scheda Installa a livello di soluzione non Mostra la versione del pacchetto [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="49332-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="49332-117">l' `project.json` aggiornamento di xproj dalla scheda installata perde lo stato [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="49332-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="49332-118">Il pacchetto NuGet in `.csproj` Ignora l'elemento file vuoti nel `.nuspec` file- [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="49332-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="49332-119">I progetti di siti Web ospitati in IIS non devono causare la mancata riuscita del ripristino [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="49332-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="49332-120">Le credenziali non vengono recuperate da Nuget.Config quando l'endpoint V3 viene reindirizzato alla versione v2- [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="49332-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="49332-121">Il pacchetto NuGet non riesce a risolvere l'assembly durante il recupero dei metadati dell'assembly portabile- [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="49332-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="49332-122">Impossibile trovare NuGet `msbuild.exe` in mono- [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="49332-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="49332-123">nuget.exe Pack non consente un tag di versione non definitiva che inizia con numeri- [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="49332-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="49332-124">l'installazione del pacchetto NuGet non riesce in VS2015E- [#1298](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="49332-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="49332-125">il filtro allowedVersions non funziona a livello di soluzione- [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="49332-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="49332-126">Il ripristino ha esito negativo in modo casuale ed è già stato aggiunto un elemento con la stessa chiave.</span><span class="sxs-lookup"><span data-stu-id="49332-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="49332-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="49332-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="49332-128">Impossibile installare NuGet. Common in `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="49332-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="49332-129">Quando si usa l'interfaccia utente per cercare un'origine V2, FindPackagesById viene chiamato due volte per ogni ID [#2517](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="49332-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="49332-130">I pacchetti non possono dipendere da progetti- [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="49332-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="49332-131">nuget.exe Pack-Exclude è documentato ma non supportato- [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="49332-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="49332-132">Problemi con i messaggi di errore quando la sezione ' contentFiles ' di `.nuspec` non è valida [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="49332-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="49332-133">Push invia sempre due volte l'intero pacchetto con le origini dei pacchetti autenticati- [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="49332-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="49332-134">Non sono state fornite informazioni durante la chiamata di nuget.exe Update \*. csproj mentre il progetto non dispone di un `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="49332-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="49332-135">`packages.config` il ripristino non ritenta sui codici di stato di 5xx da V2 origini- [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="49332-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="49332-136">Il doppio punto nel file src in `.nuspec` non funziona [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="49332-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="49332-137">Il ripristino di CoreCLR deve ignorare i feed con la crittografia [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="49332-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="49332-138">Gestione nuget.exe push 403: richiesta non corretta per le credenziali- [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="49332-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="49332-139">L'aggiornamento di NuGet tramite Gestione pacchetti rimuove le proprietà dalla `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="49332-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="49332-140">NuGet. PackageManagement. VisualStudio tenta di caricare "NuGet. TeamFoundationServer14", ma il nome della DLL è stato modificato in "NuGet. TeamFoundationServer"- [#2857](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="49332-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="49332-141">L'interfaccia utente di gestione pacchetti non Mostra la nuova versione aggiornata- [#2828](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="49332-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="49332-142">Update-Package che tenta di usare PackageID, Version anziché Package. Version- [#2771](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="49332-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="49332-143">NuGet Restore csproj dovrebbe essere errore se il progetto non usa NuGet ( `packages.config` o `project.json` )- [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="49332-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="49332-144">Errore TFS "[file] non trovato nell'area di lavoro oppure non si dispone dell'autorizzazione per accedervi" durante l'aggiornamento o la disinstallazione quando soluzione/progetto è associato al controllo del codice sorgente TFS- [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="49332-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="49332-145">il pacchetto di aggiornamento non ottiene le dipendenze per i pacchetti non di destinazione- [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="49332-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="49332-146">Non è possibile impostare il livello di dettaglio dei log per le azioni dell'interfaccia utente di gestione pacchetti NuGet- [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="49332-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="49332-147">la configurazione di NuGet non è valida-VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="49332-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="49332-148">DefaultPushSource `NuGetDefaults.Config` ( `ProgramData\NuGet` ) non funziona- [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="49332-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="49332-149">versione di NuGet 3.4.3: il recupero del valore non può essere null nella compilazione del pacchetto: [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="49332-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="49332-150">il ripristino non usa le credenziali archiviate da Nuget.Config per i feed VSTS- [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="49332-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="49332-151">[dotnet restore]--configfile è relativo alla directory del progetto anziché alla directory cmd- [#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="49332-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="49332-152">Allocazioni eccessive nel codice di comparsing delle versioni- [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="49332-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="49332-153">Più istanze di nuget.exe tentativo di installare lo stesso pacchetto in parallelo causano una doppia scrittura [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="49332-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="49332-154">Le informazioni sulle dipendenze non vengono memorizzate nella cache per le operazioni multiprogetto- [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="49332-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="49332-155">Installare e aggiornare i pacchetti di download senza controllare prima la cartella Packages- [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="49332-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="49332-156">Se l'elenco di origine del pacchetto è vuoto, non è possibile aggiungere l'origine del pacchetto tramite l'interfaccia utente (NuGet 3.4. x)- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="49332-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="49332-157">Errore fuorviante durante il tentativo di installare il pacchetto che dipende dalle facciate della fase di progettazione. [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="49332-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="49332-158">L'installazione di un pacchetto dalla console di PackageManager con l'impostazione "All" prova solo la prima origine- [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="49332-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="49332-159">Beta più recente non decomprimere ModernHttpClient- [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="49332-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="49332-160">Arresto anomalo VS2015 all'avvio con NuGet a compilazione automatica 3.4.1- [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="49332-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="49332-161">Il comando Update potrebbe essere leggermente più dettagliato se lo chiedo...- [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="49332-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="49332-162">Il progetto VSIX compilato localmente deve avere le stesse dll e file della compilazione CI.</span><span class="sxs-lookup"><span data-stu-id="49332-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="49332-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="49332-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="49332-164">Correggere gli avvisi di downgrade NuGet nel [#2396](https://github.com/NuGet/Home/issues/2396) di compilazione</span><span class="sxs-lookup"><span data-stu-id="49332-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="49332-165">Non è possibile autenticare l'origine del pacchetto (3 volte). il blocco è sempre [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="49332-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="49332-166">Il contenuto del pacchetto non viene ripristinato correttamente quando si installa un pacchetto da un feed NuGet v 3.3 + con l'argomento-NoCache quando il pacchetto contiene `.nupkg` file- [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="49332-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="49332-167">L'installazione di NuGet con tutte le origini dei pacchetti, ma il pacchetto mancante da 1 origine, non riesce [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="49332-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="49332-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet. PackageManagement. VisualStudio. VSMSBuildNuGetProjectSystem + \* lt; &gt; c__DisplayClass_0 + &lt; &lt; AddReference &gt; B__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="49332-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="49332-169">Installa i blocchi se un'unica origine non riesce a eseguire l'autorizzazione- [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="49332-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="49332-170">`.nuspec` l'intervallo di versioni deve eseguire l'override della versione-IncludeReferencedProjects- [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="49332-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="49332-171">Update-Package Super Slow: "tentativo di raccogliere informazioni sulle dipendenze"- [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="49332-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="49332-172">Pacchetto di downgrade Stealth di NuGet quando batch Aggiorna le dipendenze- [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="49332-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="49332-173">nuget.exe aggiornamento elimina il nome sicuro e l'attributo privato dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="49332-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="49332-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="49332-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="49332-175">Percorso file relativo per "DefaultPushSource"- [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="49332-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="49332-176">Migliorare i messaggi di errore del resolver- [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="49332-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="49332-177">Update-Package in V3 ha esito negativo con i pacchetti non inclusi nell'origine specificata: [#1013](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="49332-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="49332-178">L'uso di percorsi relativi per le origini dei pacchetti è problematico per l'uso di- [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="49332-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="49332-179">Dipendenza mancante nel file NUPKG generato dal progetto se esiste già una dipendenza indiretta con un requisito di versione inferiore- [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="49332-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="49332-180">L'eliminazione di un progetto chiude la finestra dell'interfaccia utente corrispondente, ma la ridenominazione di un progetto non Rinomina la finestra dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="49332-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="49332-181">Si noti che la console di gestione delle attività è in ascolto della ridenominazione del progetto e degli [#670](https://github.com/NuGet/Home/issues/670) eventi di rimozione</span><span class="sxs-lookup"><span data-stu-id="49332-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="49332-182">[Carico di lavoro Web Willow] Creazione di blocchi WSP per Razor v3- [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="49332-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="49332-183">L'installazione/ripristino di un particolare pacchetto ha esito negativo con "il pacchetto contiene più file nuspec".</span><span class="sxs-lookup"><span data-stu-id="49332-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="49332-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="49332-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="49332-185">Scenari con ID minuscolo & `packages.config` - [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="49332-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="49332-186">[3,5-beta2] Il ripristino del pacchetto non riesce a ripristinare i pacchetti "Legacy"- [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="49332-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="49332-187">il pacchetto NuGet aggiunge in modo forzato i file con estensione TT alla cartella del contenuto indipendentemente dalla [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="49332-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="49332-188">Update-Package dell'app Web ASP.NET genera un avviso relativo al file: Source- [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="49332-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="49332-189">NuGet Pack csproj (con `project.json` ) si arresta in modo anomalo se non sono presenti packOptions e Owner nel file JSON [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="49332-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="49332-190">il pacchetto NuGet per `project.json` Ignora i tag packOptions come Summary, authors, owners e così via [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="49332-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="49332-191">NullReferenceException tramite NuGet. Packaging. PhysicalPackageFile. GetStream- [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="49332-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="49332-192">Il pacchetto NuGet ignora le dipendenze nell'output `.nuspec` per `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="49332-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="49332-193">L'aggiornamento di più pacchetti con rollback lascia il progetto in uno stato di interruzione- [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="49332-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="49332-194">ContentFiles in any non sono stati aggiunti per i progetti netstandard- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="49332-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="49332-195">Non è possibile creare un pacchetto della libreria di destinazione .NET standard correttamente- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="49332-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="49332-196">File > nuovo progetto-> progetto libreria di classi (portabile) non riesce in VS2015 e Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="49332-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="49332-197">errore nuGet-1.0.0-\* non è una stringa di versione valida- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="49332-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="49332-198">Find-Package non viene visualizzato ma Install-Package funziona- [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="49332-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="49332-199">Errore durante "Install-Package jQuery. Validation" in dev15- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="49332-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="49332-200">il pacchetto NuGet di xproj viene impostato per impostazione predefinita su percorso di destinazione non valido: [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="49332-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="49332-201">Quando si esegue l'installazione di Visual Studio 2015 Update 3 su un Visual Studio che usa la versione NuGet 3.5.0 si verifica un errore [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="49332-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="49332-202">Progetto "bloccato da packages.config" in `project.json` (UWP, a. k. a Build Integrated) [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="49332-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="49332-203">aggiornare l'interfaccia della riga di comando DotNet installata dallo script di compilazione in Preview2-003121, che è la compilazione Preview2 ufficiale.</span><span class="sxs-lookup"><span data-stu-id="49332-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="49332-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="49332-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="49332-205">Interfaccia utente di gestione pacchetti: non Visualizza la nuova versione dopo l'aggiornamento di un pacchetto- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="49332-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="49332-206">-ApiKey nella riga di comando DELETE non è stato letto/inviato in 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="49332-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="49332-207">Stringa non corretta: una versione stabile di un pacchetto non deve avere una dipendenza della versione provvisoria.</span><span class="sxs-lookup"><span data-stu-id="49332-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="49332-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="49332-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="49332-209">La cache OptimizedZipPackage lascia cartelle vuote- [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="49332-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="49332-210">Creazione dell'eccezione NullRef del progetto PCL (' net46 e Windows 10).</span><span class="sxs-lookup"><span data-stu-id="49332-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="49332-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="49332-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="49332-212">L'aggiornamento di NuGet deve fornire un messaggio informativo quando una versione più alta è limitata dal vincolo allowedVersions- [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="49332-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="49332-213">Problemi di ripristino di NuGet V3- [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="49332-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="49332-214">Il plug-in delle credenziali è stato terminato con errore-1/errore durante il download del pacchetto quando si usano i provider di credenziali con più origini [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="49332-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="49332-215">`project.json` il ripristino di NuGet causa la ricompilazione quando non è stato modificato nulla [#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="49332-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="49332-216">I pacchetti di simboli non devono mai essere usati in installazione o aggiornamento- [#2807](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="49332-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="49332-217">VS non supporta variabili di ambiente in repositoryPath (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="49332-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="49332-218">Etichettare gli UIElement senza etichetta nell'interfaccia utente di gestione pacchetti per l'accessibilità- [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="49332-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="49332-219">I Framework portabili con profili con sillabazione vengono rifiutati.</span><span class="sxs-lookup"><span data-stu-id="49332-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="49332-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="49332-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="49332-221">Gestione pacchetti NuGet dovrebbe rendere chiaro che l'elenco di opzioni nei pacchetti non si applica ai `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="49332-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="49332-222">nuget.exe push/Delete non userà la chiave API- [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="49332-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="49332-223">Rimuovere la proprietà Locked dal file di blocco- [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="49332-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="49332-224">L'aggiornamento di NuGet 3.3.0 ha esito negativo con ' un vincolo aggiuntivo... definito in packages.config impedisce questa operazione.</span><span class="sxs-lookup"><span data-stu-id="49332-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="49332-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="49332-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="49332-226">L'installazione di un pacchetto da un'origine locale che non esiste genera un messaggio fasullo [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="49332-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="49332-227">Il filtro "aggiornamento disponibile" Mostra gli aggiornamenti che violano il vincolo di versione [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="49332-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="49332-228">Non è possibile aggiornare i pacchetti nativi- [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="49332-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="49332-229">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="49332-229">Features</span></span>

* <span data-ttu-id="49332-230">Supporto dell'impostazione di CopyLocal su false nei riferimenti aggiunti da NuGet- [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="49332-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="49332-231">Supporto nuget.exe per MSBuild 15- [#1937](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="49332-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="49332-232">Supporto di Pack per.`csproj`</span><span class="sxs-lookup"><span data-stu-id="49332-232">Pack support for .`csproj`</span></span><span data-ttu-id="49332-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="49332-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="49332-234">Disabilitare l'azione dell'utente quando sono in esecuzione azioni utente- [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="49332-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="49332-235">NuGet dovrebbe aggiungere il supporto per `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="49332-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="49332-236">Aggiungere le compatibilità del Framework mancanti in NuGet 2. x (che sono già in 3. x)- [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="49332-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="49332-237">Supporto per le cartelle dei pacchetti di fallback- [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="49332-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="49332-238">Progettare e implementare una nozione di tipo di pacchetto per supportare pacchetti di strumenti- [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="49332-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="49332-239">Aggiungere un'API per ottenere il percorso della cartella dei pacchetti globali- [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="49332-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="49332-240">Abilitare SemVer 2.0.0 in Pack- [#3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="49332-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="49332-241">DCR</span><span class="sxs-lookup"><span data-stu-id="49332-241">DCRs</span></span>

* <span data-ttu-id="49332-242">nuget.exe parametro di timeout push non funziona- [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="49332-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="49332-243">Il testo della descrizione del pacchetto deve essere selezionabile- [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="49332-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="49332-244">Abilitare nuget.exe per produrre `.props` `.targets` i file e per i `.nuproj` progetti [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="49332-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="49332-245">Aggiungere l'API di estensibilità per confrontare i Framework con le importazioni- [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="49332-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="49332-246">Nascondi le opzioni di dipendenza quando si usa `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="49332-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="49332-247">Stampare l'intestazione della versione nuget.exe nell'output dettagliato- [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="49332-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="49332-248">NuGet deve informare gli utenti che l'aggiornamento o l'installazione in una libreria PCL basata su DotNet TFM può causare problemi: [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="49332-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="49332-249">Avviso di installazione/aggiornamento errato per il progetto w/TFM = "DotNet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="49332-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="49332-250">Risolvere i problemi di prestazioni con reshaping e NuGet per Update- [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="49332-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="49332-251">Aggiungere il supporto per netcoreapp11 e netstandard17- [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="49332-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="49332-252">Utilizzare l'attributo AssemblyMetadata per le `.nuspec` sostituzioni di token- [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="49332-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
