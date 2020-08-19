---
title: Comando di installazione CLI NuGet
description: Riferimento per il comando nuget.exe install
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 23856728d07d07183b5aedcd6218a56a444c410b
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623097"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="8a03a-103">comando di installazione (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="8a03a-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="8a03a-104">**Si applica a:** versioni supportate per l'utilizzo di pacchetti &bullet; **:** tutti</span><span class="sxs-lookup"><span data-stu-id="8a03a-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8a03a-105">Consente di scaricare e installare un pacchetto in un progetto, per impostazione predefinita la cartella corrente, utilizzando le origini di pacchetti specificate.</span><span class="sxs-lookup"><span data-stu-id="8a03a-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="8a03a-106">Per scaricare un pacchetto direttamente al di fuori del contesto di un progetto, visitare la pagina del pacchetto in [NuGet.org](https://www.nuget.org) e selezionare il collegamento per il **download** .</span><span class="sxs-lookup"><span data-stu-id="8a03a-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="8a03a-107">Se non viene specificata alcuna origine, vengono usati quelli elencati nel file di configurazione globale `%appdata%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="8a03a-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="8a03a-108">Per ulteriori informazioni, vedere [configurazioni NuGet comuni](../../consume-packages/configuring-nuget-behavior.md) .</span><span class="sxs-lookup"><span data-stu-id="8a03a-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="8a03a-109">Se non viene specificato alcun pacchetto specifico, `install` installa tutti i pacchetti elencati nel file del progetto `packages.config` , rendendoli simili a [`restore`](cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="8a03a-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="8a03a-110">Il `install` comando non modifica un file di progetto o `packages.config` . in questo modo è simile a `restore` in quanto aggiunge solo pacchetti al disco, ma non modifica le dipendenze di un progetto.</span><span class="sxs-lookup"><span data-stu-id="8a03a-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="8a03a-111">Per aggiungere una dipendenza, aggiungere un pacchetto tramite l'interfaccia utente o la console di gestione pacchetti in Visual Studio oppure modificare `packages.config` e quindi eseguire `install` o `restore` .</span><span class="sxs-lookup"><span data-stu-id="8a03a-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="8a03a-112">Uso</span><span class="sxs-lookup"><span data-stu-id="8a03a-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="8a03a-113">dove `<packageID>` denomina il pacchetto da installare (usando la versione più recente) o `<configFilePath>` identifica il `packages.config` file in cui sono elencati i pacchetti da installare.</span><span class="sxs-lookup"><span data-stu-id="8a03a-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="8a03a-114">È possibile indicare una versione specifica con l' `-Version` opzione.</span><span class="sxs-lookup"><span data-stu-id="8a03a-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="8a03a-115">Opzioni</span><span class="sxs-lookup"><span data-stu-id="8a03a-115">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="8a03a-116">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="8a03a-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8a03a-117">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="8a03a-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DependencyVersion`**

  <span data-ttu-id="8a03a-118">*(4.4 +)* Versione dei pacchetti di dipendenze da usare. i possibili tipi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a03a-118">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="8a03a-119">*Minimo* (impostazione predefinita): versione più bassa</span><span class="sxs-lookup"><span data-stu-id="8a03a-119">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="8a03a-120">*HighestPatch*: versione con la patch principale più bassa, minore minore, più alta</span><span class="sxs-lookup"><span data-stu-id="8a03a-120">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="8a03a-121">*HighestMinor*: versione con la patch principale più bassa, minore più elevata</span><span class="sxs-lookup"><span data-stu-id="8a03a-121">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="8a03a-122">*Massimo*: la versione più recente</span><span class="sxs-lookup"><span data-stu-id="8a03a-122">*Highest*: the highest version</span></span></li><li><span data-ttu-id="8a03a-123">*Ignora*: non verrà usato alcun pacchetto di dipendenza</span><span class="sxs-lookup"><span data-stu-id="8a03a-123">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-DirectDownload`**

  <span data-ttu-id="8a03a-124">Scaricare direttamente senza popolare alcuna cache con metadati o file binari.</span><span class="sxs-lookup"><span data-stu-id="8a03a-124">Download directly without populating any caches with metadata or binaries.</span></span>

- **`-DisableParallelProcessing`**

  <span data-ttu-id="8a03a-125">Disabilita l'installazione di più pacchetti in parallelo.</span><span class="sxs-lookup"><span data-stu-id="8a03a-125">Disables installing multiple packages in parallel.</span></span>

- **`-x|-ExcludeVersion`**

  <span data-ttu-id="8a03a-126">Installa il pacchetto in una cartella denominata solo con il nome del pacchetto e non con il numero di versione.</span><span class="sxs-lookup"><span data-stu-id="8a03a-126">Installs the package to a folder named with only the package name and not the version number.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="8a03a-127">*(3.2 +)* Elenco di origini di pacchetti da usare come fallback nel caso in cui il pacchetto non venga trovato nell'origine primaria o predefinita.</span><span class="sxs-lookup"><span data-stu-id="8a03a-127">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="8a03a-128">*(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="8a03a-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Framework`**

  <span data-ttu-id="8a03a-129">*(4.4 +)* Framework di destinazione usato per la selezione delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="8a03a-129">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="8a03a-130">Se non è specificato, il valore predefinito è' any '.</span><span class="sxs-lookup"><span data-stu-id="8a03a-130">Defaults to 'Any' if not specified.</span></span>

- **`-?|-help`**

  <span data-ttu-id="8a03a-131">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="8a03a-131">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="8a03a-132">Impedisce a NuGet di usare pacchetti memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="8a03a-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="8a03a-133">Vedere [gestione dei pacchetti globali e delle cartelle della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="8a03a-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="8a03a-134">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8a03a-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="8a03a-135">Specifica la cartella in cui sono installati i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="8a03a-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="8a03a-136">Se non viene specificata alcuna cartella, viene utilizzata la cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="8a03a-136">If no folder is specified, the current folder is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="8a03a-137">Specifica i tipi di file da salvare dopo l'installazione del pacchetto: uno tra `nuspec` , `nupkg` o `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="8a03a-137">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="8a03a-138">Consente l'installazione dei pacchetti di versioni non definitive.</span><span class="sxs-lookup"><span data-stu-id="8a03a-138">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="8a03a-139">Questo flag non è obbligatorio quando si ripristinano i pacchetti con `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="8a03a-139">This flag is not required when restoring packages with `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="8a03a-140">Verifica che il ripristino dei pacchetti sia abilitato prima di scaricare e installare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="8a03a-140">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="8a03a-141">Per informazioni dettagliate, vedere [ripristino di pacchetti](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="8a03a-141">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="8a03a-142">Specifica la cartella radice della soluzione per cui ripristinare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="8a03a-142">Specifies root folder of the solution for which to restore packages.</span></span>

- **`-Source`**

   <span data-ttu-id="8a03a-143">Specifica l'elenco di origini di pacchetti (come URL) da usare.</span><span class="sxs-lookup"><span data-stu-id="8a03a-143">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="8a03a-144">Se omesso, il comando usa le origini fornite nei file di configurazione, vedere [configurazioni comuni di NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="8a03a-144">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="8a03a-145">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="8a03a-145">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="8a03a-146">Specifica la versione del pacchetto da installare.</span><span class="sxs-lookup"><span data-stu-id="8a03a-146">Specifies the version of the package to install.</span></span>

<span data-ttu-id="8a03a-147">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8a03a-147">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8a03a-148">Esempi</span><span class="sxs-lookup"><span data-stu-id="8a03a-148">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
