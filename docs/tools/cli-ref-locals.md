---
title: Comando di NuGet CLI variabili locali
description: Riferimento per il comando di nuget.exe variabili locali
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ac07dc306bc23c2fedd33c5627e8d34a6098387c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="52879-103">Comando locals (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="52879-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="52879-104">**Si applica a:** pacchetto consumo &bullet; **versioni supportate:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="52879-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="52879-105">Cancella o elenca le risorse locali di NuGet, ad esempio il *cache http*, *globale pacchetti* cartella e la cartella temporanea.</span><span class="sxs-lookup"><span data-stu-id="52879-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="52879-106">Il `locals` comando può essere utilizzato anche per visualizzare un elenco di tali percorsi.</span><span class="sxs-lookup"><span data-stu-id="52879-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="52879-107">Per altre informazioni, vedere [gestione dei pacchetti globali e alla cartella della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="52879-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="52879-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="52879-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="52879-109">in cui `<folder>` è uno dei `all`, `http-cache`, `packages-cache` *(3.5 e versioni precedenti)*, `global-packages`, e `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="52879-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="52879-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="52879-110">Options</span></span>

| <span data-ttu-id="52879-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="52879-111">Option</span></span> | <span data-ttu-id="52879-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="52879-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="52879-113">Cancella</span><span class="sxs-lookup"><span data-stu-id="52879-113">Clear</span></span> | <span data-ttu-id="52879-114">Cancella la cartella specificata.</span><span class="sxs-lookup"><span data-stu-id="52879-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="52879-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="52879-115">ConfigFile</span></span> | <span data-ttu-id="52879-116">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="52879-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="52879-117">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="52879-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="52879-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="52879-118">ForceEnglishOutput</span></span> | <span data-ttu-id="52879-119">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="52879-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="52879-120">?</span><span class="sxs-lookup"><span data-stu-id="52879-120">Help</span></span> | <span data-ttu-id="52879-121">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="52879-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="52879-122">List</span><span class="sxs-lookup"><span data-stu-id="52879-122">List</span></span> | <span data-ttu-id="52879-123">Elenca il percorso della cartella specificata o i percorsi di tutte le cartelle se usato con *tutti*.</span><span class="sxs-lookup"><span data-stu-id="52879-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="52879-124">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="52879-124">NonInteractive</span></span> | <span data-ttu-id="52879-125">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="52879-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="52879-126">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="52879-126">Verbosity</span></span> | <span data-ttu-id="52879-127">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="52879-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="52879-128">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="52879-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="52879-129">Esempi</span><span class="sxs-lookup"><span data-stu-id="52879-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="52879-130">Per ulteriori esempi, vedere [gestione dei pacchetti globali e alla cartella della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="52879-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
