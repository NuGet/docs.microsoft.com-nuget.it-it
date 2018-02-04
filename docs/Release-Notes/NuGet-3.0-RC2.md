---
title: Note sulla versione di NuGet 3.0 RC2 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per NuGet 3.0 RC2 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "NuGet 3.0 RC2 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67299408170ae3c3676c2866bec2945b41ad4184
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-30-rc2-release-notes"></a>Note sulla versione di NuGet 3.0 RC2

[Note sulla versione RC di NuGet 3.0](../release-notes/nuget-3.0-RC.md) | [note sulla versione di NuGet 3.0](../release-notes/nuget-3.0.0.md)

NuGet 3.0 RC2 è stata rilasciata 3 giugno 2015 come una versione provvisoria dalla raccolta di estensioni di Visual Studio 2015 e [Codeplex](https://nuget.codeplex.com/releases/view/615507). Questa versione include un numero di importanti correzioni di bug e miglioramenti delle prestazioni che è stato ritenuto sono importanti per rilasciare prima del rilascio di Visual Studio 2015 completato. Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.

In totale, ci chiusura 158 problemi in questa versione, quindi è possibile esaminare il [elenco completo dei problemi su GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

## <a name="summary-of-top-issues-resolved"></a>Riepilogo dei principali problemi risolti

* [Aggiornamento rete frequenti viene chiamato quando viene aggiornata la finestra di gestione del pacchetto](https://github.com/NuGet/Home/issues/515)
* [Ritardo scorrimento installato modifica per visualizzare in Gestione pacchetti](https://github.com/NuGet/Home/issues/519)
* [Chiamate di rete devono essere eseguite su un thread in background](https://github.com/NuGet/Home/issues/516)
* [Aggiunta una casella di controllo 'Non visualizzare la finestra di anteprima'](https://github.com/NuGet/Home/issues/566)
* [Processo aggiunto la limitazione delle richieste per ridurre l'utilizzo del processore](https://github.com/NuGet/Home/issues/356)
* Migliorare la gestione dei riferimenti di libreria di classi portabile
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Servizio di completamento automatico è stata fatta distinzione tra maiuscole e minuscole](https://github.com/NuGet/Home/issues/198)
* [Aggiornamento di ripristinare le credenziali di autenticazione di base](https://github.com/NuGet/Home/issues/456)
* [Registrazione migliorata degli errori](https://github.com/NuGet/Home/issues/407)
* [Messaggi di errore migliorata powershell durante la chiamata pacchetto di aggiornamento](https://github.com/NuGet/Home/issues/5)

Scaricare questo [aggiornare l'estensione NuGet](https://nuget.codeplex.com/releases/view/615507) da Codeplex, tenere d'occhio [blog](http://blog.nuget.org) per più lo stato di avanzamento e annunci per NuGet 3.0!