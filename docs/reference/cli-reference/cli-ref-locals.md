---
title: Comando variabili locali dell'interfaccia della riga di comando di NuGet
description: Riferimento per il comando nuget.exe variabili locali
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 25feb29c7b96c47681cedd8208b8595952d3ca49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779194"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="5074d-103">comando locals (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="5074d-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="5074d-104">**Si applica a:** versioni supportate per l'utilizzo di pacchetti &bullet; **:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="5074d-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="5074d-105">Cancella o elenca le risorse NuGet locali, ad esempio la *cache HTTP*, la cartella *Global-Packages* e la cartella Temp.</span><span class="sxs-lookup"><span data-stu-id="5074d-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="5074d-106">Il `locals` comando può essere usato anche per visualizzare un elenco di tali percorsi.</span><span class="sxs-lookup"><span data-stu-id="5074d-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="5074d-107">Per ulteriori informazioni, vedere [gestione dei pacchetti globali e delle cartelle della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="5074d-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="5074d-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="5074d-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="5074d-109">dove `<folder>` è uno dei `all` , `http-cache` , `packages-cache` *(3,5 e versioni precedenti)*, `global-packages` , `temp` *(3.4 +)* e `plugins-cache` *(4.8 +)*.</span><span class="sxs-lookup"><span data-stu-id="5074d-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="5074d-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="5074d-110">Options</span></span>

- **`-Clear`**

  <span data-ttu-id="5074d-111">Cancella la cartella specificata.</span><span class="sxs-lookup"><span data-stu-id="5074d-111">Clears the specified folder.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="5074d-112">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="5074d-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5074d-113">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="5074d-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="5074d-114">*(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="5074d-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="5074d-115">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="5074d-115">Displays help information for the command.</span></span>

- **`-List`**

  <span data-ttu-id="5074d-116">Indica il percorso della cartella specificata o i percorsi di tutte le cartelle quando vengono utilizzati con *tutti*.</span><span class="sxs-lookup"><span data-stu-id="5074d-116">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="5074d-117">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5074d-117">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="5074d-118">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="5074d-118">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="5074d-119">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5074d-119">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5074d-120">Esempi</span><span class="sxs-lookup"><span data-stu-id="5074d-120">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="5074d-121">Per altri esempi, vedere [gestione dei pacchetti globali e delle cartelle della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="5074d-121">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
