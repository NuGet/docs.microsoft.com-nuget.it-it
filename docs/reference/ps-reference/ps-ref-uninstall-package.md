---
title: Informazioni di riferimento su NuGet Uninstall-Package PowerShell
description: Informazioni di Uninstall-Package comando di PowerShell nella console Gestione pacchetti NuGet in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 371e95c341efbce1c4a15facefc15cd51b266141
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901785"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="80e40-103">Uninstall-Package (Gestione pacchetti Console in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="80e40-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="80e40-104">*Questo argomento descrive il comando all'interno [della console Gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows. Per il comando powershell Uninstall-Package generico, vedere le informazioni di [riferimento su PackageManagement di PowerShell.](/powershell/module/packagemanagement)*</span><span class="sxs-lookup"><span data-stu-id="80e40-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="80e40-105">Rimuove un pacchetto da un progetto, rimuovendo facoltativamente le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="80e40-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="80e40-106">Se altri pacchetti dipendono da quello corrente, il comando ha esito negativo a meno che l'opzione –Force non sia specificata.</span><span class="sxs-lookup"><span data-stu-id="80e40-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="80e40-107">Sintassi</span><span class="sxs-lookup"><span data-stu-id="80e40-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="80e40-108">Se altri pacchetti dipendono da quello corrente, il comando ha esito negativo a meno che l'opzione –Force non sia specificata.</span><span class="sxs-lookup"><span data-stu-id="80e40-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="80e40-109">Parametri</span><span class="sxs-lookup"><span data-stu-id="80e40-109">Parameters</span></span>

| <span data-ttu-id="80e40-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="80e40-110">Parameter</span></span> | <span data-ttu-id="80e40-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="80e40-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="80e40-112">Id</span><span class="sxs-lookup"><span data-stu-id="80e40-112">Id</span></span> | <span data-ttu-id="80e40-113">(Obbligatorio) Identificatore del pacchetto da disinstallare.</span><span class="sxs-lookup"><span data-stu-id="80e40-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="80e40-114">L'opzione -Id è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="80e40-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="80e40-115">Versione</span><span class="sxs-lookup"><span data-stu-id="80e40-115">Version</span></span> | <span data-ttu-id="80e40-116">Versione del pacchetto da disinstallare, che per impostazione predefinita è la versione attualmente installata.</span><span class="sxs-lookup"><span data-stu-id="80e40-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="80e40-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="80e40-117">RemoveDependencies</span></span> | <span data-ttu-id="80e40-118">Disinstallare il pacchetto e le relative dipendenze inutilizzate.</span><span class="sxs-lookup"><span data-stu-id="80e40-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="80e40-119">In altre informazioni, se una dipendenza ha un altro pacchetto che dipende da essa, viene ignorata.</span><span class="sxs-lookup"><span data-stu-id="80e40-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="80e40-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="80e40-120">ProjectName</span></span> | <span data-ttu-id="80e40-121">Progetto da cui disinstallare il pacchetto, con il progetto predefinito.</span><span class="sxs-lookup"><span data-stu-id="80e40-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="80e40-122">Force</span><span class="sxs-lookup"><span data-stu-id="80e40-122">Force</span></span> | <span data-ttu-id="80e40-123">Forza la disinstallazione di un pacchetto, anche se altri pacchetti dipendono da esso.</span><span class="sxs-lookup"><span data-stu-id="80e40-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="80e40-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="80e40-124">WhatIf</span></span> | <span data-ttu-id="80e40-125">Mostra cosa accade quando si esegue il comando senza eseguire effettivamente la disinstallazione.</span><span class="sxs-lookup"><span data-stu-id="80e40-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="80e40-126">Nessuno di questi parametri accetta l'input della pipeline o i caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="80e40-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="80e40-127">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="80e40-127">Common Parameters</span></span>

<span data-ttu-id="80e40-128">`Uninstall-Package` supporta i parametri comuni di [PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters)seguenti: Debug, Azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="80e40-128">`Uninstall-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="80e40-129">Esempi</span><span class="sxs-lookup"><span data-stu-id="80e40-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```