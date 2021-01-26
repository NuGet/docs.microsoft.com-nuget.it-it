---
title: Note sulla versione di NuGet 1,7
description: Note sulla versione per NuGet 1,7, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777062"
---
# <a name="nuget-17-release-notes"></a>Note sulla versione di NuGet 1,7

Note sulla versione di [NuGet 1,6](../release-notes/nuget-1.6.md)  |  [Note sulla versione di NuGet 1,8](../release-notes/nuget-1.8.md)

NuGet 1,7 è stato rilasciato il 4 aprile 2012.

## <a name="known-installation-issue"></a>Problema di installazione noto
Se si esegue VS 2010 SP1, potrebbe essere rilevato un errore di installazione quando si tenta di aggiornare NuGet se è installata una versione precedente.

La soluzione alternativa consiste nel disinstallare semplicemente NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.  Per altre informazioni, vedere <https://support.microsoft.com/kb/2581019>.

Nota: se Visual Studio non consente di disinstallare l'estensione (il pulsante Disinstalla è disabilitato), probabilmente è necessario riavviare Visual Studio usando "Esegui come amministratore".

## <a name="features"></a>Funzionalità

### <a name="support-opening-readmetxt-file-after-installation"></a>Supporto per l'apertura del file di readme.txt dopo l'installazione
Novità in 1,7, se il pacchetto include un `readme.txt` file alla radice del pacchetto, NuGet aprirà automaticamente il file al termine dell'installazione del pacchetto.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Mostra pacchetti di versioni non definitive nella finestra di dialogo Gestisci pacchetti NuGet
La finestra di dialogo Gestisci pacchetti NuGet include ora un elenco a discesa che consente di visualizzare i pacchetti di versioni non definitive.

![Visualizzazione dei pacchetti di versioni non definitive](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Mostra il pulsante ripristino pacchetto quando mancano i file del pacchetto
Quando si apre la console di gestione pacchetti o la finestra di dialogo Gestione pacchetti NuGet, NuGet verificherà se la soluzione corrente ha abilitato la modalità di ripristino del pacchetto e se i file di pacchetto non sono presenti nella `packages` cartella. Se queste due condizioni sono soddisfatte, NuGet invierà una notifica e mostrerà un comodo pulsante Ripristina. Quando si fa clic su questo pulsante, NuGet viene attivato per ripristinare tutti i pacchetti mancanti.

![Pulsante ripristino pacchetti nella finestra di dialogo](./media/packagerestore-dialog.png)

![Pulsante ripristino pacchetto nella console di](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Aggiungi file di packages.config a livello di soluzione
Nelle versioni precedenti di NuGet ogni progetto dispone di un `packages.config` file che tiene traccia dei pacchetti NuGet installati in tale progetto. Tuttavia, non esisteva un file simile a livello di soluzione per tenere traccia dei pacchetti a livello di soluzione. Di conseguenza, non era possibile ripristinare i pacchetti a livello di soluzione.
Questa funzionalità è ora implementata in NuGet 1,7. Il file a livello di soluzione `packages.config` si trova sotto la `.nuget` cartella nella radice della soluzione e archivia solo i pacchetti a livello di soluzione.

### <a name="remove-new-package-command"></a>Rimuovi New-Package comando
A causa dell'utilizzo ridotto, il comando New-Package è stato rimosso. Si consiglia agli sviluppatori di usare nuget.exe o la comoda utilità di esplorazione pacchetti NuGet per creare pacchetti.

## <a name="bug-fixes"></a>Correzioni di bug
NuGet 1,7 ha risolto molti bug relativi al flusso di lavoro di ripristino del pacchetto e agli scenari di rete/controllo del codice sorgente.

Per un elenco completo degli elementi di lavoro corretti in NuGet 1,7, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
