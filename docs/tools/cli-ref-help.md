---
title: Comando help NuGet CLI
description: Riferimento per il comando della Guida di nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: dbfc803e24c824d30e128d6e86cfa3c43660668f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="c4de4-103">Guida in linea o?</span><span class="sxs-lookup"><span data-stu-id="c4de4-103">help or ?</span></span> <span data-ttu-id="c4de4-104">(interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="c4de4-104">command (NuGet CLI)</span></span>

<span data-ttu-id="c4de4-105">**Si applica a:** tutti &bullet; **le versioni supportate**: tutti</span><span class="sxs-lookup"><span data-stu-id="c4de4-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="c4de4-106">Generale consente di visualizzare informazioni della Guida e le informazioni sui comandi specifici.</span><span class="sxs-lookup"><span data-stu-id="c4de4-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="c4de4-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="c4de4-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="c4de4-108">dove [comando] identifica un comando specifico per cui si desidera visualizzare la Guida.</span><span class="sxs-lookup"><span data-stu-id="c4de4-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="c4de4-109">Con alcuni comandi, tenere in considerazione specificare *Guida* prima, come con `nuget help install`, perché è un pacchetto denominato "help" in nuget.org. Se si fornisce il comando `nuget install help`, si otterranno della Guida sul comando di installazione, ma invece verrà installato il pacchetto denominato della Guida.</span><span class="sxs-lookup"><span data-stu-id="c4de4-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="c4de4-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="c4de4-110">Options</span></span>

| <span data-ttu-id="c4de4-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="c4de4-111">Option</span></span> | <span data-ttu-id="c4de4-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c4de4-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c4de4-113">Tutti</span><span class="sxs-lookup"><span data-stu-id="c4de4-113">All</span></span> | <span data-ttu-id="c4de4-114">Stampa la Guida dettagliata per tutti i comandi disponibili; ignorato se non viene specificato un comando specifico.</span><span class="sxs-lookup"><span data-stu-id="c4de4-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="c4de4-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c4de4-115">ConfigFile</span></span> | <span data-ttu-id="c4de4-116">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="c4de4-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c4de4-117">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="c4de4-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c4de4-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c4de4-118">ForceEnglishOutput</span></span> | <span data-ttu-id="c4de4-119">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="c4de4-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c4de4-120">?</span><span class="sxs-lookup"><span data-stu-id="c4de4-120">Help</span></span> | <span data-ttu-id="c4de4-121">Visualizza la Guida informazioni per il comando della Guida.</span><span class="sxs-lookup"><span data-stu-id="c4de4-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="c4de4-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="c4de4-122">Markdown</span></span> | <span data-ttu-id="c4de4-123">Stampare informazioni della Guida dettagliate in formato markdown se utilizzata con `-All`.</span><span class="sxs-lookup"><span data-stu-id="c4de4-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="c4de4-124">Ignorato in caso contrario.</span><span class="sxs-lookup"><span data-stu-id="c4de4-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="c4de4-125">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="c4de4-125">NonInteractive</span></span> | <span data-ttu-id="c4de4-126">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="c4de4-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c4de4-127">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="c4de4-127">Verbosity</span></span> | <span data-ttu-id="c4de4-128">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="c4de4-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c4de4-129">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c4de4-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c4de4-130">Esempi</span><span class="sxs-lookup"><span data-stu-id="c4de4-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
