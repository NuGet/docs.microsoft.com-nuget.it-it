---
title: Note sulla versione di NuGet 2,2
description: Note sulla versione per NuGet 2,2, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780439"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="04dc7-103">Note sulla versione di NuGet 2,2</span><span class="sxs-lookup"><span data-stu-id="04dc7-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="04dc7-104">Note sulla versione di [NuGet 2,1](../release-notes/nuget-2.1.md)  |  [Note sulla versione di NuGet 2.2.1](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="04dc7-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="04dc7-105">NuGet 2,2 è stato rilasciato il 12 dicembre 2012.</span><span class="sxs-lookup"><span data-stu-id="04dc7-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="04dc7-106">Avvio veloce di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="04dc7-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="04dc7-107">Una delle nuove funzionalità aggiunte in Visual Studio 2012 è stata la finestra di [dialogo avvio veloce](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="04dc7-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="04dc7-108">NuGet 2,2 estende questa finestra di dialogo, consentendo di inizializzare la finestra di dialogo di gestione pacchetti con i termini di ricerca immessi nell'avvio veloce.</span><span class="sxs-lookup"><span data-stu-id="04dc7-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="04dc7-109">Ad esempio, l'immissione di "jQuery" in avvio veloce include ora un'opzione nei risultati per la ricerca dei pacchetti NuGet corrispondenti a "jQuery".</span><span class="sxs-lookup"><span data-stu-id="04dc7-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![Avvio veloce di NuGet in Visual Studio](./media/quick-launch.png)

<span data-ttu-id="04dc7-111">Se si seleziona questa opzione, verrà avviata l'esperienza di ricerca standard di gestione pacchetti NuGet per il termine "jQuery".</span><span class="sxs-lookup"><span data-stu-id="04dc7-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Finestra di dialogo Gestione pacchetti NuGet pre-popolata](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="04dc7-113">Specificare l'intera cartella per il contenuto del pacchetto</span><span class="sxs-lookup"><span data-stu-id="04dc7-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="04dc7-114">NuGet 2,2 consente ora di specificare un'intera cartella nell' `<file>` elemento del `.nuspec` file per includere tutto il contenuto della cartella.</span><span class="sxs-lookup"><span data-stu-id="04dc7-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="04dc7-115">Ad esempio, il codice seguente comporterà l'aggiunta di tutti gli script nella cartella Scripts alla cartella contents\scripts quando il pacchetto viene installato in un progetto.</span><span class="sxs-lookup"><span data-stu-id="04dc7-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="04dc7-116">**Aggiornamento 6/24/16: le cartelle vuote nella cartella "Content" vengono ignorate durante l'installazione del pacchetto.**</span><span class="sxs-lookup"><span data-stu-id="04dc7-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="04dc7-117">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="04dc7-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="04dc7-118">L'installazione del pacchetto non riesce per i progetti F # quando si usa la console di gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="04dc7-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="04dc7-119">Quando si tenta di installare un pacchetto NuGet in un progetto F # usando la console di gestione pacchetti, viene generata un'eccezione InvalidOperationException.</span><span class="sxs-lookup"><span data-stu-id="04dc7-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="04dc7-120">Stiamo collaborando attivamente con il team F # per risolvere il problema, ma nel frattempo la soluzione alternativa consiste nell'installare i pacchetti NuGet in progetti F # tramite la finestra di dialogo Gestione pacchetti di NuGet invece della console.</span><span class="sxs-lookup"><span data-stu-id="04dc7-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="04dc7-121">[Ulteriori informazioni sono disponibili in CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="04dc7-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="04dc7-122">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="04dc7-122">Bug Fixes</span></span>
<span data-ttu-id="04dc7-123">NuGet 2,2 include numerose correzioni di bug.</span><span class="sxs-lookup"><span data-stu-id="04dc7-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="04dc7-124">Per un elenco completo degli elementi di lavoro corretti in NuGet 2,2, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="04dc7-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
