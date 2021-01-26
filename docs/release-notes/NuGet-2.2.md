---
title: Note sulla versione di NuGet 2,2
description: Note sulla versione per NuGet 2,2, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780439"
---
# <a name="nuget-22-release-notes"></a>Note sulla versione di NuGet 2,2

Note sulla versione di [NuGet 2,1](../release-notes/nuget-2.1.md)  |  [Note sulla versione di NuGet 2.2.1](../release-notes/nuget-2.2.1.md)

NuGet 2,2 è stato rilasciato il 12 dicembre 2012.

## <a name="visual-studio-quick-launch"></a>Avvio veloce di Visual Studio
Una delle nuove funzionalità aggiunte in Visual Studio 2012 è stata la finestra di [dialogo avvio veloce](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). NuGet 2,2 estende questa finestra di dialogo, consentendo di inizializzare la finestra di dialogo di gestione pacchetti con i termini di ricerca immessi nell'avvio veloce. Ad esempio, l'immissione di "jQuery" in avvio veloce include ora un'opzione nei risultati per la ricerca dei pacchetti NuGet corrispondenti a "jQuery".

![Avvio veloce di NuGet in Visual Studio](./media/quick-launch.png)

Se si seleziona questa opzione, verrà avviata l'esperienza di ricerca standard di gestione pacchetti NuGet per il termine "jQuery".

![Finestra di dialogo Gestione pacchetti NuGet pre-popolata](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Specificare l'intera cartella per il contenuto del pacchetto
NuGet 2,2 consente ora di specificare un'intera cartella nell' `<file>` elemento del `.nuspec` file per includere tutto il contenuto della cartella. Ad esempio, il codice seguente comporterà l'aggiunta di tutti gli script nella cartella Scripts alla cartella contents\scripts quando il pacchetto viene installato in un progetto.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Aggiornamento 6/24/16: le cartelle vuote nella cartella "Content" vengono ignorate durante l'installazione del pacchetto.**

## <a name="known-issues"></a>Problemi noti

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>L'installazione del pacchetto non riesce per i progetti F # quando si usa la console di gestione pacchetti
Quando si tenta di installare un pacchetto NuGet in un progetto F # usando la console di gestione pacchetti, viene generata un'eccezione InvalidOperationException. Stiamo collaborando attivamente con il team F # per risolvere il problema, ma nel frattempo la soluzione alternativa consiste nell'installare i pacchetti NuGet in progetti F # tramite la finestra di dialogo Gestione pacchetti di NuGet invece della console. [Ulteriori informazioni sono disponibili in CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Correzioni di bug
NuGet 2,2 include numerose correzioni di bug. Per un elenco completo degli elementi di lavoro corretti in NuGet 2,2, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
