---
title: Note sulla versione di NuGet 3.2.1
description: Note sulla versione per l'inclusione di NuGet 3.2.1 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 039fabaaacfdffd76fa88ff8183548e97cd4719b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="6502a-103">Note sulla versione di NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="6502a-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="6502a-104">[Note sulla versione di NuGet 3.2](../release-notes/nuget-3.2.md) | [note sulla versione di NuGet 3.3](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="6502a-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="6502a-105">NuGet 3.2.1 per la riga di comando è stato rilasciato il 12 ottobre 2015 con un numero limitato di ottimizzazioni e le correzioni per la versione 3.2 ed è disponibile da [dist.nuget.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="6502a-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="6502a-106">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="6502a-106">Improvements</span></span>

* <span data-ttu-id="6502a-107">NuGet Usa ora il file di configurazione con le maiuscole e minuscole originale di `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="6502a-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="6502a-108">Questo aspetto è importante in sistemi operativi distinzione maiuscole/minuscole [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="6502a-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="6502a-109">Ripristino NuGet ora ignorerà i progetti dnx (`*.xproj`) che deve essere elaborato con `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="6502a-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="6502a-110">Con ottimizzazione dell'utilizzo della rete quando si lavora `index.json` e i dati di registrazione del pacchetto [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="6502a-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="6502a-111">Download ottimale delle risorse gestione per essere più affidabili con i servizi v2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="6502a-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="6502a-112">Correzioni</span><span class="sxs-lookup"><span data-stu-id="6502a-112">Fixes</span></span>

* <span data-ttu-id="6502a-113">NuGet correttamente l'aggiornamento `.csproj` / `.vcxproj` riferimenti [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="6502a-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="6502a-114">Impediscono ora di creazione quando un SpecialFolders.UserProfile non è possibile individuare una cartella. NuGet locale [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="6502a-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="6502a-115">La gestione dei pacchetti nella cache locale che sono danneggiate durante il download migliorata [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="6502a-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="6502a-116">Un elenco completo dei problemi descritti per l'estensione di riga di comando e Visual Studio è disponibile in NuGet GitHub [3.2.1 attività cardine](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="6502a-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="6502a-117">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="6502a-117">Known Issues</span></span>

<span data-ttu-id="6502a-118">Continuiamo a tenere traccia dei problemi nella lista di problemi di GitHub che può essere trovato in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="6502a-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>