---
title: Comando elenco dell'interfaccia della riga di comando NuGet
description: Riferimento per il comando elenco nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a6a4ee434c43ad4865dba12f039b5d545a90d3c4
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238166"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="75ee4-103">comando list (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="75ee4-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="75ee4-104">**Si applica a:** utilizzo del pacchetto, pubblicazione delle &bullet; **versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="75ee4-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="75ee4-105">Visualizza un elenco di pacchetti da un'origine specificata.</span><span class="sxs-lookup"><span data-stu-id="75ee4-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="75ee4-106">Se non viene specificata alcuna origine, vengono utilizzate tutte le origini definite nel file di configurazione globale `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` .</span><span class="sxs-lookup"><span data-stu-id="75ee4-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="75ee4-107">Se `NuGet.Config` non specifica alcuna origine, `list` Usa il feed predefinito (NuGet.org).</span><span class="sxs-lookup"><span data-stu-id="75ee4-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="75ee4-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="75ee4-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="75ee4-109">dove i termini di ricerca facoltativi filtrano l'elenco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="75ee4-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="75ee4-110">I [termini di ricerca](../../consume-packages/finding-and-choosing-packages.md#search-syntax) vengono applicati ai nomi di pacchetti, tag e descrizioni del pacchetto così come sono quando vengono utilizzati in NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="75ee4-110">[Search terms](../../consume-packages/finding-and-choosing-packages.md#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="75ee4-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="75ee4-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="75ee4-112">Elencare tutte le versioni di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="75ee4-112">List all versions of a package.</span></span> <span data-ttu-id="75ee4-113">Per impostazione predefinita, viene visualizzata solo la versione più recente del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="75ee4-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="75ee4-114">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="75ee4-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="75ee4-115">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="75ee4-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="75ee4-116">*(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="75ee4-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="75ee4-117">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="75ee4-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="75ee4-118">*(3.2 +)* Visualizza i pacchetti non in elenco.</span><span class="sxs-lookup"><span data-stu-id="75ee4-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="75ee4-119">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="75ee4-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="75ee4-120">Include i pacchetti di versioni non definitive nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="75ee4-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="75ee4-121">Specifica un elenco di origini dei pacchetti in cui eseguire la ricerca.</span><span class="sxs-lookup"><span data-stu-id="75ee4-121">Specifies a list of packages sources to search.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="75ee4-122">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="75ee4-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="75ee4-123">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="75ee4-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="75ee4-124">Esempi</span><span class="sxs-lookup"><span data-stu-id="75ee4-124">Examples</span></span>

<span data-ttu-id="75ee4-125">Elencare tutti i pacchetti dai feed configurati:</span><span class="sxs-lookup"><span data-stu-id="75ee4-125">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="75ee4-126">Elencare i pacchetti correlati ad Azure con dettaglio dettagliato:</span><span class="sxs-lookup"><span data-stu-id="75ee4-126">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="75ee4-127">Elencare tutte le versioni dei pacchetti correlati ad Azure dai feed configurati:</span><span class="sxs-lookup"><span data-stu-id="75ee4-127">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="75ee4-128">Elencare tutte le versioni dei pacchetti correlati a JSON dall'origine/feed specificata:</span><span class="sxs-lookup"><span data-stu-id="75ee4-128">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="75ee4-129">Elencare i pacchetti correlati a JSON da più origini/feed:</span><span class="sxs-lookup"><span data-stu-id="75ee4-129">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```