---
title: Comando della specifica CLI di NuGet
description: Riferimento per il comando nuget.exe spec
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17603fa30a75c7906f867c96c5d77f31732eaa59
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622564"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="9f270-103">comando spec (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="9f270-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="9f270-104">**Si applica a:** versioni supportate per la creazione di pacchetti &bullet; **:** tutti</span><span class="sxs-lookup"><span data-stu-id="9f270-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="9f270-105">Genera un `.nuspec` file per un nuovo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9f270-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="9f270-106">Se viene eseguito nella stessa cartella del file di progetto ( `.csproj` , `.vbproj` , `.fsproj` ), `spec` Crea un file in `.nuspec` formato token.</span><span class="sxs-lookup"><span data-stu-id="9f270-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="9f270-107">Per ulteriori informazioni, vedere [creazione di un pacchetto](../../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="9f270-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="9f270-108">Uso</span><span class="sxs-lookup"><span data-stu-id="9f270-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="9f270-109">dove `<packageID>` è un identificatore facoltativo del pacchetto da salvare nel `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="9f270-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="9f270-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="9f270-110">Options</span></span>

- **`-AssemblyPath`**

  <span data-ttu-id="9f270-111">Specifica il percorso dell'assembly da utilizzare per i metadati.</span><span class="sxs-lookup"><span data-stu-id="9f270-111">Specifies the path to the assembly to use for metadata.</span></span>

- **`-Force`**

  <span data-ttu-id="9f270-112">Sovrascrive qualsiasi `.nuspec` file esistente.</span><span class="sxs-lookup"><span data-stu-id="9f270-112">Overwrites any existing `.nuspec` file.</span></span>


- **`-ForceEnglishOutput`**

  <span data-ttu-id="9f270-113">*(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="9f270-113">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="9f270-114">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="9f270-114">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="9f270-115">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="9f270-115">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="9f270-116">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="9f270-116">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="9f270-117">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9f270-117">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9f270-118">Esempi</span><span class="sxs-lookup"><span data-stu-id="9f270-118">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
