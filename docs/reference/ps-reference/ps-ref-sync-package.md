---
title: Guida di riferimento a NuGet Sync-Package PowerShell
description: Informazioni di riferimento per il comando Sync-Package PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fc4c875b5dcb0b90e4d048daf5984ed265370090
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238049"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="492ca-103">Sync-Package (console di gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="492ca-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="492ca-104">*Versione 3.0 +; disponibile solo nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="492ca-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="492ca-105">Ottiene la versione del pacchetto installato dal progetto specificato (o predefinito) e sincronizza la versione con i restanti progetti nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="492ca-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="492ca-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="492ca-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="492ca-107">Parametri</span><span class="sxs-lookup"><span data-stu-id="492ca-107">Parameters</span></span>

| <span data-ttu-id="492ca-108">Parametro</span><span class="sxs-lookup"><span data-stu-id="492ca-108">Parameter</span></span> | <span data-ttu-id="492ca-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="492ca-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="492ca-110">ID</span><span class="sxs-lookup"><span data-stu-id="492ca-110">Id</span></span> | <span data-ttu-id="492ca-111">Necessaria Identificatore del pacchetto da sincronizzare. L'opzione-ID è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="492ca-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="492ca-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="492ca-112">IgnoreDependencies</span></span> | <span data-ttu-id="492ca-113">Installare solo questo pacchetto e non le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="492ca-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="492ca-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="492ca-114">ProjectName</span></span> | <span data-ttu-id="492ca-115">Progetto da cui sincronizzare il pacchetto, per impostazione predefinita il progetto predefinito.</span><span class="sxs-lookup"><span data-stu-id="492ca-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="492ca-116">Versione</span><span class="sxs-lookup"><span data-stu-id="492ca-116">Version</span></span> | <span data-ttu-id="492ca-117">Versione del pacchetto da sincronizzare, per impostazione predefinita la versione attualmente installata.</span><span class="sxs-lookup"><span data-stu-id="492ca-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="492ca-118">Source (Sorgente)</span><span class="sxs-lookup"><span data-stu-id="492ca-118">Source</span></span> | <span data-ttu-id="492ca-119">URL o percorso della cartella per l'origine del pacchetto da cercare.</span><span class="sxs-lookup"><span data-stu-id="492ca-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="492ca-120">I percorsi delle cartelle locali possono essere assoluti o relativi alla cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="492ca-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="492ca-121">Se omesso, `Sync-Package` Cerca nell'origine del pacchetto attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="492ca-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="492ca-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="492ca-122">IncludePrerelease</span></span> | <span data-ttu-id="492ca-123">Include i pacchetti di versioni non definitive nella sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="492ca-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="492ca-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="492ca-124">FileConflictAction</span></span> | <span data-ttu-id="492ca-125">Azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto.</span><span class="sxs-lookup"><span data-stu-id="492ca-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="492ca-126">I valori possibili sono *overwrite, ignore, None, OverwriteAll* e *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="492ca-126">Possible values are *Overwrite, Ignore, None, OverwriteAll* , and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="492ca-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="492ca-127">DependencyVersion</span></span> | <span data-ttu-id="492ca-128">Versione dei pacchetti di dipendenze da usare. i possibili tipi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="492ca-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="492ca-129">*Minimo* (impostazione predefinita): versione più bassa</span><span class="sxs-lookup"><span data-stu-id="492ca-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="492ca-130">*HighestPatch* : versione con la patch principale più bassa, minore minore, più alta</span><span class="sxs-lookup"><span data-stu-id="492ca-130">*HighestPatch* : the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="492ca-131">*HighestMinor* : versione con la patch principale più bassa, minore più elevata</span><span class="sxs-lookup"><span data-stu-id="492ca-131">*HighestMinor* : the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="492ca-132">*Massimo* (impostazione predefinita per Update-Package senza parametri): la versione più recente</span><span class="sxs-lookup"><span data-stu-id="492ca-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="492ca-133">È possibile impostare il valore predefinito usando l' [`dependencyVersion`](../nuget-config-file.md#config-section) impostazione nel `Nuget.Config` file.</span><span class="sxs-lookup"><span data-stu-id="492ca-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="492ca-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="492ca-134">WhatIf</span></span> | <span data-ttu-id="492ca-135">Mostra cosa accade quando si esegue il comando senza eseguire effettivamente la sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="492ca-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="492ca-136">Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="492ca-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="492ca-137">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="492ca-137">Common Parameters</span></span>

<span data-ttu-id="492ca-138">`Sync-Package` supporta i seguenti [parametri comuni di PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="492ca-138">`Sync-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="492ca-139">Esempi</span><span class="sxs-lookup"><span data-stu-id="492ca-139">Examples</span></span>

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```