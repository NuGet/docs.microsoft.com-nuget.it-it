---
title: Note sulla versione 5.0 RTM di NuGet
description: Note sulla versione per NuGet 5.0 inclusi i problemi noti, correzioni di bug, nuove funzionalità e dcr.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 5e48ff19ea5c4908d7eb0a3cb19a31b738e348eb
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "58921585"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="fac2c-103">Note sulla versione 5.0 di NuGet</span><span class="sxs-lookup"><span data-stu-id="fac2c-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="fac2c-104">Veicoli per la distribuzione di NuGet:</span><span class="sxs-lookup"><span data-stu-id="fac2c-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="fac2c-105">Versione di NuGet</span><span class="sxs-lookup"><span data-stu-id="fac2c-105">NuGet version</span></span> | <span data-ttu-id="fac2c-106">Disponibile nella versione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fac2c-106">Available in Visual Studio version</span></span>| <span data-ttu-id="fac2c-107">Disponibile in .NET SDK</span><span class="sxs-lookup"><span data-stu-id="fac2c-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="fac2c-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="fac2c-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="fac2c-109">Visual Studio 2019 version 16.0</span><span class="sxs-lookup"><span data-stu-id="fac2c-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="fac2c-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="fac2c-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="fac2c-111"><sup>1</sup>installata con Visual Studio 2019 con carico di lavoro di .NET Core</span><span class="sxs-lookup"><span data-stu-id="fac2c-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="fac2c-112"><sup>2</sup>disponibile in un'installazione facoltativa con Visual Studio 2019 con carico di lavoro di .NET Core</span><span class="sxs-lookup"><span data-stu-id="fac2c-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="fac2c-113">Riepilogo: Quali sono le novità nella versione 5.0</span><span class="sxs-lookup"><span data-stu-id="fac2c-113">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="fac2c-114">Supporto per il ripristino [filtrato solutions](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [5820 #](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="fac2c-114">Support for restoring [filtered solutions](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="fac2c-115">`BuildTransitive` cartella consente pacchetti di contribuire in modo transitivo destinazioni/proprietà nel progetto host - [6091 #](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="fac2c-115">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="fac2c-116">Supporto migliorato per gli scenari di PackageReference NuGet per le API interfacce IVs - [#7005](https://github.com/NuGet/Home/issues/7005), [7493 #](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="fac2c-116">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="fac2c-117">`nuget.exe pack project.json` è stato deprecato - [7928 #](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="fac2c-117">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="fac2c-118">Plug-in Provider di credenziali di generazione 1 è stato sostituito da [generazione 2](https://aka.ms/nuget-cross-platform-authentication-plugin) e verrà presto deprecato - [7819 #](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="fac2c-118">Gen 1 Credential Provider plugin has been superseded by [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="fac2c-119">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="fac2c-119">Issues fixed in this release</span></span>

<span data-ttu-id="fac2c-120">**Bug**</span><span class="sxs-lookup"><span data-stu-id="fac2c-120">**Bugs**</span></span>

