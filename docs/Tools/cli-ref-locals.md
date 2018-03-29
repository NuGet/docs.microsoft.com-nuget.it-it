---
title: Comando di NuGet CLI variabili locali | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Riferimento per il comando di nuget.exe variabili locali
keywords: riferimento di variabili locali NuGet, il comando di variabili locali
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0122c79e55b12838bd123cf91bfcbc5dbbd2a65c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="3ba36-104">comando variabili locali (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3ba36-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="3ba36-105">**Si applica a:** pacchetto consumo &bullet; **versioni supportate:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="3ba36-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="3ba36-106">Cancella o elenca le risorse locali di NuGet, ad esempio il *cache http*, *globale pacchetti* cartella e la cartella temporanea.</span><span class="sxs-lookup"><span data-stu-id="3ba36-106">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="3ba36-107">Il `locals` comando può essere utilizzato anche per visualizzare un elenco di tali percorsi.</span><span class="sxs-lookup"><span data-stu-id="3ba36-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="3ba36-108">Per altre informazioni, vedere [gestione dei pacchetti globali e alla cartella della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="3ba36-108">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="3ba36-109">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="3ba36-109">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="3ba36-110">in cui `<folder>` è uno dei `all`, `http-cache`, `packages-cache` *(3.5 e versioni precedenti)*, `global-packages`, e `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="3ba36-110">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="3ba36-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="3ba36-111">Options</span></span>

| <span data-ttu-id="3ba36-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="3ba36-112">Option</span></span> | <span data-ttu-id="3ba36-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3ba36-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3ba36-114">Cancella</span><span class="sxs-lookup"><span data-stu-id="3ba36-114">Clear</span></span> | <span data-ttu-id="3ba36-115">Cancella la cartella specificata.</span><span class="sxs-lookup"><span data-stu-id="3ba36-115">Clears the specified folder.</span></span> |
| <span data-ttu-id="3ba36-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3ba36-116">ConfigFile</span></span> | <span data-ttu-id="3ba36-117">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="3ba36-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3ba36-118">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="3ba36-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3ba36-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3ba36-119">ForceEnglishOutput</span></span> | <span data-ttu-id="3ba36-120">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="3ba36-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3ba36-121">?</span><span class="sxs-lookup"><span data-stu-id="3ba36-121">Help</span></span> | <span data-ttu-id="3ba36-122">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="3ba36-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="3ba36-123">List</span><span class="sxs-lookup"><span data-stu-id="3ba36-123">List</span></span> | <span data-ttu-id="3ba36-124">Elenca il percorso della cartella specificata o i percorsi di tutte le cartelle se usato con *tutti*.</span><span class="sxs-lookup"><span data-stu-id="3ba36-124">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="3ba36-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3ba36-125">NonInteractive</span></span> | <span data-ttu-id="3ba36-126">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="3ba36-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3ba36-127">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="3ba36-127">Verbosity</span></span> | <span data-ttu-id="3ba36-128">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="3ba36-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3ba36-129">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3ba36-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3ba36-130">Esempi</span><span class="sxs-lookup"><span data-stu-id="3ba36-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="3ba36-131">Per ulteriori esempi, vedere [gestione dei pacchetti globali e alla cartella della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="3ba36-131">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
