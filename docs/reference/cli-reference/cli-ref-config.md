---
title: Comando config CLI di NuGet
description: Riferimento per il comando nuget.exe config
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3d50c12e34f71d7a62fe177da1dbb33eb702347a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775966"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="cee1b-103">comando config (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="cee1b-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="cee1b-104">**Si applica a:** tutte le &bullet; **versioni supportate**: tutti</span><span class="sxs-lookup"><span data-stu-id="cee1b-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="cee1b-105">Ottiene o imposta i valori di configurazione NuGet.</span><span class="sxs-lookup"><span data-stu-id="cee1b-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="cee1b-106">Per ulteriori informazioni sull'utilizzo, vedere [configurazioni comuni di NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="cee1b-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="cee1b-107">Per informazioni dettagliate sui nomi di chiave consentiti, vedere il [riferimento al file di configurazione NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="cee1b-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="cee1b-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="cee1b-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="cee1b-109">dove `<name>` e `<value>` specificano una coppia chiave-valore da impostare nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="cee1b-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="cee1b-110">È possibile specificare il numero desiderato di coppie.</span><span class="sxs-lookup"><span data-stu-id="cee1b-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="cee1b-111">Per rimuovere un valore, specificare il nome e il `=` segno senza alcun valore.</span><span class="sxs-lookup"><span data-stu-id="cee1b-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="cee1b-112">Per i nomi di chiave consentiti, vedere informazioni di [riferimento sul file di configurazione NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="cee1b-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="cee1b-113">In NuGet 3.4 +, `<value>` può usare le [variabili di ambiente](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="cee1b-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="cee1b-114">Opzioni</span><span class="sxs-lookup"><span data-stu-id="cee1b-114">Options</span></span>


- **`AsPath`**

  <span data-ttu-id="cee1b-115">Restituisce il valore di configurazione come percorso, ignorato quando `-Set` si utilizza.</span><span class="sxs-lookup"><span data-stu-id="cee1b-115">Returns the config value as a path, ignored when `-Set` is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="cee1b-116">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="cee1b-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cee1b-117">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="cee1b-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="cee1b-118">*(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="cee1b-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="cee1b-119">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="cee1b-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="cee1b-120">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="cee1b-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-Set`**

  <span data-ttu-id="cee1b-121">Una per più coppie chiave-valore da impostare nel file config.</span><span class="sxs-lookup"><span data-stu-id="cee1b-121">One on more key-value pairs to be set in config.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="cee1b-122">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="cee1b-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="cee1b-123">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cee1b-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="cee1b-124">Esempi</span><span class="sxs-lookup"><span data-stu-id="cee1b-124">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
