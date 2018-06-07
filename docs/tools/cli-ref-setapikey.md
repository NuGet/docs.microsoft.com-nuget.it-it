---
title: Comando setapikey NuGet CLI
description: Riferimento per il comando di nuget.exe setapikey
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 66fc62074b4e7c39ff2ed6b515eee9f821530536
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817684"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="5efce-103">comando setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5efce-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="5efce-104">**Si applica a:** il consumo di pacchetti, pubblicazione &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="5efce-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5efce-105">Salva una chiave API per un URL del server specificato in `NuGet.Config` in modo che non deve essere inserito per i comandi successivi.</span><span class="sxs-lookup"><span data-stu-id="5efce-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="5efce-106">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="5efce-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="5efce-107">dove `<source>` identifica il server e `<key>` è la chiave o una password per salvare.</span><span class="sxs-lookup"><span data-stu-id="5efce-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="5efce-108">Se `<source>` viene omesso, verrà utilizzato nuget.org.</span><span class="sxs-lookup"><span data-stu-id="5efce-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="5efce-109">Opzioni</span><span class="sxs-lookup"><span data-stu-id="5efce-109">Options</span></span>

| <span data-ttu-id="5efce-110">Opzione</span><span class="sxs-lookup"><span data-stu-id="5efce-110">Option</span></span> | <span data-ttu-id="5efce-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5efce-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5efce-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5efce-112">ConfigFile</span></span> | <span data-ttu-id="5efce-113">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="5efce-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5efce-114">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5efce-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5efce-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5efce-115">ForceEnglishOutput</span></span> | <span data-ttu-id="5efce-116">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="5efce-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5efce-117">?</span><span class="sxs-lookup"><span data-stu-id="5efce-117">Help</span></span> | <span data-ttu-id="5efce-118">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="5efce-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="5efce-119">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="5efce-119">NonInteractive</span></span> | <span data-ttu-id="5efce-120">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="5efce-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5efce-121">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="5efce-121">Verbosity</span></span> | <span data-ttu-id="5efce-122">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="5efce-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5efce-123">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5efce-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5efce-124">Esempi</span><span class="sxs-lookup"><span data-stu-id="5efce-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
