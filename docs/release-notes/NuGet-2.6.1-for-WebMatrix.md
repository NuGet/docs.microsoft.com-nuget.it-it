---
title: NuGet 2.6.1 per WebMatrix note
description: Note sulla versione per NuGet 2.6.1 per WebMatrix, inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550317"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 per WebMatrix note

[Note sulla versione per NuGet 2.6](../release-notes/nuget-2.6.md) | [note sulla versione per NuGet 2.7](../release-notes/nuget-2.7.md)

Il team di NuGet ha rilasciato un'aggiornato estensione Gestione pacchetti NuGet per WebMatrix 26 marzo 2014.  Questo aggiornamento può essere installato dal [raccolta di estensioni di WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) usando la procedura seguente:

1. Aprire WebMatrix 3
1. Fare clic sull'icona delle estensioni nella barra multifunzione Home
1. Selezionare la scheda aggiornamenti
1. Fare clic per aggiornare Gestione pacchetti NuGet alla versione 2.6.1
1. Chiudere e riavviare WebMatrix 3

## <a name="notable-changes"></a>Modifiche di rilievo

Questo aggiornamento risolve estensione due degli utenti principali problemi hanno dovuto affrontare dispendiosa in termini di pacchetti NuGet all'interno di WebMatrix.  Il primo è verificato un errore di versione dello schema di NuGet e il secondo è un bug iniziali alle DLL di zero byte nel `bin` cartella.

### <a name="nuget-schema-version-error"></a>Errore di versione dello Schema di NuGet

Dopo il rilascio di WebMatrix 3, le nuove funzionalità sono state introdotte in NuGet che richiedono una nuova versione dello schema per i pacchetti NuGet.  Quando si tenta di gestire i pacchetti NuGet nel sito web, questi nuovi pacchetti possono causare errori visualizzati in WebMatrix.

![Si è verificato un errore. La versione dello schema non è compatibile. Eseguire l'aggiornamento di NuGet alla versione più recente.](./media/NuGet-2.8/webmatrix-schema-version.png)

Questa versione più recente garantisce la compatibilità con i pacchetti NuGet più recente, impedendo che l'errore che si verificano. Le nuove versioni dei pacchetti, inclusi Microsoft.AspNet.WebPages ora possono essere installate in WebMatrix.  Alcuni di questi pacchetti usavano le funzionalità di NuGet, ad esempio [trasformazioni XDT config](../release-notes/nuget-2.6.md#xdt), che non era supportato in WebMatrix fino ad ora.

### <a name="zero-byte-dlls-in-bin-folder"></a>DLL a zero Byte nella cartella bin

Alcuni utenti hanno segnalato che dopo l'installazione di NuGet in pacchetti in WebMatrix che includono le DLL che viene copiate nel contenitore, che mostra la DLL nel `bin` cartella dei file di 0 byte.  Questa operazione interrompe l'applicazione in fase di esecuzione.

[Questo problema](https://nuget.codeplex.com/workitem/4060) ora risolto.

## <a name="other-recent-improvements"></a>Altri miglioramenti recenti

Quando fu rilasciato NuGet Package Manager 2.8 per Visual Studio, sono stati rilasciati anche Gestione pacchetti NuGet 2.5.0 per WebMatrix.  Mentre questa è stata menzionata la [note sulla versione di NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), viene non hai citato le specifiche delle nuove funzionalità che gli aggiornamenti introdotti.

### <a name="update-all"></a>Aggiorna tutto

È ora possibile aggiornare tutti i pacchetti del sito web in un unico passaggio.  Quando si apre l'estensione NuGet in WebMatrix, viene visualizzato l'elenco di tutti i pacchetti nella raccolta, quelle installate e quelli con gli aggiornamenti disponibili.  In precedenza, ogni pacchetto dovrà essere aggiornato singolarmente, ma ora è disponibile un pulsante "Aggiorna tutto" utile che viene visualizzato nella scheda aggiornamenti.

![Fare clic su Aggiorna tutto per aggiornare tutti i pacchetti con aggiornamenti disponibili](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Sovrascrivi file esistenti

Quando si installa i pacchetti che contengono i file già esistenti nel sito web, NuGet ha ignorato sempre automaticamente tali file (lasciare i file esistenti).  Questo potrebbe causare l'impressione che un pacchetto è stato installato o aggiornato correttamente quando in realtà non è stato.  NuGet verrà ora richiesto per i file verranno sovrascritti.

![Risoluzione dei conflitti di file](./media/NuGet-2.8/webmatrix-overwrite-file.png)
