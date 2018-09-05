---
title: Note sulla versione 3.0 di NuGet
description: Note sulla versione per NuGet 3.0.0, tra cui noti problemi, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551863"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="0ff1a-103">Note sulla versione 3.0 di NuGet</span><span class="sxs-lookup"><span data-stu-id="0ff1a-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="0ff1a-104">[Note sulla versione di NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [note sulla versione di NuGet 3.1](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="0ff1a-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="0ff1a-105">NuGet 3.0 è stato rilasciato il 20 luglio 2015 come estensione di bundle per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="0ff1a-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="0ff1a-106">Ci siamo concentrati per offrire questa versione con Visual Studio in modo che l'esperienza di NuGet 3.0 completata aggiornata sarà disponibile per i nuovi utenti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0ff1a-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="0ff1a-107">Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="0ff1a-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="0ff1a-108">È consigliabile per gli sviluppatori che dispongono dell'accesso per l'aggiornamento della raccolta di Visual Studio alla versione più recente che è disponibile, come viene pubblicata un'aggiornamento poco dopo il rilascio di Visual Studio 2015 che contiene il supporto per lo sviluppo di Windows 10.</span><span class="sxs-lookup"><span data-stu-id="0ff1a-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="0ff1a-109">In totale, abbiamo chiuso 240 problemi nella versione 3.0, ed è possibile esaminare i [elenco completo dei problemi in GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="0ff1a-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="0ff1a-110">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="0ff1a-110">Known Issues</span></span>

<span data-ttu-id="0ff1a-111">Si sono verificati alcuni problemi noti fornito con questa versione e di tutti gli elementi corretti nella versione 3.1 pianificato coincide con il rilascio di Windows 10 al 29 luglio.</span><span class="sxs-lookup"><span data-stu-id="0ff1a-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="0ff1a-112">Si è in grado di aggiornare l'estensione di Visual Studio dalla raccolta o dopo tale data per risolvere questi problemi noti.</span><span class="sxs-lookup"><span data-stu-id="0ff1a-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="0ff1a-113">Conversione non viene fornita per l'etichetta "Non visualizzare più questo messaggio" nella finestra di anteprima e l'etichetta "Autori" nella finestra di descrizione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="0ff1a-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="0ff1a-114">Quando si lavora a un progetto usando TFS controllo del codice sorgente, NuGet non può presentare package manager dell'interfaccia utente se il file NuGet. config è contrassegnato come sola lettura.</span><span class="sxs-lookup"><span data-stu-id="0ff1a-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="0ff1a-115">**Soluzione alternativa** estrarre il file da TFS.</span><span class="sxs-lookup"><span data-stu-id="0ff1a-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="0ff1a-116">Testo in giallo "riavvio bar" nella finestra di Powershell di NuGet non è visibile quando si usa il tema scuro di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0ff1a-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="0ff1a-117">**Soluzione alternativa** Usa il tema chiaro di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0ff1a-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="0ff1a-118">Riepilogo dei principali problemi risolti</span><span class="sxs-lookup"><span data-stu-id="0ff1a-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="0ff1a-119">Aggiornamenti frequenti rete viene chiamato quando viene aggiornata la finestra di gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="0ff1a-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="0ff1a-120">Scorrimento un ritardo se la modifica in installato visualizzazione in Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="0ff1a-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="0ff1a-121">Le chiamate di rete devono essere eseguite su un thread in background</span><span class="sxs-lookup"><span data-stu-id="0ff1a-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="0ff1a-122">Aggiungere la casella di controllo 'Non visualizzare la finestra di anteprima'</span><span class="sxs-lookup"><span data-stu-id="0ff1a-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="0ff1a-123">Processo aggiunto la limitazione per ridurre l'utilizzo del processore</span><span class="sxs-lookup"><span data-stu-id="0ff1a-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="0ff1a-124">Migliorata la gestione dei riferimenti di libreria di classi portabile</span><span class="sxs-lookup"><span data-stu-id="0ff1a-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="0ff1a-125">Servizio di completamento automatico è stato in maiuscole / minuscole</span><span class="sxs-lookup"><span data-stu-id="0ff1a-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="0ff1a-126">Aggiornamento reintrodurre le credenziali di autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="0ff1a-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="0ff1a-127">Registrazione degli errori migliorata</span><span class="sxs-lookup"><span data-stu-id="0ff1a-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="0ff1a-128">Messaggi di errore migliorata powershell quando si chiama Update-Package</span><span class="sxs-lookup"><span data-stu-id="0ff1a-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="0ff1a-129">Risolto il collegamento 'Altre informazioni sulle opzioni' per impedire un arresto anomalo in Windows 10</span><span class="sxs-lookup"><span data-stu-id="0ff1a-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="0ff1a-130">Ricordare di impostazione di casella di controllo di versione non definitiva</span><span class="sxs-lookup"><span data-stu-id="0ff1a-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="0ff1a-131">Gather migliorate le prestazioni memorizzando nella cache i risultati tra i progetti in una soluzione</span><span class="sxs-lookup"><span data-stu-id="0ff1a-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="0ff1a-132">Più pacchetti possono essere raccolte in parallelo</span><span class="sxs-lookup"><span data-stu-id="0ff1a-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="0ff1a-133">Rimosso install-package-forzare il comando</span><span class="sxs-lookup"><span data-stu-id="0ff1a-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="0ff1a-134">Teniamo d'occhio [nostro blog](http://blog.nuget.org) per più lo stato di avanzamento e annunci man mano che pronti a fornire supporto tecnico per lo sviluppo di Windows 10.</span><span class="sxs-lookup"><span data-stu-id="0ff1a-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>