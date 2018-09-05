---
title: Note sulla versione di NuGet 3.0 RC2
description: Note sulla versione per NuGet 3.0 RC2 inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 863e48e632387b768a43530b987683605baf6db7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545821"
---
# <a name="nuget-30-rc2-release-notes"></a>Note sulla versione di NuGet 3.0 RC2

[Note sulla versione per NuGet 3.0 RC](../release-notes/nuget-3.0-RC.md) | [note sulla versione di NuGet 3.0](../release-notes/nuget-3.0.0.md)

NuGet 3.0 RC2 è stato rilasciato 3 giugno 2015 come una versione provvisoria disponibile dalla raccolta di estensione di Visual Studio 2015 e [Codeplex](https://nuget.codeplex.com/releases/view/615507). Questa versione include numerose correzioni di bug importanti e miglioramenti delle prestazioni che è stato ritenuto erano importanti per rilasciare prima del rilascio di Visual Studio 2015 completato. Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.

In totale, abbiamo chiuso 158 problemi in questa versione, ed è possibile esaminare i [elenco completo dei problemi in GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

## <a name="summary-of-top-issues-resolved"></a>Riepilogo dei principali problemi risolti

* [Aggiornamenti frequenti rete viene chiamato quando viene aggiornata la finestra di gestione pacchetti](https://github.com/NuGet/Home/issues/515)
* [Scorrimento un ritardo se la modifica in installato visualizzazione in Gestione pacchetti](https://github.com/NuGet/Home/issues/519)
* [Le chiamate di rete devono essere eseguite su un thread in background](https://github.com/NuGet/Home/issues/516)
* [Aggiungere la casella di controllo 'Non visualizzare la finestra di anteprima'](https://github.com/NuGet/Home/issues/566)
* [Processo aggiunto la limitazione per ridurre l'utilizzo del processore](https://github.com/NuGet/Home/issues/356)
* Migliorata la gestione dei riferimenti di libreria di classi portabile
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Servizio di completamento automatico è stato in maiuscole / minuscole](https://github.com/NuGet/Home/issues/198)
* [Aggiornamento reintrodurre le credenziali di autenticazione di base](https://github.com/NuGet/Home/issues/456)
* [Registrazione degli errori migliorata](https://github.com/NuGet/Home/issues/407)
* [Messaggi di errore migliorata powershell quando si chiama Update-Package](https://github.com/NuGet/Home/issues/5)

Scaricare questa app [aggiornare l'estensione NuGet](https://nuget.codeplex.com/releases/view/615507) da Codeplex e teniamo d'occhio [nostro blog](http://blog.nuget.org) per più lo stato di avanzamento e annunci per NuGet 3.0!