* <span data-ttu-id="fac2c-121">Quando si esegue un ripristino NoOp, evitare \*. dgspec.json scrittura nella directory obj - [7854 #](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="fac2c-121">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="fac2c-122">Autorizzazioni per i file creati all'interno di ~/.nuget sono troppo open - [7673 #](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="fac2c-122">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="fac2c-123">`dotnet list package --outdated` non funziona con origini che richiedono l'autenticazione - [7605 #](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="fac2c-123">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="fac2c-124">NuGet.VisualStudio.IVsPackageInstaller - chiamata in un progetto con alcun pacchetto fa riferimento sempre Packages. config viene utilizzato, anche se il valore predefinito è impostato su PackageReference - [7005 #](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="fac2c-124">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="fac2c-125">PMC: Update-Package reinstallare ha esito negativo ("Impossibile trovare il pacchetto") nel venga rimosso dall'elenco dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="fac2c-125">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="fac2c-126"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="fac2c-126"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="fac2c-127">Aggiungi avviso di terze parti nel nostro repository e VSIX - [7409 #](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="fac2c-127">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="fac2c-128">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage consigliabile installare la versione più recente quando nessuna versione di base - [7493 #](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="fac2c-128">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="fac2c-129">-supporto interattivo per dotnet nuget push - [7519 #](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="fac2c-129">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="fac2c-130">Durante il ripristino con file di blocco, NU1603 avviso non deve essere generato.</span><span class="sxs-lookup"><span data-stu-id="fac2c-130">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="fac2c-131"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="fac2c-131"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="fac2c-132">NuGet non deve essere stampata percorso del progetto durante il ripristino con registrazione minima - [7647 #](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="fac2c-132">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="fac2c-133">-supporto interattivo per dotnet remove package - [7727 #](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="fac2c-133">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="fac2c-134">Aggiungere nuovo NuGet.Packaging.Core con attrs TypeForwardedTo - [7768 #](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="fac2c-134">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="fac2c-135">plugins_cache deve percorso più breve per funzionare bene - [7770 #](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="fac2c-135">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="fac2c-136">Preferire percorso per l'individuazione di msbuild, se l'utente non richieda la versione di msbuild specifica - [7786 #](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="fac2c-136">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="fac2c-137">`nuget.exe /?` dovrebbe elencare le versioni corrette di msbuild - [7794 #](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="fac2c-137">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="fac2c-138">NuGet.targets(498,5): error : Non è riuscito a trovare una parte del percorso "/ tmp/NuGetScratch - su mono - [7793 #](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="fac2c-138">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="fac2c-139">ripristino inutilmente enumera il contenuto di tutte le versioni del pacchetto di cui viene fatto riferimento nella cache del computer - [7639 #](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="fac2c-139">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="fac2c-140">Il rilevamento automatico MSBuild seleziona sempre 16.0 dopo l'installazione e 2019 di anteprima - [7621 #](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="fac2c-140">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="fac2c-141">elenco del pacchetto dotnet su una soluzione genera voci duplicate per framework - [7607 #](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="fac2c-141">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="fac2c-142">Eccezione "nome di percorso vuota non è valido" quando IVsPackageInstaller.InstallPackage chiamante nel vecchio progetti e pacchetti di cartella non esiste.</span><span class="sxs-lookup"><span data-stu-id="fac2c-142">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="fac2c-143"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="fac2c-143"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="fac2c-144">livello di dettaglio di MSBuild /t: Restore minimo deve essere più minimo - [4695 #](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="fac2c-144">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="fac2c-145">Visual Studio alla 16.0 UI NuGet sono disponibili schede illeggibile a causa di problemi di colore - [7735 #](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="fac2c-145">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="fac2c-146">NuGet. core e un chiarimento License di NuGet. Clients - [7629 #](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="fac2c-146">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="fac2c-147">Ripristino enumera inutilmente cartella globale dei pacchetti durante il tentativo di determinare il tipo - [7596 #](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="fac2c-147">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="fac2c-148">Errori di imposizione di file di blocco verranno visualizzate nel finestra Elenco errori - [7429 #](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="fac2c-148">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="fac2c-149">Risolvere i problemi di NuGet.Configuration - [7326 #](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="fac2c-149">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="fac2c-150">Adattare a MSBuild aggiornamento relativa installazione location - [7325 #](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="fac2c-150">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="fac2c-151">NuGet.Build.Tasks.Pack deve essere una dipendenza di sviluppo - [7249 #](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="fac2c-151">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="fac2c-152">Aggiungere il punto di estensione pack per l'inclusione di simboli - debug [7234 #](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="fac2c-152">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="fac2c-153">`dotnet pack` deve mantenere l'intervallo di versioni delle dipendenze nel pacchetto nupkg creato (anche se viene utilizzata la versione a virgola mobile) - [7232 #](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="fac2c-153">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="fac2c-154">`dotnet restore` si verifica un errore nell'origine autenticato quando config a livello di utente dispone anche di origine - [7209 #](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="fac2c-154">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="fac2c-155">Service Pack non deve limitare il set di BuildActions per i file di contenuto - [7155 #](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="fac2c-155">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="fac2c-156">Usa un ProjectReference che richiede AssetTargetFallback abbia esito positivo, deve avvisare.</span><span class="sxs-lookup"><span data-stu-id="fac2c-156">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="fac2c-157"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="fac2c-157"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="fac2c-158">Deadlock a causa di problemi relativi al threading durante la chiamata in CPS (CommonProjectSystem) - [7103 #](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="fac2c-158">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="fac2c-159">`dotnet add package` non utilizzare le credenziali nel file di configurazione globali per un'origine specificata nel file di configurazione locale - [6935 #](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="fac2c-159">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="fac2c-160">Problemi relativi al threading con MEF chiamato sul async codice percorsi - [6771 #](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="fac2c-160">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="fac2c-161">Di firma: errore rilevato due volte e senza stack di chiamate - [6455 #](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="fac2c-161">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="fac2c-162">Installazione di un pacchetto firmato con il certificato di firma non attendibile deve mostrare l'errore - [6318 #](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="fac2c-162">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="fac2c-163">NuGet in modo non corretto ripristino NOOP quando 2 progetti condividono directory obj - [6114 #](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="fac2c-163">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="fac2c-164">Non è possibile usare con PAT `dotnet restore` in Linux con i pacchetti dal feed autenticati - [5651 #](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="fac2c-164">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="fac2c-165">dotnet-restore non riesce a causa di disabilitato macchina wide feed - [5410 #](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="fac2c-165">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="fac2c-166">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="fac2c-166">**DCRs**</span></span>

* <span data-ttu-id="fac2c-167">Avvisa di futura rimozione di "dotnet pack file Project. JSON" - [7928 #](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="fac2c-167">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="fac2c-168">Aggiungere un avviso di deprecazione per plug-in delle credenziali Gen1 - [7819 #](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="fac2c-168">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="fac2c-169">Firma: Repository abilitato a richiedere la verifica di client di tutti i pacchetti come repository firmato: tramite la risorsa RepositorySignatures/5.0.0 - [7759 #](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="fac2c-169">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="fac2c-170">limitare il numero di richiesta http per ogni origine tramite NuGet. config - [4538 #](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="fac2c-170">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="fac2c-171">NuGet deve avere come destinazione Net472 (per consentire la compilazione di VSIX 16,0 pulizia) - [7143 #](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="fac2c-171">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="fac2c-172">PMC: Comando OpenPackagePage - Rimuovi [7384 #](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="fac2c-172">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="fac2c-173">Mappa di NetCoreApp 3.0 apportare a NetStandard 2.1 - [7762 #](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="fac2c-173">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="fac2c-174">Aggiungere il supporto netstandard2.0 pacchetti NuGet.\* - [6516 #](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="fac2c-174">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="fac2c-175">Consentire agli autori di pacchetti di definire il comportamento transitiva gli asset di compilazione - [6091 #](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="fac2c-175">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="fac2c-176">Supporta funzionalità di filtro di soluzioni di Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="fac2c-176">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="fac2c-177">Supporta anche progetto non in soluzioni o progetti scaricati.</span><span class="sxs-lookup"><span data-stu-id="fac2c-177">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="fac2c-178">È necessario ripristinare innanzitutto - soluzione completa (tramite la CLI o Visual Studio) [5820 #](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="fac2c-178">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="fac2c-179">Gli assembly di NuGet 5.0 in modo da richiedere .NET 4.7.2 (tramite modifica TFM, target) - [7510 #](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="fac2c-179">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="fac2c-180">NuGetLicenseData da NuGet.Packaging deve essere un tipo pubblico.</span><span class="sxs-lookup"><span data-stu-id="fac2c-180">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="fac2c-181">Aggiornare i metadati di licenza acquisiti da spdx.</span><span class="sxs-lookup"><span data-stu-id="fac2c-181">Update license metadata ingested from spdx.</span></span><span data-ttu-id="fac2c-182"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="fac2c-182"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="fac2c-183">Rimuovere API obsolete impostazioni - [7294 #](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="fac2c-183">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="fac2c-184">Soluzione alternativa ripristino timeout nei sistemi con 1 cpu - [6742 #](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="fac2c-184">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="fac2c-185">NuGet preferenziale per l'autenticazione NTLM, anche se sono presenti credenziali in NuGet. config: aggiungere l'opzione di configurazione per filtrare i tipi di autenticazione per le credenziali - [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="fac2c-185">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="fac2c-186">Abilitare EmbedInteropTypes per PackageReference (funzionalità di Packages. config corrispondente) - [2365 #](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="fac2c-186">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="fac2c-187">**[Elenco di tutti i problemi risolti in questa versione - RTM 5.0](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="fac2c-187">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="known-issues"></a><span data-ttu-id="fac2c-188">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="fac2c-188">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="fac2c-189">I pacchetti in FallbackFolders installati da .NET Core SDK hanno un'installazione personalizzata e non superano la convalida della firma.</span><span class="sxs-lookup"><span data-stu-id="fac2c-189">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="fac2c-190"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="fac2c-190"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="fac2c-191">Problema</span><span class="sxs-lookup"><span data-stu-id="fac2c-191">Issue</span></span>
<span data-ttu-id="fac2c-192">Quando si usa dotnet.exe 2.x per ripristinare un progetto destinato sia a netcoreapp 1.x che a netcoreapp 2.x, la cartella di fallback viene considerata come un file di feed.</span><span class="sxs-lookup"><span data-stu-id="fac2c-192">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="fac2c-193">Questo significa che, durante il ripristino, NuGet selezionerà il pacchetto dalla cartella di fallback e tenterà di installarlo nella cartella dei pacchetti globale e di eseguire la consueta convalida delle firme che avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="fac2c-193">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="fac2c-194">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="fac2c-194">Workaround</span></span>
<span data-ttu-id="fac2c-195">Disabilitare l'utilizzo della cartella fallback impostando la `RestoreAdditionalProjectSources` su nothing:</span><span class="sxs-lookup"><span data-stu-id="fac2c-195">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="fac2c-196">Utilizzarlo con cautela come ora verranno scaricati i pacchetti che viene ripristinati dalla cartella di fallback da NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="fac2c-196">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>
