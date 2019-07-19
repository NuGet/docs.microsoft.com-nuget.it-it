---
title: Comando della specifica CLI di NuGet
description: Informazioni di riferimento sul comando NuGet. exe spec
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327568"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="68223-103">comando spec (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="68223-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="68223-104">**Si applica a:** &bullet; **versioni supportate** per la creazione di pacchetti: tutti</span><span class="sxs-lookup"><span data-stu-id="68223-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="68223-105">Genera un `.nuspec` file per un nuovo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="68223-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="68223-106">Se viene eseguito nella stessa cartella del file di progetto (`.csproj`, `.vbproj`, `.fsproj`), `spec` crea un `.nuspec` file in formato token.</span><span class="sxs-lookup"><span data-stu-id="68223-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="68223-107">Per ulteriori informazioni, vedere [creazione di un pacchetto](../../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="68223-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="68223-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="68223-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="68223-109">dove `<packageID>` è un identificatore facoltativo del `.nuspec` pacchetto da salvare nel file.</span><span class="sxs-lookup"><span data-stu-id="68223-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="68223-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="68223-110">Options</span></span>

| <span data-ttu-id="68223-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="68223-111">Option</span></span> | <span data-ttu-id="68223-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="68223-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="68223-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="68223-113">AssemblyPath</span></span> | <span data-ttu-id="68223-114">Specifica il percorso dell'assembly da utilizzare per i metadati.</span><span class="sxs-lookup"><span data-stu-id="68223-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="68223-115">Force</span><span class="sxs-lookup"><span data-stu-id="68223-115">Force</span></span> | <span data-ttu-id="68223-116">Sovrascrive qualsiasi file esistente `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="68223-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="68223-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="68223-117">ForceEnglishOutput</span></span> | <span data-ttu-id="68223-118">*(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese.</span><span class="sxs-lookup"><span data-stu-id="68223-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="68223-119">Help</span><span class="sxs-lookup"><span data-stu-id="68223-119">Help</span></span> | <span data-ttu-id="68223-120">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="68223-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="68223-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="68223-121">NonInteractive</span></span> | <span data-ttu-id="68223-122">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="68223-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="68223-123">Verbosity</span><span class="sxs-lookup"><span data-stu-id="68223-123">Verbosity</span></span> | <span data-ttu-id="68223-124">Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*.</span><span class="sxs-lookup"><span data-stu-id="68223-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="68223-125">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="68223-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="68223-126">Esempi</span><span class="sxs-lookup"><span data-stu-id="68223-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
