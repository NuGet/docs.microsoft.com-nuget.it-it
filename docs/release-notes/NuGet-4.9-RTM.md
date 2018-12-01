---
title: Note sulla versione per NuGet 4.9 RTM
description: Note sulla versione per NuGet 4.9 incluse informazioni su problemi noti, correzioni di bug, nuove funzionalità e DCR.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 3da1056f64b76f27afa662d879ef9f85868e2a07
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453773"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="f999e-103">Note sulla versione per NuGet 4.9</span><span class="sxs-lookup"><span data-stu-id="f999e-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="f999e-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) include la funzionalità NuGet 4.9.0.</span><span class="sxs-lookup"><span data-stu-id="f999e-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.9.0 functionality.</span></span>


<span data-ttu-id="f999e-105">Sono disponibili anche le versioni da riga di comando della stessa funzionalità:</span><span class="sxs-lookup"><span data-stu-id="f999e-105">Command line versions of the same functionality are also available:</span></span>
* <span data-ttu-id="f999e-106">NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)</span><span class="sxs-lookup"><span data-stu-id="f999e-106">NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)</span></span>
* <span data-ttu-id="f999e-107">dotnet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span><span class="sxs-lookup"><span data-stu-id="f999e-107">dotnet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span></span>


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="f999e-108">Riepilogo: Novità della versione 4.9.0</span><span class="sxs-lookup"><span data-stu-id="f999e-108">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="f999e-109">Firma: abilitare ClientPolicies per richiedere l'uso di un set di autori e repository attendibili elencati nel file NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961)</span><span class="sxs-lookup"><span data-stu-id="f999e-109">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961)</span></span>

