---
title: Note sulla versione di NuGet 2.8.5
description: Note sulla versione per NuGet 2.8.5, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780351"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="44307-103">Note sulla versione di NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="44307-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="44307-104">Note sulla versione di [NuGet 2.8.3](../release-notes/nuget-2.8.3.md)  |  [Note sulla versione di NuGet versione 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="44307-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="44307-105">NuGet 2.8.5 è stato rilasciato il 30 marzo 2015.</span><span class="sxs-lookup"><span data-stu-id="44307-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="44307-106">Si tratta di un aggiornamento secondario di 2.8.3 VSIX con alcune correzioni mirate.</span><span class="sxs-lookup"><span data-stu-id="44307-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="44307-107">In questa versione è stata aggiunta la finestra di dialogo supporto per gestione pacchetti NuGet per i [moniker del Framework di destinazione DNX](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="44307-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="44307-108">Questi nuovi moniker di Framework supportati includono:</span><span class="sxs-lookup"><span data-stu-id="44307-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="44307-109">**core50** : moniker di Framework di destinazione ' base ' (TFM) compatibile con CLR di base.</span><span class="sxs-lookup"><span data-stu-id="44307-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="44307-110">**dnx452** : TFM specifico per le app basate su DNX che usano la versione completa di 4.5.2 del Framework</span><span class="sxs-lookup"><span data-stu-id="44307-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="44307-111">**dnx46** : TFM specifico per le app basate su DNX che usano la versione completa di 4,6 del Framework</span><span class="sxs-lookup"><span data-stu-id="44307-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="44307-112">**dnxcore50** : TFM specifico per le app basate su DNX che usano la versione di base 5,0 del Framework</span><span class="sxs-lookup"><span data-stu-id="44307-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="44307-113">È stato corretto un bug che impediva l'installazione corretta dei pacchetti nei progetti FSharp:</span><span class="sxs-lookup"><span data-stu-id="44307-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400