---
title: Note sulla versione di NuGet 3,4
description: Note sulla versione per NuGet 3,4, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776422"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="6a5f3-103">Note sulla versione di NuGet 3,4</span><span class="sxs-lookup"><span data-stu-id="6a5f3-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="6a5f3-104">Note sulla versione [di NuGet 3,4-RC](../release-notes/nuget-3.4-RC.md)  |  [Note sulla versione di NuGet 3.4.1](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="6a5f3-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="6a5f3-105">NuGet 3,4 è stato rilasciato il 30 marzo 2016 come parte della versione Visual Studio 2015 Update 2 e Visual Studio 15 Preview ed è stato creato con alcuni principi in mente:</span><span class="sxs-lookup"><span data-stu-id="6a5f3-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="6a5f3-106">Supporto multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="6a5f3-106">Cross-Platform support</span></span>
* <span data-ttu-id="6a5f3-107">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="6a5f3-107">Performance improvements</span></span>
* <span data-ttu-id="6a5f3-108">Miglioramenti dell'interfaccia utente secondaria</span><span class="sxs-lookup"><span data-stu-id="6a5f3-108">Minor UI improvements</span></span>

<span data-ttu-id="6a5f3-109">Le funzionalità seguenti sono state aggiunte in precedenza in RC e sono state aggiornate o completate per la versione 3,4:</span><span class="sxs-lookup"><span data-stu-id="6a5f3-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="6a5f3-110">Nuove funzioni e caratteristiche</span><span class="sxs-lookup"><span data-stu-id="6a5f3-110">New Features</span></span>

* <span data-ttu-id="6a5f3-111">I client NuGet supportano ora la codifica di contenuto gzip dai repository</span><span class="sxs-lookup"><span data-stu-id="6a5f3-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="6a5f3-112">Supporto per PDB dai pacchetti nei progetti xproj</span><span class="sxs-lookup"><span data-stu-id="6a5f3-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="6a5f3-113">Supporto per le azioni di compilazione iOS e Android nell'elemento contentFiles</span><span class="sxs-lookup"><span data-stu-id="6a5f3-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="6a5f3-114">Supporto per i moniker del Framework netstandard e netstandardapp</span><span class="sxs-lookup"><span data-stu-id="6a5f3-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="6a5f3-115">Nuove funzionalità dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="6a5f3-115">New User Interface Features</span></span>

* <span data-ttu-id="6a5f3-116">Miglioramenti significativi delle prestazioni in particolare sulle schede installate, aggiornate e consolidate</span><span class="sxs-lookup"><span data-stu-id="6a5f3-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="6a5f3-117">L'origine dell'aggregazione ' tutte le origini pacchetti ' è disponibile con Unione dei risultati di ricerca corretta</span><span class="sxs-lookup"><span data-stu-id="6a5f3-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="6a5f3-118">Le schede installato e aggiornamenti sono ora ordinate in ordine alfabetico</span><span class="sxs-lookup"><span data-stu-id="6a5f3-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="6a5f3-119">È stato aggiunto un pulsante di aggiornamento che consente di aggiornare una ricerca</span><span class="sxs-lookup"><span data-stu-id="6a5f3-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="6a5f3-120">Opzioni di compilazione più recenti all'inizio dell'elenco di versioni</span><span class="sxs-lookup"><span data-stu-id="6a5f3-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="6a5f3-121">Aggiornamenti e miglioramenti</span><span class="sxs-lookup"><span data-stu-id="6a5f3-121">Updates and Improvements</span></span>

* <span data-ttu-id="6a5f3-122">I pacchetti a cui viene fatto riferimento in `project.json` che hanno una versione mobile non vengono aggiornati in ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="6a5f3-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="6a5f3-123">Verranno invece aggiornati solo quando è necessario eseguire il ripristino, la pulizia, la ricompilazione o la modifica `project.json` .</span><span class="sxs-lookup"><span data-stu-id="6a5f3-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="6a5f3-124">le origini del repository nuget.org non sono più forzate in una configurazione di progetto quando si usa l'interfaccia utente di configurazione di NuGet.</span><span class="sxs-lookup"><span data-stu-id="6a5f3-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="6a5f3-125">NuGet non ripristina più i pacchetti nei progetti condivisi né scrive un file di blocco.</span><span class="sxs-lookup"><span data-stu-id="6a5f3-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="6a5f3-126">Si è verificato un errore di rete migliorato ed è stato effettuato un nuovo tentativo di gestione per server non raggiungibili o lenti a risposta.</span><span class="sxs-lookup"><span data-stu-id="6a5f3-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="6a5f3-127">I comportamenti della tastiera e del mouse sono stati migliorati nell'interfaccia utente di gestione pacchetti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6a5f3-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="6a5f3-128">È ora supportato lo schema più recente `project.json` in DNX.</span><span class="sxs-lookup"><span data-stu-id="6a5f3-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="6a5f3-129">Modifiche di rilievo</span><span class="sxs-lookup"><span data-stu-id="6a5f3-129">Breaking Changes</span></span>

* <span data-ttu-id="6a5f3-130">I numeri di versione del pacchetto vengono ora normalizzati nel formato *principale*. *minore*. *patch* - di *versione preliminare*   Ogni principale, minore e patch viene considerato come numeri interi ed Elimina gli zeri iniziali.</span><span class="sxs-lookup"><span data-stu-id="6a5f3-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="6a5f3-131">Le informazioni sulla versione preliminare vengono considerate come una stringa e non vengono applicate modifiche.</span><span class="sxs-lookup"><span data-stu-id="6a5f3-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="6a5f3-132">Questi numeri vengono usati nelle query dai client NuGet e dalla ricerca fornita dal servizio nuget.org.</span><span class="sxs-lookup"><span data-stu-id="6a5f3-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="6a5f3-133">Per altri dettagli, vedere la documentazione di NuGet in [versioni provvisorie](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="6a5f3-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="6a5f3-134">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="6a5f3-134">Known Issues</span></span>

* <span data-ttu-id="6a5f3-135">**Problema:** Gli utenti di Windows 10 v1511 possono riscontrare problemi o anche un arresto anomalo di Visual Studio con PowerShell in Visual Studio negli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="6a5f3-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="6a5f3-136">Installazione/disinstallazione di pacchetti con script install.ps1/uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="6a5f3-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="6a5f3-137">Caricamento di progetti con uno script di init.ps1 (ad esempio EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="6a5f3-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="6a5f3-138">Pubblicazione di contenuto Web</span><span class="sxs-lookup"><span data-stu-id="6a5f3-138">Publishing web content</span></span>

* <span data-ttu-id="6a5f3-139">**Soluzione alternativa:** Assicurarsi che per l'installazione di Windows 10 siano applicate le patch più recenti, soprattutto il 2016 gennaio (KB 3124263) o un aggiornamento successivo.</span><span class="sxs-lookup"><span data-stu-id="6a5f3-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="6a5f3-140">Ulteriori informazioni sono disponibili sul [problema GitHub #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="6a5f3-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="6a5f3-141">**Problema:** i reindirizzamenti del protocollo NuGet versione 2 sono interrotti.</span><span class="sxs-lookup"><span data-stu-id="6a5f3-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="6a5f3-142">I repository NuGet personalizzati che reindirizzano le richieste a un host alternativo non soddisfano la richiesta di reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="6a5f3-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="6a5f3-143">**Soluzione alternativa:**  Per risolvere questo problema, configurare l'URI del repository del pacchetto in impostazioni in modo che punti al percorso del server reindirizzato.</span><span class="sxs-lookup"><span data-stu-id="6a5f3-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="6a5f3-144">Per altre informazioni, vedere [#387 della richiesta pull di GitHub](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="6a5f3-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="6a5f3-145">Continuiamo a tenere traccia dei problemi nell'elenco dei problemi di GitHub disponibili all'indirizzo: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="6a5f3-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>