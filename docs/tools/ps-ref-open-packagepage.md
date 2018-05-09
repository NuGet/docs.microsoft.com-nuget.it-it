---
title: Riferimento di PowerShell di NuGet Open-PackagePage
description: Riferimento per il comando Apri PackagePage PowerShell nella Console di gestione pacchetti NuGet in Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: df4bea390105a7e3fc5d2abd476f2908d92bbcf8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="08952-103">Apri-PackagePage (Console di gestione dei pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="08952-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="08952-104">*Deprecato in 3.0 +;) disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="08952-104">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="08952-105">Avvia il browser predefinito con il progetto, licenza o report abuso URL per il pacchetto specificato.</span><span class="sxs-lookup"><span data-stu-id="08952-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="08952-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="08952-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="08952-107">Parametri</span><span class="sxs-lookup"><span data-stu-id="08952-107">Parameters</span></span>

| <span data-ttu-id="08952-108">Parametro</span><span class="sxs-lookup"><span data-stu-id="08952-108">Parameter</span></span> | <span data-ttu-id="08952-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="08952-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="08952-110">Id</span><span class="sxs-lookup"><span data-stu-id="08952-110">Id</span></span> | <span data-ttu-id="08952-111">L'ID del pacchetto del pacchetto desiderato.</span><span class="sxs-lookup"><span data-stu-id="08952-111">The package ID of the desired package.</span></span> <span data-ttu-id="08952-112">-Id switch stesso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="08952-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="08952-113">Versione</span><span class="sxs-lookup"><span data-stu-id="08952-113">Version</span></span> | <span data-ttu-id="08952-114">La versione del pacchetto, verrà utilizzato per la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="08952-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="08952-115">Origine</span><span class="sxs-lookup"><span data-stu-id="08952-115">Source</span></span> | <span data-ttu-id="08952-116">L'origine del pacchetto, verrà utilizzato per l'origine selezionata nell'elenco a discesa di origine.</span><span class="sxs-lookup"><span data-stu-id="08952-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="08952-117">Licenza</span><span class="sxs-lookup"><span data-stu-id="08952-117">License</span></span> | <span data-ttu-id="08952-118">Apre il browser all'URL di licenza del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="08952-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="08952-119">Se viene specificato - licenza né - ReportAbuse, si apre il browser con URL di progetto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="08952-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="08952-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="08952-120">ReportAbuse</span></span> | <span data-ttu-id="08952-121">Apre il browser all'URL di evitare eventuali abusi Report del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="08952-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="08952-122">Se viene specificato - licenza né - ReportAbuse, si apre il browser con URL di progetto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="08952-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="08952-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="08952-123">PassThru</span></span> | <span data-ttu-id="08952-124">Visualizza l'URL; utilizzare con - WhatIf esclusione aprendo il browser.</span><span class="sxs-lookup"><span data-stu-id="08952-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="08952-125">Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.</span><span class="sxs-lookup"><span data-stu-id="08952-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="08952-126">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="08952-126">Common Parameters</span></span>

<span data-ttu-id="08952-127">`Open-PackagePage` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="08952-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="08952-128">Esempi</span><span class="sxs-lookup"><span data-stu-id="08952-128">Examples</span></span>

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