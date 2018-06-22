---
title: Note sulla versione di NuGet 2.8.5
description: Note sulla versione per l'inclusione di NuGet 2.8.5 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820079"
---
# <a name="nuget-285-release-notes"></a>Note sulla versione di NuGet 2.8.5

[Note sulla versione di NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [note sulla versione di NuGet 2.8.6](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 è stato rilasciato il 30 marzo 2015. Si tratta di un aggiornamento secondario per il nostro 2.8.3 VSIX, con alcune destinazione correzioni.

In questa versione, è stato aggiunto il supporto per la finestra di dialogo Gestione pacchetti NuGet per [moniker Framework di destinazione DNX](https://github.com/aspnet/dnx).  Questi nuovi moniker del framework supportati includono:

* **core50** - il moniker del framework (TFM) compatibile con il Core CLR di destinazione 'base'.
* **dnx452** App specifiche DNX basato su un TFM utilizzando 4.5.2 completo - versione di framework
* **dnx46** - App specifiche DNX basato su un TFM utilizzando la versione di framework 4.6 completo
* **dnxcore50** - App specifiche DNX basato su un TFM utilizzando la versione 5.0 dei componenti di base di framework

Un bug è stato corretto che l'installazione nei progetti di FSharp correttamente i pacchetti non consentita:

https://nuget.codeplex.com/workitem/4400