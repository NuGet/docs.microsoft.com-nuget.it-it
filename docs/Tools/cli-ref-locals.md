---
title: Comando di NuGet CLI variabili locali | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 7f672c7c-74c9-4296-bc27-4d47882b541c
description: Riferimento per il comando di nuget.exe variabili locali
keywords: riferimento di variabili locali NuGet, il comando di variabili locali
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8cc06eedc20507e2bdd210e40c471ff551b89563
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
## <a name="locals-command-nuget-cli"></a><span data-ttu-id="84345-104">comando variabili locali (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="84345-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="84345-105">**Si applica a:** pacchetto consumo &bullet; **le versioni supportate:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="84345-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="84345-106">Cancella o elenca le risorse locali di NuGet, ad esempio la cache della richiesta http, la cache di pacchetti e la cartella pacchetti globali a livello di computer.</span><span class="sxs-lookup"><span data-stu-id="84345-106">Clears or lists local NuGet resources such as the http-request cache, packages cache, and the machine-wide global packages folder.</span></span> <span data-ttu-id="84345-107">Il `locals` comando può essere utilizzato anche per visualizzare un elenco di tali percorsi.</span><span class="sxs-lookup"><span data-stu-id="84345-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="84345-108">Per ulteriori informazioni, vedere [gestione delle NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="84345-108">For more information, see [Managing the NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

## <a name="usage"></a><span data-ttu-id="84345-109">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="84345-109">Usage</span></span>

```
nuget locals <cache> [options]
```

<span data-ttu-id="84345-110">dove `<cache>` è uno dei `all`, `http-cache`, `packages-cache`, `global-packages`, e `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="84345-110">where `<cache>` is one of `all`, `http-cache`, `packages-cache`, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="84345-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="84345-111">Options</span></span>

| <span data-ttu-id="84345-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="84345-112">Option</span></span> | <span data-ttu-id="84345-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="84345-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="84345-114">Cancella</span><span class="sxs-lookup"><span data-stu-id="84345-114">Clear</span></span> | <span data-ttu-id="84345-115">Cancella la cache specificata.</span><span class="sxs-lookup"><span data-stu-id="84345-115">Clears the specified cache.</span></span> |
| <span data-ttu-id="84345-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="84345-116">ConfigFile</span></span> | <span data-ttu-id="84345-117">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="84345-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="84345-118">Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="84345-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="84345-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="84345-119">ForceEnglishOutput</span></span> | <span data-ttu-id="84345-120">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="84345-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="84345-121">?</span><span class="sxs-lookup"><span data-stu-id="84345-121">Help</span></span> | <span data-ttu-id="84345-122">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="84345-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="84345-123">Elenco</span><span class="sxs-lookup"><span data-stu-id="84345-123">List</span></span> | <span data-ttu-id="84345-124">Elenca il percorso della cache specificata o i percorsi di tutte le cache se utilizzata con *tutti*.</span><span class="sxs-lookup"><span data-stu-id="84345-124">Lists the location of the specified cache, or the locations of all caches when used with *all*.</span></span> |
| <span data-ttu-id="84345-125">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="84345-125">NonInteractive</span></span> | <span data-ttu-id="84345-126">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="84345-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="84345-127">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="84345-127">Verbosity</span></span> | <span data-ttu-id="84345-128">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="84345-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="84345-129">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="84345-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="84345-130">Esempi</span><span class="sxs-lookup"><span data-stu-id="84345-130">Examples</span></span>

```
nuget locals all -list
nuget locals http-cache -clear
```
