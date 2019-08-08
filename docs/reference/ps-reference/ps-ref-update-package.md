---
title: Informazioni di riferimento su PowerShell Update-Package
description: Riferimento per il comando Update-Package di PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 57e50ed805496b3511bc3b808f89da6f7ad413fc
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327268"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="749d4-103">Update-Package (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="749d4-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="749d4-104">*Disponibile solo nella [console di gestione pacchetti NuGet](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="749d4-104">*Available only within the [NuGet Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="749d4-105">Aggiorna un pacchetto e le relative dipendenze o tutti i pacchetti di un progetto a una versione più recente.</span><span class="sxs-lookup"><span data-stu-id="749d4-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="749d4-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="749d4-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="749d4-107">In NuGet 2.8 +, `Update-Package` può essere usato per eseguire il downgrade di un pacchetto esistente nel progetto.</span><span class="sxs-lookup"><span data-stu-id="749d4-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="749d4-108">Se, ad esempio, è installato Microsoft. AspNet. MVC 5.1.0-RC1, il comando seguente esegue il downgrade a 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="749d4-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="749d4-109">Parametri</span><span class="sxs-lookup"><span data-stu-id="749d4-109">Parameters</span></span>

|  <span data-ttu-id="749d4-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="749d4-110">Parameter</span></span> | <span data-ttu-id="749d4-111">DESCRIZIONE</span><span class="sxs-lookup"><span data-stu-id="749d4-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="749d4-112">ID</span><span class="sxs-lookup"><span data-stu-id="749d4-112">Id</span></span> | <span data-ttu-id="749d4-113">Identificatore del pacchetto da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="749d4-113">The identifier of the package to update.</span></span> <span data-ttu-id="749d4-114">Se omesso, aggiorna tutti i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="749d4-114">If omitted, updates all packages.</span></span> <span data-ttu-id="749d4-115">L'opzione-ID è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="749d4-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="749d4-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="749d4-116">IgnoreDependencies</span></span> | <span data-ttu-id="749d4-117">Ignora l'aggiornamento delle dipendenze del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="749d4-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="749d4-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="749d4-118">ProjectName</span></span> | <span data-ttu-id="749d4-119">Nome del progetto contenente i pacchetti da aggiornare, per impostazione predefinita tutti i progetti.</span><span class="sxs-lookup"><span data-stu-id="749d4-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="749d4-120">Version</span><span class="sxs-lookup"><span data-stu-id="749d4-120">Version</span></span> | <span data-ttu-id="749d4-121">Versione da usare per l'aggiornamento, per impostazione predefinita la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="749d4-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="749d4-122">In NuGet 3.0 +, il valore della versione deve essere uno dei valori *minimo, massimo, HighestMinor*o *HighestPatch* (equivalente a-safe).</span><span class="sxs-lookup"><span data-stu-id="749d4-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="749d4-123">Safe</span><span class="sxs-lookup"><span data-stu-id="749d4-123">Safe</span></span> | <span data-ttu-id="749d4-124">Vincola gli aggiornamenti solo alle versioni con la stessa versione principale e secondaria del pacchetto attualmente installato.</span><span class="sxs-lookup"><span data-stu-id="749d4-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="749d4-125">Source</span><span class="sxs-lookup"><span data-stu-id="749d4-125">Source</span></span> | <span data-ttu-id="749d4-126">URL o percorso della cartella per l'origine del pacchetto da cercare.</span><span class="sxs-lookup"><span data-stu-id="749d4-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="749d4-127">I percorsi delle cartelle locali possono essere assoluti o relativi alla cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="749d4-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="749d4-128">Se omesso, `Update-Package` Cerca nell'origine del pacchetto attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="749d4-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="749d4-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="749d4-129">IncludePrerelease</span></span> | <span data-ttu-id="749d4-130">Include pacchetti di versioni non definitive per gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="749d4-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="749d4-131">Reinstallazione</span><span class="sxs-lookup"><span data-stu-id="749d4-131">Reinstall</span></span> | <span data-ttu-id="749d4-132">Resintalls i pacchetti usando le versioni attualmente installate.</span><span class="sxs-lookup"><span data-stu-id="749d4-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="749d4-133">Vedere [Reinstallazione e aggiornamento di pacchetti](../../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="749d4-133">See [Reinstalling and updating packages](../../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="749d4-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="749d4-134">FileConflictAction</span></span> | <span data-ttu-id="749d4-135">Azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto.</span><span class="sxs-lookup"><span data-stu-id="749d4-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="749d4-136">I valori possibili sono *overwrite, ignore, None, OverwriteAll*e *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="749d4-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="749d4-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="749d4-137">DependencyVersion</span></span> | <span data-ttu-id="749d4-138">Versione dei pacchetti di dipendenze da usare. i possibili tipi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="749d4-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="749d4-139">*Più bassa* (impostazione predefinita): versione più bassa</span><span class="sxs-lookup"><span data-stu-id="749d4-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="749d4-140">*HighestPatch*: versione con la patch principale più bassa, minore minore, più alta</span><span class="sxs-lookup"><span data-stu-id="749d4-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="749d4-141">*HighestMinor*: versione con la patch principale più bassa, minore più elevata</span><span class="sxs-lookup"><span data-stu-id="749d4-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="749d4-142">*Più alta* (impostazione predefinita per Update-Package senza parametri): la versione più recente</span><span class="sxs-lookup"><span data-stu-id="749d4-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="749d4-143">È possibile impostare il valore predefinito usando l' [`dependencyVersion`](../nuget-config-file.md#config-section) impostazione `Nuget.Config` nel file.</span><span class="sxs-lookup"><span data-stu-id="749d4-143">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="749d4-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="749d4-144">ToHighestPatch</span></span> | <span data-ttu-id="749d4-145">equivalente a-safe.</span><span class="sxs-lookup"><span data-stu-id="749d4-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="749d4-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="749d4-146">ToHighestMinor</span></span> | <span data-ttu-id="749d4-147">Vincola gli aggiornamenti solo alle versioni con la stessa versione principale del pacchetto attualmente installato.</span><span class="sxs-lookup"><span data-stu-id="749d4-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="749d4-148">Whatif</span><span class="sxs-lookup"><span data-stu-id="749d4-148">WhatIf</span></span> | <span data-ttu-id="749d4-149">Mostra cosa accade quando si esegue il comando senza eseguire effettivamente l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="749d4-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="749d4-150">Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="749d4-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="749d4-151">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="749d4-151">Common Parameters</span></span>

<span data-ttu-id="749d4-152">`Update-Package`supporta i seguenti [parametri comuni di PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="749d4-152">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="749d4-153">Esempi</span><span class="sxs-lookup"><span data-stu-id="749d4-153">Examples</span></span>

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