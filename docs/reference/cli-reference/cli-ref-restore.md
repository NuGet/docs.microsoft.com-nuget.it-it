---
title: Comando di ripristino di NuGet CLI
description: Riferimento per il comando nuget.exe Restore
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 49fabbd0ef0c1c0c16f13bdf741296575fa72359
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780033"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="d0452-103">comando Restore (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="d0452-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="d0452-104">**Si applica a:** versioni supportate per l'utilizzo di pacchetti &bullet; **:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="d0452-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="d0452-105">Scarica e installa tutti i pacchetti mancanti nella `packages` cartella.</span><span class="sxs-lookup"><span data-stu-id="d0452-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="d0452-106">Se usato con NuGet 4.0 + e il formato PackageReference, genera un `<project>.nuget.props` file, se necessario, nella `obj` cartella.</span><span class="sxs-lookup"><span data-stu-id="d0452-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="d0452-107">Il file può essere omesso dal controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="d0452-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="d0452-108">In Mac OSX e Linux con l'interfaccia della riga di comando in mono, il ripristino dei pacchetti non è supportato con PackageReference.</span><span class="sxs-lookup"><span data-stu-id="d0452-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="d0452-109">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="d0452-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="d0452-110">dove `<projectPath>` specifica il percorso di una soluzione o di un `packages.config` file.</span><span class="sxs-lookup"><span data-stu-id="d0452-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="d0452-111">Per informazioni sui comportamenti, vedere la [sezione Osservazioni](#remarks) di seguito.</span><span class="sxs-lookup"><span data-stu-id="d0452-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="d0452-112">Opzioni</span><span class="sxs-lookup"><span data-stu-id="d0452-112">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="d0452-113">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="d0452-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d0452-114">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="d0452-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DirectDownload`**

  <span data-ttu-id="d0452-115">*(4.0 +)* Scarica i pacchetti direttamente senza popolare le cache con i file binari o i metadati.</span><span class="sxs-lookup"><span data-stu-id="d0452-115">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span>

- **`-DisableParallelProcessing`**

   <span data-ttu-id="d0452-116">Disabilita il ripristino di più pacchetti in parallelo.</span><span class="sxs-lookup"><span data-stu-id="d0452-116">Disables restoring multiple packages in parallel.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="d0452-117">*(3.2 +)* Elenco di origini di pacchetti da usare come fallback nel caso in cui il pacchetto non venga trovato nell'origine primaria o predefinita.</span><span class="sxs-lookup"><span data-stu-id="d0452-117">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> <span data-ttu-id="d0452-118">Utilizzare un punto e virgola per separare le voci dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="d0452-118">Use a semicolon to separate list entries.</span></span>

