---
title: Comando specifica di CLI di NuGet
description: Informazioni di riferimento per il comando specifica nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68b165751ab6794d2a01d7e466619b1ce4d7ed72
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546449"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="39550-103">comando Spec (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="39550-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="39550-104">**Si applica a:** creazione del pacchetto &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="39550-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="39550-105">Genera un `.nuspec` file per un nuovo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="39550-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="39550-106">Se eseguito nella stessa cartella un file di progetto (`.csproj`, `.vbproj`, `.fsproj`), `spec` consente di creare un token `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="39550-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="39550-107">Per altre informazioni, vedere [creazione di un pacchetto](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="39550-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="39550-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="39550-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="39550-109">in cui `<packageID>` è un identificatore di pacchetto facoltativo per salvare il `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="39550-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="39550-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="39550-110">Options</span></span>

| <span data-ttu-id="39550-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="39550-111">Option</span></span> | <span data-ttu-id="39550-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="39550-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="39550-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="39550-113">AssemblyPath</span></span> | <span data-ttu-id="39550-114">Specifica il percorso dell'assembly da utilizzare per i metadati.</span><span class="sxs-lookup"><span data-stu-id="39550-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="39550-115">Force</span><span class="sxs-lookup"><span data-stu-id="39550-115">Force</span></span> | <span data-ttu-id="39550-116">Sovrascrive tutte le classi esistenti `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="39550-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="39550-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="39550-117">ForceEnglishOutput</span></span> | <span data-ttu-id="39550-118">*(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="39550-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="39550-119">?</span><span class="sxs-lookup"><span data-stu-id="39550-119">Help</span></span> | <span data-ttu-id="39550-120">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="39550-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="39550-121">Non interattive</span><span class="sxs-lookup"><span data-stu-id="39550-121">NonInteractive</span></span> | <span data-ttu-id="39550-122">Elimina richieste di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="39550-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="39550-123">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="39550-123">Verbosity</span></span> | <span data-ttu-id="39550-124">Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="39550-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="39550-125">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="39550-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="39550-126">Esempi</span><span class="sxs-lookup"><span data-stu-id="39550-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
