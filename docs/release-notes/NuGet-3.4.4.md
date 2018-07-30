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
# <a name="nuget-344-release-notes"></a>Note sulla versione di NuGet 3.4.4

[Note sulla versione di NuGet la versione 3.4.3](../release-notes/nuget-3.4.3.md) | [note sulla versione 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md)

L'obiettivo principale di questa versione è stata miglioramenti alla qualità della versione 3.4.3 versione di nuget.exe con alcune correzioni nonché l'estensione di Visual Studio.

È possibile scaricare il progetto VSIX sia nuget.exe [qui](https://dist.nuget.org/index.html).

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Log delle modifiche completo](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Elenco dei problemi](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Modifiche

- Miglioramenti apportati al Service Pack: Miglioramenti compressione dei simboli, con di compressione `project.json` e altre [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- Eccezione viene visualizzato quando si verifica un errore di ricerca di progetti nel comando di aggiornamento [\#605] (https://github.com/NuGet/NuGet.Client/pull/605
- Leggere il tipo di pacchetto da un input `.nuspec` e `project.json` quando compressione [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- Rendere NuGet.Shared non a un progetto. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Utilizzare il timeout di push come il timeout della risposta HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- File del pacchetto con futuri tentativi non avrà i relativi tempi utilizzati [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- L'aggiornamento `NuGet.Core.dll` versione da 2.12.0 per risolvere il problema XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- Supportare./NuGet.CommandLine.XPlat - v \<dettaglio\> \<modalità\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- Visualizzazione errore durante il ripristino senza `project.json` oppure `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- Correzione di versioni di dipendenza quando le versioni richieste differiscono [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)