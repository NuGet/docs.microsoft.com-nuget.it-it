---
title: Comando di aggiornamento dell'interfaccia della riga di comando di NuGet
description: Riferimento per il comando nuget.exe update
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323648"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="ac910-103">Comando update (interfaccia della riga di comando NuGet)</span><span class="sxs-lookup"><span data-stu-id="ac910-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="ac910-104">**Si applica a:** Utilizzo pacchetti &bullet; **Versioni supportate:** tutte</span><span class="sxs-lookup"><span data-stu-id="ac910-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ac910-105">Esegue l'aggiornamento di tutti i pacchetti in un progetto (usando `packages.config`) alle versioni disponibili più recenti.</span><span class="sxs-lookup"><span data-stu-id="ac910-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="ac910-106">È consigliabile eseguire ['restore'](cli-ref-restore.md) prima di eseguire `update` .</span><span class="sxs-lookup"><span data-stu-id="ac910-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="ac910-107">Per aggiornare un singolo pacchetto, usare senza specificare un numero di versione, nel qual caso [`nuget install`](cli-ref-install.md) NuGet installa la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="ac910-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="ac910-108">Nota: non funziona con l'interfaccia della riga di comando in esecuzione in Mono (Mac OSX o Linux) o quando `update` si usa il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="ac910-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="ac910-109">Il `update` comando aggiorna anche i riferimenti agli assembly nel file di progetto, a condizione che tali riferimenti esistano già.</span><span class="sxs-lookup"><span data-stu-id="ac910-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="ac910-110">Se a un pacchetto aggiornato è stato aggiunto un assembly, non viene aggiunto *un nuovo* riferimento.</span><span class="sxs-lookup"><span data-stu-id="ac910-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="ac910-111">Alle nuove dipendenze del pacchetto non vengono aggiunti anche i riferimenti agli assembly.</span><span class="sxs-lookup"><span data-stu-id="ac910-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="ac910-112">Per includere queste operazioni come parte di un aggiornamento, aggiornare il pacchetto in Visual Studio usando l'interfaccia Gestione pacchetti o la console Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="ac910-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="ac910-113">Questo comando può essere usato anche per aggiornare nuget.exe usando il flag *-self.*</span><span class="sxs-lookup"><span data-stu-id="ac910-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="ac910-114">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="ac910-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="ac910-115">dove `<configPath>` identifica un file di soluzione o che elenca le `packages.config` dipendenze del progetto.</span><span class="sxs-lookup"><span data-stu-id="ac910-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="ac910-116">Opzioni</span><span class="sxs-lookup"><span data-stu-id="ac910-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="ac910-117">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="ac910-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ac910-118">Se non specificato, `%AppData%\NuGet\NuGet.Config` viene usato `~/.nuget/NuGet/NuGet.Config` (Windows) o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="ac910-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  <span data-ttu-id="ac910-119">Specifica la versione dei pacchetti di dipendenze da usare, che può essere una delle seguenti:</span><span class="sxs-lookup"><span data-stu-id="ac910-119">Specifies the version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="ac910-120">*Minimo* (impostazione predefinita): la versione più bassa</span><span class="sxs-lookup"><span data-stu-id="ac910-120">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="ac910-121">*HighestPatch:* la versione con la patch principale, secondaria più bassa e più alta</span><span class="sxs-lookup"><span data-stu-id="ac910-121">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="ac910-122">*HighestMinor:* la versione con la patch principale, secondaria più alta e più alta</span><span class="sxs-lookup"><span data-stu-id="ac910-122">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="ac910-123">*Più alta:* la versione più alta</span><span class="sxs-lookup"><span data-stu-id="ac910-123">*Highest*: the highest version</span></span></li><li><span data-ttu-id="ac910-124">*Ignora:* non verranno usati pacchetti di dipendenze</span><span class="sxs-lookup"><span data-stu-id="ac910-124">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="ac910-125">Specifica l'azione predefinita quando un file di un pacchetto esiste già nel progetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="ac910-125">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="ac910-126">Impostare su `Overwrite` per sovrascrivere sempre i file.</span><span class="sxs-lookup"><span data-stu-id="ac910-126">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="ac910-127">Impostare su `Ignore` per ignorare i file.</span><span class="sxs-lookup"><span data-stu-id="ac910-127">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="ac910-128">L'azione, l'impostazione predefinita, richiederà ogni file in conflitto, a meno che non venga specificato o `PromptUser` , che verrà applicato a tutti i file `OverwriteAll` `IgnoreAll` rimanenti.</span><span class="sxs-lookup"><span data-stu-id="ac910-128">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="ac910-129">*(3.5+)* Forza nuget.exe'esecuzione usando impostazioni cultura invarianti basate sull'inglese.</span><span class="sxs-lookup"><span data-stu-id="ac910-129">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="ac910-130">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="ac910-130">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="ac910-131">Specifica un elenco di ID pacchetto da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="ac910-131">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="ac910-132">*(4.0+)* Specifica il percorso di MSBuild da usare con il comando , che ha la precedenza su `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="ac910-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="ac910-133">*(3.2+)* Specifica la versione di MSBuild da usare con questo comando.</span><span class="sxs-lookup"><span data-stu-id="ac910-133">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="ac910-134">I valori supportati sono 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span><span class="sxs-lookup"><span data-stu-id="ac910-134">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="ac910-135">Per impostazione predefinita, msBuild nel percorso viene selezionato, in caso contrario viene impostata la versione installata più elevata di MSBuild.</span><span class="sxs-lookup"><span data-stu-id="ac910-135">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="ac910-136">Elimina le richieste di input o di conferma dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ac910-136">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="ac910-137">Consente l'aggiornamento alle versioni non definitive.</span><span class="sxs-lookup"><span data-stu-id="ac910-137">Allows updating to prerelease versions.</span></span> <span data-ttu-id="ac910-138">Questo flag non è obbligatorio quando si aggiornano pacchetti non definitive già installati.</span><span class="sxs-lookup"><span data-stu-id="ac910-138">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="ac910-139">Specifica la cartella locale in cui vengono installati i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="ac910-139">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="ac910-140">Specifica che verranno installati solo gli aggiornamenti con la versione più recente disponibile nella stessa versione principale e secondaria del pacchetto installato.</span><span class="sxs-lookup"><span data-stu-id="ac910-140">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="ac910-141">Aggiornamenti `nuget.exe` alla versione più recente.</span><span class="sxs-lookup"><span data-stu-id="ac910-141">Updates `nuget.exe` to the latest version.</span></span> <span data-ttu-id="ac910-142">`-Source` È possibile usare tuttavia tutti gli altri argomenti vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="ac910-142">`-Source` can be used however all other arguments are ignored.</span></span> <span data-ttu-id="ac910-143">Se non viene specificata alcuna origine, verifica `nuget.org` la disponibilità di aggiornamenti indipendentemente dalle `NuGet.Config` impostazioni.</span><span class="sxs-lookup"><span data-stu-id="ac910-143">If no source is provided, checks `nuget.org` for updates regardless of `NuGet.Config` settings.</span></span>

- **`-Source`**

  <span data-ttu-id="ac910-144">Specifica l'elenco di origini dei pacchetti (come URL) da usare per gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="ac910-144">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="ac910-145">Se omesso, il comando usa le origini fornite nei file di configurazione, vedere [Configurazioni NuGet comuni](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ac910-145">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="ac910-146">Specifica la quantità di dettagli visualizzati nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="ac910-146">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="ac910-147">Se usato con un ID pacchetto, specifica la versione del pacchetto da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="ac910-147">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="ac910-148">Vedere anche [Variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ac910-148">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ac910-149">Esempi</span><span class="sxs-lookup"><span data-stu-id="ac910-149">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