- **`-Force`**

  <span data-ttu-id="d0452-119">Nei progetti basati su PackageReference, impone la risoluzione di tutte le dipendenze anche se l'ultimo ripristino ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="d0452-119">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="d0452-120">La specifica di questo flag è simile all'eliminazione del `project.assets.json` file.</span><span class="sxs-lookup"><span data-stu-id="d0452-120">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="d0452-121">Questa operazione non consente di ignorare la cache HTTP.</span><span class="sxs-lookup"><span data-stu-id="d0452-121">This does not bypass the http-cache.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="d0452-122">*(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="d0452-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-ForceEvaluate`**

  <span data-ttu-id="d0452-123">Forza il ripristino per rivalutare tutte le dipendenze anche se un file di blocco esiste già.</span><span class="sxs-lookup"><span data-stu-id="d0452-123">Forces restore to reevaluate all dependencies even if a lock file already exists.</span></span>

- **`-?|-help`**

  <span data-ttu-id="d0452-124">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="d0452-124">Displays help information for the command.</span></span>

- **`-LockFilePath`**

  <span data-ttu-id="d0452-125">Percorso di output in cui viene scritto il file di blocco del progetto.</span><span class="sxs-lookup"><span data-stu-id="d0452-125">Output location where project lock file is written.</span></span> <span data-ttu-id="d0452-126">Per impostazione predefinita, tale valore è `PROJECT_ROOT\packages.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="d0452-126">By default, this is `PROJECT_ROOT\packages.lock.json`.</span></span>

- **`-LockedMode`**

  <span data-ttu-id="d0452-127">Non consentire l'aggiornamento del file di blocco del progetto.</span><span class="sxs-lookup"><span data-stu-id="d0452-127">Don't allow updating project lock file.</span></span>

- **`-MSBuildPath`**

   <span data-ttu-id="d0452-128">*(4.0 +)* Specifica il percorso di MSBuild da usare con il comando, avendo la precedenza su `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="d0452-128">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="d0452-129">*(3.2 +)* Specifica la versione di MSBuild da usare con questo comando.</span><span class="sxs-lookup"><span data-stu-id="d0452-129">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="d0452-130">I valori supportati sono 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="d0452-130">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="d0452-131">Per impostazione predefinita, viene scelto MSBuild nel percorso; in caso contrario, per impostazione predefinita viene impostata la versione più recente di MSBuild.</span><span class="sxs-lookup"><span data-stu-id="d0452-131">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoCache`**

  <span data-ttu-id="d0452-132">Impedisce a NuGet di usare pacchetti memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="d0452-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="d0452-133">Vedere [gestione dei pacchetti globali e delle cartelle della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="d0452-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="d0452-134">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d0452-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="d0452-135">Specifica la cartella in cui sono installati i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d0452-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="d0452-136">Se non viene specificata alcuna cartella, viene utilizzata la cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="d0452-136">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="d0452-137">Obbligatorio quando si esegue il ripristino con un `packages.config` file a meno che non `PackagesDirectory` `SolutionDirectory` venga usato o.</span><span class="sxs-lookup"><span data-stu-id="d0452-137">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="d0452-138">Specifica i tipi di file da salvare dopo l'installazione del pacchetto: uno tra `nuspec` , `nupkg` o `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="d0452-138">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="d0452-139">Uguale a `OutputDirectory`.</span><span class="sxs-lookup"><span data-stu-id="d0452-139">Same as `OutputDirectory`.</span></span> <span data-ttu-id="d0452-140">Obbligatorio quando si esegue il ripristino con un `packages.config` file a meno che non `OutputDirectory` `SolutionDirectory` venga usato o.</span><span class="sxs-lookup"><span data-stu-id="d0452-140">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span>

- **`-Project2ProjectTimeOut`**

  <span data-ttu-id="d0452-141">Timeout in secondi per la risoluzione di riferimenti da progetto a progetto.</span><span class="sxs-lookup"><span data-stu-id="d0452-141">Timeout in seconds for resolving project-to-project references.</span></span>

- **`-Recursive`**

  <span data-ttu-id="d0452-142">*(4.0 +)* Ripristina tutti i progetti di riferimento per i progetti UWP e .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d0452-142">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="d0452-143">Non si applica ai progetti che usano `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="d0452-143">Does not apply to projects using `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="d0452-144">Verifica che il ripristino dei pacchetti sia abilitato prima di scaricare e installare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d0452-144">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="d0452-145">Per informazioni dettagliate, vedere [ripristino di pacchetti](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="d0452-145">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="d0452-146">Specifica la cartella della soluzione.</span><span class="sxs-lookup"><span data-stu-id="d0452-146">Specifies the solution folder.</span></span> <span data-ttu-id="d0452-147">Non valido durante il ripristino dei pacchetti per una soluzione.</span><span class="sxs-lookup"><span data-stu-id="d0452-147">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="d0452-148">Obbligatorio quando si esegue il ripristino con un `packages.config` file a meno che non `PackagesDirectory` `OutputDirectory` venga usato o.</span><span class="sxs-lookup"><span data-stu-id="d0452-148">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span>

- **`-Source`**

  <span data-ttu-id="d0452-149">Specifica l'elenco di origini di pacchetti (come URL) da usare per il ripristino.</span><span class="sxs-lookup"><span data-stu-id="d0452-149">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="d0452-150">Se omesso, il comando usa le origini fornite nei file di configurazione, vedere [configurazione del comportamento di NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="d0452-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="d0452-151">Utilizzare un punto e virgola per separare le voci dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="d0452-151">Use a semicolon to separate list entries.</span></span>

- **`-UseLockFile`**

  <span data-ttu-id="d0452-152">Consente la generazione e l'utilizzo del file di blocco del progetto con il ripristino.</span><span class="sxs-lookup"><span data-stu-id="d0452-152">Enables project lock file to be generated and used with restore.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="d0452-153">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="d0452-153">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="d0452-154">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d0452-154">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="d0452-155">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="d0452-155">Remarks</span></span>

<span data-ttu-id="d0452-156">Il comando RESTORE esegue i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d0452-156">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="d0452-157">Determinare la modalità operativa del comando Restore.</span><span class="sxs-lookup"><span data-stu-id="d0452-157">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="d0452-158">tipo di file projectPath</span><span class="sxs-lookup"><span data-stu-id="d0452-158">projectPath file type</span></span> | <span data-ttu-id="d0452-159">Comportamento</span><span class="sxs-lookup"><span data-stu-id="d0452-159">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="d0452-160">Soluzione (cartella)</span><span class="sxs-lookup"><span data-stu-id="d0452-160">Solution (folder)</span></span> | <span data-ttu-id="d0452-161">NuGet Cerca un `.sln` file e lo usa se è stato trovato; in caso contrario, restituisce un errore.</span><span class="sxs-lookup"><span data-stu-id="d0452-161">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="d0452-162">`(SolutionDir)\.nuget` viene utilizzato come cartella iniziale.</span><span class="sxs-lookup"><span data-stu-id="d0452-162">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="d0452-163">File `.sln`</span><span class="sxs-lookup"><span data-stu-id="d0452-163">`.sln` file</span></span> | <span data-ttu-id="d0452-164">Ripristinare i pacchetti identificati dalla soluzione; Restituisce un errore se `-SolutionDirectory` viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="d0452-164">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="d0452-165">`$(SolutionDir)\.nuget` viene utilizzato come cartella iniziale.</span><span class="sxs-lookup"><span data-stu-id="d0452-165">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="d0452-166">`packages.config` o file di progetto</span><span class="sxs-lookup"><span data-stu-id="d0452-166">`packages.config` or project file</span></span> | <span data-ttu-id="d0452-167">Ripristinare i pacchetti elencati nel file, risolvendo e installando le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="d0452-167">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="d0452-168">Altro tipo di file</span><span class="sxs-lookup"><span data-stu-id="d0452-168">Other file type</span></span> | <span data-ttu-id="d0452-169">Si presuppone che il file sia un `.sln` file come sopra; se non è una soluzione, NuGet restituisce un errore.</span><span class="sxs-lookup"><span data-stu-id="d0452-169">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="d0452-170">(projectPath non specificato)</span><span class="sxs-lookup"><span data-stu-id="d0452-170">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="d0452-171">NuGet Cerca i file della soluzione nella cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="d0452-171">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="d0452-172">Se viene trovato un singolo file, viene usato per ripristinare i pacchetti; Se vengono rilevate più soluzioni, NuGet restituisce un errore.</span><span class="sxs-lookup"><span data-stu-id="d0452-172">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="d0452-173">Se non sono presenti file di soluzione, NuGet Cerca un oggetto `packages.config` e lo usa per ripristinare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d0452-173">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="d0452-174">Se non viene trovata alcuna soluzione o `packages.config` file, NuGet restituisce un errore.</span><span class="sxs-lookup"><span data-stu-id="d0452-174">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="d0452-175">Determinare la cartella dei pacchetti usando l'ordine di priorità seguente (NuGet restituisce un errore se nessuna di queste cartelle viene trovata):</span><span class="sxs-lookup"><span data-stu-id="d0452-175">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="d0452-176">Cartella specificata con `-PackagesDirectory` .</span><span class="sxs-lookup"><span data-stu-id="d0452-176">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="d0452-177">Il `repositoryPath` valore in `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="d0452-177">The `repositoryPath` value in `Nuget.Config`</span></span>
    - <span data-ttu-id="d0452-178">Cartella specificata con `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="d0452-178">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="d0452-179">Quando si ripristinano i pacchetti per una soluzione, NuGet esegue le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d0452-179">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="d0452-180">Carica il file di soluzione.</span><span class="sxs-lookup"><span data-stu-id="d0452-180">Loads the solution file.</span></span>
    - <span data-ttu-id="d0452-181">Ripristina i pacchetti a livello di soluzione elencati nella `$(SolutionDir)\.nuget\packages.config` `packages` cartella.</span><span class="sxs-lookup"><span data-stu-id="d0452-181">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="d0452-182">Ripristinare i pacchetti elencati nella `$(ProjectDir)\packages.config` `packages` cartella.</span><span class="sxs-lookup"><span data-stu-id="d0452-182">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="d0452-183">Per ogni pacchetto specificato, ripristinare il pacchetto in parallelo, a meno che non `-DisableParallelProcessing` sia specificato.</span><span class="sxs-lookup"><span data-stu-id="d0452-183">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="d0452-184">Esempi</span><span class="sxs-lookup"><span data-stu-id="d0452-184">Examples</span></span>

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
