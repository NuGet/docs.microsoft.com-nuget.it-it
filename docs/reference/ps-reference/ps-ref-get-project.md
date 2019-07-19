---
title: Guida di riferimento a NuGet Get-Project PowerShell
description: Riferimento per il comando di PowerShell GetProject nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 830746f032bb4eb916508ef320c5b3d0486b89a4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327358"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="aa6b6-103">Get-Project (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="aa6b6-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="aa6b6-104">*Disponibile solo nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="aa6b6-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="aa6b6-105">Visualizza le informazioni relative al progetto predefinito o specificato.</span><span class="sxs-lookup"><span data-stu-id="aa6b6-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="aa6b6-106">`Get-Project`in particolare, restituisce un referente all'oggetto DTE di Visual Studio (ambiente degli strumenti di sviluppo) per il progetto.</span><span class="sxs-lookup"><span data-stu-id="aa6b6-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="aa6b6-107">Sintassi</span><span class="sxs-lookup"><span data-stu-id="aa6b6-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="aa6b6-108">Parametri</span><span class="sxs-lookup"><span data-stu-id="aa6b6-108">Parameters</span></span>

| <span data-ttu-id="aa6b6-109">Parametro</span><span class="sxs-lookup"><span data-stu-id="aa6b6-109">Parameter</span></span> | <span data-ttu-id="aa6b6-110">DESCRIZIONE</span><span class="sxs-lookup"><span data-stu-id="aa6b6-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aa6b6-111">Name</span><span class="sxs-lookup"><span data-stu-id="aa6b6-111">Name</span></span> | <span data-ttu-id="aa6b6-112">Specifica il progetto da visualizzare, per impostazione predefinita il progetto predefinito selezionato nella console di gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="aa6b6-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="aa6b6-113">L'opzione-Name è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="aa6b6-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="aa6b6-114">Tutti</span><span class="sxs-lookup"><span data-stu-id="aa6b6-114">All</span></span> | <span data-ttu-id="aa6b6-115">Visualizza le informazioni per ogni progetto nella soluzione. l'ordine dei progetti non è deterministico.</span><span class="sxs-lookup"><span data-stu-id="aa6b6-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="aa6b6-116">Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="aa6b6-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="aa6b6-117">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="aa6b6-117">Common Parameters</span></span>

<span data-ttu-id="aa6b6-118">`Get-Project`supporta i seguenti [parametri comuni di PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="aa6b6-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="aa6b6-119">Esempi</span><span class="sxs-lookup"><span data-stu-id="aa6b6-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```