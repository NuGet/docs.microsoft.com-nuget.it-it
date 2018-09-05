---
title: Note sulla versione 2.2 di NuGet
description: Note sulla versione per NuGet 2.2 inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545992"
---
# <a name="nuget-22-release-notes"></a>Note sulla versione 2.2 di NuGet

[Note sulla versione di NuGet 2.1](../release-notes/nuget-2.1.md) | [note sulla versione di NuGet 2.2.1](../release-notes/nuget-2.2.1.md)

2.2 di NuGet è stato rilasciato il 12 dicembre 2012.

## <a name="visual-studio-quick-launch"></a>Avvio veloce di Visual Studio
Una delle nuove funzionalità che è stato aggiunto in Visual Studio 2012 è stata la [della finestra di avvio veloce](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). 2.2 di NuGet si estende questa finestra di dialogo, in modo che possa inizializzare la finestra di dialogo Gestione pacchetti con i termini di ricerca immessi in avvio veloce. Nei risultati della ricerca i pacchetti NuGet corrispondenti a 'jquery' immettendo 'jquery' in avvio veloce ora include ad esempio, un'opzione.

![NuGet in Visual Studio avvio veloce](./media/quick-launch.png)

Se si seleziona questa opzione avvierà il standard NuGet package manager esperienza di ricerca del termine 'jquery'.

![Finestra di dialogo Gestione pacchetti NuGet prepopolato](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Specificare l'intera cartella del contenuto del pacchetto
2.2 NuGet ora consente di specificare un'intera cartella nel `<file>` elemento del `.nuspec` file da includere tutto il contenuto di tale cartella. Ad esempio, di seguito determinerà tutti gli script nella cartella script del pacchetto da aggiungere nella cartella contents\scripts quando il pacchetto viene installato in un progetto.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Aggiornamento 6 o 24/16: le cartelle vuote nella cartella "content" vengono ignorate quando si installa il pacchetto.**

## <a name="known-issues"></a>Problemi noti

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Installazione del pacchetto ha esito negativo per i progetti F # quando si usa la console di gestione pacchetti
Quando provi a installare un pacchetto NuGet in un progetto F # tramite la console di gestione pacchetti, viene generata un'eccezione InvalidOperationException. Stiamo lavorando attivamente con il team F # per risolvere il problema, ma nel frattempo, la soluzione alternativa consiste nell'installare pacchetti NuGet nei progetti F # tramite finestra di dialogo Gestione pacchetti NuGet, anziché la console. [Altre informazioni sono disponibili sul sito CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Correzioni di bug
NuGet 2.2 include varie correzioni di bug. Per un elenco completo di lavoro gli elementi corretti in 2.2, NuGet, vista la [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
