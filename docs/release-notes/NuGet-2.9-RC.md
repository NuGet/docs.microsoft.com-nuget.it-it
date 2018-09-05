---
title: Note sulla versione 2.9-RC di NuGet
description: Note sulla versione per NuGet 2.9 RC, tra cui i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 17c1c3a0c91928602aa47b5ba599faeac0424a4a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548324"
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="32ba7-103">Note sulla versione 2.9-RC di NuGet</span><span class="sxs-lookup"><span data-stu-id="32ba7-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="32ba7-104">[Note sulla versione di NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [note sulla versione di anteprima di NuGet 3.0](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="32ba7-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="32ba7-105">2.9 di NuGet è stata rilasciata il 10 settembre 2015 come un aggiornamento per il 2.8.7 VSIX per Visual Studio 2012 e 2013.</span><span class="sxs-lookup"><span data-stu-id="32ba7-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="32ba7-106">Aggiornamenti in questa versione</span><span class="sxs-lookup"><span data-stu-id="32ba7-106">Updates in this release</span></span>

* <span data-ttu-id="32ba7-107">A questo punto verrà ignorata l'elaborazione pacchetti se la classe contenuta `.nuspec` documento non è valido - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="32ba7-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="32ba7-108">Corretta gestione multipartwebrequest di \r\n per gli scenari di Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="32ba7-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="32ba7-109">Corretta integrazione con gli eventi di compilazione in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="32ba7-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="32ba7-110">L'elenco completo di correzioni disponibili in questa versione è reperibile in GitHub nel [2.8.8 attività cardine](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="32ba7-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
