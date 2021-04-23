---
title: Informazioni di riferimento Find-Package PowerShell per NuGet
description: Informazioni di Find-Package comando di PowerShell nella console Gestione pacchetti NuGet in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 263835da64340a13737b32ab54ab057cb640a080
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901759"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="27539-103">Find-Package (Gestione pacchetti Console in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="27539-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="27539-104">*Versione 3.0+; Questo argomento descrive il comando all'interno [della console Gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows. Per il comando di gestione Find-Package PowerShell generico, vedere le informazioni di [riferimento su PackageManagement di PowerShell.](/powershell/module/packagemanagement)*</span><span class="sxs-lookup"><span data-stu-id="27539-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="27539-105">Ottiene il set di pacchetti remoti con l'ID o le parole chiave specificati dall'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="27539-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="27539-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="27539-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="27539-107">Parametri</span><span class="sxs-lookup"><span data-stu-id="27539-107">Parameters</span></span>

| <span data-ttu-id="27539-108">Parametro</span><span class="sxs-lookup"><span data-stu-id="27539-108">Parameter</span></span> | <span data-ttu-id="27539-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="27539-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="27539-110">Parole chiave &lt; id&gt;</span><span class="sxs-lookup"><span data-stu-id="27539-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="27539-111">(Obbligatorio) Parole chiave da usare durante la ricerca nell'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="27539-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="27539-112">Usare -ExactMatch per restituire solo i pacchetti il cui ID pacchetto corrisponde alle parole chiave .</span><span class="sxs-lookup"><span data-stu-id="27539-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="27539-113">Se non viene specificata alcuna parola chiave, restituisce un elenco dei primi 20 pacchetti per download o il `Find-Package` numero specificato da -First.</span><span class="sxs-lookup"><span data-stu-id="27539-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="27539-114">Si noti che -Id è facoltativo e non operativo.</span><span class="sxs-lookup"><span data-stu-id="27539-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="27539-115">Source (Sorgente)</span><span class="sxs-lookup"><span data-stu-id="27539-115">Source</span></span> | <span data-ttu-id="27539-116">URL o percorso della cartella per l'origine del pacchetto in cui eseguire la ricerca.</span><span class="sxs-lookup"><span data-stu-id="27539-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="27539-117">I percorsi delle cartelle locali possono essere assoluti o relativi alla cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="27539-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="27539-118">Se omesso, `Find-Package` cerca l'origine del pacchetto attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="27539-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="27539-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="27539-119">AllVersions</span></span> | <span data-ttu-id="27539-120">Visualizza tutte le versioni disponibili di ogni pacchetto anziché solo la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="27539-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="27539-121">First (Primo)</span><span class="sxs-lookup"><span data-stu-id="27539-121">First</span></span> | <span data-ttu-id="27539-122">Numero di pacchetti da restituire dall'inizio dell'elenco. il valore predefinito è 20.</span><span class="sxs-lookup"><span data-stu-id="27539-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="27539-123">Ignora</span><span class="sxs-lookup"><span data-stu-id="27539-123">Skip</span></span> | <span data-ttu-id="27539-124">Omette i primi &lt; pacchetti int &gt; dall'elenco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="27539-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="27539-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="27539-125">IncludePrerelease</span></span> | <span data-ttu-id="27539-126">Include i pacchetti in versione non definitiva nei risultati.</span><span class="sxs-lookup"><span data-stu-id="27539-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="27539-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="27539-127">ExactMatch</span></span> | <span data-ttu-id="27539-128">Specificato per usare parole &lt; chiave come ID pacchetto con &gt; distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="27539-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="27539-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="27539-129">StartWith</span></span> | <span data-ttu-id="27539-130">Restituisce i pacchetti il cui ID pacchetto inizia con le &lt; parole chiave &gt; .</span><span class="sxs-lookup"><span data-stu-id="27539-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="27539-131">Nessuno di questi parametri accetta l'input della pipeline o i caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="27539-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="27539-132">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="27539-132">Common Parameters</span></span>

<span data-ttu-id="27539-133">`Find-Package` supporta i parametri comuni di [PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters)seguenti: Debug, Azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="27539-133">`Find-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="27539-134">Esempi</span><span class="sxs-lookup"><span data-stu-id="27539-134">Examples</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```