---
title: Note sulla versione di NuGet 3.4 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 80a429f5-7569-4349-ad7f-4fe9218eac23
description: "Note sulla versione per NuGet 3.4, inclusi i problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet 3.4 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 911e4377ad9c8b1f865b0721f43ff73b62df6d1e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="ca2ca-104">Note sulla versione 3.4 di NuGet</span><span class="sxs-lookup"><span data-stu-id="ca2ca-104">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="ca2ca-105">[Note sulla versione 3.4 RC NuGet](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 note](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="ca2ca-105">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="ca2ca-106">NuGet 3.4 il 30 marzo 2016 è stato rilasciato come parte di Visual Studio 2015 Update 2 e Release di Visual Studio 15 Preview ed è stata compilata con alcuni principi in mente:</span><span class="sxs-lookup"><span data-stu-id="ca2ca-106">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

*  <span data-ttu-id="ca2ca-107">Supporto multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="ca2ca-107">Cross-Platform support</span></span>
*  <span data-ttu-id="ca2ca-108">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="ca2ca-108">Performance improvements</span></span>
*  <span data-ttu-id="ca2ca-109">Piccoli miglioramenti dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="ca2ca-109">Minor UI improvements</span></span>

<span data-ttu-id="ca2ca-110">Le funzionalità seguenti sono aggiunti in precedenza in RC e sono state aggiornate o completate per la versione 3.4:</span><span class="sxs-lookup"><span data-stu-id="ca2ca-110">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="ca2ca-111">Nuove funzionalità</span><span class="sxs-lookup"><span data-stu-id="ca2ca-111">New Features</span></span>

* <span data-ttu-id="ca2ca-112">I client NuGet ora supportano la codifica di contenuto gzip dai repository</span><span class="sxs-lookup"><span data-stu-id="ca2ca-112">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="ca2ca-113">Supporto per PDB dai pacchetti nei progetti xproj</span><span class="sxs-lookup"><span data-stu-id="ca2ca-113">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="ca2ca-114">Supporto per iOS e le azioni di compilazione Android nell'elemento contentFiles</span><span class="sxs-lookup"><span data-stu-id="ca2ca-114">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="ca2ca-115">Supporto per il moniker del framework moniker netstandard e netstandardapp</span><span class="sxs-lookup"><span data-stu-id="ca2ca-115">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="ca2ca-116">Nuove funzionalità dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="ca2ca-116">New User Interface Features</span></span>

* <span data-ttu-id="ca2ca-117">Miglioramenti significativi delle prestazioni in particolare nelle schede installato, aggiornamenti e Consolidate</span><span class="sxs-lookup"><span data-stu-id="ca2ca-117">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="ca2ca-118">Origine di aggregazione 'Tutte le origini pacchetti' è disponibile con l'unione di risultati di ricerca corretta</span><span class="sxs-lookup"><span data-stu-id="ca2ca-118">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="ca2ca-119">Installato e le schede degli aggiornamenti sono ora ordinate in ordine alfabetico</span><span class="sxs-lookup"><span data-stu-id="ca2ca-119">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="ca2ca-120">Aggiungere un pulsante di aggiornamento che consente una ricerca da aggiornare</span><span class="sxs-lookup"><span data-stu-id="ca2ca-120">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="ca2ca-121">Opzioni di compilazione più recente nella parte superiore dell'elenco versione</span><span class="sxs-lookup"><span data-stu-id="ca2ca-121">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="ca2ca-122">Aggiornamenti e miglioramenti</span><span class="sxs-lookup"><span data-stu-id="ca2ca-122">Updates and Improvements</span></span>

