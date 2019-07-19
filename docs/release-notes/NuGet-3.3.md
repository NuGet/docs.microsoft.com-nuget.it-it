---
title: Note sulla versione di NuGet 3,3
description: Note sulla versione per NuGet 3,3, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 482c03a4f6ca39edf317b6ef8d535e79b53d5d16
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317036"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="70fd9-103">Note sulla versione di NuGet 3,3</span><span class="sxs-lookup"><span data-stu-id="70fd9-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="70fd9-104">[Note sulla versione di NuGet 3.2.1](../release-notes/nuget-3.2.1.md)[(note sulla versione di NuGet 3,4-RC)](../release-notes/nuget-3.4-RC.md)  | </span><span class="sxs-lookup"><span data-stu-id="70fd9-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="70fd9-105">NuGet 3,3 è stato rilasciato il 30 novembre 2015 con un numero significativo di aggiornamenti dell'interfaccia utente e funzionalità della riga di comando, oltre a una raccolta di utili correzioni per i client NuGet.</span><span class="sxs-lookup"><span data-stu-id="70fd9-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="70fd9-106">Nuove funzionalità</span><span class="sxs-lookup"><span data-stu-id="70fd9-106">New Features</span></span>

* <span data-ttu-id="70fd9-107">Sono stati introdotti i provider di credenziali che consentono ai client della riga di comando NuGet di funzionare senza interruzioni con un feed autenticato.</span><span class="sxs-lookup"><span data-stu-id="70fd9-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="70fd9-108">Le [istruzioni su come installare il provider di credenziali Visual Studio Team Services](../api/nuget-exe-credential-providers.md) e configurare i client NuGet per usarlo sono disponibili nella documentazione di NuGet.</span><span class="sxs-lookup"><span data-stu-id="70fd9-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="70fd9-109">Nuove funzionalità dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="70fd9-109">New User Interface Features</span></span>

* <span data-ttu-id="70fd9-110">Schede di esplorazione, installazione e aggiornamento separate</span><span class="sxs-lookup"><span data-stu-id="70fd9-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="70fd9-111">Aggiorna il badge disponibile che indica il numero di pacchetti con aggiornamenti disponibili</span><span class="sxs-lookup"><span data-stu-id="70fd9-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="70fd9-112">Notifiche del pacchetto nell'elenco dei pacchetti per indicare se il pacchetto è installato o se è disponibile un aggiornamento</span><span class="sxs-lookup"><span data-stu-id="70fd9-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="70fd9-113">Numero di download e autore aggiunti all'elenco dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="70fd9-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="70fd9-114">Numero di versione più elevato e numero di versione attualmente installato nell'elenco dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="70fd9-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="70fd9-115">Pulsanti di azione per consentire l'installazione rapida, l'aggiornamento e la disinstallazione dall'elenco dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="70fd9-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="70fd9-116">Pulsanti di azione più chiari nel pannello dei dettagli del pacchetto</span><span class="sxs-lookup"><span data-stu-id="70fd9-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="70fd9-117">Data di aggiornamento del pacchetto nel pannello dei dettagli del pacchetto</span><span class="sxs-lookup"><span data-stu-id="70fd9-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="70fd9-118">Consolidare il pannello nella visualizzazione soluzione</span><span class="sxs-lookup"><span data-stu-id="70fd9-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="70fd9-119">Griglia ordinabile di progetti e numeri di versione installati nella visualizzazione soluzione</span><span class="sxs-lookup"><span data-stu-id="70fd9-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="70fd9-120">Nuove funzionalità della riga di comando</span><span class="sxs-lookup"><span data-stu-id="70fd9-120">New Command-line Features</span></span>

<span data-ttu-id="70fd9-121">In questa versione sono stati introdotti `init` i comandi e per inizializzare i `add` repository basati su cartelle come descritto nel riferimento a [NuGet. exe](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="70fd9-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="70fd9-122">I repository costruiti e gestiti con questa struttura di cartelle offriranno [vantaggi significativi](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) in materia di prestazioni, come descritto nel Blog.</span><span class="sxs-lookup"><span data-stu-id="70fd9-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="70fd9-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="70fd9-123">ContentFiles</span></span>

<span data-ttu-id="70fd9-124">Il contenuto è ora supportato `project.json` nei progetti gestiti tramite la `contentFiles` nuova notazione `.nuspec` di elementi e `contentFiles` cartelle.</span><span class="sxs-lookup"><span data-stu-id="70fd9-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="70fd9-125">Questo contenuto può essere specificato più direttamente dall'autore del pacchetto per le interazioni con i sistemi di progetto.</span><span class="sxs-lookup"><span data-stu-id="70fd9-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="70fd9-126">Altre informazioni su come configurare contentFiles in un `.nuspec` documento sono disponibili nel [riferimento. NuSpec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="70fd9-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="70fd9-127">Gestione cache NuGet locale</span><span class="sxs-lookup"><span data-stu-id="70fd9-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="70fd9-128">La riga di comando di NuGet è stata aggiornata per includere informazioni su come gestire le cache locali in una workstation.</span><span class="sxs-lookup"><span data-stu-id="70fd9-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="70fd9-129">Altre informazioni sul comando variabili locali sono disponibili nella Guida di [riferimento alla riga di comando di NuGet](../reference/cli-reference/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="70fd9-129">More information about the locals command is available in the [NuGet command-line reference](../reference/cli-reference/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="70fd9-130">Problemi risolti</span><span class="sxs-lookup"><span data-stu-id="70fd9-130">Fixed Issues</span></span>

<span data-ttu-id="70fd9-131">**Problemi rilevanti**</span><span class="sxs-lookup"><span data-stu-id="70fd9-131">**Notable Issues**</span></span>

* <span data-ttu-id="70fd9-132">Supporto della riga di comando di NuGet ripristinato per il ripristino di pacchetti con un file di soluzione in mono- [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="70fd9-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="70fd9-133">L'elenco completo dei problemi risolti nella versione 3,3 è disponibile in GitHub nell' [attività cardine 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="70fd9-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="70fd9-134">L'elenco dei problemi risolti nella versione della riga di comando 3,3 viene registrato nell' [attività cardine della riga di comando 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="70fd9-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="70fd9-135">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="70fd9-135">Known Issues</span></span>

<span data-ttu-id="70fd9-136">Continuiamo a tenere traccia dei problemi nell'elenco dei problemi di GitHub disponibili all'indirizzo:[http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="70fd9-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>