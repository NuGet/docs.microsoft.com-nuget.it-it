---
title: Comando della Guida CLI di NuGet
description: Riferimento per il comando della Guida nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5d91638c4a6f167ea8a04e5dfa2905cb55084ddd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779351"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="fd369-103">help o ?</span><span class="sxs-lookup"><span data-stu-id="fd369-103">help or ?</span></span> <span data-ttu-id="fd369-104">(interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="fd369-104">command (NuGet CLI)</span></span>

<span data-ttu-id="fd369-105">**Si applica a:** tutte le &bullet; **versioni supportate**: tutti</span><span class="sxs-lookup"><span data-stu-id="fd369-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="fd369-106">Visualizza informazioni generali sulla guida e informazioni su comandi specifici.</span><span class="sxs-lookup"><span data-stu-id="fd369-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="fd369-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="fd369-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="fd369-108">dove [Command] identifica un comando specifico per il quale visualizzare la guida.</span><span class="sxs-lookup"><span data-stu-id="fd369-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="fd369-109">Con alcuni comandi, prestare attenzione a specificare prima di tutto la *Guida* , come con `nuget help install` , perché in NuGet.org è presente un pacchetto denominato "Help". Se si assegna il comando `nuget install help` , non si otterrà la guida sul comando di installazione, ma si installerà il pacchetto denominato Help.</span><span class="sxs-lookup"><span data-stu-id="fd369-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="fd369-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="fd369-110">Options</span></span>

- **`-All`**

  <span data-ttu-id="fd369-111">Stampa la guida dettagliata per tutti i comandi disponibili; viene ignorato se viene specificato un comando specifico.</span><span class="sxs-lookup"><span data-stu-id="fd369-111">Print detailed help for all available commands; ignored if a specific command is given.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="fd369-112">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="fd369-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fd369-113">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="fd369-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="fd369-114">*(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="fd369-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="fd369-115">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="fd369-115">Displays help information for the command.</span></span>

- **`-Markdown`**

  <span data-ttu-id="fd369-116">Stampa la guida dettagliata nel formato Markdown quando viene usato con `-All` .</span><span class="sxs-lookup"><span data-stu-id="fd369-116">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="fd369-117">In caso contrario, verrà ignorato.</span><span class="sxs-lookup"><span data-stu-id="fd369-117">Ignored otherwise.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="fd369-118">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="fd369-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="fd369-119">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="fd369-119">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="fd369-120">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fd369-120">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fd369-121">Esempi</span><span class="sxs-lookup"><span data-stu-id="fd369-121">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
