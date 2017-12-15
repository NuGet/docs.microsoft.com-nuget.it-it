---
title: Aggiornare il comando CLI NuGet | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 61fde945-6983-46a5-8636-da0fada4e641
description: Riferimento per il comando di aggiornamento di nuget.exe
keywords: NuGet Aggiorna riferimento, il comando di pacchetto dell'aggiornamento
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 654144e93a99a4a4f8d79c0db5660cfb7c6c308e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="392a7-104">comando di aggiornamento (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="392a7-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="392a7-105">**Si applica a:** pacchetto consumo &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="392a7-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="392a7-106">Aggiorna tutti i pacchetti in un progetto (usando `packages.config`) alle versioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="392a7-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="392a7-107">È consigliabile eseguire ['restore'](#restore) prima di eseguire il `update`.</span><span class="sxs-lookup"><span data-stu-id="392a7-107">It is recommended to run ['restore'](#restore) before running the `update`.</span></span> <span data-ttu-id="392a7-108">(Per aggiornare un singolo pacchetto, utilizzare [ `nuget install` ](cli-ref-install.md) senza specificare un numero di versione, in cui NuGet case consente di installare la versione più recente.)</span><span class="sxs-lookup"><span data-stu-id="392a7-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="392a7-109">Nota: `update` non funziona con l'interfaccia CLI in esecuzione in Mono (Mac OSX o Linux).</span><span class="sxs-lookup"><span data-stu-id="392a7-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux).</span></span> <span data-ttu-id="392a7-110">Il comando non funziona inoltre con i progetti utilizzando `project.json` o PackageReference gestione formati.</span><span class="sxs-lookup"><span data-stu-id="392a7-110">The command also does not work with projects using `project.json` or PackageReference management formats.</span></span>

<span data-ttu-id="392a7-111">Il `update` comando Aggiorna anche i riferimenti all'assembly nel file di progetto, fornito quelli fa riferimento a già esiste.</span><span class="sxs-lookup"><span data-stu-id="392a7-111">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="392a7-112">Se un pacchetto aggiornato è un assembly aggiunto, un nuovo riferimento è *non* aggiunto.</span><span class="sxs-lookup"><span data-stu-id="392a7-112">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="392a7-113">Inoltre, nuove dipendenze di pacchetto non sono i riferimenti ad assembly aggiunto.</span><span class="sxs-lookup"><span data-stu-id="392a7-113">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="392a7-114">Per includere queste operazioni come parte di un aggiornamento, aggiornare il pacchetto in Visual Studio utilizzando la UI Package Manager o la Console di gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="392a7-114">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="392a7-115">Questo comando può essere utilizzato anche per aggiornare nuget.exe stesso utilizzando il *-self* flag.</span><span class="sxs-lookup"><span data-stu-id="392a7-115">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="392a7-116">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="392a7-116">Usage</span></span>

```
nuget update <configPath> [options]
```

<span data-ttu-id="392a7-117">dove `<configPath>` identifica uno un `packages.config` o file di soluzione che elenca le dipendenze del progetto.</span><span class="sxs-lookup"><span data-stu-id="392a7-117">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="392a7-118">Opzioni</span><span class="sxs-lookup"><span data-stu-id="392a7-118">Options</span></span>

| <span data-ttu-id="392a7-119">Opzione</span><span class="sxs-lookup"><span data-stu-id="392a7-119">Option</span></span> | <span data-ttu-id="392a7-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="392a7-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="392a7-121">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="392a7-121">ConfigFile</span></span> | <span data-ttu-id="392a7-122">*(2.5 +)*  Questo file di configurazione da applicare.</span><span class="sxs-lookup"><span data-stu-id="392a7-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="392a7-123">Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="392a7-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="392a7-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="392a7-124">FileConflictAction</span></span> | <span data-ttu-id="392a7-125">*(2.5 +)*  Specifica l'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto.</span><span class="sxs-lookup"><span data-stu-id="392a7-125">*(2.5+)* Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="392a7-126">I valori sono *sovrascrivere, ignorare, Nessuno*.</span><span class="sxs-lookup"><span data-stu-id="392a7-126">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="392a7-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="392a7-127">ForceEnglishOutput</span></span> | <span data-ttu-id="392a7-128">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="392a7-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="392a7-129">?</span><span class="sxs-lookup"><span data-stu-id="392a7-129">Help</span></span> | <span data-ttu-id="392a7-130">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="392a7-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="392a7-131">Id</span><span class="sxs-lookup"><span data-stu-id="392a7-131">Id</span></span> | <span data-ttu-id="392a7-132">Specifica un elenco di ID per l'aggiornamento pacchetto.</span><span class="sxs-lookup"><span data-stu-id="392a7-132">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="392a7-133">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="392a7-133">MSBuildPath</span></span> | <span data-ttu-id="392a7-134">*(4.0 +)*  Specifica il percorso di MSBuild da usare con il comando, che avrà la precedenza `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="392a7-134">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="392a7-135">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="392a7-135">MSBuildVersion</span></span> | <span data-ttu-id="392a7-136">*(3.2 +)*  Specifica la versione di MSBuild da usare con questo comando.</span><span class="sxs-lookup"><span data-stu-id="392a7-136">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="392a7-137">Valori supportati sono 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="392a7-137">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="392a7-138">Per impostazione predefinita che viene selezionato il percorso di MSBuild, in caso contrario il valore predefinito la versione più aggiornata di MSBuild.</span><span class="sxs-lookup"><span data-stu-id="392a7-138">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="392a7-139">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="392a7-139">NonInteractive</span></span> | <span data-ttu-id="392a7-140">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="392a7-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="392a7-141">Versione provvisoria</span><span class="sxs-lookup"><span data-stu-id="392a7-141">PreRelease</span></span> | <span data-ttu-id="392a7-142">Consente l'aggiornamento di versioni non definitive.</span><span class="sxs-lookup"><span data-stu-id="392a7-142">Allows updating to prerelease versions.</span></span> <span data-ttu-id="392a7-143">Questo flag non è richiesto durante l'aggiornamento preliminari pacchetti che sono già installati.</span><span class="sxs-lookup"><span data-stu-id="392a7-143">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="392a7-144">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="392a7-144">RepositoryPath</span></span> | <span data-ttu-id="392a7-145">Specifica la cartella locale in cui sono installati i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="392a7-145">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="392a7-146">Safe</span><span class="sxs-lookup"><span data-stu-id="392a7-146">Safe</span></span> | <span data-ttu-id="392a7-147">Specifica che solo gli aggiornamenti con la versione più recente disponibile all'interno della stessa versione principale e secondaria verrà installato il pacchetto installato.</span><span class="sxs-lookup"><span data-stu-id="392a7-147">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="392a7-148">Self</span><span class="sxs-lookup"><span data-stu-id="392a7-148">Self</span></span> | <span data-ttu-id="392a7-149">*(1.4 +)*  Aggiorna nuget.exe alla versione più recente; vengono ignorati tutti gli altri argomenti.</span><span class="sxs-lookup"><span data-stu-id="392a7-149">*(1.4+)* Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="392a7-150">Origine</span><span class="sxs-lookup"><span data-stu-id="392a7-150">Source</span></span> | <span data-ttu-id="392a7-151">Specifica l'elenco delle origini pacchetto (come URL) da usare per gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="392a7-151">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="392a7-152">Se omesso, il comando Usa le origini disponibili in file di configurazione, vedere [il comportamento di configurazione NuGet](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="392a7-152">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="392a7-153">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="392a7-153">Verbosity</span></span> | <span data-ttu-id="392a7-154">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="392a7-154">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="392a7-155">Versione</span><span class="sxs-lookup"><span data-stu-id="392a7-155">Version</span></span> | <span data-ttu-id="392a7-156">Se usato con un ID di pacchetto, specifica la versione del pacchetto da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="392a7-156">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="392a7-157">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="392a7-157">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="392a7-158">Esempi</span><span class="sxs-lookup"><span data-stu-id="392a7-158">Examples</span></span>

```
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
