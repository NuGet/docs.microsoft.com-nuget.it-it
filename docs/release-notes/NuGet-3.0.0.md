---
title: Note sulla versione 3.0 di NuGet
description: Note sulla versione per NuGet 3.0.0, tra cui noti problemi, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551863"
---
# <a name="nuget-30-release-notes"></a>Note sulla versione 3.0 di NuGet

[Note sulla versione di NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [note sulla versione di NuGet 3.1](../release-notes/nuget-3.1.md)

NuGet 3.0 è stato rilasciato il 20 luglio 2015 come estensione di bundle per Visual Studio 2015. Ci siamo concentrati per offrire questa versione con Visual Studio in modo che l'esperienza di NuGet 3.0 completata aggiornata sarà disponibile per i nuovi utenti di Visual Studio. Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.

È consigliabile per gli sviluppatori che dispongono dell'accesso per l'aggiornamento della raccolta di Visual Studio alla versione più recente che è disponibile, come viene pubblicata un'aggiornamento poco dopo il rilascio di Visual Studio 2015 che contiene il supporto per lo sviluppo di Windows 10.

In totale, abbiamo chiuso 240 problemi nella versione 3.0, ed è possibile esaminare i [elenco completo dei problemi in GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Problemi noti

Si sono verificati alcuni problemi noti fornito con questa versione e di tutti gli elementi corretti nella versione 3.1 pianificato coincide con il rilascio di Windows 10 al 29 luglio.  Si è in grado di aggiornare l'estensione di Visual Studio dalla raccolta o dopo tale data per risolvere questi problemi noti.

*  Conversione non viene fornita per l'etichetta "Non visualizzare più questo messaggio" nella finestra di anteprima e l'etichetta "Autori" nella finestra di descrizione del pacchetto.
*  Quando si lavora a un progetto usando TFS controllo del codice sorgente, NuGet non può presentare package manager dell'interfaccia utente se il file NuGet. config è contrassegnato come sola lettura.
   * **Soluzione alternativa** estrarre il file da TFS.
*  Testo in giallo "riavvio bar" nella finestra di Powershell di NuGet non è visibile quando si usa il tema scuro di Visual Studio.
   * **Soluzione alternativa** Usa il tema chiaro di Visual Studio.


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
* [Risolto il collegamento 'Altre informazioni sulle opzioni' per impedire un arresto anomalo in Windows 10](https://github.com/NuGet/Home/issues/822)
* [Ricordare di impostazione di casella di controllo di versione non definitiva](https://github.com/NuGet/Home/issues/732)
* [Gather migliorate le prestazioni memorizzando nella cache i risultati tra i progetti in una soluzione](https://github.com/NuGet/Home/issues/721)
* [Più pacchetti possono essere raccolte in parallelo](https://github.com/NuGet/Home/issues/713)
* [Rimosso install-package-forzare il comando](https://github.com/NuGet/Home/issues/697)

Teniamo d'occhio [nostro blog](http://blog.nuget.org) per più lo stato di avanzamento e annunci man mano che pronti a fornire supporto tecnico per lo sviluppo di Windows 10.