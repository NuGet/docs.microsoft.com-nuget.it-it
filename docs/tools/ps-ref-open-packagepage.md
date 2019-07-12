---
title: Informazioni di riferimento di NuGet Open-PackagePage PowerShell
description: Informazioni di riferimento per il comando PowerShell Open-PackagePage nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fd738f15b461051c4e9413b3035456c687979b97
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842270"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="d20cb-103">Open-PackagePage (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d20cb-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d20cb-104">*Deprecato in 3.0 e versioni successive; disponibile solo all'interno di [Console di gestione pacchetti](package-manager-console.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="d20cb-104">*Deprecated in 3.0+; available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="d20cb-105">Avvia il browser predefinito con il progetto, licenza o URL per segnalare abusi per il pacchetto specificato.</span><span class="sxs-lookup"><span data-stu-id="d20cb-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="d20cb-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="d20cb-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="d20cb-107">Parametri</span><span class="sxs-lookup"><span data-stu-id="d20cb-107">Parameters</span></span>

| <span data-ttu-id="d20cb-108">Parametro</span><span class="sxs-lookup"><span data-stu-id="d20cb-108">Parameter</span></span> | <span data-ttu-id="d20cb-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d20cb-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d20cb-110">ID</span><span class="sxs-lookup"><span data-stu-id="d20cb-110">Id</span></span> | <span data-ttu-id="d20cb-111">L'ID del pacchetto del pacchetto desiderato.</span><span class="sxs-lookup"><span data-stu-id="d20cb-111">The package ID of the desired package.</span></span> <span data-ttu-id="d20cb-112">-Id commutatore stesso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="d20cb-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="d20cb-113">Version</span><span class="sxs-lookup"><span data-stu-id="d20cb-113">Version</span></span> | <span data-ttu-id="d20cb-114">La versione del pacchetto, verrà utilizzato per la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="d20cb-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="d20cb-115">`Source`</span><span class="sxs-lookup"><span data-stu-id="d20cb-115">Source</span></span> | <span data-ttu-id="d20cb-116">L'origine del pacchetto, verrà utilizzato per l'origine selezionata nell'elenco a discesa di origine.</span><span class="sxs-lookup"><span data-stu-id="d20cb-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="d20cb-117">Licenza</span><span class="sxs-lookup"><span data-stu-id="d20cb-117">License</span></span> | <span data-ttu-id="d20cb-118">Apre il browser all'URL della licenza del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d20cb-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="d20cb-119">Se viene specificato - licenza né - ReportAbuse, nel browser verrà aperta URL del progetto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d20cb-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="d20cb-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="d20cb-120">ReportAbuse</span></span> | <span data-ttu-id="d20cb-121">Apre il browser all'URL per segnalare abusi del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d20cb-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="d20cb-122">Se viene specificato - licenza né - ReportAbuse, nel browser verrà aperta URL del progetto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d20cb-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="d20cb-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="d20cb-123">PassThru</span></span> | <span data-ttu-id="d20cb-124">Viene visualizzato l'URL; usare con - WhatIf per non visualizzare aprendo il browser.</span><span class="sxs-lookup"><span data-stu-id="d20cb-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="d20cb-125">Nessuno di questi parametri accettano caratteri jolly o input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="d20cb-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d20cb-126">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="d20cb-126">Common Parameters</span></span>

<span data-ttu-id="d20cb-127">`Open-PackagePage` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d20cb-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d20cb-128">Esempi</span><span class="sxs-lookup"><span data-stu-id="d20cb-128">Examples</span></span>

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```