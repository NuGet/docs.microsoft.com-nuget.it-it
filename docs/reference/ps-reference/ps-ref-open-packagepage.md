---
title: Guida di riferimento a NuGet Open-PackagePage PowerShell
description: Informazioni di riferimento per il comando Open-PackagePage PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d34a91007197f8004e4923deedb1cdb26d662d53
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780403"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="a3a21-103">Open-PackagePage (console di gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="a3a21-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a3a21-104">*Deprecato in 3.0 +; disponibile solo nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="a3a21-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="a3a21-105">Avvia il browser predefinito con l'URL del progetto, della licenza o dell'abuso del report per il pacchetto specificato.</span><span class="sxs-lookup"><span data-stu-id="a3a21-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="a3a21-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="a3a21-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a3a21-107">Parametri</span><span class="sxs-lookup"><span data-stu-id="a3a21-107">Parameters</span></span>

| <span data-ttu-id="a3a21-108">Parametro</span><span class="sxs-lookup"><span data-stu-id="a3a21-108">Parameter</span></span> | <span data-ttu-id="a3a21-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a3a21-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a3a21-110">Id</span><span class="sxs-lookup"><span data-stu-id="a3a21-110">Id</span></span> | <span data-ttu-id="a3a21-111">ID del pacchetto desiderato.</span><span class="sxs-lookup"><span data-stu-id="a3a21-111">The package ID of the desired package.</span></span> <span data-ttu-id="a3a21-112">L'opzione-ID è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="a3a21-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="a3a21-113">Versione</span><span class="sxs-lookup"><span data-stu-id="a3a21-113">Version</span></span> | <span data-ttu-id="a3a21-114">Versione del pacchetto, per impostazione predefinita la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="a3a21-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="a3a21-115">Source (Sorgente)</span><span class="sxs-lookup"><span data-stu-id="a3a21-115">Source</span></span> | <span data-ttu-id="a3a21-116">Origine del pacchetto, per impostazione predefinita l'origine selezionata nell'elenco a discesa origine.</span><span class="sxs-lookup"><span data-stu-id="a3a21-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="a3a21-117">Licenza</span><span class="sxs-lookup"><span data-stu-id="a3a21-117">License</span></span> | <span data-ttu-id="a3a21-118">Apre il browser all'URL di licenza del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a3a21-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="a3a21-119">Se non si specifica né-License né-ReportAbuse, il browser apre l'URL del progetto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a3a21-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="a3a21-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="a3a21-120">ReportAbuse</span></span> | <span data-ttu-id="a3a21-121">Apre il browser all'URL di utilizzo del report del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a3a21-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="a3a21-122">Se non si specifica né-License né-ReportAbuse, il browser apre l'URL del progetto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a3a21-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="a3a21-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="a3a21-123">PassThru</span></span> | <span data-ttu-id="a3a21-124">Visualizza l'URL. usare con-WhatIf per non visualizzare l'apertura del browser.</span><span class="sxs-lookup"><span data-stu-id="a3a21-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="a3a21-125">Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="a3a21-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a3a21-126">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="a3a21-126">Common Parameters</span></span>

<span data-ttu-id="a3a21-127">`Open-PackagePage` supporta i seguenti [parametri comuni di PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="a3a21-127">`Open-PackagePage` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a3a21-128">Esempi</span><span class="sxs-lookup"><span data-stu-id="a3a21-128">Examples</span></span>

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