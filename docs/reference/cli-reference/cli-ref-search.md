---
title: Comando di ricerca CLI NuGet
description: Riferimento per il comando di ricerca di nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 6f4adcdf3981e5ec0e5e88337a8c3bcdd9158ca3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779157"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="5c812-103">comando Search (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="5c812-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="5c812-104">**Si applica a:** versioni supportate per l'utilizzo di pacchetti &bullet; **:** 5.8 +</span><span class="sxs-lookup"><span data-stu-id="5c812-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="5c812-105">Esegue la ricerca di una determinata origine utilizzando la stringa di query specificata.</span><span class="sxs-lookup"><span data-stu-id="5c812-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="5c812-106">Se non viene specificata alcuna origine, vengono utilizzate tutte le origini definite in% AppData% \NuGet\NuGet.config.</span><span class="sxs-lookup"><span data-stu-id="5c812-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="5c812-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="5c812-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="5c812-108">dove vengono applicati i termini di ricerca ai nomi di pacchetti, tag e descrizioni del pacchetto come quando si usano in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="5c812-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="5c812-109">Opzioni</span><span class="sxs-lookup"><span data-stu-id="5c812-109">Options</span></span>

| <span data-ttu-id="5c812-110">Nome</span><span class="sxs-lookup"><span data-stu-id="5c812-110">Name</span></span> | <span data-ttu-id="5c812-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5c812-111">Description</span></span> | <span data-ttu-id="5c812-112">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="5c812-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="5c812-113">PreRelease</span><span class="sxs-lookup"><span data-stu-id="5c812-113">PreRelease</span></span> | <span data-ttu-id="5c812-114">I pacchetti di versioni non definitive non sono inclusi per impostazione predefinita, ma possono essere inclusi usando questo argomento</span><span class="sxs-lookup"><span data-stu-id="5c812-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="5c812-115">-Versione preliminare</span><span class="sxs-lookup"><span data-stu-id="5c812-115">-PreRelease</span></span> |
| <span data-ttu-id="5c812-116">Source (Sorgente)</span><span class="sxs-lookup"><span data-stu-id="5c812-116">Source</span></span> | <span data-ttu-id="5c812-117">Origini pacchetti specifiche in cui eseguire la ricerca anziché eseguire query sulle origini predefinite in __nuget.config__</span><span class="sxs-lookup"><span data-stu-id="5c812-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="5c812-118">-Origine `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="5c812-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="5c812-119">Take</span><span class="sxs-lookup"><span data-stu-id="5c812-119">Take</span></span> | <span data-ttu-id="5c812-120">Numero di risultati da restituire.</span><span class="sxs-lookup"><span data-stu-id="5c812-120">The number of results to return.</span></span> <span data-ttu-id="5c812-121">Il valore predefinito è 20.</span><span class="sxs-lookup"><span data-stu-id="5c812-121">The default value is 20.</span></span> | <span data-ttu-id="5c812-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="5c812-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="5c812-123">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="5c812-123">Verbosity</span></span> | <span data-ttu-id="5c812-124">Livello di dettaglio da visualizzare nell'output.</span><span class="sxs-lookup"><span data-stu-id="5c812-124">The level of detail to display in the output.</span></span> <span data-ttu-id="5c812-125">Il valore predefinito è _Normal_.</span><span class="sxs-lookup"><span data-stu-id="5c812-125">The default is _normal_.</span></span> <span data-ttu-id="5c812-126">(Vedere la nota di seguito)</span><span class="sxs-lookup"><span data-stu-id="5c812-126">(See the note below)</span></span>  | <span data-ttu-id="5c812-127">-Livello di dettaglio `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="5c812-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="5c812-128">Guida</span><span class="sxs-lookup"><span data-stu-id="5c812-128">Help</span></span> | <span data-ttu-id="5c812-129">Visualizza le informazioni della Guida per il comando</span><span class="sxs-lookup"><span data-stu-id="5c812-129">Displays help information for the command</span></span> | <span data-ttu-id="5c812-130">-Guida</span><span class="sxs-lookup"><span data-stu-id="5c812-130">-Help</span></span> |

<span data-ttu-id="5c812-131">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5c812-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="5c812-132">Livelli di dettaglio:</span><span class="sxs-lookup"><span data-stu-id="5c812-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="5c812-133">_quiet_ -ID pacchetto, versione</span><span class="sxs-lookup"><span data-stu-id="5c812-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="5c812-134">_normale_ -ID pacchetto, versione, download, anteprima della descrizione</span><span class="sxs-lookup"><span data-stu-id="5c812-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="5c812-135">_Dettagli_ -ID pacchetto, versione, download, descrizione completa, altre informazioni, ad esempio l'URL della query</span><span class="sxs-lookup"><span data-stu-id="5c812-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="5c812-136">Esempi</span><span class="sxs-lookup"><span data-stu-id="5c812-136">Examples</span></span>

<span data-ttu-id="5c812-137">Cercare i pacchetti correlati alla *registrazione* da origini predefinite:</span><span class="sxs-lookup"><span data-stu-id="5c812-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="5c812-138">Cercare i pacchetti correlati alla *registrazione* con un livello di dettaglio dettagliato:</span><span class="sxs-lookup"><span data-stu-id="5c812-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="5c812-139">Cercare i pacchetti correlati alla *registrazione* e visualizzare solo i primi 5 risultati:</span><span class="sxs-lookup"><span data-stu-id="5c812-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="5c812-140">Cercare i pacchetti correlati a *JSON*, incluse le versioni non definitive, dall'origine/feed specificati:</span><span class="sxs-lookup"><span data-stu-id="5c812-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="5c812-141">Cercare pacchetti correlati a *JSON* da più origini/feed:</span><span class="sxs-lookup"><span data-stu-id="5c812-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
