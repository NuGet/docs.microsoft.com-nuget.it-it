---
title: Riferimento di PowerShell di NuGet. Get a progetto
description: Riferimento per il comando GetProject PowerShell nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: afdf9f762bbd34531f9d9093238a2fed27e3f4d3
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817756"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="61717-103">Get-Project (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="61717-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="61717-104">*Disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="61717-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="61717-105">Visualizza informazioni sul valore predefinito o il progetto specificato.</span><span class="sxs-lookup"><span data-stu-id="61717-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="61717-106">`Get-Project` in particolare, restituisce un riferimento per l'oggetto di Visual Studio DTE (Development Tools Environment) per il progetto.</span><span class="sxs-lookup"><span data-stu-id="61717-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="61717-107">Sintassi</span><span class="sxs-lookup"><span data-stu-id="61717-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="61717-108">Parametri</span><span class="sxs-lookup"><span data-stu-id="61717-108">Parameters</span></span>

| <span data-ttu-id="61717-109">Parametro</span><span class="sxs-lookup"><span data-stu-id="61717-109">Parameter</span></span> | <span data-ttu-id="61717-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="61717-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="61717-111">nome</span><span class="sxs-lookup"><span data-stu-id="61717-111">Name</span></span> | <span data-ttu-id="61717-112">Specifica il progetto da visualizzare, verrà utilizzato per il progetto predefinito selezionato nella Console di gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="61717-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="61717-113">-Il nome del parametro è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="61717-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="61717-114">Tutti</span><span class="sxs-lookup"><span data-stu-id="61717-114">All</span></span> | <span data-ttu-id="61717-115">Visualizza informazioni per ogni progetto nella soluzione. l'ordine dei progetti non è deterministico.</span><span class="sxs-lookup"><span data-stu-id="61717-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="61717-116">Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.</span><span class="sxs-lookup"><span data-stu-id="61717-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="61717-117">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="61717-117">Common Parameters</span></span>

<span data-ttu-id="61717-118">`Get-Project` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="61717-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="61717-119">Esempi</span><span class="sxs-lookup"><span data-stu-id="61717-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```