---
title: Note sulla versione di NuGet versione 3.4.3 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per l'inclusione di NuGet versione 3.4.3 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet versione 3.4.3 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 68aab607659d15f96aefeab7bb90afc787710824
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="580a2-104">Note sulla versione di NuGet versione 3.4.3</span><span class="sxs-lookup"><span data-stu-id="580a2-104">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="580a2-105">[Note sulla versione di NuGet sezione 3.4.2](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 note](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="580a2-105">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="580a2-106">È stata rilasciata NuGet versione 3.4.3 22 aprile 2016 a risolvere alcuni problemi che sono stati identificati nelle versioni 3.4 o successive.</span><span class="sxs-lookup"><span data-stu-id="580a2-106">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="580a2-107">È possibile scaricare il progetto VSIX sia nuget.exe [qui](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="580a2-107">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="580a2-108">Aggiornamenti e miglioramenti</span><span class="sxs-lookup"><span data-stu-id="580a2-108">Updates and Improvements</span></span>

* <span data-ttu-id="580a2-109">Maggiore affidabilità di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="580a2-109">Improved Visual Studio reliability.</span></span> <span data-ttu-id="580a2-110">È stato risolto i problemi in NuGet che ha causato gli arresti anomali in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="580a2-110">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="580a2-111">Correzioni</span><span class="sxs-lookup"><span data-stu-id="580a2-111">Fixes</span></span>

* <span data-ttu-id="580a2-112">Risolti alcuni problemi di autorizzazione con nuget privato protetto da password feed.</span><span class="sxs-lookup"><span data-stu-id="580a2-112">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="580a2-113">Risolto un problema attorno all'impossibilità di ripristinare PCL da `project.json` con runtime specificati.</span><span class="sxs-lookup"><span data-stu-id="580a2-113">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="580a2-114">Alcuni clienti erano in esecuzione in verificati errori intermittenti durante l'installazione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="580a2-114">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="580a2-115">Questa ora è stato risolto in questa versione.</span><span class="sxs-lookup"><span data-stu-id="580a2-115">This has now been fixed in this release.</span></span>
* <span data-ttu-id="580a2-116">Risolto un problema che ha generato degli errori di ripristino in C + + CLI progetti con `project.json`.</span><span class="sxs-lookup"><span data-stu-id="580a2-116">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="580a2-117">Alcuni pacchetti (ad esempio ModernHttpClient) in cui non è stato decompresso correttamente quando si usa nuget in mono.</span><span class="sxs-lookup"><span data-stu-id="580a2-117">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="580a2-118">Questa ora è stato risolto in questa versione.</span><span class="sxs-lookup"><span data-stu-id="580a2-118">This has now been fixed in this release.</span></span>

<span data-ttu-id="580a2-119">Per l'elenco completo delle correzioni e miglioramenti in questa versione, consultare l'elenco dei problemi [qui](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="580a2-119">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>