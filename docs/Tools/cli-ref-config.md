---
title: Comando config NuGet CLI | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Riferimento per il comando config di nuget.exe
keywords: riferimento di configurazione NuGet, il comando di configurazione
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e3d08f210bd56fcb8eb701fc9b241a3ab45998ec
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="69579-104">comando config (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="69579-104">config command (NuGet CLI)</span></span>

<span data-ttu-id="69579-105">**Si applica a:** tutti &bullet; **le versioni supportate**: tutti</span><span class="sxs-lookup"><span data-stu-id="69579-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="69579-106">Ottiene o imposta i valori di configurazione NuGet.</span><span class="sxs-lookup"><span data-stu-id="69579-106">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="69579-107">Per ulteriori informazioni sulla sintassi, vedere [configurazione NuGet comportamento](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="69579-107">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="69579-108">Per ulteriori informazioni sui nomi di chiave consentiti, vedere il [riferimento al file di configurazione NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="69579-108">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="69579-109">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="69579-109">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="69579-110">dove `<name>` e `<value>` specificare una coppia chiave-valore da impostare nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="69579-110">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="69579-111">È possibile specificare un numero di coppie in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="69579-111">You can specify as many pairs as desired.</span></span> <span data-ttu-id="69579-112">Per rimuovere un valore, specificare il nome e il `=` sign ma nessun valore.</span><span class="sxs-lookup"><span data-stu-id="69579-112">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="69579-113">Per i nomi di chiave consentiti, vedere il [riferimento al file di configurazione NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="69579-113">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="69579-114">In NuGet 3.4 + `<value>` consente [le variabili di ambiente](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="69579-114">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="69579-115">Opzioni</span><span class="sxs-lookup"><span data-stu-id="69579-115">Options</span></span>

| <span data-ttu-id="69579-116">Opzione</span><span class="sxs-lookup"><span data-stu-id="69579-116">Option</span></span> | <span data-ttu-id="69579-117">Descrizione</span><span class="sxs-lookup"><span data-stu-id="69579-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="69579-118">AsPath</span><span class="sxs-lookup"><span data-stu-id="69579-118">AsPath</span></span> | <span data-ttu-id="69579-119">Restituisce la configurazione di valore come un percorso, ignorati quando `-Set` viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="69579-119">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="69579-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="69579-120">ConfigFile</span></span> | <span data-ttu-id="69579-121">Il file di configurazione NuGet da modificare.</span><span class="sxs-lookup"><span data-stu-id="69579-121">The NuGet configuration file to modify.</span></span> <span data-ttu-id="69579-122">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="69579-122">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="69579-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="69579-123">ForceEnglishOutput</span></span> | <span data-ttu-id="69579-124">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="69579-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="69579-125">?</span><span class="sxs-lookup"><span data-stu-id="69579-125">Help</span></span> | <span data-ttu-id="69579-126">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="69579-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="69579-127">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="69579-127">NonInteractive</span></span> | <span data-ttu-id="69579-128">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="69579-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="69579-129">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="69579-129">Verbosity</span></span> | <span data-ttu-id="69579-130">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="69579-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="69579-131">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="69579-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="69579-132">Esempi</span><span class="sxs-lookup"><span data-stu-id="69579-132">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
