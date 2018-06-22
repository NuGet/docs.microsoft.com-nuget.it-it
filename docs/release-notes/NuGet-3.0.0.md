---
title: Note sulla versione 3.0 di NuGet
description: Note sulla versione per l'inclusione di NuGet 3.0.0 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 26236c2db0e1a6be9c660905db567d9ebbbbe377
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820290"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="c4587-103">Note sulla versione 3.0 di NuGet</span><span class="sxs-lookup"><span data-stu-id="c4587-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="c4587-104">[Note sulla versione di NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [note sulla versione 3.1 NuGet](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="c4587-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="c4587-105">NuGet 3.0 è stata rilasciata come estensione bundle di Visual Studio 2015 20 luglio 2015.</span><span class="sxs-lookup"><span data-stu-id="c4587-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="c4587-106">Abbiamo inserito per fornire questa versione con Visual Studio in modo che l'esperienza di NuGet 3.0 aggiornata completezza deve essere disponibile per i nuovi utenti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c4587-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="c4587-107">Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="c4587-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="c4587-108">È consigliabile gli sviluppatori che dispongono dell'accesso per l'aggiornamento della raccolta di Visual Studio per la versione più recente è disponibile, come un aggiornamento attualmente vengono pubblicati poco dopo il rilascio di Visual Studio 2015 che contiene il supporto per lo sviluppo di Windows 10.</span><span class="sxs-lookup"><span data-stu-id="c4587-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="c4587-109">In totale, è stato chiuso 240 problemi nella versione 3.0 e puoi esaminare il [elenco completo dei problemi su GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="c4587-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="c4587-110">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="c4587-110">Known Issues</span></span>

<span data-ttu-id="c4587-111">Si sono verificati alcuni problemi noti forniti con questa versione e di tutti gli elementi corretti nella versione 3.1 pianificato in occasione del rilascio di Windows 10 del 29 luglio.</span><span class="sxs-lookup"><span data-stu-id="c4587-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="c4587-112">Si è in grado di aggiornare l'estensione di Visual Studio dalla raccolta o dopo tale data per risolvere questi problemi noti.</span><span class="sxs-lookup"><span data-stu-id="c4587-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="c4587-113">Conversione non viene fornita per l'etichetta "Non visualizzare più questo messaggio" nella finestra di anteprima e l'etichetta "Autori" nella finestra di descrizione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c4587-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="c4587-114">Quando si lavora su un progetto TFS con controllo del codice sorgente, NuGet non è presente la gestione dei pacchetti dell'interfaccia utente se il file NuGet. config è contrassegnato come di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="c4587-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="c4587-115">**Soluzione alternativa** estrarre il file da TFS.</span><span class="sxs-lookup"><span data-stu-id="c4587-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="c4587-116">Testo in giallo "riavvio barra" nella finestra di Powershell di NuGet non è visibile quando si usa il tema scuro di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c4587-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="c4587-117">**Soluzione alternativa** utilizzare il tema chiaro Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c4587-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="c4587-118">Riepilogo dei principali problemi risolti</span><span class="sxs-lookup"><span data-stu-id="c4587-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="c4587-119">Aggiornamento rete frequenti viene chiamato quando viene aggiornata la finestra di gestione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="c4587-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="c4587-120">Ritardo scorrimento installato modifica per visualizzare in Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="c4587-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="c4587-121">Chiamate di rete devono essere eseguite su un thread in background</span><span class="sxs-lookup"><span data-stu-id="c4587-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="c4587-122">Aggiunta una casella di controllo 'Non visualizzare la finestra di anteprima'</span><span class="sxs-lookup"><span data-stu-id="c4587-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="c4587-123">Processo aggiunto la limitazione delle richieste per ridurre l'utilizzo del processore</span><span class="sxs-lookup"><span data-stu-id="c4587-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="c4587-124">Migliorare la gestione dei riferimenti di libreria di classi portabile</span><span class="sxs-lookup"><span data-stu-id="c4587-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="c4587-125">Servizio di completamento automatico è stata fatta distinzione tra maiuscole e minuscole</span><span class="sxs-lookup"><span data-stu-id="c4587-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="c4587-126">Aggiornamento di ripristinare le credenziali di autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="c4587-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="c4587-127">Registrazione migliorata degli errori</span><span class="sxs-lookup"><span data-stu-id="c4587-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="c4587-128">Messaggi di errore migliorata powershell durante la chiamata pacchetto di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="c4587-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="c4587-129">Fissa il collegamento 'Ulteriori informazioni sulle opzioni' per impedire un arresto anomalo in Windows 10</span><span class="sxs-lookup"><span data-stu-id="c4587-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="c4587-130">Memorizza l'impostazione di casella di controllo di versione non definitiva</span><span class="sxs-lookup"><span data-stu-id="c4587-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="c4587-131">Gather migliorate le prestazioni memorizzando nella cache i risultati per i progetti in una soluzione</span><span class="sxs-lookup"><span data-stu-id="c4587-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="c4587-132">È possono raccogliere più pacchetti in parallelo</span><span class="sxs-lookup"><span data-stu-id="c4587-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="c4587-133">Ha rimosso il pacchetto di installazione-forzare il comando</span><span class="sxs-lookup"><span data-stu-id="c4587-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="c4587-134">Tenere d'occhio [blog](http://blog.nuget.org) per più lo stato di avanzamento e annunci man mano per fornire supporto per lo sviluppo di Windows 10.</span><span class="sxs-lookup"><span data-stu-id="c4587-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>