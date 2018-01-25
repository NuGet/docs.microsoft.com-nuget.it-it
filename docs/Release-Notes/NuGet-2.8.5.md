---
title: Note sulla versione di NuGet 2.8.5 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per l'inclusione di NuGet 2.8.5 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet 2.8.5 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ace56284e56f24394d49c0598ec3604b62caaf67
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-285-release-notes"></a>Note sulla versione di NuGet 2.8.5

[Note sulla versione di NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [note sulla versione di NuGet 2.8.6](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 è stato rilasciato il 30 marzo 2015. Si tratta di un aggiornamento secondario per il nostro 2.8.3 VSIX, con alcune destinazione correzioni.

In questa versione, è stato aggiunto il supporto per la finestra di dialogo Gestione pacchetti NuGet per [moniker Framework di destinazione DNX](https://github.com/aspnet/dnx).  Questi nuovi moniker del framework supportati includono:

* **core50** - il moniker del framework (TFM) compatibile con il Core CLR di destinazione 'base'.
* **dnx452** App delle specifiche di DNX TFM A utilizzando il 4.5.2 completo - versione di framework
* **dnx46** - app di specifiche di DNX TFM A utilizzando la versione di framework 4.6 completo
* **dnxcore50** - app di specifiche di DNX TFM A utilizzando la versione di framework di Core 5.0

Un bug è stato corretto che l'installazione nei progetti di FSharp correttamente i pacchetti non consentita:

https://nuget.codeplex.com/workitem/4400