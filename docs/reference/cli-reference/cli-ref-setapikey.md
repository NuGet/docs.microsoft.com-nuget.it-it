---
title: Comando setApiKey dell'interfaccia della riga di comando NuGet
description: Informazioni di riferimento per il comando setApiKey di NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231227"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="64a1e-103">comando setApiKey (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="64a1e-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="64a1e-104">**Si applica a:** utilizzo del pacchetto, pubblicazione &bullet; **versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="64a1e-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="64a1e-105">Salva una chiave API per un URL server specificato in `NuGet.Config` in modo che non debba essere immessa per i comandi successivi.</span><span class="sxs-lookup"><span data-stu-id="64a1e-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="64a1e-106">Uso</span><span class="sxs-lookup"><span data-stu-id="64a1e-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="64a1e-107">dove `<source>` identifica il server e `<key>` è la chiave da salvare.</span><span class="sxs-lookup"><span data-stu-id="64a1e-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="64a1e-108">Se `<source>` viene omesso, viene utilizzato nuget.org.</span><span class="sxs-lookup"><span data-stu-id="64a1e-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="64a1e-109">La chiave API non viene usata per l'autenticazione con il feed privato.</span><span class="sxs-lookup"><span data-stu-id="64a1e-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="64a1e-110">Fare riferimento a [`nuget sources` comando](../cli-reference/cli-ref-sources.md) per gestire le credenziali per l'autenticazione con l'origine.</span><span class="sxs-lookup"><span data-stu-id="64a1e-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="64a1e-111">Le chiavi API possono essere ottenute dai singoli server NuGet.</span><span class="sxs-lookup"><span data-stu-id="64a1e-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="64a1e-112">Per creare e gestire APIKeys per nuget.org, fare riferimento a [Publish-API-Key](../../quickstart/includes/publish-api-key.md)</span><span class="sxs-lookup"><span data-stu-id="64a1e-112">To create and manage APIKeys for nuget.org refer to [publish-api-key](../../quickstart/includes/publish-api-key.md)</span></span>

## <a name="options"></a><span data-ttu-id="64a1e-113">Opzioni</span><span class="sxs-lookup"><span data-stu-id="64a1e-113">Options</span></span>

| <span data-ttu-id="64a1e-114">Opzione</span><span class="sxs-lookup"><span data-stu-id="64a1e-114">Option</span></span> | <span data-ttu-id="64a1e-115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="64a1e-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="64a1e-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="64a1e-116">ConfigFile</span></span> | <span data-ttu-id="64a1e-117">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="64a1e-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="64a1e-118">Se non specificato, viene usato `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="64a1e-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="64a1e-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="64a1e-119">ForceEnglishOutput</span></span> | <span data-ttu-id="64a1e-120">*(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese.</span><span class="sxs-lookup"><span data-stu-id="64a1e-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="64a1e-121">Guida</span><span class="sxs-lookup"><span data-stu-id="64a1e-121">Help</span></span> | <span data-ttu-id="64a1e-122">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="64a1e-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="64a1e-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="64a1e-123">NonInteractive</span></span> | <span data-ttu-id="64a1e-124">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="64a1e-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="64a1e-125">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="64a1e-125">Verbosity</span></span> | <span data-ttu-id="64a1e-126">Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*.</span><span class="sxs-lookup"><span data-stu-id="64a1e-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="64a1e-127">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="64a1e-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="64a1e-128">Esempi</span><span class="sxs-lookup"><span data-stu-id="64a1e-128">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
