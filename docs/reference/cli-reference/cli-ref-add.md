---
title: Comando di aggiunta CLI di NuGet
description: Riferimento per il comando nuget.exe Aggiungi
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 096d2f7a61a3c861ce2084368500ab8e8b21f212
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776091"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="b9168-103">comando Add (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="b9168-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="b9168-104">**Si applica a**: versioni supportate per la pubblicazione di pacchetti &bullet; : 3.3 +</span><span class="sxs-lookup"><span data-stu-id="b9168-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="b9168-105">Aggiunge un pacchetto specificato a un'origine pacchetto non HTTP (una cartella o un percorso UNC) in un layout gerarchico, in cui vengono create cartelle per l'ID del pacchetto e il numero di versione.</span><span class="sxs-lookup"><span data-stu-id="b9168-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="b9168-106">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b9168-106">For example:</span></span>

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

<span data-ttu-id="b9168-107">Quando si esegue il ripristino o l'aggiornamento con l'origine del pacchetto, il layout gerarchico garantisce prestazioni significativamente migliori.</span><span class="sxs-lookup"><span data-stu-id="b9168-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="b9168-108">Per espandere tutti i file del pacchetto nell'origine del pacchetto di destinazione, utilizzare l' `-Expand` opzione.</span><span class="sxs-lookup"><span data-stu-id="b9168-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="b9168-109">Ciò comporta in genere la visualizzazione di sottocartelle aggiuntive nella destinazione, ad esempio `tools` e `lib` .</span><span class="sxs-lookup"><span data-stu-id="b9168-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="b9168-110">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="b9168-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="b9168-111">dove `<packagePath>` è il percorso del pacchetto da aggiungere e `<sourcePath>` specifica l'origine del pacchetto basata su cartelle a cui verrà aggiunto il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b9168-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="b9168-112">Le origini HTTP non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="b9168-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="b9168-113">Opzioni</span><span class="sxs-lookup"><span data-stu-id="b9168-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="b9168-114">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="b9168-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b9168-115">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="b9168-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="b9168-116">Aggiunge tutti i file del pacchetto all'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b9168-116">Adds all the files in the package to the package source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="b9168-117">*(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="b9168-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>
<span data-ttu-id="b9168-118">Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="b9168-118">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="b9168-119">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="b9168-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="b9168-120">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b9168-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

   <span data-ttu-id="b9168-121">Specifica l'origine del pacchetto, ovvero una cartella o una condivisione UNC, a cui verranno aggiunti i nupkg.</span><span class="sxs-lookup"><span data-stu-id="b9168-121">Specifies the package source, which is a folder or UNC share, to which the nupkg will be added.</span></span> <span data-ttu-id="b9168-122">Le origini http non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="b9168-122">Http sources are not supported.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="b9168-123">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="b9168-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="b9168-124">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b9168-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b9168-125">Esempi</span><span class="sxs-lookup"><span data-stu-id="b9168-125">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
