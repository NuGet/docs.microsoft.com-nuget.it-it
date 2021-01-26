---
title: Note sulla versione di NuGet 2.8.5
description: Note sulla versione per NuGet 2.8.5, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780351"
---
# <a name="nuget-285-release-notes"></a>Note sulla versione di NuGet 2.8.5

Note sulla versione di [NuGet 2.8.3](../release-notes/nuget-2.8.3.md)  |  [Note sulla versione di NuGet versione 2.8.6](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 è stato rilasciato il 30 marzo 2015. Si tratta di un aggiornamento secondario di 2.8.3 VSIX con alcune correzioni mirate.

In questa versione è stata aggiunta la finestra di dialogo supporto per gestione pacchetti NuGet per i [moniker del Framework di destinazione DNX](https://github.com/aspnet/dnx).  Questi nuovi moniker di Framework supportati includono:

* **core50** : moniker di Framework di destinazione ' base ' (TFM) compatibile con CLR di base.
* **dnx452** : TFM specifico per le app basate su DNX che usano la versione completa di 4.5.2 del Framework
* **dnx46** : TFM specifico per le app basate su DNX che usano la versione completa di 4,6 del Framework
* **dnxcore50** : TFM specifico per le app basate su DNX che usano la versione di base 5,0 del Framework

È stato corretto un bug che impediva l'installazione corretta dei pacchetti nei progetti FSharp:

https://nuget.codeplex.com/workitem/4400