---
title: Comando di NuGet CLI setapikey | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Riferimento per il comando di nuget.exe setapikey
keywords: NuGet setapikey riferimento, il comando setapikey
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 696ccf9df5af487d3bf75925c1c1e0d1d1bf7f7b
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="de6d3-104">comando setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="de6d3-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="de6d3-105">**Si applica a:** il consumo di pacchetti, pubblicazione &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="de6d3-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="de6d3-106">Salva una chiave API per un URL del server specificato in `NuGet.Config` in modo che non deve essere inserito per i comandi successivi.</span><span class="sxs-lookup"><span data-stu-id="de6d3-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="de6d3-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="de6d3-107">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="de6d3-108">dove `<source>` identifica il server e `<key>` è la chiave o una password per salvare.</span><span class="sxs-lookup"><span data-stu-id="de6d3-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="de6d3-109">Se `<source>` viene omesso, verrà utilizzato nuget.org.</span><span class="sxs-lookup"><span data-stu-id="de6d3-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="de6d3-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="de6d3-110">Options</span></span>

| <span data-ttu-id="de6d3-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="de6d3-111">Option</span></span> | <span data-ttu-id="de6d3-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="de6d3-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de6d3-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="de6d3-113">ConfigFile</span></span> | <span data-ttu-id="de6d3-114">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="de6d3-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="de6d3-115">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="de6d3-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="de6d3-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="de6d3-116">ForceEnglishOutput</span></span> | <span data-ttu-id="de6d3-117">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="de6d3-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="de6d3-118">?</span><span class="sxs-lookup"><span data-stu-id="de6d3-118">Help</span></span> | <span data-ttu-id="de6d3-119">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="de6d3-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="de6d3-120">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="de6d3-120">NonInteractive</span></span> | <span data-ttu-id="de6d3-121">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="de6d3-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="de6d3-122">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="de6d3-122">Verbosity</span></span> | <span data-ttu-id="de6d3-123">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="de6d3-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="de6d3-124">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="de6d3-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="de6d3-125">Esempi</span><span class="sxs-lookup"><span data-stu-id="de6d3-125">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
