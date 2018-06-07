---
title: Comando specifica di NuGet CLI
description: Riferimento per il comando specifica di nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17d3c5fc083f52fd9ab4a854ad358995bc55293b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817086"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="eb5c4-103">Specifica di comando (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="eb5c4-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="eb5c4-104">**Si applica a:** creazione di pacchetti &bullet; **versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="eb5c4-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="eb5c4-105">Genera un `.nuspec` file per un nuovo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="eb5c4-106">Se l'esecuzione nella stessa cartella un file di progetto (`.csproj`, `.vbproj`, `.fsproj`), `spec` crea un token `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="eb5c4-107">Per ulteriori informazioni, vedere [creazione di un pacchetto](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="eb5c4-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="eb5c4-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="eb5c4-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="eb5c4-109">dove `<packageID>` è un identificatore di pacchetto facoltativo per salvare il `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="eb5c4-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="eb5c4-110">Options</span></span>

| <span data-ttu-id="eb5c4-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="eb5c4-111">Option</span></span> | <span data-ttu-id="eb5c4-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eb5c4-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eb5c4-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="eb5c4-113">AssemblyPath</span></span> | <span data-ttu-id="eb5c4-114">Specifica il percorso dell'assembly da usare per i metadati.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="eb5c4-115">Force</span><span class="sxs-lookup"><span data-stu-id="eb5c4-115">Force</span></span> | <span data-ttu-id="eb5c4-116">Sovrascrive qualsiasi esistente `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="eb5c4-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="eb5c4-117">ForceEnglishOutput</span></span> | <span data-ttu-id="eb5c4-118">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="eb5c4-119">?</span><span class="sxs-lookup"><span data-stu-id="eb5c4-119">Help</span></span> | <span data-ttu-id="eb5c4-120">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="eb5c4-121">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="eb5c4-121">NonInteractive</span></span> | <span data-ttu-id="eb5c4-122">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="eb5c4-123">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="eb5c4-123">Verbosity</span></span> | <span data-ttu-id="eb5c4-124">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="eb5c4-125">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="eb5c4-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="eb5c4-126">Esempi</span><span class="sxs-lookup"><span data-stu-id="eb5c4-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
