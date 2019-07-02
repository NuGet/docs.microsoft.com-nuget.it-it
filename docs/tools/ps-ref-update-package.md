---
title: Riferimento di PowerShell Update-pacchetto NuGet
description: Informazioni di riferimento per il comando di PowerShell Update-Package nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5b5a11ee11d9e2cf6a90d56ac63b1f7bad750ea
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496482"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="e67e6-103">Update-Package (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e67e6-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e67e6-104">*Disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="e67e6-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e67e6-105">Aggiorna un pacchetto e le relative dipendenze o tutti i pacchetti in un progetto, a una versione più recente.</span><span class="sxs-lookup"><span data-stu-id="e67e6-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="e67e6-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="e67e6-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="e67e6-107">In NuGet 2.8 + `Update-Package` può essere utilizzato per effettuare il downgrade di un pacchetto esistente nel progetto.</span><span class="sxs-lookup"><span data-stu-id="e67e6-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="e67e6-108">Ad esempio, se hai 5.1.0-rc1 ASPNET installato, il comando seguente potrebbe effettuare il downgrade alla 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="e67e6-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="e67e6-109">Parametri</span><span class="sxs-lookup"><span data-stu-id="e67e6-109">Parameters</span></span>

|  <span data-ttu-id="e67e6-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="e67e6-110">Parameter</span></span> | <span data-ttu-id="e67e6-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e67e6-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e67e6-112">Id</span><span class="sxs-lookup"><span data-stu-id="e67e6-112">Id</span></span> | <span data-ttu-id="e67e6-113">L'identificatore del pacchetto da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="e67e6-113">The identifier of the package to update.</span></span> <span data-ttu-id="e67e6-114">Se omesso, Aggiorna tutti i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="e67e6-114">If omitted, updates all packages.</span></span> <span data-ttu-id="e67e6-115">-Id commutatore stesso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="e67e6-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="e67e6-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="e67e6-116">IgnoreDependencies</span></span> | <span data-ttu-id="e67e6-117">Ignora l'aggiornamento delle dipendenze del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e67e6-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="e67e6-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="e67e6-118">ProjectName</span></span> | <span data-ttu-id="e67e6-119">Il nome del progetto che contiene i pacchetti da aggiornare, utilizzando per impostazione predefinita a tutti i progetti.</span><span class="sxs-lookup"><span data-stu-id="e67e6-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="e67e6-120">Versione</span><span class="sxs-lookup"><span data-stu-id="e67e6-120">Version</span></span> | <span data-ttu-id="e67e6-121">La versione da usare per l'aggiornamento, verrà utilizzato per la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="e67e6-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="e67e6-122">In NuGet 3.0 +, il valore della versione deve essere uno dei *minima, massima, HighestMinor*, o *HighestPatch* (equivalente a - Safe).</span><span class="sxs-lookup"><span data-stu-id="e67e6-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="e67e6-123">Safe</span><span class="sxs-lookup"><span data-stu-id="e67e6-123">Safe</span></span> | <span data-ttu-id="e67e6-124">Vincola gli aggiornamenti alle versioni sole con la stessa versione principale e secondaria del pacchetto attualmente installata.</span><span class="sxs-lookup"><span data-stu-id="e67e6-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="e67e6-125">Origine</span><span class="sxs-lookup"><span data-stu-id="e67e6-125">Source</span></span> | <span data-ttu-id="e67e6-126">Il percorso URL o una cartella per l'origine del pacchetto da cercare.</span><span class="sxs-lookup"><span data-stu-id="e67e6-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="e67e6-127">I percorsi di cartella locale possono essere assoluto o relativo rispetto alla cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="e67e6-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="e67e6-128">Se omesso, `Update-Package` Cerca l'origine del pacchetto attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="e67e6-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="e67e6-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="e67e6-129">IncludePrerelease</span></span> | <span data-ttu-id="e67e6-130">Include i pacchetti non definitive degli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="e67e6-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="e67e6-131">Reinstallazione</span><span class="sxs-lookup"><span data-stu-id="e67e6-131">Reinstall</span></span> | <span data-ttu-id="e67e6-132">Pacchetti Resintalls utilizzando le versioni attualmente installate.</span><span class="sxs-lookup"><span data-stu-id="e67e6-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="e67e6-133">Vedere [Reinstallazione e aggiornamento di pacchetti](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="e67e6-133">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="e67e6-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="e67e6-134">FileConflictAction</span></span> | <span data-ttu-id="e67e6-135">L'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti farvi riferimento il progetto.</span><span class="sxs-lookup"><span data-stu-id="e67e6-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="e67e6-136">I valori possibili sono *Sovrascrivi, Ignore, None, OverwriteAll*, e *IgnoreAll* (3.0 e versioni successive).</span><span class="sxs-lookup"><span data-stu-id="e67e6-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="e67e6-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="e67e6-137">DependencyVersion</span></span> | <span data-ttu-id="e67e6-138">La versione dei pacchetti di dipendenza da usare, che può essere uno dei seguenti:</span><span class="sxs-lookup"><span data-stu-id="e67e6-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="e67e6-139">*Più basso* (impostazione predefinita): la versione più bassa</span><span class="sxs-lookup"><span data-stu-id="e67e6-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="e67e6-140">*HighestPatch*: la versione con patch più bassa principali, più bassa secondaria, più alto</span><span class="sxs-lookup"><span data-stu-id="e67e6-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="e67e6-141">*HighestMinor*: la versione con il minimo principali, patch secondaria, massima più alto</span><span class="sxs-lookup"><span data-stu-id="e67e6-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="e67e6-142">*Più alto* (valore predefinito per Update-Package senza parametri): la versione più recente</span><span class="sxs-lookup"><span data-stu-id="e67e6-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="e67e6-143">È possibile impostare il valore predefinito usando il [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) impostazione nel `Nuget.Config` file.</span><span class="sxs-lookup"><span data-stu-id="e67e6-143">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="e67e6-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="e67e6-144">ToHighestPatch</span></span> | <span data-ttu-id="e67e6-145">equivalente allo - Safe.</span><span class="sxs-lookup"><span data-stu-id="e67e6-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="e67e6-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="e67e6-146">ToHighestMinor</span></span> | <span data-ttu-id="e67e6-147">Vincola gli aggiornamenti solo alle versioni con la stessa versione principale del pacchetto attualmente installata.</span><span class="sxs-lookup"><span data-stu-id="e67e6-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="e67e6-148">Whatif</span><span class="sxs-lookup"><span data-stu-id="e67e6-148">WhatIf</span></span> | <span data-ttu-id="e67e6-149">Viene illustrato che cosa accadrebbe quando si esegue il comando senza eseguire effettivamente l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="e67e6-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="e67e6-150">Nessuno di questi parametri accettano caratteri jolly o input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="e67e6-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="e67e6-151">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="e67e6-151">Common Parameters</span></span>

<span data-ttu-id="e67e6-152">`Update-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e67e6-152">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="e67e6-153">Esempi</span><span class="sxs-lookup"><span data-stu-id="e67e6-153">Examples</span></span>

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
