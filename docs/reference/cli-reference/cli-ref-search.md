---
title: Comando di ricerca dell'interfaccia della riga di comando di NuGet
description: Informazioni di riferimento per il nuget.exe di ricerca
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323661"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="85330-103">Comando search (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="85330-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="85330-104">**Si applica a:** utilizzo del pacchetto &bullet; **Versioni supportate:** 5.8+</span><span class="sxs-lookup"><span data-stu-id="85330-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="85330-105">Cerca in un'origine specificata usando la stringa di query fornita.</span><span class="sxs-lookup"><span data-stu-id="85330-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="85330-106">Se non viene specificata alcuna origine, vengono usate tutte le origini definite in %AppData%\NuGet\NuGet.Config.</span><span class="sxs-lookup"><span data-stu-id="85330-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.Config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="85330-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="85330-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="85330-108">in cui i termini di ricerca vengono applicati ai nomi dei pacchetti, dei tag e delle descrizioni dei pacchetti esattamente come quando vengono utilizzati in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="85330-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="85330-109">Opzioni</span><span class="sxs-lookup"><span data-stu-id="85330-109">Options</span></span>

| <span data-ttu-id="85330-110">Nome</span><span class="sxs-lookup"><span data-stu-id="85330-110">Name</span></span> | <span data-ttu-id="85330-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="85330-111">Description</span></span> | <span data-ttu-id="85330-112">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="85330-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="85330-113">Preliminare</span><span class="sxs-lookup"><span data-stu-id="85330-113">PreRelease</span></span> | <span data-ttu-id="85330-114">I pacchetti di versioni non definitiva non sono inclusi per impostazione predefinita, ma possono essere inclusi usando questo argomento</span><span class="sxs-lookup"><span data-stu-id="85330-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="85330-115">-PreRelease</span><span class="sxs-lookup"><span data-stu-id="85330-115">-PreRelease</span></span> |
| <span data-ttu-id="85330-116">Origine</span><span class="sxs-lookup"><span data-stu-id="85330-116">Source</span></span> | <span data-ttu-id="85330-117">Origini del pacchetto specifiche in cui eseguire la ricerca anziché eseguire query nelle origini predefinite __nuget.config__</span><span class="sxs-lookup"><span data-stu-id="85330-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="85330-118">-Source `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="85330-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="85330-119">Take</span><span class="sxs-lookup"><span data-stu-id="85330-119">Take</span></span> | <span data-ttu-id="85330-120">Numero di risultati da restituire.</span><span class="sxs-lookup"><span data-stu-id="85330-120">The number of results to return.</span></span> <span data-ttu-id="85330-121">Il valore predefinito è 20.</span><span class="sxs-lookup"><span data-stu-id="85330-121">The default value is 20.</span></span> | <span data-ttu-id="85330-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="85330-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="85330-123">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="85330-123">Verbosity</span></span> | <span data-ttu-id="85330-124">Livello di dettaglio da visualizzare nell'output.</span><span class="sxs-lookup"><span data-stu-id="85330-124">The level of detail to display in the output.</span></span> <span data-ttu-id="85330-125">Il valore predefinito è _normale._</span><span class="sxs-lookup"><span data-stu-id="85330-125">The default is _normal_.</span></span> <span data-ttu-id="85330-126">(Vedere la nota seguente)</span><span class="sxs-lookup"><span data-stu-id="85330-126">(See the note below)</span></span>  | <span data-ttu-id="85330-127">-Verbosity `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="85330-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="85330-128">Help</span><span class="sxs-lookup"><span data-stu-id="85330-128">Help</span></span> | <span data-ttu-id="85330-129">Visualizza le informazioni della Guida per il comando</span><span class="sxs-lookup"><span data-stu-id="85330-129">Displays help information for the command</span></span> | <span data-ttu-id="85330-130">-Help</span><span class="sxs-lookup"><span data-stu-id="85330-130">-Help</span></span> |

<span data-ttu-id="85330-131">Vedere anche [Variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="85330-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="85330-132">Livelli di dettaglio:</span><span class="sxs-lookup"><span data-stu-id="85330-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="85330-133">_quiet_ - ID pacchetto, versione</span><span class="sxs-lookup"><span data-stu-id="85330-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="85330-134">_normal_ - ID pacchetto, versione, download, anteprima della descrizione</span><span class="sxs-lookup"><span data-stu-id="85330-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="85330-135">_detailed_ : ID pacchetto, versione, download, descrizione completa, altre informazioni, ad esempio l'URL della query</span><span class="sxs-lookup"><span data-stu-id="85330-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="85330-136">Esempio</span><span class="sxs-lookup"><span data-stu-id="85330-136">Examples</span></span>

<span data-ttu-id="85330-137">Cercare i *pacchetti* correlati alla registrazione dalle origini predefinite:</span><span class="sxs-lookup"><span data-stu-id="85330-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="85330-138">Cercare i *pacchetti* correlati alla registrazione con un livello di dettaglio dettagliato:</span><span class="sxs-lookup"><span data-stu-id="85330-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="85330-139">Cercare i *pacchetti* correlati alla registrazione e visualizzare solo i primi 5 risultati:</span><span class="sxs-lookup"><span data-stu-id="85330-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="85330-140">Cercare i pacchetti correlati a *JSON,* incluse le versioni non definitiva, dall'origine/feed specificato:</span><span class="sxs-lookup"><span data-stu-id="85330-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="85330-141">Cercare pacchetti correlati a *JSON* da più origini/feed:</span><span class="sxs-lookup"><span data-stu-id="85330-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
