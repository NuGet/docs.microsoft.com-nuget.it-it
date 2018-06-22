---
title: Note sulla versione 2.9 RC NuGet
description: Note sulla versione per NuGet 2.9 RC inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 15665e7c3f9f638b434b0d7be2f7ff3215c787c6
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819375"
---
# <a name="nuget-29-rc-release-notes"></a>Note sulla versione 2.9 RC NuGet

[Note sulla versione di NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [note sulla versione di anteprima di NuGet 3.0](../release-notes/nuget-3.0-preview.md)

2.9 NuGet è stato rilasciato il 10 settembre 2015, come un aggiornamento per il 2.8.7 VSIX per Visual Studio 2012 e 2013.

### <a name="updates-in-this-release"></a>Aggiornamenti in questa versione

* A questo punto verrà ignorata l'elaborazione pacchetti se i relativi contenuti `.nuspec` documento non è valido - [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Correzione gestione multipartwebrequest di \r\n per gli scenari di Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)
* Correzione di integrazione con gli eventi di compilazione in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)


L'elenco completo delle correzioni apportate in questa versione è reperibile in GitHub nel [2.8.8 attività cardine](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
