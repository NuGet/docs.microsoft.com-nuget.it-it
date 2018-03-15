---
title: Comando help NuGet CLI | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando della Guida di nuget.exe
keywords: riferimento alla Guida NuGet, comandi della Guida.
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 281c6ccc7c58d153280441430be063d9ee89955d
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/15/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="b63a0-104">Guida in linea o?</span><span class="sxs-lookup"><span data-stu-id="b63a0-104">help or ?</span></span> <span data-ttu-id="b63a0-105">comando (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="b63a0-105">command (NuGet CLI)</span></span>

<span data-ttu-id="b63a0-106">**Si applica a:** tutti &bullet; **le versioni supportate**: tutti</span><span class="sxs-lookup"><span data-stu-id="b63a0-106">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="b63a0-107">Generale consente di visualizzare informazioni della Guida e le informazioni sui comandi specifici.</span><span class="sxs-lookup"><span data-stu-id="b63a0-107">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="b63a0-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="b63a0-108">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="b63a0-109">dove [comando] identifica un comando specifico per cui si desidera visualizzare la Guida.</span><span class="sxs-lookup"><span data-stu-id="b63a0-109">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="b63a0-110">Con alcuni comandi, tenere in considerazione specificare *Guida* prima, come con `nuget help install`, perché è un pacchetto denominato "help" in nuget.org. Se si fornisce il comando `nuget install help`, si otterranno della Guida sul comando di installazione, ma invece verrà installato il pacchetto denominato della Guida.</span><span class="sxs-lookup"><span data-stu-id="b63a0-110">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="b63a0-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="b63a0-111">Options</span></span>

| <span data-ttu-id="b63a0-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="b63a0-112">Option</span></span> | <span data-ttu-id="b63a0-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b63a0-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b63a0-114">Tutti</span><span class="sxs-lookup"><span data-stu-id="b63a0-114">All</span></span> | <span data-ttu-id="b63a0-115">Stampa la Guida dettagliata per tutti i comandi disponibili; ignorato se non viene specificato un comando specifico.</span><span class="sxs-lookup"><span data-stu-id="b63a0-115">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="b63a0-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b63a0-116">ConfigFile</span></span> | <span data-ttu-id="b63a0-117">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="b63a0-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b63a0-118">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="b63a0-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b63a0-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b63a0-119">ForceEnglishOutput</span></span> | <span data-ttu-id="b63a0-120">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="b63a0-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b63a0-121">?</span><span class="sxs-lookup"><span data-stu-id="b63a0-121">Help</span></span> | <span data-ttu-id="b63a0-122">Visualizza la Guida informazioni per il comando della Guida.</span><span class="sxs-lookup"><span data-stu-id="b63a0-122">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="b63a0-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="b63a0-123">Markdown</span></span> | <span data-ttu-id="b63a0-124">Stampare informazioni della Guida dettagliate in formato markdown se utilizzata con `-All`.</span><span class="sxs-lookup"><span data-stu-id="b63a0-124">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="b63a0-125">Ignorato in caso contrario.</span><span class="sxs-lookup"><span data-stu-id="b63a0-125">Ignored otherwise.</span></span> |
| <span data-ttu-id="b63a0-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b63a0-126">NonInteractive</span></span> | <span data-ttu-id="b63a0-127">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="b63a0-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b63a0-128">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="b63a0-128">Verbosity</span></span> | <span data-ttu-id="b63a0-129">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="b63a0-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b63a0-130">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b63a0-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b63a0-131">Esempi</span><span class="sxs-lookup"><span data-stu-id="b63a0-131">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
