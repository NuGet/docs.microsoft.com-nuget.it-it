---
title: Comando della Guida CLI di NuGet
description: Riferimento per il comando della Guida di NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327798"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="a241b-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="a241b-103">help or ?</span></span> <span data-ttu-id="a241b-104">(interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="a241b-104">command (NuGet CLI)</span></span>

<span data-ttu-id="a241b-105">**Si applica a:** tutte le &bullet; **versioni supportate**: tutti</span><span class="sxs-lookup"><span data-stu-id="a241b-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="a241b-106">Visualizza informazioni generali sulla guida e informazioni su comandi specifici.</span><span class="sxs-lookup"><span data-stu-id="a241b-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="a241b-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="a241b-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="a241b-108">dove [Command] identifica un comando specifico per il quale visualizzare la guida.</span><span class="sxs-lookup"><span data-stu-id="a241b-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="a241b-109">Con alcuni comandi, prestare attenzione a specificare  prima di tutto la Guida `nuget help install`, come con, perché in NuGet.org è presente un pacchetto denominato "Help". Se si assegna il comando `nuget install help`, non si otterrà la guida sul comando di installazione, ma si installerà il pacchetto denominato Help.</span><span class="sxs-lookup"><span data-stu-id="a241b-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="a241b-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="a241b-110">Options</span></span>

| <span data-ttu-id="a241b-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="a241b-111">Option</span></span> | <span data-ttu-id="a241b-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a241b-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a241b-113">Tutti</span><span class="sxs-lookup"><span data-stu-id="a241b-113">All</span></span> | <span data-ttu-id="a241b-114">Stampa la guida dettagliata per tutti i comandi disponibili; viene ignorato se viene specificato un comando specifico.</span><span class="sxs-lookup"><span data-stu-id="a241b-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="a241b-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a241b-115">ConfigFile</span></span> | <span data-ttu-id="a241b-116">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="a241b-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a241b-117">Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="a241b-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a241b-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a241b-118">ForceEnglishOutput</span></span> | <span data-ttu-id="a241b-119">*(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese.</span><span class="sxs-lookup"><span data-stu-id="a241b-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a241b-120">?</span><span class="sxs-lookup"><span data-stu-id="a241b-120">Help</span></span> | <span data-ttu-id="a241b-121">Visualizza le informazioni della Guida per il comando della guida.</span><span class="sxs-lookup"><span data-stu-id="a241b-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="a241b-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="a241b-122">Markdown</span></span> | <span data-ttu-id="a241b-123">Stampa la guida dettagliata nel formato Markdown quando viene `-All`usato con.</span><span class="sxs-lookup"><span data-stu-id="a241b-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="a241b-124">In caso contrario, verrà ignorato.</span><span class="sxs-lookup"><span data-stu-id="a241b-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="a241b-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a241b-125">NonInteractive</span></span> | <span data-ttu-id="a241b-126">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a241b-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a241b-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="a241b-127">Verbosity</span></span> | <span data-ttu-id="a241b-128">Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*.</span><span class="sxs-lookup"><span data-stu-id="a241b-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a241b-129">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a241b-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a241b-130">Esempi</span><span class="sxs-lookup"><span data-stu-id="a241b-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
