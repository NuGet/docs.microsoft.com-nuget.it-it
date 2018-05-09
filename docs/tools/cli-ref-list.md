---
title: Comando di elenco NuGet CLI
description: Riferimento per il comando di elenco di nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4a44c70937e7cb49e472c53e9857e9f44d269f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="2d103-103">comando di elenco (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2d103-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="2d103-104">**Si applica a:** il consumo di pacchetti, pubblicazione &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="2d103-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="2d103-105">Visualizza un elenco di pacchetti da un'origine specificata.</span><span class="sxs-lookup"><span data-stu-id="2d103-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="2d103-106">Se non vengono specificata alcuna origine, tutte le origini definito nel file di configurazione globale, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config`, vengono utilizzati.</span><span class="sxs-lookup"><span data-stu-id="2d103-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="2d103-107">Se `NuGet.Config` non specifica nessuna origine, quindi `list` Usa il feed predefinito (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="2d103-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="2d103-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="2d103-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="2d103-109">in termini di ricerca facoltativo verranno filtrato l'elenco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="2d103-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="2d103-110">I termini di ricerca vengono applicati ai nomi dei pacchetti, tag e le descrizioni di pacchetto, esattamente come quando il loro utilizzo su nuget.org.</span><span class="sxs-lookup"><span data-stu-id="2d103-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="2d103-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="2d103-111">Options</span></span>

| <span data-ttu-id="2d103-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="2d103-112">Option</span></span> | <span data-ttu-id="2d103-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2d103-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2d103-114">Completaversioni</span><span class="sxs-lookup"><span data-stu-id="2d103-114">AllVersions</span></span> | <span data-ttu-id="2d103-115">Elencare tutte le versioni di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2d103-115">List all versions of a package.</span></span> <span data-ttu-id="2d103-116">Per impostazione predefinita, viene visualizzata solo la versione più recente del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2d103-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="2d103-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2d103-117">ConfigFile</span></span> | <span data-ttu-id="2d103-118">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="2d103-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2d103-119">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="2d103-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2d103-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2d103-120">ForceEnglishOutput</span></span> | <span data-ttu-id="2d103-121">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="2d103-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2d103-122">?</span><span class="sxs-lookup"><span data-stu-id="2d103-122">Help</span></span> | <span data-ttu-id="2d103-123">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="2d103-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="2d103-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="2d103-124">IncludeDelisted</span></span> | <span data-ttu-id="2d103-125">*(3.2 +)*  Visualizzare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="2d103-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="2d103-126">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="2d103-126">NonInteractive</span></span> | <span data-ttu-id="2d103-127">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="2d103-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2d103-128">Versione provvisoria</span><span class="sxs-lookup"><span data-stu-id="2d103-128">PreRelease</span></span> | <span data-ttu-id="2d103-129">Include pacchetti della versione provvisoria, nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="2d103-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="2d103-130">Origine</span><span class="sxs-lookup"><span data-stu-id="2d103-130">Source</span></span> | <span data-ttu-id="2d103-131">Specifica un elenco di origini dei pacchetti per la ricerca.</span><span class="sxs-lookup"><span data-stu-id="2d103-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="2d103-132">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="2d103-132">Verbosity</span></span> | <span data-ttu-id="2d103-133">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="2d103-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2d103-134">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2d103-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2d103-135">Esempi</span><span class="sxs-lookup"><span data-stu-id="2d103-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
