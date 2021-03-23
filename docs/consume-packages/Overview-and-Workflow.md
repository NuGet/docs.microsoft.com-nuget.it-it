---
title: Panoramica e flusso di lavoro dell'uso di pacchetti NuGet
description: Panoramica del processo di utilizzo dei pacchetti NuGet in un progetto, con collegamenti ad altre parti specifiche del processo.
author: JonDouglas
ms.author: jodou
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: 92968236262f891106ab2d4cd3ba399f1644400b
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859213"
---
# <a name="package-consumption-workflow"></a>Flusso di lavoro dell'utilizzo di pacchetti

Tra nuget.org e le raccolte di pacchetti private che un'organizzazione può stabilire, è possibile trovare decine di migliaia di pacchetti estremamente utili da usare all'interno di app e servizi. Ma indipendentemente dall'origine, l'utilizzo di un pacchetto segue lo stesso flusso di lavoro generale.

![Flusso di selezione di un'origine pacchetto, ricerca di un pacchetto, installazione di un pacchetto in un progetto, aggiunta di un'istruzione Using e chiamate all'API del pacchetto](media/Overview-01-GeneralFlow.png)

\*_Solo Visual Studio e `dotnet.exe` . Il `nuget install` comando non modifica i file di progetto o il `packages.config` file. le voci devono essere gestite manualmente._

Per altri dettagli, vedere [Ricerca e scelta di pacchetti](../consume-packages/finding-and-choosing-packages.md) e [Cosa accade quando viene installato un pacchetto?](../concepts/package-installation-process.md).

NuGet memorizza l'identità e il numero di versione di ogni pacchetto installato, registrandoli nel file di progetto (con [PackageReference](../consume-packages/package-references-in-project-files.md)) o in [`packages.config`](../reference/packages-config.md), a seconda del tipo di progetto e della versione di NuGet in uso. Con NuGet 4.0+ è preferito PackageReference, anche se questa opzione è configurabile in Visual Studio tramite l'[interfaccia utente di Gestione pacchetti](install-use-packages-visual-studio.md). In tutti i casi, è possibile esaminare il file appropriato in qualsiasi momento per visualizzare l'elenco completo delle dipendenze per il progetto.

> [!Tip]
> È consigliabile verificare sempre la licenza per ogni pacchetto che si intende usare nel software. Su nuget.org è disponibile un collegamento **License Info** (Informazioni di licenza) sul lato destro della pagina di descrizione di ogni pacchetto. Se per un pacchetto non sono specificate le condizioni di licenza, contattare il proprietario del pacchetto direttamente usando il collegamento **Contact owners** (Contatta proprietari) nella pagina del pacchetto. Microsoft non concede in licenza all'utente alcuna proprietà intellettuale dei provider di pacchetti di terze parti e non è responsabile per le informazioni fornite da terze parti.

Durante l'installazione dei pacchetti, NuGet verifica in genere se il pacchetto è già disponibile nella relativa cache. È possibile cancellare manualmente questa cache dalla riga di comando, come descritto in [Gestione delle cartelle dei pacchetti globali e della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).

NuGet verifica inoltre che i framework di destinazione supportati dal pacchetto siano compatibili con il progetto. Se il pacchetto non contiene assembly compatibili, NuGet visualizza un errore. Vedere [Risoluzione degli errori dei pacchetti incompatibili](../concepts/dependency-resolution.md#resolving-incompatible-package-errors).

Quando si aggiunge il codice del progetto a un repository di origine, in genere non si includono i pacchetti NuGet. Gli utenti che clonano successivamente il repository o acquisiscono in altro modo il progetto, inclusi gli agenti di compilazione in sistemi come Visual Studio Team Services, devono ripristinare i pacchetti necessari prima di eseguire una compilazione:

![Flusso di ripristino dei pacchetti NuGet tramite la clonazione di un repository e l'uso di un comando di ripristino](media/Overview-02-RestoreFlow.png)

L'opzione [Ripristino pacchetto](../consume-packages/package-restore.md) usa le informazioni nel file di progetto o `packages.config` per reinstallare tutte le dipendenze. Si noti che ci sono differenze nel processo interessato, come descritto in [Risoluzione delle dipendenze](../concepts/dependency-resolution.md). Il diagramma precedente, poi, non visualizza un comando di ripristino per la console di Gestione pacchetti perché con la console si è già nel contesto di Visual Studio, che in genere ripristina automaticamente i pacchetti e fornisce il comando a livello di soluzione, come illustrato.

In alcuni casi è necessario reinstallare i pacchetti che sono già inclusi in un progetto, reinstallando anche le dipendenze. Si tratta di un'operazione semplice da eseguire con il comando `nuget reinstall` o la console di Gestione pacchetti NuGet. Per maggiori dettagli, vedere [Reinstallazione e aggiornamento di pacchetti](../consume-packages/reinstalling-and-updating-packages.md).

Infine, il comportamento di NuGet è determinato dai file `Nuget.Config`. È possibile usare più file per centralizzare determinate impostazioni a livelli diversi, come illustrato in [Configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md).

## <a name="ways-to-install-a-nuget-package"></a>Modi per installare un pacchetto NuGet

I pacchetti NuGet vengono scaricati e installati usando uno dei metodi descritti nella tabella seguente.

| Strumento | Piattaforme | Descrizione |
| --- | --- | --- |
| [Interfaccia della riga di comando di dotnet](install-use-packages-dotnet-cli.md) | Tutti | Strumento della riga di comando per librerie .NET Core e .NET Standard e per progetti in stile SDK destinati a .NET Framework (vedere [Attributo Sdk](/dotnet/core/tools/csproj#additions)). Recupera il pacchetto identificato da \<package_name\> e aggiunge un riferimento al file di progetto. Inoltre, recupera e installa le dipendenze. |
| Visual Studio | Windows e Mac | Fornisce un'interfaccia utente tramite la quale è possibile esplorare, selezionare e installare i pacchetti e le relative dipendenze in un progetto da un'origine del pacchetto specificata. Aggiunge i riferimenti ai pacchetti installati nel file di progetto.<ul><li>[Installare e gestire pacchetti con Visual Studio](install-use-packages-visual-studio.md)</li><li>[Inserimento di un pacchetto NuGet nel progetto (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [Console di Gestione pacchetti (Visual Studio)](install-use-packages-powershell.md) | Solo Windows | Recupera e installa il pacchetto identificato da \<package_name\> da un'origine selezionata in un progetto specificato nella soluzione, quindi aggiunge un riferimento al file di progetto. Inoltre, recupera e installa le dipendenze. |
| [Interfaccia della riga di comando di nuget.exe](install-use-packages-nuget-cli.md) | Tutti | Strumento della riga di comando per librerie .NET Framework e per i progetti non in stile SDK destinati alle librerie .NET Standard. Recupera il pacchetto identificato da \<package_name\> e ne espande il contenuto in una cartella nella directory corrente; può recuperare anche tutti i pacchetti elencati in un `packages.config` file. Inoltre, recupera e installa le dipendenze, ma non apporta modifiche ai file di progetto o a `packages.config`. |
