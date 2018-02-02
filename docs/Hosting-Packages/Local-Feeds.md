---
title: Configurazione dei feed NuGet locali | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Come creare un feed locale per i pacchetti NuGet usando le cartelle nella rete locale
keywords: Feed NuGet, raccolta NuGet, feed locale per i pacchetti
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0b8633db78b19fecddeb057a9f287ef971aef27a
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="local-feeds"></a><span data-ttu-id="cf7be-104">Feed locali</span><span class="sxs-lookup"><span data-stu-id="cf7be-104">Local feeds</span></span>

<span data-ttu-id="cf7be-105">I feed locali per i pacchetti NuGet sono semplicemente strutture di cartelle gerarchiche nella rete locale (o nel computer personale) in cui vengono posizionati i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cf7be-105">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="cf7be-106">Questi feed possono quindi essere usati come origini di pacchetto con tutte le altre operazioni NuGet tramite l'interfaccia della riga di comando, l'interfaccia utente di Gestione pacchetti e la console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cf7be-106">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="cf7be-107">Per abilitare l'origine, aggiungere il nome del percorso (ad esempio `\\myserver\packages`) all'elenco delle origini tramite l'[interfaccia utente di Gestione pacchetti](../tools/package-manager-ui.md#package-sources) o il comando [`nuget sources`](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="cf7be-107">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../tools/package-manager-ui.md#package-sources) or the [`nuget sources`](../tools/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="cf7be-108">Le strutture di cartelle gerarchiche sono supportate in NuGet 3.3+.</span><span class="sxs-lookup"><span data-stu-id="cf7be-108">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="cf7be-109">Le versioni precedenti di NuGet usano solo una singola cartella contenente i pacchetti, con prestazioni molto inferiori rispetto alla struttura gerarchica.</span><span class="sxs-lookup"><span data-stu-id="cf7be-109">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="cf7be-110">Inizializzazione e gestione delle cartelle gerarchiche</span><span class="sxs-lookup"><span data-stu-id="cf7be-110">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="cf7be-111">L'albero delle cartelle gerarchiche con versioni ha la struttura generale seguente:</span><span class="sxs-lookup"><span data-stu-id="cf7be-111">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="cf7be-112">NuGet crea questa struttura automaticamente quando si usa il comando [`nuget add`](../tools/cli-ref-add.md) per copiare un pacchetto nel feed:</span><span class="sxs-lookup"><span data-stu-id="cf7be-112">NuGet creates this structure automatically when you use the [`nuget add`](../tools/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="cf7be-113">Il comando `nuget add` funziona con un pacchetto alla volta e ciò può risultare poco pratico per la configurazione di un feed con più pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cf7be-113">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="cf7be-114">In questi casi, usare il comando [`nuget init`](../tools/cli-ref-init.md) per copiare tutti i pacchetti in una cartella nel feed, come se si eseguisse `nuget add` su ognuno singolarmente.</span><span class="sxs-lookup"><span data-stu-id="cf7be-114">In such cases, use the [`nuget init`](../tools/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="cf7be-115">Ad esempio, il comando seguente copia tutti i pacchetti da `c:\packages` a un albero gerarchico in `\\myserver\packages`:</span><span class="sxs-lookup"><span data-stu-id="cf7be-115">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="cf7be-116">Come con il comando `add`, `init` crea una cartella per ogni identificatore di pacchetto, ognuna delle quali contiene una cartella con numero di versione, all'interno della quale si trova il pacchetto appropriato.</span><span class="sxs-lookup"><span data-stu-id="cf7be-116">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
