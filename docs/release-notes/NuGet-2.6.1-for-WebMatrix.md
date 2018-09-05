---
title: NuGet 2.6.1 per WebMatrix note
description: Note sulla versione per NuGet 2.6.1 per WebMatrix, inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550317"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="709d5-103">NuGet 2.6.1 per WebMatrix note</span><span class="sxs-lookup"><span data-stu-id="709d5-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="709d5-104">[Note sulla versione per NuGet 2.6](../release-notes/nuget-2.6.md) | [note sulla versione per NuGet 2.7](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="709d5-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="709d5-105">Il team di NuGet ha rilasciato un'aggiornato estensione Gestione pacchetti NuGet per WebMatrix 26 marzo 2014.</span><span class="sxs-lookup"><span data-stu-id="709d5-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="709d5-106">Questo aggiornamento può essere installato dal [raccolta di estensioni di WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) usando la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="709d5-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="709d5-107">Aprire WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="709d5-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="709d5-108">Fare clic sull'icona delle estensioni nella barra multifunzione Home</span><span class="sxs-lookup"><span data-stu-id="709d5-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="709d5-109">Selezionare la scheda aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="709d5-109">Select the Updates tab</span></span>
1. <span data-ttu-id="709d5-110">Fare clic per aggiornare Gestione pacchetti NuGet alla versione 2.6.1</span><span class="sxs-lookup"><span data-stu-id="709d5-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="709d5-111">Chiudere e riavviare WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="709d5-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="709d5-112">Modifiche di rilievo</span><span class="sxs-lookup"><span data-stu-id="709d5-112">Notable Changes</span></span>

<span data-ttu-id="709d5-113">Questo aggiornamento risolve estensione due degli utenti principali problemi hanno dovuto affrontare dispendiosa in termini di pacchetti NuGet all'interno di WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="709d5-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="709d5-114">Il primo è verificato un errore di versione dello schema di NuGet e il secondo è un bug iniziali alle DLL di zero byte nel `bin` cartella.</span><span class="sxs-lookup"><span data-stu-id="709d5-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="709d5-115">Errore di versione dello Schema di NuGet</span><span class="sxs-lookup"><span data-stu-id="709d5-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="709d5-116">Dopo il rilascio di WebMatrix 3, le nuove funzionalità sono state introdotte in NuGet che richiedono una nuova versione dello schema per i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="709d5-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="709d5-117">Quando si tenta di gestire i pacchetti NuGet nel sito web, questi nuovi pacchetti possono causare errori visualizzati in WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="709d5-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Si è verificato un errore.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="709d5-121">Questa versione più recente garantisce la compatibilità con i pacchetti NuGet più recente, impedendo che l'errore che si verificano.</span><span class="sxs-lookup"><span data-stu-id="709d5-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="709d5-122">Le nuove versioni dei pacchetti, inclusi Microsoft.AspNet.WebPages ora possono essere installate in WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="709d5-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="709d5-123">Alcuni di questi pacchetti usavano le funzionalità di NuGet, ad esempio [trasformazioni XDT config](../release-notes/nuget-2.6.md#xdt), che non era supportato in WebMatrix fino ad ora.</span><span class="sxs-lookup"><span data-stu-id="709d5-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="709d5-124">DLL a zero Byte nella cartella bin</span><span class="sxs-lookup"><span data-stu-id="709d5-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="709d5-125">Alcuni utenti hanno segnalato che dopo l'installazione di NuGet in pacchetti in WebMatrix che includono le DLL che viene copiate nel contenitore, che mostra la DLL nel `bin` cartella dei file di 0 byte.</span><span class="sxs-lookup"><span data-stu-id="709d5-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="709d5-126">Questa operazione interrompe l'applicazione in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="709d5-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="709d5-127">[Questo problema](https://nuget.codeplex.com/workitem/4060) ora risolto.</span><span class="sxs-lookup"><span data-stu-id="709d5-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="709d5-128">Altri miglioramenti recenti</span><span class="sxs-lookup"><span data-stu-id="709d5-128">Other Recent Improvements</span></span>

<span data-ttu-id="709d5-129">Quando fu rilasciato NuGet Package Manager 2.8 per Visual Studio, sono stati rilasciati anche Gestione pacchetti NuGet 2.5.0 per WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="709d5-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="709d5-130">Mentre questa è stata menzionata la [note sulla versione di NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), viene non hai citato le specifiche delle nuove funzionalità che gli aggiornamenti introdotti.</span><span class="sxs-lookup"><span data-stu-id="709d5-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="709d5-131">Aggiorna tutto</span><span class="sxs-lookup"><span data-stu-id="709d5-131">Update All</span></span>

<span data-ttu-id="709d5-132">È ora possibile aggiornare tutti i pacchetti del sito web in un unico passaggio.</span><span class="sxs-lookup"><span data-stu-id="709d5-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="709d5-133">Quando si apre l'estensione NuGet in WebMatrix, viene visualizzato l'elenco di tutti i pacchetti nella raccolta, quelle installate e quelli con gli aggiornamenti disponibili.</span><span class="sxs-lookup"><span data-stu-id="709d5-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="709d5-134">In precedenza, ogni pacchetto dovrà essere aggiornato singolarmente, ma ora è disponibile un pulsante "Aggiorna tutto" utile che viene visualizzato nella scheda aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="709d5-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Fare clic su Aggiorna tutto per aggiornare tutti i pacchetti con aggiornamenti disponibili](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="709d5-136">Sovrascrivi file esistenti</span><span class="sxs-lookup"><span data-stu-id="709d5-136">Overwrite Existing Files</span></span>

<span data-ttu-id="709d5-137">Quando si installa i pacchetti che contengono i file già esistenti nel sito web, NuGet ha ignorato sempre automaticamente tali file (lasciare i file esistenti).</span><span class="sxs-lookup"><span data-stu-id="709d5-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="709d5-138">Questo potrebbe causare l'impressione che un pacchetto è stato installato o aggiornato correttamente quando in realtà non è stato.</span><span class="sxs-lookup"><span data-stu-id="709d5-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="709d5-139">NuGet verrà ora richiesto per i file verranno sovrascritti.</span><span class="sxs-lookup"><span data-stu-id="709d5-139">NuGet will now prompt for files to be overwritten.</span></span>

![Risoluzione dei conflitti di file](./media/NuGet-2.8/webmatrix-overwrite-file.png)
