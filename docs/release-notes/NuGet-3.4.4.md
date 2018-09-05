---
title: Note sulla versione di NuGet 3.4.4
description: Note sulla versione per NuGet 3.4.4 inclusi noti problemi, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547473"
---
# <a name="nuget-344-release-notes"></a>Note sulla versione di NuGet 3.4.4

[Note sulla versione di NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [note sulla versione 3.5-Beta NuGet](../release-notes/nuget-3.5-Beta.md)

L'obiettivo principale di questa versione è stata miglioramenti alla qualità del 3.4.3 versione di nuget.exe con alcune correzioni anche all'estensione di Visual Studio.

È possibile scaricare il progetto VSIX sia nuget.exe [qui](https://dist.nuget.org/index.html).

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Log delle modifiche completo](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Elenco dei problemi](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Modifiche

- Pack miglioramenti: Miglioramenti alla compressione dei simboli, con compressione `project.json` e altre [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- Visualizzare l'eccezione quando si verifica un errore di ricerca di progetti in comando update [\#605] (https://github.com/NuGet/NuGet.Client/pull/605
- Leggere il tipo di pacchetto da un input `.nuspec` e `project.json` la creazione [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- Rendere NuGet.Shared non a un progetto. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Usare il timeout di push come il timeout della risposta HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- I file di pacchetto con periodi futuri non avrà i rispettivi tempi usati [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- L'aggiornamento `NuGet.Core.dll` versione per risolvere il problema XML 2.12.0 [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- Supportare./NuGet.CommandLine.XPlat - v \</verbosity\> \<modalità\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- Visualizzazione errore durante il ripristino senza `project.json` oppure `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- Correggere le versioni delle dipendenze, se le versioni obbligatorie si differenziano [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)