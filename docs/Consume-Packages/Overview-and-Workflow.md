---
title: Panoramica e flusso di lavoro dell'uso di pacchetti NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3c60f920-457d-4f43-9efe-210c514e5242
description: Panoramica del processo di utilizzo dei pacchetti NuGet in un progetto, con collegamenti ad altre parti specifiche del processo.
keywords: Utilizzo di pacchetti NuGet, panoramica dell'utilizzo di pacchetti NuGet, flusso di lavoro dell'utilizzo di pacchetti NuGet, flusso di lavoro dell'utilizzo dei pacchetti, panoramica dell'utilizzo dei pacchetti
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c48351cb6fed0ac94bd437d9443811f46c032bd0
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="package-consumption-workflow"></a>Flusso di lavoro dell'utilizzo di pacchetti

Tra nuget.org e le raccolte di pacchetti private che un'organizzazione può stabilire, è possibile trovare decine di migliaia di pacchetti estremamente utili da usare all'interno di app e servizi. Ma indipendentemente dall'origine, l'utilizzo di un pacchetto segue lo stesso flusso di lavoro generale illustrato di seguito. Per maggiori dettagli, vedere [Ricerca e scelta di pacchetti](../consume-packages/finding-and-choosing-packages.md) e la [Guida rapida all'uso di un pacchetto](../quickstart/use-a-package.md).

![Flusso di selezione di un'origine pacchetto, ricerca di un pacchetto, installazione di un pacchetto in un progetto, aggiunta di un'istruzione Using e chiamate all'API del pacchetto](media/Overview-01-GeneralFlow.png)

\* _Tranne che con `nuget install` dalla riga di comando, nel qual caso è necessario modificare i file di configurazione manualmente. Vedere [install command reference](../tools/cli-ref-install.md) (Informazioni di riferimento sul comando install)._

NuGet memorizza l'identità e il numero di versione di ogni pacchetto installato, registrandoli in `packages.config`, nel file di progetto o in un file `project.json` nella radice del progetto, a seconda del tipo di progetto e della versione di NuGet in uso. Con NuGet 4.0+, l'[archiviazione delle dipendenze nel file di progetto](../consume-packages/package-references-in-project-files.md) è l'impostazione predefinita (tranne per i progetti UWP che hanno come destinazione Windows 10 RS1). In tutti i casi, è possibile esaminare il file appropriato in qualsiasi momento per visualizzare l'elenco completo delle dipendenze per il progetto.

> [!Tip]
> È consigliabile verificare sempre la licenza per ogni pacchetto che si intende usare nel software. Su nuget.org è disponibile un collegamento **License Info** (Informazioni di licenza) sul lato destro della pagina di descrizione di ogni pacchetto. Se per un pacchetto non sono specificate le condizioni di licenza, contattare il proprietario del pacchetto direttamente usando il collegamento **Contact owners** (Contatta proprietari) nella pagina del pacchetto. Microsoft non concede in licenza all'utente alcuna proprietà intellettuale dei provider di pacchetti di terze parti e non è responsabile delle informazioni fornite da terze parti.

Durante l'installazione dei pacchetti, NuGet verifica in genere se il pacchetto è già disponibile nella relativa cache. È possibile cancellare manualmente questa cache dalla riga di comando, come descritto in [Gestione delle cache NuGet](../consume-packages/managing-the-nuget-cache.md).

NuGet verifica inoltre che i framework di destinazione supportati dal pacchetto siano compatibili con il progetto. Se il pacchetto non contiene assembly compatibili, NuGet restituirà un messaggio di errore. Vedere [Risoluzione degli errori dei pacchetti incompatibili](dependency-resolution.md#resolving-incompatible-package-errors).

Quando si aggiunge il codice del progetto a un repository di origine, in genere non si includono i pacchetti NuGet. Gli utenti che clonano successivamente il repository, operazione che include agenti di compilazione in sistemi come Visual Studio Team Services, devono ripristinare i pacchetti necessari prima di eseguire una compilazione:

![Flusso di ripristino dei pacchetti NuGet tramite la clonazione di un repository e l'uso di un comando di ripristino](media/Overview-02-RestoreFlow.png)

L'opzione [Ripristino pacchetto](../consume-packages/package-restore.md) usa le informazioni nel file di progetto, `packages.config`, `project.json` per reinstallare tutte le dipendenze. Si noti che ci sono differenze nel processo interessato, come descritto in [Risoluzione delle dipendenze](../consume-packages/dependency-resolution.md).

In alcuni casi è necessario reinstallare i pacchetti che sono già inclusi in un progetto, reinstallando anche le dipendenze. Si tratta di un'operazione semplice da eseguire con il comando `reinstall` tramite la riga di comando di NuGet o la console di Gestione pacchetti NuGet. Per maggiori dettagli, vedere [Reinstallazione e aggiornamento di pacchetti](../consume-packages/reinstalling-and-updating-packages.md).

Infine, il comportamento di NuGet è determinato dai file di configurazione `Nuget.Config`. È possibile usare più file per centralizzare determinate impostazioni a livelli diversi, come illustrato in [Configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md).

In conclusione, con i pacchetti NuGet la codifica è produttiva.
