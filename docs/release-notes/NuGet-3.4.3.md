---
title: Note sulla versione di NuGet 3.4.3
description: Note sulla versione per NuGet 3.4.3, tra cui noti problemi, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549165"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="7bd3c-103">Note sulla versione di NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="7bd3c-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="7bd3c-104">[Note sulla versione di NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [note sulla versione di NuGet 3.4.4](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="7bd3c-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="7bd3c-105">NuGet 3.4.3 è stato rilasciato il 22 aprile 2016 a risolvere alcuni problemi che sono stati identificati nelle versioni 3.4 e successive.</span><span class="sxs-lookup"><span data-stu-id="7bd3c-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="7bd3c-106">È possibile scaricare il progetto VSIX sia nuget.exe [qui](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="7bd3c-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="7bd3c-107">Aggiornamenti e miglioramenti</span><span class="sxs-lookup"><span data-stu-id="7bd3c-107">Updates and Improvements</span></span>

* <span data-ttu-id="7bd3c-108">Miglioramento dell'affidabilità Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7bd3c-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="7bd3c-109">Sono stati corretti alcuni problemi di NuGet che ha causato gli arresti anomali in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7bd3c-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="7bd3c-110">Correzioni</span><span class="sxs-lookup"><span data-stu-id="7bd3c-110">Fixes</span></span>

* <span data-ttu-id="7bd3c-111">Risolti alcuni problemi di autorizzazione con nuget privato protetto da password feed.</span><span class="sxs-lookup"><span data-stu-id="7bd3c-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="7bd3c-112">Risolto un problema intorno all'impossibilità di ripristinare PCL da `project.json` con runtime specificati.</span><span class="sxs-lookup"><span data-stu-id="7bd3c-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="7bd3c-113">Alcuni clienti erano in esecuzione in errori intermittenti durante l'installazione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="7bd3c-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="7bd3c-114">Questo è stato ora risolto in questa versione.</span><span class="sxs-lookup"><span data-stu-id="7bd3c-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="7bd3c-115">Risolto un problema che causava errori di ripristino in C + + / progetti con `project.json`.</span><span class="sxs-lookup"><span data-stu-id="7bd3c-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="7bd3c-116">Alcuni pacchetti (ad esempio ModernHttpClient) in cui non è stato decompresso in modo corretto quando si usa nuget in mono.</span><span class="sxs-lookup"><span data-stu-id="7bd3c-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="7bd3c-117">Questo è stato ora risolto in questa versione.</span><span class="sxs-lookup"><span data-stu-id="7bd3c-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="7bd3c-118">Per l'elenco completo delle correzioni e miglioramenti in questa versione, consultare l'elenco dei problemi [qui](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="7bd3c-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>