* <span data-ttu-id="f999e-110">Creare file ".snupkg" per contenere i simboli nel pacchetto -- ottimizzare il push per fare in modo che il protocollo nuget accetti file snupkg per il server dei simboli - [#6878](https://github.com/NuGet/Home/issues/6878)</span><span class="sxs-lookup"><span data-stu-id="f999e-110">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878)</span></span>

* <span data-ttu-id="f999e-111">Plug-in credenziali NuGet versione 2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="f999e-111">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="f999e-112">Pacchetti NuGet completi - Licenza - [#4628](https://github.com/NuGet/Home/issues/4628)</span><span class="sxs-lookup"><span data-stu-id="f999e-112">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628)</span></span>

* <span data-ttu-id="f999e-113">Abilitare i metadati "GeneratePathProperty" con consenso esplicito per un PackageReference per generare una proprietà MSBuild per ogni pacchetto per la directory "Foo.Bar\1.0\" - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="f999e-113">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="f999e-114">Migliorare la soddisfazione dei clienti con operazioni NuGet - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="f999e-114">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="f999e-115">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="f999e-115">Issues fixed in this release</span></span>

* <span data-ttu-id="f999e-116">Gli avvisi elevati a errori (tramite WarnAsErrors) generati da PackageExtraction non devono mai lasciare in giro il pacchetto estratto - [ #7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="f999e-116">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="f999e-117">I pacchetti con firma non valida non devono finire nella cartella dei pacchetti globale - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="f999e-117">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="f999e-118">La generazione di reindirizzamenti di binding non deve ignorare gli assembly di facciata - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="f999e-118">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="f999e-119">Il metodo Equals di VersionRange non confronta intervalli mobili - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="f999e-119">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="f999e-120">Ripristino: regressione delle prestazioni usando il nuovo stack HTTP .NET Core 2.1 - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="f999e-120">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="f999e-121">L'aggiornamento di un pacchetto non deve modificare PrivateAssets di un PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="f999e-121">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="f999e-122">Firma: la firma deve avere esito negativo se un pacchetto include troppe voci di pacchetto (>65534)- [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="f999e-122">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="f999e-123">Il percorso di codice "dotnet nuget push" deve supportare il nuovo provider di credenziali - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="f999e-123">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="f999e-124">Supporto dell'esecuzione dei plug-in con impostazioni cultura inglese non dipendenti da paese/area geografica (come accade in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="f999e-124">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="f999e-125">Il comando nuget sources add non deve eliminare le credenziali da NuGet.Config - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="f999e-125">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="f999e-126">L'installazione di un devDependency PackageReference deve usare l'impostazione predefinita excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="f999e-126">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="f999e-127">Correggere l'opzione migrator in modo da visualizzarla per tutti i progetti e che mostri un errore se il progetto è incompatibile - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="f999e-127">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="f999e-128">Il comando "dotnet add package" deve eseguire il commit del ripristino eseguito nel file di asset - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="f999e-128">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="f999e-129">Firma: migliorare i messaggi di errore correlati alla firma- [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="f999e-129">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="f999e-130">[Errore di test] [zh-TW] Stringa "Console di Gestione pacchetti" non localizzata nella Console di Gestione pacchetti - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="f999e-130">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="f999e-131">Il messaggio di errore "Impossibile trovare le informazioni sul progetto" deve essere un po' più specifico all'interno di Visual Studio - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="f999e-131">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="f999e-132">Messaggio di errore poco utile quando si usa in modo non corretto il tag version per nuspec di nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="f999e-132">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="f999e-133">DCR - firma: supporto del protocollo NuGet: risorsa RepositorySignatures/4.9.0 - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="f999e-133">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="f999e-134">DCR -Il file nupkg.metadata verrà ora creato durante l'estrazione del pacchetto - Contiene "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="f999e-134">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="f999e-135">DCR - Verifica authenticode non eseguita per i plug-in durante l'esecuzione in Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="f999e-135">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="f999e-136">Elenco di tutti i problemi corretti nella versione 4.9.0</span><span class="sxs-lookup"><span data-stu-id="f999e-136">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="f999e-137">Riepilogo: Novità della versione 4.9.1</span><span class="sxs-lookup"><span data-stu-id="f999e-137">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="f999e-138">Aggiunta del supporto per la lettura di una scrittura in NuGet.Config tramite un nuovo comando trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="f999e-138">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="f999e-139">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="f999e-139">Issues fixed in this release</span></span>

* <span data-ttu-id="f999e-140">Correzione della generazione di collegamenti di licenza - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="f999e-140">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="f999e-141">Regressione dei codici di errore per la convalida delle firme- [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="f999e-141">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="f999e-142">Il pacchetto NuGet.Build.Tasks.Pack non include informazioni di licenza - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="f999e-142">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="f999e-143">Elenco di tutti i problemi corretti nella versione 4.9.1</span><span class="sxs-lookup"><span data-stu-id="f999e-143">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="known-issues"></a><span data-ttu-id="f999e-144">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="f999e-144">Known issues</span></span>

### <a name="dotnetexenugetexe-doesnt-use-credentials-when-source-name-contains-a-whitespace---7517httpsgithubcomnugethomeissues7517"></a><span data-ttu-id="f999e-145">dotnet.exe/nuget.exe non usa credenziali quando il nome dell'origine contiene uno spazio vuoto - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="f999e-145">dotnet.exe/nuget.exe doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

#### <a name="issue"></a><span data-ttu-id="f999e-146">Problema</span><span class="sxs-lookup"><span data-stu-id="f999e-146">Issue</span></span>
<span data-ttu-id="f999e-147">Quando è presente uno spazio vuoto nel nome dell'origine, nuget.exe genera un errore come `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`</span><span class="sxs-lookup"><span data-stu-id="f999e-147">When there is a whitespace in the source name, nuget.exe throws an error like `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`</span></span>

#### <a name="workaround"></a><span data-ttu-id="f999e-148">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="f999e-148">Workaround</span></span>
<span data-ttu-id="f999e-149">Modificare il nome dell'origine in modo che non contenga uno spazio vuoto.</span><span class="sxs-lookup"><span data-stu-id="f999e-149">Change the name of the source to not contain a whitespace.</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="f999e-150">dotnet nuget push --interactive genera un errore in Mac.</span><span class="sxs-lookup"><span data-stu-id="f999e-150">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="f999e-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="f999e-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="f999e-152">Problema</span><span class="sxs-lookup"><span data-stu-id="f999e-152">Issue</span></span>
<span data-ttu-id="f999e-153">L'argomento `--interactive` non viene inoltrato dall'interfaccia della riga di comando dotnet e genera l'errore `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="f999e-153">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="f999e-154">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="f999e-154">Workaround</span></span>
<span data-ttu-id="f999e-155">Eseguire qualsiasi altro comando dotnet con l'opzione interactive, ad esempio `dotnet restore --interactive`, ed eseguire l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="f999e-155">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="f999e-156">L'autenticazione potrebbe essere così memorizzata nella cache dal provider di credenziali.</span><span class="sxs-lookup"><span data-stu-id="f999e-156">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="f999e-157">Eseguire quindi `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="f999e-157">Then run `dotnet nuget push`.</span></span>

### <a name="licenseacceptancewindow-and-licensefilewindow-accessibility-issues---7452httpsgithubcomnugethomeissues7452"></a><span data-ttu-id="f999e-158">Problemi di accessibilità per LicenseFileWindow e LicenseAcceptanceWindow - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="f999e-158">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

#### <a name="issue"></a><span data-ttu-id="f999e-159">Problema</span><span class="sxs-lookup"><span data-stu-id="f999e-159">Issue</span></span>
<span data-ttu-id="f999e-160">La finestra di accettazione della licenza e la finestra del file di licenza hanno problemi di accessibilità per gli spostamenti tramite tastiera e le descrizioni con utilità per la lettura dello schermo e JAWS.</span><span class="sxs-lookup"><span data-stu-id="f999e-160">The license acceptance window and license file window have accessibility issues with keyboard navigation and narration with screen reader and JAWS.</span></span>

#### <a name="workaround"></a><span data-ttu-id="f999e-161">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="f999e-161">Workaround</span></span>
<span data-ttu-id="f999e-162">Nessuna soluzione alternativa.</span><span class="sxs-lookup"><span data-stu-id="f999e-162">No workaround.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="f999e-163">I pacchetti in FallbackFolders installati da .NET Core SDK hanno un'installazione personalizzata e non superano la convalida della firma.</span><span class="sxs-lookup"><span data-stu-id="f999e-163">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="f999e-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="f999e-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="f999e-165">Problema</span><span class="sxs-lookup"><span data-stu-id="f999e-165">Issue</span></span>
<span data-ttu-id="f999e-166">Quando si usa dotnet.exe 2.x per ripristinare un progetto destinato sia a netcoreapp 1.x che a netcoreapp 2.x, la cartella di fallback viene considerata come un file di feed.</span><span class="sxs-lookup"><span data-stu-id="f999e-166">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="f999e-167">Questo significa che, durante il ripristino, NuGet selezionerà il pacchetto dalla cartella di fallback e tenterà di installarlo nella cartella dei pacchetti globale e di eseguire la consueta convalida delle firme che avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="f999e-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="f999e-168">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="f999e-168">Workaround</span></span>
<span data-ttu-id="f999e-169">Disabilitare l'utilizzo della cartella di fallback impostando `RestoreAdditionalProjectSources` su un valore vuoto.</span><span class="sxs-lookup"><span data-stu-id="f999e-169">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="f999e-170">`<RestoreAdditionalProjectSources/>` Usare con cautela perché ciò causerà il download di numerosi pacchetti da NuGet.org che altrimenti verrebbero ripristinati dalla cartella di fallback.</span><span class="sxs-lookup"><span data-stu-id="f999e-170">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
