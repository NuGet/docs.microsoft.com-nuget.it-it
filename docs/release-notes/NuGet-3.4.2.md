---
title: Note sulla versione di NuGet 3.4.2
description: Note sulla versione per NuGet 3.4.2, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780246"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="6b6b0-103">Note sulla versione di NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="6b6b0-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="6b6b0-104">Note sulla versione di [NuGet 3.4.1](../release-notes/nuget-3.4.1.md)  |  [Note sulla versione di NuGet 3.4.3](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="6b6b0-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="6b6b0-105">NuGet 3.4.2 è stato rilasciato l'8 aprile 2016 per risolvere diversi problemi identificati nella versione 3,4 e 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="6b6b0-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="6b6b0-106">nuget.exe 3.4.2 RC è ora disponibile</span><span class="sxs-lookup"><span data-stu-id="6b6b0-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="6b6b0-107">È possibile scaricare la versione finale candidata di nuget.exe 3.4.2 [qui](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="6b6b0-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="6b6b0-108">Aggiornamenti e miglioramenti</span><span class="sxs-lookup"><span data-stu-id="6b6b0-108">Updates and Improvements</span></span>

* <span data-ttu-id="6b6b0-109">Sono state migliorate significativamente le prestazioni degli aggiornamenti in uno scenario specifico, in cui gli aggiornamenti sui pacchetti con grafici con dipendenze approfondite hanno richiesto un tempo molto lungo e sono stati sospesi in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b6b0-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="6b6b0-110">il ripristino di NuGet senza traffico di rete è 2,5 x-3x più velocemente in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b6b0-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="6b6b0-111">Oltre a questa modifica, è stato risolto un problema per cui la rete veniva raggiunta due volte durante il recupero del numero di aggiornamenti nell'interfaccia utente di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b6b0-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="6b6b0-112">Questo è stato parzialmente responsabile di alcuni problemi di timeout riscontrati dai clienti in 3.4/3.4.1.</span><span class="sxs-lookup"><span data-stu-id="6b6b0-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="6b6b0-113">Aggiunta del supporto per l'impostazione di no_proxy</span><span class="sxs-lookup"><span data-stu-id="6b6b0-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="6b6b0-114">Correzioni</span><span class="sxs-lookup"><span data-stu-id="6b6b0-114">Fixes</span></span>

* <span data-ttu-id="6b6b0-115">È stato risolto un problema per cui l'origine nuget.org non era presente nelle impostazioni o nella configurazione di NuGet dopo l'aggiornamento alla 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="6b6b0-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="6b6b0-116">Correzione di un problema per cui una modifica di maiuscole e minuscole in FindPackagesById in 3.4.1 interrompe Artifactory.</span><span class="sxs-lookup"><span data-stu-id="6b6b0-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="6b6b0-117">Correzione di un problema con FIPS che ha causato errori con il ripristino NuGet con nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="6b6b0-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="6b6b0-118">Correzione di un arresto anomalo durante l'esplorazione di origini con URL icona non valido.</span><span class="sxs-lookup"><span data-stu-id="6b6b0-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="6b6b0-119">Correzione dei problemi relativi all'Unione di versioni e voci da "tutte le origini".</span><span class="sxs-lookup"><span data-stu-id="6b6b0-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="6b6b0-120">Problemi noti in 3.4.2 Windows x86 CommandLine (RC)</span><span class="sxs-lookup"><span data-stu-id="6b6b0-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="6b6b0-121">Questi problemi verranno risolti prima della prossima settimana prima di raggiungere la versione RTM.</span><span class="sxs-lookup"><span data-stu-id="6b6b0-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="6b6b0-122">L'esecuzione di NuGet Restore in una soluzione avrà esito negativo se il file della soluzione viene inserito in una gerarchia di cartelle inferiore rispetto ai file di progetto.</span><span class="sxs-lookup"><span data-stu-id="6b6b0-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="6b6b0-123">L'esecuzione del comando NuGet Delete in un pacchetto con il feed V2 avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="6b6b0-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="6b6b0-124">In alternativa, usare il feed V3.</span><span class="sxs-lookup"><span data-stu-id="6b6b0-124">Use V3 feed instead.</span></span>


<span data-ttu-id="6b6b0-125">Per l'elenco completo delle correzioni e dei miglioramenti in questa versione, vedere l'elenco dei problemi [qui](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="6b6b0-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>