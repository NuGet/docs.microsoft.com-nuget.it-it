---
title: Note sulla versione di anteprima di NuGet 3.0 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6762b6f8-82b7-4bab-a1f0-cd25e5dc1fb4
description: "Note sulla versione per l'anteprima di NuGet 3.0 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "Anteprima di NuGet 3.0 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ae137af6f9722c454458fdcb4f20760c08d6e8bb
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-30-preview-release-notes"></a>Note sulla versione di anteprima 3.0 NuGet

[Note sulla versione RC NuGet 2.9](../release-notes/nuget-2.9-rc.md) | [note sulla versione Beta di NuGet 3.0](../release-notes/nuget-3.0-beta.md)

Anteprima di NuGet 3.0 è stata rilasciata il 12 novembre 2014 come parte della versione di Visual Studio 2015 Preview. Anteprima di NuGet 3.0 è stato rilasciato. Si tratta di una grande versione per noi (sebbene un'anteprima), e siamo entusiasti di iniziare a ottenere commenti e suggerimenti su tali modifiche.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Questa versione di anteprima di NuGet 3.0 è incluso in Visual Studio 2015 Preview. Stiamo lavorando per ottenere presto anteprima Elimina per Visual Studio 2012 e Visual Studio 2013. È stato annunciato in precedenza l'intenzione di [interrompere gli aggiornamenti per Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), e si prendere tale decisione difficile.

## <a name="brand-new-ui"></a>Nuova interfaccia utente

La prima cosa da notare sui NuGet 3.0 anteprima è l'interfaccia utente di nuovo. Non è più di una finestra di dialogo modale; è ora una finestra del documento completa Visual Studio. Ciò consente di aprire l'interfaccia utente per più progetti (e/o la soluzione) in una sola volta, estrarre la finestra in un altro monitor, ancorarla, tuttavia, potrebbe ad esempio, e così via.

![Nuova UI NuGet](./media/NuGet-3.0-Preview/new-ui.png)

Oltre alle differenze di usabilità a causa la chiusura di finestra di dialogo modale, sono disponibili anche molte delle nuove funzionalità nella nuova interfaccia utente.

### <a name="version-selection"></a>Selezione della versione

Probabilmente più richiesto funzionalità dell'interfaccia utente per consentire la selezione di versione per l'installazione del pacchetto e l'aggiornamento è ora disponibile.

![Selezione della versione del pacchetto](./media/NuGet-3.0-Preview/version-selection.png)

Se si desidera installare o aggiornare un pacchetto, l'elenco a discesa versione consente di visualizzare tutte le versioni disponibili per il pacchetto, con alcune versioni rilevanti alzate di livello nella parte superiore dell'elenco per facilitare la selezione. Non è necessario utilizzare la Console di PowerShell per ottenere versioni specifiche che non sono più recenti.

### <a name="combined-installedonlineupdates-workflows"></a>Combinare i flussi di lavoro/Online/aggiornamenti installati

L'interfaccia utente di precedente era 3 schede per installato, Online e gli aggiornamenti. I pacchetti elencati sono specifici per i flussi di lavoro e sono specifiche per i flussi di lavoro nonché le azioni disponibili. Mentre che sembrava logico, abbiamo saputo che molti di voi sarebbe spesso ottenere attivati da questa separazione.

È ora disponibile un'esperienza, in cui è possibile installare, aggiornare o disinstallare un pacchetto indipendentemente dalla modalità con cui è stato ottenuto il pacchetto selezionato. Per agevolare i flussi di lavoro specifici, è ora disponibile un elenco a discesa di filtro che consente di filtrare i pacchetti visibili, ma quindi le azioni disponibili per il pacchetto siano coerenti.

![Disinstallazione di un pacchetto](./media/NuGet-3.0-Preview/uninstall-package.png)

Tramite il filtro "Installed", quindi è possibile visualizzare facilmente i pacchetti installati, quelle che invece presentano gli aggiornamenti disponibili, e quindi è possibile disinstallare o aggiornare il pacchetto, modificare la selezione della versione per vedere modificare l'azione disponibile.

![Un pacchetto di aggiornamento](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Consolidamento di versione

È comune disporre dello stesso pacchetto installato in più progetti all'interno della soluzione. In alcuni casi le versioni installate in ogni progetto possono passare ed è necessario consolidare le versioni in uso. Anteprima di NuGet 3.0 introduce una nuova funzionalità per solo questo scenario.

La finestra di gestione di pacchetti a livello di soluzione sono accessibili facendo clic sulla soluzione e scegliere Gestisci pacchetti NuGet per la soluzione. Da qui, se si seleziona un pacchetto che viene installato in più progetti, ma con diverse versioni in uso, diventa disponibile una nuova azione "Consolida". Nella cattura di schermata seguente, `Newtonsoft.Json` in cui è stato installato il `SamplesClassLibrary` con versione `6.0.4` e installata in `SamplesConsoleApp` con versione `5.0.4`.

![Consolidare le versioni](./media/NuGet-3.0-Preview/consolidate.png)

Di seguito è riportato il flusso di lavoro per il consolidamento in una singola versione.

1. Selezionare il `Newtonsoft.Json` pacchetto nell'elenco
1. Scegliere `Consolidate` dal `Action` elenco a discesa
1. Utilizzare il `Version` elenco a discesa per selezionare la versione per essere consolidati nel
1. Selezionare le caselle per i progetti che debbano essere consolidate in tale versione (si noti che i progetti già nella versione selezionata verranno visualizzato in grigio)
1. Fare clic sul `Consolidate` pulsante per eseguire il consolidamento

### <a name="operation-previews"></a>Anteprime di operazione

Indipendentemente dall'operazione che si sta eseguendo - installazione/aggiornamento/disinstallazione, la nuova interfaccia utente offre ora un modo per visualizzare in anteprima le modifiche apportate al progetto. Questa versione di anteprima verrà visualizzato alcun nuovo pacchetto che verrà installato, i pacchetti che verranno aggiornati e pacchetti che verranno disinstallati, insieme ai pacchetti che verranno invariati durante l'operazione.

Nell'esempio seguente, si noterà che l'installazione di Microsoft. Aspnet implica alcune modifiche al progetto.

![Visualizzare in anteprima l'installazione di SignalR](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Opzioni di installazione

Utilizzando la Console di PowerShell, era controllo su un paio di opzioni di installazione rilevanti. A questo punto, è stata introdotta tali funzionalità in anche l'interfaccia utente. È ora possibile controllare il comportamento di risoluzione delle dipendenze per la modalità di selezione delle versioni delle dipendenze.

![Comportamento di dipendenza](./media/NuGet-3.0-Preview/dependency-behavior.png)

È inoltre possibile specificare l'azione da intraprendere quando i file dai pacchetti di contenuto in conflitto con i file già presenti nel progetto.

![Azione di conflitti di file](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Scorrimento infinita

È utilizzato per ottenere abbastanza di commenti e suggerimenti sull'interfaccia utente che dispongono di entrambe le barre di scorrimento e paging paradigmi quando l'elenco di pacchetti. È piuttosto comune a scorrere fino alla fine di un breve elenco, fare clic sul numero di pagina successivo e quindi scorrere nuovamente. Con la nuova interfaccia utente sono state implementate infinito lo scorrimento nell'elenco dei pacchetti in modo che è necessario scorrere - paging non sono più presenti.

![Scorrimento infinita](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Verificare il lavoro, renderlo veloce, renderlo Pretty

Siamo entusiasti ottenere questa nuova interfaccia utente per provare. Durante questa versione di anteprima, siamo stati seguendo il buon vecchio credenza "renderlo di lavoro, renderlo più rapido, piacevole." In questa versione di anteprima è stata eseguita la maggior parte di tale obiettivo prima - funziona. Sappiamo che non è ancora molto rapido e sappiamo che non è abbastanza piuttosto ancora. Trust che si lavorerà su tali obiettivi tra il momento e la versione RC. Nel frattempo, Saremmo lieti di ricevere commenti e suggerimenti sul *usabilità* dell'interfaccia utente nuova - i flussi di lavoro, le operazioni e come si *abbia* come utilizzare la nuova interfaccia utente.

Esistono un paio di funzioni che è stata rimossa rispetto all'interfaccia utente precedente. Uno di questi era intenzionale e altro semplicemente non essere eseguito nel tempo.

#### <a name="searching-all-package-sources"></a>La ricerca dell'origine del pacchetto "Tutto"

L'interfaccia utente precedente consentiva di eseguire una ricerca del pacchetto in tutte le origini del pacchetto. È stata rimossa la funzionalità dell'interfaccia utente e abbiamo non sarà possibile inserirlo nuovamente. Questa caratteristica è utilizzata per eseguire operazioni di ricerca su tutte le origini del pacchetto, combinano insieme i risultati e tenta di ordinare i risultati in base alla selezione di ordinamento.

È stato rilevato che è molto difficile fondere insieme rilevanza di ricerca. È possibile immaginare eseguendo una ricerca da Google e Bing e svolte i risultati? Inoltre, questa funzionalità è stata lenta, facili da *accidentalmente* uso e si ritiene raramente era effettivamente utile. A causa di problemi di funzionalità introdotta, abbiamo ricevuto un numero di report di bug su di esso potrebbe non sono stati corretti.

#### <a name="update-all"></a>Aggiornare tutte

Per è disponibile il pulsante "Aggiorna tutte" nell'interfaccia utente precedente che non è presente nell'interfaccia utente nuova ancora utilizzato. Si verrà ripristinare questa funzionalità per la versione RC.

## <a name="new-clientserver-api"></a>Nuovo Client/Server API

Oltre a tutte le nuove funzionalità nella nuova interfaccia utente di gestione di pacchetto, è stato inoltre lavorato alcuni dettagli di implementazione per il protocollo client/server NuGet. Il lavoro svolto consiste nel creare "v3 API" per NuGet, che viene progettato attorno a disponibilità elevata per gli scenari critici, ad esempio ripristino del pacchetto e l'installazione dei pacchetti. La nuova API è basata su REST e Hypermedia e sono state selezionate [JSON LD](http://json-ld.org) come il formato della risorsa.

Nei bit di NuGet 3.0 Preview, si noterà una nuova origine pacchetto chiamata "preview.nuget.org" nell'elenco a discesa origine pacchetto. Se si seleziona l'origine del pacchetto, la nuova API utilizzeremo invece connettersi nuget.org. Sono stati apportati disponibile nell'interfaccia utente di anteprima di origine mentre si continua a test, modificare e migliorare la nuova API. In NuGet 3.0 RC, la nuova origine pacchetto basato su v3 API sostituirà l'origine del pacchetto basato su v2 "nuget.org".

Nonostante l'investimento che ci stiamo messa in API v3, sono stati apportati tutte queste nuove funzionalità funziona anche con il protocollo di v2 API esistente, ovvero che funzionano con le origini esistenti pacchetto diverso da nuget.org anche.

## <a name="new-features-coming"></a>Nuove funzionalità

Tra l'ora e la versione 3.0 RTM, Microsoft sta lavorando alcune fondamentali nuove NuGet funzionalità, oltre a ciò che verrà visualizzato nell'interfaccia utente. Ecco un breve elenco di aree di investimento principali:

1. Si sta collaborando con Visual Studio e team di MSBuild per ottenere [NuGet più profondo nella piattaforma](http://blog.nuget.org/20141014/in-the-platform.html).
1. Stiamo lavorando per annullare le convenzioni di pacchetto in fase di installazione e vengono invece applicate le convenzioni in fase di creazione di pacchetti introducendo un nuovo "autorevole" [manifesto di pacchetto](http://blog.nuget.org/20141023/package-manifests.html).
1. Stiamo lavorando per effettuare il refactoring NuGet codebase riutilizzabili per i componenti client e server in domini diversi, oltre a gestione dei pacchetti in Visual Studio.
1. Stiamo ricercando la causa la nozione di "dipendenze private" in un pacchetto può indicare che non ha dipendenze da altri pacchetti per solo i dettagli di implementazione e le dipendenze non devono essere resi visibili come dipendenze di primo livello.

## <a name="stay-tuned"></a>In futuro

Tenere d'occhio [blog](http://blog.nuget.org) per più lo stato di avanzamento e annunci per NuGet 3.0!