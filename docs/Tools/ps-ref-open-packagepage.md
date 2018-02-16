---
title: Riferimento di PowerShell di NuGet Open-PackagePage | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando Apri PackagePage PowerShell nella Console di gestione pacchetti NuGet in Visual Studio.
keywords: Console di gestione, i comandi di Powershell di NuGet, riferimenti di NuGet Powershell, aprire PackagePage del pacchetto NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4cc645d9a2779fd6b1b329e9aac4777d50f75d16
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="0fc57-104">Apri-PackagePage (Console di gestione dei pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="0fc57-104">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="0fc57-105">*Deprecato in 3.0 +;) disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="0fc57-105">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="0fc57-106">Avvia il browser predefinito con il progetto, licenza o report abuso URL per il pacchetto specificato.</span><span class="sxs-lookup"><span data-stu-id="0fc57-106">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="0fc57-107">Sintassi</span><span class="sxs-lookup"><span data-stu-id="0fc57-107">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="0fc57-108">Parametri</span><span class="sxs-lookup"><span data-stu-id="0fc57-108">Parameters</span></span>

| <span data-ttu-id="0fc57-109">Parametro</span><span class="sxs-lookup"><span data-stu-id="0fc57-109">Parameter</span></span> | <span data-ttu-id="0fc57-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0fc57-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0fc57-111">Id</span><span class="sxs-lookup"><span data-stu-id="0fc57-111">Id</span></span> | <span data-ttu-id="0fc57-112">L'ID del pacchetto del pacchetto desiderato.</span><span class="sxs-lookup"><span data-stu-id="0fc57-112">The package ID of the desired package.</span></span> <span data-ttu-id="0fc57-113">-Id switch stesso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="0fc57-113">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="0fc57-114">Versione</span><span class="sxs-lookup"><span data-stu-id="0fc57-114">Version</span></span> | <span data-ttu-id="0fc57-115">La versione del pacchetto, verrà utilizzato per la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="0fc57-115">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="0fc57-116">Origine</span><span class="sxs-lookup"><span data-stu-id="0fc57-116">Source</span></span> | <span data-ttu-id="0fc57-117">L'origine del pacchetto, verrà utilizzato per l'origine selezionata nell'elenco a discesa di origine.</span><span class="sxs-lookup"><span data-stu-id="0fc57-117">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="0fc57-118">Licenza</span><span class="sxs-lookup"><span data-stu-id="0fc57-118">License</span></span> | <span data-ttu-id="0fc57-119">Apre il browser all'URL di licenza del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="0fc57-119">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="0fc57-120">Se viene specificato - licenza né - ReportAbuse, si apre il browser con URL di progetto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="0fc57-120">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="0fc57-121">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="0fc57-121">ReportAbuse</span></span> | <span data-ttu-id="0fc57-122">Apre il browser all'URL di evitare eventuali abusi Report del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="0fc57-122">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="0fc57-123">Se viene specificato - licenza né - ReportAbuse, si apre il browser con URL di progetto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="0fc57-123">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="0fc57-124">PassThru</span><span class="sxs-lookup"><span data-stu-id="0fc57-124">PassThru</span></span> | <span data-ttu-id="0fc57-125">Visualizza l'URL; utilizzare con - WhatIf esclusione aprendo il browser.</span><span class="sxs-lookup"><span data-stu-id="0fc57-125">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="0fc57-126">Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.</span><span class="sxs-lookup"><span data-stu-id="0fc57-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="0fc57-127">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="0fc57-127">Common Parameters</span></span>

<span data-ttu-id="0fc57-128">`Open-PackagePage` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="0fc57-128">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="0fc57-129">Esempi</span><span class="sxs-lookup"><span data-stu-id="0fc57-129">Examples</span></span>

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