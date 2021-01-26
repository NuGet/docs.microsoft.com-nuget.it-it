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
# <a name="nuget-343-release-notes"></a>Note sulla versione di NuGet 3.4.3

Note sulla versione di [NuGet 3.4.2](../release-notes/nuget-3.4.2.md)  |  [Note sulla versione di NuGet 3.4.4](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 è stato rilasciato il 22 aprile 2016 per risolvere diversi problemi che sono stati identificati in 3,4 e nelle versioni successive.

È possibile scaricare sia VSIX che nuget.exe [qui](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Aggiornamenti e miglioramenti

* Miglioramento dell'affidabilità di Visual Studio. Sono stati corretti alcuni problemi in NuGet che causavano arresti anomali in Visual Studio.

## <a name="fixes"></a>Correzioni

* Correzione di alcuni problemi di autorizzazione con i feed NuGet privati protetti da password.
* Correzione di un problema relativo all'impossibilità di ripristinare le librerie di classi portabili da `project.json` con Runtime specificati.
* Alcuni clienti stavano riscontrando errori intermittenti durante l'installazione dei pacchetti. Questo problema è stato risolto in questa versione.
* È stato risolto un problema che causava errori di ripristino nei progetti C++/CLI con `project.json` .
* Alcuni pacchetti (ad esempio ModernHttpClient) in cui non vengono decompressi correttamente quando si usa NuGet in mono. Questo problema è stato risolto in questa versione.

Per l'elenco completo delle correzioni e dei miglioramenti in questa versione, vedere l'elenco dei problemi [qui](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).