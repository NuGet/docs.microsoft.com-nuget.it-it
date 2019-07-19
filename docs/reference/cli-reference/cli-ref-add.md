---
title: Comando di aggiunta CLI di NuGet
description: Riferimento per il comando Add di NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327858"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="91d8d-103">Comando add (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="91d8d-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="91d8d-104">**Si applica a**: &bullet; **versioni supportate**per la pubblicazione di pacchetti: 3.3+</span><span class="sxs-lookup"><span data-stu-id="91d8d-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="91d8d-105">Aggiunge un pacchetto specificato a un'origine pacchetto non HTTP (una cartella o un percorso UNC) in un layout gerarchico, in cui vengono create cartelle per l'ID del pacchetto e il numero di versione.</span><span class="sxs-lookup"><span data-stu-id="91d8d-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="91d8d-106">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="91d8d-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="91d8d-107">Quando si esegue il ripristino o l'aggiornamento con l'origine del pacchetto, il layout gerarchico garantisce prestazioni significativamente migliori.</span><span class="sxs-lookup"><span data-stu-id="91d8d-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="91d8d-108">Per espandere tutti i file del pacchetto nell'origine del pacchetto di destinazione, utilizzare l' `-Expand` opzione.</span><span class="sxs-lookup"><span data-stu-id="91d8d-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="91d8d-109">Ciò comporta in genere la visualizzazione di sottocartelle aggiuntive nella destinazione, ad esempio `tools` e. `lib`</span><span class="sxs-lookup"><span data-stu-id="91d8d-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="91d8d-110">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="91d8d-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="91d8d-111">dove `<packagePath>` è il percorso del pacchetto da aggiungere e `<sourcePath>` specifica l'origine del pacchetto basata su cartelle a cui verrà aggiunto il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="91d8d-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="91d8d-112">Le origini HTTP non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="91d8d-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="91d8d-113">Opzioni</span><span class="sxs-lookup"><span data-stu-id="91d8d-113">Options</span></span>

| <span data-ttu-id="91d8d-114">Opzione</span><span class="sxs-lookup"><span data-stu-id="91d8d-114">Option</span></span> | <span data-ttu-id="91d8d-115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="91d8d-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="91d8d-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="91d8d-116">ConfigFile</span></span> | <span data-ttu-id="91d8d-117">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="91d8d-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="91d8d-118">Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="91d8d-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="91d8d-119">Expand</span><span class="sxs-lookup"><span data-stu-id="91d8d-119">Expand</span></span> | <span data-ttu-id="91d8d-120">Aggiunge tutti i file del pacchetto all'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="91d8d-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="91d8d-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="91d8d-121">ForceEnglishOutput</span></span> | <span data-ttu-id="91d8d-122">*(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese.</span><span class="sxs-lookup"><span data-stu-id="91d8d-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="91d8d-123">Help</span><span class="sxs-lookup"><span data-stu-id="91d8d-123">Help</span></span> | <span data-ttu-id="91d8d-124">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="91d8d-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="91d8d-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="91d8d-125">NonInteractive</span></span> | <span data-ttu-id="91d8d-126">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="91d8d-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="91d8d-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="91d8d-127">Verbosity</span></span> | <span data-ttu-id="91d8d-128">Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*.</span><span class="sxs-lookup"><span data-stu-id="91d8d-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="91d8d-129">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="91d8d-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="91d8d-130">Esempi</span><span class="sxs-lookup"><span data-stu-id="91d8d-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
