---
title: Note sulla versione 1.7 di NuGet
description: Note sulla versione per NuGet 1.7 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 81db81642ac21b7dd41f5940dfba919d0871ec01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820927"
---
# <a name="nuget-17-release-notes"></a>Note sulla versione 1.7 di NuGet

[Note sulla versione 1.6 NuGet](../release-notes/nuget-1.6.md) | [note sulla versione 1.8 NuGet](../release-notes/nuget-1.8.md)

NuGet 1.7 è stata rilasciata 4 aprile 2012.

## <a name="known-installation-issue"></a>Problema di installazione noti
Se si esegue Visual Studio 2010 SP1, è possibile eseguire in un errore di installazione durante il tentativo di aggiornare NuGet, se è installata una versione precedente.

La soluzione alternativa consiste nel disinstallare semplicemente NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.  Per altre informazioni, vedere [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

Nota: Se Visual Studio non consente di disinstallare l'estensione (il pulsante di disinstallazione è disabilitato), quindi probabile che sia necessario riavviare Visual Studio utilizzando "Esegui come amministratore".

## <a name="features"></a>Funzionalità

### <a name="support-opening-readmetxt-file-after-installation"></a>Supporto di apertura file Readme. txt dopo l'installazione
Novità di 1.7, se il pacchetto include un `readme.txt` file alla radice del pacchetto NuGet verrà aperto automaticamente questo file dopo avere completato l'installazione del pacchetto.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Mostra i pacchetti della versione provvisoria della finestra di dialogo Gestisci NuGet pacchetti
La finestra di dialogo Gestisci pacchetti NuGet include ora un elenco a discesa che fornisce l'opzione per visualizzare i pacchetti della versione provvisoria.

![Visualizzazione di pacchetti della versione provvisoria](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Mostra pulsante di ripristino dei pacchetti quando mancano i file di pacchetto
Quando si apre la console di gestione pacchetti o finestra di dialogo dei pacchetti NuGet gestione, controlla se la soluzione corrente è abilitata la modalità di ripristino dei pacchetti NuGet e, se mancano eventuali file di pacchetto di `packages` cartella. Se queste due condizioni vengono soddisfatte, NuGet invierà una notifica e verrà visualizzato un pulsante di ripristino semplice. Fare clic su questo pulsante attiverà NuGet per ripristinare tutti i pacchetti mancanti.

![Pulsante di ripristino del pacchetto nella finestra di dialogo](./media/packagerestore-dialog.png)

![Pulsante di ripristino del pacchetto nella console](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Aggiungere file a livello di soluzione Packages.
Nelle versioni precedenti di NuGet, ogni progetto dispone di un `packages.config` file che tiene traccia di quali pacchetti NuGet vengono installati in tale progetto. Tuttavia, si è verificato alcun file simile a livello di soluzione per tenere traccia dei pacchetti a livello di soluzione. Di conseguenza, si è verificato alcun modo per ripristinare i pacchetti a livello di soluzione.
Questa funzionalità è ora implementata in NuGet 1.7. A livello di soluzione `packages.config` file si trova sotto il `.nuget` cartella soluzione radice e verranno archiviati i pacchetti solo a livello di soluzione.

### <a name="remove-new-package-command"></a>Rimuovere il comando New-Package
A causa di scarso utilizzo, il comando New-Package è stato rimosso. Gli sviluppatori si consiglia di utilizzare nuget.exe o Esplora pacchetti NuGet utili per creare pacchetti.

## <a name="bug-fixes"></a>Correzioni di bug
1.7 NuGet è risolto numerosi bug per il ripristino dei pacchetti del flusso di lavoro e gli scenari di controllo di rete di origine.

Per un elenco completo di lavoro gli elementi corretti in NuGet 1.7,. visualizzazione di [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
