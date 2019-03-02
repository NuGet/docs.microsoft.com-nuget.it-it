---
title: Note sulla versione 5.0-preview di NuGet
description: Note sulla versione per le anteprime di NuGet 5.0, inclusi i problemi noti, correzioni di bug, nuove funzionalità e dcr.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 4b05dcb9a2960c1e3231e81d4b4c122d3a518753
ms.sourcegitcommit: 571644118e3c5a2fd818891d305b4b8de8ef21de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2019
ms.locfileid: "57225888"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="01c46-103">Note sulla versione di NuGet 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="01c46-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="01c46-104">Versioni di anteprima 5.0 di NuGet</span><span class="sxs-lookup"><span data-stu-id="01c46-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="01c46-105">27 febbraio 2019 - [NuGet 5.0 Preview 4](#whats-new-in-nuget-50-preview-4)</span><span class="sxs-lookup"><span data-stu-id="01c46-105">February 27, 2019 - [NuGet 5.0 Preview 4](#whats-new-in-nuget-50-preview-4)</span></span>
* <span data-ttu-id="01c46-106">13 febbraio 2019 - [NuGet 5.0 Preview 3](#whats-new-in-nuget-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="01c46-106">February 13, 2019 - [NuGet 5.0 Preview 3](#whats-new-in-nuget-50-preview-3)</span></span>
* <span data-ttu-id="01c46-107">23 gennaio 2019 - [NuGet 5.0 Preview 2](#whats-new-in-nuget-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="01c46-107">January 23, 2019 - [NuGet 5.0 Preview 2](#whats-new-in-nuget-50-preview-2)</span></span>

## <a name="whats-new-in-nuget-50-preview-4"></a><span data-ttu-id="01c46-108">What ' s New in NuGet 5.0 Preview 4</span><span class="sxs-lookup"><span data-stu-id="01c46-108">What's New in NuGet 5.0 Preview 4</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="01c46-109">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="01c46-109">Issues fixed in this release</span></span>

<span data-ttu-id="01c46-110">**Bug**</span><span class="sxs-lookup"><span data-stu-id="01c46-110">**Bugs**</span></span>

* <span data-ttu-id="01c46-111">NuGet.VisualStudio.IVsPackageInstaller - chiamata in un progetto con alcun pacchetto fa riferimento sempre Packages. config viene utilizzato, anche se il valore predefinito è impostato su PackageReference - [7005 #](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="01c46-111">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="01c46-112">PMC: Update-Package reinstallare ha esito negativo ("Impossibile trovare il pacchetto") nel venga rimosso dall'elenco dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="01c46-112">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="01c46-113"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="01c46-113"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="01c46-114">Aggiungi avviso di terze parti nel nostro repository e VSIX - [7409 #](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="01c46-114">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="01c46-115">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage consigliabile installare la versione più recente quando nessuna versione di base - [7493 #](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="01c46-115">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="01c46-116">-supporto interattivo per dotnet nuget push - [7519 #](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="01c46-116">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="01c46-117">Durante il ripristino con file di blocco, NU1603 avviso non deve essere generato.</span><span class="sxs-lookup"><span data-stu-id="01c46-117">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="01c46-118"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="01c46-118"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="01c46-119">NuGet non deve essere stampata percorso del progetto durante il ripristino con registrazione minima - [7647 #](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="01c46-119">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="01c46-120">-supporto interattivo per dotnet remove package - [7727 #](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="01c46-120">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="01c46-121">Aggiungere nuovo NuGet.Packaging.Core con attrs TypeForwardedTo - [7768 #](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="01c46-121">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="01c46-122">plugins_cache deve percorso più breve per funzionare bene - [7770 #](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="01c46-122">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="01c46-123">Preferire percorso per l'individuazione di msbuild, se l'utente non richieda la versione di msbuild specifica - [7786 #](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="01c46-123">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

<span data-ttu-id="01c46-124">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="01c46-124">**DCRs**</span></span>

* <span data-ttu-id="01c46-125">limitare il numero di richiesta http per ogni origine tramite NuGet. config - [4538 #](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="01c46-125">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="01c46-126">NuGet deve avere come destinazione Net472 (per consentire la compilazione di VSIX 16,0 pulizia) - [7143 #](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="01c46-126">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="01c46-127">PMC: Comando OpenPackagePage - Rimuovi [7384 #](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="01c46-127">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="01c46-128">Mappa di NetCoreApp 3.0 apportare a NetStandard 2.1 - [7762 #](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="01c46-128">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="01c46-129">Aggiungere il supporto netstandard2.0 pacchetti NuGet.\* - [6516 #](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="01c46-129">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>


## <a name="whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="01c46-130">What ' s New in NuGet 5.0 Preview 3</span><span class="sxs-lookup"><span data-stu-id="01c46-130">What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="01c46-131">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="01c46-131">Issues fixed in this release</span></span> 

<span data-ttu-id="01c46-132">**Bug**</span><span class="sxs-lookup"><span data-stu-id="01c46-132">**Bugs**</span></span>

* <span data-ttu-id="01c46-133">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="01c46-133">nuget.exe /?</span></span> <span data-ttu-id="01c46-134">dovrebbe elencare le versioni corrette di msbuild - [7794 #](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="01c46-134">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="01c46-135">NuGet.targets(498,5): error : Non è riuscito a trovare una parte del percorso "/ tmp/NuGetScratch - su mono - [7793 #](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="01c46-135">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="01c46-136">ripristino inutilmente enumera il contenuto di tutte le versioni del pacchetto di cui viene fatto riferimento nella cache del computer - [7639 #](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="01c46-136">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="01c46-137">Il rilevamento automatico MSBuild seleziona sempre 16.0 dopo l'installazione e 2019 di anteprima - [7621 #](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="01c46-137">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="01c46-138">elenco del pacchetto dotnet su una soluzione genera voci duplicate per framework - [7607 #](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="01c46-138">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="01c46-139">Eccezione "nome di percorso vuota non è valido" quando IVsPackageInstaller.InstallPackage chiamante nel vecchio progetti e pacchetti di cartella non esiste.</span><span class="sxs-lookup"><span data-stu-id="01c46-139">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="01c46-140"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="01c46-140"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="01c46-141">livello di dettaglio di MSBuild /t: Restore minimo deve essere più minimo - [4695 #](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="01c46-141">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="01c46-142">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="01c46-142">**DCRs**</span></span>

* <span data-ttu-id="01c46-143">Consentire agli autori di pacchetti di definire il comportamento transitiva gli asset di compilazione - [6091 #](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="01c46-143">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="01c46-144">Abilitare il ripristino in VS abbia esito positivo se un progetto non fa parte della soluzione o non è stato caricato, ma è stato ripristinato in precedenza - [5820 #](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="01c46-144">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="whats-new-in-nuget-50-preview-2"></a><span data-ttu-id="01c46-145">What ' s New in NuGet 5.0 Preview 2</span><span class="sxs-lookup"><span data-stu-id="01c46-145">What's New in NuGet 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="01c46-146">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="01c46-146">Issues fixed in this release</span></span>

<span data-ttu-id="01c46-147">**Bug**</span><span class="sxs-lookup"><span data-stu-id="01c46-147">**Bugs**</span></span>

* <span data-ttu-id="01c46-148">Visual Studio alla 16.0 UI NuGet sono disponibili schede illeggibile a causa di problemi di colore - [7735 #](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="01c46-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="01c46-149">NuGet. core e un chiarimento License di NuGet. Clients - [7629 #](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="01c46-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="01c46-150">Ripristino enumera inutilmente cartella globale dei pacchetti durante il tentativo di determinare il tipo - [7596 #](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="01c46-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="01c46-151">Errori di imposizione di file di blocco verranno visualizzate nel finestra Elenco errori - [7429 #](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="01c46-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="01c46-152">Risolvere i problemi di NuGet.Configuration - [7326 #](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="01c46-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="01c46-153">Adattare all'aggiornamento di MSBuild relativo percorso di installazione.</span><span class="sxs-lookup"><span data-stu-id="01c46-153">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="01c46-154">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="01c46-154">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="01c46-155">NuGet.Build.Tasks.Pack deve essere una dipendenza di sviluppo - [7249 #](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="01c46-155">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="01c46-156">Aggiungere il punto di estensione pack per l'inclusione di simboli - debug [7234 #](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="01c46-156">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="01c46-157">dotnet pack deve mantenere l'intervallo di versioni delle dipendenze nel pacchetto nupkg creato.</span><span class="sxs-lookup"><span data-stu-id="01c46-157">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="01c46-158">(anche se viene utilizzata la versione a virgola mobile) - [7232 #](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="01c46-158">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="01c46-159">dotnet-restore non riesce in origine autenticata quando config a livello di utente dispone anche di origine - [7209 #](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="01c46-159">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="01c46-160">Service Pack non deve limitare il set di BuildActions per i file di contenuto - [7155 #](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="01c46-160">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="01c46-161">Usa un projectreference che richiede AssetTargetFallback abbia esito positivo, deve avvisare.</span><span class="sxs-lookup"><span data-stu-id="01c46-161">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="01c46-162"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="01c46-162"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="01c46-163">Deadlock a causa di problemi relativi al threading durante la chiamata in CPS (CommonProjectSystem) - [7103 #](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="01c46-163">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="01c46-164">aggiungere dotnet pacchetto non verrà usate le credenziali nel file di configurazione globali per un'origine specificata nel file di configurazione locale - [6935 #](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="01c46-164">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="01c46-165">I problemi con MEF in corso di threading chiamato su percorsi del codice asincrono - [6771 #](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="01c46-165">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="01c46-166">Di firma: errore rilevato due volte e senza stack di chiamate - [6455 #](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="01c46-166">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="01c46-167">Installazione di un pacchetto firmato con il certificato di firma non attendibile deve mostrare l'errore - [6318 #](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="01c46-167">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="01c46-168">NuGet in modo non corretto ripristino NOOP quando 2 progetti condividono directory obj - [6114 #](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="01c46-168">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="01c46-169">Non è possibile usare token di accesso personale con dotnet restore in Linux con i pacchetti dal feed autenticati - [5651 #](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="01c46-169">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="01c46-170">dotnet-restore non riesce a causa di disabilitato macchina wide feed - [5410 #](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="01c46-170">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="01c46-171">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="01c46-171">**DCRs**</span></span>

* <span data-ttu-id="01c46-172">Gli assembly di NuGet 5.0 in modo da richiedere .NET 4.7.2 (tramite modifica TFM, target) - [7510 #](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="01c46-172">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="01c46-173">NuGetLicenseData da NuGet.Packaging deve essere un tipo pubblico.</span><span class="sxs-lookup"><span data-stu-id="01c46-173">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="01c46-174">Aggiornare i metadati di licenza acquisiti da spdx.</span><span class="sxs-lookup"><span data-stu-id="01c46-174">Update license metadata ingested from spdx.</span></span><span data-ttu-id="01c46-175"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="01c46-175"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="01c46-176">Rimuovere API obsolete impostazioni - [7294 #](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="01c46-176">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="01c46-177">Soluzione alternativa ripristino timeout nei sistemi con 1 cpu - [6742 #](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="01c46-177">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="01c46-178">NuGet preferenziale per l'autenticazione NTLM, anche se sono presenti credenziali in NuGet. config: aggiungere l'opzione di configurazione per filtrare i tipi di autenticazione per le credenziali - [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="01c46-178">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="01c46-179">Abilitare EmbedInteropTypes per PackageReference (funzionalità di Packages. config corrispondente) - [2365 #](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="01c46-179">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="01c46-180">Elenco di tutti i problemi risolti in questa versione 5.0.0-preview2</span><span class="sxs-lookup"><span data-stu-id="01c46-180">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="01c46-181">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="01c46-181">Known issues</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="01c46-182">I pacchetti in FallbackFolders installati da .NET Core SDK hanno un'installazione personalizzata e non superano la convalida della firma.</span><span class="sxs-lookup"><span data-stu-id="01c46-182">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="01c46-183"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="01c46-183"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="01c46-184">**Problema** quando si usa dotnet.exe 2.x in modo da ripristinare tale netcoreapp a più destinazioni di un progetto 1.x e netcoreapp 2.x, la cartella di fallback viene considerato come un file di feed.</span><span class="sxs-lookup"><span data-stu-id="01c46-184">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="01c46-185">Questo significa che, durante il ripristino, NuGet selezionerà il pacchetto dalla cartella di fallback e tenterà di installarlo nella cartella dei pacchetti globale e di eseguire la consueta convalida delle firme che avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="01c46-185">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="01c46-186">**Soluzione alternativa** disabilita l'utilizzo della cartella fallback impostando la `RestoreAdditionalProjectSources` su nothing.</span><span class="sxs-lookup"><span data-stu-id="01c46-186">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="01c46-187">`<RestoreAdditionalProjectSources/>` Usare con cautela perché ciò causerà il download di numerosi pacchetti da NuGet.org che altrimenti verrebbero ripristinati dalla cartella di fallback.</span><span class="sxs-lookup"><span data-stu-id="01c46-187">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
