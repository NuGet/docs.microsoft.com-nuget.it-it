---
title: Note sulla versione di NuGet 3,0
description: Note sulla versione per NuGet 3.0.0, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776546"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="62bcd-103">Note sulla versione di NuGet 3,0</span><span class="sxs-lookup"><span data-stu-id="62bcd-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="62bcd-104">Note sulla versione di [NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)  |  [Note sulla versione di NuGet 3,1](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="62bcd-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="62bcd-105">NuGet 3,0 è stato rilasciato il 20 luglio 2015 come estensione del bundle a Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="62bcd-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="62bcd-106">Abbiamo effettuato il push per fornire questa versione con Visual Studio in modo che l'esperienza completa aggiornata di NuGet 3,0 sia disponibile per i nuovi utenti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="62bcd-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="62bcd-107">Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="62bcd-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="62bcd-108">Si consiglia agli sviluppatori che hanno accesso a Visual Studio Gallery di eseguire l'aggiornamento alla versione più recente disponibile, in quanto viene pubblicato un aggiornamento poco dopo il rilascio di Visual Studio 2015 che contiene il supporto per lo sviluppo di Windows 10.</span><span class="sxs-lookup"><span data-stu-id="62bcd-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="62bcd-109">In totale, sono stati chiusi 240 problemi nella versione 3,0 ed è possibile esaminare l' [elenco completo dei problemi in GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="62bcd-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="62bcd-110">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="62bcd-110">Known Issues</span></span>

<span data-ttu-id="62bcd-111">Con questa versione sono stati introdotti numerosi problemi noti e tutti questi elementi sono stati risolti nella versione 3,1 prevista per coincidere con il rilascio di Windows 10 il 29 luglio.</span><span class="sxs-lookup"><span data-stu-id="62bcd-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="62bcd-112">È possibile aggiornare l'estensione di Visual Studio dalla raccolta in data o dopo tale data per risolvere questi problemi noti.</span><span class="sxs-lookup"><span data-stu-id="62bcd-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="62bcd-113">La traduzione non è stata specificata per l'etichetta "non visualizzare più questo messaggio" nella finestra di anteprima e l'etichetta "authors" nella finestra di descrizione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="62bcd-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="62bcd-114">Quando si usa un progetto con il controllo del codice sorgente TFS, NuGet non è in grado di presentare l'interfaccia utente di gestione pacchetti se il file Nuget.Config è contrassegnato come di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="62bcd-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="62bcd-115">**Soluzione alternativa** Estrarre il file da TFS.</span><span class="sxs-lookup"><span data-stu-id="62bcd-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="62bcd-116">Quando si usa il tema scuro di Visual Studio, il testo nella "barra di riavvio" gialla della finestra di PowerShell di NuGet non è visibile.</span><span class="sxs-lookup"><span data-stu-id="62bcd-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="62bcd-117">**Soluzione alternativa** Usare il tema chiaro di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="62bcd-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="62bcd-118">Riepilogo dei principali problemi risolti</span><span class="sxs-lookup"><span data-stu-id="62bcd-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="62bcd-119">Frequenti chiamate di aggiornamento della rete quando viene aggiornata la finestra di gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="62bcd-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="62bcd-120">Scorrimento ritardato durante la modifica della visualizzazione installata in Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="62bcd-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="62bcd-121">Le chiamate di rete devono essere eseguite in un thread in background</span><span class="sxs-lookup"><span data-stu-id="62bcd-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="62bcd-122">È stata aggiunta la casella di controllo ' non visualizzare la finestra di anteprima '</span><span class="sxs-lookup"><span data-stu-id="62bcd-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="62bcd-123">Aggiunta limitazione del processo per ridurre l'utilizzo del processore</span><span class="sxs-lookup"><span data-stu-id="62bcd-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="62bcd-124">Gestione migliorata dei riferimenti alla libreria di classi portabile</span><span class="sxs-lookup"><span data-stu-id="62bcd-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="62bcd-125">Distinzione tra maiuscole e minuscole per il servizio AutoComplete</span><span class="sxs-lookup"><span data-stu-id="62bcd-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="62bcd-126">Aggiornare per reintrodurre le credenziali di autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="62bcd-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="62bcd-127">È stata migliorata la registrazione degli errori</span><span class="sxs-lookup"><span data-stu-id="62bcd-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="62bcd-128">Messaggi di errore di PowerShell migliorati quando si chiama Update-Package</span><span class="sxs-lookup"><span data-stu-id="62bcd-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="62bcd-129">Correzione del collegamento ' informazioni sulle opzioni ' per impedire arresti anomali in Windows 10</span><span class="sxs-lookup"><span data-stu-id="62bcd-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="62bcd-130">Ricorda impostazione della casella di controllo versione non definitiva</span><span class="sxs-lookup"><span data-stu-id="62bcd-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="62bcd-131">Miglioramento della raccolta delle prestazioni mediante la memorizzazione nella cache dei risultati tra i progetti in una soluzione</span><span class="sxs-lookup"><span data-stu-id="62bcd-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="62bcd-132">È possibile raccogliere più pacchetti in parallelo</span><span class="sxs-lookup"><span data-stu-id="62bcd-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="62bcd-133">Comando Install-Package-Force rimosso</span><span class="sxs-lookup"><span data-stu-id="62bcd-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="62bcd-134">Tieni sotto controllo il [nostro Blog](http://blog.nuget.org) per ottenere più informazioni sullo stato di avanzamento e sugli annunci, perché siamo pronti per offrire supporto per lo sviluppo in Windows 10.</span><span class="sxs-lookup"><span data-stu-id="62bcd-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>