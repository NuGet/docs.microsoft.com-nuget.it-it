---
title: Guida di riferimento a NuGet Uninstall-Package PowerShell
description: Informazioni di riferimento sul comando Uninstall-package di PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5c963588d28cab42e5fb6a43b31a17e26e49d0d2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327278"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="085a1-103">Uninstall-Package (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="085a1-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="085a1-104">*In questo argomento viene descritto il comando nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows. Per il comando generico Uninstall-package di PowerShell, vedere le informazioni di [riferimento su PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="085a1-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="085a1-105">Rimuove un pacchetto da un progetto, rimuovendo facoltativamente le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="085a1-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="085a1-106">Se gli altri pacchetti dipendono da questo pacchetto, il comando avrà esito negativo a meno che non venga specificata l'opzione-Force.</span><span class="sxs-lookup"><span data-stu-id="085a1-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="085a1-107">Sintassi</span><span class="sxs-lookup"><span data-stu-id="085a1-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="085a1-108">Se gli altri pacchetti dipendono da questo pacchetto, il comando avrà esito negativo a meno che non venga specificata l'opzione-Force.</span><span class="sxs-lookup"><span data-stu-id="085a1-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="085a1-109">Parametri</span><span class="sxs-lookup"><span data-stu-id="085a1-109">Parameters</span></span>

| <span data-ttu-id="085a1-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="085a1-110">Parameter</span></span> | <span data-ttu-id="085a1-111">DESCRIZIONE</span><span class="sxs-lookup"><span data-stu-id="085a1-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="085a1-112">ID</span><span class="sxs-lookup"><span data-stu-id="085a1-112">Id</span></span> | <span data-ttu-id="085a1-113">Necessaria Identificatore del pacchetto da disinstallare.</span><span class="sxs-lookup"><span data-stu-id="085a1-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="085a1-114">L'opzione-ID è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="085a1-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="085a1-115">Version</span><span class="sxs-lookup"><span data-stu-id="085a1-115">Version</span></span> | <span data-ttu-id="085a1-116">Versione del pacchetto da disinstallare, per impostazione predefinita la versione attualmente installata.</span><span class="sxs-lookup"><span data-stu-id="085a1-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="085a1-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="085a1-117">RemoveDependencies</span></span> | <span data-ttu-id="085a1-118">Disinstallare il pacchetto e le relative dipendenze non utilizzate.</span><span class="sxs-lookup"><span data-stu-id="085a1-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="085a1-119">Ovvero, se una dipendenza dispone di un altro pacchetto che dipende da esso, viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="085a1-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="085a1-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="085a1-120">ProjectName</span></span> | <span data-ttu-id="085a1-121">Progetto da cui disinstallare il pacchetto, per impostazione predefinita il progetto predefinito.</span><span class="sxs-lookup"><span data-stu-id="085a1-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="085a1-122">Force</span><span class="sxs-lookup"><span data-stu-id="085a1-122">Force</span></span> | <span data-ttu-id="085a1-123">Forza la disinstallazione di un pacchetto, anche se altri pacchetti dipendono da esso.</span><span class="sxs-lookup"><span data-stu-id="085a1-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="085a1-124">Whatif</span><span class="sxs-lookup"><span data-stu-id="085a1-124">WhatIf</span></span> | <span data-ttu-id="085a1-125">Mostra cosa accade quando si esegue il comando senza eseguire effettivamente la disinstallazione.</span><span class="sxs-lookup"><span data-stu-id="085a1-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="085a1-126">Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="085a1-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="085a1-127">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="085a1-127">Common Parameters</span></span>

<span data-ttu-id="085a1-128">`Uninstall-Package`supporta i seguenti [parametri comuni di PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="085a1-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="085a1-129">Esempi</span><span class="sxs-lookup"><span data-stu-id="085a1-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
