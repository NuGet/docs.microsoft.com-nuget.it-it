---
title: Informazioni di riferimento su PowerShell Install-Package di NuGet
description: Riferimento per il comando di PowerShell Install-Package nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 1899662049735189ab4dcb728df5d56afdc5f7c5
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327338"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="9ff68-103">Install-Package (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="9ff68-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="9ff68-104">*In questo argomento viene descritto il comando nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows. Per il comando di PowerShell Install-Package generico, vedere le informazioni di [riferimento su PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="9ff68-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="9ff68-105">Installa un pacchetto e le relative dipendenze in un progetto.</span><span class="sxs-lookup"><span data-stu-id="9ff68-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="9ff68-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="9ff68-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="9ff68-107">In NuGet 2.8 +, `Install-Package` può effettuare il downgrade di un pacchetto esistente nel progetto.</span><span class="sxs-lookup"><span data-stu-id="9ff68-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="9ff68-108">Se, ad esempio, è installato Microsoft. AspNet. MVC 5.1.0-RC1, il comando seguente esegue il downgrade a 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="9ff68-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="9ff68-109">Parametri</span><span class="sxs-lookup"><span data-stu-id="9ff68-109">Parameters</span></span>

| <span data-ttu-id="9ff68-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="9ff68-110">Parameter</span></span> | <span data-ttu-id="9ff68-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9ff68-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9ff68-112">ID</span><span class="sxs-lookup"><span data-stu-id="9ff68-112">Id</span></span> | <span data-ttu-id="9ff68-113">Necessaria Identificatore del pacchetto da installare.</span><span class="sxs-lookup"><span data-stu-id="9ff68-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="9ff68-114">(*3.0 +* ) L'identificatore può essere un percorso o un URL di `packages.config` un file `.nupkg` o di un file.</span><span class="sxs-lookup"><span data-stu-id="9ff68-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="9ff68-115">L'opzione-ID è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="9ff68-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="9ff68-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="9ff68-116">IgnoreDependencies</span></span> | <span data-ttu-id="9ff68-117">Installare solo questo pacchetto e non le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="9ff68-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="9ff68-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="9ff68-118">ProjectName</span></span> | <span data-ttu-id="9ff68-119">Progetto in cui installare il pacchetto, per impostazione predefinita il progetto predefinito.</span><span class="sxs-lookup"><span data-stu-id="9ff68-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="9ff68-120">Source</span><span class="sxs-lookup"><span data-stu-id="9ff68-120">Source</span></span> | <span data-ttu-id="9ff68-121">URL o percorso della cartella per l'origine del pacchetto da cercare.</span><span class="sxs-lookup"><span data-stu-id="9ff68-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="9ff68-122">I percorsi delle cartelle locali possono essere assoluti o relativi alla cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="9ff68-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="9ff68-123">Se omesso, `Install-Package` Cerca nell'origine del pacchetto attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="9ff68-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="9ff68-124">Version</span><span class="sxs-lookup"><span data-stu-id="9ff68-124">Version</span></span> | <span data-ttu-id="9ff68-125">Versione del pacchetto da installare, per impostazione predefinita la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="9ff68-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="9ff68-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="9ff68-126">IncludePrerelease</span></span> | <span data-ttu-id="9ff68-127">Considera i pacchetti di versioni non definitive per l'installazione.</span><span class="sxs-lookup"><span data-stu-id="9ff68-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="9ff68-128">Se omesso, vengono considerati solo i pacchetti stabili.</span><span class="sxs-lookup"><span data-stu-id="9ff68-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="9ff68-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="9ff68-129">FileConflictAction</span></span> | <span data-ttu-id="9ff68-130">Azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto.</span><span class="sxs-lookup"><span data-stu-id="9ff68-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="9ff68-131">I valori possibili sono *overwrite, ignore, None, OverwriteAll*e *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="9ff68-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="9ff68-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="9ff68-132">DependencyVersion</span></span> | <span data-ttu-id="9ff68-133">Versione dei pacchetti di dipendenze da usare. i possibili tipi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="9ff68-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="9ff68-134">*Più bassa* (impostazione predefinita): versione più bassa</span><span class="sxs-lookup"><span data-stu-id="9ff68-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="9ff68-135">*HighestPatch*: versione con la patch principale più bassa, minore minore, più alta</span><span class="sxs-lookup"><span data-stu-id="9ff68-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="9ff68-136">*HighestMinor*: versione con la patch principale più bassa, minore più elevata</span><span class="sxs-lookup"><span data-stu-id="9ff68-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="9ff68-137">*Più alta* (impostazione predefinita per Update-Package senza parametri): la versione più recente</span><span class="sxs-lookup"><span data-stu-id="9ff68-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="9ff68-138">È possibile impostare il valore predefinito usando l' [`dependencyVersion`](../nuget-config-file.md#config-section) impostazione `Nuget.Config` nel file.</span><span class="sxs-lookup"><span data-stu-id="9ff68-138">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="9ff68-139">Whatif</span><span class="sxs-lookup"><span data-stu-id="9ff68-139">WhatIf</span></span> | <span data-ttu-id="9ff68-140">Mostra cosa accade quando si esegue il comando senza eseguire effettivamente l'installazione.</span><span class="sxs-lookup"><span data-stu-id="9ff68-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="9ff68-141">Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="9ff68-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="9ff68-142">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="9ff68-142">Common Parameters</span></span>

<span data-ttu-id="9ff68-143">`Install-Package`supporta i seguenti [parametri comuni di PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9ff68-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="9ff68-144">Esempi</span><span class="sxs-lookup"><span data-stu-id="9ff68-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
