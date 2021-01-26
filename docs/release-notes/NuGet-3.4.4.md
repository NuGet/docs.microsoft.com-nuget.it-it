---
title: Note sulla versione di NuGet 3.4.4
description: Note sulla versione per NuGet 3.4.4, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780227"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="48acd-103">Note sulla versione di NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="48acd-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="48acd-104">Note sulla versione di [NuGet 3.4.3](../release-notes/nuget-3.4.3.md)  |  [Note sulla versione di NuGet 3,5-beta](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="48acd-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="48acd-105">L'obiettivo principale di questa versione è costituito dai miglioramenti apportati alla qualità della versione 3.4.3 di nuget.exe con alcune correzioni anche per l'estensione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="48acd-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="48acd-106">È possibile scaricare sia VSIX che nuget.exe [qui](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="48acd-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtm-2016-05-19"></a><span data-ttu-id="48acd-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="48acd-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="48acd-108">Changelog completo</span><span class="sxs-lookup"><span data-stu-id="48acd-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="48acd-109">Elenco di problemi</span><span class="sxs-lookup"><span data-stu-id="48acd-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="48acd-110">Modifiche</span><span class="sxs-lookup"><span data-stu-id="48acd-110">Changes</span></span>

- <span data-ttu-id="48acd-111">Miglioramenti di Pack: miglioramenti per la compressione dei simboli, compressione con `project.json` e altro ancora [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="48acd-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="48acd-112">Visualizza l'eccezione quando si verifica un errore durante la ricerca di progetti nel comando di aggiornamento [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="48acd-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="48acd-113">Leggere il tipo di pacchetto dall'input `.nuspec` e `project.json` quando si imballa [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="48acd-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="48acd-114">Fare in modo che NuGet. Shared non sia un progetto.</span><span class="sxs-lookup"><span data-stu-id="48acd-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="48acd-115">\#602</span><span class="sxs-lookup"><span data-stu-id="48acd-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="48acd-116">Usare il timeout push come timeout di risposta HTTP [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="48acd-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="48acd-117">I file di pacchetto con tempi futuri non avranno il tempo usato [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="48acd-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="48acd-118">Aggiornamento della `NuGet.Core.dll` versione di 2.12.0 per la correzione del problema XML [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="48acd-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="48acd-119">Supporto./NuGet.CommandLine.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="48acd-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="48acd-120">Visualizza errore durante il ripristino senza `project.json` o `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="48acd-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="48acd-121">Correzione delle versioni delle dipendenze quando le versioni richieste sono diverse [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="48acd-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>