---
title: Comando setApiKey dell'interfaccia della riga di comando NuGet
description: Informazioni di riferimento per il comando setApiKey di NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327608"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="364da-103">comando setApiKey (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="364da-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="364da-104">**Si applica a:** utilizzo del pacchetto &bullet; , pubblicazione delle **versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="364da-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="364da-105">Salva una chiave API per un URL del server specificato `NuGet.Config` in in modo che non debba essere immessa per i comandi successivi.</span><span class="sxs-lookup"><span data-stu-id="364da-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="364da-106">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="364da-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="364da-107">dove `<source>` identifica il server e `<key>` è la chiave o la password da salvare.</span><span class="sxs-lookup"><span data-stu-id="364da-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="364da-108">Se `<source>` viene omesso, viene utilizzato NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="364da-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="364da-109">Opzioni</span><span class="sxs-lookup"><span data-stu-id="364da-109">Options</span></span>

| <span data-ttu-id="364da-110">Opzione</span><span class="sxs-lookup"><span data-stu-id="364da-110">Option</span></span> | <span data-ttu-id="364da-111">DESCRIZIONE</span><span class="sxs-lookup"><span data-stu-id="364da-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="364da-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="364da-112">ConfigFile</span></span> | <span data-ttu-id="364da-113">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="364da-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="364da-114">Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="364da-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="364da-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="364da-115">ForceEnglishOutput</span></span> | <span data-ttu-id="364da-116">*(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese.</span><span class="sxs-lookup"><span data-stu-id="364da-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="364da-117">Help</span><span class="sxs-lookup"><span data-stu-id="364da-117">Help</span></span> | <span data-ttu-id="364da-118">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="364da-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="364da-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="364da-119">NonInteractive</span></span> | <span data-ttu-id="364da-120">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="364da-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="364da-121">Verbosity</span><span class="sxs-lookup"><span data-stu-id="364da-121">Verbosity</span></span> | <span data-ttu-id="364da-122">Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*.</span><span class="sxs-lookup"><span data-stu-id="364da-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="364da-123">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="364da-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="364da-124">Esempi</span><span class="sxs-lookup"><span data-stu-id="364da-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
