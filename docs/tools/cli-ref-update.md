---
title: Comando update NuGet CLI
description: Riferimento per il comando di aggiornamento di nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 39e269b10a0cf144d5971d2af9f82a606e0b6904
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817707"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="23ff3-103">Comando update (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="23ff3-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="23ff3-104">**Si applica a:** pacchetto consumo &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="23ff3-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="23ff3-105">Aggiorna tutti i pacchetti in un progetto (usando `packages.config`) alle versioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="23ff3-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="23ff3-106">È consigliabile eseguire ['restore'](cli-ref-restore.md) prima di eseguire il `update`.</span><span class="sxs-lookup"><span data-stu-id="23ff3-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="23ff3-107">(Per aggiornare un singolo pacchetto, utilizzare [ `nuget install` ](cli-ref-install.md) senza specificare un numero di versione, in cui NuGet case consente di installare la versione più recente.)</span><span class="sxs-lookup"><span data-stu-id="23ff3-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="23ff3-108">Nota: `update` non funziona con l'interfaccia CLI in esecuzione in Mono (Mac OSX o Linux) o quando si utilizza il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="23ff3-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="23ff3-109">Il `update` comando Aggiorna anche i riferimenti all'assembly nel file di progetto, fornito quelli fa riferimento a già esiste.</span><span class="sxs-lookup"><span data-stu-id="23ff3-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="23ff3-110">Se un pacchetto aggiornato è un assembly aggiunto, un nuovo riferimento è *non* aggiunto.</span><span class="sxs-lookup"><span data-stu-id="23ff3-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="23ff3-111">Inoltre, nuove dipendenze di pacchetto non sono i riferimenti ad assembly aggiunto.</span><span class="sxs-lookup"><span data-stu-id="23ff3-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="23ff3-112">Per includere queste operazioni come parte di un aggiornamento, aggiornare il pacchetto in Visual Studio utilizzando la UI Package Manager o la Console di gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="23ff3-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="23ff3-113">Questo comando può essere utilizzato anche per aggiornare nuget.exe stesso utilizzando il *-self* flag.</span><span class="sxs-lookup"><span data-stu-id="23ff3-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="23ff3-114">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="23ff3-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="23ff3-115">dove `<configPath>` identifica uno un `packages.config` o file di soluzione che elenca le dipendenze del progetto.</span><span class="sxs-lookup"><span data-stu-id="23ff3-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="23ff3-116">Opzioni</span><span class="sxs-lookup"><span data-stu-id="23ff3-116">Options</span></span>

| <span data-ttu-id="23ff3-117">Opzione</span><span class="sxs-lookup"><span data-stu-id="23ff3-117">Option</span></span> | <span data-ttu-id="23ff3-118">Descrizione</span><span class="sxs-lookup"><span data-stu-id="23ff3-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="23ff3-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="23ff3-119">ConfigFile</span></span> | <span data-ttu-id="23ff3-120">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="23ff3-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="23ff3-121">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="23ff3-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="23ff3-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="23ff3-122">FileConflictAction</span></span> | <span data-ttu-id="23ff3-123">Specifica l'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto.</span><span class="sxs-lookup"><span data-stu-id="23ff3-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="23ff3-124">I valori sono *sovrascrivere, ignorare, Nessuno*.</span><span class="sxs-lookup"><span data-stu-id="23ff3-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="23ff3-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="23ff3-125">ForceEnglishOutput</span></span> | <span data-ttu-id="23ff3-126">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="23ff3-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="23ff3-127">?</span><span class="sxs-lookup"><span data-stu-id="23ff3-127">Help</span></span> | <span data-ttu-id="23ff3-128">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="23ff3-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="23ff3-129">Id</span><span class="sxs-lookup"><span data-stu-id="23ff3-129">Id</span></span> | <span data-ttu-id="23ff3-130">Specifica un elenco di ID per l'aggiornamento pacchetto.</span><span class="sxs-lookup"><span data-stu-id="23ff3-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="23ff3-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="23ff3-131">MSBuildPath</span></span> | <span data-ttu-id="23ff3-132">*(4.0 +)*  Specifica il percorso di MSBuild da usare con il comando, che avrà la precedenza `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="23ff3-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="23ff3-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="23ff3-133">MSBuildVersion</span></span> | <span data-ttu-id="23ff3-134">*(3.2 +)*  Specifica la versione di MSBuild da usare con questo comando.</span><span class="sxs-lookup"><span data-stu-id="23ff3-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="23ff3-135">Valori supportati sono 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="23ff3-135">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="23ff3-136">Per impostazione predefinita che viene selezionato il percorso di MSBuild, in caso contrario il valore predefinito la versione più aggiornata di MSBuild.</span><span class="sxs-lookup"><span data-stu-id="23ff3-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="23ff3-137">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="23ff3-137">NonInteractive</span></span> | <span data-ttu-id="23ff3-138">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="23ff3-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="23ff3-139">Versione provvisoria</span><span class="sxs-lookup"><span data-stu-id="23ff3-139">PreRelease</span></span> | <span data-ttu-id="23ff3-140">Consente l'aggiornamento di versioni non definitive.</span><span class="sxs-lookup"><span data-stu-id="23ff3-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="23ff3-141">Questo flag non è richiesto durante l'aggiornamento preliminari pacchetti che sono già installati.</span><span class="sxs-lookup"><span data-stu-id="23ff3-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="23ff3-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="23ff3-142">RepositoryPath</span></span> | <span data-ttu-id="23ff3-143">Specifica la cartella locale in cui sono installati i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="23ff3-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="23ff3-144">Safe</span><span class="sxs-lookup"><span data-stu-id="23ff3-144">Safe</span></span> | <span data-ttu-id="23ff3-145">Specifica che solo gli aggiornamenti con la versione più recente disponibile all'interno della stessa versione principale e secondaria verrà installato il pacchetto installato.</span><span class="sxs-lookup"><span data-stu-id="23ff3-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="23ff3-146">Self</span><span class="sxs-lookup"><span data-stu-id="23ff3-146">Self</span></span> | <span data-ttu-id="23ff3-147">Nuget.exe gli aggiornamenti per la versione più recente; tutti gli altri argomenti vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="23ff3-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="23ff3-148">Origine</span><span class="sxs-lookup"><span data-stu-id="23ff3-148">Source</span></span> | <span data-ttu-id="23ff3-149">Specifica l'elenco delle origini pacchetto (come URL) da usare per gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="23ff3-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="23ff3-150">Se omesso, il comando Usa le origini disponibili in file di configurazione, vedere [il comportamento di configurazione NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="23ff3-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="23ff3-151">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="23ff3-151">Verbosity</span></span> | <span data-ttu-id="23ff3-152">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="23ff3-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="23ff3-153">Versione</span><span class="sxs-lookup"><span data-stu-id="23ff3-153">Version</span></span> | <span data-ttu-id="23ff3-154">Se usato con un ID di pacchetto, specifica la versione del pacchetto da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="23ff3-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="23ff3-155">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="23ff3-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="23ff3-156">Esempi</span><span class="sxs-lookup"><span data-stu-id="23ff3-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
