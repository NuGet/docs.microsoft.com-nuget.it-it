---
title: Note sulla versione di NuGet 3.0 Preview
description: Note sulla versione per NuGet 3.0 Preview inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9389639476172d05556b95d589e429ddfe0e3026
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546465"
---
# <a name="nuget-30-preview-release-notes"></a>Note sulla versione di NuGet 3.0 Preview

[Note sulla versione per NuGet 2.9 RC](../release-notes/nuget-2.9-rc.md) | [note sulla versione di NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md)

Anteprima di NuGet 3.0 è stato rilasciato il 12 novembre 2014 come parte della versione di Visual Studio 2015 Preview. Sono stati rilasciati NuGet 3.0 Preview. Si tratta di un rilascio importante per noi (benché un'anteprima), e siamo lieti di iniziare a ottenere commenti e suggerimenti su tali modifiche.

## <a name="visual-studio-2012"></a>Visual Studio 2012+

Questa versione di anteprima di NuGet 3.0 è incluso in Visual Studio 2015 Preview. Stiamo lavorando per sfuggire cadute di anteprima per Visual Studio 2012 e Visual Studio 2013 molto presto. È stato annunciato in precedenza il nostro obiettivo per [interrompere gli aggiornamenti per Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), e si è presa questa decisione difficile.

## <a name="brand-new-ui"></a>Nuova interfaccia utente

La prima cosa che notare su NuGet 3.0 Preview è l'interfaccia utente completamente nuova. Non è più una finestra di dialogo modale; è ora una finestra del documento completa Visual Studio. In questo modo è possibile aprire l'interfaccia utente per più progetti (e/o la soluzione) in una sola volta, trascinare la finestra in un altro monitor, ancorarla ma sarebbe mi piace e così via.

![Nuova UI NuGet](./media/NuGet-3.0-Preview/new-ui.png)

Oltre alle differenze di usabilità a causa dell'abbandono la finestra di dialogo modale, sono anche disponibili numerose nuove funzionalità nell'interfaccia utente di nuovo.

### <a name="version-selection"></a>Selezione della versione

Forse più richiesto funzionalità dell'interfaccia utente per consentire la selezione versione per l'installazione del pacchetto e di aggiornamento, questa funzionalità è ora disponibile.

![Selezione della versione del pacchetto](./media/NuGet-3.0-Preview/version-selection.png)

Se si intende installare o aggiornare un pacchetto, l'elenco a discesa versione consente di visualizzare tutte le versioni disponibili per il pacchetto, con alcune versioni rilevanti promossi all'inizio dell'elenco per facilitare la selezione. È non è più necessario usare la Console di PowerShell per ottenere versioni specifiche che non sono la versione più recente.

### <a name="combined-installedonlineupdates-workflows"></a>Combinare i flussi di lavoro/Online/aggiornamenti installati

L'interfaccia utente precedente era 3 schede per installato, Online e gli aggiornamenti. I pacchetti elencati erano specifici per i flussi di lavoro e le azioni disponibili sono stati specifiche di anche i flussi di lavoro. Mentre che sembrava logico, visto che molti di voi sarebbe spesso ottenere perché entrano in gioco da questa separazione.

È ora disponibile un'esperienza complessiva, in cui è possibile installare, aggiornare o disinstallare un pacchetto indipendentemente dal modo in cui è stato ottenuto il pacchetto selezionato. Per semplificare i flussi di lavoro specifici, è ora disponibile un elenco a discesa filtro che consente di filtrare i pacchetti visibili, ma quindi le azioni disponibili per il pacchetto siano coerenti.

![Disinstalla un pacchetto](./media/NuGet-3.0-Preview/uninstall-package.png)

Tramite il filtro "Installato", quindi è possibile visualizzare facilmente i pacchetti installati, quelle che sono disponibili aggiornamenti, e quindi è possibile disinstallare o aggiornare il pacchetto modificando la selezione versione per visualizzare modificare l'azione disponibile.

![Aggiornare un pacchetto](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Consolidamento di versione

Accade spesso di avere lo stesso pacchetto installato in più progetti all'interno della soluzione. In alcuni casi le versioni installate in ogni progetto possono deviano distanti tra loro ed è necessario consolidare le versioni in uso. Versione di anteprima di NuGet 3.0 introduce una nuova funzionalità per affrontare queste situazioni.

Finestra di gestione di pacchetti a livello di soluzione sono accessibili facendo clic sulla soluzione e scegliendo Gestisci pacchetti NuGet per la soluzione. Da qui, se si seleziona un pacchetto viene installato in più progetti, ma con diverse versioni in uso, una nuova azione di "Consolidamento" diventa disponibile. Nella schermata seguente, `Newtonsoft.Json` è stato installato nel `SamplesClassLibrary` con la versione `6.0.4` e installate nel `SamplesConsoleApp` con la versione `5.0.4`.

![Consolidare le versioni](./media/NuGet-3.0-Preview/consolidate.png)

Ecco il flusso di lavoro per il consolidamento su una singola versione.

1. Selezionare il `Newtonsoft.Json` pacchetto nell'elenco
1. Scegli `Consolidate` dal `Action` elenco a discesa
1. Usare il `Version` elenco a discesa per selezionare la versione per essere consolidati nel
1. Selezionare le caselle per i progetti che devono essere consolidati nel tale versione (si noti che i progetti già nella versione selezionata è disabilitati)
1. Fare clic su di `Consolidate` pulsante per eseguire il consolidamento

### <a name="operation-previews"></a>Anteprime di operazione

Indipendentemente dal fatto l'operazione che si sta eseguendo, installare/aggiornare/disinstallare: la nuova interfaccia utente ora offre un modo per visualizzare in anteprima le modifiche che verranno apportate al progetto. Questa versione di anteprima verranno visualizzati i nuovi pacchetti che verranno installati, i pacchetti verranno aggiornati e i pacchetti che verranno disinstallati, insieme ai pacchetti che verranno invariati durante l'operazione.

Nell'esempio seguente, noteremo che installazione ASPNET implica alcune modifiche al progetto.

![Anteprima di installazione di SignalR](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Opzioni di installazione

Usare la Console di PowerShell, sono state controllare un paio di opzioni di installazione rilevanti. È stata ora introdotta tali funzionalità in anche l'interfaccia utente. È ora possibile controllare il comportamento di risoluzione delle dipendenze per la modalità di selezione delle versioni delle dipendenze.

![Comportamento di dipendenza](./media/NuGet-3.0-Preview/dependency-behavior.png)

È anche possibile specificare l'azione da intraprendere quando i file di contenuto dai pacchetti sono in conflitto con i file già presenti nel progetto.

![Azione di conflitti di file](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Lo scorrimento infinito

Abbiamo utilizzato per ottenere abbastanza di commenti e suggerimenti nella nostra interfaccia utente con entrambe le barre di scorrimento e paradigmi di paging quando si elencano i pacchetti. Era piuttosto comune a dover scorrere fino alla fine dell'elenco breve, fare clic sul numero di pagina successivo e quindi scorrere verso il nuovo. Con la nuova interfaccia utente, abbiamo implementato lo scorrimento infinito nell'elenco di pacchetti in modo che è sufficiente scorrere, il paging non è più.

![Lo scorrimento infinito](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Assicurare la lavoro è necessario renderlo veloce, consentono di tipo Pretty

Siamo lieti di ottenere questa nuova UI out per poter provare. Durante questa attività cardine di anteprima, siamo stati seguendo il buon credenza "rendono di lavoro, rendono più veloce, piacevole." In questa versione di anteprima è stata eseguita la maggior parte di tale obiettivo prima, funziona. Sappiamo che non è ancora abbastanza veloce e sappiamo che non è abbastanza piuttosto ancora. Relazione di trust che si starà lavorando su tali obiettivi da ora e la versione RC. Nel frattempo, saremo lieti di ricevere commenti e suggerimenti sul *usabilità* della nuova interfaccia utente, i flussi di lavoro, operazioni e in che modo viene *ritiene* per usare la nuova interfaccia utente.

Esistono un paio di funzioni che è stata rimossa rispetto all'interfaccia utente precedente. Uno di questi era intenzionale e altro semplicemente non facevo nel tempo.

#### <a name="searching-all-package-sources"></a>La ricerca di "Tutti" origini dei pacchetti

L'interfaccia utente precedente consente di eseguire una ricerca di pacchetti in tutte le origini pacchetto. Tale funzionalità è stata rimossa nell'interfaccia utente e Microsoft non sarà possibile inserirlo nuovamente. Questa funzionalità consente di eseguire operazioni di ricerca su tutte le origini di pacchetti, fondere insieme i risultati e tenta di ordinare i risultati in base alla selezione di ordinamento.

È stato rilevato che è molto difficile eseguire fondere insieme pertinenza delle ricerche. È possibile immaginare eseguendo una ricerca su Bing e Google e svolte i risultati? Inoltre, questa funzionalità è stata lenta, di facile *accidentalmente* uso e si ritiene che raramente era effettivamente utile. A causa di problemi la funzionalità introdotta, abbiamo ricevuto numerosi bug i report correlati che è stato mai sono stati risolti.

#### <a name="update-all"></a>Aggiorna tutto

Abbiamo utilizzato per disporre di un pulsante "Aggiorna tutto" nell'interfaccia utente precedente che non è presente nella nuova UI ancora. Si verrà riprendere questa funzionalità per la versione RC.

## <a name="new-clientserver-api"></a>Nuovo Client/Server API

Oltre a tutte le nuove funzionalità nel nuovo pacchetto interfaccia di gestione, è anche concentrato su alcuni dettagli di implementazione per il protocollo client/server di NuGet. Il lavoro svolto consiste nel creare "v3 API" per NuGet, che viene progettato attorno a disponibilità elevata per scenari critici, ad esempio il ripristino dei pacchetti e l'installazione dei pacchetti. La nuova API è basata su REST e abbiamo selezionato Ipermedia e abbiamo [JSON-LD](http://json-ld.org) come il formato della risorsa.

I bit di anteprima di NuGet 3.0, visualizza una nuova origine pacchetto denominata "preview.nuget.org" nell'elenco a discesa origine pacchetto. Se si seleziona tale origine del pacchetto, si userà la nuova API invece di connettersi in nuget.org. È ora disponibile l'anteprima di origine nell'interfaccia utente mentre continuiamo a test, modificare e migliorare la nuova API. In NuGet 3.0 RC, la nuova origine pacchetto v3 basati su API sostituirà l'origine del pacchetto basato su v2 "nuget.org".

Nonostante l'investimento che inseriamo nell'API v3, sono state apportate tutte queste nuove funzionalità funzionano anche con il protocollo di v2 API esistente, che significa che siano compatibili con origini dei pacchetti esistente diverso da nuget.org anche.

## <a name="new-features-coming"></a>Nuove funzionalità

Da ora e 3.0 RTM, Microsoft sta lavorando inoltre alcune fondamentali funzionalità NuGet nuove, oltre a ciò che viene visualizzato nell'interfaccia utente. Ecco un breve elenco di aree di investimento principali:

1. Stiamo collaborando con Visual Studio e team di MSBuild per ottenere [NuGet più profondo nella piattaforma](http://blog.nuget.org/20141014/in-the-platform.html).
1. Stiamo lavorando per abbandonare convenzioni dei pacchetti in fase di installazione e vengono invece applicate tali convenzioni in fase di creazione di pacchetti con l'introduzione di un nuovo "attendibile" [manifesto del pacchetto](http://blog.nuget.org/20141023/package-manifests.html).
1. Ci stiamo impegnando per effettuare il refactoring di NuGet codebase per rendere i componenti client e server riutilizzabili in domini diversi oltre a Gestione pacchetti in Visual Studio.
1. Stiamo analizzando la nozione di "le dipendenze private" in cui un pacchetto può indicare che non presenta dipendenze da altri pacchetti per solo i dettagli di implementazione, e tali dipendenze non devono essere resi visibili come dipendenze di livello superiore.

## <a name="stay-tuned"></a>Continua a seguirci

Teniamo d'occhio [nostro blog](http://blog.nuget.org) per più lo stato di avanzamento e annunci per NuGet 3.0!