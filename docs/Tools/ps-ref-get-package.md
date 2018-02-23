---
title: Riferimento di PowerShell Get-pacchetto NuGet | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando PowerShell Get-Package nella Console di gestione pacchetti NuGet in Visual Studio.
keywords: Creare un pacchetto NuGet console di gestione, i comandi di Powershell di NuGet, riferimento di Powershell di NuGet, Get-Package
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 01a874ce9ae59dcaeb696a45f23cc5e9f2cfa251
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="d78a9-104">Get-pacchetto (Package Manager Console in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d78a9-104">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d78a9-105">*Questo argomento viene descritto il comando all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows. Per il comando PowerShell Get-Package generico, vedere il [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="d78a9-105">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="d78a9-106">Recupera l'elenco di pacchetti installati nell'archivio locale, Elenca i pacchetti disponibili da un'origine del pacchetto quando si utilizza l'opzione - ListAvailable o elenca gli aggiornamenti disponibili quando si utilizza l'opzione-Update.</span><span class="sxs-lookup"><span data-stu-id="d78a9-106">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="d78a9-107">Sintassi</span><span class="sxs-lookup"><span data-stu-id="d78a9-107">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="d78a9-108">Senza parametri, `Get-Package` Visualizza l'elenco dei pacchetti installati nel progetto predefinito.</span><span class="sxs-lookup"><span data-stu-id="d78a9-108">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="d78a9-109">Parametri</span><span class="sxs-lookup"><span data-stu-id="d78a9-109">Parameters</span></span>

| <span data-ttu-id="d78a9-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="d78a9-110">Parameter</span></span> | <span data-ttu-id="d78a9-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d78a9-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d78a9-112">Origine</span><span class="sxs-lookup"><span data-stu-id="d78a9-112">Source</span></span> | <span data-ttu-id="d78a9-113">Il percorso URL o una cartella per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d78a9-113">The URL or folder path for the package .</span></span> <span data-ttu-id="d78a9-114">I percorsi di cartella locale possono essere assoluto o relativo della cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="d78a9-114">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="d78a9-115">Se omesso, `Get-Package` Cerca l'origine pacchetto attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="d78a9-115">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="d78a9-116">Quando usato con - ListAvailable, per impostazione predefinita nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d78a9-116">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="d78a9-117">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="d78a9-117">ListAvailable</span></span> | <span data-ttu-id="d78a9-118">Elenca i pacchetti disponibili da un'origine del pacchetto, verrà utilizzato nuget.org. Mostra il valore predefinito è 50 pacchetti a meno che non vengono specificati - PageSize e/o - First.</span><span class="sxs-lookup"><span data-stu-id="d78a9-118">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="d78a9-119">Aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="d78a9-119">Updates</span></span> | <span data-ttu-id="d78a9-120">Elenca i pacchetti sono disponibile un aggiornamento dall'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d78a9-120">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="d78a9-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="d78a9-121">ProjectName</span></span> | <span data-ttu-id="d78a9-122">Il progetto da cui recuperare i pacchetti installati.</span><span class="sxs-lookup"><span data-stu-id="d78a9-122">The project from which to get installed packages.</span></span> <span data-ttu-id="d78a9-123">Se omesso, restituisce installati progetti per l'intera soluzione.</span><span class="sxs-lookup"><span data-stu-id="d78a9-123">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="d78a9-124">Filtro</span><span class="sxs-lookup"><span data-stu-id="d78a9-124">Filter</span></span> | <span data-ttu-id="d78a9-125">Una stringa di filtro utilizzata per limitare l'elenco dei pacchetti viene applicato per l'ID del pacchetto, la descrizione e tag.</span><span class="sxs-lookup"><span data-stu-id="d78a9-125">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="d78a9-126">First</span><span class="sxs-lookup"><span data-stu-id="d78a9-126">First</span></span> | <span data-ttu-id="d78a9-127">Il numero di pacchetti da restituire dall'inizio dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="d78a9-127">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="d78a9-128">Se non specificato, per impostazione predefinita a 50.</span><span class="sxs-lookup"><span data-stu-id="d78a9-128">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="d78a9-129">Skip</span><span class="sxs-lookup"><span data-stu-id="d78a9-129">Skip</span></span> | <span data-ttu-id="d78a9-130">Omette il primo &lt;int&gt; pacchetti nell'elenco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="d78a9-130">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="d78a9-131">Completaversioni</span><span class="sxs-lookup"><span data-stu-id="d78a9-131">AllVersions</span></span> | <span data-ttu-id="d78a9-132">Visualizza tutte le versioni disponibili di ogni pacchetto anziché solo la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="d78a9-132">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="d78a9-133">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="d78a9-133">IncludePrerelease</span></span> | <span data-ttu-id="d78a9-134">Include i pacchetti non definitiva nei risultati.</span><span class="sxs-lookup"><span data-stu-id="d78a9-134">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="d78a9-135">PageSize</span><span class="sxs-lookup"><span data-stu-id="d78a9-135">PageSize</span></span> | <span data-ttu-id="d78a9-136">*(3.0 +)*  Quando usato con - ListAvailable (obbligatorio), il numero di pacchetti per visualizzare l'elenco prima di consegnare un prompt dei comandi per continuare.</span><span class="sxs-lookup"><span data-stu-id="d78a9-136">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="d78a9-137">Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.</span><span class="sxs-lookup"><span data-stu-id="d78a9-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d78a9-138">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="d78a9-138">Common Parameters</span></span>

<span data-ttu-id="d78a9-139">`Get-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d78a9-139">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d78a9-140">Esempi</span><span class="sxs-lookup"><span data-stu-id="d78a9-140">Examples</span></span>

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
