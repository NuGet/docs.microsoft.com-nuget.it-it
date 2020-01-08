---
title: Note sulla versione di NuGet 1,7
description: Note sulla versione per NuGet 1,7, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a98da76038582202396c8da96f8eae166e6096f6
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383319"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="18c41-103">Note sulla versione di NuGet 1,7</span><span class="sxs-lookup"><span data-stu-id="18c41-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="18c41-104">[Note sulla versione di nuget 1,6](../release-notes/nuget-1.6.md) | [Note sulla versione di NuGet 1,8](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="18c41-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="18c41-105">NuGet 1,7 è stato rilasciato il 4 aprile 2012.</span><span class="sxs-lookup"><span data-stu-id="18c41-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="18c41-106">Problema di installazione noto</span><span class="sxs-lookup"><span data-stu-id="18c41-106">Known Installation Issue</span></span>
<span data-ttu-id="18c41-107">Se si esegue VS 2010 SP1, potrebbe essere rilevato un errore di installazione quando si tenta di aggiornare NuGet se è installata una versione precedente.</span><span class="sxs-lookup"><span data-stu-id="18c41-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="18c41-108">La soluzione alternativa consiste nel disinstallare semplicemente NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="18c41-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="18c41-109">Per altre informazioni, vedere <https://support.microsoft.com/kb/2581019>.</span><span class="sxs-lookup"><span data-stu-id="18c41-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="18c41-110">Nota: se Visual Studio non consente di disinstallare l'estensione (il pulsante Disinstalla è disabilitato), probabilmente è necessario riavviare Visual Studio usando "Esegui come amministratore".</span><span class="sxs-lookup"><span data-stu-id="18c41-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="18c41-111">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="18c41-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="18c41-112">Supporto per l'apertura del file Readme. txt dopo l'installazione</span><span class="sxs-lookup"><span data-stu-id="18c41-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="18c41-113">Una novità di 1,7, se il pacchetto include un file di `readme.txt` alla radice del pacchetto, NuGet aprirà automaticamente il file al termine dell'installazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="18c41-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="18c41-114">Mostra pacchetti di versioni non definitive nella finestra di dialogo Gestisci pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="18c41-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="18c41-115">La finestra di dialogo Gestisci pacchetti NuGet include ora un elenco a discesa che consente di visualizzare i pacchetti di versioni non definitive.</span><span class="sxs-lookup"><span data-stu-id="18c41-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Visualizzazione dei pacchetti di versioni non definitive](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="18c41-117">Mostra il pulsante ripristino pacchetto quando mancano i file del pacchetto</span><span class="sxs-lookup"><span data-stu-id="18c41-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="18c41-118">Quando si apre la console di gestione pacchetti o la finestra di dialogo Gestione pacchetti NuGet, NuGet verificherà se la soluzione corrente ha abilitato la modalità di ripristino del pacchetto e se i file di pacchetto non sono presenti nella cartella `packages`.</span><span class="sxs-lookup"><span data-stu-id="18c41-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="18c41-119">Se queste due condizioni sono soddisfatte, NuGet invierà una notifica e mostrerà un comodo pulsante Ripristina.</span><span class="sxs-lookup"><span data-stu-id="18c41-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="18c41-120">Quando si fa clic su questo pulsante, NuGet viene attivato per ripristinare tutti i pacchetti mancanti.</span><span class="sxs-lookup"><span data-stu-id="18c41-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Pulsante ripristino pacchetti nella finestra di dialogo](./media/packagerestore-dialog.png)

![Pulsante ripristino pacchetto nella console di](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="18c41-123">Aggiungere il file Packages. config a livello di soluzione</span><span class="sxs-lookup"><span data-stu-id="18c41-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="18c41-124">Nelle versioni precedenti di NuGet ogni progetto dispone di un file `packages.config` che tiene traccia dei pacchetti NuGet installati in tale progetto.</span><span class="sxs-lookup"><span data-stu-id="18c41-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="18c41-125">Tuttavia, non esisteva un file simile a livello di soluzione per tenere traccia dei pacchetti a livello di soluzione.</span><span class="sxs-lookup"><span data-stu-id="18c41-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="18c41-126">Di conseguenza, non era possibile ripristinare i pacchetti a livello di soluzione.</span><span class="sxs-lookup"><span data-stu-id="18c41-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="18c41-127">Questa funzionalità è ora implementata in NuGet 1,7.</span><span class="sxs-lookup"><span data-stu-id="18c41-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="18c41-128">Il file di `packages.config` a livello di soluzione si trova nella cartella `.nuget` sotto la radice della soluzione e archivia solo i pacchetti a livello di soluzione.</span><span class="sxs-lookup"><span data-stu-id="18c41-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="18c41-129">Comando Rimuovi nuovo pacchetto</span><span class="sxs-lookup"><span data-stu-id="18c41-129">Remove New-Package command</span></span>
<span data-ttu-id="18c41-130">A causa dell'utilizzo ridotto, il comando New-Package è stato rimosso.</span><span class="sxs-lookup"><span data-stu-id="18c41-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="18c41-131">Si consiglia agli sviluppatori di usare NuGet. exe o la comoda utilità di esplorazione pacchetti NuGet per creare pacchetti.</span><span class="sxs-lookup"><span data-stu-id="18c41-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="18c41-132">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="18c41-132">Bug Fixes</span></span>
<span data-ttu-id="18c41-133">NuGet 1,7 ha risolto molti bug relativi al flusso di lavoro di ripristino del pacchetto e agli scenari di rete/controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="18c41-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="18c41-134">Per un elenco completo degli elementi di lavoro corretti in NuGet 1,7, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="18c41-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
