---
title: Comando di installazione NuGet CLI | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 59ac622f-837c-4545-bc93-a56330e02d71
description: Riferimento per il comando di installazione di nuget.exe
keywords: NuGet riferimento, il comando pacchetto installato
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88c123a7f2a3d628713cefcc4b110fb0205093b4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="645e3-104">installare comando (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="645e3-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="645e3-105">**Si applica a:** pacchetto consumo &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="645e3-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="645e3-106">Scarica e installa un pacchetto in un progetto, verrà utilizzato per la cartella corrente, usando l'origine del pacchetto specificato.</span><span class="sxs-lookup"><span data-stu-id="645e3-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="645e3-107">Per scaricare un pacchetto direttamente all'esterno del contesto di un progetto, visitare la pagina del pacchetto su [nuget.org](https://www.nuget.org) e selezionare il **scaricare** collegamento.</span><span class="sxs-lookup"><span data-stu-id="645e3-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span> 

<span data-ttu-id="645e3-108">Se non vengono specificata alcuna origine, quelli elencati nel file di configurazione globale, `%APPDATA%\NuGet\NuGet.Config`, vengono utilizzati.</span><span class="sxs-lookup"><span data-stu-id="645e3-108">If no sources are specified, those listed in the global configuration file, `%APPDATA%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="645e3-109">Vedere [configurazione NuGet comportamento](../consume-packages/configuring-nuget-behavior.md) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="645e3-109">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="645e3-110">Se non viene specificato alcun pacchetto specifico, `install` installa tutti i pacchetti elencati del progetto `packages.config` file, rendendola simile a [ `restore` ](#restore).</span><span class="sxs-lookup"><span data-stu-id="645e3-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](#restore).</span></span> <span data-ttu-id="645e3-111">(Il `install` comando non funziona con `project.json`.)</span><span class="sxs-lookup"><span data-stu-id="645e3-111">(The `install` command does not work with `project.json`.)</span></span>

<span data-ttu-id="645e3-112">Il `install` comando non modifichi un file di progetto o `packages.config`; in questo modo è simile a `restore` perché solo aggiunge i pacchetti su disco ma non modificare le dipendenze di un progetto.</span><span class="sxs-lookup"><span data-stu-id="645e3-112">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="645e3-113">Per aggiungere una dipendenza, aggiungere un progetto tramite l'interfaccia utente di gestione di pacchetto o la Console in Visual Studio oppure modificare `packages.config` e quindi eseguire uno `install` o `restore`.</span><span class="sxs-lookup"><span data-stu-id="645e3-113">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span> <span data-ttu-id="645e3-114">Per i progetti utilizzando `project.json`, è possibile modificare tale file e quindi eseguire `restore`.</span><span class="sxs-lookup"><span data-stu-id="645e3-114">For projects using `project.json`, you can modify that file and then run `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="645e3-115">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="645e3-115">Usage</span></span>

```
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="645e3-116">dove `<packageID>` denomina il pacchetto di installazione (utilizzando la versione più recente), o `<configFilePath>` identifica il `packages.config` file che elenca i pacchetti da installare.</span><span class="sxs-lookup"><span data-stu-id="645e3-116">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="645e3-117">È possibile indicare una versione specifica con la `-Version` opzione.</span><span class="sxs-lookup"><span data-stu-id="645e3-117">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="645e3-118">Opzioni</span><span class="sxs-lookup"><span data-stu-id="645e3-118">Options</span></span>

| <span data-ttu-id="645e3-119">Opzione</span><span class="sxs-lookup"><span data-stu-id="645e3-119">Option</span></span> | <span data-ttu-id="645e3-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="645e3-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="645e3-121">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="645e3-121">ConfigFile</span></span> | <span data-ttu-id="645e3-122">*(2.5 +)*  Questo file di configurazione da applicare.</span><span class="sxs-lookup"><span data-stu-id="645e3-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="645e3-123">Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="645e3-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="645e3-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="645e3-124">DisableParallelProcessing</span></span> | <span data-ttu-id="645e3-125">Disabilita l'installazione di più pacchetti in parallelo.</span><span class="sxs-lookup"><span data-stu-id="645e3-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="645e3-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="645e3-126">ExcludeVersion</span></span> | <span data-ttu-id="645e3-127">Installa il pacchetto in una cartella denominata con solo il nome del pacchetto e non il numero di versione.</span><span class="sxs-lookup"><span data-stu-id="645e3-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="645e3-128">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="645e3-128">FallbackSource</span></span> | <span data-ttu-id="645e3-129">*(3.2 +)*  Un elenco delle origini pacchetto da utilizzare come fallback nel caso in cui il pacchetto non viene trovato nel database primario o di origine predefinita.</span><span class="sxs-lookup"><span data-stu-id="645e3-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="645e3-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="645e3-130">ForceEnglishOutput</span></span> | <span data-ttu-id="645e3-131">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="645e3-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="645e3-132">Framework</span><span class="sxs-lookup"><span data-stu-id="645e3-132">Framework</span></span> | <span data-ttu-id="645e3-133">*(4.4 +)*  Framework di destinazione utilizzato per la selezione delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="645e3-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="645e3-134">Il valore predefinito 'Any' Se non specificato.</span><span class="sxs-lookup"><span data-stu-id="645e3-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="645e3-135">?</span><span class="sxs-lookup"><span data-stu-id="645e3-135">Help</span></span> | <span data-ttu-id="645e3-136">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="645e3-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="645e3-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="645e3-137">NoCache</span></span> | <span data-ttu-id="645e3-138">Impedisce l'utilizzo di pacchetti dalla cache locale NuGet.</span><span class="sxs-lookup"><span data-stu-id="645e3-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="645e3-139">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="645e3-139">NonInteractive</span></span> | <span data-ttu-id="645e3-140">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="645e3-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="645e3-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="645e3-141">OutputDirectory</span></span> | <span data-ttu-id="645e3-142">Specifica la cartella in cui sono installati i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="645e3-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="645e3-143">Se viene specificata alcuna cartella, viene utilizzata la cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="645e3-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="645e3-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="645e3-144">PackageSaveMode</span></span> | <span data-ttu-id="645e3-145">Specifica i tipi di file da salvare dopo l'installazione del pacchetto: uno dei `nuspec`, `nupkg`, o `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="645e3-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="645e3-146">Versione provvisoria</span><span class="sxs-lookup"><span data-stu-id="645e3-146">PreRelease</span></span> | <span data-ttu-id="645e3-147">Consente di pacchetti della versione provvisoria da installare.</span><span class="sxs-lookup"><span data-stu-id="645e3-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="645e3-148">Questo flag non è necessario durante il ripristino di pacchetti con `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="645e3-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="645e3-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="645e3-149">RequireConsent</span></span> | <span data-ttu-id="645e3-150">Verifica che il ripristino dei pacchetti è abilitato prima di scaricare e installare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="645e3-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="645e3-151">Per informazioni dettagliate, vedere [il ripristino del pacchetto](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="645e3-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="645e3-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="645e3-152">SolutionDirectory</span></span> | <span data-ttu-id="645e3-153">Specifica la cartella radice della soluzione per cui si desidera ripristinare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="645e3-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="645e3-154">Origine</span><span class="sxs-lookup"><span data-stu-id="645e3-154">Source</span></span> | <span data-ttu-id="645e3-155">Specifica l'elenco delle origini pacchetto (come URL) per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="645e3-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="645e3-156">Se omesso, il comando Usa le origini disponibili in file di configurazione, vedere [il comportamento di configurazione NuGet](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="645e3-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="645e3-157">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="645e3-157">Verbosity</span></span> | <span data-ttu-id="645e3-158">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="645e3-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="645e3-159">Versione</span><span class="sxs-lookup"><span data-stu-id="645e3-159">Version</span></span> | <span data-ttu-id="645e3-160">Specifica la versione del pacchetto da installare.</span><span class="sxs-lookup"><span data-stu-id="645e3-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="645e3-161">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="645e3-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="645e3-162">Esempi</span><span class="sxs-lookup"><span data-stu-id="645e3-162">Examples</span></span>

```
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
