---
title: Note sulla versione 1.7 NuGet | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: df7becc6-993d-4d06-8495-a0c26748bdfa
description: "Note sulla versione per NuGet 1.7 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "1.7 NuGet note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 420b40576cb3862f0e4406966f9ccca9fd1f39a1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="c9e58-104">Note sulla versione 1.7 di NuGet</span><span class="sxs-lookup"><span data-stu-id="c9e58-104">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="c9e58-105">[Note sulla versione 1.6 NuGet](../release-notes/nuget-1.6.md) | [note sulla versione 1.8 NuGet](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="c9e58-105">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="c9e58-106">NuGet 1.7 è stata rilasciata 4 aprile 2012.</span><span class="sxs-lookup"><span data-stu-id="c9e58-106">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="c9e58-107">Problema di installazione noti</span><span class="sxs-lookup"><span data-stu-id="c9e58-107">Known Installation Issue</span></span>
<span data-ttu-id="c9e58-108">Se si esegue Visual Studio 2010 SP1, è possibile eseguire in un errore di installazione durante il tentativo di aggiornare NuGet, se è installata una versione precedente.</span><span class="sxs-lookup"><span data-stu-id="c9e58-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="c9e58-109">La soluzione alternativa consiste nel disinstallare semplicemente NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c9e58-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="c9e58-110">Vedere [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="c9e58-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="c9e58-111">Nota: Se Visual Studio non consente di disinstallare l'estensione (il pulsante di disinstallazione è disabilitato), quindi probabile che sia necessario riavviare Visual Studio utilizzando "Esegui come amministratore".</span><span class="sxs-lookup"><span data-stu-id="c9e58-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="c9e58-112">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="c9e58-112">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="c9e58-113">Supporto di apertura file Readme. txt dopo l'installazione</span><span class="sxs-lookup"><span data-stu-id="c9e58-113">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="c9e58-114">Novità di 1.7, se il pacchetto include un `readme.txt` file alla radice del pacchetto NuGet verrà aperto automaticamente questo file dopo avere completato l'installazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c9e58-114">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="c9e58-115">Mostra i pacchetti della versione provvisoria della finestra di dialogo Gestisci NuGet pacchetti</span><span class="sxs-lookup"><span data-stu-id="c9e58-115">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="c9e58-116">La finestra di dialogo Gestisci pacchetti NuGet include ora un elenco a discesa che fornisce l'opzione per visualizzare i pacchetti della versione provvisoria.</span><span class="sxs-lookup"><span data-stu-id="c9e58-116">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Visualizzazione di pacchetti della versione provvisoria](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="c9e58-118">Mostra pulsante di ripristino dei pacchetti quando mancano i file di pacchetto</span><span class="sxs-lookup"><span data-stu-id="c9e58-118">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="c9e58-119">Quando si apre la console di gestione pacchetti o finestra di dialogo dei pacchetti NuGet gestione, controlla se la soluzione corrente è abilitata la modalità di ripristino dei pacchetti NuGet e, se mancano eventuali file di pacchetto di `packages` cartella.</span><span class="sxs-lookup"><span data-stu-id="c9e58-119">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="c9e58-120">Se queste due condizioni vengono soddisfatte, NuGet invierà una notifica e verrà visualizzato un pulsante di ripristino semplice.</span><span class="sxs-lookup"><span data-stu-id="c9e58-120">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="c9e58-121">Fare clic su questo pulsante attiverà NuGet per ripristinare tutti i pacchetti mancanti.</span><span class="sxs-lookup"><span data-stu-id="c9e58-121">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Pulsante di ripristino del pacchetto nella finestra di dialogo](./media/packagerestore-dialog.png)

![Pulsante di ripristino del pacchetto nella console](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="c9e58-124">Aggiungere file a livello di soluzione Packages.</span><span class="sxs-lookup"><span data-stu-id="c9e58-124">Add solution-level packages.config file</span></span>
<span data-ttu-id="c9e58-125">Nelle versioni precedenti di NuGet, ogni progetto dispone di un `packages.config` file che tiene traccia di quali pacchetti NuGet vengono installati in tale progetto.</span><span class="sxs-lookup"><span data-stu-id="c9e58-125">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="c9e58-126">Tuttavia, si è verificato alcun file simile a livello di soluzione per tenere traccia dei pacchetti a livello di soluzione.</span><span class="sxs-lookup"><span data-stu-id="c9e58-126">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="c9e58-127">Di conseguenza, si è verificato alcun modo per ripristinare i pacchetti a livello di soluzione.</span><span class="sxs-lookup"><span data-stu-id="c9e58-127">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="c9e58-128">Questa funzionalità è ora implementata in NuGet 1.7.</span><span class="sxs-lookup"><span data-stu-id="c9e58-128">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="c9e58-129">A livello di soluzione `packages.config` file si trova sotto il `.nuget` cartella soluzione radice e verranno archiviati i pacchetti solo a livello di soluzione.</span><span class="sxs-lookup"><span data-stu-id="c9e58-129">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="c9e58-130">Rimuovere il comando New-Package</span><span class="sxs-lookup"><span data-stu-id="c9e58-130">Remove New-Package command</span></span>
<span data-ttu-id="c9e58-131">A causa di scarso utilizzo, il comando New-Package è stato rimosso.</span><span class="sxs-lookup"><span data-stu-id="c9e58-131">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="c9e58-132">Gli sviluppatori si consiglia di utilizzare nuget.exe o Esplora pacchetti NuGet utili per creare pacchetti.</span><span class="sxs-lookup"><span data-stu-id="c9e58-132">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="c9e58-133">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="c9e58-133">Bug Fixes</span></span>
<span data-ttu-id="c9e58-134">1.7 NuGet è risolto numerosi bug per il ripristino dei pacchetti del flusso di lavoro e gli scenari di controllo di rete di origine.</span><span class="sxs-lookup"><span data-stu-id="c9e58-134">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="c9e58-135">Per un elenco completo di lavoro gli elementi corretti in NuGet 1.7,. visualizzazione di [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="c9e58-135">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
