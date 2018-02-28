---
title: Riferimento di PowerShell Install-Package NuGet | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 879db0ef-6b72-4a4a-bb68-f9e3a00f64b8
description: Riferimento per il comando di PowerShell Install-Package nella Console di gestione pacchetti NuGet in Visual Studio.
keywords: Console di gestione, i comandi di Powershell di NuGet, riferimento di Powershell di NuGet, pacchetto di installazione del pacchetto NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f5f6b3dffb27af510b750650561cdff597c927e0
ms.sourcegitcommit: a40a6ce6897b2d9411397b2e29b1be234eb6e50c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/27/2018
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="d1a4d-104">Pacchetto di installazione (Console di gestione dei pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d1a4d-104">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d1a4d-105">*Questo argomento viene descritto il comando all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows. Per il comando di PowerShell Install-Package generico, vedere il [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="d1a4d-105">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="d1a4d-106">Installa un pacchetto e le relative dipendenze in un progetto.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-106">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="d1a4d-107">Sintassi</span><span class="sxs-lookup"><span data-stu-id="d1a4d-107">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="d1a4d-108">In NuGet 2.8 + `Install-Package` può effettuare il downgrade di un pacchetto esistente nel progetto.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-108">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="d1a4d-109">Ad esempio, se si dispone di 5.1.0-rc1 italiano installato, il comando seguente sarebbe effettuare il downgrade a 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="d1a4d-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

<span data-ttu-id="d1a4d-110">NuGet 2.7 e versioni precedenti si verifica un errore che informa che è già installata una versione più recente.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-110">NuGet 2.7 and earlier gives an error saying that a newer version is already installed.</span></span>
  
## <a name="parameters"></a><span data-ttu-id="d1a4d-111">Parametri</span><span class="sxs-lookup"><span data-stu-id="d1a4d-111">Parameters</span></span>

| <span data-ttu-id="d1a4d-112">Parametro</span><span class="sxs-lookup"><span data-stu-id="d1a4d-112">Parameter</span></span> | <span data-ttu-id="d1a4d-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d1a4d-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1a4d-114">Id</span><span class="sxs-lookup"><span data-stu-id="d1a4d-114">Id</span></span> | <span data-ttu-id="d1a4d-115">(Obbligatorio) L'identificatore del pacchetto da installare.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-115">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="d1a4d-116">(*3.0 +*) l'identificatore può essere un percorso o URL di un `packages.config` file o un `.nupkg` file.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-116">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="d1a4d-117">-Id switch stesso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-117">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="d1a4d-118">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="d1a4d-118">IgnoreDependencies</span></span> | <span data-ttu-id="d1a4d-119">Installa solo questo pacchetto e non le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-119">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="d1a4d-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="d1a4d-120">ProjectName</span></span> | <span data-ttu-id="d1a4d-121">Il progetto in cui installare il pacchetto, verrà utilizzato per il progetto predefinito.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-121">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="d1a4d-122">Origine</span><span class="sxs-lookup"><span data-stu-id="d1a4d-122">Source</span></span> | <span data-ttu-id="d1a4d-123">Il percorso URL o una cartella per l'origine del pacchetto da cercare.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-123">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="d1a4d-124">I percorsi di cartella locale possono essere assoluto o relativo della cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-124">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="d1a4d-125">Se omesso, `Install-Package` Cerca l'origine pacchetto attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-125">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="d1a4d-126">Versione</span><span class="sxs-lookup"><span data-stu-id="d1a4d-126">Version</span></span> | <span data-ttu-id="d1a4d-127">La versione del pacchetto da installare, verrà utilizzato per la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-127">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="d1a4d-128">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="d1a4d-128">IncludePrerelease</span></span> | <span data-ttu-id="d1a4d-129">Considera i pacchetti della versione provvisoria per l'installazione.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-129">Considers prerelease packages for the install.</span></span> <span data-ttu-id="d1a4d-130">Se omesso, vengono considerati solo i pacchetti definitivi.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-130">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="d1a4d-131">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="d1a4d-131">FileConflictAction</span></span> | <span data-ttu-id="d1a4d-132">L'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-132">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="d1a4d-133">I valori possibili sono *sovrascrittura, Ignora, None, OverwriteAll*, e *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-133">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="d1a4d-134">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="d1a4d-134">DependencyVersion</span></span> | <span data-ttu-id="d1a4d-135">La versione dei pacchetti di dipendenza da usare, che può essere uno dei seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1a4d-135">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="d1a4d-136">*Più basso* (impostazione predefinita): la versione minima</span><span class="sxs-lookup"><span data-stu-id="d1a4d-136">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="d1a4d-137">*HighestPatch*: la versione con la patch più basso principale, secondaria più basso, più elevata</span><span class="sxs-lookup"><span data-stu-id="d1a4d-137">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="d1a4d-138">*HighestMinor*: la versione con il minimo principali, patch più alto, minore più alto</span><span class="sxs-lookup"><span data-stu-id="d1a4d-138">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="d1a4d-139">*Più alto* (impostazione predefinita per il pacchetto di aggiornamento senza parametri): la versione più recente</span><span class="sxs-lookup"><span data-stu-id="d1a4d-139">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="d1a4d-140">È possibile impostare il valore predefinito utilizzando il [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) impostazione di `Nuget.Config` file.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-140">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="d1a4d-141">WhatIf</span><span class="sxs-lookup"><span data-stu-id="d1a4d-141">WhatIf</span></span> | <span data-ttu-id="d1a4d-142">Viene illustrato che cosa accadrebbe eseguendo il comando senza eseguire effettivamente l'installazione.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-142">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="d1a4d-143">Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-143">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d1a4d-144">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="d1a4d-144">Common Parameters</span></span>

<span data-ttu-id="d1a4d-145">`Install-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d1a4d-145">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d1a4d-146">Esempi</span><span class="sxs-lookup"><span data-stu-id="d1a4d-146">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
