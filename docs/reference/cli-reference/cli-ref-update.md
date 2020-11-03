---
title: Comando di aggiornamento CLI di NuGet
description: Riferimento per il comando nuget.exe Update
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 106c4027f03d8e8c1d19545b3ca9b6cd5263830e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236789"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="22d88-103">comando Update (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="22d88-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="22d88-104">**Si applica a:** versioni supportate per l'utilizzo di pacchetti &bullet; **:** tutti</span><span class="sxs-lookup"><span data-stu-id="22d88-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="22d88-105">Esegue l'aggiornamento di tutti i pacchetti in un progetto (usando `packages.config`) alle versioni disponibili più recenti.</span><span class="sxs-lookup"><span data-stu-id="22d88-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="22d88-106">È consigliabile eseguire [' Restore '](cli-ref-restore.md) prima di eseguire `update` .</span><span class="sxs-lookup"><span data-stu-id="22d88-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="22d88-107">Per aggiornare un singolo pacchetto, usare [`nuget install`](cli-ref-install.md) senza specificare un numero di versione, nel qual caso NuGet installa la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="22d88-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="22d88-108">Nota: non `update` funziona con l'interfaccia della riga di comando in esecuzione in mono (Mac OSX o Linux) o quando si usa il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="22d88-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="22d88-109">Il `update` comando Aggiorna inoltre i riferimenti ad assembly nel file di progetto, a condizione che tali riferimenti esistano già.</span><span class="sxs-lookup"><span data-stu-id="22d88-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="22d88-110">Se un pacchetto aggiornato include un assembly aggiunto, *non* viene aggiunto un nuovo riferimento.</span><span class="sxs-lookup"><span data-stu-id="22d88-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="22d88-111">Anche per le nuove dipendenze dei pacchetti non sono stati aggiunti riferimenti ad assembly.</span><span class="sxs-lookup"><span data-stu-id="22d88-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="22d88-112">Per includere queste operazioni come parte di un aggiornamento, aggiornare il pacchetto in Visual Studio usando l'interfaccia utente di gestione pacchetti o la console di gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="22d88-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="22d88-113">Questo comando può essere usato anche per aggiornare nuget.exe stesso usando il flag *-self* .</span><span class="sxs-lookup"><span data-stu-id="22d88-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="22d88-114">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="22d88-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="22d88-115">dove `<configPath>` identifica un `packages.config` file di soluzione o che elenca le dipendenze del progetto.</span><span class="sxs-lookup"><span data-stu-id="22d88-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="22d88-116">Opzioni</span><span class="sxs-lookup"><span data-stu-id="22d88-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="22d88-117">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="22d88-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="22d88-118">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="22d88-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  <span data-ttu-id="22d88-119">Specifica la versione dei pacchetti di dipendenze da usare. i possibili tipi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="22d88-119">Specifies the version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="22d88-120">*Minimo* (impostazione predefinita): versione più bassa</span><span class="sxs-lookup"><span data-stu-id="22d88-120">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="22d88-121">*HighestPatch* : versione con la patch principale più bassa, minore minore, più alta</span><span class="sxs-lookup"><span data-stu-id="22d88-121">*HighestPatch* : the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="22d88-122">*HighestMinor* : versione con la patch principale più bassa, minore più elevata</span><span class="sxs-lookup"><span data-stu-id="22d88-122">*HighestMinor* : the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="22d88-123">*Massimo* : la versione più recente</span><span class="sxs-lookup"><span data-stu-id="22d88-123">*Highest* : the highest version</span></span></li><li><span data-ttu-id="22d88-124">*Ignora* : non verrà usato alcun pacchetto di dipendenza</span><span class="sxs-lookup"><span data-stu-id="22d88-124">*Ignore* : No dependency packages will be used</span></span></li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="22d88-125">Specifica l'azione predefinita quando un file di un pacchetto esiste già nel progetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="22d88-125">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="22d88-126">Impostare su `Overwrite` per sovrascrivere sempre i file.</span><span class="sxs-lookup"><span data-stu-id="22d88-126">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="22d88-127">Impostare su `Ignore` per ignorare i file.</span><span class="sxs-lookup"><span data-stu-id="22d88-127">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="22d88-128">`PromptUser`Per impostazione predefinita, l'azione richiederà tutti i file in conflitto, a meno che non `OverwriteAll` `IgnoreAll` sia specificato o, che verrà applicato a tutti i file rimanenti.</span><span class="sxs-lookup"><span data-stu-id="22d88-128">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="22d88-129">*(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="22d88-129">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="22d88-130">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="22d88-130">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="22d88-131">Specifica un elenco di ID di pacchetto da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="22d88-131">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="22d88-132">*(4.0 +)* Specifica il percorso di MSBuild da usare con il comando, avendo la precedenza su `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="22d88-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="22d88-133">*(3.2 +)* Specifica la versione di MSBuild da usare con questo comando.</span><span class="sxs-lookup"><span data-stu-id="22d88-133">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="22d88-134">I valori supportati sono 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="22d88-134">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="22d88-135">Per impostazione predefinita, viene scelto MSBuild nel percorso; in caso contrario, per impostazione predefinita viene impostata la versione più recente di MSBuild.</span><span class="sxs-lookup"><span data-stu-id="22d88-135">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="22d88-136">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="22d88-136">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="22d88-137">Consente l'aggiornamento alle versioni provvisorie.</span><span class="sxs-lookup"><span data-stu-id="22d88-137">Allows updating to prerelease versions.</span></span> <span data-ttu-id="22d88-138">Questo flag non è obbligatorio quando si aggiornano i pacchetti di versioni non definitive già installati.</span><span class="sxs-lookup"><span data-stu-id="22d88-138">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="22d88-139">Specifica la cartella locale in cui sono installati i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="22d88-139">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="22d88-140">Specifica che verranno installati solo gli aggiornamenti con la versione più recente disponibile all'interno della stessa versione principale e secondaria del pacchetto installato.</span><span class="sxs-lookup"><span data-stu-id="22d88-140">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="22d88-141">Aggiorna nuget.exe alla versione più recente. tutti gli altri argomenti vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="22d88-141">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span>

- **`-Source`**

  <span data-ttu-id="22d88-142">Specifica l'elenco di origini di pacchetti (come URL) da usare per gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="22d88-142">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="22d88-143">Se omesso, il comando usa le origini fornite nei file di configurazione, vedere [configurazioni comuni di NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="22d88-143">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="22d88-144">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="22d88-144">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="22d88-145">Se utilizzata con un ID pacchetto, specifica la versione del pacchetto da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="22d88-145">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="22d88-146">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="22d88-146">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="22d88-147">Esempi</span><span class="sxs-lookup"><span data-stu-id="22d88-147">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
