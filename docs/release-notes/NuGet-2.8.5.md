---
title: Note sulla versione di NuGet 2.8.5
description: Note sulla versione per NuGet 2.8.5 inclusi noti problemi, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548625"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="4f7bf-103">Note sulla versione di NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="4f7bf-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="4f7bf-104">[Note sulla versione di NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [note sulla versione di NuGet versione 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="4f7bf-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="4f7bf-105">NuGet 2.8.5 è stata rilasciata il 30 marzo 2015.</span><span class="sxs-lookup"><span data-stu-id="4f7bf-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="4f7bf-106">Si tratta di un aggiornamento secondario al nostro 2.8.3 VSIX con alcune correzioni di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4f7bf-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="4f7bf-107">In questa versione è stato aggiunto il supporto per la finestra di dialogo Gestione pacchetti NuGet per [DNX Target Framework moniker](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="4f7bf-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="4f7bf-108">Questi nuovi moniker del framework supportate includono:</span><span class="sxs-lookup"><span data-stu-id="4f7bf-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="4f7bf-109">**core50** : un moniker di framework (TFM) che è compatibile con il Core CLR di destinazione 'base'.</span><span class="sxs-lookup"><span data-stu-id="4f7bf-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="4f7bf-110">**dnx452** App specifiche a basati su DNX un moniker Framework di destinazione utilizzando il 4.5.2 completo - versione di framework</span><span class="sxs-lookup"><span data-stu-id="4f7bf-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="4f7bf-111">**dnx46** App specifiche a basati su DNX un moniker Framework di destinazione utilizzando la versione 4.6 completo del framework:</span><span class="sxs-lookup"><span data-stu-id="4f7bf-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="4f7bf-112">**dnxcore50** App specifiche a basati su DNX un moniker Framework di destinazione utilizzando la versione 5.0 di Core del framework:</span><span class="sxs-lookup"><span data-stu-id="4f7bf-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="4f7bf-113">Da pacchetti ha impedito di installare correttamente nei progetti di FSharp è stato corretto un bug:</span><span class="sxs-lookup"><span data-stu-id="4f7bf-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400