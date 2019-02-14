---
title: Note sulla versione 5.0-preview di NuGet
description: Note sulla versione per le anteprime di NuGet 5.0, inclusi i problemi noti, correzioni di bug, nuove funzionalità e dcr.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 5889ea52f993fa8fe841f8eb83b6da659cdede93
ms.sourcegitcommit: 1ab750ff17e55c763d646c50e7630138804ce8b8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247659"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="b3a24-103">Note sulla versione di NuGet 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="b3a24-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="b3a24-104">Versioni di anteprima 5.0 di NuGet</span><span class="sxs-lookup"><span data-stu-id="b3a24-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="b3a24-105">13 febbraio 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="b3a24-105">February 13, 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span></span>
* <span data-ttu-id="b3a24-106">23 gennaio 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="b3a24-106">January 23, 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span></span>

## <a name="summary-whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="b3a24-107">Riepilogo: What ' s New in NuGet 5.0 Preview 3</span><span class="sxs-lookup"><span data-stu-id="b3a24-107">Summary: What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="b3a24-108">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="b3a24-108">Issues fixed in this release</span></span> 

<span data-ttu-id="b3a24-109">**Bug:**</span><span class="sxs-lookup"><span data-stu-id="b3a24-109">**Bugs:**</span></span>

* <span data-ttu-id="b3a24-110">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="b3a24-110">nuget.exe /?</span></span> <span data-ttu-id="b3a24-111">dovrebbe elencare le versioni corrette di msbuild - [7794 #](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="b3a24-111">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="b3a24-112">NuGet.targets(498,5): error : Non è riuscito a trovare una parte del percorso "/ tmp/NuGetScratch - su mono - [7793 #](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="b3a24-112">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="b3a24-113">ripristino inutilmente enumera il contenuto di tutte le versioni del pacchetto di cui viene fatto riferimento nella cache del computer - [7639 #](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="b3a24-113">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="b3a24-114">Il rilevamento automatico MSBuild seleziona sempre 16.0 dopo l'installazione e 2019 di anteprima - [7621 #](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="b3a24-114">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="b3a24-115">elenco del pacchetto dotnet su una soluzione genera voci duplicate per framework - [7607 #](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="b3a24-115">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="b3a24-116">Eccezione "nome di percorso vuota non è valido" quando IVsPackageInstaller.InstallPackage chiamante nel vecchio progetti e pacchetti di cartella non esiste.</span><span class="sxs-lookup"><span data-stu-id="b3a24-116">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="b3a24-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="b3a24-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="b3a24-118">livello di dettaglio di MSBuild /t: Restore minimo deve essere più minimo - [4695 #](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="b3a24-118">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="b3a24-119">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="b3a24-119">**DCRs**</span></span>

* <span data-ttu-id="b3a24-120">Consentire agli autori di pacchetti di definire il comportamento transitiva gli asset di compilazione - [6091 #](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="b3a24-120">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="b3a24-121">Abilitare il ripristino in VS abbia esito positivo se un progetto non fa parte della soluzione o non è stato caricato, ma è stato ripristinato in precedenza - [5820 #](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="b3a24-121">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="b3a24-122">Riepilogo: What ' s New in 5.0 Preview 2</span><span class="sxs-lookup"><span data-stu-id="b3a24-122">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="b3a24-123">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="b3a24-123">Issues fixed in this release</span></span>

<span data-ttu-id="b3a24-124">**Bug:**</span><span class="sxs-lookup"><span data-stu-id="b3a24-124">**Bugs:**</span></span>

* <span data-ttu-id="b3a24-125">Visual Studio alla 16.0 UI NuGet sono disponibili schede illeggibile a causa di problemi di colore - [7735 #](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="b3a24-125">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="b3a24-126">NuGet. core e un chiarimento License di NuGet. Clients - [7629 #](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="b3a24-126">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="b3a24-127">Ripristino enumera inutilmente cartella globale dei pacchetti durante il tentativo di determinare il tipo - [7596 #](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="b3a24-127">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="b3a24-128">Errori di imposizione di file di blocco verranno visualizzate nel finestra Elenco errori - [7429 #](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="b3a24-128">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="b3a24-129">Risolvere i problemi di NuGet.Configuration - [7326 #](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="b3a24-129">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="b3a24-130">Adattare all'aggiornamento di MSBuild relativo percorso di installazione.</span><span class="sxs-lookup"><span data-stu-id="b3a24-130">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="b3a24-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="b3a24-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="b3a24-132">NuGet.Build.Tasks.Pack deve essere una dipendenza di sviluppo - [7249 #](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="b3a24-132">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="b3a24-133">Aggiungere il punto di estensione pack per l'inclusione di simboli - debug [7234 #](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="b3a24-133">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="b3a24-134">dotnet pack deve mantenere l'intervallo di versioni delle dipendenze nel pacchetto nupkg creato.</span><span class="sxs-lookup"><span data-stu-id="b3a24-134">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="b3a24-135">(anche se viene utilizzata la versione a virgola mobile) - [7232 #](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="b3a24-135">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="b3a24-136">dotnet-restore non riesce in origine autenticata quando config a livello di utente dispone anche di origine - [7209 #](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="b3a24-136">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="b3a24-137">Service Pack non deve limitare il set di BuildActions per i file di contenuto - [7155 #](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="b3a24-137">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="b3a24-138">Usa un projectreference che richiede AssetTargetFallback abbia esito positivo, deve avvisare.</span><span class="sxs-lookup"><span data-stu-id="b3a24-138">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="b3a24-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="b3a24-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="b3a24-140">Deadlock a causa di problemi relativi al threading durante la chiamata in CPS (CommonProjectSystem) - [7103 #](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="b3a24-140">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="b3a24-141">aggiungere dotnet pacchetto non verrà usate le credenziali nel file di configurazione globali per un'origine specificata nel file di configurazione locale - [6935 #](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="b3a24-141">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="b3a24-142">I problemi con MEF in corso di threading chiamato su percorsi del codice asincrono - [6771 #](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="b3a24-142">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="b3a24-143">Di firma: errore rilevato due volte e senza stack di chiamate - [6455 #](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="b3a24-143">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="b3a24-144">Installazione di un pacchetto firmato con il certificato di firma non attendibile deve mostrare l'errore - [6318 #](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="b3a24-144">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="b3a24-145">NuGet in modo non corretto ripristino NOOP quando 2 progetti condividono directory obj - [6114 #](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="b3a24-145">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="b3a24-146">Non è possibile usare token di accesso personale con dotnet restore in Linux con i pacchetti dal feed autenticati - [5651 #](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="b3a24-146">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="b3a24-147">dotnet-restore non riesce a causa di disabilitato macchina wide feed - [5410 #](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="b3a24-147">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="b3a24-148">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="b3a24-148">**DCRs**</span></span>

* <span data-ttu-id="b3a24-149">Gli assembly di NuGet 5.0 in modo da richiedere .NET 4.7.2 (tramite modifica TFM, target) - [7510 #](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="b3a24-149">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="b3a24-150">NuGetLicenseData da NuGet.Packaging deve essere un tipo pubblico.</span><span class="sxs-lookup"><span data-stu-id="b3a24-150">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="b3a24-151">Aggiornare i metadati di licenza acquisiti da spdx.</span><span class="sxs-lookup"><span data-stu-id="b3a24-151">Update license metadata ingested from spdx.</span></span><span data-ttu-id="b3a24-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="b3a24-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="b3a24-153">Rimuovere API obsolete impostazioni - [7294 #](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="b3a24-153">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="b3a24-154">Soluzione alternativa ripristino timeout nei sistemi con 1 cpu - [6742 #](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="b3a24-154">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="b3a24-155">NuGet preferenziale per l'autenticazione NTLM, anche se sono presenti credenziali in NuGet. config: aggiungere l'opzione di configurazione per filtrare i tipi di autenticazione per le credenziali - [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="b3a24-155">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="b3a24-156">Abilitare EmbedInteropTypes per PackageReference (funzionalità di Packages. config corrispondente) - [2365 #](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="b3a24-156">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="b3a24-157">Elenco di tutti i problemi risolti in questa versione 5.0.0-preview2</span><span class="sxs-lookup"><span data-stu-id="b3a24-157">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="b3a24-158">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="b3a24-158">Known issues</span></span>

#### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="b3a24-159">dotnet nuget push --interactive genera un errore in Mac.</span><span class="sxs-lookup"><span data-stu-id="b3a24-159">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="b3a24-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="b3a24-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>
<span data-ttu-id="b3a24-161">**Problema** il `--interactive` argomento non viene inoltrato da dotnet cli e genera l'errore `error: Missing value for option 'interactive'` 
 **soluzione alternativa** eseguire qualsiasi altro comando di dotnet con l'opzione interattiva, ad esempio `dotnet restore --interactive` ed eseguire l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="b3a24-161">**Issue** The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`
**Workaround** Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="b3a24-162">L'autenticazione potrebbe essere così memorizzata nella cache dal provider di credenziali.</span><span class="sxs-lookup"><span data-stu-id="b3a24-162">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="b3a24-163">Eseguire quindi `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="b3a24-163">Then run `dotnet nuget push`.</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="b3a24-164">I pacchetti in FallbackFolders installati da .NET Core SDK hanno un'installazione personalizzata e non superano la convalida della firma.</span><span class="sxs-lookup"><span data-stu-id="b3a24-164">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="b3a24-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="b3a24-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="b3a24-166">**Problema** quando si usa dotnet.exe 2.x in modo da ripristinare tale netcoreapp a più destinazioni di un progetto 1.x e netcoreapp 2.x, la cartella di fallback viene considerato come un file di feed.</span><span class="sxs-lookup"><span data-stu-id="b3a24-166">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="b3a24-167">Questo significa che, durante il ripristino, NuGet selezionerà il pacchetto dalla cartella di fallback e tenterà di installarlo nella cartella dei pacchetti globale e di eseguire la consueta convalida delle firme che avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="b3a24-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="b3a24-168">**Soluzione alternativa** disabilita l'utilizzo della cartella fallback impostando la `RestoreAdditionalProjectSources` su nothing.</span><span class="sxs-lookup"><span data-stu-id="b3a24-168">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="b3a24-169">`<RestoreAdditionalProjectSources/>` Usare con cautela perché ciò causerà il download di numerosi pacchetti da NuGet.org che altrimenti verrebbero ripristinati dalla cartella di fallback.</span><span class="sxs-lookup"><span data-stu-id="b3a24-169">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
