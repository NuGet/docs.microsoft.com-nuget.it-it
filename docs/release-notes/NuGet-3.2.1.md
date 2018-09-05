---
title: Note sulla versione di NuGet 3.2.1
description: Note sulla versione per NuGet 3.2.1, tra cui noti problemi, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548190"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="9756b-103">Note sulla versione di NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="9756b-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="9756b-104">[Note sulla versione di NuGet 3.2](../release-notes/nuget-3.2.md) | [note sulla versione di NuGet 3.3](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="9756b-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="9756b-105">NuGet 3.2.1 per la riga di comando è stato rilasciato il 12 ottobre 2015 grazie a una serie di ottimizzazioni e correzioni per la versione 3.2 ed è disponibile dal [dist.nuget.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="9756b-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="9756b-106">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="9756b-106">Improvements</span></span>

* <span data-ttu-id="9756b-107">NuGet ora Usa il file di configurazione con le maiuscole e minuscole originali di `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="9756b-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="9756b-108">Questo aspetto è importante nei sistemi operativi distinzione maiuscole/minuscole [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="9756b-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="9756b-109">Ripristino di NuGet ignorerà ora progetti dnx (`*.xproj`) che deve essere elaborato con `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="9756b-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="9756b-110">Ottimizzata l'utilizzo della rete quando si lavora con `index.json` e i dati di registrazione del pacchetto [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="9756b-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="9756b-111">Download delle risorse migliorate funzionalità di gestione per essere più affidabile con i servizi v2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="9756b-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="9756b-112">Correzioni</span><span class="sxs-lookup"><span data-stu-id="9756b-112">Fixes</span></span>

* <span data-ttu-id="9756b-113">Aggiornamento di NuGet aggiorni correttamente `.csproj` / `.vcxproj` riferimenti [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="9756b-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="9756b-114">Impediscono ora di creazione quando un SpecialFolders.UserProfile non è possibile individuare una cartella locale .nuget [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="9756b-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="9756b-115">La gestione dei pacchetti nella cache locale che sono danneggiate durante il download migliorata [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="9756b-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="9756b-116">Un elenco completo dei problemi risolti per l'estensione di riga di comando e Visual Studio è disponibili in GitHub di NuGet [3.2.1 attività cardine](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="9756b-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="9756b-117">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="9756b-117">Known Issues</span></span>

<span data-ttu-id="9756b-118">Continuiamo a tenere traccia dei problemi nel nostro elenco di problemi di GitHub che può trovarsi in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="9756b-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>