---
title: Note sulla versione di NuGet 3.0 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 8ad13a67-9348-4f04-8f8b-b8f4a0b2c6df
description: "Note sulla versione per l'inclusione di NuGet 3.0.0 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet 3.0.0 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 95c4bf92f5eeb676fa6bcc3b7bcbf191efa9cb9e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-release-notes"></a>Note sulla versione 3.0 di NuGet

[Note sulla versione di NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [note sulla versione 3.1 NuGet](../release-notes/nuget-3.1.md)

NuGet 3.0 è stata rilasciata come estensione bundle di Visual Studio 2015 20 luglio 2015. Abbiamo inserito per fornire questa versione con Visual Studio in modo che l'esperienza di NuGet 3.0 aggiornata completezza deve essere disponibile per i nuovi utenti di Visual Studio. Questa versione dell'estensione NuGet è disponibile solo per Visual Studio 2015.

È consigliabile gli sviluppatori che dispongono dell'accesso per l'aggiornamento della raccolta di Visual Studio per la versione più recente è disponibile, come un aggiornamento attualmente vengono pubblicati poco dopo il rilascio di Visual Studio 2015 che contiene il supporto per lo sviluppo di Windows 10.

In totale, è stato chiuso 240 problemi nella versione 3.0 e puoi esaminare il [elenco completo dei problemi su GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Problemi noti

Si sono verificati alcuni problemi noti forniti con questa versione e di tutti gli elementi corretti nella versione 3.1 pianificato in occasione del rilascio di Windows 10 del 29 luglio.  Sarà in grado di aggiornare l'estensione di Visual Studio dalla raccolta o dopo tale data per risolvere questi problemi noti.

*  Conversione non viene fornita per l'etichetta "Non visualizzare più questo messaggio" nella finestra di anteprima e l'etichetta "Autori" nella finestra di descrizione del pacchetto.
*  Quando si lavora su un progetto TFS con controllo del codice sorgente, NuGet non è presente la gestione dei pacchetti dell'interfaccia utente se il file NuGet. config è contrassegnato come di sola lettura.
   * **Soluzione alternativa** estrarre il file da TFS.
*  Testo in giallo "riavvio barra" nella finestra di Powershell di NuGet non è visibile quando si usa il tema scuro di Visual Studio.
   * **Soluzione alternativa** utilizzare il tema chiaro Visual Studio.


## <a name="summary-of-top-issues-resolved"></a>Riepilogo dei principali problemi risolti

* [Aggiornamento rete frequenti viene chiamato quando viene aggiornata la finestra di gestione del pacchetto](https://github.com/NuGet/Home/issues/515)
* [Ritardo scorrimento installato modifica per visualizzare in Gestione pacchetti](https://github.com/NuGet/Home/issues/519)
* [Chiamate di rete devono essere eseguite su un thread in background](https://github.com/NuGet/Home/issues/516)
* [Aggiunta una casella di controllo 'Non visualizzare la finestra di anteprima'](https://github.com/NuGet/Home/issues/566)
* [Processo aggiunto la limitazione delle richieste per ridurre l'utilizzo del processore](https://github.com/NuGet/Home/issues/356)
* Migliorare la gestione dei riferimenti di libreria di classi portabile
    * [https://github.com/NuGet/home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Servizio di completamento automatico è stata fatta distinzione tra maiuscole e minuscole](https://github.com/NuGet/Home/issues/198)
* [Aggiornamento di ripristinare le credenziali di autenticazione di base](https://github.com/NuGet/Home/issues/456)
* [Registrazione migliorata degli errori](https://github.com/NuGet/Home/issues/407)
* [Messaggi di errore migliorata powershell durante la chiamata pacchetto di aggiornamento](https://github.com/NuGet/Home/issues/5)
* [Fissa il collegamento 'Ulteriori informazioni sulle opzioni' per impedire un arresto anomalo in Windows 10](https://github.com/NuGet/Home/issues/822)
* [Memorizza l'impostazione di casella di controllo di versione non definitiva](https://github.com/NuGet/Home/issues/732)
* [Gather migliorate le prestazioni memorizzando nella cache i risultati per i progetti in una soluzione](https://github.com/NuGet/Home/issues/721)
* [È possono raccogliere più pacchetti in parallelo](https://github.com/NuGet/Home/issues/713)
* [Ha rimosso il pacchetto di installazione-forzare il comando](https://github.com/NuGet/Home/issues/697)

Tenere d'occhio [blog](http://blog.nuget.org) per più lo stato di avanzamento e annunci man mano per fornire supporto per lo sviluppo di Windows 10.