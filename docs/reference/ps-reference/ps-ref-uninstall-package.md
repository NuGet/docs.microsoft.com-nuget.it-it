---
title: Guida di riferimento a NuGet Uninstall-Package PowerShell
description: Informazioni di riferimento per il comando Uninstall-Package PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: d164176355e32e5bbe0a017fc2b291cbc9ef326a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237127"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="d72c8-103">Uninstall-Package (console di gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d72c8-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d72c8-104">*In questo argomento viene descritto il comando nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows. Per il comando generico di Uninstall-Package PowerShell, vedere le informazioni di [riferimento su PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="d72c8-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="d72c8-105">Rimuove un pacchetto da un progetto, rimuovendo facoltativamente le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="d72c8-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="d72c8-106">Se altri pacchetti dipendono da quello corrente, il comando ha esito negativo a meno che l'opzione –Force non sia specificata.</span><span class="sxs-lookup"><span data-stu-id="d72c8-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="d72c8-107">Sintassi</span><span class="sxs-lookup"><span data-stu-id="d72c8-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="d72c8-108">Se altri pacchetti dipendono da quello corrente, il comando ha esito negativo a meno che l'opzione –Force non sia specificata.</span><span class="sxs-lookup"><span data-stu-id="d72c8-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="d72c8-109">Parametri</span><span class="sxs-lookup"><span data-stu-id="d72c8-109">Parameters</span></span>

| <span data-ttu-id="d72c8-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="d72c8-110">Parameter</span></span> | <span data-ttu-id="d72c8-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d72c8-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d72c8-112">ID</span><span class="sxs-lookup"><span data-stu-id="d72c8-112">Id</span></span> | <span data-ttu-id="d72c8-113">Necessaria Identificatore del pacchetto da disinstallare.</span><span class="sxs-lookup"><span data-stu-id="d72c8-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="d72c8-114">L'opzione-ID è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="d72c8-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="d72c8-115">Versione</span><span class="sxs-lookup"><span data-stu-id="d72c8-115">Version</span></span> | <span data-ttu-id="d72c8-116">Versione del pacchetto da disinstallare, per impostazione predefinita la versione attualmente installata.</span><span class="sxs-lookup"><span data-stu-id="d72c8-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="d72c8-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="d72c8-117">RemoveDependencies</span></span> | <span data-ttu-id="d72c8-118">Disinstallare il pacchetto e le relative dipendenze non utilizzate.</span><span class="sxs-lookup"><span data-stu-id="d72c8-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="d72c8-119">Ovvero, se una dipendenza dispone di un altro pacchetto che dipende da esso, viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="d72c8-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="d72c8-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="d72c8-120">ProjectName</span></span> | <span data-ttu-id="d72c8-121">Progetto da cui disinstallare il pacchetto, per impostazione predefinita il progetto predefinito.</span><span class="sxs-lookup"><span data-stu-id="d72c8-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="d72c8-122">Force</span><span class="sxs-lookup"><span data-stu-id="d72c8-122">Force</span></span> | <span data-ttu-id="d72c8-123">Forza la disinstallazione di un pacchetto, anche se altri pacchetti dipendono da esso.</span><span class="sxs-lookup"><span data-stu-id="d72c8-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="d72c8-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="d72c8-124">WhatIf</span></span> | <span data-ttu-id="d72c8-125">Mostra cosa accade quando si esegue il comando senza eseguire effettivamente la disinstallazione.</span><span class="sxs-lookup"><span data-stu-id="d72c8-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="d72c8-126">Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="d72c8-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d72c8-127">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="d72c8-127">Common Parameters</span></span>

<span data-ttu-id="d72c8-128">`Uninstall-Package` supporta i seguenti [parametri comuni di PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d72c8-128">`Uninstall-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d72c8-129">Esempi</span><span class="sxs-lookup"><span data-stu-id="d72c8-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```