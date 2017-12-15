---
title: Note sulla versione di NuGet 2.8.5 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 60b96b2e-2a61-4f10-b5ad-3299f5a6d453
description: "Note sulla versione per l'inclusione di NuGet 2.8.5 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet 2.8.5 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3b297704968b8423f60e9de08e27860dc375c019
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="0ee87-104">Note sulla versione di NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="0ee87-104">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="0ee87-105">[Note sulla versione di NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [note sulla versione di NuGet 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="0ee87-105">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="0ee87-106">NuGet 2.8.5 è stato rilasciato il 30 marzo 2015.</span><span class="sxs-lookup"><span data-stu-id="0ee87-106">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="0ee87-107">Si tratta di un aggiornamento secondario per il nostro 2.8.3 VSIX, con alcune destinazione correzioni.</span><span class="sxs-lookup"><span data-stu-id="0ee87-107">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="0ee87-108">In questa versione, è stato aggiunto il supporto per la finestra di dialogo Gestione pacchetti NuGet per [moniker Framework di destinazione DNX](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="0ee87-108">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="0ee87-109">Questi nuovi moniker del framework supportati includono:</span><span class="sxs-lookup"><span data-stu-id="0ee87-109">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="0ee87-110">**core50** - il moniker del framework (TFM) compatibile con il Core CLR di destinazione 'base'.</span><span class="sxs-lookup"><span data-stu-id="0ee87-110">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="0ee87-111">**dnx452** App delle specifiche di DNX TFM A utilizzando il 4.5.2 completo - versione di framework</span><span class="sxs-lookup"><span data-stu-id="0ee87-111">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="0ee87-112">**dnx46** - app di specifiche di DNX TFM A utilizzando la versione di framework 4.6 completo</span><span class="sxs-lookup"><span data-stu-id="0ee87-112">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="0ee87-113">**dnxcore50** - app di specifiche di DNX TFM A utilizzando la versione di framework di Core 5.0</span><span class="sxs-lookup"><span data-stu-id="0ee87-113">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="0ee87-114">Un bug è stato corretto che l'installazione nei progetti di FSharp correttamente i pacchetti non consentita:</span><span class="sxs-lookup"><span data-stu-id="0ee87-114">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

<span data-ttu-id="0ee87-115">https://NuGet.codeplex.com/WorkItem/4400</span><span class="sxs-lookup"><span data-stu-id="0ee87-115">https://nuget.codeplex.com/workitem/4400</span></span>