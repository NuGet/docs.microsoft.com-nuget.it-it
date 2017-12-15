---
title: Note sulla versione 2.2 NuGet | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 25389d8c-e7db-4920-ab5e-cff20cebee7e
description: "Note sulla versione per NuGet 2.2 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "2.2 NuGet note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 690e76a0686a5e7bb699410edef4a6e62ccd2a32
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-22-release-notes"></a>Note sulla versione 2.2 di NuGet

[Note sulla versione 2.1 NuGet](../release-notes/nuget-2.1.md) | [note sulla versione 2.2.1 NuGet](../release-notes/nuget-2.2.1.md)

2.2 NuGet è stato rilasciato il 12 dicembre 2012.

## <a name="visual-studio-quick-launch"></a>Avvio veloce di Visual Studio
Una delle nuove funzionalità che è stato aggiunto in Visual Studio 2012 è stato il [finestra avvio veloce](http://msdn.microsoft.com/library/hh417697.aspx). 2.2 NuGet estende questa finestra di dialogo che consente di inizializzare la finestra di dialogo di gestione di pacchetti con i termini di ricerca immessi in avvio veloce. Nei risultati per la ricerca di pacchetti NuGet corrispondenti a 'jquery' immettendo 'jquery' in avvio veloce ora include, ad esempio, un'opzione.

![NuGet in avvio veloce di Visual Studio](./media/quick-launch.png)

Se si seleziona questa opzione avvierà il standard NuGet package manager un'esperienza di ricerca per il termine 'jquery'.

![Finestra di dialogo Gestione pacchetti NuGet prepopolato](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Specificare l'intera cartella di contenuto del pacchetto
Ora consente di specificare un'intera cartella in NuGet 2.2 il `<file>` elemento del `.nuspec` file da includere tutto il contenuto della cartella. Ad esempio, il seguente causerà tutti gli script nella cartella script del pacchetto da aggiungere alla cartella contents\scripts quando il pacchetto viene installato in un progetto.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Aggiornare il 24/6/16: le cartelle vuote nella cartella "contenuto" verranno ignorate durante l'installazione del pacchetto.**

## <a name="known-issues"></a>Problemi noti

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Installazione del pacchetto ha esito negativo per i progetti F # quando si utilizza la console di gestione pacchetti
Quando si tenta di installare un pacchetto NuGet in un progetto F # mediante la console di gestione del pacchetto, viene generata un'eccezione InvalidOperationException. Stiamo lavorando attivamente con il team di F # per risolvere il problema, ma nel frattempo, la soluzione consiste nell'installare i pacchetti NuGet in progetti F # tramite una finestra di dialogo Gestione pacchetti NuGet anziché la console. [Altre informazioni sono disponibile in CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Correzioni di bug
NuGet 2.2 include varie correzioni di bug. Per un elenco completo di lavoro gli elementi corretti in NuGet 2.2,. visualizzazione di [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
