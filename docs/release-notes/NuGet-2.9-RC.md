---
title: Note sulla versione di NuGet 2,9-RC
description: Note sulla versione per NuGet 2,9 RC, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b9d32f09fae7e12f81cf92b5b6e6b36c71d55f26
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780318"
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="c03e7-103">Note sulla versione di NuGet 2,9-RC</span><span class="sxs-lookup"><span data-stu-id="c03e7-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="c03e7-104">Note sulla versione di [NuGet 2.8.7](../release-notes/nuget-2.8.7.md)  |  [Note sulla versione di NuGet 3,0 Preview](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="c03e7-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="c03e7-105">NuGet 2,9 è stato rilasciato il 10 settembre 2015 come aggiornamento di 2.8.7 VSIX per Visual Studio 2012 e 2013.</span><span class="sxs-lookup"><span data-stu-id="c03e7-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="c03e7-106">Aggiornamenti in questa versione</span><span class="sxs-lookup"><span data-stu-id="c03e7-106">Updates in this release</span></span>

* <span data-ttu-id="c03e7-107">L'elaborazione dei pacchetti verrà ignorata se il `.nuspec` documento contenuto è in formato non corretto- [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="c03e7-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="c03e7-108">Correzione della gestione multipartwebrequest di \r\n per scenari UNIX/Linux- [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="c03e7-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="c03e7-109">Correzione dell'integrazione con gli eventi di compilazione in Visual Studio 2013 Community Edition- [1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="c03e7-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="c03e7-110">L'elenco completo delle correzioni in questa versione è disponibile in GitHub nell' [attività cardine 2.8.8](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="c03e7-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
