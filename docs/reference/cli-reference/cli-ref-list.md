---
title: Comando elenco dell'interfaccia della riga di comando NuGet
description: Riferimento per il comando elenco NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327738"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="fe1d3-103">comando list (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="fe1d3-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="fe1d3-104">**Si applica a:** utilizzo del pacchetto &bullet; , pubblicazione delle **versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="fe1d3-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="fe1d3-105">Visualizza un elenco di pacchetti da un'origine specificata.</span><span class="sxs-lookup"><span data-stu-id="fe1d3-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="fe1d3-106">Se non viene specificata alcuna origine, vengono utilizzate tutte le origini definite nel file `%AppData%\NuGet\NuGet.Config` di configurazione globale ( `~/.nuget/NuGet/NuGet.Config`Windows) o.</span><span class="sxs-lookup"><span data-stu-id="fe1d3-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="fe1d3-107">Se `NuGet.Config` non specifica alcuna origine `list` , usa il feed predefinito (NuGet.org).</span><span class="sxs-lookup"><span data-stu-id="fe1d3-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="fe1d3-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="fe1d3-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="fe1d3-109">dove i termini di ricerca facoltativi filtrano l'elenco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="fe1d3-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="fe1d3-110">I termini di ricerca vengono applicati ai nomi di pacchetti, tag e descrizioni del pacchetto così come sono quando vengono utilizzati in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="fe1d3-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="fe1d3-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="fe1d3-111">Options</span></span>

| <span data-ttu-id="fe1d3-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="fe1d3-112">Option</span></span> | <span data-ttu-id="fe1d3-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe1d3-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fe1d3-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="fe1d3-114">AllVersions</span></span> | <span data-ttu-id="fe1d3-115">Elencare tutte le versioni di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fe1d3-115">List all versions of a package.</span></span> <span data-ttu-id="fe1d3-116">Per impostazione predefinita, viene visualizzata solo la versione più recente del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fe1d3-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="fe1d3-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fe1d3-117">ConfigFile</span></span> | <span data-ttu-id="fe1d3-118">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="fe1d3-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fe1d3-119">Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="fe1d3-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="fe1d3-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fe1d3-120">ForceEnglishOutput</span></span> | <span data-ttu-id="fe1d3-121">*(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese.</span><span class="sxs-lookup"><span data-stu-id="fe1d3-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fe1d3-122">Help</span><span class="sxs-lookup"><span data-stu-id="fe1d3-122">Help</span></span> | <span data-ttu-id="fe1d3-123">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="fe1d3-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="fe1d3-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="fe1d3-124">IncludeDelisted</span></span> | <span data-ttu-id="fe1d3-125">*(3.2 +)* Visualizza i pacchetti non in elenco.</span><span class="sxs-lookup"><span data-stu-id="fe1d3-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="fe1d3-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="fe1d3-126">NonInteractive</span></span> | <span data-ttu-id="fe1d3-127">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="fe1d3-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fe1d3-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="fe1d3-128">PreRelease</span></span> | <span data-ttu-id="fe1d3-129">Include i pacchetti di versioni non definitive nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="fe1d3-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="fe1d3-130">Source</span><span class="sxs-lookup"><span data-stu-id="fe1d3-130">Source</span></span> | <span data-ttu-id="fe1d3-131">Specifica un elenco di origini dei pacchetti in cui eseguire la ricerca.</span><span class="sxs-lookup"><span data-stu-id="fe1d3-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="fe1d3-132">Verbosity</span><span class="sxs-lookup"><span data-stu-id="fe1d3-132">Verbosity</span></span> | <span data-ttu-id="fe1d3-133">Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*.</span><span class="sxs-lookup"><span data-stu-id="fe1d3-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="fe1d3-134">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fe1d3-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fe1d3-135">Esempi</span><span class="sxs-lookup"><span data-stu-id="fe1d3-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
