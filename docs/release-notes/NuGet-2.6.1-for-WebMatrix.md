---
title: Note sulla versione di NuGet 2.6.1 per WebMatrix
description: Note sulla versione per NuGet 2.6.1 per WebMatrix, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780427"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="2bcd8-103">Note sulla versione di NuGet 2.6.1 per WebMatrix</span><span class="sxs-lookup"><span data-stu-id="2bcd8-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="2bcd8-104">Note sulla versione di [NuGet 2,6](../release-notes/nuget-2.6.md)  |  [Note sulla versione di NuGet 2,7](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="2bcd8-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="2bcd8-105">Il team NuGet ha rilasciato un'estensione di gestione pacchetti NuGet aggiornata per WebMatrix il 26 marzo 2014.</span><span class="sxs-lookup"><span data-stu-id="2bcd8-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="2bcd8-106">Questo aggiornamento può essere installato dalla [raccolta di estensioni WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) attenendosi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2bcd8-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="2bcd8-107">Apri WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="2bcd8-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="2bcd8-108">Fare clic sull'icona estensioni nella scheda Home della barra multifunzione</span><span class="sxs-lookup"><span data-stu-id="2bcd8-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="2bcd8-109">Selezionare la scheda aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="2bcd8-109">Select the Updates tab</span></span>
1. <span data-ttu-id="2bcd8-110">Fare clic per aggiornare Gestione pacchetti NuGet a 2.6.1</span><span class="sxs-lookup"><span data-stu-id="2bcd8-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="2bcd8-111">Chiudere e riavviare WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="2bcd8-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="2bcd8-112">Modifiche rilevanti</span><span class="sxs-lookup"><span data-stu-id="2bcd8-112">Notable Changes</span></span>

<span data-ttu-id="2bcd8-113">Questo aggiornamento dell'estensione risolve due dei principali problemi riscontrati dagli utenti per l'utilizzo di pacchetti NuGet all'interno di WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="2bcd8-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="2bcd8-114">Il primo è un errore di versione dello schema NuGet e il secondo è un bug che conduce a DLL a zero byte nella `bin` cartella.</span><span class="sxs-lookup"><span data-stu-id="2bcd8-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="2bcd8-115">Errore di versione dello schema NuGet</span><span class="sxs-lookup"><span data-stu-id="2bcd8-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="2bcd8-116">Poiché WebMatrix 3 è stato rilasciato, nuove funzionalità sono state introdotte in NuGet che richiedono una nuova versione dello schema per i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="2bcd8-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="2bcd8-117">Quando si tenta di gestire i pacchetti NuGet nel sito Web, questi nuovi pacchetti possono causare errori visualizzati in WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="2bcd8-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Si è verificato un errore.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="2bcd8-121">Questa versione più recente offre la compatibilità con i pacchetti NuGet più recenti, evitando che questo errore si verifichi.</span><span class="sxs-lookup"><span data-stu-id="2bcd8-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="2bcd8-122">Le nuove versioni dei pacchetti, tra cui Microsoft. AspNet. WebPages, possono ora essere installate in WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="2bcd8-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="2bcd8-123">Alcuni di questi pacchetti usavano le funzionalità di NuGet, ad esempio le [trasformazioni di configurazione di xdt](../release-notes/nuget-2.6.md#xdt), che finora non era supportata in WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="2bcd8-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="2bcd8-124">Zero-Byte dll nella cartella bin</span><span class="sxs-lookup"><span data-stu-id="2bcd8-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="2bcd8-125">Alcuni utenti hanno segnalato che dopo l'installazione di pacchetti NuGet in WebMatrix che includono dll che vengono copiate nel contenitore, le dll vengono visualizzate nella `bin` cartella come file da 0 byte.</span><span class="sxs-lookup"><span data-stu-id="2bcd8-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="2bcd8-126">Questa operazione interrompe l'applicazione in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2bcd8-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="2bcd8-127">[Questo problema](https://nuget.codeplex.com/workitem/4060) è stato risolto.</span><span class="sxs-lookup"><span data-stu-id="2bcd8-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="2bcd8-128">Altri miglioramenti recenti</span><span class="sxs-lookup"><span data-stu-id="2bcd8-128">Other Recent Improvements</span></span>

<span data-ttu-id="2bcd8-129">Quando la versione di gestione pacchetti NuGet 2,8 è stata rilasciata per Visual Studio, è stato rilasciato anche gestione pacchetti NuGet 2.5.0 per WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="2bcd8-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="2bcd8-130">Sebbene sia stato menzionato nelle [Note sulla versione di NuGet 2,8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), non sono state citate le nuove funzionalità specifiche introdotte dall'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="2bcd8-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="2bcd8-131">Aggiorna tutto</span><span class="sxs-lookup"><span data-stu-id="2bcd8-131">Update All</span></span>

<span data-ttu-id="2bcd8-132">È ora possibile aggiornare tutti i pacchetti del sito Web in un unico passaggio.</span><span class="sxs-lookup"><span data-stu-id="2bcd8-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="2bcd8-133">Quando si apre l'estensione NuGet in WebMatrix, viene visualizzato l'elenco di tutti i pacchetti nella raccolta, quelli installati e quelli con aggiornamenti disponibili.</span><span class="sxs-lookup"><span data-stu-id="2bcd8-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="2bcd8-134">In precedenza, ogni pacchetto deve essere aggiornato singolarmente, ma ora è disponibile un pulsante "Aggiorna tutto" che viene visualizzato nella scheda aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="2bcd8-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Fare clic su Aggiorna tutto per aggiornare tutti i pacchetti con gli aggiornamenti disponibili](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="2bcd8-136">Sovrascrivi file esistenti</span><span class="sxs-lookup"><span data-stu-id="2bcd8-136">Overwrite Existing Files</span></span>

<span data-ttu-id="2bcd8-137">Quando si installano pacchetti che contengono file già presenti nel sito Web, NuGet ha sempre ignorato automaticamente i file (lasciando solo i file esistenti).</span><span class="sxs-lookup"><span data-stu-id="2bcd8-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="2bcd8-138">Questo potrebbe comportare l'impressione che un pacchetto sia stato installato o aggiornato correttamente quando in realtà non lo era.</span><span class="sxs-lookup"><span data-stu-id="2bcd8-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="2bcd8-139">In NuGet verrà ora richiesto di sovrascrivere i file.</span><span class="sxs-lookup"><span data-stu-id="2bcd8-139">NuGet will now prompt for files to be overwritten.</span></span>

![Risoluzione dei conflitti di file](./media/NuGet-2.8/webmatrix-overwrite-file.png)
