---
title: Comando di NuGet CLI list
description: Informazioni di riferimento per il comando list nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549801"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="cb0bd-103">comando List (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cb0bd-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="cb0bd-104">**Si applica a:** utilizzo di un pacchetto, la pubblicazione &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="cb0bd-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="cb0bd-105">Visualizza un elenco dei pacchetti da un'origine specificata.</span><span class="sxs-lookup"><span data-stu-id="cb0bd-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="cb0bd-106">Se non sono specificate origini, tutte le origini definite nel file di configurazione globali `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config`, vengono usati.</span><span class="sxs-lookup"><span data-stu-id="cb0bd-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="cb0bd-107">Se `NuGet.Config` non specifica nessuna origine, quindi `list` Usa il feed predefinito (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="cb0bd-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="cb0bd-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="cb0bd-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="cb0bd-109">in cui i termini di ricerca facoltativo filtrerà l'elenco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="cb0bd-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="cb0bd-110">I termini di ricerca vengono applicati ai nomi dei pacchetti, tag e descrizioni dei pacchetti, esattamente come lo sono quando vengono utilizzati in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="cb0bd-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="cb0bd-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="cb0bd-111">Options</span></span>

| <span data-ttu-id="cb0bd-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="cb0bd-112">Option</span></span> | <span data-ttu-id="cb0bd-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cb0bd-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cb0bd-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="cb0bd-114">AllVersions</span></span> | <span data-ttu-id="cb0bd-115">Elencare tutte le versioni di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cb0bd-115">List all versions of a package.</span></span> <span data-ttu-id="cb0bd-116">Per impostazione predefinita, viene visualizzato solo l'ultima versione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cb0bd-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="cb0bd-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="cb0bd-117">ConfigFile</span></span> | <span data-ttu-id="cb0bd-118">Il file di configurazione di NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="cb0bd-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cb0bd-119">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.</span><span class="sxs-lookup"><span data-stu-id="cb0bd-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="cb0bd-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cb0bd-120">ForceEnglishOutput</span></span> | <span data-ttu-id="cb0bd-121">*(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="cb0bd-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cb0bd-122">?</span><span class="sxs-lookup"><span data-stu-id="cb0bd-122">Help</span></span> | <span data-ttu-id="cb0bd-123">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="cb0bd-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="cb0bd-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="cb0bd-124">IncludeDelisted</span></span> | <span data-ttu-id="cb0bd-125">*(3.2 +)*  Visualizzare pacchetti rimossi dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="cb0bd-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="cb0bd-126">Non interattive</span><span class="sxs-lookup"><span data-stu-id="cb0bd-126">NonInteractive</span></span> | <span data-ttu-id="cb0bd-127">Elimina richieste di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="cb0bd-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="cb0bd-128">Versione preliminare</span><span class="sxs-lookup"><span data-stu-id="cb0bd-128">PreRelease</span></span> | <span data-ttu-id="cb0bd-129">Include prerelease pacchetti nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="cb0bd-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="cb0bd-130">Origine</span><span class="sxs-lookup"><span data-stu-id="cb0bd-130">Source</span></span> | <span data-ttu-id="cb0bd-131">Specifica un elenco di origini di pacchetti per la ricerca.</span><span class="sxs-lookup"><span data-stu-id="cb0bd-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="cb0bd-132">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="cb0bd-132">Verbosity</span></span> | <span data-ttu-id="cb0bd-133">Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="cb0bd-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="cb0bd-134">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cb0bd-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cb0bd-135">Esempi</span><span class="sxs-lookup"><span data-stu-id="cb0bd-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
