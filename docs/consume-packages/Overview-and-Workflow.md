---
title: Panoramica e flusso di lavoro dell'uso di pacchetti NuGet
description: Panoramica del processo di utilizzo dei pacchetti NuGet in un progetto, con collegamenti ad altre parti specifiche del processo.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: 765b48b474aee17415f53491514bf6e9d50af010
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="package-consumption-workflow"></a>Flusso di lavoro dell'utilizzo di pacchetti

Tra nuget.org e le raccolte di pacchetti private che un'organizzazione può stabilire, è possibile trovare decine di migliaia di pacchetti estremamente utili da usare all'interno di app e servizi. Ma indipendentemente dall'origine, l'utilizzo di un pacchetto segue lo stesso flusso di lavoro generale.

![Flusso di selezione di un'origine pacchetto, ricerca di un pacchetto, installazione di un pacchetto in un progetto, aggiunta di un'istruzione Using e chiamate all'API del pacchetto](media/Overview-01-GeneralFlow.png)

\* _Solo Visual Studio e dotnet.exe. Il comando nuget install non modifica i file di progetto o il file packages.config. Le voci devono essere gestite manualmente._

Per altri dettagli, vedere [Ricerca e scelta di pacchetti](../consume-packages/finding-and-choosing-packages.md) e [Diversi modi per installare un pacchetto NuGet](ways-to-install-a-package.md).

NuGet memorizza l'identità e il numero di versione di ogni pacchetto installato, registrandoli in [`packages.config`](../reference/packages-config.md) o nel file di progetto (con [PackageReference](../consume-packages/package-references-in-project-files.md)), a seconda del tipo di progetto e della versione di NuGet in uso. Con NuGet 4.0 + è preferito PackageReference, anche se questa opzione è configurabile in Visual Studio tramite le [opzioni dell'interfaccia utente di Gestione pacchetti](../tools/package-manager-ui.md). In tutti i casi, è possibile esaminare il file appropriato in qualsiasi momento per visualizzare l'elenco completo delle dipendenze per il progetto.

> [!Tip]
> È consigliabile verificare sempre la licenza per ogni pacchetto che si intende usare nel software. Su nuget.org è disponibile un collegamento **License Info** (Informazioni di licenza) sul lato destro della pagina di descrizione di ogni pacchetto. Se per un pacchetto non sono specificate le condizioni di licenza, contattare il proprietario del pacchetto direttamente usando il collegamento **Contact owners** (Contatta proprietari) nella pagina del pacchetto. Microsoft non concede in licenza all'utente alcuna proprietà intellettuale dei provider di pacchetti di terze parti e non è responsabile delle informazioni fornite da terze parti.

Durante l'installazione dei pacchetti, NuGet verifica in genere se il pacchetto è già disponibile nella relativa cache. È possibile cancellare manualmente questa cache dalla riga di comando, come descritto in [Gestione delle cartelle dei pacchetti globali e della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).

NuGet verifica inoltre che i framework di destinazione supportati dal pacchetto siano compatibili con il progetto. Se il pacchetto non contiene assembly compatibili, NuGet visualizza un errore. Vedere [Risoluzione degli errori dei pacchetti incompatibili](dependency-resolution.md#resolving-incompatible-package-errors).

Quando si aggiunge il codice del progetto a un repository di origine, in genere non si includono i pacchetti NuGet. Gli utenti che clonano successivamente il repository o acquisiscono in altro modo il progetto, inclusi gli agenti di compilazione in sistemi come Visual Studio Team Services, devono ripristinare i pacchetti necessari prima di eseguire una compilazione:

![Flusso di ripristino dei pacchetti NuGet tramite la clonazione di un repository e l'uso di un comando di ripristino](media/Overview-02-RestoreFlow.png)

L'opzione [Ripristino pacchetto](../consume-packages/package-restore.md) usa le informazioni nel file di progetto o `packages.config` per reinstallare tutte le dipendenze. Si noti che ci sono differenze nel processo interessato, come descritto in [Risoluzione delle dipendenze](../consume-packages/dependency-resolution.md). Inoltre, il diagramma precedente non visualizza un comando di ripristino per la console di Gestione pacchetti perché con la console si è già nel contesto di Visual Studio, che in genere ripristina automaticamente i pacchetti e fornisce il comando a livello di soluzione, come illustrato.

In alcuni casi è necessario reinstallare i pacchetti che sono già inclusi in un progetto, reinstallando anche le dipendenze. Si tratta di un'operazione semplice da eseguire con il comando `nuget reinstall` o la console di Gestione pacchetti NuGet. Per maggiori dettagli, vedere [Reinstallazione e aggiornamento di pacchetti](../consume-packages/reinstalling-and-updating-packages.md).

Infine, il comportamento di NuGet è determinato dai file `Nuget.Config`. È possibile usare più file per centralizzare determinate impostazioni a livelli diversi, come illustrato in [Configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md).

In conclusione, con i pacchetti NuGet la codifica è produttiva.
