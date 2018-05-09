---
title: Note sulla versione di NuGet 3.4.1
description: Note sulla versione per l'inclusione di NuGet 3.4.1 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d492afc59fe2f9237aaf54dca56e09f9148a0dcf
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-341-release-notes"></a>Note sulla versione di NuGet 3.4.1

[Note sulla versione di NuGet 3.4](../release-notes/nuget-3.4.md) | [note sulla versione di NuGet sezione 3.4.2](../release-notes/nuget-3.4.2.md)

NuGet 3.4.1 è stato rilasciato il 30 marzo 2016 allo stesso tempo come Visual Studio 2015 Update 2 e versione Visual Studio 15 Preview a risolvere alcuni problemi che sono stati identificati nella versione 3.4.

## <a name="updates-and-improvements"></a>Aggiornamenti e miglioramenti

* Corretto un problema che impediva l'esplorazione dei pacchetti da interfaccia utente di Visual Studio con l'installazione minima di Visual Studio
* Correggere un problema con l'individuazione di Visual Studio `lucene.net.dll`
* Tutte le origini non devono essere l'origine di repository predefinito dopo un'estensione NuGet installare o aggiornare.  È possibile acconsentire esplicitamente a questa funzionalità, dalle impostazioni di configurazione.

Continuiamo a tenere traccia dei problemi nella lista di problemi di GitHub che può essere trovato in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)