---
title: Comando init NuGet CLI
description: Riferimento per il comando di nuget.exe init
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4fda33aabd51fbbf0e5559baaa42af065366ba4
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817818"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="49173-103">comando Init (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="49173-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="49173-104">**Si applica a:** creazione di pacchetti &bullet; **versioni supportate:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="49173-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="49173-105">Copia tutti i pacchetti da una cartella in una cartella di destinazione utilizzando un layout organizzato gerarchicamente, come descritto per il [aggiungere comando](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="49173-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="49173-106">Vale a dire usando `init` equivale all'utilizzo di `add` comando in ogni pacchetto nella cartella.</span><span class="sxs-lookup"><span data-stu-id="49173-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="49173-107">Come con `add`, la destinazione deve essere una cartella locale o un percorso UNC. Repository di pacchetti HTTP, ad esempio nuget.org o server private non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="49173-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="49173-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="49173-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="49173-109">dove `<source>` è la cartella contenente i pacchetti e `<destination>` è la cartella locale o un nome di percorso UNC in cui vengono copiati i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="49173-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="49173-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="49173-110">Options</span></span>

| <span data-ttu-id="49173-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="49173-111">Option</span></span> | <span data-ttu-id="49173-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="49173-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="49173-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="49173-113">ConfigFile</span></span> | <span data-ttu-id="49173-114">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="49173-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="49173-115">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="49173-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="49173-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="49173-116">ForceEnglishOutput</span></span> | <span data-ttu-id="49173-117">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="49173-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="49173-118">Expand</span><span class="sxs-lookup"><span data-stu-id="49173-118">Expand</span></span> | <span data-ttu-id="49173-119">Aggiunge tutti i file in ogni pacchetto che viene aggiunto all'origine del pacchetto; uguale a `-Expand` con il `add` comando.</span><span class="sxs-lookup"><span data-stu-id="49173-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="49173-120">?</span><span class="sxs-lookup"><span data-stu-id="49173-120">Help</span></span> | <span data-ttu-id="49173-121">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="49173-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="49173-122">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="49173-122">NonInteractive</span></span> | <span data-ttu-id="49173-123">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="49173-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="49173-124">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="49173-124">Verbosity</span></span> | <span data-ttu-id="49173-125">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="49173-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="49173-126">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="49173-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="49173-127">Esempi</span><span class="sxs-lookup"><span data-stu-id="49173-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
