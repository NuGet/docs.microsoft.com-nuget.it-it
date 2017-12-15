---
title: Note sulla versione di NuGet 3.3 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 4110a36a-cffe-4038-8da4-e841bce6e94b
description: "Note sulla versione per NuGet 3.3 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "3.3 NuGet note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f35f7621db324957b0af8329cf9faa11493835e2
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="cd297-104">Note sulla versione 3.3 di NuGet</span><span class="sxs-lookup"><span data-stu-id="cd297-104">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="cd297-105">[Note sulla versione di NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC note](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="cd297-105">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="cd297-106">3.3 NuGet è stato rilasciato il 30 novembre 2015 con un numero significativo di aggiornamenti dell'interfaccia utente e le funzionalità della riga di comando, nonché una raccolta di correzioni utile ai client NuGet.</span><span class="sxs-lookup"><span data-stu-id="cd297-106">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="cd297-107">Nuove funzionalità</span><span class="sxs-lookup"><span data-stu-id="cd297-107">New Features</span></span>

* <span data-ttu-id="cd297-108">Sono stati introdotti i provider di credenziali che consentono ai client della riga di comando di NuGet essere in grado di utilizzare facilmente un feed autenticato.</span><span class="sxs-lookup"><span data-stu-id="cd297-108">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="cd297-109">[Provider di credenziali di istruzioni su come installare Visual Studio Team Services ](../API/nuget-exe-Credential-Providers.md) e configurare NuGet ai client di utilizzare, sono disponibili in NuGet Docs.</span><span class="sxs-lookup"><span data-stu-id="cd297-109">[Instructions on how to install the Visual Studio Team Services credential provider ](../API/nuget-exe-Credential-Providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="cd297-110">Nuove funzionalità dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="cd297-110">New User Interface Features</span></span>

* <span data-ttu-id="cd297-111">Schede separate di esplorazione, installato e gli aggiornamenti disponibili</span><span class="sxs-lookup"><span data-stu-id="cd297-111">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="cd297-112">Gli aggiornamenti disponibile badge che indica il numero di pacchetti con aggiornamenti disponibili</span><span class="sxs-lookup"><span data-stu-id="cd297-112">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="cd297-113">Badge pacchetto nell'elenco del pacchetto per indicare se il pacchetto è installato o è disponibile un aggiornamento</span><span class="sxs-lookup"><span data-stu-id="cd297-113">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="cd297-114">Scaricare conteggio e l'autore aggiunto all'elenco di pacchetti</span><span class="sxs-lookup"><span data-stu-id="cd297-114">Download count and author added to the package list</span></span>
* <span data-ttu-id="cd297-115">Numero massimo di versione disponibili e il numero di versione attualmente installata di elenco di pacchetti</span><span class="sxs-lookup"><span data-stu-id="cd297-115">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="cd297-116">Pulsanti di azione per consentire l'installazione rapida, aggiornare e disinstallare dall'elenco di pacchetti</span><span class="sxs-lookup"><span data-stu-id="cd297-116">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="cd297-117">Più chiari pulsanti di azione nel riquadro dettagli di pacchetto</span><span class="sxs-lookup"><span data-stu-id="cd297-117">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="cd297-118">Data di aggiornamento del pacchetto nel riquadro dettagli di pacchetto</span><span class="sxs-lookup"><span data-stu-id="cd297-118">Package update date on the package detail panel</span></span>
* <span data-ttu-id="cd297-119">Consolidare pannello nella visualizzazione soluzione</span><span class="sxs-lookup"><span data-stu-id="cd297-119">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="cd297-120">Griglia ordinabile dei progetti e dei numeri di versione nella visualizzazione soluzione</span><span class="sxs-lookup"><span data-stu-id="cd297-120">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="cd297-121">Nuove funzionalità della riga di comando</span><span class="sxs-lookup"><span data-stu-id="cd297-121">New Command-line Features</span></span>

<span data-ttu-id="cd297-122">In questa versione è stata introdotta la `add` e `init` comandi inizializzare repository basati su cartelle come descritto nel [nuget.exe riferimento](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="cd297-122">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="cd297-123">Struttura di repository che vengono costruiti e mantenuti con questa cartella verrà [offrire vantaggi significativi delle prestazioni](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) come descritto nel blog.</span><span class="sxs-lookup"><span data-stu-id="cd297-123">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="cd297-124">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="cd297-124">ContentFiles</span></span>

<span data-ttu-id="cd297-125">Il contenuto è ora supportato in `project.json` gestiti progetti tramite il nuovo `contentFiles` cartella e `.nuspec` `contentFiles` notazione di elemento.</span><span class="sxs-lookup"><span data-stu-id="cd297-125">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="cd297-126">Questo contenuto può essere specificato in modo più diretto dall'autore del pacchetto per le interazioni con i sistemi di progetto.</span><span class="sxs-lookup"><span data-stu-id="cd297-126">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="cd297-127">Ulteriori informazioni su come configurare contentFiles in un `.nuspec` documento, vedere il [. nuspec riferimento](../schema/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="cd297-127">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../schema/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="cd297-128">Variabili locali NuGet memorizzare nella Cache di gestione</span><span class="sxs-lookup"><span data-stu-id="cd297-128">NuGet Locals Cache Management</span></span>

<span data-ttu-id="cd297-129">NuGet da riga di comando è stato aggiornato per includere informazioni su come gestire la cache locale in una workstation.</span><span class="sxs-lookup"><span data-stu-id="cd297-129">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="cd297-130">Ulteriori informazioni sul comando variabili locali sono disponibile nel [NuGet da riga di comando](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="cd297-130">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="cd297-131">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="cd297-131">Fixed Issues</span></span>

<span data-ttu-id="cd297-132">**Problemi rilevanti**</span><span class="sxs-lookup"><span data-stu-id="cd297-132">**Notable Issues**</span></span>

* <span data-ttu-id="cd297-133">NuGet da riga di comando ripristinato il supporto per il ripristino dei pacchetti con un file di soluzione in Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="cd297-133">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="cd297-134">L'elenco completo dei problemi che sono stati risolti nella versione 3.3 sono reperibili in GitHub sotto il [attività cardine 3.3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="cd297-134">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="cd297-135">L'elenco di problemi risolti nella versione della riga di comando 3.3 vengono registrati nella [3.3 attività cardine della riga di comando](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="cd297-135">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="cd297-136">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="cd297-136">Known Issues</span></span>

<span data-ttu-id="cd297-137">Continuiamo a tenere traccia dei problemi nell'elenco di problemi di GitHub in cui è reperibile in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="cd297-137">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>