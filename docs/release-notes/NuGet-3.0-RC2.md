---
title: Note sulla versione di NuGet 3,0 RC2
description: Note sulla versione per NuGet 3,0 RC2, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780281"
---
# <a name="nuget-30-rc2-release-notes"></a>Note sulla versione di NuGet 3,0 RC2

Note sulla versione di [NuGet 3,0 RC](../release-notes/nuget-3.0-RC.md)  |  [Note sulla versione di NuGet 3,0](../release-notes/nuget-3.0.0.md)

NuGet 3,0 RC2 è stato rilasciato il 3 giugno 2015 come versione provvisoria disponibile dalla raccolta di estensioni di Visual Studio 2015 e da [codeplex](https://nuget.codeplex.com/releases/view/615507). Questa versione include alcune importanti correzioni di bug e miglioramenti delle prestazioni ritenuti importanti per il rilascio prima della versione completa di Visual Studio 2015. Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.

In totale, sono stati chiusi 158 problemi in questa versione ed è possibile esaminare l' [elenco completo dei problemi in GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

## <a name="summary-of-top-issues-resolved"></a>Riepilogo dei principali problemi risolti

* [Frequenti chiamate di aggiornamento della rete quando viene aggiornata la finestra di gestione pacchetti](https://github.com/NuGet/Home/issues/515)
* [Scorrimento ritardato durante la modifica della visualizzazione installata in Gestione pacchetti](https://github.com/NuGet/Home/issues/519)
* [Le chiamate di rete devono essere eseguite in un thread in background](https://github.com/NuGet/Home/issues/516)
* [È stata aggiunta la casella di controllo ' non visualizzare la finestra di anteprima '](https://github.com/NuGet/Home/issues/566)
* [Aggiunta limitazione del processo per ridurre l'utilizzo del processore](https://github.com/NuGet/Home/issues/356)
* Gestione migliorata dei riferimenti alla libreria di classi portabile
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Distinzione tra maiuscole e minuscole per il servizio AutoComplete](https://github.com/NuGet/Home/issues/198)
* [Aggiornare per reintrodurre le credenziali di autenticazione di base](https://github.com/NuGet/Home/issues/456)
* [È stata migliorata la registrazione degli errori](https://github.com/NuGet/Home/issues/407)
* [Messaggi di errore di PowerShell migliorati quando si chiama Update-Package](https://github.com/NuGet/Home/issues/5)

Scaricare questo [aggiornamento nell'estensione NuGet](https://nuget.codeplex.com/releases/view/615507) da CodePlex e tenere sotto controllo il [Blog](http://blog.nuget.org) per altri progressi e annunci per NuGet 3,0!