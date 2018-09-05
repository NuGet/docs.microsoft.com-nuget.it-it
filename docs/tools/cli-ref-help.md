---
title: Comando di NuGet CLI?
description: Informazioni di riferimento per il comando help nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546563"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="8f6ca-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="8f6ca-103">help or ?</span></span> <span data-ttu-id="8f6ca-104">(interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="8f6ca-104">command (NuGet CLI)</span></span>

<span data-ttu-id="8f6ca-105">**Si applica a:** tutte &bullet; **le versioni supportate**: tutti</span><span class="sxs-lookup"><span data-stu-id="8f6ca-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="8f6ca-106">Generale consente di visualizzare informazioni della Guida e informazioni sui comandi specifici per il supporto.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="8f6ca-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="8f6ca-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="8f6ca-108">dove [comando] identifica un comando specifico per cui si desidera visualizzare la Guida.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="8f6ca-109">Con alcuni comandi, tenere conto specificare *aiutare* prima, come con `nuget help install`, essendo presente un pacchetto denominato "help" su nuget.org. Qualora il Licenziatario fornisca il comando `nuget install help`, si otterranno della Guida sul comando install ma verranno invece installare il pacchetto denominato della Guida.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="8f6ca-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="8f6ca-110">Options</span></span>

| <span data-ttu-id="8f6ca-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="8f6ca-111">Option</span></span> | <span data-ttu-id="8f6ca-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8f6ca-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8f6ca-113">Tutti</span><span class="sxs-lookup"><span data-stu-id="8f6ca-113">All</span></span> | <span data-ttu-id="8f6ca-114">Stampa una Guida dettagliata per tutti i comandi disponibili; ignorato se viene fornito un comando specifico.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="8f6ca-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8f6ca-115">ConfigFile</span></span> | <span data-ttu-id="8f6ca-116">Il file di configurazione di NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8f6ca-117">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8f6ca-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8f6ca-118">ForceEnglishOutput</span></span> | <span data-ttu-id="8f6ca-119">*(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8f6ca-120">?</span><span class="sxs-lookup"><span data-stu-id="8f6ca-120">Help</span></span> | <span data-ttu-id="8f6ca-121">Visualizza la Guida informazioni per il comando della Guida in linea se stesso.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="8f6ca-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="8f6ca-122">Markdown</span></span> | <span data-ttu-id="8f6ca-123">Stampa la Guida dettagliata in formato markdown quando usato con `-All`.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="8f6ca-124">Ignorato in caso contrario.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="8f6ca-125">Non interattive</span><span class="sxs-lookup"><span data-stu-id="8f6ca-125">NonInteractive</span></span> | <span data-ttu-id="8f6ca-126">Elimina richieste di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8f6ca-127">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="8f6ca-127">Verbosity</span></span> | <span data-ttu-id="8f6ca-128">Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="8f6ca-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8f6ca-129">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8f6ca-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8f6ca-130">Esempi</span><span class="sxs-lookup"><span data-stu-id="8f6ca-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
