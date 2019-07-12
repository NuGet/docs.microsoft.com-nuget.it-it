---
title: Riferimento di PowerShell di NuGet Uninstall-Package
description: Informazioni di riferimento per il comando PowerShell Uninstall-Package nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: c95479103be2cba3b4eb6964ea761870477863bd
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842478"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="cbe28-103">Uninstall-Package (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="cbe28-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="cbe28-104">*In questo argomento descrive il comando all'interno di [Console di gestione pacchetti](package-manager-console.md) in Visual Studio in Windows. Per il comando PowerShell Uninstall-Package generico, vedere la [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="cbe28-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="cbe28-105">Rimuove un pacchetto da un progetto, se lo si desidera rimuovere le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="cbe28-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="cbe28-106">Se altri pacchetti dipendono da questo pacchetto, il comando avrà esito negativo a meno che non – Force è specificata l'opzione.</span><span class="sxs-lookup"><span data-stu-id="cbe28-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="cbe28-107">Sintassi</span><span class="sxs-lookup"><span data-stu-id="cbe28-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="cbe28-108">Se altri pacchetti dipendono da questo pacchetto, il comando avrà esito negativo a meno che non – Force è specificata l'opzione.</span><span class="sxs-lookup"><span data-stu-id="cbe28-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="cbe28-109">Parametri</span><span class="sxs-lookup"><span data-stu-id="cbe28-109">Parameters</span></span>

| <span data-ttu-id="cbe28-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="cbe28-110">Parameter</span></span> | <span data-ttu-id="cbe28-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cbe28-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cbe28-112">ID</span><span class="sxs-lookup"><span data-stu-id="cbe28-112">Id</span></span> | <span data-ttu-id="cbe28-113">(Obbligatorio) L'identificatore del pacchetto da disinstallare.</span><span class="sxs-lookup"><span data-stu-id="cbe28-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="cbe28-114">-Id commutatore stesso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="cbe28-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="cbe28-115">Version</span><span class="sxs-lookup"><span data-stu-id="cbe28-115">Version</span></span> | <span data-ttu-id="cbe28-116">La versione del pacchetto da disinstallare, verrà utilizzato per la versione attualmente installata.</span><span class="sxs-lookup"><span data-stu-id="cbe28-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="cbe28-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="cbe28-117">RemoveDependencies</span></span> | <span data-ttu-id="cbe28-118">Disinstallare il pacchetto e le relative dipendenze inutilizzati.</span><span class="sxs-lookup"><span data-stu-id="cbe28-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="cbe28-119">Vale a dire, se tutte le dipendenze dispone di un altro pacchetto dipendente, si viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="cbe28-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="cbe28-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="cbe28-120">ProjectName</span></span> | <span data-ttu-id="cbe28-121">Il progetto da cui disinstallare il pacchetto, verrà utilizzato per il progetto predefinito.</span><span class="sxs-lookup"><span data-stu-id="cbe28-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="cbe28-122">Force</span><span class="sxs-lookup"><span data-stu-id="cbe28-122">Force</span></span> | <span data-ttu-id="cbe28-123">Forza un pacchetto da disinstallare, anche se altri pacchetti dipendono da esso.</span><span class="sxs-lookup"><span data-stu-id="cbe28-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="cbe28-124">Whatif</span><span class="sxs-lookup"><span data-stu-id="cbe28-124">WhatIf</span></span> | <span data-ttu-id="cbe28-125">Viene illustrato che cosa accadrebbe quando si esegue il comando senza eseguire effettivamente la disinstallazione.</span><span class="sxs-lookup"><span data-stu-id="cbe28-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="cbe28-126">Nessuno di questi parametri accettano caratteri jolly o input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="cbe28-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="cbe28-127">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="cbe28-127">Common Parameters</span></span>

<span data-ttu-id="cbe28-128">`Uninstall-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="cbe28-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="cbe28-129">Esempi</span><span class="sxs-lookup"><span data-stu-id="cbe28-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
