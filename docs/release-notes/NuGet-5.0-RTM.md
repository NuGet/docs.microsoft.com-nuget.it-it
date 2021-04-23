---
title: Note sulla versione di NuGet 5.0 RTM
description: Note sulla versione per NuGet 5.0, inclusi problemi noti, correzioni di bug, nuove funzionalità e controller di dominio.
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 19173d2be7cd66b65651655385466b40f5e08352
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901746"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="c77e3-103">Note sulla versione di NuGet 5.0</span><span class="sxs-lookup"><span data-stu-id="c77e3-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="c77e3-104">Veicoli per la distribuzione di NuGet:</span><span class="sxs-lookup"><span data-stu-id="c77e3-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="c77e3-105">Versione di NuGet</span><span class="sxs-lookup"><span data-stu-id="c77e3-105">NuGet version</span></span> | <span data-ttu-id="c77e3-106">Disponibile nella versione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c77e3-106">Available in Visual Studio version</span></span>| <span data-ttu-id="c77e3-107">Disponibile in .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c77e3-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="c77e3-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="c77e3-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="c77e3-109">Visual Studio 2019 versione 16.0</span><span class="sxs-lookup"><span data-stu-id="c77e3-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="c77e3-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="c77e3-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="c77e3-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="c77e3-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="c77e3-112">Visual Studio 2019 versione 16.0.4</span><span class="sxs-lookup"><span data-stu-id="c77e3-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="c77e3-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1,</sup> [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="c77e3-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="c77e3-114"><sup>1</sup> Installato con il Visual Studio 2019 con carico di lavoro .NET Core</span><span class="sxs-lookup"><span data-stu-id="c77e3-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="c77e3-115"><sup>2</sup> Disponibile come installazione facoltativa con un carico Visual Studio 2019 con .NET Core</span><span class="sxs-lookup"><span data-stu-id="c77e3-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="c77e3-116">Riepilogo: Novità nella versione 5.0</span><span class="sxs-lookup"><span data-stu-id="c77e3-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="c77e3-117">Supporto per il [ripristino di soluzioni](/visualstudio/ide/filtered-solutions) filtrate in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="c77e3-117">Support for restoring [filtered solutions](/visualstudio/ide/filtered-solutions) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="c77e3-118">`BuildTransitive` la cartella consente ai pacchetti di fornire in modo transitivo destinazioni/proprietà al progetto host [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="c77e3-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="c77e3-119">Supporto migliore per gli scenari PackageReference nelle API IVs NuGet [-](https://github.com/NuGet/Home/issues/7005)#7005 , [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="c77e3-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="c77e3-120">`nuget.exe pack project.json` è stato deprecato - [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="c77e3-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="c77e3-121">Il plug-Provider di credenziali gen 1 è stato sostituito da [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) e verrà presto deprecato- [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="c77e3-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="c77e3-122">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="c77e3-122">Issues fixed in this release</span></span>

<span data-ttu-id="c77e3-123">**Bug**</span><span class="sxs-lookup"><span data-stu-id="c77e3-123">**Bugs**</span></span>

* <span data-ttu-id="c77e3-124">Quando si esegue un ripristino NoOp, evitare \*.dgspec.jsin scrittura nella directory obj - [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="c77e3-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="c77e3-125">Le autorizzazioni per i file creati all'interno di ~/.nuget sono troppo aperte- [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="c77e3-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="c77e3-126">`dotnet list package --outdated` non funziona con le origini che necessitano di autenticazione - [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="c77e3-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="c77e3-127">NuGet.VisualStudio.IVsPackageInstaller: la chiamata a un progetto senza riferimenti al pacchetto usa sempre packages.config, anche se il valore predefinito è impostato su PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="c77e3-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="c77e3-128">PMC: Update-Package reinstallazione non riesce ("Impossibile trovare il pacchetto") nei pacchetti delisted.</span><span class="sxs-lookup"><span data-stu-id="c77e3-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="c77e3-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="c77e3-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="c77e3-130">Aggiungere un avviso di terze parti nel nostro repo e VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="c77e3-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="c77e3-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage deve installare la versione più recente quando non viene specificata alcuna [versione, #7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="c77e3-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="c77e3-132">Supporto interattivo per dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="c77e3-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="c77e3-133">Quando si esegue il ripristino con il file di blocco, l'avviso NU1603 non deve essere generato.</span><span class="sxs-lookup"><span data-stu-id="c77e3-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="c77e3-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="c77e3-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="c77e3-135">NuGet non deve stampare il percorso del progetto durante il ripristino con registrazione [minima- #7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="c77e3-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="c77e3-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="c77e3-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="c77e3-137">Aggiungere di nuovo NuGet.Packaging.Core con attr TypeForwardedTo - [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="c77e3-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="c77e3-138">plugins_cache percorso più breve per funzionare correttamente- [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="c77e3-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="c77e3-139">Preferire il percorso per l'individuazione msbuild se l'utente non ha chiesto una versione specifica di [msbuild- #7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="c77e3-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="c77e3-140">`nuget.exe /?` dovrebbe elencare le versioni corrette di msbuild [- #7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="c77e3-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="c77e3-141">NuGet.targets(498,5): errore: Impossibile trovare una parte del percorso '/tmp/NuGetScratch - in mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="c77e3-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="c77e3-142">restore enumera inutilmente il contenuto di tutte le versioni del pacchetto a cui si fa riferimento nella cache del [computer- #7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="c77e3-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="c77e3-143">Il rilevamento automatico di MSBuild seleziona sempre la versione 16.0 dopo l'installazione di VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="c77e3-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="c77e3-144">dotnet list package in una soluzione restituisce voci duplicate per framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="c77e3-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="c77e3-145">Eccezione "Il nome del percorso vuoto non è valido" quando si chiama IVsPackageInstaller.InstallPackage in progetti e cartella pacchetti non esistenti.</span><span class="sxs-lookup"><span data-stu-id="c77e3-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="c77e3-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="c77e3-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="c77e3-147">msbuild /t:restore il livello di dettaglio minimo deve essere più minimo [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="c77e3-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="c77e3-148">L'interfaccia utente NuGet di VS 16.0 ha schede illeggibili a causa di problemi di colore [- #7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="c77e3-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="c77e3-149">Chiarimento di NuGet.Core & NuGet.Clients License.txt - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="c77e3-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="c77e3-150">Il ripristino enumera inutilmente la cartella globale del pacchetto nel tentativo di determinare il tipo [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="c77e3-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="c77e3-151">Gli errori di imposizione del file di blocco dovrebbero essere visualizzati nella finestra Elenco errori - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="c77e3-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="c77e3-152">Risolvere NuGet.Configproblemi di uration - [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="c77e3-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="c77e3-153">Adattare a MSBuild aggiornando il percorso di installazione - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="c77e3-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="c77e3-154">NuGet.Build.Tasks.Pack deve essere una dipendenza di sviluppo - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="c77e3-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="c77e3-155">Aggiungere il punto di estensione di tipo pack per includere i simboli di debug - [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="c77e3-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="c77e3-156">`dotnet pack` deve mantenere l'intervallo di versioni delle dipendenze nell'nupkg creato (anche se viene usata la versione mobile) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="c77e3-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="c77e3-157">`dotnet restore` ha esito negativo nell'origine autenticata quando anche la configurazione a livello di utente ha origine [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="c77e3-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="c77e3-158">Pack non deve limitare il set di BuildActions per i file di contenuto - [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="c77e3-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="c77e3-159">L'uso di projectReference che richiede l'esito positivo di AssetTargetFallback dovrebbe essere avvisato.</span><span class="sxs-lookup"><span data-stu-id="c77e3-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="c77e3-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="c77e3-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="c77e3-161">Deadlock causato da problemi di threading durante la chiamata a CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="c77e3-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="c77e3-162">`dotnet add package` non usa le credenziali della configurazione globale per un'origine specificata nella configurazione locale - [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="c77e3-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="c77e3-163">Problemi di threading relativi alla chiamata di MEF in percorsi di codice asincroni - [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="c77e3-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="c77e3-164">Firma: errore segnalato due volte e senza stack di chiamate - [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="c77e3-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="c77e3-165">L'installazione di un pacchetto firmato con un certificato di firma non attendibile dovrebbe visualizzare l'errore [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="c77e3-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="c77e3-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="c77e3-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="c77e3-167">Non è possibile usare PAT `dotnet restore` con in Linux con pacchetti dal feed autenticato - [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="c77e3-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="c77e3-168">dotnet restore si verifica un errore a causa di un feed a livello di computer [disabilitato - #5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="c77e3-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="c77e3-169">**DCR**</span><span class="sxs-lookup"><span data-stu-id="c77e3-169">**DCRs**</span></span>

* <span data-ttu-id="c77e3-170">Avvisa della rimozione futura di "dotnet pack project.js" - [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="c77e3-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="c77e3-171">Aggiungere un avviso di deprecazione per il plug-in delle credenziali Gen1 - [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="c77e3-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="c77e3-172">Firma: il repository abilitato per richiedere la verifica client di ogni pacchetto come repository firmato -- tramite la risorsa RepositorySignatures/5.0.0 - [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="c77e3-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="c77e3-173">limitare il numero di richiesta HTTP per ogni origine NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="c77e3-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="c77e3-174">NuGet deve avere come destinazione Net472 (per facilitare la pulizia della build 16.0 di VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="c77e3-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="c77e3-175">PMC: Rimuovere il comando OpenPackagePage - [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="c77e3-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="c77e3-176">Eseguire il mapping di NetCoreApp 3.0 a NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="c77e3-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="c77e3-177">Aggiungere il supporto netstandard2.0 ai pacchetti NuGet.\* - [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="c77e3-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="c77e3-178">Consentire agli autori di pacchetti di definire il comportamento transitivo degli asset di compilazione [- #6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="c77e3-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="c77e3-179">Supporto della funzionalità Filtro soluzione di VS 2019.</span><span class="sxs-lookup"><span data-stu-id="c77e3-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="c77e3-180">Supporta anche progetti non presenti nella soluzione o progetti scaricati.</span><span class="sxs-lookup"><span data-stu-id="c77e3-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="c77e3-181">È necessario ripristinare prima la soluzione completa (tramite l'interfaccia della riga di comando o Visual [Studio)](https://github.com/NuGet/Home/issues/5820) - #5820</span><span class="sxs-lookup"><span data-stu-id="c77e3-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="c77e3-182">Assembly NuGet 5.0 per richiedere .NET 4.7.2 (tramite modifica TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="c77e3-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="c77e3-183">NuGetLicenseData di NuGet.Packaging deve essere un tipo pubblico.</span><span class="sxs-lookup"><span data-stu-id="c77e3-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="c77e3-184">Aggiornare i metadati delle licenze inseriti da spdx.</span><span class="sxs-lookup"><span data-stu-id="c77e3-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="c77e3-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="c77e3-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="c77e3-186">Rimuovere le API delle impostazioni obsolete - [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="c77e3-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="c77e3-187">Soluzione alternativa: timeout di ripristino nei sistemi con 1 cpu [- #6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="c77e3-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="c77e3-188">NuGet preferisce l'autenticazione NTLM anche se sono presenti credenziali in NuGet.config - aggiungere l'opzione di configurazione per filtrare i tipi di autenticazione per le credenziali - [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="c77e3-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="c77e3-189">Abilitare EmbedInteropTypes per PackageReference (Packages.Config funzionalità) - [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="c77e3-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="c77e3-190">**[Elenco di tutti i problemi risolti in questa versione - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="c77e3-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="c77e3-191">Riepilogo: Novità nella versione 5.0.2</span><span class="sxs-lookup"><span data-stu-id="c77e3-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="c77e3-192">Sicurezza (se eseguita tramite dotnet.exe o mono.exe): la cartella obj deve essere creata con le autorizzazioni [#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="c77e3-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="c77e3-193">nuget.exe ripristino in mono/MacOS ha esito negativo con nuget.config e `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span><span class="sxs-lookup"><span data-stu-id="c77e3-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="c77e3-194">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="c77e3-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="c77e3-195">I pacchetti in FallbackFolders installati da .NET Core SDK hanno un'installazione personalizzata e non superano la convalida della firma.</span><span class="sxs-lookup"><span data-stu-id="c77e3-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="c77e3-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="c77e3-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="c77e3-197">Problema</span><span class="sxs-lookup"><span data-stu-id="c77e3-197">Issue</span></span>
<span data-ttu-id="c77e3-198">Quando si usa dotnet.exe 2.x per ripristinare un progetto destinato sia a netcoreapp 1.x che a netcoreapp 2.x, la cartella di fallback viene considerata come un file di feed.</span><span class="sxs-lookup"><span data-stu-id="c77e3-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="c77e3-199">Questo significa che, durante il ripristino, NuGet selezionerà il pacchetto dalla cartella di fallback e tenterà di installarlo nella cartella dei pacchetti globale e di eseguire la consueta convalida delle firme che avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="c77e3-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="c77e3-200">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="c77e3-200">Workaround</span></span>
<span data-ttu-id="c77e3-201">Disabilitare l'utilizzo della cartella di fallback impostando `RestoreAdditionalProjectSources` su nothing:</span><span class="sxs-lookup"><span data-stu-id="c77e3-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="c77e3-202">Usare questa opzione con cautela perché i pacchetti che verrebbero ripristinati dalla cartella di fallback verranno scaricati da NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c77e3-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>