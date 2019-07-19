---
title: Guida di riferimento a NuGet Find-Package PowerShell
description: Informazioni di riferimento sul comando find-package di PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4bb6d090b97dd55fc1be0625855aab27a0d181c4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327388"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="3c220-103">Find-Package (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3c220-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3c220-104">*Versione 3.0 +; in questo argomento viene descritto il comando nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows. Per il comando Generic PowerShell Find-Package, vedere la Guida di [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="3c220-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="3c220-105">Ottiene il set di pacchetti remoti con ID o parole chiave specificati dall'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="3c220-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="3c220-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="3c220-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="3c220-107">Parametri</span><span class="sxs-lookup"><span data-stu-id="3c220-107">Parameters</span></span>

| <span data-ttu-id="3c220-108">Parametro</span><span class="sxs-lookup"><span data-stu-id="3c220-108">Parameter</span></span> | <span data-ttu-id="3c220-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3c220-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3c220-110">Parole &lt;chiave ID&gt;</span><span class="sxs-lookup"><span data-stu-id="3c220-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="3c220-111">Necessaria Parole chiave da usare durante la ricerca nell'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="3c220-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="3c220-112">Usare-ExactMatch per restituire solo i pacchetti il cui ID pacchetto corrisponde alle parole chiave.</span><span class="sxs-lookup"><span data-stu-id="3c220-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="3c220-113">Se non viene specificata alcuna parola `Find-Package` chiave, restituisce un elenco dei primi 20 pacchetti per download o il numero specificato da-First.</span><span class="sxs-lookup"><span data-stu-id="3c220-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="3c220-114">Si noti che-ID è facoltativo e un no-op.</span><span class="sxs-lookup"><span data-stu-id="3c220-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="3c220-115">Source</span><span class="sxs-lookup"><span data-stu-id="3c220-115">Source</span></span> | <span data-ttu-id="3c220-116">URL o percorso della cartella per l'origine del pacchetto da cercare.</span><span class="sxs-lookup"><span data-stu-id="3c220-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="3c220-117">I percorsi delle cartelle locali possono essere assoluti o relativi alla cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="3c220-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="3c220-118">Se omesso, `Find-Package` Cerca nell'origine del pacchetto attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="3c220-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="3c220-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="3c220-119">AllVersions</span></span> | <span data-ttu-id="3c220-120">Visualizza tutte le versioni disponibili di ogni pacchetto anziché solo la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="3c220-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="3c220-121">Primo</span><span class="sxs-lookup"><span data-stu-id="3c220-121">First</span></span> | <span data-ttu-id="3c220-122">Numero di pacchetti da restituire dall'inizio dell'elenco; il valore predefinito è 20.</span><span class="sxs-lookup"><span data-stu-id="3c220-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="3c220-123">Skip</span><span class="sxs-lookup"><span data-stu-id="3c220-123">Skip</span></span> | <span data-ttu-id="3c220-124">Omette i primi &lt;pacchetti int&gt; dall'elenco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="3c220-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="3c220-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="3c220-125">IncludePrerelease</span></span> | <span data-ttu-id="3c220-126">Include i pacchetti di versioni non definitive nei risultati.</span><span class="sxs-lookup"><span data-stu-id="3c220-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="3c220-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="3c220-127">ExactMatch</span></span> | <span data-ttu-id="3c220-128">Specificato per usare &lt;parole&gt; chiave come ID pacchetto con distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="3c220-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="3c220-129">Cominciamo</span><span class="sxs-lookup"><span data-stu-id="3c220-129">StartWith</span></span> | <span data-ttu-id="3c220-130">Restituisce i pacchetti il cui ID di &lt;pacchetto&gt;inizia con parole chiave.</span><span class="sxs-lookup"><span data-stu-id="3c220-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="3c220-131">Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.</span><span class="sxs-lookup"><span data-stu-id="3c220-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3c220-132">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="3c220-132">Common Parameters</span></span>

<span data-ttu-id="3c220-133">`Find-Package`supporta i seguenti [parametri comuni di PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3c220-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3c220-134">Esempi</span><span class="sxs-lookup"><span data-stu-id="3c220-134">Examples</span></span>

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
