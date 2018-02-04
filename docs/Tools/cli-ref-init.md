---
title: Comando di NuGet CLI init | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando di nuget.exe init
keywords: NuGet init riferimento, il comando init
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6d7710cd024e2c2956fb73aa767c3be55b9fb0f9
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="fab20-104">comando Init (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fab20-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="fab20-105">**Si applica a:** creazione di pacchetti &bullet; **le versioni supportate:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="fab20-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="fab20-106">Copia tutti i pacchetti da una cartella in una cartella di destinazione utilizzando un layout organizzato gerarchicamente, come descritto per il [aggiungere comando](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="fab20-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="fab20-107">Vale a dire usando `init` equivale all'utilizzo di `add` comando in ogni pacchetto nella cartella.</span><span class="sxs-lookup"><span data-stu-id="fab20-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="fab20-108">Come con `add`, la destinazione deve essere una cartella locale o un percorso UNC. Repository di pacchetti HTTP, ad esempio nuget.org o server private non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="fab20-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="fab20-109">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="fab20-109">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="fab20-110">dove `<source>` è la cartella contenente i pacchetti e `<destination>` è la cartella locale o un nome di percorso UNC in cui vengono copiati i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="fab20-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="fab20-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="fab20-111">Options</span></span>

| <span data-ttu-id="fab20-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="fab20-112">Option</span></span> | <span data-ttu-id="fab20-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fab20-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fab20-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fab20-114">ConfigFile</span></span> | <span data-ttu-id="fab20-115">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="fab20-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fab20-116">Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="fab20-116">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="fab20-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fab20-117">ForceEnglishOutput</span></span> | <span data-ttu-id="fab20-118">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="fab20-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fab20-119">Expand</span><span class="sxs-lookup"><span data-stu-id="fab20-119">Expand</span></span> | <span data-ttu-id="fab20-120">Aggiunge tutti i file in ogni pacchetto che viene aggiunto all'origine del pacchetto; uguale a `-Expand` con il `add` comando.</span><span class="sxs-lookup"><span data-stu-id="fab20-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="fab20-121">?</span><span class="sxs-lookup"><span data-stu-id="fab20-121">Help</span></span> | <span data-ttu-id="fab20-122">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="fab20-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="fab20-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="fab20-123">NonInteractive</span></span> | <span data-ttu-id="fab20-124">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="fab20-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fab20-125">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="fab20-125">Verbosity</span></span> | <span data-ttu-id="fab20-126">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="fab20-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="fab20-127">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fab20-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fab20-128">Esempi</span><span class="sxs-lookup"><span data-stu-id="fab20-128">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
