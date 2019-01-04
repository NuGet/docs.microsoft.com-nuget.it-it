---
title: Note sulla versione per NuGet 4.9 RTM
description: Note sulla versione per NuGet 4.9 incluse informazioni su problemi noti, correzioni di bug, nuove funzionalità e DCR.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 7dcb2e430ad80815f716f5567b511ff08acfe31b
ms.sourcegitcommit: a9babe261f67da0f714d168d04ea54a66628974b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2018
ms.locfileid: "53735136"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="90d71-103">Note sulla versione per NuGet 4.9</span><span class="sxs-lookup"><span data-stu-id="90d71-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="90d71-104">Veicoli per la distribuzione di NuGet:</span><span class="sxs-lookup"><span data-stu-id="90d71-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="90d71-105">Versione di NuGet</span><span class="sxs-lookup"><span data-stu-id="90d71-105">NuGet version</span></span> | <span data-ttu-id="90d71-106">Disponibile nella versione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="90d71-106">Available in Visual Studio version</span></span>| <span data-ttu-id="90d71-107">Disponibile in .NET SDK</span><span class="sxs-lookup"><span data-stu-id="90d71-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| <span data-ttu-id="90d71-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="90d71-108">**4.9.0**</span></span> | <span data-ttu-id="90d71-109">Visual Studio 2017 versione 15.9.0</span><span class="sxs-lookup"><span data-stu-id="90d71-109">Visual Studio 2017 version 15.9.0</span></span> | <span data-ttu-id="90d71-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="90d71-110">2.1.500, 2.2.100</span></span> |
| <span data-ttu-id="90d71-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="90d71-111">**4.9.1**</span></span> | <span data-ttu-id="90d71-112">N/D</span><span class="sxs-lookup"><span data-stu-id="90d71-112">n/a</span></span> | <span data-ttu-id="90d71-113">N/D</span><span class="sxs-lookup"><span data-stu-id="90d71-113">n/a</span></span> |
| [<span data-ttu-id="90d71-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="90d71-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="90d71-115">Visual Studio 2017 versione 15.9.4</span><span class="sxs-lookup"><span data-stu-id="90d71-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="90d71-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="90d71-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |

## <a name="summary-whats-new-in-490"></a><span data-ttu-id="90d71-117">Riepilogo: Novità nella versione 4.9.0</span><span class="sxs-lookup"><span data-stu-id="90d71-117">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="90d71-118">Firma: abilitare ClientPolicies per richiedere l'uso di un set di autori e repository attendibili elencati nel file NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [post di blog](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="90d71-118">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="90d71-119">Creare file ".snupkg" per contenere i simboli nel pacchetto -- ottimizzare il push per fare in modo che il protocollo nuget accetti file snupkg per il server dei simboli - [#6878](https://github.com/NuGet/Home/issues/6878), [post di blog](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="90d71-119">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="90d71-120">Plug-in credenziali NuGet versione 2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="90d71-120">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="90d71-121">Pacchetti NuGet completi - Licenza - [#4628](https://github.com/NuGet/Home/issues/4628), [annuncio](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="90d71-121">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="90d71-122">Abilitare i metadati "GeneratePathProperty" con consenso esplicito per un PackageReference per generare una proprietà MSBuild per ogni pacchetto per la directory "Foo.Bar\1.0\" - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="90d71-122">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="90d71-123">Migliorare la soddisfazione dei clienti con operazioni NuGet - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="90d71-123">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="90d71-124">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="90d71-124">Issues fixed in this release</span></span>

* <span data-ttu-id="90d71-125">Gli avvisi elevati a errori (tramite WarnAsErrors) generati da PackageExtraction non devono mai lasciare in giro il pacchetto estratto - [ #7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="90d71-125">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="90d71-126">I pacchetti con firma non valida non devono finire nella cartella dei pacchetti globale - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="90d71-126">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="90d71-127">La generazione di reindirizzamenti di binding non deve ignorare gli assembly di facciata - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="90d71-127">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="90d71-128">Il metodo Equals di VersionRange non confronta intervalli mobili - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="90d71-128">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="90d71-129">Ripristino: regressione delle prestazioni usando il nuovo stack HTTP .NET Core 2.1 - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="90d71-129">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="90d71-130">L'aggiornamento di un pacchetto non deve modificare PrivateAssets di un PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="90d71-130">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="90d71-131">Firma: la firma deve avere esito negativo se un pacchetto include troppe voci di pacchetto (>65534)- [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="90d71-131">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="90d71-132">Il percorso di codice "dotnet nuget push" deve supportare il nuovo provider di credenziali - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="90d71-132">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="90d71-133">Supporto dell'esecuzione dei plug-in con impostazioni cultura inglese non dipendenti da paese/area geografica (come accade in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="90d71-133">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="90d71-134">Il comando nuget sources add non deve eliminare le credenziali da NuGet.Config - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="90d71-134">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="90d71-135">L'installazione di un devDependency PackageReference deve usare l'impostazione predefinita excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="90d71-135">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="90d71-136">Correggere l'opzione migrator in modo da visualizzarla per tutti i progetti e che mostri un errore se il progetto è incompatibile - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="90d71-136">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="90d71-137">Il comando "dotnet add package" deve eseguire il commit del ripristino eseguito nel file di asset - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="90d71-137">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="90d71-138">Firma: migliorare i messaggi di errore correlati alla firma- [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="90d71-138">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="90d71-139">[Errore di test] [zh-TW] Stringa "Console di Gestione pacchetti" non localizzata nella Console di Gestione pacchetti - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="90d71-139">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="90d71-140">Il messaggio di errore "Impossibile trovare le informazioni sul progetto" deve essere un po' più specifico all'interno di Visual Studio - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="90d71-140">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="90d71-141">Messaggio di errore poco utile quando si usa in modo non corretto il tag version per nuspec di nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="90d71-141">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="90d71-142">DCR - firma: supporto del protocollo NuGet: risorsa RepositorySignatures/4.9.0 - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="90d71-142">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="90d71-143">DCR -Il file nupkg.metadata verrà ora creato durante l'estrazione del pacchetto - Contiene "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="90d71-143">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="90d71-144">DCR - Verifica authenticode non eseguita per i plug-in durante l'esecuzione in Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="90d71-144">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="90d71-145">Elenco di tutti i problemi corretti nella versione 4.9.0</span><span class="sxs-lookup"><span data-stu-id="90d71-145">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="90d71-146">Riepilogo: Novità nella versione 4.9.1</span><span class="sxs-lookup"><span data-stu-id="90d71-146">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="90d71-147">Aggiunta del supporto per la lettura di una scrittura in NuGet.Config tramite un nuovo comando trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="90d71-147">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="90d71-148">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="90d71-148">Issues fixed in this release</span></span>

* <span data-ttu-id="90d71-149">Correzione della generazione di collegamenti di licenza - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="90d71-149">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="90d71-150">Regressione dei codici di errore per la convalida delle firme- [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="90d71-150">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="90d71-151">Il pacchetto NuGet.Build.Tasks.Pack non include informazioni di licenza - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="90d71-151">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="90d71-152">Elenco di tutti i problemi corretti nella versione 4.9.1</span><span class="sxs-lookup"><span data-stu-id="90d71-152">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="90d71-153">Riepilogo: Novità nella versione 4.9.2</span><span class="sxs-lookup"><span data-stu-id="90d71-153">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="90d71-154">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="90d71-154">Issues fixed in this release</span></span>

* <span data-ttu-id="90d71-155">VS/dotnet.exe/nuget.exe/msbuild.exe restore non usa credenziali quando il nome dell'origine contiene uno spazio vuoto - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="90d71-155">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="90d71-156">Problemi di accessibilità per LicenseFileWindow e LicenseAcceptanceWindow - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="90d71-156">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="90d71-157">Correggere FormatException in DateTime.Parse da DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="90d71-157">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="90d71-158">Elenco di tutti i problemi corretti nella versione 4.9.2</span><span class="sxs-lookup"><span data-stu-id="90d71-158">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="known-issues"></a><span data-ttu-id="90d71-159">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="90d71-159">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="90d71-160">dotnet nuget push --interactive genera un errore in Mac.</span><span class="sxs-lookup"><span data-stu-id="90d71-160">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="90d71-161"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="90d71-161"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="90d71-162">Problema</span><span class="sxs-lookup"><span data-stu-id="90d71-162">Issue</span></span>
<span data-ttu-id="90d71-163">L'argomento `--interactive` non viene inoltrato dall'interfaccia della riga di comando dotnet e genera l'errore `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="90d71-163">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="90d71-164">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="90d71-164">Workaround</span></span>
<span data-ttu-id="90d71-165">Eseguire qualsiasi altro comando dotnet con l'opzione interactive, ad esempio `dotnet restore --interactive`, ed eseguire l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="90d71-165">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="90d71-166">L'autenticazione potrebbe essere così memorizzata nella cache dal provider di credenziali.</span><span class="sxs-lookup"><span data-stu-id="90d71-166">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="90d71-167">Eseguire quindi `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="90d71-167">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="90d71-168">I pacchetti in FallbackFolders installati da .NET Core SDK hanno un'installazione personalizzata e non superano la convalida della firma.</span><span class="sxs-lookup"><span data-stu-id="90d71-168">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="90d71-169"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="90d71-169"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="90d71-170">Problema</span><span class="sxs-lookup"><span data-stu-id="90d71-170">Issue</span></span>
<span data-ttu-id="90d71-171">Quando si usa dotnet.exe 2.x per ripristinare un progetto destinato sia a netcoreapp 1.x che a netcoreapp 2.x, la cartella di fallback viene considerata come un file di feed.</span><span class="sxs-lookup"><span data-stu-id="90d71-171">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="90d71-172">Questo significa che, durante il ripristino, NuGet selezionerà il pacchetto dalla cartella di fallback e tenterà di installarlo nella cartella dei pacchetti globale e di eseguire la consueta convalida delle firme che avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="90d71-172">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="90d71-173">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="90d71-173">Workaround</span></span>
<span data-ttu-id="90d71-174">Disabilitare l'utilizzo della cartella di fallback impostando `RestoreAdditionalProjectSources` su un valore vuoto.</span><span class="sxs-lookup"><span data-stu-id="90d71-174">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="90d71-175">`<RestoreAdditionalProjectSources/>` Usare con cautela perché ciò causerà il download di numerosi pacchetti da NuGet.org che altrimenti verrebbero ripristinati dalla cartella di fallback.</span><span class="sxs-lookup"><span data-stu-id="90d71-175">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
