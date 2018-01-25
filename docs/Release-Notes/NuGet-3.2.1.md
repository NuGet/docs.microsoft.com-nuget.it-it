---
title: Note sulla versione di NuGet 3.2.1 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per l'inclusione di NuGet 3.2.1 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet 3.2.1 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7c9c2457c33eb3630f632c98bf0cf96703c3a548
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="5bf5c-104">Note sulla versione di NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="5bf5c-104">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="5bf5c-105">[Note sulla versione 3.2 NuGet](../release-notes/nuget-3.2.md) | [note sulla versione 3.3 NuGet](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="5bf5c-105">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="5bf5c-106">NuGet 3.2.1 per la riga di comando è stato rilasciato il 12 ottobre 2015 con un numero limitato di ottimizzazioni e le correzioni per la versione 3.2 ed è disponibile da [dist.nuget.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="5bf5c-106">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="5bf5c-107">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="5bf5c-107">Improvements</span></span>

* <span data-ttu-id="5bf5c-108">NuGet Usa ora il file di configurazione con le maiuscole e minuscole originale di `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="5bf5c-108">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="5bf5c-109">Questo aspetto è importante nei sistemi operativi distinzione maiuscole/minuscole [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="5bf5c-109">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="5bf5c-110">Ripristino NuGet ora ignorerà i progetti dnx (`*.xproj`) che deve essere elaborato con `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="5bf5c-110">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="5bf5c-111">Ottimizzazione dell'utilizzo della rete quando si lavora con `index.json` e dati di registrazione del pacchetto [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="5bf5c-111">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="5bf5c-112">Download di risorse migliorate funzionalità di gestione per essere più affidabili con servizi v2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="5bf5c-112">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="5bf5c-113">Correzioni</span><span class="sxs-lookup"><span data-stu-id="5bf5c-113">Fixes</span></span>

* <span data-ttu-id="5bf5c-114">NuGet correttamente l'aggiornamento `.csproj` / `.vcxproj` riferimenti [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="5bf5c-114">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="5bf5c-115">Impediscono ora di creazione quando un SpecialFolders.UserProfile non è possibile individuare una cartella. NuGet locale [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="5bf5c-115">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="5bf5c-116">La gestione dei pacchetti nella cache locale che sono danneggiate durante il download migliorata [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="5bf5c-116">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="5bf5c-117">Un elenco completo dei problemi descritti per l'estensione di riga di comando e Visual Studio è disponibile in NuGet GitHub [3.2.1 attività cardine](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="5bf5c-117">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="5bf5c-118">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="5bf5c-118">Known Issues</span></span>

<span data-ttu-id="5bf5c-119">Continuiamo a tenere traccia dei problemi nell'elenco di problemi di GitHub in cui è reperibile in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="5bf5c-119">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>