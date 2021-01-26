---
title: Note sulla versione di NuGet 3,0
description: Note sulla versione per NuGet 3.0.0, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776546"
---
# <a name="nuget-30-release-notes"></a>Note sulla versione di NuGet 3,0

Note sulla versione di [NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)  |  [Note sulla versione di NuGet 3,1](../release-notes/nuget-3.1.md)

NuGet 3,0 è stato rilasciato il 20 luglio 2015 come estensione del bundle a Visual Studio 2015. Abbiamo effettuato il push per fornire questa versione con Visual Studio in modo che l'esperienza completa aggiornata di NuGet 3,0 sia disponibile per i nuovi utenti di Visual Studio. Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.

Si consiglia agli sviluppatori che hanno accesso a Visual Studio Gallery di eseguire l'aggiornamento alla versione più recente disponibile, in quanto viene pubblicato un aggiornamento poco dopo il rilascio di Visual Studio 2015 che contiene il supporto per lo sviluppo di Windows 10.

In totale, sono stati chiusi 240 problemi nella versione 3,0 ed è possibile esaminare l' [elenco completo dei problemi in GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Problemi noti

Con questa versione sono stati introdotti numerosi problemi noti e tutti questi elementi sono stati risolti nella versione 3,1 prevista per coincidere con il rilascio di Windows 10 il 29 luglio.  È possibile aggiornare l'estensione di Visual Studio dalla raccolta in data o dopo tale data per risolvere questi problemi noti.

*  La traduzione non è stata specificata per l'etichetta "non visualizzare più questo messaggio" nella finestra di anteprima e l'etichetta "authors" nella finestra di descrizione del pacchetto.
*  Quando si usa un progetto con il controllo del codice sorgente TFS, NuGet non è in grado di presentare l'interfaccia utente di gestione pacchetti se il file Nuget.Config è contrassegnato come di sola lettura.
   * **Soluzione alternativa** Estrarre il file da TFS.
*  Quando si usa il tema scuro di Visual Studio, il testo nella "barra di riavvio" gialla della finestra di PowerShell di NuGet non è visibile.
   * **Soluzione alternativa** Usare il tema chiaro di Visual Studio.


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
* [Correzione del collegamento ' informazioni sulle opzioni ' per impedire arresti anomali in Windows 10](https://github.com/NuGet/Home/issues/822)
* [Ricorda impostazione della casella di controllo versione non definitiva](https://github.com/NuGet/Home/issues/732)
* [Miglioramento della raccolta delle prestazioni mediante la memorizzazione nella cache dei risultati tra i progetti in una soluzione](https://github.com/NuGet/Home/issues/721)
* [È possibile raccogliere più pacchetti in parallelo](https://github.com/NuGet/Home/issues/713)
* [Comando Install-Package-Force rimosso](https://github.com/NuGet/Home/issues/697)

Tieni sotto controllo il [nostro Blog](http://blog.nuget.org) per ottenere più informazioni sullo stato di avanzamento e sugli annunci, perché siamo pronti per offrire supporto per lo sviluppo in Windows 10.