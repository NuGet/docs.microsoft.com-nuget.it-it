---
title: Riferimento di PowerShell Sync-pacchetto NuGet
description: Informazioni di riferimento per il comando PowerShell Sync-pacchetto nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: de0b612e1335cafdcd6a0b802d54f2182d27ad22
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842255"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="5ed13-103">Sync-Package (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="5ed13-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="5ed13-104">*Versione 3.0 e versioni successive; disponibile solo all'interno di [Console di gestione pacchetti](package-manager-console.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="5ed13-104">*Version 3.0+; available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="5ed13-105">Ottiene la versione del pacchetto installato da specificato (o predefinito) del progetto e sincronizza la versione per il resto dei progetti nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="5ed13-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="5ed13-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="5ed13-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="5ed13-107">Parametri</span><span class="sxs-lookup"><span data-stu-id="5ed13-107">Parameters</span></span>

| <span data-ttu-id="5ed13-108">Parametro</span><span class="sxs-lookup"><span data-stu-id="5ed13-108">Parameter</span></span> | <span data-ttu-id="5ed13-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ed13-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5ed13-110">ID</span><span class="sxs-lookup"><span data-stu-id="5ed13-110">Id</span></span> | <span data-ttu-id="5ed13-111">(Obbligatorio) L'identificatore del pacchetto per la sincronizzazione. -Id commutatore stesso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="5ed13-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="5ed13-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="5ed13-112">IgnoreDependencies</span></span> | <span data-ttu-id="5ed13-113">Installare solo il pacchetto e non le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="5ed13-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="5ed13-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="5ed13-114">ProjectName</span></span> | <span data-ttu-id="5ed13-115">Il progetto per la sincronizzazione del pacchetto, verrà utilizzato per il progetto predefinito.</span><span class="sxs-lookup"><span data-stu-id="5ed13-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="5ed13-116">Version</span><span class="sxs-lookup"><span data-stu-id="5ed13-116">Version</span></span> | <span data-ttu-id="5ed13-117">La versione del pacchetto per la sincronizzazione, verrà utilizzato per la versione attualmente installata.</span><span class="sxs-lookup"><span data-stu-id="5ed13-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="5ed13-118">`Source`</span><span class="sxs-lookup"><span data-stu-id="5ed13-118">Source</span></span> | <span data-ttu-id="5ed13-119">Il percorso URL o una cartella per l'origine del pacchetto da cercare.</span><span class="sxs-lookup"><span data-stu-id="5ed13-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="5ed13-120">I percorsi di cartella locale possono essere assoluto o relativo rispetto alla cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="5ed13-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="5ed13-121">Se omesso, `Sync-Package` Cerca l'origine del pacchetto attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="5ed13-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="5ed13-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="5ed13-122">IncludePrerelease</span></span> | <span data-ttu-id="5ed13-123">Include pacchetti versione non definitivo in sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="5ed13-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="5ed13-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="5ed13-124">FileConflictAction</span></span> | <span data-ttu-id="5ed13-125">L'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti farvi riferimento il progetto.</span><span class="sxs-lookup"><span data-stu-id="5ed13-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="5ed13-126">I valori possibili sono *Sovrascrivi, Ignore, None, OverwriteAll*, e *(3.0 e versioni successive)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="5ed13-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="5ed13-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="5ed13-127">DependencyVersion</span></span> | <span data-ttu-id="5ed13-128">La versione dei pacchetti di dipendenza da usare, che può essere uno dei seguenti:</span><span class="sxs-lookup"><span data-stu-id="5ed13-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="5ed13-129">*Più basso* (impostazione predefinita): la versione più bassa</span><span class="sxs-lookup"><span data-stu-id="5ed13-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="5ed13-130">*HighestPatch*: la versione con patch più bassa principali, più bassa secondaria, più alto</span><span class="sxs-lookup"><span data-stu-id="5ed13-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="5ed13-131">*HighestMinor*: la versione con il minimo principali, patch secondaria, massima più alto</span><span class="sxs-lookup"><span data-stu-id="5ed13-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="5ed13-132">*Più alto* (valore predefinito per Update-Package senza parametri): la versione più recente</span><span class="sxs-lookup"><span data-stu-id="5ed13-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="5ed13-133">È possibile impostare il valore predefinito usando il [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) impostazione nel `Nuget.Config` file.</span><span class="sxs-lookup"><span data-stu-id="5ed13-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="5ed13-134">Whatif</span><span class="sxs-lookup"><span data-stu-id="5ed13-134">WhatIf</span></span> | <span data-ttu-id="5ed13-135">Viene illustrato che cosa accadrebbe quando si esegue il comando senza effettivamente eseguire la sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="5ed13-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="5ed13-136">Nessuno di questi parametri accettano caratteri jolly o input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="5ed13-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="5ed13-137">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="5ed13-137">Common Parameters</span></span>

<span data-ttu-id="5ed13-138">`Sync-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5ed13-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="5ed13-139">Esempi</span><span class="sxs-lookup"><span data-stu-id="5ed13-139">Examples</span></span>

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
