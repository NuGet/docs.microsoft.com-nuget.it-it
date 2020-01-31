---
title: Comando elenco dell'interfaccia della riga di comando NuGet
description: Riferimento per il comando elenco NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813338"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="eb57d-103">comando list (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="eb57d-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="eb57d-104">**Si applica a:** utilizzo del pacchetto, pubblicazione &bullet; **versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="eb57d-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="eb57d-105">Visualizza un elenco di pacchetti da un'origine specificata.</span><span class="sxs-lookup"><span data-stu-id="eb57d-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="eb57d-106">Se non viene specificata alcuna origine, vengono utilizzate tutte le origini definite nel file di configurazione globale, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="eb57d-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="eb57d-107">Se `NuGet.Config` non specifica alcuna origine, `list` usa il feed predefinito (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="eb57d-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="eb57d-108">Usage</span><span class="sxs-lookup"><span data-stu-id="eb57d-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="eb57d-109">dove i termini di ricerca facoltativi filtrano l'elenco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="eb57d-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="eb57d-110">I termini di ricerca vengono applicati ai nomi di pacchetti, tag e descrizioni del pacchetto così come sono quando vengono utilizzati in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="eb57d-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="eb57d-111">Options</span><span class="sxs-lookup"><span data-stu-id="eb57d-111">Options</span></span>

| <span data-ttu-id="eb57d-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="eb57d-112">Option</span></span> | <span data-ttu-id="eb57d-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eb57d-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eb57d-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="eb57d-114">AllVersions</span></span> | <span data-ttu-id="eb57d-115">Elencare tutte le versioni di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="eb57d-115">List all versions of a package.</span></span> <span data-ttu-id="eb57d-116">Per impostazione predefinita, viene visualizzata solo la versione più recente del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="eb57d-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="eb57d-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="eb57d-117">ConfigFile</span></span> | <span data-ttu-id="eb57d-118">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="eb57d-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="eb57d-119">Se non specificato, viene usato `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="eb57d-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="eb57d-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="eb57d-120">ForceEnglishOutput</span></span> | <span data-ttu-id="eb57d-121">*(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese.</span><span class="sxs-lookup"><span data-stu-id="eb57d-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="eb57d-122">Guida di</span><span class="sxs-lookup"><span data-stu-id="eb57d-122">Help</span></span> | <span data-ttu-id="eb57d-123">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="eb57d-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="eb57d-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="eb57d-124">IncludeDelisted</span></span> | <span data-ttu-id="eb57d-125">*(3.2 +)* Visualizza i pacchetti non in elenco.</span><span class="sxs-lookup"><span data-stu-id="eb57d-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="eb57d-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="eb57d-126">NonInteractive</span></span> | <span data-ttu-id="eb57d-127">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="eb57d-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="eb57d-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="eb57d-128">PreRelease</span></span> | <span data-ttu-id="eb57d-129">Include i pacchetti di versioni non definitive nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="eb57d-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="eb57d-130">Source</span><span class="sxs-lookup"><span data-stu-id="eb57d-130">Source</span></span> | <span data-ttu-id="eb57d-131">Specifica un elenco di origini dei pacchetti in cui eseguire la ricerca.</span><span class="sxs-lookup"><span data-stu-id="eb57d-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="eb57d-132">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="eb57d-132">Verbosity</span></span> | <span data-ttu-id="eb57d-133">Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*.</span><span class="sxs-lookup"><span data-stu-id="eb57d-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="eb57d-134">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="eb57d-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="eb57d-135">Esempi</span><span class="sxs-lookup"><span data-stu-id="eb57d-135">Examples</span></span>

<span data-ttu-id="eb57d-136">Elencare tutti i pacchetti dai feed configurati:</span><span class="sxs-lookup"><span data-stu-id="eb57d-136">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="eb57d-137">Elencare i pacchetti correlati ad Azure con dettaglio dettagliato:</span><span class="sxs-lookup"><span data-stu-id="eb57d-137">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="eb57d-138">Elencare tutte le versioni dei pacchetti correlati ad Azure dai feed configurati:</span><span class="sxs-lookup"><span data-stu-id="eb57d-138">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="eb57d-139">Elencare tutte le versioni dei pacchetti correlati a JSON dall'origine/feed specificata:</span><span class="sxs-lookup"><span data-stu-id="eb57d-139">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="eb57d-140">Elencare i pacchetti correlati a JSON da più origini/feed:</span><span class="sxs-lookup"><span data-stu-id="eb57d-140">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

