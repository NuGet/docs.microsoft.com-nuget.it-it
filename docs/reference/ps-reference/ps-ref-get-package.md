---
title: Guida di riferimento a NuGet Get-Package PowerShell
description: Informazioni di riferimento per il comando Get-Package PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8394f888ec3d5e57eacd351a4867173da1070ead
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777501"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="4ac60-103">Get-Package (console di gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4ac60-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4ac60-104">*In questo argomento viene descritto il comando nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows. Per il comando generico di Get-Package PowerShell, vedere le informazioni di [riferimento su PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="4ac60-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="4ac60-105">Recupera l'elenco dei pacchetti installati nel repository locale, elenca i pacchetti disponibili da un'origine del pacchetto quando viene usato con l'opzione-ListAvailable oppure elenca gli aggiornamenti disponibili se usati con l'opzione-Update.</span><span class="sxs-lookup"><span data-stu-id="4ac60-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="4ac60-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="4ac60-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="4ac60-107">Senza parametri, `Get-Package` Visualizza l'elenco dei pacchetti installati nel progetto predefinito.</span><span class="sxs-lookup"><span data-stu-id="4ac60-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="4ac60-108">Parametri</span><span class="sxs-lookup"><span data-stu-id="4ac60-108">Parameters</span></span>

| <span data-ttu-id="4ac60-109">Parametro</span><span class="sxs-lookup"><span data-stu-id="4ac60-109">Parameter</span></span> | <span data-ttu-id="4ac60-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4ac60-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4ac60-111">Source (Sorgente)</span><span class="sxs-lookup"><span data-stu-id="4ac60-111">Source</span></span> | <span data-ttu-id="4ac60-112">URL o percorso della cartella per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4ac60-112">The URL or folder path for the package .</span></span> <span data-ttu-id="4ac60-113">I percorsi delle cartelle locali possono essere assoluti o relativi alla cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="4ac60-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="4ac60-114">Se omesso, `Get-Package` Cerca nell'origine del pacchetto attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="4ac60-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="4ac60-115">Se usato con-ListAvailable, il valore predefinito è nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4ac60-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="4ac60-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="4ac60-116">ListAvailable</span></span> | <span data-ttu-id="4ac60-117">Elenca i pacchetti disponibili da un'origine del pacchetto, per impostazione predefinita nuget.org. Mostra un valore predefinito di 50 pacchetti, a meno che non siano specificati-PageSize e/o-First.</span><span class="sxs-lookup"><span data-stu-id="4ac60-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="4ac60-118">Aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="4ac60-118">Updates</span></span> | <span data-ttu-id="4ac60-119">Elenca i pacchetti per i quali è disponibile un aggiornamento dall'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4ac60-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="4ac60-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="4ac60-120">ProjectName</span></span> | <span data-ttu-id="4ac60-121">Progetto da cui ottenere i pacchetti installati.</span><span class="sxs-lookup"><span data-stu-id="4ac60-121">The project from which to get installed packages.</span></span> <span data-ttu-id="4ac60-122">Se omesso, restituisce i progetti installati per l'intera soluzione.</span><span class="sxs-lookup"><span data-stu-id="4ac60-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="4ac60-123">Filtra</span><span class="sxs-lookup"><span data-stu-id="4ac60-123">Filter</span></span> | <span data-ttu-id="4ac60-124">Stringa di filtro utilizzata per restringere l'elenco dei pacchetti mediante l'applicazione dell'ID, della descrizione e dei tag del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4ac60-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="4ac60-125">First (Primo)</span><span class="sxs-lookup"><span data-stu-id="4ac60-125">First</span></span> | <span data-ttu-id="4ac60-126">Numero di pacchetti da restituire dall'inizio dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="4ac60-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="4ac60-127">Se non è specificato, il valore predefinito è 50.</span><span class="sxs-lookup"><span data-stu-id="4ac60-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="4ac60-128">Ignora</span><span class="sxs-lookup"><span data-stu-id="4ac60-128">Skip</span></span> | <span data-ttu-id="4ac60-129">Omette i primi &lt; pacchetti int &gt; dall'elenco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="4ac60-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="4ac60-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="4ac60-130">AllVersions</span></span> | <span data-ttu-id="4ac60-131">Visualizza tutte le versioni disponibili di ogni pacchetto anziché solo la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="4ac60-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="4ac60-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="4ac60-132">IncludePrerelease</span></span> | <span data-ttu-id="4ac60-133">Include i pacchetti di versioni non definitive nei risultati.</span><span class="sxs-lookup"><span data-stu-id="4ac60-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="4ac60-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="4ac60-134">PageSize</span></span> | <span data-ttu-id="4ac60-135">*(3.0 +)* Se usato con-ListAvailable (obbligatorio), il numero di pacchetti da elencare prima di fornire un prompt per continuare.</span><span class="sxs-lookup"><span data-stu-id="4ac60-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="4ac60-136">Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="4ac60-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4ac60-137">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="4ac60-137">Common Parameters</span></span>

<span data-ttu-id="4ac60-138">`Get-Package` supporta i seguenti [parametri comuni di PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="4ac60-138">`Get-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4ac60-139">Esempi</span><span class="sxs-lookup"><span data-stu-id="4ac60-139">Examples</span></span>

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