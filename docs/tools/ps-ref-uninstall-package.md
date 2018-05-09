---
title: Riferimento di PowerShell di NuGet Uninstall-Package
description: Riferimento per il comando di PowerShell Uninstall-Package nella Console di gestione pacchetti NuGet in Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5969526a12cb6e06f23f35a2481d0385bb9780ab
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="6ff10-103">Uninstall-Package (Package Manager Console in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="6ff10-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="6ff10-104">*Questo argomento viene descritto il comando all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows. Per il comando PowerShell Uninstall-Package generico, vedere il [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="6ff10-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="6ff10-105">Rimuove un pacchetto da un progetto, rimuovere facoltativamente le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="6ff10-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="6ff10-106">Se altri pacchetti dipendono da questo pacchetto, il comando avrà esito negativo a meno che non – Force non sia specificata l'opzione.</span><span class="sxs-lookup"><span data-stu-id="6ff10-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="6ff10-107">Sintassi</span><span class="sxs-lookup"><span data-stu-id="6ff10-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="6ff10-108">Se altri pacchetti dipendono da questo pacchetto, il comando avrà esito negativo a meno che non – Force non sia specificata l'opzione.</span><span class="sxs-lookup"><span data-stu-id="6ff10-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="6ff10-109">Parametri</span><span class="sxs-lookup"><span data-stu-id="6ff10-109">Parameters</span></span>

| <span data-ttu-id="6ff10-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="6ff10-110">Parameter</span></span> | <span data-ttu-id="6ff10-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6ff10-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6ff10-112">Id</span><span class="sxs-lookup"><span data-stu-id="6ff10-112">Id</span></span> | <span data-ttu-id="6ff10-113">(Obbligatorio) L'identificatore del pacchetto da disinstallare.</span><span class="sxs-lookup"><span data-stu-id="6ff10-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="6ff10-114">-Id switch stesso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="6ff10-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="6ff10-115">Versione</span><span class="sxs-lookup"><span data-stu-id="6ff10-115">Version</span></span> | <span data-ttu-id="6ff10-116">La versione del pacchetto da disinstallare, verrà utilizzato per la versione attualmente installata.</span><span class="sxs-lookup"><span data-stu-id="6ff10-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="6ff10-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="6ff10-117">RemoveDependencies</span></span> | <span data-ttu-id="6ff10-118">Disinstallare il pacchetto e delle relative dipendenze non utilizzate.</span><span class="sxs-lookup"><span data-stu-id="6ff10-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="6ff10-119">Vale a dire, se tutte le dipendenze dispone di un altro pacchetto dipendente, viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="6ff10-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="6ff10-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="6ff10-120">ProjectName</span></span> | <span data-ttu-id="6ff10-121">Il progetto da cui disinstallare il pacchetto, verrà utilizzato per il progetto predefinito.</span><span class="sxs-lookup"><span data-stu-id="6ff10-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="6ff10-122">Force</span><span class="sxs-lookup"><span data-stu-id="6ff10-122">Force</span></span> | <span data-ttu-id="6ff10-123">Forza un pacchetto da disinstallare, anche se altri pacchetti dipendono da esso.</span><span class="sxs-lookup"><span data-stu-id="6ff10-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="6ff10-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="6ff10-124">WhatIf</span></span> | <span data-ttu-id="6ff10-125">Viene illustrato che cosa accadrebbe eseguendo il comando senza eseguire effettivamente la disinstallazione.</span><span class="sxs-lookup"><span data-stu-id="6ff10-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="6ff10-126">Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.</span><span class="sxs-lookup"><span data-stu-id="6ff10-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="6ff10-127">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="6ff10-127">Common Parameters</span></span>

<span data-ttu-id="6ff10-128">`Uninstall-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6ff10-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="6ff10-129">Esempi</span><span class="sxs-lookup"><span data-stu-id="6ff10-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
