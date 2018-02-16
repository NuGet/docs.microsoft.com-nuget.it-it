---
title: Guida di riferimento di sincronizzazione-pacchetto NuGet PowerShell | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando di PowerShell di sincronizzazione pacchetto nella Console di gestione pacchetti NuGet in Visual Studio.
keywords: Console di gestione, i comandi di Powershell di NuGet, riferimenti di NuGet Powershell, sincronizzazione pacchetto del pacchetto NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8e4b627cff01a353440c47883b98cd93f9edd6cb
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="280e7-104">Sincronizzazione-pacchetto (Package Manager Console in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="280e7-104">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="280e7-105">*Versione 3.0; disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="280e7-105">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="280e7-106">Ottiene la versione del pacchetto installato dal specificato (o predefinito) del progetto e sincronizza la versione ai restanti progetti nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="280e7-106">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="280e7-107">Sintassi</span><span class="sxs-lookup"><span data-stu-id="280e7-107">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="280e7-108">Parametri</span><span class="sxs-lookup"><span data-stu-id="280e7-108">Parameters</span></span>

| <span data-ttu-id="280e7-109">Parametro</span><span class="sxs-lookup"><span data-stu-id="280e7-109">Parameter</span></span> | <span data-ttu-id="280e7-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="280e7-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="280e7-111">Id</span><span class="sxs-lookup"><span data-stu-id="280e7-111">Id</span></span> | <span data-ttu-id="280e7-112">(Obbligatorio) L'identificatore del pacchetto per la sincronizzazione. -Id switch stesso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="280e7-112">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="280e7-113">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="280e7-113">IgnoreDependencies</span></span> | <span data-ttu-id="280e7-114">Installa solo questo pacchetto e non le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="280e7-114">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="280e7-115">ProjectName</span><span class="sxs-lookup"><span data-stu-id="280e7-115">ProjectName</span></span> | <span data-ttu-id="280e7-116">Progetto per sincronizzare il pacchetto, verrà utilizzato per il progetto predefinito.</span><span class="sxs-lookup"><span data-stu-id="280e7-116">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="280e7-117">Versione</span><span class="sxs-lookup"><span data-stu-id="280e7-117">Version</span></span> | <span data-ttu-id="280e7-118">La versione del pacchetto per la sincronizzazione, verrà utilizzato per la versione attualmente installata.</span><span class="sxs-lookup"><span data-stu-id="280e7-118">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="280e7-119">Origine</span><span class="sxs-lookup"><span data-stu-id="280e7-119">Source</span></span> | <span data-ttu-id="280e7-120">Il percorso URL o una cartella per l'origine del pacchetto da cercare.</span><span class="sxs-lookup"><span data-stu-id="280e7-120">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="280e7-121">I percorsi di cartella locale possono essere assoluto o relativo della cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="280e7-121">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="280e7-122">Se omesso, `Sync-Package` Cerca l'origine pacchetto attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="280e7-122">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="280e7-123">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="280e7-123">IncludePrerelease</span></span> | <span data-ttu-id="280e7-124">Include pacchetti della versione provvisoria della sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="280e7-124">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="280e7-125">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="280e7-125">FileConflictAction</span></span> | <span data-ttu-id="280e7-126">L'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto.</span><span class="sxs-lookup"><span data-stu-id="280e7-126">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="280e7-127">I valori possibili sono *sovrascrittura, Ignora, None, OverwriteAll*, e *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="280e7-127">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="280e7-128">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="280e7-128">DependencyVersion</span></span> | <span data-ttu-id="280e7-129">La versione dei pacchetti di dipendenza da usare, che può essere uno dei seguenti:</span><span class="sxs-lookup"><span data-stu-id="280e7-129">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="280e7-130">*Più basso* (impostazione predefinita): la versione minima</span><span class="sxs-lookup"><span data-stu-id="280e7-130">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="280e7-131">*HighestPatch*: la versione con la patch più basso principale, secondaria più basso, più elevata</span><span class="sxs-lookup"><span data-stu-id="280e7-131">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="280e7-132">*HighestMinor*: la versione con il minimo principali, patch più alto, minore più alto</span><span class="sxs-lookup"><span data-stu-id="280e7-132">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="280e7-133">*Più alto* (impostazione predefinita per il pacchetto di aggiornamento senza parametri): la versione più recente</span><span class="sxs-lookup"><span data-stu-id="280e7-133">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="280e7-134">È possibile impostare il valore predefinito utilizzando il [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) impostazione di `Nuget.Config` file.</span><span class="sxs-lookup"><span data-stu-id="280e7-134">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="280e7-135">WhatIf</span><span class="sxs-lookup"><span data-stu-id="280e7-135">WhatIf</span></span> | <span data-ttu-id="280e7-136">Viene illustrato che cosa accadrebbe eseguendo il comando senza eseguire effettivamente la sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="280e7-136">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="280e7-137">Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.</span><span class="sxs-lookup"><span data-stu-id="280e7-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="280e7-138">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="280e7-138">Common Parameters</span></span>

<span data-ttu-id="280e7-139">`Sync-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="280e7-139">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="280e7-140">Esempi</span><span class="sxs-lookup"><span data-stu-id="280e7-140">Examples</span></span>

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