* <span data-ttu-id="ca2ca-123">Pacchetti di cui viene fatto riferimento `project.json` mobile con versione non verrà aggiornata per ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="ca2ca-123">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="ca2ca-124">Al contrario, si aggiornerà solo quando forzato per il ripristino, pulire, ricompilare o modificare `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ca2ca-124">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="ca2ca-125">le origini dei repository NuGet.org non forzate in una configurazione di progetto quando si utilizza l'interfaccia utente di configurazione NuGet.</span><span class="sxs-lookup"><span data-stu-id="ca2ca-125">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="ca2ca-126">NuGet non ripristina i pacchetti in progetti condivisi né scrive un file di blocco.</span><span class="sxs-lookup"><span data-stu-id="ca2ca-126">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="ca2ca-127">Abbiamo migliorati errore di rete e ripetere la gestione di server non è raggiungibile o lento a rispondere.</span><span class="sxs-lookup"><span data-stu-id="ca2ca-127">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="ca2ca-128">I comportamenti di tastiera e mouse vengono aggiornati nell'UI gestione pacchetto di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca2ca-128">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="ca2ca-129">È ora supportano la versione più recente `project.json` schema DNX.</span><span class="sxs-lookup"><span data-stu-id="ca2ca-129">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="ca2ca-130">Modifiche di interruzione</span><span class="sxs-lookup"><span data-stu-id="ca2ca-130">Breaking Changes</span></span>

* <span data-ttu-id="ca2ca-131">Numeri di versione del pacchetto vengono normalizzati ora nel formato *principali*. *secondaria*. *patch*-*provvisoria* ogni versione principale e secondaria e applicare patch vengono considerati come numeri interi ed eliminare eventuali zeri iniziali.</span><span class="sxs-lookup"><span data-stu-id="ca2ca-131">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="ca2ca-132">Le informazioni sulla versione provvisoria viene considerate come una stringa e non vengono applicate modifiche a esso.</span><span class="sxs-lookup"><span data-stu-id="ca2ca-132">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="ca2ca-133">Questi numeri vengono usati nelle query per i client NuGet e la ricerca fornito dal servizio di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ca2ca-133">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="ca2ca-134">Ulteriori dettagli, vedere la documentazione di NuGet in [versione provvisoria versioni](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ca2ca-134">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="ca2ca-135">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="ca2ca-135">Known Issues</span></span>

* <span data-ttu-id="ca2ca-136">**Problema:** agli utenti di Windows 10 v1511 potrebbero verificarsi problemi o anche un blocco di Visual Studio con Powershell in Visual Studio negli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="ca2ca-136">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="ca2ca-137">L'installazione / disinstallazione di pacchetti con install.ps1 / uninstall.ps1 script</span><span class="sxs-lookup"><span data-stu-id="ca2ca-137">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="ca2ca-138">Il caricamento di progetti che dispone di uno script init.ps1 (ad esempio EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="ca2ca-138">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="ca2ca-139">Pubblicazione di contenuto web</span><span class="sxs-lookup"><span data-stu-id="ca2ca-139">Publishing web content</span></span>

* <span data-ttu-id="ca2ca-140">**Soluzione alternativa:** assicurarsi che l'installazione di Windows 10 è applicate le patch più recenti, expecially di gennaio 2016 (KB 3124263) o un aggiornamento successivo.</span><span class="sxs-lookup"><span data-stu-id="ca2ca-140">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="ca2ca-141">Ulteriori dettagli sono disponibili su [il problema #1638 di GitHub](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="ca2ca-141">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="ca2ca-142">**Problema:** i reindirizzamenti del protocollo NuGet versione 2 sono interrotti.</span><span class="sxs-lookup"><span data-stu-id="ca2ca-142">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="ca2ca-143">I repository NuGet personalizzati che reindirizzano le richieste a un host alternativo non soddisfano la richiesta di reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="ca2ca-143">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="ca2ca-144">**Soluzione alternativa:** per risolvere questo problema, configurare l'URI del repository di pacchetti nelle impostazioni in modo che punti al percorso del server reindirizzato.</span><span class="sxs-lookup"><span data-stu-id="ca2ca-144">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="ca2ca-145">Per ulteriori informazioni, vedere [richiesta pull GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="ca2ca-145">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="ca2ca-146">Continuiamo a tenere traccia dei problemi nell'elenco di problemi di GitHub in cui è reperibile in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="ca2ca-146">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>