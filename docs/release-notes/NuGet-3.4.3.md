---
title: Note sulla versione di NuGet 3.4.3
description: Note sulla versione per NuGet 3.4.3, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776474"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="adaf7-103">Note sulla versione di NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="adaf7-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="adaf7-104">Note sulla versione di [NuGet 3.4.2](../release-notes/nuget-3.4.2.md)  |  [Note sulla versione di NuGet 3.4.4](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="adaf7-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="adaf7-105">NuGet 3.4.3 è stato rilasciato il 22 aprile 2016 per risolvere diversi problemi che sono stati identificati in 3,4 e nelle versioni successive.</span><span class="sxs-lookup"><span data-stu-id="adaf7-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="adaf7-106">È possibile scaricare sia VSIX che nuget.exe [qui](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="adaf7-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="adaf7-107">Aggiornamenti e miglioramenti</span><span class="sxs-lookup"><span data-stu-id="adaf7-107">Updates and Improvements</span></span>

* <span data-ttu-id="adaf7-108">Miglioramento dell'affidabilità di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="adaf7-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="adaf7-109">Sono stati corretti alcuni problemi in NuGet che causavano arresti anomali in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="adaf7-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="adaf7-110">Correzioni</span><span class="sxs-lookup"><span data-stu-id="adaf7-110">Fixes</span></span>

* <span data-ttu-id="adaf7-111">Correzione di alcuni problemi di autorizzazione con i feed NuGet privati protetti da password.</span><span class="sxs-lookup"><span data-stu-id="adaf7-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="adaf7-112">Correzione di un problema relativo all'impossibilità di ripristinare le librerie di classi portabili da `project.json` con Runtime specificati.</span><span class="sxs-lookup"><span data-stu-id="adaf7-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="adaf7-113">Alcuni clienti stavano riscontrando errori intermittenti durante l'installazione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="adaf7-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="adaf7-114">Questo problema è stato risolto in questa versione.</span><span class="sxs-lookup"><span data-stu-id="adaf7-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="adaf7-115">È stato risolto un problema che causava errori di ripristino nei progetti C++/CLI con `project.json` .</span><span class="sxs-lookup"><span data-stu-id="adaf7-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="adaf7-116">Alcuni pacchetti (ad esempio ModernHttpClient) in cui non vengono decompressi correttamente quando si usa NuGet in mono.</span><span class="sxs-lookup"><span data-stu-id="adaf7-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="adaf7-117">Questo problema è stato risolto in questa versione.</span><span class="sxs-lookup"><span data-stu-id="adaf7-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="adaf7-118">Per l'elenco completo delle correzioni e dei miglioramenti in questa versione, vedere l'elenco dei problemi [qui](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="adaf7-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>