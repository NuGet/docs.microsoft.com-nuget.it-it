---
title: Riferimento di PowerShell Get-progetti per NuGet
description: Informazioni di riferimento per il comando GetProject PowerShell nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 2ceb1557eafd213c148d3ab870925ef5bbbee145
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842273"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="85888-103">Get-Project (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="85888-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="85888-104">*Disponibile solo all'interno di [Console di gestione pacchetti](package-manager-console.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="85888-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="85888-105">Visualizza informazioni sull'impostazione predefinita o progetto specificato.</span><span class="sxs-lookup"><span data-stu-id="85888-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="85888-106">`Get-Project` in particolare, restituisce un riferimento all'oggetto per il progetto di Visual Studio DTE (Development Tools Environment).</span><span class="sxs-lookup"><span data-stu-id="85888-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="85888-107">Sintassi</span><span class="sxs-lookup"><span data-stu-id="85888-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="85888-108">Parametri</span><span class="sxs-lookup"><span data-stu-id="85888-108">Parameters</span></span>

| <span data-ttu-id="85888-109">Parametro</span><span class="sxs-lookup"><span data-stu-id="85888-109">Parameter</span></span> | <span data-ttu-id="85888-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="85888-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="85888-111">NOME</span><span class="sxs-lookup"><span data-stu-id="85888-111">Name</span></span> | <span data-ttu-id="85888-112">Specifica il progetto per la visualizzazione, verrà utilizzato per il progetto predefinito selezionato nella Console di gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="85888-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="85888-113">-Nome del commutatore è a sua volta facoltativo.</span><span class="sxs-lookup"><span data-stu-id="85888-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="85888-114">Tutti</span><span class="sxs-lookup"><span data-stu-id="85888-114">All</span></span> | <span data-ttu-id="85888-115">Visualizza le informazioni per ogni progetto nella soluzione; l'ordine dei progetti non è deterministico.</span><span class="sxs-lookup"><span data-stu-id="85888-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="85888-116">Nessuno di questi parametri accettano caratteri jolly o input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="85888-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="85888-117">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="85888-117">Common Parameters</span></span>

<span data-ttu-id="85888-118">`Get-Project` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="85888-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="85888-119">Esempi</span><span class="sxs-lookup"><span data-stu-id="85888-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```