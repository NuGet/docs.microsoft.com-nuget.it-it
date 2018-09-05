---
title: Comando setapikey NuGet CLI
description: Informazioni di riferimento per il comando setapikey nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549220"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="d3f3d-103">comando setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d3f3d-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="d3f3d-104">**Si applica a:** utilizzo di un pacchetto, la pubblicazione &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="d3f3d-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d3f3d-105">Consente di salvare una chiave API per un URL del server specificato in `NuGet.Config` in modo che non è necessario specificare per i comandi successivi.</span><span class="sxs-lookup"><span data-stu-id="d3f3d-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="d3f3d-106">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="d3f3d-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="d3f3d-107">in cui `<source>` identifica il server e `<key>` è la chiave o password per salvare.</span><span class="sxs-lookup"><span data-stu-id="d3f3d-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="d3f3d-108">Se `<source>` viene omesso, viene usato nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d3f3d-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="d3f3d-109">Opzioni</span><span class="sxs-lookup"><span data-stu-id="d3f3d-109">Options</span></span>

| <span data-ttu-id="d3f3d-110">Opzione</span><span class="sxs-lookup"><span data-stu-id="d3f3d-110">Option</span></span> | <span data-ttu-id="d3f3d-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d3f3d-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d3f3d-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d3f3d-112">ConfigFile</span></span> | <span data-ttu-id="d3f3d-113">Il file di configurazione di NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="d3f3d-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d3f3d-114">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.</span><span class="sxs-lookup"><span data-stu-id="d3f3d-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d3f3d-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d3f3d-115">ForceEnglishOutput</span></span> | <span data-ttu-id="d3f3d-116">*(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="d3f3d-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d3f3d-117">?</span><span class="sxs-lookup"><span data-stu-id="d3f3d-117">Help</span></span> | <span data-ttu-id="d3f3d-118">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="d3f3d-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="d3f3d-119">Non interattive</span><span class="sxs-lookup"><span data-stu-id="d3f3d-119">NonInteractive</span></span> | <span data-ttu-id="d3f3d-120">Elimina richieste di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d3f3d-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d3f3d-121">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="d3f3d-121">Verbosity</span></span> | <span data-ttu-id="d3f3d-122">Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="d3f3d-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d3f3d-123">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d3f3d-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d3f3d-124">Esempi</span><span class="sxs-lookup"><span data-stu-id="d3f3d-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
