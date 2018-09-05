---
title: Note sulla versione 1.7 di NuGet
description: Note sulla versione per NuGet 1.7 inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 07cd541ef215d2a1bacc45995a22dadb6dfeac6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551467"
---
# <a name="nuget-17-release-notes"></a>Note sulla versione 1.7 di NuGet

[Note sulla versione di NuGet 1.6](../release-notes/nuget-1.6.md) | [note sulla versione di NuGet 1.8](../release-notes/nuget-1.8.md)

1.7 NuGet è stato rilasciato il 4 aprile 2012.

## <a name="known-installation-issue"></a>Problema di installazione noti
Se si esegue Visual Studio 2010 SP1, è possibile eseguire in un errore di installazione durante il tentativo di aggiornare NuGet, se è installata una versione precedente.

Per risolvere il problema è sufficiente disinstallare NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.  Per altre informazioni, vedere [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

Nota: Se Visual Studio non consentirà di disinstallare l'estensione (il pulsante Disinstalla è disabilitato), quindi probabile che sia necessario riavviare Visual Studio tramite "Esegui come amministratore".

## <a name="features"></a>Funzionalità

### <a name="support-opening-readmetxt-file-after-installation"></a>Supporto di apertura file Readme. txt al termine dell'installazione
Novità in 1.7, se il pacchetto include un `readme.txt` file nella radice del pacchetto, NuGet verrà automaticamente aperto il file al termine dell'installazione del pacchetto.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Mostra pacchetti versione non definitivo della finestra di dialogo Gestisci NuGet pacchetti
La finestra di dialogo Gestisci pacchetti NuGet include ora un elenco a discesa che fornisce l'opzione per visualizzare i pacchetti di versione non definitivo.

![Visualizzazione di pacchetti di versione non definitivo](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Mostra pulsante di ripristino dei pacchetti quando mancano i file di pacchetto
Quando si apre la console di gestione pacchetti o finestra di dialogo di pacchetti Manager NuGet, verifica se la soluzione corrente è abilitata la modalità di ripristino dei pacchetti NuGet e, se tutti i file del pacchetto non sono presenti il `packages` cartella. Se queste due condizioni vengono soddisfatte, NuGet invierà una notifica e verrà visualizzato un pulsante di ripristino pratico. Facendo clic su questo pulsante, si attiverà di NuGet per ripristinare tutti i pacchetti mancanti.

![Pulsante di ripristino del pacchetto nella finestra di dialogo](./media/packagerestore-dialog.png)

![Pulsante di ripristino del pacchetto nella console di](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Aggiungere file Packages. config a livello di soluzione
Nelle versioni precedenti di NuGet, ogni progetto ha un `packages.config` file che tiene traccia di quali pacchetti NuGet vengono installati in tale progetto. Tuttavia, si è verificato alcun file simili a livello di soluzione per tenere traccia dei pacchetti a livello di soluzione. Di conseguenza, vi era Nessuna possibilità di ripristinare i pacchetti a livello di soluzione.
Questa funzionalità è ora implementata in NuGet 1.7. Il livello di soluzione `packages.config` file si trova sotto il `.nuget` cartella nella soluzione root e verranno archiviati i pacchetti solo livello di soluzione.

### <a name="remove-new-package-command"></a>Rimuovere il comando New-Package
A causa di scarsa attività, il comando New-pacchetto è stato rimosso. Gli sviluppatori si consiglia di utilizzare nuget.exe o utile NuGet Package Explorer per creare pacchetti.

## <a name="bug-fixes"></a>Correzioni di bug
1.7 NuGet ha risolto numerosi bug per il ripristino del pacchetto del flusso di lavoro e scenari di controllo di rete di origine.

Per un elenco completo di lavoro gli elementi corretti in 1.7, NuGet, vista la [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
