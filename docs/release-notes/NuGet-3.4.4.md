---
title: Note sulla versione di NuGet 3.4.4
description: Note sulla versione per l'inclusione di NuGet 3.4.4 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 891d5c7ee884d31f405118739b57a169b9cd93b3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820867"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="fb8f8-103">Note sulla versione di NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="fb8f8-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="fb8f8-104">[Note sulla versione di NuGet la versione 3.4.3](../release-notes/nuget-3.4.3.md) | [note sulla versione 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="fb8f8-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="fb8f8-105">L'obiettivo principale di questa versione è stata miglioramenti alla qualità della versione 3.4.3 versione di nuget.exe con alcune correzioni nonché l'estensione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb8f8-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="fb8f8-106">È possibile scaricare il progetto VSIX sia nuget.exe [qui](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="fb8f8-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="fb8f8-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="fb8f8-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="fb8f8-108">Log delle modifiche completo</span><span class="sxs-lookup"><span data-stu-id="fb8f8-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="fb8f8-109">Elenco dei problemi</span><span class="sxs-lookup"><span data-stu-id="fb8f8-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="fb8f8-110">Modifiche</span><span class="sxs-lookup"><span data-stu-id="fb8f8-110">Changes</span></span>

- <span data-ttu-id="fb8f8-111">Miglioramenti apportati al Service Pack: Miglioramenti compressione dei simboli, con di compressione `project.json` e altre [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="fb8f8-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="fb8f8-112">Eccezione viene visualizzato quando si verifica un errore di ricerca di progetti nel comando di aggiornamento [\#605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="fb8f8-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="fb8f8-113">Leggere il tipo di pacchetto da un input `.nuspec` e `project.json` quando compressione [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="fb8f8-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="fb8f8-114">Rendere NuGet.Shared non a un progetto.</span><span class="sxs-lookup"><span data-stu-id="fb8f8-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="fb8f8-115">\#602</span><span class="sxs-lookup"><span data-stu-id="fb8f8-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="fb8f8-116">Utilizzare il timeout di push come il timeout della risposta HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="fb8f8-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="fb8f8-117">File del pacchetto con futuri tentativi non avrà i relativi tempi utilizzati [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="fb8f8-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="fb8f8-118">L'aggiornamento `NuGet.Core.dll` versione da 2.12.0 per risolvere il problema XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="fb8f8-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="fb8f8-119">Supportare./NuGet.CommandLine.XPlat - v \<dettaglio\> \<modalità\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="fb8f8-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="fb8f8-120">Visualizzazione errore durante il ripristino senza `project.json` oppure `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="fb8f8-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="fb8f8-121">Correzione di versioni di dipendenza quando le versioni richieste differiscono [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="fb8f8-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>