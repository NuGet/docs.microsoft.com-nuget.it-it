---
title: Riferimento di PowerShell Get-pacchetto NuGet
description: Informazioni di riferimento per il comando PowerShell Get-Package nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d0d25cb6e21f6d0d42389e08340b6f1e1baf8a64
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842509"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="a7b20-103">Get-Package (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="a7b20-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a7b20-104">*In questo argomento descrive il comando all'interno di [Console di gestione pacchetti](package-manager-console.md) in Visual Studio in Windows. Per il comando PowerShell Get-Package generico, vedere la [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="a7b20-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="a7b20-105">Recupera l'elenco dei pacchetti installati nel repository locale, sono elencati i pacchetti disponibili da un'origine del pacchetto quando usato con l'opzione - ListAvailable o elenca gli aggiornamenti disponibili quando usato con l'opzione-Update.</span><span class="sxs-lookup"><span data-stu-id="a7b20-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="a7b20-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="a7b20-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="a7b20-107">Senza parametri, `Get-Package` consente di visualizzare l'elenco dei pacchetti installati nel progetto predefinito.</span><span class="sxs-lookup"><span data-stu-id="a7b20-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="a7b20-108">Parametri</span><span class="sxs-lookup"><span data-stu-id="a7b20-108">Parameters</span></span>

| <span data-ttu-id="a7b20-109">Parametro</span><span class="sxs-lookup"><span data-stu-id="a7b20-109">Parameter</span></span> | <span data-ttu-id="a7b20-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7b20-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a7b20-111">`Source`</span><span class="sxs-lookup"><span data-stu-id="a7b20-111">Source</span></span> | <span data-ttu-id="a7b20-112">Il percorso URL o una cartella per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a7b20-112">The URL or folder path for the package .</span></span> <span data-ttu-id="a7b20-113">I percorsi di cartella locale possono essere assoluto o relativo rispetto alla cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="a7b20-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="a7b20-114">Se omesso, `Get-Package` Cerca l'origine del pacchetto attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="a7b20-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="a7b20-115">Quando usato con - ListAvailable, per impostazione predefinita in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a7b20-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="a7b20-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="a7b20-116">ListAvailable</span></span> | <span data-ttu-id="a7b20-117">Elenca i pacchetti disponibili da un'origine del pacchetto, verrà utilizzato in nuget.org. Mostra un valore predefinito di 50 pacchetti a meno che non vengono specificati - PageSize e/o - First.</span><span class="sxs-lookup"><span data-stu-id="a7b20-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="a7b20-118">Aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="a7b20-118">Updates</span></span> | <span data-ttu-id="a7b20-119">Elenca i pacchetti che hanno un aggiornamento disponibile dall'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a7b20-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="a7b20-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="a7b20-120">ProjectName</span></span> | <span data-ttu-id="a7b20-121">Il progetto da cui ottenere i pacchetti installati.</span><span class="sxs-lookup"><span data-stu-id="a7b20-121">The project from which to get installed packages.</span></span> <span data-ttu-id="a7b20-122">Se omesso, restituisce installati progetti per l'intera soluzione.</span><span class="sxs-lookup"><span data-stu-id="a7b20-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="a7b20-123">Filtro</span><span class="sxs-lookup"><span data-stu-id="a7b20-123">Filter</span></span> | <span data-ttu-id="a7b20-124">Una stringa di filtro utilizzata per limitare l'elenco dei pacchetti viene applicato per l'ID del pacchetto, la descrizione e tag.</span><span class="sxs-lookup"><span data-stu-id="a7b20-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="a7b20-125">Primo</span><span class="sxs-lookup"><span data-stu-id="a7b20-125">First</span></span> | <span data-ttu-id="a7b20-126">Il numero di pacchetti da restituire dall'inizio dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="a7b20-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="a7b20-127">Se non specificato, valore predefinito è 50.</span><span class="sxs-lookup"><span data-stu-id="a7b20-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="a7b20-128">Skip</span><span class="sxs-lookup"><span data-stu-id="a7b20-128">Skip</span></span> | <span data-ttu-id="a7b20-129">Omette il primo &lt;int&gt; pacchetti nell'elenco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="a7b20-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="a7b20-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="a7b20-130">AllVersions</span></span> | <span data-ttu-id="a7b20-131">Consente di visualizzare tutte le versioni disponibili di ogni pacchetto invece solo la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="a7b20-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="a7b20-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="a7b20-132">IncludePrerelease</span></span> | <span data-ttu-id="a7b20-133">Include pacchetti versione non definitivo nei risultati.</span><span class="sxs-lookup"><span data-stu-id="a7b20-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="a7b20-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="a7b20-134">PageSize</span></span> | <span data-ttu-id="a7b20-135">*(3.0 e versioni successive)*  Quando utilizzato con - ListAvailable (obbligatorio), il numero di pacchetti per ottenere l'elenco prima di fornire un prompt dei comandi per continuare.</span><span class="sxs-lookup"><span data-stu-id="a7b20-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="a7b20-136">Nessuno di questi parametri accettano caratteri jolly o input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="a7b20-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a7b20-137">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="a7b20-137">Common Parameters</span></span>

<span data-ttu-id="a7b20-138">`Get-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="a7b20-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a7b20-139">Esempi</span><span class="sxs-lookup"><span data-stu-id="a7b20-139">Examples</span></span>

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
