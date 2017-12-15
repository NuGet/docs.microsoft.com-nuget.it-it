---
title: NuGet CLI aggiungere comando | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 4f68a016-ad4e-41fc-b869-88910fc5121e
description: Riferimento per il nuget.exe Aggiungi comando
keywords: NuGet Aggiungi riferimento, aggiungere il comando di pacchetto
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bf9a6e51dfbf1716ba40273487b76ae04c18e948
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="bda95-104">aggiungere il comando (CLI NuGet)</span><span class="sxs-lookup"><span data-stu-id="bda95-104">add command (NuGet CLI)</span></span>

<span data-ttu-id="bda95-105">**Si applica a**: la pubblicazione del pacchetto &bullet; **le versioni supportate**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="bda95-105">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="bda95-106">Aggiunge un pacchetto specifico a un'origine del pacchetto non HTTP (una cartella o un percorso UNC) in un layout organizzato gerarchicamente, in cui vengono create le cartelle per il numero di ID e la versione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bda95-106">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="bda95-107">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="bda95-107">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="bda95-108">Durante il ripristino o l'aggiornamento in base all'origine del pacchetto, layout organizzato gerarchicamente fornisce un miglioramento significativo delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="bda95-108">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="bda95-109">Per espandere tutti i file del pacchetto all'origine del pacchetto di destinazione, utilizzare il `-Expand` passare.</span><span class="sxs-lookup"><span data-stu-id="bda95-109">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="bda95-110">Ciò comporta in genere nelle sottocartelle aggiuntive nella destinazione, ad esempio `tools` e `lib`.</span><span class="sxs-lookup"><span data-stu-id="bda95-110">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="bda95-111">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="bda95-111">Usage</span></span>

```
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="bda95-112">dove `<packagePath>` sia il percorso per il pacchetto da aggiungere, e `<sourcePath>` specifica l'origine del pacchetto basati sulla cartella in cui verrà aggiunto il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bda95-112">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="bda95-113">Origini HTTP non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="bda95-113">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="bda95-114">Opzioni</span><span class="sxs-lookup"><span data-stu-id="bda95-114">Options</span></span>

| <span data-ttu-id="bda95-115">Opzione</span><span class="sxs-lookup"><span data-stu-id="bda95-115">Option</span></span> | <span data-ttu-id="bda95-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bda95-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bda95-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="bda95-117">ConfigFile</span></span> | <span data-ttu-id="bda95-118">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="bda95-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="bda95-119">Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bda95-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span>| 
| <span data-ttu-id="bda95-120">Expand</span><span class="sxs-lookup"><span data-stu-id="bda95-120">Expand</span></span> | <span data-ttu-id="bda95-121">Aggiunge tutti i file del pacchetto per l'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bda95-121">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="bda95-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="bda95-122">ForceEnglishOutput</span></span> | <span data-ttu-id="bda95-123">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="bda95-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="bda95-124">?</span><span class="sxs-lookup"><span data-stu-id="bda95-124">Help</span></span> | <span data-ttu-id="bda95-125">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="bda95-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="bda95-126">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="bda95-126">NonInteractive</span></span> | <span data-ttu-id="bda95-127">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="bda95-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="bda95-128">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="bda95-128">Verbosity</span></span> | <span data-ttu-id="bda95-129">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="bda95-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="bda95-130">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="bda95-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="bda95-131">Esempi</span><span class="sxs-lookup"><span data-stu-id="bda95-131">Examples</span></span>

```
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
