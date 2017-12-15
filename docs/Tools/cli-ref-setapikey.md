---
title: Comando di NuGet CLI setapikey | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a64c0462-973d-4100-ba3f-8902a2b127f7
description: Riferimento per il comando di nuget.exe setapikey
keywords: NuGet setapikey riferimento, il comando setapikey
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a07c35b8bdd57157391e391e04a90204342b1d5c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
## <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="f1cb2-104">comando setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f1cb2-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="f1cb2-105">**Si applica a:** il consumo di pacchetti, pubblicazione &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="f1cb2-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f1cb2-106">Salva una chiave API per un URL del server specificato in `NuGet.Config` in modo che non deve essere inserito per i comandi successivi.</span><span class="sxs-lookup"><span data-stu-id="f1cb2-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="f1cb2-107">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="f1cb2-107">Usage</span></span>

```
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="f1cb2-108">dove `<source>` identifica il server e `<key>` è la chiave o una password per salvare.</span><span class="sxs-lookup"><span data-stu-id="f1cb2-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="f1cb2-109">Se `<source>` viene omesso, verrà utilizzato nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f1cb2-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="f1cb2-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="f1cb2-110">Options</span></span>

| <span data-ttu-id="f1cb2-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="f1cb2-111">Option</span></span> | <span data-ttu-id="f1cb2-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f1cb2-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f1cb2-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f1cb2-113">ConfigFile</span></span> | <span data-ttu-id="f1cb2-114">*(2.5 +)*  Questo file di configurazione da modificare.</span><span class="sxs-lookup"><span data-stu-id="f1cb2-114">*(2.5+)* The NuGet configuration file to modify.</span></span> <span data-ttu-id="f1cb2-115">Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="f1cb2-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="f1cb2-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f1cb2-116">ForceEnglishOutput</span></span> | <span data-ttu-id="f1cb2-117">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="f1cb2-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f1cb2-118">?</span><span class="sxs-lookup"><span data-stu-id="f1cb2-118">Help</span></span> | <span data-ttu-id="f1cb2-119">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="f1cb2-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="f1cb2-120">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="f1cb2-120">NonInteractive</span></span> | <span data-ttu-id="f1cb2-121">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="f1cb2-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f1cb2-122">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="f1cb2-122">Verbosity</span></span> | <span data-ttu-id="f1cb2-123">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="f1cb2-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="f1cb2-124">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f1cb2-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f1cb2-125">Esempi</span><span class="sxs-lookup"><span data-stu-id="f1cb2-125">Examples</span></span>

```
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
