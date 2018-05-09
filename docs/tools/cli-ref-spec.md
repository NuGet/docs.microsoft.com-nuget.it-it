---
title: Comando specifica di NuGet CLI
description: Riferimento per il comando specifica di nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68d661030ce7bcff7d7a3a1c96c07e149ad4ffea
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="a7021-103">Specifica di comando (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="a7021-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="a7021-104">**Si applica a:** creazione di pacchetti &bullet; **versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="a7021-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a7021-105">Genera un `.nuspec` file per un nuovo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a7021-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="a7021-106">Se l'esecuzione nella stessa cartella un file di progetto (`.csproj`, `.vbproj`, `.fsproj`), `spec` crea un token `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="a7021-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="a7021-107">Per ulteriori informazioni, vedere [creazione di un pacchetto](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="a7021-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a7021-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="a7021-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="a7021-109">dove `<packageID>` è un identificatore di pacchetto facoltativo per salvare il `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="a7021-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="a7021-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="a7021-110">Options</span></span>

| <span data-ttu-id="a7021-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="a7021-111">Option</span></span> | <span data-ttu-id="a7021-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7021-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a7021-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="a7021-113">AssemblyPath</span></span> | <span data-ttu-id="a7021-114">Specifica il percorso dell'assembly da usare per i metadati.</span><span class="sxs-lookup"><span data-stu-id="a7021-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="a7021-115">Force</span><span class="sxs-lookup"><span data-stu-id="a7021-115">Force</span></span> | <span data-ttu-id="a7021-116">Sovrascrive qualsiasi esistente `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="a7021-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="a7021-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a7021-117">ForceEnglishOutput</span></span> | <span data-ttu-id="a7021-118">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="a7021-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a7021-119">?</span><span class="sxs-lookup"><span data-stu-id="a7021-119">Help</span></span> | <span data-ttu-id="a7021-120">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="a7021-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="a7021-121">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="a7021-121">NonInteractive</span></span> | <span data-ttu-id="a7021-122">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="a7021-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a7021-123">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="a7021-123">Verbosity</span></span> | <span data-ttu-id="a7021-124">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="a7021-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a7021-125">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a7021-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a7021-126">Esempi</span><span class="sxs-lookup"><span data-stu-id="a7021-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
