---
title: Riferimento di PowerShell di NuGet Uninstall-Package | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando di PowerShell Uninstall-Package nella Console di gestione pacchetti NuGet in Visual Studio.
keywords: Console di gestione, i comandi di Powershell di NuGet, riferimento di Powershell di NuGet, pacchetto di disinstallazione del pacchetto NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: db7cf9b2282bf40988eee2308c256381c4fd5124
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="371fb-104">Uninstall-Package (Package Manager Console in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="371fb-104">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="371fb-105">*Questo argomento viene descritto il comando all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows. Per il comando PowerShell Uninstall-Package generico, vedere il [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="371fb-105">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="371fb-106">Rimuove un pacchetto da un progetto, rimuovere facoltativamente le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="371fb-106">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="371fb-107">Se altri pacchetti dipendono da questo pacchetto, il comando avrà esito negativo a meno che non – Force non sia specificata l'opzione.</span><span class="sxs-lookup"><span data-stu-id="371fb-107">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="371fb-108">Sintassi</span><span class="sxs-lookup"><span data-stu-id="371fb-108">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="371fb-109">Se altri pacchetti dipendono da questo pacchetto, il comando avrà esito negativo a meno che non – Force non sia specificata l'opzione.</span><span class="sxs-lookup"><span data-stu-id="371fb-109">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="371fb-110">Parametri</span><span class="sxs-lookup"><span data-stu-id="371fb-110">Parameters</span></span>

| <span data-ttu-id="371fb-111">Parametro</span><span class="sxs-lookup"><span data-stu-id="371fb-111">Parameter</span></span> | <span data-ttu-id="371fb-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="371fb-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="371fb-113">Id</span><span class="sxs-lookup"><span data-stu-id="371fb-113">Id</span></span> | <span data-ttu-id="371fb-114">(Obbligatorio) L'identificatore del pacchetto da disinstallare.</span><span class="sxs-lookup"><span data-stu-id="371fb-114">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="371fb-115">-Id switch stesso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="371fb-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="371fb-116">Versione</span><span class="sxs-lookup"><span data-stu-id="371fb-116">Version</span></span> | <span data-ttu-id="371fb-117">La versione del pacchetto da disinstallare, verrà utilizzato per la versione attualmente installata.</span><span class="sxs-lookup"><span data-stu-id="371fb-117">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="371fb-118">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="371fb-118">RemoveDependencies</span></span> | <span data-ttu-id="371fb-119">Disinstallare il pacchetto e delle relative dipendenze non utilizzate.</span><span class="sxs-lookup"><span data-stu-id="371fb-119">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="371fb-120">Vale a dire, se tutte le dipendenze dispone di un altro pacchetto dipendente, viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="371fb-120">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="371fb-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="371fb-121">ProjectName</span></span> | <span data-ttu-id="371fb-122">Il progetto da cui disinstallare il pacchetto, verrà utilizzato per il progetto predefinito.</span><span class="sxs-lookup"><span data-stu-id="371fb-122">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="371fb-123">Force</span><span class="sxs-lookup"><span data-stu-id="371fb-123">Force</span></span> | <span data-ttu-id="371fb-124">Forza un pacchetto da disinstallare, anche se altri pacchetti dipendono da esso.</span><span class="sxs-lookup"><span data-stu-id="371fb-124">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="371fb-125">WhatIf</span><span class="sxs-lookup"><span data-stu-id="371fb-125">WhatIf</span></span> | <span data-ttu-id="371fb-126">Viene illustrato che cosa accadrebbe eseguendo il comando senza eseguire effettivamente la disinstallazione.</span><span class="sxs-lookup"><span data-stu-id="371fb-126">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="371fb-127">Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.</span><span class="sxs-lookup"><span data-stu-id="371fb-127">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="371fb-128">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="371fb-128">Common Parameters</span></span>

<span data-ttu-id="371fb-129">`Uninstall-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="371fb-129">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="371fb-130">Esempi</span><span class="sxs-lookup"><span data-stu-id="371fb-130">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
