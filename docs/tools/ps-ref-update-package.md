---
title: Riferimento di PowerShell Update-pacchetto NuGet
description: Riferimento per il comando di PowerShell di pacchetto di aggiornamento nella Console di gestione pacchetti NuGet in Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 621e59633117a29c58fe643860ee7e2b40a4fbe2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="45c5a-103">Update-Package (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="45c5a-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="45c5a-104">*Disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="45c5a-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="45c5a-105">Aggiorna un pacchetto e le relative dipendenze o tutti i pacchetti in un progetto a una versione più recente.</span><span class="sxs-lookup"><span data-stu-id="45c5a-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="45c5a-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="45c5a-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="45c5a-107">In NuGet 2.8 + `Update-Package` può essere usato per effettuare il downgrade di un pacchetto esistente nel progetto.</span><span class="sxs-lookup"><span data-stu-id="45c5a-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="45c5a-108">Ad esempio, se si dispone di 5.1.0-rc1 italiano installato, il comando seguente sarebbe effettuare il downgrade a 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="45c5a-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="45c5a-109">Parametri</span><span class="sxs-lookup"><span data-stu-id="45c5a-109">Parameters</span></span>

|  <span data-ttu-id="45c5a-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="45c5a-110">Parameter</span></span> | <span data-ttu-id="45c5a-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="45c5a-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="45c5a-112">Id</span><span class="sxs-lookup"><span data-stu-id="45c5a-112">Id</span></span> | <span data-ttu-id="45c5a-113">L'identificatore del pacchetto da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="45c5a-113">The identifier of the package to update.</span></span> <span data-ttu-id="45c5a-114">Se omesso, Aggiorna tutti i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="45c5a-114">If omitted, updates all packages.</span></span> <span data-ttu-id="45c5a-115">-Id switch stesso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="45c5a-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="45c5a-116">MSI</span><span class="sxs-lookup"><span data-stu-id="45c5a-116">IgnoreDependencies</span></span> | <span data-ttu-id="45c5a-117">Ignora le dipendenze del pacchetto di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="45c5a-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="45c5a-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="45c5a-118">ProjectName</span></span> | <span data-ttu-id="45c5a-119">Il nome del progetto contenente i pacchetti da aggiornare, verrà utilizzato per tutti i progetti.</span><span class="sxs-lookup"><span data-stu-id="45c5a-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="45c5a-120">Versione</span><span class="sxs-lookup"><span data-stu-id="45c5a-120">Version</span></span> | <span data-ttu-id="45c5a-121">La versione da utilizzare per l'aggiornamento, verrà utilizzato per la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="45c5a-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="45c5a-122">In NuGet 3.0 e successive, il valore di versione deve essere uno dei *minima, massima, HighestMinor*, o *HighestPatch* (equivalente a - Safe).</span><span class="sxs-lookup"><span data-stu-id="45c5a-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="45c5a-123">Safe</span><span class="sxs-lookup"><span data-stu-id="45c5a-123">Safe</span></span> | <span data-ttu-id="45c5a-124">Vincola gli aggiornamenti alle versioni sole con la stessa versione principale e secondaria del pacchetto attualmente installata.</span><span class="sxs-lookup"><span data-stu-id="45c5a-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="45c5a-125">Origine</span><span class="sxs-lookup"><span data-stu-id="45c5a-125">Source</span></span> | <span data-ttu-id="45c5a-126">Il percorso URL o una cartella per l'origine del pacchetto da cercare.</span><span class="sxs-lookup"><span data-stu-id="45c5a-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="45c5a-127">I percorsi di cartella locale possono essere assoluto o relativo della cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="45c5a-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="45c5a-128">Se omesso, `Update-Package` Cerca l'origine pacchetto attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="45c5a-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="45c5a-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="45c5a-129">IncludePrerelease</span></span> | <span data-ttu-id="45c5a-130">Include pacchetti della versione provvisoria per gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="45c5a-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="45c5a-131">Reinstallazione</span><span class="sxs-lookup"><span data-stu-id="45c5a-131">Reinstall</span></span> | <span data-ttu-id="45c5a-132">Pacchetti di Resintalls utilizzando la versione attualmente installata.</span><span class="sxs-lookup"><span data-stu-id="45c5a-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="45c5a-133">Vedere [Reinstallazione e aggiornamento di pacchetti](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="45c5a-133">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="45c5a-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="45c5a-134">FileConflictAction</span></span> | <span data-ttu-id="45c5a-135">L'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto.</span><span class="sxs-lookup"><span data-stu-id="45c5a-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="45c5a-136">I valori possibili sono *sovrascrittura, Ignora, None, OverwriteAll*, e *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="45c5a-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="45c5a-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="45c5a-137">DependencyVersion</span></span> | <span data-ttu-id="45c5a-138">La versione dei pacchetti di dipendenza da usare, che può essere uno dei seguenti:</span><span class="sxs-lookup"><span data-stu-id="45c5a-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="45c5a-139">*Più basso* (impostazione predefinita): la versione minima</span><span class="sxs-lookup"><span data-stu-id="45c5a-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="45c5a-140">*HighestPatch*: la versione con la patch più basso principale, secondaria più basso, più elevata</span><span class="sxs-lookup"><span data-stu-id="45c5a-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="45c5a-141">*HighestMinor*: la versione con il minimo principali, patch più alto, minore più alto</span><span class="sxs-lookup"><span data-stu-id="45c5a-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="45c5a-142">*Più alto* (impostazione predefinita per il pacchetto di aggiornamento senza parametri): la versione più recente</span><span class="sxs-lookup"><span data-stu-id="45c5a-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="45c5a-143">È possibile impostare il valore predefinito utilizzando il [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) impostazione di `Nuget.Config` file.</span><span class="sxs-lookup"><span data-stu-id="45c5a-143">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="45c5a-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="45c5a-144">ToHighestPatch</span></span> | <span data-ttu-id="45c5a-145">Vincola gli aggiornamenti solo alle versioni con la stessa versione secondaria del pacchetto attualmente installata.</span><span class="sxs-lookup"><span data-stu-id="45c5a-145">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="45c5a-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="45c5a-146">ToHighestMinor</span></span> | <span data-ttu-id="45c5a-147">Vincola gli aggiornamenti solo alle versioni con la stessa versione principale del pacchetto attualmente installata.</span><span class="sxs-lookup"><span data-stu-id="45c5a-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="45c5a-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="45c5a-148">WhatIf</span></span> | <span data-ttu-id="45c5a-149">Viene illustrato che cosa accadrebbe eseguendo il comando senza eseguire effettivamente l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="45c5a-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="45c5a-150">Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.</span><span class="sxs-lookup"><span data-stu-id="45c5a-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="45c5a-151">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="45c5a-151">Common Parameters</span></span>

<span data-ttu-id="45c5a-152">`Update-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="45c5a-152">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="45c5a-153">Esempi</span><span class="sxs-lookup"><span data-stu-id="45c5a-153">Examples</span></span>

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
