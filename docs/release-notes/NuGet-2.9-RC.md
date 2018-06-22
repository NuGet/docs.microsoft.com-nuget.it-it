---
title: Note sulla versione 2.9 RC NuGet
description: Note sulla versione per NuGet 2.9 RC inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 15665e7c3f9f638b434b0d7be2f7ff3215c787c6
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819375"
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="c8927-103">Note sulla versione 2.9 RC NuGet</span><span class="sxs-lookup"><span data-stu-id="c8927-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="c8927-104">[Note sulla versione di NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [note sulla versione di anteprima di NuGet 3.0](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="c8927-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="c8927-105">2.9 NuGet è stato rilasciato il 10 settembre 2015, come un aggiornamento per il 2.8.7 VSIX per Visual Studio 2012 e 2013.</span><span class="sxs-lookup"><span data-stu-id="c8927-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="c8927-106">Aggiornamenti in questa versione</span><span class="sxs-lookup"><span data-stu-id="c8927-106">Updates in this release</span></span>

* <span data-ttu-id="c8927-107">A questo punto verrà ignorata l'elaborazione pacchetti se i relativi contenuti `.nuspec` documento non è valido - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="c8927-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="c8927-108">Correzione gestione multipartwebrequest di \r\n per gli scenari di Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="c8927-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="c8927-109">Correzione di integrazione con gli eventi di compilazione in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="c8927-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="c8927-110">L'elenco completo delle correzioni apportate in questa versione è reperibile in GitHub nel [2.8.8 attività cardine](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="c8927-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
