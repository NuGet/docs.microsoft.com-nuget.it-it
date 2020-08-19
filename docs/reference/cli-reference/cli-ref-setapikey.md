---
title: Comando setApiKey dell'interfaccia della riga di comando NuGet
description: Riferimento per il comando nuget.exe setApiKey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b84d4257c580f6e734c26ebfc589be27bea10c82
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622811"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="c591d-103">comando setApiKey (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="c591d-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="c591d-104">**Si applica a:** utilizzo del pacchetto, pubblicazione delle &bullet; **versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="c591d-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c591d-105">Salva una chiave API per un URL del server specificato in in `NuGet.Config` modo che non debba essere immessa per i comandi successivi.</span><span class="sxs-lookup"><span data-stu-id="c591d-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="c591d-106">Uso</span><span class="sxs-lookup"><span data-stu-id="c591d-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="c591d-107">dove `<source>` identifica il server e `<key>` è la chiave da salvare.</span><span class="sxs-lookup"><span data-stu-id="c591d-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="c591d-108">Se `<source>` viene omesso, viene utilizzato NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c591d-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="c591d-109">La chiave API non viene usata per l'autenticazione con il feed privato.</span><span class="sxs-lookup"><span data-stu-id="c591d-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="c591d-110">Fare riferimento al [ `nuget sources` comando](../cli-reference/cli-ref-sources.md) per gestire le credenziali per l'autenticazione con l'origine.</span><span class="sxs-lookup"><span data-stu-id="c591d-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="c591d-111">Le chiavi API possono essere ottenute dai singoli server NuGet.</span><span class="sxs-lookup"><span data-stu-id="c591d-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="c591d-112">Per creare e gestire APIKeys per nuget.org, vedere [acquisizione-an-API-Key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span><span class="sxs-lookup"><span data-stu-id="c591d-112">To create and manage APIKeys for nuget.org refer to [acquire-an-api-key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span></span>

## <a name="options"></a><span data-ttu-id="c591d-113">Opzioni</span><span class="sxs-lookup"><span data-stu-id="c591d-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="c591d-114">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="c591d-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c591d-115">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="c591d-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="c591d-116">*(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="c591d-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="c591d-117">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="c591d-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="c591d-118">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c591d-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="c591d-119">URL del server in cui la chiave API è valida.</span><span class="sxs-lookup"><span data-stu-id="c591d-119">Server URL where the API key is valid.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="c591d-120">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="c591d-120">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="c591d-121">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c591d-121">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c591d-122">Esempi</span><span class="sxs-lookup"><span data-stu-id="c591d-122">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
