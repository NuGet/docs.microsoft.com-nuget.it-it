---
title: Comando locals NuGet CLI
description: Informazioni di riferimento per il comando locals nuget.exe
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ea216c4651ba9619bc3b6a7ab52546fd299b0bb6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545028"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="5096f-103">Comando locals (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="5096f-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="5096f-104">**Si applica a:** consumo del pacchetto &bullet; **le versioni supportate:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="5096f-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="5096f-105">Cancella o elenca risorse NuGet locali, ad esempio la *http-cache*, *global-packages* cartella e la cartella temporanea.</span><span class="sxs-lookup"><span data-stu-id="5096f-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="5096f-106">Il `locals` comando può essere utilizzato anche per visualizzare un elenco di queste posizioni.</span><span class="sxs-lookup"><span data-stu-id="5096f-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="5096f-107">Per altre informazioni, vedere [gestione dei pacchetti globali e le cartelle cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="5096f-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="5096f-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="5096f-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="5096f-109">in cui `<folder>` è uno dei `all`, `http-cache`, `packages-cache` *(3.5 e versioni precedenti)*, `global-packages`, `temp` *(3.4 +)*, e `plugins-cache` *(4.8)*.</span><span class="sxs-lookup"><span data-stu-id="5096f-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="5096f-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="5096f-110">Options</span></span>

| <span data-ttu-id="5096f-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="5096f-111">Option</span></span> | <span data-ttu-id="5096f-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5096f-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5096f-113">Cancella</span><span class="sxs-lookup"><span data-stu-id="5096f-113">Clear</span></span> | <span data-ttu-id="5096f-114">Cancella la cartella specificata.</span><span class="sxs-lookup"><span data-stu-id="5096f-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="5096f-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5096f-115">ConfigFile</span></span> | <span data-ttu-id="5096f-116">Il file di configurazione di NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="5096f-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5096f-117">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.</span><span class="sxs-lookup"><span data-stu-id="5096f-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5096f-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5096f-118">ForceEnglishOutput</span></span> | <span data-ttu-id="5096f-119">*(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="5096f-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5096f-120">?</span><span class="sxs-lookup"><span data-stu-id="5096f-120">Help</span></span> | <span data-ttu-id="5096f-121">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="5096f-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="5096f-122">List</span><span class="sxs-lookup"><span data-stu-id="5096f-122">List</span></span> | <span data-ttu-id="5096f-123">Elenca il percorso della cartella specificata o i percorsi di tutte le cartelle quando abbinata *tutti*.</span><span class="sxs-lookup"><span data-stu-id="5096f-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="5096f-124">Non interattive</span><span class="sxs-lookup"><span data-stu-id="5096f-124">NonInteractive</span></span> | <span data-ttu-id="5096f-125">Elimina richieste di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5096f-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5096f-126">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="5096f-126">Verbosity</span></span> | <span data-ttu-id="5096f-127">Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="5096f-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5096f-128">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5096f-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5096f-129">Esempi</span><span class="sxs-lookup"><span data-stu-id="5096f-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="5096f-130">Per altri esempi, vedere [gestione dei pacchetti globali e le cartelle cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="5096f-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
