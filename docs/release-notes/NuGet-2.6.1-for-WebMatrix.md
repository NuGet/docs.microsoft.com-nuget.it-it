---
title: Note sulla versione di NuGet 2.6.1 per WebMatrix
description: Note sulla versione per NuGet 2.6.1 per WebMatrix, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780427"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>Note sulla versione di NuGet 2.6.1 per WebMatrix

Note sulla versione di [NuGet 2,6](../release-notes/nuget-2.6.md)  |  [Note sulla versione di NuGet 2,7](../release-notes/nuget-2.7.md)

Il team NuGet ha rilasciato un'estensione di gestione pacchetti NuGet aggiornata per WebMatrix il 26 marzo 2014.  Questo aggiornamento può essere installato dalla [raccolta di estensioni WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) attenendosi alla procedura seguente:

1. Apri WebMatrix 3
1. Fare clic sull'icona estensioni nella scheda Home della barra multifunzione
1. Selezionare la scheda aggiornamenti
1. Fare clic per aggiornare Gestione pacchetti NuGet a 2.6.1
1. Chiudere e riavviare WebMatrix 3

## <a name="notable-changes"></a>Modifiche rilevanti

Questo aggiornamento dell'estensione risolve due dei principali problemi riscontrati dagli utenti per l'utilizzo di pacchetti NuGet all'interno di WebMatrix.  Il primo è un errore di versione dello schema NuGet e il secondo è un bug che conduce a DLL a zero byte nella `bin` cartella.

### <a name="nuget-schema-version-error"></a>Errore di versione dello schema NuGet

Poiché WebMatrix 3 è stato rilasciato, nuove funzionalità sono state introdotte in NuGet che richiedono una nuova versione dello schema per i pacchetti NuGet.  Quando si tenta di gestire i pacchetti NuGet nel sito Web, questi nuovi pacchetti possono causare errori visualizzati in WebMatrix.

![Si è verificato un errore. La versione dello schema non è compatibile. Aggiornare NuGet alla versione più recente.](./media/NuGet-2.8/webmatrix-schema-version.png)

Questa versione più recente offre la compatibilità con i pacchetti NuGet più recenti, evitando che questo errore si verifichi. Le nuove versioni dei pacchetti, tra cui Microsoft. AspNet. WebPages, possono ora essere installate in WebMatrix.  Alcuni di questi pacchetti usavano le funzionalità di NuGet, ad esempio le [trasformazioni di configurazione di xdt](../release-notes/nuget-2.6.md#xdt), che finora non era supportata in WebMatrix.

### <a name="zero-byte-dlls-in-bin-folder"></a>Zero-Byte dll nella cartella bin

Alcuni utenti hanno segnalato che dopo l'installazione di pacchetti NuGet in WebMatrix che includono dll che vengono copiate nel contenitore, le dll vengono visualizzate nella `bin` cartella come file da 0 byte.  Questa operazione interrompe l'applicazione in fase di esecuzione.

[Questo problema](https://nuget.codeplex.com/workitem/4060) è stato risolto.

## <a name="other-recent-improvements"></a>Altri miglioramenti recenti

Quando la versione di gestione pacchetti NuGet 2,8 è stata rilasciata per Visual Studio, è stato rilasciato anche gestione pacchetti NuGet 2.5.0 per WebMatrix.  Sebbene sia stato menzionato nelle [Note sulla versione di NuGet 2,8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), non sono state citate le nuove funzionalità specifiche introdotte dall'aggiornamento.

### <a name="update-all"></a>Aggiorna tutto

È ora possibile aggiornare tutti i pacchetti del sito Web in un unico passaggio.  Quando si apre l'estensione NuGet in WebMatrix, viene visualizzato l'elenco di tutti i pacchetti nella raccolta, quelli installati e quelli con aggiornamenti disponibili.  In precedenza, ogni pacchetto deve essere aggiornato singolarmente, ma ora è disponibile un pulsante "Aggiorna tutto" che viene visualizzato nella scheda aggiornamenti.

![Fare clic su Aggiorna tutto per aggiornare tutti i pacchetti con gli aggiornamenti disponibili](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Sovrascrivi file esistenti

Quando si installano pacchetti che contengono file già presenti nel sito Web, NuGet ha sempre ignorato automaticamente i file (lasciando solo i file esistenti).  Questo potrebbe comportare l'impressione che un pacchetto sia stato installato o aggiornato correttamente quando in realtà non lo era.  In NuGet verrà ora richiesto di sovrascrivere i file.

![Risoluzione dei conflitti di file](./media/NuGet-2.8/webmatrix-overwrite-file.png)
