---
title: Riferimento di PowerShell Get-pacchetto NuGet
description: Riferimento per il comando PowerShell Get-Package nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f4b71fc44e44dcbd5d123a0e2fed63adb79964b5
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818503"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="36c42-103">Get-Package (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="36c42-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="36c42-104">*Questo argomento viene descritto il comando all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows. Per il comando PowerShell Get-Package generico, vedere il [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="36c42-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="36c42-105">Recupera l'elenco di pacchetti installati nell'archivio locale, Elenca i pacchetti disponibili da un'origine del pacchetto quando si utilizza l'opzione - ListAvailable o elenca gli aggiornamenti disponibili quando si utilizza l'opzione-Update.</span><span class="sxs-lookup"><span data-stu-id="36c42-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="36c42-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="36c42-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="36c42-107">Senza parametri, `Get-Package` Visualizza l'elenco dei pacchetti installati nel progetto predefinito.</span><span class="sxs-lookup"><span data-stu-id="36c42-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="36c42-108">Parametri</span><span class="sxs-lookup"><span data-stu-id="36c42-108">Parameters</span></span>

| <span data-ttu-id="36c42-109">Parametro</span><span class="sxs-lookup"><span data-stu-id="36c42-109">Parameter</span></span> | <span data-ttu-id="36c42-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="36c42-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="36c42-111">Origine</span><span class="sxs-lookup"><span data-stu-id="36c42-111">Source</span></span> | <span data-ttu-id="36c42-112">Il percorso URL o una cartella per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="36c42-112">The URL or folder path for the package .</span></span> <span data-ttu-id="36c42-113">I percorsi di cartella locale possono essere assoluto o relativo della cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="36c42-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="36c42-114">Se omesso, `Get-Package` Cerca l'origine pacchetto attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="36c42-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="36c42-115">Quando usato con - ListAvailable, per impostazione predefinita nuget.org.</span><span class="sxs-lookup"><span data-stu-id="36c42-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="36c42-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="36c42-116">ListAvailable</span></span> | <span data-ttu-id="36c42-117">Elenca i pacchetti disponibili da un'origine del pacchetto, verrà utilizzato nuget.org. Mostra il valore predefinito è 50 pacchetti a meno che non vengono specificati - PageSize e/o - First.</span><span class="sxs-lookup"><span data-stu-id="36c42-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="36c42-118">Aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="36c42-118">Updates</span></span> | <span data-ttu-id="36c42-119">Elenca i pacchetti sono disponibile un aggiornamento dall'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="36c42-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="36c42-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="36c42-120">ProjectName</span></span> | <span data-ttu-id="36c42-121">Il progetto da cui recuperare i pacchetti installati.</span><span class="sxs-lookup"><span data-stu-id="36c42-121">The project from which to get installed packages.</span></span> <span data-ttu-id="36c42-122">Se omesso, restituisce installati progetti per l'intera soluzione.</span><span class="sxs-lookup"><span data-stu-id="36c42-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="36c42-123">Filtro</span><span class="sxs-lookup"><span data-stu-id="36c42-123">Filter</span></span> | <span data-ttu-id="36c42-124">Una stringa di filtro utilizzata per limitare l'elenco dei pacchetti viene applicato per l'ID del pacchetto, la descrizione e tag.</span><span class="sxs-lookup"><span data-stu-id="36c42-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="36c42-125">First</span><span class="sxs-lookup"><span data-stu-id="36c42-125">First</span></span> | <span data-ttu-id="36c42-126">Il numero di pacchetti da restituire dall'inizio dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="36c42-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="36c42-127">Se non specificato, per impostazione predefinita a 50.</span><span class="sxs-lookup"><span data-stu-id="36c42-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="36c42-128">Skip</span><span class="sxs-lookup"><span data-stu-id="36c42-128">Skip</span></span> | <span data-ttu-id="36c42-129">Omette il primo &lt;int&gt; pacchetti nell'elenco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="36c42-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="36c42-130">Completaversioni</span><span class="sxs-lookup"><span data-stu-id="36c42-130">AllVersions</span></span> | <span data-ttu-id="36c42-131">Visualizza tutte le versioni disponibili di ogni pacchetto anziché solo la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="36c42-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="36c42-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="36c42-132">IncludePrerelease</span></span> | <span data-ttu-id="36c42-133">Include i pacchetti non definitiva nei risultati.</span><span class="sxs-lookup"><span data-stu-id="36c42-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="36c42-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="36c42-134">PageSize</span></span> | <span data-ttu-id="36c42-135">*(3.0 +)*  Quando usato con - ListAvailable (obbligatorio), il numero di pacchetti per visualizzare l'elenco prima di consegnare un prompt dei comandi per continuare.</span><span class="sxs-lookup"><span data-stu-id="36c42-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="36c42-136">Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.</span><span class="sxs-lookup"><span data-stu-id="36c42-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="36c42-137">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="36c42-137">Common Parameters</span></span>

<span data-ttu-id="36c42-138">`Get-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="36c42-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="36c42-139">Esempi</span><span class="sxs-lookup"><span data-stu-id="36c42-139">Examples</span></span>

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```
