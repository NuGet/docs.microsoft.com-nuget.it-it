---
title: Note sulla versione di NuGet 3.4.2
description: Note sulla versione per NuGet 3.4.2 inclusi noti problemi, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549151"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="52085-103">Note sulla versione di NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="52085-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="52085-104">[Note sulla versione di NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [note sulla versione di NuGet 3.4.3](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="52085-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="52085-105">NuGet 3.4.2 è stato rilasciato l'8 aprile 2016 a risolvere alcuni problemi che sono stati identificati durante la 3.4 e 3.4.1 di rilascio.</span><span class="sxs-lookup"><span data-stu-id="52085-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="52085-106">NuGet.exe 3.4.2 RC è ora disponibile</span><span class="sxs-lookup"><span data-stu-id="52085-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="52085-107">È possibile scaricare la versione finale candidata di nuget.exe 3.4.2 [qui](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="52085-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="52085-108">Aggiornamenti e miglioramenti</span><span class="sxs-lookup"><span data-stu-id="52085-108">Updates and Improvements</span></span>

* <span data-ttu-id="52085-109">È stato migliorato in modo significativo le prestazioni degli aggiornamenti in uno scenario specifico, in cui gli aggiornamenti per i pacchetti con grafici di dipendenza completa richiede molto tempo e all'avvio di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52085-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="52085-110">ripristino di NuGet senza il traffico di rete è 2,5 x-3 volte più veloce all'interno di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52085-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="52085-111">Oltre a questa modifica, è stato risolto un problema in cui abbiamo stavamo raggiungere la rete due volte quando il numero di recupero dell'aggiornamento nell'interfaccia utente di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52085-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="52085-112">Questo è stato parzialmente responsabile per alcuni clienti di problemi di timeout esperti in 3.4/3.4.1.</span><span class="sxs-lookup"><span data-stu-id="52085-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="52085-113">Aggiunta del supporto per l'impostazione no_proxy</span><span class="sxs-lookup"><span data-stu-id="52085-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="52085-114">Correzioni</span><span class="sxs-lookup"><span data-stu-id="52085-114">Fixes</span></span>

* <span data-ttu-id="52085-115">Risolto un problema in cui origine di nuget.org non presente nella configurazione o impostazioni NuGet dopo l'aggiornamento a 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="52085-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="52085-116">Risolto un problema in cui una modifica di maiuscole e minuscole a FindPackagesById in 3.4.1 interrompe Artifactory.</span><span class="sxs-lookup"><span data-stu-id="52085-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="52085-117">Risolto un problema con FIPS che generava errori di ripristino di NuGet con nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="52085-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="52085-118">Corretto un arresto anomalo durante l'esplorazione delle origini con l'URL dell'icona non valido.</span><span class="sxs-lookup"><span data-stu-id="52085-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="52085-119">Risoluzione dei problemi con l'unione delle versioni e le voci da 'Tutte le origini'.</span><span class="sxs-lookup"><span data-stu-id="52085-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="52085-120">Problemi noti nella sezione 3.4.2 Windows x86 della riga di comando (RC)</span><span class="sxs-lookup"><span data-stu-id="52085-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="52085-121">Questi problemi verranno risolti anticipata prossima settimana prima sono stati raggiunti RTM.</span><span class="sxs-lookup"><span data-stu-id="52085-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="52085-122">Ripristino di nuget in esecuzione su una soluzione avrà esito negativo se il file della soluzione viene inserito in una gerarchia di cartelle inferiore rispetto ai file di progetto.</span><span class="sxs-lookup"><span data-stu-id="52085-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="52085-123">Esegue il comando di eliminazione di nuget in un pacchetto con il feed V2 avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="52085-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="52085-124">Usare feed di V3.</span><span class="sxs-lookup"><span data-stu-id="52085-124">Use V3 feed instead.</span></span>


<span data-ttu-id="52085-125">Per l'elenco completo delle correzioni e miglioramenti in questa versione, consultare l'elenco dei problemi [qui](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="52085-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>