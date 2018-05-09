---
title: Note sulla versione 2.2 di NuGet
description: Note sulla versione per NuGet 2.2 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 21f212de53da5faf1ec0762f97a840968b615b19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="33db2-103">Note sulla versione 2.2 di NuGet</span><span class="sxs-lookup"><span data-stu-id="33db2-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="33db2-104">[Note sulla versione di NuGet 2.1](../release-notes/nuget-2.1.md) | [note sulla versione 2.2.1 NuGet](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="33db2-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="33db2-105">2.2 NuGet è stato rilasciato il 12 dicembre 2012.</span><span class="sxs-lookup"><span data-stu-id="33db2-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="33db2-106">Avvio veloce di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="33db2-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="33db2-107">Una delle nuove funzionalità che è stato aggiunto in Visual Studio 2012 è stato il [finestra avvio veloce](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="33db2-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="33db2-108">2.2 NuGet estende questa finestra di dialogo che consente di inizializzare la finestra di dialogo di gestione di pacchetti con i termini di ricerca immessi in avvio veloce.</span><span class="sxs-lookup"><span data-stu-id="33db2-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="33db2-109">Nei risultati per la ricerca di pacchetti NuGet corrispondenti a 'jquery' immettendo 'jquery' in avvio veloce ora include, ad esempio, un'opzione.</span><span class="sxs-lookup"><span data-stu-id="33db2-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![NuGet in avvio veloce di Visual Studio](./media/quick-launch.png)

<span data-ttu-id="33db2-111">Se si seleziona questa opzione avvierà il standard NuGet package manager un'esperienza di ricerca per il termine 'jquery'.</span><span class="sxs-lookup"><span data-stu-id="33db2-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Finestra di dialogo Gestione pacchetti NuGet prepopolato](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="33db2-113">Specificare l'intera cartella di contenuto del pacchetto</span><span class="sxs-lookup"><span data-stu-id="33db2-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="33db2-114">Ora consente di specificare un'intera cartella in NuGet 2.2 il `<file>` elemento del `.nuspec` file da includere tutto il contenuto della cartella.</span><span class="sxs-lookup"><span data-stu-id="33db2-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="33db2-115">Ad esempio, il seguente causerà tutti gli script nella cartella script del pacchetto da aggiungere alla cartella contents\scripts quando il pacchetto viene installato in un progetto.</span><span class="sxs-lookup"><span data-stu-id="33db2-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="33db2-116">**Aggiornamento 6/24/16: le cartelle vuote nella cartella "content" vengono ignorate quando si installa il pacchetto.**</span><span class="sxs-lookup"><span data-stu-id="33db2-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="33db2-117">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="33db2-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="33db2-118">Installazione del pacchetto ha esito negativo per i progetti F # quando si utilizza la console di gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="33db2-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="33db2-119">Quando si tenta di installare un pacchetto NuGet in un progetto F # mediante la console di gestione del pacchetto, viene generata un'eccezione InvalidOperationException.</span><span class="sxs-lookup"><span data-stu-id="33db2-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="33db2-120">Stiamo lavorando attivamente con il team di F # per risolvere il problema, ma nel frattempo, la soluzione consiste nell'installare i pacchetti NuGet in progetti F # tramite una finestra di dialogo Gestione pacchetti NuGet anziché la console.</span><span class="sxs-lookup"><span data-stu-id="33db2-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="33db2-121">[Ulteriori informazioni sono disponibili sul sito CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="33db2-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="33db2-122">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="33db2-122">Bug Fixes</span></span>
<span data-ttu-id="33db2-123">NuGet 2.2 include varie correzioni di bug.</span><span class="sxs-lookup"><span data-stu-id="33db2-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="33db2-124">Per un elenco completo di lavoro gli elementi corretti in NuGet 2.2,. visualizzazione di [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="33db2-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
