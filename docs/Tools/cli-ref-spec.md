---
title: Comando specifica CLI NuGet | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando specifica di nuget.exe
keywords: riferimento specifica NuGet, specifiche di comando
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc7e772e737a0f74929d13e2b126f7796b6d0dc7
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="4a684-104">Specifica di comando (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="4a684-104">spec command (NuGet CLI)</span></span>

<span data-ttu-id="4a684-105">**Si applica a:** creazione di pacchetti &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="4a684-105">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="4a684-106">Genera un `.nuspec` file per un nuovo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4a684-106">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="4a684-107">Se l'esecuzione nella stessa cartella un file di progetto (`.csproj`, `.vbproj`, `.fsproj`), `spec` crea un token `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="4a684-107">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="4a684-108">Per ulteriori informazioni, vedere [creazione di un pacchetto](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="4a684-108">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="4a684-109">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="4a684-109">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="4a684-110">dove `<packageID>` è un identificatore di pacchetto facoltativo per salvare il `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="4a684-110">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="4a684-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="4a684-111">Options</span></span>

| <span data-ttu-id="4a684-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="4a684-112">Option</span></span> | <span data-ttu-id="4a684-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a684-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4a684-114">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="4a684-114">AssemblyPath</span></span> | <span data-ttu-id="4a684-115">Specifica il percorso dell'assembly da usare per i metadati.</span><span class="sxs-lookup"><span data-stu-id="4a684-115">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="4a684-116">Force</span><span class="sxs-lookup"><span data-stu-id="4a684-116">Force</span></span> | <span data-ttu-id="4a684-117">Sovrascrive qualsiasi esistente `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="4a684-117">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="4a684-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4a684-118">ForceEnglishOutput</span></span> | <span data-ttu-id="4a684-119">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="4a684-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4a684-120">?</span><span class="sxs-lookup"><span data-stu-id="4a684-120">Help</span></span> | <span data-ttu-id="4a684-121">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="4a684-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="4a684-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="4a684-122">NonInteractive</span></span> | <span data-ttu-id="4a684-123">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="4a684-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4a684-124">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="4a684-124">Verbosity</span></span> | <span data-ttu-id="4a684-125">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="4a684-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="4a684-126">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4a684-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4a684-127">Esempi</span><span class="sxs-lookup"><span data-stu-id="4a684-127">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
