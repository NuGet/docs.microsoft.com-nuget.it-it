---
title: Comando init CLI di NuGet
description: Informazioni di riferimento sul comando NuGet. exe init
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327778"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="b14d0-103">comando init (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="b14d0-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="b14d0-104">**Si applica a:** &bullet; **versioni supportate** per la creazione di pacchetti: 3.3+</span><span class="sxs-lookup"><span data-stu-id="b14d0-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="b14d0-105">Copia tutti i pacchetti da una cartella flat in una cartella di destinazione usando un layout gerarchico come descritto per il [comando Aggiungi](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="b14d0-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="b14d0-106">Ovvero, l'utilizzo `init` di equivale a utilizzare il `add` comando su ogni pacchetto nella cartella.</span><span class="sxs-lookup"><span data-stu-id="b14d0-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="b14d0-107">Come per `add`, la destinazione deve essere una cartella locale o un percorso UNC; I repository del pacchetto HTTP, ad esempio nuget.org o i server privati, non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="b14d0-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="b14d0-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="b14d0-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="b14d0-109">dove `<source>` è la cartella che contiene i `<destination>` pacchetti e è la cartella locale o il percorso UNC in cui vengono copiati i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="b14d0-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="b14d0-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="b14d0-110">Options</span></span>

| <span data-ttu-id="b14d0-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="b14d0-111">Option</span></span> | <span data-ttu-id="b14d0-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b14d0-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b14d0-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b14d0-113">ConfigFile</span></span> | <span data-ttu-id="b14d0-114">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="b14d0-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b14d0-115">Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="b14d0-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b14d0-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b14d0-116">ForceEnglishOutput</span></span> | <span data-ttu-id="b14d0-117">*(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese.</span><span class="sxs-lookup"><span data-stu-id="b14d0-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b14d0-118">Expand</span><span class="sxs-lookup"><span data-stu-id="b14d0-118">Expand</span></span> | <span data-ttu-id="b14d0-119">Aggiunge tutti i file in ogni pacchetto aggiunto all'origine del pacchetto. uguale a quello del `add`comando. `-Expand`</span><span class="sxs-lookup"><span data-stu-id="b14d0-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="b14d0-120">?</span><span class="sxs-lookup"><span data-stu-id="b14d0-120">Help</span></span> | <span data-ttu-id="b14d0-121">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="b14d0-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="b14d0-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b14d0-122">NonInteractive</span></span> | <span data-ttu-id="b14d0-123">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b14d0-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b14d0-124">Verbosity</span><span class="sxs-lookup"><span data-stu-id="b14d0-124">Verbosity</span></span> | <span data-ttu-id="b14d0-125">Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*.</span><span class="sxs-lookup"><span data-stu-id="b14d0-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b14d0-126">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b14d0-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b14d0-127">Esempi</span><span class="sxs-lookup"><span data-stu-id="b14d0-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
