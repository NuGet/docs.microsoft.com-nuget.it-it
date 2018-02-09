---
title: Aggiornare il comando CLI NuGet | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando di aggiornamento di nuget.exe
keywords: NuGet Aggiorna riferimento, il comando di pacchetto dell'aggiornamento
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 891ce1f27102b16125c93e7a66ebd29f6fc626db
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="dadfe-104">comando di aggiornamento (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="dadfe-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="dadfe-105">**Si applica a:** pacchetto consumo &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="dadfe-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="dadfe-106">Aggiorna tutti i pacchetti in un progetto (usando `packages.config`) alle versioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="dadfe-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="dadfe-107">È consigliabile eseguire ['restore'](cli-ref-restore.md) prima di eseguire il `update`.</span><span class="sxs-lookup"><span data-stu-id="dadfe-107">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="dadfe-108">(Per aggiornare un singolo pacchetto, utilizzare [ `nuget install` ](cli-ref-install.md) senza specificare un numero di versione, in cui NuGet case consente di installare la versione più recente.)</span><span class="sxs-lookup"><span data-stu-id="dadfe-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="dadfe-109">Nota: `update` non funziona con l'interfaccia CLI in esecuzione in Mono (Mac OSX o Linux) o quando si utilizza il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="dadfe-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="dadfe-110">Il `update` comando Aggiorna anche i riferimenti all'assembly nel file di progetto, fornito quelli fa riferimento a già esiste.</span><span class="sxs-lookup"><span data-stu-id="dadfe-110">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="dadfe-111">Se un pacchetto aggiornato è un assembly aggiunto, un nuovo riferimento è *non* aggiunto.</span><span class="sxs-lookup"><span data-stu-id="dadfe-111">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="dadfe-112">Inoltre, nuove dipendenze di pacchetto non sono i riferimenti ad assembly aggiunto.</span><span class="sxs-lookup"><span data-stu-id="dadfe-112">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="dadfe-113">Per includere queste operazioni come parte di un aggiornamento, aggiornare il pacchetto in Visual Studio utilizzando la UI Package Manager o la Console di gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="dadfe-113">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="dadfe-114">Questo comando può essere utilizzato anche per aggiornare nuget.exe stesso utilizzando il *-self* flag.</span><span class="sxs-lookup"><span data-stu-id="dadfe-114">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="dadfe-115">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="dadfe-115">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="dadfe-116">dove `<configPath>` identifica uno un `packages.config` o file di soluzione che elenca le dipendenze del progetto.</span><span class="sxs-lookup"><span data-stu-id="dadfe-116">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="dadfe-117">Opzioni</span><span class="sxs-lookup"><span data-stu-id="dadfe-117">Options</span></span>

| <span data-ttu-id="dadfe-118">Opzione</span><span class="sxs-lookup"><span data-stu-id="dadfe-118">Option</span></span> | <span data-ttu-id="dadfe-119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dadfe-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dadfe-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="dadfe-120">ConfigFile</span></span> | <span data-ttu-id="dadfe-121">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="dadfe-121">The NuGet configuration file to apply.</span></span> <span data-ttu-id="dadfe-122">Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="dadfe-122">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="dadfe-123">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="dadfe-123">FileConflictAction</span></span> | <span data-ttu-id="dadfe-124">Specifica l'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto.</span><span class="sxs-lookup"><span data-stu-id="dadfe-124">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="dadfe-125">I valori sono *sovrascrivere, ignorare, Nessuno*.</span><span class="sxs-lookup"><span data-stu-id="dadfe-125">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="dadfe-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="dadfe-126">ForceEnglishOutput</span></span> | <span data-ttu-id="dadfe-127">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="dadfe-127">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="dadfe-128">?</span><span class="sxs-lookup"><span data-stu-id="dadfe-128">Help</span></span> | <span data-ttu-id="dadfe-129">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="dadfe-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="dadfe-130">Id</span><span class="sxs-lookup"><span data-stu-id="dadfe-130">Id</span></span> | <span data-ttu-id="dadfe-131">Specifica un elenco di ID per l'aggiornamento pacchetto.</span><span class="sxs-lookup"><span data-stu-id="dadfe-131">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="dadfe-132">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="dadfe-132">MSBuildPath</span></span> | <span data-ttu-id="dadfe-133">*(4.0 +)*  Specifica il percorso di MSBuild da usare con il comando, che avrà la precedenza `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="dadfe-133">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="dadfe-134">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="dadfe-134">MSBuildVersion</span></span> | <span data-ttu-id="dadfe-135">*(3.2 +)*  Specifica la versione di MSBuild da usare con questo comando.</span><span class="sxs-lookup"><span data-stu-id="dadfe-135">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="dadfe-136">Valori supportati sono 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="dadfe-136">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="dadfe-137">Per impostazione predefinita che viene selezionato il percorso di MSBuild, in caso contrario il valore predefinito la versione più aggiornata di MSBuild.</span><span class="sxs-lookup"><span data-stu-id="dadfe-137">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="dadfe-138">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="dadfe-138">NonInteractive</span></span> | <span data-ttu-id="dadfe-139">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="dadfe-139">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="dadfe-140">Versione provvisoria</span><span class="sxs-lookup"><span data-stu-id="dadfe-140">PreRelease</span></span> | <span data-ttu-id="dadfe-141">Consente l'aggiornamento di versioni non definitive.</span><span class="sxs-lookup"><span data-stu-id="dadfe-141">Allows updating to prerelease versions.</span></span> <span data-ttu-id="dadfe-142">Questo flag non è richiesto durante l'aggiornamento preliminari pacchetti che sono già installati.</span><span class="sxs-lookup"><span data-stu-id="dadfe-142">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="dadfe-143">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="dadfe-143">RepositoryPath</span></span> | <span data-ttu-id="dadfe-144">Specifica la cartella locale in cui sono installati i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="dadfe-144">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="dadfe-145">Safe</span><span class="sxs-lookup"><span data-stu-id="dadfe-145">Safe</span></span> | <span data-ttu-id="dadfe-146">Specifica che solo gli aggiornamenti con la versione più recente disponibile all'interno della stessa versione principale e secondaria verrà installato il pacchetto installato.</span><span class="sxs-lookup"><span data-stu-id="dadfe-146">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="dadfe-147">Self</span><span class="sxs-lookup"><span data-stu-id="dadfe-147">Self</span></span> | <span data-ttu-id="dadfe-148">Nuget.exe gli aggiornamenti per la versione più recente; tutti gli altri argomenti vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="dadfe-148">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="dadfe-149">Origine</span><span class="sxs-lookup"><span data-stu-id="dadfe-149">Source</span></span> | <span data-ttu-id="dadfe-150">Specifica l'elenco delle origini pacchetto (come URL) da usare per gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="dadfe-150">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="dadfe-151">Se omesso, il comando Usa le origini disponibili in file di configurazione, vedere [il comportamento di configurazione NuGet](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="dadfe-151">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="dadfe-152">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="dadfe-152">Verbosity</span></span> | <span data-ttu-id="dadfe-153">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="dadfe-153">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="dadfe-154">Versione</span><span class="sxs-lookup"><span data-stu-id="dadfe-154">Version</span></span> | <span data-ttu-id="dadfe-155">Se usato con un ID di pacchetto, specifica la versione del pacchetto da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="dadfe-155">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="dadfe-156">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="dadfe-156">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="dadfe-157">Esempi</span><span class="sxs-lookup"><span data-stu-id="dadfe-157">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```