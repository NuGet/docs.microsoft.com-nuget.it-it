---
title: Comando elenco dell'interfaccia della riga di comando NuGet
description: Riferimento per il comando elenco nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 55ccf0d86ad6df8001e7401d430ec29cd7a154c3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780063"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="867d4-103">comando list (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="867d4-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="867d4-104">**Si applica a:** utilizzo del pacchetto, pubblicazione delle &bullet; **versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="867d4-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="867d4-105">Visualizza un elenco di pacchetti da un'origine specificata.</span><span class="sxs-lookup"><span data-stu-id="867d4-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="867d4-106">Se non viene specificata alcuna origine, vengono utilizzate tutte le origini definite nel file di configurazione globale `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` .</span><span class="sxs-lookup"><span data-stu-id="867d4-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="867d4-107">Se `NuGet.Config` non specifica alcuna origine, `list` Usa il feed predefinito (NuGet.org).</span><span class="sxs-lookup"><span data-stu-id="867d4-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="867d4-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="867d4-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="867d4-109">dove i termini di ricerca facoltativi filtrano l'elenco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="867d4-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="867d4-110">I [termini di ricerca](../../consume-packages/finding-and-choosing-packages.md#search-syntax) vengono applicati ai nomi di pacchetti, tag e descrizioni del pacchetto così come sono quando vengono utilizzati in NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="867d4-110">[Search terms](../../consume-packages/finding-and-choosing-packages.md#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="867d4-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="867d4-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="867d4-112">Elencare tutte le versioni di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="867d4-112">List all versions of a package.</span></span> <span data-ttu-id="867d4-113">Per impostazione predefinita, viene visualizzata solo la versione più recente del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="867d4-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="867d4-114">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="867d4-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="867d4-115">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="867d4-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="867d4-116">*(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="867d4-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="867d4-117">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="867d4-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="867d4-118">*(3.2 +)* Visualizza i pacchetti non in elenco.</span><span class="sxs-lookup"><span data-stu-id="867d4-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="867d4-119">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="867d4-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="867d4-120">Include i pacchetti di versioni non definitive nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="867d4-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="867d4-121">Origine del pacchetto da cercare.</span><span class="sxs-lookup"><span data-stu-id="867d4-121">The package source to search.</span></span> <span data-ttu-id="867d4-122">È possibile specificare più origini usando l' `-Source` opzione più volte.</span><span class="sxs-lookup"><span data-stu-id="867d4-122">You can specify multiple sources by using the `-Source` option multiple times.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="867d4-123">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="867d4-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="867d4-124">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="867d4-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="867d4-125">Esempi</span><span class="sxs-lookup"><span data-stu-id="867d4-125">Examples</span></span>

<span data-ttu-id="867d4-126">Elencare tutti i pacchetti dai feed configurati:</span><span class="sxs-lookup"><span data-stu-id="867d4-126">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="867d4-127">Elencare i pacchetti correlati ad Azure con dettaglio dettagliato:</span><span class="sxs-lookup"><span data-stu-id="867d4-127">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="867d4-128">Elencare tutte le versioni dei pacchetti correlati ad Azure dai feed configurati:</span><span class="sxs-lookup"><span data-stu-id="867d4-128">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="867d4-129">Elencare tutte le versioni dei pacchetti correlati a JSON dall'origine/feed specificata:</span><span class="sxs-lookup"><span data-stu-id="867d4-129">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="867d4-130">Elencare i pacchetti correlati a JSON da più origini/feed:</span><span class="sxs-lookup"><span data-stu-id="867d4-130">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```
