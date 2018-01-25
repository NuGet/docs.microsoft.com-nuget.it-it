---
title: NuGet 2.6.1 delle note sulla versione di WebMatrix | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 119ea65b-b38b-4a8c-a4ed-6ea06f1aad09
description: "Note sulla versione per NuGet 2.6.1 per WebMatrix, inclusi i problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet 2.6.1 per le note sulla versione di WebMatrix, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9c37ddc998378b8aaa477dd5df814bab6f0b3c58
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="c8187-104">NuGet 2.6.1 delle note sulla versione di WebMatrix</span><span class="sxs-lookup"><span data-stu-id="c8187-104">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="c8187-105">[Note sulla versione 2.6 NuGet](../release-notes/nuget-2.6.md) | [note sulla versione 2.7 NuGet](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="c8187-105">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="c8187-106">Il team di NuGet rilasciati da un'estensione Gestione pacchetti NuGet aggiornato per WebMatrix 26 marzo 2014.</span><span class="sxs-lookup"><span data-stu-id="c8187-106">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="c8187-107">Questo aggiornamento può essere installato dal [raccolta estensioni WebMatrix](http://extensions.webmatrix.com/packages/NuGetPackageManager/) usando la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c8187-107">This update can be installed from the [WebMatrix Extension Gallery](http://extensions.webmatrix.com/packages/NuGetPackageManager/) using the following steps:</span></span>

1. <span data-ttu-id="c8187-108">Aprire WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="c8187-108">Open WebMatrix 3</span></span>
2. <span data-ttu-id="c8187-109">Fare clic sull'icona di estensioni della barra multifunzione Home</span><span class="sxs-lookup"><span data-stu-id="c8187-109">Click the Extensions icon in the Home ribbon</span></span>
3. <span data-ttu-id="c8187-110">Selezionare la scheda di aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="c8187-110">Select the Updates tab</span></span>
4. <span data-ttu-id="c8187-111">Fare clic per aggiornare Gestione pacchetti NuGet per 2.6.1</span><span class="sxs-lookup"><span data-stu-id="c8187-111">Click to update NuGet Package Manager to 2.6.1</span></span>
6. <span data-ttu-id="c8187-112">Chiudere e riavviare WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="c8187-112">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="c8187-113">Modifiche significative</span><span class="sxs-lookup"><span data-stu-id="c8187-113">Notable Changes</span></span>

<span data-ttu-id="c8187-114">Questo aggiornamento risolve estensione due dei principali utenti problemi sono riscontrate dispendiosa in termini di pacchetti NuGet all'interno di WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="c8187-114">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="c8187-115">Il primo è un errore di versione dello schema di NuGet e il secondo è un bug iniziali per le DLL a zero byte nel `bin` cartella.</span><span class="sxs-lookup"><span data-stu-id="c8187-115">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="c8187-116">Errore di versione dello Schema di NuGet</span><span class="sxs-lookup"><span data-stu-id="c8187-116">NuGet Schema Version Error</span></span>

<span data-ttu-id="c8187-117">Dopo il rilascio 3 WebMatrix, nuove funzionalità sono state introdotte in NuGet che richiedono una nuova versione dello schema per i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="c8187-117">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="c8187-118">Durante il tentativo di gestire i pacchetti di NuGet nel sito web, questi nuovi pacchetti possono comportare errori che si noterà in WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="c8187-118">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you'll see in WebMatrix.</span></span>

![Si è verificato un errore.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="c8187-122">Questa versione più recente garantisce la compatibilità con i pacchetti NuGet più recente, impedendo che l'errore che si verificano.</span><span class="sxs-lookup"><span data-stu-id="c8187-122">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="c8187-123">Le nuove versioni dei pacchetti, inclusi Microsoft.AspNet.WebPages ora possono essere installate in WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="c8187-123">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="c8187-124">Alcuni di questi pacchetti sono stati usare funzionalità di NuGet come [trasformazioni di configurazione XDT](../release-notes/nuget-2.6.md#xdt), che non è supportato in WebMatrix fino ad ora.</span><span class="sxs-lookup"><span data-stu-id="c8187-124">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="c8187-125">DLL di zero Byte nella cartella bin</span><span class="sxs-lookup"><span data-stu-id="c8187-125">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="c8187-126">Alcuni utenti hanno segnalato che dopo l'installazione di NuGet pacchetti in WebMatrix che includono le DLL che vengono copiate su bin, che mostra la DLL di nel `bin` cartella dei file di 0 byte.</span><span class="sxs-lookup"><span data-stu-id="c8187-126">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="c8187-127">L'applicazione viene interrotta in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c8187-127">This breaks the application at runtime.</span></span>

<span data-ttu-id="c8187-128">[Questo problema](https://nuget.codeplex.com/workitem/4060) ora è stato risolto.</span><span class="sxs-lookup"><span data-stu-id="c8187-128">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="c8187-129">Altri miglioramenti di recente</span><span class="sxs-lookup"><span data-stu-id="c8187-129">Other Recent Improvements</span></span>

<span data-ttu-id="c8187-130">Quando è stato rilasciato 2.8 di gestione pacchetti NuGet per Visual Studio, Gestione pacchetti NuGet 2.5.0 sono stati rilasciati anche per WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="c8187-130">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="c8187-131">Mentre questo è stato riportato nel [note sulla versione di NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), è ancora specifica nuove funzionalità che gli aggiornamenti introdotti.</span><span class="sxs-lookup"><span data-stu-id="c8187-131">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="c8187-132">Aggiornare tutte</span><span class="sxs-lookup"><span data-stu-id="c8187-132">Update All</span></span>

<span data-ttu-id="c8187-133">È ora possibile aggiornare tutti i pacchetti del sito web in un unico passaggio.</span><span class="sxs-lookup"><span data-stu-id="c8187-133">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="c8187-134">Quando si apre l'estensione NuGet in WebMatrix, di visualizzare l'elenco di tutti i pacchetti nella raccolta, questi sono installati e quelli con gli aggiornamenti disponibili.</span><span class="sxs-lookup"><span data-stu-id="c8187-134">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="c8187-135">In precedenza, ogni pacchetto deve essere aggiornato singolarmente, ma ora è disponibile un pulsante di "Aggiorna tutte" utile che viene visualizzato nella scheda aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="c8187-135">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Fare clic su Aggiorna tutto per aggiornare tutti i pacchetti con aggiornamenti disponibili](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="c8187-137">Sovrascrivi file esistenti</span><span class="sxs-lookup"><span data-stu-id="c8187-137">Overwrite Existing Files</span></span>

<span data-ttu-id="c8187-138">Quando si installano i pacchetti che contengono i file già esistenti nel sito web, NuGet è sempre ignorati i file (lasciare i file esistenti).</span><span class="sxs-lookup"><span data-stu-id="c8187-138">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="c8187-139">Ciò potrebbe causare l'impressione che un pacchetto è stato installato o aggiornato correttamente quando in realtà non è stato.</span><span class="sxs-lookup"><span data-stu-id="c8187-139">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="c8187-140">NuGet verrà ora richiesto per i file devono essere sovrascritti.</span><span class="sxs-lookup"><span data-stu-id="c8187-140">NuGet will now prompt for files to be overwritten.</span></span>

![Risoluzione dei conflitti di file](./media/NuGet-2.8/webmatrix-overwrite-file.png)
