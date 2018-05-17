---
title: Note sulla versione di NuGet 2.8.5
description: Note sulla versione per l'inclusione di NuGet 2.8.5 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="7e889-103">Note sulla versione di NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="7e889-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="7e889-104">[Note sulla versione di NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [note sulla versione di NuGet 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="7e889-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="7e889-105">NuGet 2.8.5 è stato rilasciato il 30 marzo 2015.</span><span class="sxs-lookup"><span data-stu-id="7e889-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="7e889-106">Si tratta di un aggiornamento secondario per il nostro 2.8.3 VSIX, con alcune destinazione correzioni.</span><span class="sxs-lookup"><span data-stu-id="7e889-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="7e889-107">In questa versione, è stato aggiunto il supporto per la finestra di dialogo Gestione pacchetti NuGet per [moniker Framework di destinazione DNX](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="7e889-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="7e889-108">Questi nuovi moniker del framework supportati includono:</span><span class="sxs-lookup"><span data-stu-id="7e889-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="7e889-109">**core50** - il moniker del framework (TFM) compatibile con il Core CLR di destinazione 'base'.</span><span class="sxs-lookup"><span data-stu-id="7e889-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="7e889-110">**dnx452** App specifiche DNX basato su un TFM utilizzando 4.5.2 completo - versione di framework</span><span class="sxs-lookup"><span data-stu-id="7e889-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="7e889-111">**dnx46** - App specifiche DNX basato su un TFM utilizzando la versione di framework 4.6 completo</span><span class="sxs-lookup"><span data-stu-id="7e889-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="7e889-112">**dnxcore50** - App specifiche DNX basato su un TFM utilizzando la versione 5.0 dei componenti di base di framework</span><span class="sxs-lookup"><span data-stu-id="7e889-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="7e889-113">Un bug è stato corretto che l'installazione nei progetti di FSharp correttamente i pacchetti non consentita:</span><span class="sxs-lookup"><span data-stu-id="7e889-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400