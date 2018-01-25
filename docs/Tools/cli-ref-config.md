---
title: Comando config NuGet CLI | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando config di nuget.exe
keywords: riferimento di configurazione NuGet, il comando di configurazione
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 31abc5c1ade0aff9a2f23ec89ec7082acedb3653
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="67408-104">comando config (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="67408-104">config command (NuGet CLI)</span></span>

<span data-ttu-id="67408-105">**Si applica a:** tutti &bullet; **le versioni supportate**: tutti</span><span class="sxs-lookup"><span data-stu-id="67408-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="67408-106">Ottiene o imposta i valori di configurazione NuGet.</span><span class="sxs-lookup"><span data-stu-id="67408-106">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="67408-107">Per ulteriori informazioni sulla sintassi, vedere [configurazione NuGet comportamento](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="67408-107">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="67408-108">Per ulteriori informazioni sui nomi di chiave consentiti, vedere il [riferimento al file di configurazione NuGet](../Schema/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="67408-108">For details on allowable key names, refer to the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="67408-109">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="67408-109">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="67408-110">dove `<name>` e `<value>` specificare una coppia chiave-valore da impostare nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="67408-110">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="67408-111">È possibile specificare un numero di coppie in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="67408-111">You can specify as many pairs as desired.</span></span> <span data-ttu-id="67408-112">Per rimuovere un valore, specificare il nome e il `=` sign ma nessun valore.</span><span class="sxs-lookup"><span data-stu-id="67408-112">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="67408-113">Per i nomi di chiave consentiti, vedere il [riferimento al file di configurazione NuGet](../Schema/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="67408-113">For allowable key names, see the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

<span data-ttu-id="67408-114">In NuGet 3.4 + `<value>` consente [le variabili di ambiente](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="67408-114">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="67408-115">Opzioni</span><span class="sxs-lookup"><span data-stu-id="67408-115">Options</span></span>

| <span data-ttu-id="67408-116">Opzione</span><span class="sxs-lookup"><span data-stu-id="67408-116">Option</span></span> | <span data-ttu-id="67408-117">Descrizione</span><span class="sxs-lookup"><span data-stu-id="67408-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="67408-118">AsPath</span><span class="sxs-lookup"><span data-stu-id="67408-118">AsPath</span></span> | <span data-ttu-id="67408-119">Restituisce la configurazione di valore come un percorso, ignorati quando `-Set` viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="67408-119">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="67408-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="67408-120">ConfigFile</span></span> | <span data-ttu-id="67408-121">Il file di configurazione NuGet da modificare.</span><span class="sxs-lookup"><span data-stu-id="67408-121">The NuGet configuration file to modify.</span></span> <span data-ttu-id="67408-122">Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="67408-122">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="67408-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="67408-123">ForceEnglishOutput</span></span> | <span data-ttu-id="67408-124">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="67408-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="67408-125">?</span><span class="sxs-lookup"><span data-stu-id="67408-125">Help</span></span> | <span data-ttu-id="67408-126">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="67408-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="67408-127">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="67408-127">NonInteractive</span></span> | <span data-ttu-id="67408-128">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="67408-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="67408-129">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="67408-129">Verbosity</span></span> | <span data-ttu-id="67408-130">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="67408-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="67408-131">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="67408-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="67408-132">Esempi</span><span class="sxs-lookup"><span data-stu-id="67408-132">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
