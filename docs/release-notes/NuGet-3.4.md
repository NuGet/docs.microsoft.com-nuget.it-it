---
title: Note sulla versione 3.4 di NuGet
description: Note sulla versione per NuGet 3.4, inclusi i problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f2a945b628022bdcc6e69a7a4b1be6c53b65626
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820472"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="11e1a-103">Note sulla versione 3.4 di NuGet</span><span class="sxs-lookup"><span data-stu-id="11e1a-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="11e1a-104">[NuGet 3.4 RC note](../release-notes/nuget-3.4-RC.md) | [note sulla versione di NuGet 3.4.1](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="11e1a-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="11e1a-105">NuGet 3.4 il 30 marzo 2016 è stato rilasciato come parte di Visual Studio 2015 Update 2 e Release di Visual Studio 15 Preview ed è stata compilata con alcuni principi in mente:</span><span class="sxs-lookup"><span data-stu-id="11e1a-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="11e1a-106">Supporto multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="11e1a-106">Cross-Platform support</span></span>
* <span data-ttu-id="11e1a-107">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="11e1a-107">Performance improvements</span></span>
* <span data-ttu-id="11e1a-108">Piccoli miglioramenti dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="11e1a-108">Minor UI improvements</span></span>

<span data-ttu-id="11e1a-109">Le funzionalità seguenti sono aggiunti in precedenza in RC e sono state aggiornate o completate per la versione 3.4:</span><span class="sxs-lookup"><span data-stu-id="11e1a-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="11e1a-110">Nuove funzionalità</span><span class="sxs-lookup"><span data-stu-id="11e1a-110">New Features</span></span>

* <span data-ttu-id="11e1a-111">I client NuGet ora supportano la codifica di contenuto gzip dai repository</span><span class="sxs-lookup"><span data-stu-id="11e1a-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="11e1a-112">Supporto per PDB dai pacchetti nei progetti xproj</span><span class="sxs-lookup"><span data-stu-id="11e1a-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="11e1a-113">Supporto per iOS e le azioni di compilazione Android nell'elemento contentFiles</span><span class="sxs-lookup"><span data-stu-id="11e1a-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="11e1a-114">Supporto per il moniker del framework moniker netstandard e netstandardapp</span><span class="sxs-lookup"><span data-stu-id="11e1a-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="11e1a-115">Nuove funzionalità dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="11e1a-115">New User Interface Features</span></span>

* <span data-ttu-id="11e1a-116">Miglioramenti significativi delle prestazioni in particolare nelle schede installato, aggiornamenti e Consolidate</span><span class="sxs-lookup"><span data-stu-id="11e1a-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="11e1a-117">Origine di aggregazione 'Tutte le origini pacchetti' è disponibile con l'unione di risultati di ricerca corretta</span><span class="sxs-lookup"><span data-stu-id="11e1a-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="11e1a-118">Installato e le schede degli aggiornamenti sono ora ordinate in ordine alfabetico</span><span class="sxs-lookup"><span data-stu-id="11e1a-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="11e1a-119">Aggiungere un pulsante di aggiornamento che consente una ricerca da aggiornare</span><span class="sxs-lookup"><span data-stu-id="11e1a-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="11e1a-120">Opzioni di compilazione più recente nella parte superiore dell'elenco versione</span><span class="sxs-lookup"><span data-stu-id="11e1a-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="11e1a-121">Aggiornamenti e miglioramenti</span><span class="sxs-lookup"><span data-stu-id="11e1a-121">Updates and Improvements</span></span>

* <span data-ttu-id="11e1a-122">Pacchetti di cui viene fatto riferimento `project.json` mobile con versione non verrà aggiornata per ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="11e1a-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="11e1a-123">Al contrario, si aggiornerà solo quando forzato per il ripristino, pulire, ricompilare o modificare `project.json`.</span><span class="sxs-lookup"><span data-stu-id="11e1a-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="11e1a-124">le origini dei repository NuGet.org non forzate in una configurazione di progetto quando si utilizza l'interfaccia utente di configurazione NuGet.</span><span class="sxs-lookup"><span data-stu-id="11e1a-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="11e1a-125">NuGet non ripristina i pacchetti in progetti condivisi né scrive un file di blocco.</span><span class="sxs-lookup"><span data-stu-id="11e1a-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="11e1a-126">Abbiamo migliorati errore di rete e ripetere la gestione di server non è raggiungibile o lento a rispondere.</span><span class="sxs-lookup"><span data-stu-id="11e1a-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="11e1a-127">I comportamenti di tastiera e mouse vengono aggiornati nell'UI gestione pacchetto di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="11e1a-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="11e1a-128">È ora supportano la versione più recente `project.json` schema DNX.</span><span class="sxs-lookup"><span data-stu-id="11e1a-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="11e1a-129">Modifiche di interruzione</span><span class="sxs-lookup"><span data-stu-id="11e1a-129">Breaking Changes</span></span>

* <span data-ttu-id="11e1a-130">Numeri di versione del pacchetto vengono normalizzati ora nel formato *principali*. *secondaria*. *patch*-*provvisoria* ogni versione principale e secondaria e applicare patch vengono considerati come numeri interi ed eliminare eventuali zeri iniziali.</span><span class="sxs-lookup"><span data-stu-id="11e1a-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="11e1a-131">Le informazioni sulla versione provvisoria viene considerate come una stringa e non vengono applicate modifiche a esso.</span><span class="sxs-lookup"><span data-stu-id="11e1a-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="11e1a-132">Questi numeri vengono usati nelle query per i client NuGet e la ricerca fornito dal servizio di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="11e1a-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="11e1a-133">Ulteriori dettagli, vedere la documentazione di NuGet in [versione provvisoria versioni](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="11e1a-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="11e1a-134">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="11e1a-134">Known Issues</span></span>

* <span data-ttu-id="11e1a-135">**Problema:** gli utenti di Windows 10 v1511 potrebbero riscontrare problemi o anche un blocco di Visual Studio con Powershell in Visual Studio negli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="11e1a-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="11e1a-136">L'installazione / disinstallazione di pacchetti con install.ps1 / uninstall.ps1 script</span><span class="sxs-lookup"><span data-stu-id="11e1a-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="11e1a-137">Il caricamento di progetti che dispone di uno script init.ps1 (ad esempio EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="11e1a-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="11e1a-138">Pubblicazione di contenuto web</span><span class="sxs-lookup"><span data-stu-id="11e1a-138">Publishing web content</span></span>

* <span data-ttu-id="11e1a-139">**Soluzione alternativa:** assicurarsi che l'installazione di Windows 10 è applicate le patch più recenti, expecially gennaio 2016 (KB 3124263) o un aggiornamento successivo.</span><span class="sxs-lookup"><span data-stu-id="11e1a-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="11e1a-140">Ulteriori dettagli sono disponibili su [problema #1638 di GitHub](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="11e1a-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="11e1a-141">**Problema:** i reindirizzamenti del protocollo NuGet versione 2 sono interrotti.</span><span class="sxs-lookup"><span data-stu-id="11e1a-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="11e1a-142">I repository NuGet personalizzati che reindirizzano le richieste a un host alternativo non soddisfano la richiesta di reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="11e1a-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="11e1a-143">**Soluzione alternativa:** per risolvere questo problema, configurare l'URI del repository di pacchetti nelle impostazioni in modo che punti al percorso del server reindirizzato.</span><span class="sxs-lookup"><span data-stu-id="11e1a-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="11e1a-144">Per ulteriori informazioni, vedere [richiesta pull GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="11e1a-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="11e1a-145">Continuiamo a tenere traccia dei problemi nella lista di problemi di GitHub che può essere trovato in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="11e1a-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>