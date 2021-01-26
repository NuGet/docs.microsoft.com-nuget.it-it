---
title: Note sulla versione di NuGet 3,0 Preview
description: Note sulla versione per NuGet 3,0 Preview, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ecaed21c5e689a488e033404f8042cd1f17eed0d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780325"
---
# <a name="nuget-30-preview-release-notes"></a>Note sulla versione di NuGet 3,0 Preview

Note sulla versione di [NuGet 2,9 RC](../release-notes/nuget-2.9-rc.md)  |  [Note sulla versione di NuGet 3,0 beta](../release-notes/nuget-3.0-beta.md)

NuGet 3,0 Preview è stato rilasciato il 12 novembre 2014 come parte della versione di anteprima di Visual Studio 2015. È stata rilasciata l'anteprima di NuGet 3,0. Si tratta di una versione di grandi dimensioni (anche se un'anteprima) e siamo entusiasti di iniziare a ricevere commenti e suggerimenti sulle modifiche.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Questa versione di anteprima di NuGet 3,0 è inclusa in Visual Studio 2015 Preview. Si sta lavorando per ottenere la versione di anteprima per Visual Studio 2012 e Visual Studio 2013 molto presto. In precedenza abbiamo condiviso l'intento di [interrompere gli aggiornamenti per Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)e abbiamo deciso di prendere tale decisione.

## <a name="brand-new-ui"></a>Interfaccia utente nuovissima

La prima cosa che si nota su NuGet 3,0 Preview è la nuova interfaccia utente. Non è più una finestra di dialogo modale; Ora si tratta di una finestra completa del documento di Visual Studio. In questo modo è possibile aprire l'interfaccia utente per più progetti (e/o la soluzione) in una sola volta, rimuovere la finestra da un altro monitor, ancorarla e così via.

![Nuova interfaccia utente di NuGet](./media/NuGet-3.0-Preview/new-ui.png)

Oltre alle differenze di usabilità, a causa dell'abbandono della finestra di dialogo modale, abbiamo anche molte nuove funzionalità nella nuova interfaccia utente.

### <a name="version-selection"></a>Selezione della versione

Probabilmente la funzionalità dell'interfaccia utente più richiesta è quella di consentire la selezione della versione per l'installazione e l'aggiornamento del pacchetto, che è ora disponibile.

![Selezione della versione del pacchetto](./media/NuGet-3.0-Preview/version-selection.png)

Se si installa o si aggiorna un pacchetto, l'elenco a discesa versione consente di visualizzare tutte le versioni disponibili per il pacchetto, con alcune versioni rilevanti innalzate di livello nella parte superiore dell'elenco per facilitarne la selezione. Non è più necessario usare la console di PowerShell per ottenere versioni specifiche che non sono le più recenti.

### <a name="combined-installedonlineupdates-workflows"></a>Flussi di lavoro installati/online/aggiornati combinati

L'interfaccia utente precedente aveva 3 schede per installato, online e gli aggiornamenti. I pacchetti elencati erano specifici dei flussi di lavoro e le azioni disponibili erano specifiche anche per i flussi di lavoro. Sebbene ciò fosse logico, abbiamo sentito che molti di essi venivano spesso rilevati da questa separazione.

È ora disponibile un'esperienza combinata, in cui è possibile installare, aggiornare o disinstallare un pacchetto, indipendentemente dal modo in cui è stato selezionato il pacchetto. Per supportare i flussi di lavoro specifici, ora è disponibile un elenco a discesa filtro che consente di filtrare i pacchetti visibili, ma le azioni disponibili per il pacchetto sono coerenti.

![Disinstalla un pacchetto](./media/NuGet-3.0-Preview/uninstall-package.png)

Utilizzando il filtro "installato", è possibile visualizzare facilmente i pacchetti installati, quelli con aggiornamenti disponibili, quindi è possibile disinstallare o aggiornare il pacchetto modificando la selezione della versione per visualizzare la modifica dell'azione disponibile.

