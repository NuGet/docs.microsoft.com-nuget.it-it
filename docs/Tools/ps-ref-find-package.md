---
title: Riferimento di PowerShell di NuGet. Find-Package | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 2f7b8847-8259-4366-98c0-13cab88d6e1b
description: Riferimento per il comando di PowerShell di Find-Package nella Console di gestione pacchetti NuGet in Visual Studio.
keywords: Creare un pacchetto NuGet console di gestione, i comandi di Powershell di NuGet, riferimento di Powershell di NuGet, Find-Package
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fb55cc71e0d4b8eee28b232e64d2cc42364fc153
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="9cbba-104">Find-Package (Package Manager Console in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="9cbba-104">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="9cbba-105">*Versione 3.0; questo argomento viene descritto il comando all'interno di [Console di gestione pacchetti NuGet](Package-Manager-Console.md) in Visual Studio in Windows. Per il comando di PowerShell. Find-Package generico, vedere il [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="9cbba-105">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="9cbba-106">Ottiene il set di pacchetti remoti con parole chiave o un ID specificato dall'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9cbba-106">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="9cbba-107">Sintassi</span><span class="sxs-lookup"><span data-stu-id="9cbba-107">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="9cbba-108">Parametri</span><span class="sxs-lookup"><span data-stu-id="9cbba-108">Parameters</span></span>

| <span data-ttu-id="9cbba-109">Parametro</span><span class="sxs-lookup"><span data-stu-id="9cbba-109">Parameter</span></span> | <span data-ttu-id="9cbba-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9cbba-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9cbba-111">ID &lt;parole chiave&gt;</span><span class="sxs-lookup"><span data-stu-id="9cbba-111">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="9cbba-112">(Obbligatorio) Parole chiave per la ricerca dell'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9cbba-112">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="9cbba-113">Utilizzare - ExactMatch per restituire solo i pacchetti il cui ID di pacchetto consente di ricercare le parole chiave.</span><span class="sxs-lookup"><span data-stu-id="9cbba-113">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="9cbba-114">Se nessuna parola chiave vengono specificata, `Find-Package` restituisce un elenco dei pacchetti primi 20 tramite download o il numero specificato da - prima.</span><span class="sxs-lookup"><span data-stu-id="9cbba-114">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="9cbba-115">Si noti che - Id è facoltativo e nessuna operazione.</span><span class="sxs-lookup"><span data-stu-id="9cbba-115">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="9cbba-116">Origine</span><span class="sxs-lookup"><span data-stu-id="9cbba-116">Source</span></span> | <span data-ttu-id="9cbba-117">Il percorso URL o una cartella per l'origine del pacchetto da cercare.</span><span class="sxs-lookup"><span data-stu-id="9cbba-117">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="9cbba-118">I percorsi di cartella locale possono essere assoluto o relativo della cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="9cbba-118">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="9cbba-119">Se omesso, `Find-Package` Cerca l'origine pacchetto attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="9cbba-119">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="9cbba-120">Completaversioni</span><span class="sxs-lookup"><span data-stu-id="9cbba-120">AllVersions</span></span> | <span data-ttu-id="9cbba-121">Visualizza tutte le versioni disponibili di ogni pacchetto anziché solo la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="9cbba-121">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="9cbba-122">First</span><span class="sxs-lookup"><span data-stu-id="9cbba-122">First</span></span> | <span data-ttu-id="9cbba-123">Il numero di pacchetti da restituire dall'inizio dell'elenco. il valore predefinito è 20.</span><span class="sxs-lookup"><span data-stu-id="9cbba-123">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="9cbba-124">Skip</span><span class="sxs-lookup"><span data-stu-id="9cbba-124">Skip</span></span> | <span data-ttu-id="9cbba-125">Omette il primo &lt;int&gt; pacchetti nell'elenco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="9cbba-125">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="9cbba-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="9cbba-126">IncludePrerelease</span></span> | <span data-ttu-id="9cbba-127">Include i pacchetti non definitiva nei risultati.</span><span class="sxs-lookup"><span data-stu-id="9cbba-127">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="9cbba-128">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="9cbba-128">ExactMatch</span></span> | <span data-ttu-id="9cbba-129">Specificato da utilizzare &lt;parole chiave&gt; come un ID pacchetto tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="9cbba-129">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="9cbba-130">StartWith</span><span class="sxs-lookup"><span data-stu-id="9cbba-130">StartWith</span></span> | <span data-ttu-id="9cbba-131">Restituisce pacchetti con pacchetto ID inizia con &lt;parole chiave&gt;.</span><span class="sxs-lookup"><span data-stu-id="9cbba-131">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="9cbba-132">Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.</span><span class="sxs-lookup"><span data-stu-id="9cbba-132">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="9cbba-133">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="9cbba-133">Common Parameters</span></span>

<span data-ttu-id="9cbba-134">`Find-Package`supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9cbba-134">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="9cbba-135">Esempi</span><span class="sxs-lookup"><span data-stu-id="9cbba-135">Examples</span></span>

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
