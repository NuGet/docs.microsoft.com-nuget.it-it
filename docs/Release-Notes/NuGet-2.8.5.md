---
title: Note sulla versione di NuGet 2.8.5 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per l'inclusione di NuGet 2.8.5 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet 2.8.5 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ace56284e56f24394d49c0598ec3604b62caaf67
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="e838f-104">Note sulla versione di NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="e838f-104">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="e838f-105">[Note sulla versione di NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [note sulla versione di NuGet 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="e838f-105">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="e838f-106">NuGet 2.8.5 è stato rilasciato il 30 marzo 2015.</span><span class="sxs-lookup"><span data-stu-id="e838f-106">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="e838f-107">Si tratta di un aggiornamento secondario per il nostro 2.8.3 VSIX, con alcune destinazione correzioni.</span><span class="sxs-lookup"><span data-stu-id="e838f-107">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="e838f-108">In questa versione, è stato aggiunto il supporto per la finestra di dialogo Gestione pacchetti NuGet per [moniker Framework di destinazione DNX](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="e838f-108">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="e838f-109">Questi nuovi moniker del framework supportati includono:</span><span class="sxs-lookup"><span data-stu-id="e838f-109">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="e838f-110">**core50** - il moniker del framework (TFM) compatibile con il Core CLR di destinazione 'base'.</span><span class="sxs-lookup"><span data-stu-id="e838f-110">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="e838f-111">**dnx452** App delle specifiche di DNX TFM A utilizzando il 4.5.2 completo - versione di framework</span><span class="sxs-lookup"><span data-stu-id="e838f-111">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="e838f-112">**dnx46** - app di specifiche di DNX TFM A utilizzando la versione di framework 4.6 completo</span><span class="sxs-lookup"><span data-stu-id="e838f-112">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="e838f-113">**dnxcore50** - app di specifiche di DNX TFM A utilizzando la versione di framework di Core 5.0</span><span class="sxs-lookup"><span data-stu-id="e838f-113">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="e838f-114">Un bug è stato corretto che l'installazione nei progetti di FSharp correttamente i pacchetti non consentita:</span><span class="sxs-lookup"><span data-stu-id="e838f-114">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

<span data-ttu-id="e838f-115">https://nuget.codeplex.com/workitem/4400</span><span class="sxs-lookup"><span data-stu-id="e838f-115">https://nuget.codeplex.com/workitem/4400</span></span>