---
title: Note sulla versione 3.3 di NuGet
description: Note sulla versione per NuGet 3.3, inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546647"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="43f04-103">Note sulla versione 3.3 di NuGet</span><span class="sxs-lookup"><span data-stu-id="43f04-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="43f04-104">[Note sulla versione di NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC note](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="43f04-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="43f04-105">NuGet 3.3 è stata rilasciata il 30 novembre 2015 con un numero significativo degli aggiornamenti dell'interfaccia utente e le funzionalità della riga di comando, nonché una raccolta di correzioni utile per i client NuGet.</span><span class="sxs-lookup"><span data-stu-id="43f04-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="43f04-106">Nuove funzionalità</span><span class="sxs-lookup"><span data-stu-id="43f04-106">New Features</span></span>

* <span data-ttu-id="43f04-107">Sono stati introdotti i provider di credenziali che consentono ai client della riga di comando di NuGet essere in grado di integrarsi facilmente con un feed autenticato.</span><span class="sxs-lookup"><span data-stu-id="43f04-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="43f04-108">[Provider di credenziali di istruzioni su come installare Visual Studio Team Services ](../api/nuget-exe-credential-providers.md) e configurare NuGet ai client di usare, sono disponibili in NuGet Docs.</span><span class="sxs-lookup"><span data-stu-id="43f04-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="43f04-109">Nuove funzionalità dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="43f04-109">New User Interface Features</span></span>

* <span data-ttu-id="43f04-110">Schede separate di esplorazione, installato e gli aggiornamenti disponibili</span><span class="sxs-lookup"><span data-stu-id="43f04-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="43f04-111">Badge disponibili gli aggiornamenti che indica il numero di pacchetti con aggiornamenti disponibili</span><span class="sxs-lookup"><span data-stu-id="43f04-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="43f04-112">Notifiche pacchetto nell'elenco di pacchetti per indicare se il pacchetto viene installato o è disponibile un aggiornamento</span><span class="sxs-lookup"><span data-stu-id="43f04-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="43f04-113">Download di conteggio e autore aggiunto all'elenco dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="43f04-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="43f04-114">Numero di versione disponibile più alto e il numero di versione attualmente installata nell'elenco di pacchetti</span><span class="sxs-lookup"><span data-stu-id="43f04-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="43f04-115">Pulsanti di azione per consentire l'installazione rapida, aggiornare e disinstallare dall'elenco dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="43f04-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="43f04-116">Pulsanti di azione più chiari nel pannello dei dettagli del pacchetto</span><span class="sxs-lookup"><span data-stu-id="43f04-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="43f04-117">Data di aggiornamento del pacchetto nel pannello dei dettagli del pacchetto</span><span class="sxs-lookup"><span data-stu-id="43f04-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="43f04-118">Consolidare pannello nella visualizzazione della soluzione</span><span class="sxs-lookup"><span data-stu-id="43f04-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="43f04-119">Griglia ordinabile di progetti e i numeri di versione installata nella visualizzazione della soluzione</span><span class="sxs-lookup"><span data-stu-id="43f04-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="43f04-120">Nuove funzionalità della riga di comando</span><span class="sxs-lookup"><span data-stu-id="43f04-120">New Command-line Features</span></span>

<span data-ttu-id="43f04-121">In questa versione è stato introdotto il `add` e `init` comandi per inizializzare i repository basati su cartelle come descritto nel [nuget.exe riferimento](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="43f04-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="43f04-122">Struttura di repository in cui vengono costruiti e gestiti in questa cartella verrà [offrire vantaggi significativi delle prestazioni](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) come descritto nel blog.</span><span class="sxs-lookup"><span data-stu-id="43f04-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="43f04-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="43f04-123">ContentFiles</span></span>

<span data-ttu-id="43f04-124">È ora supportato contenuto nel `project.json` progetti tramite il nuovo gestiti `contentFiles` cartella e `.nuspec` `contentFiles` notazione elemento.</span><span class="sxs-lookup"><span data-stu-id="43f04-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="43f04-125">Questo contenuto può essere specificato in modo più diretto dall'autore del pacchetto per le interazioni con i sistemi di progetto.</span><span class="sxs-lookup"><span data-stu-id="43f04-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="43f04-126">Altre informazioni su come configurare contentFiles in una `.nuspec` documento è reperibile nella [riferimento file con estensione nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="43f04-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="43f04-127">Variabili locali NuGet memorizza nella Cache di gestione</span><span class="sxs-lookup"><span data-stu-id="43f04-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="43f04-128">Il riga di comando di NuGet è stato aggiornato per includere informazioni su come gestire le cache in una workstation locale.</span><span class="sxs-lookup"><span data-stu-id="43f04-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="43f04-129">Altre informazioni sul comando variabili locali sono disponibile nel [riferimento della riga di comando di NuGet](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="43f04-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="43f04-130">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="43f04-130">Fixed Issues</span></span>

<span data-ttu-id="43f04-131">**Errori rilevanti**</span><span class="sxs-lookup"><span data-stu-id="43f04-131">**Notable Issues**</span></span>

* <span data-ttu-id="43f04-132">Supporto ripristinato da riga di comando di NuGet per il ripristino dei pacchetti con un file di soluzione su Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="43f04-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="43f04-133">L'elenco completo dei problemi che sono stati risolti nella versione 3.3 è reperibile in GitHub con il [3.3 attività cardine](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="43f04-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="43f04-134">L'elenco dei problemi risolti nella versione di riga di comando 3.3 vengono registrati nella [3.3 attività cardine della riga di comando](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="43f04-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="43f04-135">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="43f04-135">Known Issues</span></span>

<span data-ttu-id="43f04-136">Continuiamo a tenere traccia dei problemi nel nostro elenco di problemi di GitHub che può trovarsi in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="43f04-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>