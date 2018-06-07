---
title: NuGet CLI aggiungere comandi
description: Riferimento per il nuget.exe Aggiungi comando
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f229ca100463c556f9c4cefc49f52724a9c4ba77
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817610"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="f64e0-103">Comando add (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="f64e0-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="f64e0-104">**Si applica a**: la pubblicazione del pacchetto &bullet; **versioni supportate**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="f64e0-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="f64e0-105">Aggiunge un pacchetto specifico a un'origine del pacchetto non HTTP (una cartella o un percorso UNC) in un layout organizzato gerarchicamente, in cui vengono create le cartelle per il numero di ID e la versione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f64e0-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="f64e0-106">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="f64e0-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="f64e0-107">Durante il ripristino o l'aggiornamento in base all'origine del pacchetto, layout organizzato gerarchicamente fornisce un miglioramento significativo delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="f64e0-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="f64e0-108">Per espandere tutti i file del pacchetto all'origine del pacchetto di destinazione, utilizzare il `-Expand` passare.</span><span class="sxs-lookup"><span data-stu-id="f64e0-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="f64e0-109">Ciò comporta in genere nelle sottocartelle aggiuntive nella destinazione, ad esempio `tools` e `lib`.</span><span class="sxs-lookup"><span data-stu-id="f64e0-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="f64e0-110">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="f64e0-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="f64e0-111">dove `<packagePath>` sia il percorso per il pacchetto da aggiungere, e `<sourcePath>` specifica l'origine del pacchetto basati sulla cartella in cui verrà aggiunto il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f64e0-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="f64e0-112">Origini HTTP non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="f64e0-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="f64e0-113">Opzioni</span><span class="sxs-lookup"><span data-stu-id="f64e0-113">Options</span></span>

| <span data-ttu-id="f64e0-114">Opzione</span><span class="sxs-lookup"><span data-stu-id="f64e0-114">Option</span></span> | <span data-ttu-id="f64e0-115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f64e0-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f64e0-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f64e0-116">ConfigFile</span></span> | <span data-ttu-id="f64e0-117">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="f64e0-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f64e0-118">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="f64e0-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f64e0-119">Expand</span><span class="sxs-lookup"><span data-stu-id="f64e0-119">Expand</span></span> | <span data-ttu-id="f64e0-120">Aggiunge tutti i file del pacchetto per l'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f64e0-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="f64e0-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f64e0-121">ForceEnglishOutput</span></span> | <span data-ttu-id="f64e0-122">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="f64e0-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f64e0-123">?</span><span class="sxs-lookup"><span data-stu-id="f64e0-123">Help</span></span> | <span data-ttu-id="f64e0-124">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="f64e0-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="f64e0-125">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="f64e0-125">NonInteractive</span></span> | <span data-ttu-id="f64e0-126">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="f64e0-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f64e0-127">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="f64e0-127">Verbosity</span></span> | <span data-ttu-id="f64e0-128">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="f64e0-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f64e0-129">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f64e0-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f64e0-130">Esempi</span><span class="sxs-lookup"><span data-stu-id="f64e0-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