![Aggiornare un pacchetto](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Consolidamento della versione

È comune che lo stesso pacchetto sia installato in più progetti all'interno della soluzione. Talvolta le versioni installate in ogni progetto possono essere separate ed è necessario consolidare le versioni in uso. NuGet 3,0 Preview introduce una nuova funzionalità solo per questo scenario.

È possibile accedere alla finestra di gestione dei pacchetti a livello di soluzione facendo clic con il pulsante destro del mouse sulla soluzione e scegliendo Gestisci pacchetti NuGet per la soluzione. A questo punto, se si seleziona un pacchetto che viene installato in più progetti, ma con versioni diverse in uso, diventa disponibile una nuova azione "consolida". Nello screenshot seguente `Newtonsoft.Json` è stato installato nella `SamplesClassLibrary` versione con `6.0.4` e installato in `SamplesConsoleApp` con la versione `5.0.4` .

![Consolidare le versioni](./media/NuGet-3.0-Preview/consolidate.png)

Di seguito è riportato il flusso di lavoro per il consolidamento su una singola versione.

1. Selezionare il `Newtonsoft.Json` pacchetto nell'elenco
1. Scegliere `Consolidate` dall' `Action` elenco a discesa
1. Usare l' `Version` elenco a discesa per selezionare la versione da consolidare
1. Selezionare le caselle per i progetti che devono essere consolidati in tale versione (si noti che i progetti già nella versione selezionata verranno disattivati)
1. Fare clic sul `Consolidate` pulsante per eseguire il consolidamento

### <a name="operation-previews"></a>Anteprime delle operazioni

Indipendentemente dall'operazione che si sta eseguendo, ovvero installazione/aggiornamento/disinstallazione, la nuova interfaccia utente ora offre un modo per visualizzare in anteprima le modifiche che verranno apportate al progetto. In questa anteprima verranno visualizzati tutti i nuovi pacchetti che verranno installati, i pacchetti che verranno aggiornati e i pacchetti che verranno disinstallati, insieme ai pacchetti che non verranno modificati durante l'operazione.

Nell'esempio seguente si noterà che l'installazione di Microsoft. AspNet. SignalR comporta alcune modifiche al progetto.

![Anteprima installazione di SignalR](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Opzione di installazione

Utilizzando la console di PowerShell, è stato effettuato il controllo su un paio di opzioni di installazione rilevanti. Ora le funzionalità sono state introdotte nell'interfaccia utente. È ora possibile controllare il comportamento di risoluzione delle dipendenze per il modo in cui vengono selezionate le versioni delle dipendenze.

![Comportamento della dipendenza](./media/NuGet-3.0-Preview/dependency-behavior.png)

È anche possibile specificare l'azione da eseguire quando i file di contenuto dei pacchetti sono in conflitto con i file già presenti nel progetto.

![Azione conflitto file](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Scorrimento infinito

Abbiamo usato per ottenere commenti e suggerimenti sull'interfaccia utente con i paradigmi di scorrimento e di paging quando si elencano i pacchetti. Era piuttosto comune dover scorrere fino alla fine dell'elenco breve, fare clic sul numero della pagina successiva e quindi scorrere nuovamente. Con la nuova interfaccia utente, abbiamo implementato lo scorrimento infinito nell'elenco dei pacchetti, in modo che sia necessario solo scorrere, senza ulteriori paging.

![Scorrimento infinito](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Per renderlo funzionante, renderlo più veloce,

Siamo entusiasti di ottenere questa nuova interfaccia utente per provare. Durante questa attività cardine di anteprima, abbiamo seguito il buon Adagio precedente di "make it work, make it it that it that it that that it that be make it pretty." In questa versione di anteprima è stata completata la maggior parte del primo obiettivo, che funziona. Sappiamo che non è ancora molto veloce e sappiamo che non è ancora abbastanza. Consideriamo attendibile l'utilizzo di tali obiettivi tra ora e la versione RC. Nel frattempo, saremmo lieti di ricevere i tuoi commenti sull' *usabilità* della nuova interfaccia utente, ovvero i flussi di lavoro, le operazioni e il modo in cui si *ritiene* di usare la nuova interfaccia utente.

Ci sono due funzioni che sono state rimosse rispetto all'interfaccia utente precedente. Uno di questi è stato intenzionale e l'altro non ha avuto successo nel tempo.

#### <a name="searching-all-package-sources"></a>Ricerca di tutte le origini di pacchetti

L'interfaccia utente precedente consentiva di eseguire una ricerca di pacchetti in tutte le origini dei pacchetti. Questa funzionalità è stata rimossa nell'interfaccia utente e non verrà riportata. Questa funzionalità consente di eseguire operazioni di ricerca in tutte le origini dei pacchetti, di unire i risultati e di ordinare i risultati in base alla selezione di ordinamento.

È stato rilevato che la pertinenza della ricerca è molto difficile da tessere insieme. Si supponga di eseguire una ricerca su Google e Bing e di tessere i risultati insieme? Inoltre, questa funzionalità era lenta, è facile da usare *accidentalmente* e si ritiene che era raramente utile. A causa dei problemi introdotti dalla funzionalità, abbiamo ricevuto una serie di report sui bug che potrebbero non essere mai stati corretti.

#### <a name="update-all"></a>Aggiorna tutto

È stato usato un pulsante "Aggiorna tutto" nell'interfaccia utente precedente che non è ancora presente nella nuova interfaccia utente. Questa funzionalità verrà rilasciata per la versione RC.

## <a name="new-clientserver-api"></a>Nuova API client/server

Oltre a tutte le nuove funzionalità della nuova interfaccia utente di gestione pacchetti, abbiamo lavorato anche su alcuni dettagli di implementazione per il protocollo client/server di NuGet. Il lavoro svolto consiste nel creare "API V3" per NuGet, progettato per la disponibilità elevata per scenari critici come il ripristino dei pacchetti e l'installazione di pacchetti. La nuova API si basa su REST e su ipermedia ed è stato selezionato [JSON-LD](http://json-ld.org) come formato di risorsa.

Nei bit di anteprima di NuGet 3,0, viene visualizzata una nuova origine del pacchetto denominata "preview.nuget.org" nell'elenco a discesa origine pacchetto. Se si seleziona l'origine del pacchetto, si userà la nuova API invece di connettersi a nuget.org. L'origine di anteprima è stata resa disponibile nell'interfaccia utente mentre continuiamo a testare, rivedere e migliorare la nuova API. In NuGet 3,0 RC questa nuova origine del pacchetto basata sull'API V3 sostituirà l'origine del pacchetto "nuget.org" basata su V2.

Nonostante l'investimento inserito nell'API V3, tutte queste nuove funzionalità funzionano anche con il protocollo API v2 esistente, il che significa che funzionano con le origini di pacchetti esistenti diverse da nuget.org.

## <a name="new-features-coming"></a>Nuove funzionalità in arrivo

Tra ora e 3,0 RTM, stiamo lavorando anche su alcune nuove funzionalità di NuGet, oltre a quelle visualizzate nell'interfaccia utente. Di seguito è riportato un breve elenco di aree di investimento salienti:

1. Stiamo collaborando con i team di Visual Studio e MSBuild per ottenere [NuGet più approfondita sulla piattaforma](http://blog.nuget.org/20141014/in-the-platform.html).
1. Ci stiamo impegnando per abbandonare le convenzioni dei pacchetti in fase di installazione e applicare le convenzioni in fase di creazione del pacchetto introducendo un nuovo [manifesto del pacchetto](http://blog.nuget.org/20141023/package-manifests.html)"autorevole".
1. Stiamo lavorando per eseguire il refactoring della codebase NuGet per rendere i componenti client e server riutilizzabili in domini diversi oltre alla gestione dei pacchetti in Visual Studio.
1. Stiamo esaminando la nozione di "dipendenze private" in cui un pacchetto può indicare che ha dipendenze da altri pacchetti solo per i dettagli di implementazione e tali dipendenze non devono essere rivelate come dipendenze di primo livello.

## <a name="stay-tuned"></a>Rimanere sintonizzati

Per ulteriori informazioni sullo stato di avanzamento e sugli annunci per NuGet 3,0, tenere sotto controllo il [Blog](http://blog.nuget.org) .