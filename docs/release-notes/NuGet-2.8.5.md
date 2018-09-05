---
title: Note sulla versione di NuGet 2.8.5
description: Note sulla versione per NuGet 2.8.5 inclusi noti problemi, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548625"
---
# <a name="nuget-285-release-notes"></a>Note sulla versione di NuGet 2.8.5

[Note sulla versione di NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [note sulla versione di NuGet versione 2.8.6](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 è stata rilasciata il 30 marzo 2015. Si tratta di un aggiornamento secondario al nostro 2.8.3 VSIX con alcune correzioni di destinazione.

In questa versione è stato aggiunto il supporto per la finestra di dialogo Gestione pacchetti NuGet per [DNX Target Framework moniker](https://github.com/aspnet/dnx).  Questi nuovi moniker del framework supportate includono:

* **core50** : un moniker di framework (TFM) che è compatibile con il Core CLR di destinazione 'base'.
* **dnx452** App specifiche a basati su DNX un moniker Framework di destinazione utilizzando il 4.5.2 completo - versione di framework
* **dnx46** App specifiche a basati su DNX un moniker Framework di destinazione utilizzando la versione 4.6 completo del framework:
* **dnxcore50** App specifiche a basati su DNX un moniker Framework di destinazione utilizzando la versione 5.0 di Core del framework:

Da pacchetti ha impedito di installare correttamente nei progetti di FSharp è stato corretto un bug:

https://nuget.codeplex.com/workitem/4400