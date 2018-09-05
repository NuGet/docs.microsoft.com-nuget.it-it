---
title: Riferimento di PowerShell di NuGet Install-Package
description: Informazioni di riferimento per il comando di PowerShell Install-Package nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: e7ddf9ad97cbb4ec9cfc8b01f366511239f41416
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546026"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="7a5f3-103">Install-Package (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="7a5f3-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7a5f3-104">*In questo argomento descrive il comando all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows. Per il comando di PowerShell Install-Package generico, vedere la [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="7a5f3-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="7a5f3-105">Installa un pacchetto e le relative dipendenze in un progetto.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="7a5f3-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="7a5f3-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="7a5f3-107">In NuGet 2.8 + `Install-Package` può effettuare il downgrade di un pacchetto esistente nel progetto.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="7a5f3-108">Ad esempio, se hai 5.1.0-rc1 ASPNET installato, il comando seguente potrebbe effettuare il downgrade alla 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="7a5f3-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="7a5f3-109">Parametri</span><span class="sxs-lookup"><span data-stu-id="7a5f3-109">Parameters</span></span>

| <span data-ttu-id="7a5f3-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="7a5f3-110">Parameter</span></span> | <span data-ttu-id="7a5f3-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7a5f3-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7a5f3-112">Id</span><span class="sxs-lookup"><span data-stu-id="7a5f3-112">Id</span></span> | <span data-ttu-id="7a5f3-113">(Obbligatorio) L'identificatore del pacchetto da installare.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="7a5f3-114">(*3.0 e versioni successive*) l'identificatore può essere un percorso o URL di un `packages.config` file o un `.nupkg` file.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="7a5f3-115">-Id commutatore stesso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="7a5f3-116">MSI</span><span class="sxs-lookup"><span data-stu-id="7a5f3-116">IgnoreDependencies</span></span> | <span data-ttu-id="7a5f3-117">Installare solo il pacchetto e non le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="7a5f3-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="7a5f3-118">ProjectName</span></span> | <span data-ttu-id="7a5f3-119">Il progetto in cui si desidera installare il pacchetto, verrà utilizzato per il progetto predefinito.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="7a5f3-120">Origine</span><span class="sxs-lookup"><span data-stu-id="7a5f3-120">Source</span></span> | <span data-ttu-id="7a5f3-121">Il percorso URL o una cartella per l'origine del pacchetto da cercare.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="7a5f3-122">I percorsi di cartella locale possono essere assoluto o relativo rispetto alla cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="7a5f3-123">Se omesso, `Install-Package` Cerca l'origine del pacchetto attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="7a5f3-124">Versione</span><span class="sxs-lookup"><span data-stu-id="7a5f3-124">Version</span></span> | <span data-ttu-id="7a5f3-125">La versione del pacchetto da installare, verrà utilizzato per la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="7a5f3-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="7a5f3-126">IncludePrerelease</span></span> | <span data-ttu-id="7a5f3-127">Prende in considerazione i pacchetti di versione non definitivo per l'installazione.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="7a5f3-128">Se omesso, vengono considerati solo i pacchetti stabili.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="7a5f3-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="7a5f3-129">FileConflictAction</span></span> | <span data-ttu-id="7a5f3-130">L'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti farvi riferimento il progetto.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="7a5f3-131">I valori possibili sono *Sovrascrivi, Ignore, None, OverwriteAll*, e *(3.0 e versioni successive)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="7a5f3-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="7a5f3-132">DependencyVersion</span></span> | <span data-ttu-id="7a5f3-133">La versione dei pacchetti di dipendenza da usare, che può essere uno dei seguenti:</span><span class="sxs-lookup"><span data-stu-id="7a5f3-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="7a5f3-134">*Più basso* (impostazione predefinita): la versione più bassa</span><span class="sxs-lookup"><span data-stu-id="7a5f3-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="7a5f3-135">*HighestPatch*: la versione con patch più bassa principali, più bassa secondaria, più alto</span><span class="sxs-lookup"><span data-stu-id="7a5f3-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="7a5f3-136">*HighestMinor*: la versione con il minimo principali, patch secondaria, massima più alto</span><span class="sxs-lookup"><span data-stu-id="7a5f3-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="7a5f3-137">*Più alto* (valore predefinito per Update-Package senza parametri): la versione più recente</span><span class="sxs-lookup"><span data-stu-id="7a5f3-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="7a5f3-138">È possibile impostare il valore predefinito usando il [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) impostazione nel `Nuget.Config` file.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-138">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="7a5f3-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="7a5f3-139">WhatIf</span></span> | <span data-ttu-id="7a5f3-140">Viene illustrato che cosa accadrebbe quando si esegue il comando senza eseguire effettivamente l'installazione.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="7a5f3-141">Nessuno di questi parametri accettano caratteri jolly o input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7a5f3-142">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="7a5f3-142">Common Parameters</span></span>

<span data-ttu-id="7a5f3-143">`Install-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="7a5f3-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7a5f3-144">Esempi</span><span class="sxs-lookup"><span data-stu-id="7a5f3-144">Examples</span></span>

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
