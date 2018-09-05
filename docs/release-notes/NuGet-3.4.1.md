---
title: Note sulla versione di NuGet 3.4.1
description: Note sulla versione per NuGet 3.4.1, tra cui noti problemi, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e3f90646149b6a1a0e6a2639979110fb779d973c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547557"
---
# <a name="nuget-341-release-notes"></a>Note sulla versione di NuGet 3.4.1

[Note sulla versione di NuGet 3.4](../release-notes/nuget-3.4.md) | [note sulla versione di NuGet 3.4.2](../release-notes/nuget-3.4.2.md)

NuGet 3.4.1 è stata rilasciata il 30 marzo 2016 allo stesso tempo come Visual Studio 2015 Update 2 e Visual Studio 15 Preview Release a risolvere alcuni problemi che sono stati identificati nella versione 3.4.

## <a name="updates-and-improvements"></a>Aggiornamenti e miglioramenti

* Corretto un problema che impediva la visualizzazione di pacchetti dall'interfaccia utente di Visual Studio con un'installazione minima di Visual Studio
* Corretto un problema con l'individuazione di Visual Studio `lucene.net.dll`
* Tutte le origini non devono essere l'origine di repository predefinita dopo un'estensione NuGet di installare o aggiornare.  È possibile acconsentire esplicitamente a questa funzionalità, dalle impostazioni di configurazione.

Continuiamo a tenere traccia dei problemi nel nostro elenco di problemi di GitHub che può trovarsi in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)