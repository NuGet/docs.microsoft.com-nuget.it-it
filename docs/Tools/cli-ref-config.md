---
title: Comando config NuGet CLI
description: Riferimento per il comando config di nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 414eb8386f949347772f33170de881534dc71482
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="31290-103">comando config (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="31290-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="31290-104">**Si applica a:** tutti &bullet; **le versioni supportate**: tutti</span><span class="sxs-lookup"><span data-stu-id="31290-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="31290-105">Ottiene o imposta i valori di configurazione NuGet.</span><span class="sxs-lookup"><span data-stu-id="31290-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="31290-106">Per ulteriori informazioni sulla sintassi, vedere [configurazione NuGet comportamento](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="31290-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="31290-107">Per ulteriori informazioni sui nomi di chiave consentiti, vedere il [riferimento al file di configurazione NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="31290-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="31290-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="31290-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="31290-109">dove `<name>` e `<value>` specificare una coppia chiave-valore da impostare nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="31290-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="31290-110">È possibile specificare un numero di coppie in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="31290-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="31290-111">Per rimuovere un valore, specificare il nome e il `=` sign ma nessun valore.</span><span class="sxs-lookup"><span data-stu-id="31290-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="31290-112">Per i nomi di chiave consentiti, vedere il [riferimento al file di configurazione NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="31290-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="31290-113">In NuGet 3.4 + `<value>` consente [le variabili di ambiente](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="31290-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="31290-114">Opzioni</span><span class="sxs-lookup"><span data-stu-id="31290-114">Options</span></span>

| <span data-ttu-id="31290-115">Opzione</span><span class="sxs-lookup"><span data-stu-id="31290-115">Option</span></span> | <span data-ttu-id="31290-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="31290-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="31290-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="31290-117">AsPath</span></span> | <span data-ttu-id="31290-118">Restituisce la configurazione di valore come un percorso, ignorati quando `-Set` viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="31290-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="31290-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="31290-119">ConfigFile</span></span> | <span data-ttu-id="31290-120">Il file di configurazione NuGet da modificare.</span><span class="sxs-lookup"><span data-stu-id="31290-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="31290-121">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="31290-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="31290-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="31290-122">ForceEnglishOutput</span></span> | <span data-ttu-id="31290-123">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="31290-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="31290-124">?</span><span class="sxs-lookup"><span data-stu-id="31290-124">Help</span></span> | <span data-ttu-id="31290-125">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="31290-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="31290-126">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="31290-126">NonInteractive</span></span> | <span data-ttu-id="31290-127">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="31290-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="31290-128">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="31290-128">Verbosity</span></span> | <span data-ttu-id="31290-129">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="31290-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="31290-130">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="31290-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="31290-131">Esempi</span><span class="sxs-lookup"><span data-stu-id="31290-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
