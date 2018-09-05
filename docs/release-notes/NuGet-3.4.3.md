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
# <a name="nuget-343-release-notes"></a>Note sulla versione di NuGet 3.4.3

[Note sulla versione di NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [note sulla versione di NuGet 3.4.4](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 è stato rilasciato il 22 aprile 2016 a risolvere alcuni problemi che sono stati identificati nelle versioni 3.4 e successive.

È possibile scaricare il progetto VSIX sia nuget.exe [qui](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Aggiornamenti e miglioramenti

* Miglioramento dell'affidabilità Visual Studio. Sono stati corretti alcuni problemi di NuGet che ha causato gli arresti anomali in Visual Studio.

## <a name="fixes"></a>Correzioni

* Risolti alcuni problemi di autorizzazione con nuget privato protetto da password feed.
* Risolto un problema intorno all'impossibilità di ripristinare PCL da `project.json` con runtime specificati.
* Alcuni clienti erano in esecuzione in errori intermittenti durante l'installazione di pacchetti. Questo è stato ora risolto in questa versione.
* Risolto un problema che causava errori di ripristino in C + + / progetti con `project.json`.
* Alcuni pacchetti (ad esempio ModernHttpClient) in cui non è stato decompresso in modo corretto quando si usa nuget in mono. Questo è stato ora risolto in questa versione.

Per l'elenco completo delle correzioni e miglioramenti in questa versione, consultare l'elenco dei problemi [qui](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).