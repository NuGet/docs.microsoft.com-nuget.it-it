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
# <a name="nuget-344-release-notes"></a>Note sulla versione di NuGet 3.4.4

Note sulla versione di [NuGet 3.4.3](../release-notes/nuget-3.4.3.md)  |  [Note sulla versione di NuGet 3,5-beta](../release-notes/nuget-3.5-Beta.md)

L'obiettivo principale di questa versione è costituito dai miglioramenti apportati alla qualità della versione 3.4.3 di nuget.exe con alcune correzioni anche per l'estensione di Visual Studio.

È possibile scaricare sia VSIX che nuget.exe [qui](https://dist.nuget.org/index.html).

## <a name="344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Changelog completo](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Elenco di problemi](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Modifiche

- Miglioramenti di Pack: miglioramenti per la compressione dei simboli, compressione con `project.json` e altro ancora [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606)
- Visualizza l'eccezione quando si verifica un errore durante la ricerca di progetti nel comando di aggiornamento [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605
- Leggere il tipo di pacchetto dall'input `.nuspec` e `project.json` quando si imballa [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)
- Fare in modo che NuGet. Shared non sia un progetto. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Usare il timeout push come timeout di risposta HTTP [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599)
- I file di pacchetto con tempi futuri non avranno il tempo usato [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)
- Aggiornamento della `NuGet.Core.dll` versione di 2.12.0 per la correzione del problema XML [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)
- Supporto./NuGet.CommandLine.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)
- Visualizza errore durante il ripristino senza `project.json` o `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590)
- Correzione delle versioni delle dipendenze quando le versioni richieste sono diverse [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)