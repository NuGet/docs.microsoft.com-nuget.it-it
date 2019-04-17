---
title: Comando Aggiungi NuGet CLI
description: Informazioni di riferimento per il nuget.exe Aggiungi comando
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545834"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="468a3-103">Comando add (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="468a3-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="468a3-104">**Si applica a**: pubblicazione del pacchetto &bullet; **le versioni supportate**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="468a3-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="468a3-105">Aggiunge un pacchetto specifico a un'origine di pacchetti non HTTP (una cartella o percorso UNC) in un layout organizzato gerarchicamente, in cui vengono create cartelle per il numero di ID e la versione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="468a3-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="468a3-106">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="468a3-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="468a3-107">Durante il ripristino o l'aggiornamento in base all'origine del pacchetto, layout organizzato gerarchicamente offre prestazioni notevolmente migliori.</span><span class="sxs-lookup"><span data-stu-id="468a3-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="468a3-108">Per espandere tutti i file nel pacchetto per l'origine del pacchetto di destinazione, usare il `-Expand` passare.</span><span class="sxs-lookup"><span data-stu-id="468a3-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="468a3-109">Ciò comporta in genere presenti nelle sottocartelle aggiuntive visualizzati nella destinazione, ad esempio `tools` e `lib`.</span><span class="sxs-lookup"><span data-stu-id="468a3-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="468a3-110">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="468a3-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="468a3-111">in cui `<packagePath>` è il nome del percorso al pacchetto da aggiungere, e `<sourcePath>` specifica l'origine del pacchetto basato sulla cartella in cui verrà aggiunto il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="468a3-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="468a3-112">Non sono supportate le origini HTTP.</span><span class="sxs-lookup"><span data-stu-id="468a3-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="468a3-113">Opzioni</span><span class="sxs-lookup"><span data-stu-id="468a3-113">Options</span></span>

| <span data-ttu-id="468a3-114">Opzione</span><span class="sxs-lookup"><span data-stu-id="468a3-114">Option</span></span> | <span data-ttu-id="468a3-115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="468a3-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="468a3-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="468a3-116">ConfigFile</span></span> | <span data-ttu-id="468a3-117">Il file di configurazione di NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="468a3-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="468a3-118">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.</span><span class="sxs-lookup"><span data-stu-id="468a3-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="468a3-119">Expand</span><span class="sxs-lookup"><span data-stu-id="468a3-119">Expand</span></span> | <span data-ttu-id="468a3-120">Aggiunge tutti i file nel pacchetto per l'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="468a3-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="468a3-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="468a3-121">ForceEnglishOutput</span></span> | <span data-ttu-id="468a3-122">*(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="468a3-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="468a3-123">Help</span><span class="sxs-lookup"><span data-stu-id="468a3-123">Help</span></span> | <span data-ttu-id="468a3-124">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="468a3-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="468a3-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="468a3-125">NonInteractive</span></span> | <span data-ttu-id="468a3-126">Elimina richieste di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="468a3-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="468a3-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="468a3-127">Verbosity</span></span> | <span data-ttu-id="468a3-128">Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="468a3-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="468a3-129">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="468a3-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="468a3-130">Esempi</span><span class="sxs-lookup"><span data-stu-id="468a3-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
