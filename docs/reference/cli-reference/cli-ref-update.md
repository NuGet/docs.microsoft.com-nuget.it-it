---
title: Comando di aggiornamento CLI di NuGet
description: Riferimento per il comando di aggiornamento di NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327508"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="5bf19-103">Comando update (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="5bf19-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="5bf19-104">**Si applica a:** &bullet; **versioni supportate** per l'utilizzo di pacchetti: tutti</span><span class="sxs-lookup"><span data-stu-id="5bf19-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5bf19-105">Esegue l'aggiornamento di tutti i pacchetti in un progetto (usando `packages.config`) alle versioni disponibili più recenti.</span><span class="sxs-lookup"><span data-stu-id="5bf19-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="5bf19-106">È consigliabile eseguire [' Restore '](cli-ref-restore.md) prima di eseguire `update`.</span><span class="sxs-lookup"><span data-stu-id="5bf19-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="5bf19-107">Per aggiornare un singolo pacchetto, usare [`nuget install`](cli-ref-install.md) senza specificare un numero di versione, nel qual caso NuGet installa la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="5bf19-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="5bf19-108">Nota: `update` non funziona con l'interfaccia della riga di comando in esecuzione in mono (Mac OSX o Linux) o quando si usa il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="5bf19-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="5bf19-109">Il `update` comando Aggiorna inoltre i riferimenti ad assembly nel file di progetto, a condizione che tali riferimenti esistano già.</span><span class="sxs-lookup"><span data-stu-id="5bf19-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="5bf19-110">Se un pacchetto aggiornato include un assembly aggiunto, *non* viene aggiunto un nuovo riferimento.</span><span class="sxs-lookup"><span data-stu-id="5bf19-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="5bf19-111">Anche per le nuove dipendenze dei pacchetti non sono stati aggiunti riferimenti ad assembly.</span><span class="sxs-lookup"><span data-stu-id="5bf19-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="5bf19-112">Per includere queste operazioni come parte di un aggiornamento, aggiornare il pacchetto in Visual Studio usando l'interfaccia utente di gestione pacchetti o la console di gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5bf19-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="5bf19-113">Questo comando può essere usato anche per aggiornare NuGet. exe con il flag *-self* .</span><span class="sxs-lookup"><span data-stu-id="5bf19-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="5bf19-114">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="5bf19-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="5bf19-115">dove `<configPath>` identifica un `packages.config` file di soluzione o che elenca le dipendenze del progetto.</span><span class="sxs-lookup"><span data-stu-id="5bf19-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="5bf19-116">Opzioni</span><span class="sxs-lookup"><span data-stu-id="5bf19-116">Options</span></span>

| <span data-ttu-id="5bf19-117">Opzione</span><span class="sxs-lookup"><span data-stu-id="5bf19-117">Option</span></span> | <span data-ttu-id="5bf19-118">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5bf19-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5bf19-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5bf19-119">ConfigFile</span></span> | <span data-ttu-id="5bf19-120">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="5bf19-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5bf19-121">Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="5bf19-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5bf19-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="5bf19-122">FileConflictAction</span></span> | <span data-ttu-id="5bf19-123">Specifica l'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto.</span><span class="sxs-lookup"><span data-stu-id="5bf19-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="5bf19-124">I valori sono *overwrite, ignore, None*.</span><span class="sxs-lookup"><span data-stu-id="5bf19-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="5bf19-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5bf19-125">ForceEnglishOutput</span></span> | <span data-ttu-id="5bf19-126">*(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese.</span><span class="sxs-lookup"><span data-stu-id="5bf19-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5bf19-127">Help</span><span class="sxs-lookup"><span data-stu-id="5bf19-127">Help</span></span> | <span data-ttu-id="5bf19-128">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="5bf19-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="5bf19-129">ID</span><span class="sxs-lookup"><span data-stu-id="5bf19-129">Id</span></span> | <span data-ttu-id="5bf19-130">Specifica un elenco di ID di pacchetto da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="5bf19-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="5bf19-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="5bf19-131">MSBuildPath</span></span> | <span data-ttu-id="5bf19-132">*(4.0 +)* Specifica il percorso di MSBuild da usare con il comando, avendo la precedenza `-MSBuildVersion`su.</span><span class="sxs-lookup"><span data-stu-id="5bf19-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="5bf19-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="5bf19-133">MSBuildVersion</span></span> | <span data-ttu-id="5bf19-134">*(3.2 +)* Specifica la versione di MSBuild da usare con questo comando.</span><span class="sxs-lookup"><span data-stu-id="5bf19-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="5bf19-135">I valori supportati sono 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="5bf19-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="5bf19-136">Per impostazione predefinita, viene scelto MSBuild nel percorso; in caso contrario, per impostazione predefinita viene impostata la versione più recente di MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5bf19-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="5bf19-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="5bf19-137">NonInteractive</span></span> | <span data-ttu-id="5bf19-138">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5bf19-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5bf19-139">PreRelease</span><span class="sxs-lookup"><span data-stu-id="5bf19-139">PreRelease</span></span> | <span data-ttu-id="5bf19-140">Consente l'aggiornamento alle versioni provvisorie.</span><span class="sxs-lookup"><span data-stu-id="5bf19-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="5bf19-141">Questo flag non è obbligatorio quando si aggiornano i pacchetti di versioni non definitive già installati.</span><span class="sxs-lookup"><span data-stu-id="5bf19-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="5bf19-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="5bf19-142">RepositoryPath</span></span> | <span data-ttu-id="5bf19-143">Specifica la cartella locale in cui sono installati i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5bf19-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="5bf19-144">Safe</span><span class="sxs-lookup"><span data-stu-id="5bf19-144">Safe</span></span> | <span data-ttu-id="5bf19-145">Specifica che verranno installati solo gli aggiornamenti con la versione più recente disponibile all'interno della stessa versione principale e secondaria del pacchetto installato.</span><span class="sxs-lookup"><span data-stu-id="5bf19-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="5bf19-146">Auto</span><span class="sxs-lookup"><span data-stu-id="5bf19-146">Self</span></span> | <span data-ttu-id="5bf19-147">Aggiorna NuGet. exe alla versione più recente. tutti gli altri argomenti vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="5bf19-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="5bf19-148">Source</span><span class="sxs-lookup"><span data-stu-id="5bf19-148">Source</span></span> | <span data-ttu-id="5bf19-149">Specifica l'elenco di origini di pacchetti (come URL) da usare per gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="5bf19-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="5bf19-150">Se omesso, il comando usa le origini fornite nei file di configurazione, vedere [configurazioni comuni di NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="5bf19-150">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="5bf19-151">Verbosity</span><span class="sxs-lookup"><span data-stu-id="5bf19-151">Verbosity</span></span> | <span data-ttu-id="5bf19-152">Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*.</span><span class="sxs-lookup"><span data-stu-id="5bf19-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="5bf19-153">Version</span><span class="sxs-lookup"><span data-stu-id="5bf19-153">Version</span></span> | <span data-ttu-id="5bf19-154">Se utilizzata con un ID pacchetto, specifica la versione del pacchetto da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="5bf19-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="5bf19-155">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5bf19-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5bf19-156">Esempi</span><span class="sxs-lookup"><span data-stu-id="5bf19-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
