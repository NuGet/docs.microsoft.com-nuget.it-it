---
title: Comando help NuGet CLI
description: Riferimento per il comando della Guida di nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d7112209a0a2a267343c3458ebacaf6b744786a9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818256"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="e7a87-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="e7a87-103">help or ?</span></span> <span data-ttu-id="e7a87-104">(interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="e7a87-104">command (NuGet CLI)</span></span>

<span data-ttu-id="e7a87-105">**Si applica a:** tutti &bullet; **le versioni supportate**: tutti</span><span class="sxs-lookup"><span data-stu-id="e7a87-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="e7a87-106">Generale consente di visualizzare informazioni della Guida e le informazioni sui comandi specifici.</span><span class="sxs-lookup"><span data-stu-id="e7a87-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="e7a87-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="e7a87-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="e7a87-108">dove [comando] identifica un comando specifico per cui si desidera visualizzare la Guida.</span><span class="sxs-lookup"><span data-stu-id="e7a87-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="e7a87-109">Con alcuni comandi, tenere in considerazione specificare *Guida* prima, come con `nuget help install`, perché è un pacchetto denominato "help" in nuget.org. Se si fornisce il comando `nuget install help`, si otterranno della Guida sul comando di installazione, ma invece verrà installato il pacchetto denominato della Guida.</span><span class="sxs-lookup"><span data-stu-id="e7a87-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="e7a87-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="e7a87-110">Options</span></span>

| <span data-ttu-id="e7a87-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="e7a87-111">Option</span></span> | <span data-ttu-id="e7a87-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e7a87-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e7a87-113">Tutti</span><span class="sxs-lookup"><span data-stu-id="e7a87-113">All</span></span> | <span data-ttu-id="e7a87-114">Stampa la Guida dettagliata per tutti i comandi disponibili; ignorato se non viene specificato un comando specifico.</span><span class="sxs-lookup"><span data-stu-id="e7a87-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="e7a87-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e7a87-115">ConfigFile</span></span> | <span data-ttu-id="e7a87-116">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="e7a87-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e7a87-117">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="e7a87-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e7a87-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e7a87-118">ForceEnglishOutput</span></span> | <span data-ttu-id="e7a87-119">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="e7a87-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e7a87-120">?</span><span class="sxs-lookup"><span data-stu-id="e7a87-120">Help</span></span> | <span data-ttu-id="e7a87-121">Visualizza la Guida informazioni per il comando della Guida.</span><span class="sxs-lookup"><span data-stu-id="e7a87-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="e7a87-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="e7a87-122">Markdown</span></span> | <span data-ttu-id="e7a87-123">Stampare informazioni della Guida dettagliate in formato markdown se utilizzata con `-All`.</span><span class="sxs-lookup"><span data-stu-id="e7a87-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="e7a87-124">Ignorato in caso contrario.</span><span class="sxs-lookup"><span data-stu-id="e7a87-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="e7a87-125">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="e7a87-125">NonInteractive</span></span> | <span data-ttu-id="e7a87-126">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="e7a87-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e7a87-127">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="e7a87-127">Verbosity</span></span> | <span data-ttu-id="e7a87-128">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="e7a87-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="e7a87-129">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e7a87-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e7a87-130">Esempi</span><span class="sxs-lookup"><span data-stu-id="e7a87-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
