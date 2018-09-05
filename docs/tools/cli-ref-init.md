---
title: Comando di NuGet CLI init
description: Informazioni di riferimento per il comando init nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551410"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="e3564-103">comando Init (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e3564-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="e3564-104">**Si applica a:** creazione del pacchetto &bullet; **le versioni supportate:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="e3564-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="e3564-105">Copia tutti i pacchetti da una cartella flat in una cartella di destinazione utilizzando un layout organizzato gerarchicamente, come descritto per il [Aggiungi comando](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="e3564-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="e3564-106">Vale a dire usando `init` equivale all'uso di `add` comando in ogni pacchetto nella cartella.</span><span class="sxs-lookup"><span data-stu-id="e3564-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="e3564-107">Come con `add`, la destinazione deve essere una cartella locale o un percorso UNC. I repository dei pacchetti HTTP, ad esempio nuget.org o server privati non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="e3564-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="e3564-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="e3564-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="e3564-109">in cui `<source>` è la cartella che contiene i pacchetti e `<destination>` è la cartella locale o il nome di percorso UNC in cui vengono copiati i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="e3564-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="e3564-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="e3564-110">Options</span></span>

| <span data-ttu-id="e3564-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="e3564-111">Option</span></span> | <span data-ttu-id="e3564-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e3564-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e3564-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e3564-113">ConfigFile</span></span> | <span data-ttu-id="e3564-114">Il file di configurazione di NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="e3564-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e3564-115">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.</span><span class="sxs-lookup"><span data-stu-id="e3564-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e3564-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e3564-116">ForceEnglishOutput</span></span> | <span data-ttu-id="e3564-117">*(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="e3564-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e3564-118">Expand</span><span class="sxs-lookup"><span data-stu-id="e3564-118">Expand</span></span> | <span data-ttu-id="e3564-119">Aggiunge tutti i file in ogni pacchetto che viene aggiunto all'origine del pacchetto; uguale allo `-Expand` con il `add` comando.</span><span class="sxs-lookup"><span data-stu-id="e3564-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="e3564-120">?</span><span class="sxs-lookup"><span data-stu-id="e3564-120">Help</span></span> | <span data-ttu-id="e3564-121">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="e3564-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="e3564-122">Non interattive</span><span class="sxs-lookup"><span data-stu-id="e3564-122">NonInteractive</span></span> | <span data-ttu-id="e3564-123">Elimina richieste di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e3564-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e3564-124">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="e3564-124">Verbosity</span></span> | <span data-ttu-id="e3564-125">Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="e3564-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="e3564-126">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e3564-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e3564-127">Esempi</span><span class="sxs-lookup"><span data-stu-id="e3564-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
