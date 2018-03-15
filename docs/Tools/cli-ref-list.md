---
title: Comando di NuGet CLI elenco | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando di elenco di nuget.exe
keywords: riferimento elenco NuGet, comando elenco di pacchetti
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7e0945b9e64a15a839f62bde0a0ef8f3d83335d4
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/15/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="dde7f-104">comando di elenco (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="dde7f-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="dde7f-105">**Si applica a:** il consumo di pacchetti, pubblicazione &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="dde7f-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="dde7f-106">Visualizza un elenco di pacchetti da un'origine specificata.</span><span class="sxs-lookup"><span data-stu-id="dde7f-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="dde7f-107">Se non vengono specificata alcuna origine, tutte le origini definito nel file di configurazione globale, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config`, vengono utilizzati.</span><span class="sxs-lookup"><span data-stu-id="dde7f-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="dde7f-108">Se `NuGet.Config` non specifica nessuna origine, quindi `list` Usa il feed predefinito (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="dde7f-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="dde7f-109">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="dde7f-109">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="dde7f-110">in termini di ricerca facoltativo verranno filtrato l'elenco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="dde7f-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="dde7f-111">I termini di ricerca vengono applicati ai nomi dei pacchetti, tag e le descrizioni di pacchetto, esattamente come quando il loro utilizzo su nuget.org.</span><span class="sxs-lookup"><span data-stu-id="dde7f-111">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="dde7f-112">Opzioni</span><span class="sxs-lookup"><span data-stu-id="dde7f-112">Options</span></span>

| <span data-ttu-id="dde7f-113">Opzione</span><span class="sxs-lookup"><span data-stu-id="dde7f-113">Option</span></span> | <span data-ttu-id="dde7f-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dde7f-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dde7f-115">Completaversioni</span><span class="sxs-lookup"><span data-stu-id="dde7f-115">AllVersions</span></span> | <span data-ttu-id="dde7f-116">Elencare tutte le versioni di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="dde7f-116">List all versions of a package.</span></span> <span data-ttu-id="dde7f-117">Per impostazione predefinita, viene visualizzata solo la versione più recente del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="dde7f-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="dde7f-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="dde7f-118">ConfigFile</span></span> | <span data-ttu-id="dde7f-119">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="dde7f-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="dde7f-120">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="dde7f-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="dde7f-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="dde7f-121">ForceEnglishOutput</span></span> | <span data-ttu-id="dde7f-122">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="dde7f-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="dde7f-123">?</span><span class="sxs-lookup"><span data-stu-id="dde7f-123">Help</span></span> | <span data-ttu-id="dde7f-124">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="dde7f-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="dde7f-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="dde7f-125">IncludeDelisted</span></span> | <span data-ttu-id="dde7f-126">*(3.2 +)*  Visualizzare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="dde7f-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="dde7f-127">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="dde7f-127">NonInteractive</span></span> | <span data-ttu-id="dde7f-128">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="dde7f-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="dde7f-129">Versione provvisoria</span><span class="sxs-lookup"><span data-stu-id="dde7f-129">PreRelease</span></span> | <span data-ttu-id="dde7f-130">Include pacchetti della versione provvisoria, nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="dde7f-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="dde7f-131">Origine</span><span class="sxs-lookup"><span data-stu-id="dde7f-131">Source</span></span> | <span data-ttu-id="dde7f-132">Specifica un elenco di origini dei pacchetti per la ricerca.</span><span class="sxs-lookup"><span data-stu-id="dde7f-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="dde7f-133">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="dde7f-133">Verbosity</span></span> | <span data-ttu-id="dde7f-134">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="dde7f-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="dde7f-135">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="dde7f-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="dde7f-136">Esempi</span><span class="sxs-lookup"><span data-stu-id="dde7f-136">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
