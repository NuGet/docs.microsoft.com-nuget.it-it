---
title: Comando config CLI di NuGet
description: Riferimento per il comando di configurazione NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 51c4c9937483e7f8a57356515c06a60c0f9e6f62
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327848"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="f682f-103">comando config (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="f682f-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="f682f-104">**Si applica a:** tutte le &bullet; **versioni supportate**: tutti</span><span class="sxs-lookup"><span data-stu-id="f682f-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="f682f-105">Ottiene o imposta i valori di configurazione NuGet.</span><span class="sxs-lookup"><span data-stu-id="f682f-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="f682f-106">Per ulteriori informazioni sull'utilizzo, vedere [configurazioni comuni di NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="f682f-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="f682f-107">Per informazioni dettagliate sui nomi di chiave consentiti, vedere il [riferimento al file di configurazione NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="f682f-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="f682f-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="f682f-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="f682f-109">dove `<name>` e`<value>` specificano una coppia chiave-valore da impostare nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="f682f-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="f682f-110">È possibile specificare il numero desiderato di coppie.</span><span class="sxs-lookup"><span data-stu-id="f682f-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="f682f-111">Per rimuovere un valore, specificare il nome e il `=` segno senza alcun valore.</span><span class="sxs-lookup"><span data-stu-id="f682f-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="f682f-112">Per i nomi di chiave consentiti, vedere informazioni di [riferimento sul file di configurazione NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="f682f-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="f682f-113">In NuGet 3.4 +, `<value>` può usare le [variabili di ambiente](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="f682f-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="f682f-114">Opzioni</span><span class="sxs-lookup"><span data-stu-id="f682f-114">Options</span></span>

| <span data-ttu-id="f682f-115">Opzione</span><span class="sxs-lookup"><span data-stu-id="f682f-115">Option</span></span> | <span data-ttu-id="f682f-116">DESCRIZIONE</span><span class="sxs-lookup"><span data-stu-id="f682f-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f682f-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="f682f-117">AsPath</span></span> | <span data-ttu-id="f682f-118">Restituisce il valore di configurazione come percorso, ignorato quando `-Set` si utilizza.</span><span class="sxs-lookup"><span data-stu-id="f682f-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="f682f-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f682f-119">ConfigFile</span></span> | <span data-ttu-id="f682f-120">File di configurazione NuGet da modificare.</span><span class="sxs-lookup"><span data-stu-id="f682f-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="f682f-121">Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="f682f-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f682f-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f682f-122">ForceEnglishOutput</span></span> | <span data-ttu-id="f682f-123">*(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese.</span><span class="sxs-lookup"><span data-stu-id="f682f-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f682f-124">Help</span><span class="sxs-lookup"><span data-stu-id="f682f-124">Help</span></span> | <span data-ttu-id="f682f-125">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="f682f-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="f682f-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f682f-126">NonInteractive</span></span> | <span data-ttu-id="f682f-127">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="f682f-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f682f-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="f682f-128">Verbosity</span></span> | <span data-ttu-id="f682f-129">Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*.</span><span class="sxs-lookup"><span data-stu-id="f682f-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f682f-130">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f682f-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="f682f-131">Esempi</span><span class="sxs-lookup"><span data-stu-id="f682f-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
