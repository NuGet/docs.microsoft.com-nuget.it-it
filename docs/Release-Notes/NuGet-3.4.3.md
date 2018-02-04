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
# <a name="nuget-343-release-notes"></a>Note sulla versione di NuGet versione 3.4.3

[Note sulla versione di NuGet sezione 3.4.2](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 note](../release-notes/nuget-3.4.4.md)

È stata rilasciata NuGet versione 3.4.3 22 aprile 2016 a risolvere alcuni problemi che sono stati identificati nelle versioni 3.4 o successive.

È possibile scaricare il progetto VSIX sia nuget.exe [qui](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Aggiornamenti e miglioramenti

* Maggiore affidabilità di Visual Studio. È stato risolto i problemi in NuGet che ha causato gli arresti anomali in Visual Studio.

## <a name="fixes"></a>Correzioni

* Risolti alcuni problemi di autorizzazione con nuget privato protetto da password feed.
* Risolto un problema attorno all'impossibilità di ripristinare PCL da `project.json` con runtime specificati.
* Alcuni clienti erano in esecuzione in verificati errori intermittenti durante l'installazione di pacchetti. Questa ora è stato risolto in questa versione.
* Risolto un problema che ha generato degli errori di ripristino in C + + CLI progetti con `project.json`.
* Alcuni pacchetti (ad esempio ModernHttpClient) in cui non è stato decompresso correttamente quando si usa nuget in mono. Questa ora è stato risolto in questa versione.

Per l'elenco completo delle correzioni e miglioramenti in questa versione, consultare l'elenco dei problemi [qui](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).