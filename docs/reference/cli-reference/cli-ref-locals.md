---
title: Comando variabili locali dell'interfaccia della riga di comando di NuGet
description: Informazioni di riferimento per il comando locals di NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327808"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="eb4a1-103">Comando locals (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="eb4a1-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="eb4a1-104">**Si applica a:** &bullet; **versioni supportate** per l'utilizzo di pacchetti: 3.3+</span><span class="sxs-lookup"><span data-stu-id="eb4a1-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="eb4a1-105">Cancella o elenca le risorse NuGet locali, ad esempio la *cache HTTP*, la cartella *Global-Packages* e la cartella Temp.</span><span class="sxs-lookup"><span data-stu-id="eb4a1-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="eb4a1-106">Il `locals` comando può essere usato anche per visualizzare un elenco di tali percorsi.</span><span class="sxs-lookup"><span data-stu-id="eb4a1-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="eb4a1-107">Per ulteriori informazioni, vedere [gestione dei pacchetti globali e delle cartelle della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="eb4a1-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="eb4a1-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="eb4a1-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="eb4a1-109">dove `<folder>` è uno dei `all`, `http-cache` `global-packages` `temp` `plugins-cache` , `packages-cache` *(3,5 e versioni precedenti)* ,, *(3.4 +)* e *(4.8 +)* .</span><span class="sxs-lookup"><span data-stu-id="eb4a1-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="eb4a1-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="eb4a1-110">Options</span></span>

| <span data-ttu-id="eb4a1-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="eb4a1-111">Option</span></span> | <span data-ttu-id="eb4a1-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eb4a1-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eb4a1-113">Cancella</span><span class="sxs-lookup"><span data-stu-id="eb4a1-113">Clear</span></span> | <span data-ttu-id="eb4a1-114">Cancella la cartella specificata.</span><span class="sxs-lookup"><span data-stu-id="eb4a1-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="eb4a1-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="eb4a1-115">ConfigFile</span></span> | <span data-ttu-id="eb4a1-116">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="eb4a1-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="eb4a1-117">Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="eb4a1-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="eb4a1-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="eb4a1-118">ForceEnglishOutput</span></span> | <span data-ttu-id="eb4a1-119">*(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese.</span><span class="sxs-lookup"><span data-stu-id="eb4a1-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="eb4a1-120">Help</span><span class="sxs-lookup"><span data-stu-id="eb4a1-120">Help</span></span> | <span data-ttu-id="eb4a1-121">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="eb4a1-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="eb4a1-122">List</span><span class="sxs-lookup"><span data-stu-id="eb4a1-122">List</span></span> | <span data-ttu-id="eb4a1-123">Indica il percorso della cartella specificata o i percorsi di tutte le cartelle quando vengono utilizzati con *tutti*.</span><span class="sxs-lookup"><span data-stu-id="eb4a1-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="eb4a1-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="eb4a1-124">NonInteractive</span></span> | <span data-ttu-id="eb4a1-125">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="eb4a1-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="eb4a1-126">Verbosity</span><span class="sxs-lookup"><span data-stu-id="eb4a1-126">Verbosity</span></span> | <span data-ttu-id="eb4a1-127">Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*.</span><span class="sxs-lookup"><span data-stu-id="eb4a1-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="eb4a1-128">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="eb4a1-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="eb4a1-129">Esempi</span><span class="sxs-lookup"><span data-stu-id="eb4a1-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="eb4a1-130">Per altri esempi, vedere [gestione dei pacchetti globali e delle cartelle della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="eb4a1-130">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
