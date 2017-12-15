---
title: Comando di NuGet CLI elenco | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: Riferimento per il comando di elenco di nuget.exe
keywords: riferimento elenco NuGet, comando elenco di pacchetti
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="81ca4-104">comando di elenco (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="81ca4-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="81ca4-105">**Si applica a:** il consumo di pacchetti, pubblicazione &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="81ca4-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="81ca4-106">Visualizza un elenco di pacchetti da un'origine specificata.</span><span class="sxs-lookup"><span data-stu-id="81ca4-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="81ca4-107">Se non vengono specificata alcuna origine, tutte le origini definito nel file di configurazione globale, `%AppData%\NuGet\NuGet.Config`, vengono utilizzati.</span><span class="sxs-lookup"><span data-stu-id="81ca4-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="81ca4-108">Se `NuGet.Config` non specifica nessuna origine, quindi `list` Usa il feed predefinito (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="81ca4-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="81ca4-109">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="81ca4-109">Usage</span></span>

```
nuget list [search terms] [options]
```

<span data-ttu-id="81ca4-110">in termini di ricerca facoltativo verranno filtrato l'elenco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="81ca4-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="81ca4-111">I termini di ricerca vengono applicati ai nomi dei pacchetti, tag e le descrizioni di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="81ca4-111">Search terms are applied to the names of packages, tags, and package descriptions.</span></span>

## <a name="options"></a><span data-ttu-id="81ca4-112">Opzioni</span><span class="sxs-lookup"><span data-stu-id="81ca4-112">Options</span></span>
| <span data-ttu-id="81ca4-113">Opzione</span><span class="sxs-lookup"><span data-stu-id="81ca4-113">Option</span></span> | <span data-ttu-id="81ca4-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="81ca4-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="81ca4-115">Completaversioni</span><span class="sxs-lookup"><span data-stu-id="81ca4-115">AllVersions</span></span> | <span data-ttu-id="81ca4-116">Elencare tutte le versioni di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="81ca4-116">List all versions of a package.</span></span> <span data-ttu-id="81ca4-117">Per impostazione predefinita, viene visualizzata solo la versione più recente del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="81ca4-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="81ca4-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="81ca4-118">ConfigFile</span></span> | <span data-ttu-id="81ca4-119">*(2.5 +)*  Questo file di configurazione da applicare.</span><span class="sxs-lookup"><span data-stu-id="81ca4-119">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="81ca4-120">Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="81ca4-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="81ca4-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="81ca4-121">ForceEnglishOutput</span></span> | <span data-ttu-id="81ca4-122">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="81ca4-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="81ca4-123">?</span><span class="sxs-lookup"><span data-stu-id="81ca4-123">Help</span></span> | <span data-ttu-id="81ca4-124">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="81ca4-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="81ca4-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="81ca4-125">IncludeDelisted</span></span> | <span data-ttu-id="81ca4-126">*(3.2 +)*  Visualizzare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="81ca4-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="81ca4-127">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="81ca4-127">NonInteractive</span></span> | <span data-ttu-id="81ca4-128">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="81ca4-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="81ca4-129">Versione provvisoria</span><span class="sxs-lookup"><span data-stu-id="81ca4-129">PreRelease</span></span> | <span data-ttu-id="81ca4-130">Include pacchetti della versione provvisoria, nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="81ca4-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="81ca4-131">Origine</span><span class="sxs-lookup"><span data-stu-id="81ca4-131">Source</span></span> | <span data-ttu-id="81ca4-132">Specifica un elenco di origini dei pacchetti per la ricerca.</span><span class="sxs-lookup"><span data-stu-id="81ca4-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="81ca4-133">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="81ca4-133">Verbosity</span></span> | <span data-ttu-id="81ca4-134">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="81ca4-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="81ca4-135">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="81ca4-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="81ca4-136">Esempi</span><span class="sxs-lookup"><span data-stu-id="81ca4-136">Examples</span></span>

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
