---
title: Panoramica e flusso di lavoro dell'uso di pacchetti NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Panoramica del processo di utilizzo dei pacchetti NuGet in un progetto, con collegamenti ad altre parti specifiche del processo.
keywords: Utilizzo di pacchetti NuGet, panoramica dell'utilizzo di pacchetti NuGet, flusso di lavoro dell'utilizzo di pacchetti NuGet, flusso di lavoro dell'utilizzo dei pacchetti, panoramica dell'utilizzo dei pacchetti
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 731e0d3eb4ccb887624e4e46a18b4cc77857a784
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/15/2018
---
# <a name="package-consumption-workflow"></a><span data-ttu-id="239ed-104">Flusso di lavoro dell'utilizzo di pacchetti</span><span class="sxs-lookup"><span data-stu-id="239ed-104">Package consumption workflow</span></span>

<span data-ttu-id="239ed-105">Tra nuget.org e le raccolte di pacchetti private che un'organizzazione può stabilire, è possibile trovare decine di migliaia di pacchetti estremamente utili da usare all'interno di app e servizi.</span><span class="sxs-lookup"><span data-stu-id="239ed-105">Between nuget.org and private package galleries that your organization might establish, you can find tens of thousands of highly useful packages to use in your apps and services.</span></span> <span data-ttu-id="239ed-106">Ma indipendentemente dall'origine, l'utilizzo di un pacchetto segue lo stesso flusso di lavoro generale illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="239ed-106">But regardless of the source, consuming a package follows the same general workflow as shown below.</span></span> <span data-ttu-id="239ed-107">Per informazioni dettagliate, vedere [Ricerca e scelta di pacchetti](../consume-packages/finding-and-choosing-packages.md) e [Modi per installare pacchetti NuGet](ways-to-install-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="239ed-107">For details, see [Finding and Choosing Packages](../consume-packages/finding-and-choosing-packages.md) and [Different ways to install a NuGet package](ways-to-install-a-package.md).</span></span>

![Flusso di selezione di un'origine pacchetto, ricerca di un pacchetto, installazione di un pacchetto in un progetto, aggiunta di un'istruzione Using e chiamate all'API del pacchetto](media/Overview-01-GeneralFlow.png)

<span data-ttu-id="239ed-109">\* _Tranne che con `nuget install` dalla riga di comando, nel qual caso è necessario modificare i file di configurazione manualmente. Vedere [install command reference](../tools/cli-ref-install.md) (Informazioni di riferimento sul comando install)._</span><span class="sxs-lookup"><span data-stu-id="239ed-109">\* _Except with `nuget install` from the command-line, in which case it's necessary to edit the configuration files by hand. See the [install command reference](../tools/cli-ref-install.md)._</span></span>

<span data-ttu-id="239ed-110">NuGet memorizza l'identità e il numero di versione di ogni pacchetto installato, registrandoli in [`packages.config`](../reference/packages-config.md) o nel file di progetto, a seconda del tipo di progetto e della versione di NuGet in uso.</span><span class="sxs-lookup"><span data-stu-id="239ed-110">NuGet remembers the identity and version number of each installed package, recording it in either [`packages.config`](../reference/packages-config.md) or the project file, depending on project type and your version of NuGet.</span></span> <span data-ttu-id="239ed-111">Con NuGet 4.0 +, [l'archiviazione delle dipendenze in file di progetto o PackageReference](../consume-packages/package-references-in-project-files.md) è in genere l'impostazione predefinita, anche se è configurabile in Visual Studio tramite le [opzioni dell'interfaccia utente di Gestione pacchetti](../tools/package-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="239ed-111">With NuGet 4.0+, [storing dependencies in the project file, or PackageReference](../consume-packages/package-references-in-project-files.md) is generally the default, although this is configurable in Visual Studio through the [Package Manager UI options](../tools/package-manager-ui.md).</span></span> <span data-ttu-id="239ed-112">In tutti i casi, è possibile esaminare il file appropriato in qualsiasi momento per visualizzare l'elenco completo delle dipendenze per il progetto.</span><span class="sxs-lookup"><span data-stu-id="239ed-112">In any case, you can look in the appropriate file at any time to see the full list of dependencies for your project.</span></span>

> [!Tip]
> <span data-ttu-id="239ed-113">È consigliabile verificare sempre la licenza per ogni pacchetto che si intende usare nel software.</span><span class="sxs-lookup"><span data-stu-id="239ed-113">It's prudent to always check the license for each package you intend to use in your software.</span></span> <span data-ttu-id="239ed-114">Su nuget.org è disponibile un collegamento **License Info** (Informazioni di licenza) sul lato destro della pagina di descrizione di ogni pacchetto.</span><span class="sxs-lookup"><span data-stu-id="239ed-114">On nuget.org, you find a **License Info** link on the right side of each package's description page.</span></span> <span data-ttu-id="239ed-115">Se per un pacchetto non sono specificate le condizioni di licenza, contattare il proprietario del pacchetto direttamente usando il collegamento **Contact owners** (Contatta proprietari) nella pagina del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="239ed-115">If a package does not specify license terms, contact the package owner directly using the **Contact owners** link on the package page.</span></span> <span data-ttu-id="239ed-116">Microsoft non concede in licenza all'utente alcuna proprietà intellettuale dei provider di pacchetti di terze parti e non è responsabile delle informazioni fornite da terze parti.</span><span class="sxs-lookup"><span data-stu-id="239ed-116">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

<span data-ttu-id="239ed-117">Durante l'installazione dei pacchetti, NuGet verifica in genere se il pacchetto è già disponibile nella relativa cache.</span><span class="sxs-lookup"><span data-stu-id="239ed-117">When installing packages, NuGet typically checks if the package is already available from its cache.</span></span> <span data-ttu-id="239ed-118">È possibile cancellare manualmente questa cache dalla riga di comando, come descritto in [Gestione delle cache NuGet](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="239ed-118">You can manually clear this cache from the command line, as described on [Managing the NuGet cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

<span data-ttu-id="239ed-119">NuGet verifica inoltre che i framework di destinazione supportati dal pacchetto siano compatibili con il progetto.</span><span class="sxs-lookup"><span data-stu-id="239ed-119">NuGet also makes sure that the target frameworks supported by the package are compatible with your project.</span></span> <span data-ttu-id="239ed-120">Se il pacchetto non contiene assembly compatibili, NuGet restituirà un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="239ed-120">If the package does not contain compatible assemblies, NuGet will give you an error message.</span></span> <span data-ttu-id="239ed-121">Vedere [Risoluzione degli errori dei pacchetti incompatibili](dependency-resolution.md#resolving-incompatible-package-errors).</span><span class="sxs-lookup"><span data-stu-id="239ed-121">See [Resolving incompatible package errors](dependency-resolution.md#resolving-incompatible-package-errors).</span></span>

<span data-ttu-id="239ed-122">Quando si aggiunge il codice del progetto a un repository di origine, in genere non si includono i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="239ed-122">When adding project code to a source repository, you typically don't include NuGet packages.</span></span> <span data-ttu-id="239ed-123">Gli utenti che clonano successivamente il repository, operazione che include agenti di compilazione in sistemi come Visual Studio Team Services, devono ripristinare i pacchetti necessari prima di eseguire una compilazione:</span><span class="sxs-lookup"><span data-stu-id="239ed-123">Those who later clone the repository, which includes build agents on systems like Visual Studio Team Services, must restore the necessary packages prior to running a build:</span></span>

![Flusso di ripristino dei pacchetti NuGet tramite la clonazione di un repository e l'uso di un comando di ripristino](media/Overview-02-RestoreFlow.png)

<span data-ttu-id="239ed-125">L'opzione [Ripristino pacchetto](../consume-packages/package-restore.md) usa le informazioni nel file di progetto o `packages.config` per reinstallare tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="239ed-125">[Package Restore](../consume-packages/package-restore.md) uses the information in the project file or `packages.config` to reinstall all dependencies.</span></span> <span data-ttu-id="239ed-126">Si noti che ci sono differenze nel processo interessato, come descritto in [Risoluzione delle dipendenze](../consume-packages/dependency-resolution.md).</span><span class="sxs-lookup"><span data-stu-id="239ed-126">Note that there are differences in the process involved, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span>

<span data-ttu-id="239ed-127">In alcuni casi è necessario reinstallare i pacchetti che sono già inclusi in un progetto, reinstallando anche le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="239ed-127">Occasionally it's necessary to reinstall packages that are already included in a project, which may also reinstall dependencies.</span></span> <span data-ttu-id="239ed-128">Si tratta di un'operazione semplice da eseguire con il comando `reinstall` tramite la riga di comando di NuGet o la console di Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="239ed-128">This is easy to do using the `reinstall` command via the NuGet command line or the NuGet Package Manager Console.</span></span> <span data-ttu-id="239ed-129">Per maggiori dettagli, vedere [Reinstallazione e aggiornamento di pacchetti](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="239ed-129">For details, see [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>

<span data-ttu-id="239ed-130">Infine, il comportamento di NuGet è determinato dai file di configurazione `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="239ed-130">Finally, NuGet's behavior is driven by `Nuget.Config` configuration files.</span></span> <span data-ttu-id="239ed-131">È possibile usare più file per centralizzare determinate impostazioni a livelli diversi, come illustrato in [Configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="239ed-131">Multiple files can be used to centralize certain settings at different levels, as explained in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="239ed-132">In conclusione, con i pacchetti NuGet la codifica è produttiva.</span><span class="sxs-lookup"><span data-stu-id="239ed-132">Enjoy your productive coding with NuGet packages!</span></span>