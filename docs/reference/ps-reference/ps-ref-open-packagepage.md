---
title: Riferimenti per PowerShell open-PackagePage NuGet
description: Informazioni di riferimento sul comando di PowerShell open-PackagePage nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 39199ebfc37756ed40158a1c07afca7709067350
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384428"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="f1ce8-103">Open-PackagePage (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f1ce8-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f1ce8-104">*Deprecato in 3.0 +; disponibile solo nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="f1ce8-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f1ce8-105">Avvia il browser predefinito con l'URL del progetto, della licenza o dell'abuso del report per il pacchetto specificato.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="f1ce8-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="f1ce8-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f1ce8-107">Parametri</span><span class="sxs-lookup"><span data-stu-id="f1ce8-107">Parameters</span></span>

| <span data-ttu-id="f1ce8-108">Parametro</span><span class="sxs-lookup"><span data-stu-id="f1ce8-108">Parameter</span></span> | <span data-ttu-id="f1ce8-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f1ce8-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f1ce8-110">Id</span><span class="sxs-lookup"><span data-stu-id="f1ce8-110">Id</span></span> | <span data-ttu-id="f1ce8-111">ID del pacchetto desiderato.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-111">The package ID of the desired package.</span></span> <span data-ttu-id="f1ce8-112">L'opzione-ID è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="f1ce8-113">Versione</span><span class="sxs-lookup"><span data-stu-id="f1ce8-113">Version</span></span> | <span data-ttu-id="f1ce8-114">Versione del pacchetto, per impostazione predefinita la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="f1ce8-115">Source</span><span class="sxs-lookup"><span data-stu-id="f1ce8-115">Source</span></span> | <span data-ttu-id="f1ce8-116">Origine del pacchetto, per impostazione predefinita l'origine selezionata nell'elenco a discesa origine.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="f1ce8-117">Licenza</span><span class="sxs-lookup"><span data-stu-id="f1ce8-117">License</span></span> | <span data-ttu-id="f1ce8-118">Apre il browser all'URL di licenza del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="f1ce8-119">Se non si specifica né-License né-ReportAbuse, il browser apre l'URL del progetto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="f1ce8-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="f1ce8-120">ReportAbuse</span></span> | <span data-ttu-id="f1ce8-121">Apre il browser all'URL di utilizzo del report del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="f1ce8-122">Se non si specifica né-License né-ReportAbuse, il browser apre l'URL del progetto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="f1ce8-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="f1ce8-123">PassThru</span></span> | <span data-ttu-id="f1ce8-124">Visualizza l'URL. usare con-WhatIf per non visualizzare l'apertura del browser.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="f1ce8-125">Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f1ce8-126">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="f1ce8-126">Common Parameters</span></span>

<span data-ttu-id="f1ce8-127">`Open-PackagePage` supporta i [parametri di PowerShell comuni](https://go.microsoft.com/fwlink/?LinkID=113216)seguenti: debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-127">`Open-PackagePage` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f1ce8-128">Esempi</span><span class="sxs-lookup"><span data-stu-id="f1ce8-128">Examples</span></span>

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