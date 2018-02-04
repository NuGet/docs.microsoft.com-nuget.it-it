---
title: Note sulla versione di NuGet 3.4.4 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per l'inclusione di NuGet 3.4.4 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet 3.4.4 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fabc10ae5c8e0bd43581f85c7763eb23e9483aaf
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-344-release-notes"></a>Note sulla versione di NuGet 3.4.4

[Note sulla versione di NuGet versione 3.4.3](../release-notes/nuget-3.4.3.md) | [note sulla versione 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md)

L'obiettivo principale di questa versione è stata miglioramenti alla qualità della versione 3.4.3 versione di nuget.exe con alcune correzioni nonché l'estensione di Visual Studio.

È possibile scaricare il progetto VSIX sia nuget.exe [qui](https://dist.nuget.org/index.html).

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Log delle modifiche completo](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Elenco dei problemi](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Modifiche

- Miglioramenti apportati al Service Pack: Miglioramenti compressione dei simboli, compressione con `project.json` e altre [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- Visualizzare l'eccezione quando si verifica un errore di ricerca di progetti nel comando di aggiornamento [\#605] (https://github.com/NuGet/NuGet.Client/pull/605
- Leggere il tipo di pacchetto da un input `.nuspec` e `project.json` quando compressione [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- Rendere NuGet.Shared non a un progetto. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Utilizzare il timeout di push come il timeout della risposta HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- File di pacchetto con futuri tentativi non avrà i relativi tempi utilizzati [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- L'aggiornamento `NuGet.Core.dll` versione 2.12.0 per risolvere il problema XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- Supportare./NuGet.CommandLine.XPlat - v \<dettaglio\> \<modalità\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- Visualizzazione errore durante il ripristino senza `project.json` o `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- La risoluzione delle versioni di dipendenza quando versioni richieste differiscono [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)