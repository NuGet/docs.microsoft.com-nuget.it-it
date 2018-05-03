---
title: NuGet 2.6.1 delle note sulla versione di WebMatrix
description: Note sulla versione per NuGet 2.6.1 per WebMatrix, inclusi i problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3d767788d348553cbb5cb82c6f70aac1894628c3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 delle note sulla versione di WebMatrix

[Note sulla versione 2.6 NuGet](../release-notes/nuget-2.6.md) | [note sulla versione 2.7 NuGet](../release-notes/nuget-2.7.md)

Il team di NuGet rilasciati da un'estensione Gestione pacchetti NuGet aggiornato per WebMatrix 26 marzo 2014.  Questo aggiornamento può essere installato dal [raccolta estensioni WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) usando la procedura seguente:

1. Aprire WebMatrix 3
1. Fare clic sull'icona di estensioni della barra multifunzione Home
1. Selezionare la scheda di aggiornamenti
1. Fare clic per aggiornare Gestione pacchetti NuGet per 2.6.1
1. Chiudere e riavviare WebMatrix 3

## <a name="notable-changes"></a>Modifiche significative

Questo aggiornamento risolve estensione due dei principali utenti problemi sono riscontrate dispendiosa in termini di pacchetti NuGet all'interno di WebMatrix.  Il primo è un errore di versione dello schema di NuGet e il secondo è un bug iniziali per le DLL a zero byte nel `bin` cartella.

### <a name="nuget-schema-version-error"></a>Errore di versione dello Schema di NuGet

Dopo il rilascio 3 WebMatrix, nuove funzionalità sono state introdotte in NuGet che richiedono una nuova versione dello schema per i pacchetti NuGet.  Durante il tentativo di gestire i pacchetti di NuGet nel sito web, questi nuovi pacchetti possono comportare errori visualizzati in WebMatrix.

![Si è verificato un errore. La versione dello schema non è compatibile. Aggiornare NuGet alla versione più recente.](./media/NuGet-2.8/webmatrix-schema-version.png)

Questa versione più recente garantisce la compatibilità con i pacchetti NuGet più recente, impedendo che l'errore che si verificano. Le nuove versioni dei pacchetti, inclusi Microsoft.AspNet.WebPages ora possono essere installate in WebMatrix.  Alcuni di questi pacchetti sono stati usare funzionalità di NuGet come [trasformazioni di configurazione XDT](../release-notes/nuget-2.6.md#xdt), che non è supportato in WebMatrix fino ad ora.

### <a name="zero-byte-dlls-in-bin-folder"></a>DLL di zero Byte nella cartella bin

Alcuni utenti hanno segnalato che dopo l'installazione di NuGet pacchetti in WebMatrix che includono le DLL che vengono copiate su bin, che mostra la DLL di nel `bin` cartella dei file di 0 byte.  L'applicazione viene interrotta in fase di esecuzione.

[Questo problema](https://nuget.codeplex.com/workitem/4060) ora è stato risolto.

## <a name="other-recent-improvements"></a>Altri miglioramenti di recente

Quando è stato rilasciato 2.8 di gestione pacchetti NuGet per Visual Studio, Gestione pacchetti NuGet 2.5.0 sono stati rilasciati anche per WebMatrix.  Mentre questo è stato riportato nel [note sulla versione di NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), è ancora specifica nuove funzionalità che gli aggiornamenti introdotti.

### <a name="update-all"></a>Aggiornare tutte

È ora possibile aggiornare tutti i pacchetti del sito web in un unico passaggio.  Quando si apre l'estensione NuGet in WebMatrix, di visualizzare l'elenco di tutti i pacchetti nella raccolta, questi sono installati e quelli con gli aggiornamenti disponibili.  In precedenza, ogni pacchetto deve essere aggiornato singolarmente, ma ora è disponibile un pulsante di "Aggiorna tutte" utile che viene visualizzato nella scheda aggiornamenti.

![Fare clic su Aggiorna tutto per aggiornare tutti i pacchetti con aggiornamenti disponibili](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Sovrascrivi file esistenti

Quando si installano i pacchetti che contengono i file già esistenti nel sito web, NuGet è sempre ignorati i file (lasciare i file esistenti).  Ciò potrebbe causare l'impressione che un pacchetto è stato installato o aggiornato correttamente quando in realtà non è stato.  NuGet verrà ora richiesto per i file devono essere sovrascritti.

![Risoluzione dei conflitti di file](./media/NuGet-2.8/webmatrix-overwrite-file.png)
