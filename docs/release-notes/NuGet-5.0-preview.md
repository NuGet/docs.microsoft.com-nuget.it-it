---
title: Note sulla versione 5.0-preview di NuGet
description: Note sulla versione per le anteprime di NuGet 5.0, inclusi i problemi noti, correzioni di bug, nuove funzionalità e dcr.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: ed3294f88ff99d5e26f630bdbca03aa8446b6e7f
ms.sourcegitcommit: 0cb4c9853cde3647291062eadee2298dd273311e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2019
ms.locfileid: "55084937"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="909d6-103">Note sulla versione di NuGet 5.0 Preview</span><span class="sxs-lookup"><span data-stu-id="909d6-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="909d6-104">Riepilogo: What ' s New in 5.0 Preview 2</span><span class="sxs-lookup"><span data-stu-id="909d6-104">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="909d6-105">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="909d6-105">Issues fixed in this release</span></span>

#### <a name="bugs"></a><span data-ttu-id="909d6-106">Bug:</span><span class="sxs-lookup"><span data-stu-id="909d6-106">Bugs:</span></span>

* <span data-ttu-id="909d6-107">Visual Studio alla 16.0 UI NuGet sono disponibili schede illeggibile a causa di problemi di colore - [7735 #](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="909d6-107">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="909d6-108">NuGet. core e un chiarimento License di NuGet. Clients - [7629 #](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="909d6-108">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="909d6-109">Ripristino enumera inutilmente cartella globale dei pacchetti durante il tentativo di determinare il tipo - [7596 #](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="909d6-109">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="909d6-110">Errori di imposizione di file di blocco verranno visualizzate nel finestra Elenco errori - [7429 #](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="909d6-110">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="909d6-111">Risolvere i problemi di NuGet.Configuration - [7326 #](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="909d6-111">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="909d6-112">Adattare all'aggiornamento di MSBuild relativo percorso di installazione.</span><span class="sxs-lookup"><span data-stu-id="909d6-112">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="909d6-113">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="909d6-113">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="909d6-114">NuGet.Build.Tasks.Pack deve essere una dipendenza di sviluppo - [7249 #](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="909d6-114">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="909d6-115">Aggiungere il punto di estensione pack per l'inclusione di simboli - debug [7234 #](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="909d6-115">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="909d6-116">dotnet pack deve mantenere l'intervallo di versioni delle dipendenze nel pacchetto nupkg creato.</span><span class="sxs-lookup"><span data-stu-id="909d6-116">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="909d6-117">(anche se viene utilizzata la versione a virgola mobile) - [7232 #](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="909d6-117">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="909d6-118">dotnet-restore non riesce in origine autenticata quando config a livello di utente dispone anche di origine - [7209 #](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="909d6-118">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="909d6-119">Service Pack non deve limitare il set di BuildActions per i file di contenuto - [7155 #](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="909d6-119">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="909d6-120">Usa un projectreference che richiede AssetTargetFallback abbia esito positivo, deve avvisare.</span><span class="sxs-lookup"><span data-stu-id="909d6-120">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="909d6-121"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="909d6-121"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="909d6-122">Deadlock a causa di problemi relativi al threading durante la chiamata in CPS (CommonProjectSystem) - [7103 #](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="909d6-122">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="909d6-123">aggiungere dotnet pacchetto non verrà usate le credenziali nel file di configurazione globali per un'origine specificata nel file di configurazione locale - [6935 #](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="909d6-123">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="909d6-124">I problemi con MEF in corso di threading chiamato su percorsi del codice asincrono - [6771 #](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="909d6-124">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="909d6-125">Di firma: errore rilevato due volte e senza stack di chiamate - [6455 #](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="909d6-125">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="909d6-126">Installazione di un pacchetto firmato con il certificato di firma non attendibile deve mostrare l'errore - [6318 #](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="909d6-126">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="909d6-127">NuGet in modo non corretto ripristino NOOP quando 2 progetti condividono directory obj - [6114 #](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="909d6-127">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="909d6-128">Non è possibile usare token di accesso personale con dotnet restore in Linux con i pacchetti dal feed autenticati - [5651 #](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="909d6-128">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="909d6-129">dotnet-restore non riesce a causa di disabilitato macchina wide feed - [5410 #](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="909d6-129">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

#### <a name="dcrs"></a><span data-ttu-id="909d6-130">DCR</span><span class="sxs-lookup"><span data-stu-id="909d6-130">DCRs</span></span>

* <span data-ttu-id="909d6-131">Gli assembly di NuGet 5.0 in modo da richiedere .NET 4.7.2 (tramite modifica TFM, target) - [7510 #](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="909d6-131">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="909d6-132">NuGetLicenseData da NuGet.Packaging deve essere un tipo pubblico.</span><span class="sxs-lookup"><span data-stu-id="909d6-132">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="909d6-133">Aggiornare i metadati di licenza acquisiti da spdx.</span><span class="sxs-lookup"><span data-stu-id="909d6-133">Update license metadata ingested from spdx.</span></span><span data-ttu-id="909d6-134"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="909d6-134"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="909d6-135">Rimuovere API obsolete impostazioni - [7294 #](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="909d6-135">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="909d6-136">Soluzione alternativa ripristino timeout nei sistemi con 1 cpu - [6742 #](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="909d6-136">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="909d6-137">NuGet preferenziale per l'autenticazione NTLM, anche se sono presenti credenziali in NuGet. config: aggiungere l'opzione di configurazione per filtrare i tipi di autenticazione per le credenziali - [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="909d6-137">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="909d6-138">Abilitare EmbedInteropTypes per PackageReference (funzionalità di Packages. config corrispondente) - [2365 #](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="909d6-138">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="909d6-139">Elenco di tutti i problemi risolti in questa versione 5.0.0-preview2</span><span class="sxs-lookup"><span data-stu-id="909d6-139">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")


## <a name="known-issues"></a><span data-ttu-id="909d6-140">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="909d6-140">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="909d6-141">dotnet nuget push --interactive genera un errore in Mac.</span><span class="sxs-lookup"><span data-stu-id="909d6-141">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="909d6-142"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="909d6-142"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="909d6-143">Problema</span><span class="sxs-lookup"><span data-stu-id="909d6-143">Issue</span></span>
<span data-ttu-id="909d6-144">L'argomento `--interactive` non viene inoltrato dall'interfaccia della riga di comando dotnet e genera l'errore `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="909d6-144">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="909d6-145">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="909d6-145">Workaround</span></span>
<span data-ttu-id="909d6-146">Eseguire qualsiasi altro comando dotnet con l'opzione interactive, ad esempio `dotnet restore --interactive`, ed eseguire l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="909d6-146">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="909d6-147">L'autenticazione potrebbe essere così memorizzata nella cache dal provider di credenziali.</span><span class="sxs-lookup"><span data-stu-id="909d6-147">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="909d6-148">Eseguire quindi `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="909d6-148">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="909d6-149">I pacchetti in FallbackFolders installati da .NET Core SDK hanno un'installazione personalizzata e non superano la convalida della firma.</span><span class="sxs-lookup"><span data-stu-id="909d6-149">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="909d6-150"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="909d6-150"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="909d6-151">Problema</span><span class="sxs-lookup"><span data-stu-id="909d6-151">Issue</span></span>
<span data-ttu-id="909d6-152">Quando si usa dotnet.exe 2.x per ripristinare un progetto destinato sia a netcoreapp 1.x che a netcoreapp 2.x, la cartella di fallback viene considerata come un file di feed.</span><span class="sxs-lookup"><span data-stu-id="909d6-152">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="909d6-153">Questo significa che, durante il ripristino, NuGet selezionerà il pacchetto dalla cartella di fallback e tenterà di installarlo nella cartella dei pacchetti globale e di eseguire la consueta convalida delle firme che avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="909d6-153">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="909d6-154">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="909d6-154">Workaround</span></span>
<span data-ttu-id="909d6-155">Disabilitare l'utilizzo della cartella di fallback impostando `RestoreAdditionalProjectSources` su un valore vuoto.</span><span class="sxs-lookup"><span data-stu-id="909d6-155">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="909d6-156">`<RestoreAdditionalProjectSources/>` Usare con cautela perché ciò causerà il download di numerosi pacchetti da NuGet.org che altrimenti verrebbero ripristinati dalla cartella di fallback.</span><span class="sxs-lookup"><span data-stu-id="909d6-156">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
