---
title: Note sulla versione di NuGet 2.6
description: Note sulla versione per NuGet 2.6, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e controller di dominio.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6b25b9df062afc88466ad107e718f632878debfc
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901421"
---
# <a name="nuget-26-release-notes"></a>Note sulla versione di NuGet 2.6

[Note sulla versione di NuGet 2.5](../release-notes/nuget-2.5.md)  |  [Note sulla versione di NuGet 2.6.1 per WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 è stato rilasciato il 26 giugno 2013.

## <a name="notable-features-in-the-release"></a>Funzionalità importanti nella versione

### <a name="support-for-visual-studio-2013"></a>Supporto per Visual Studio 2013

NuGet 2.6 è la prima versione che fornisce supporto per Visual Studio 2013. Come per Visual Studio 2012, l'estensione Gestione pacchetti NuGet è inclusa in ogni edizione di Visual Studio.

Per offrire il miglior supporto possibile per Visual Studio 2013, pur supportando sia Visual Studio 2010 che Visual Studio 2012 e mantenendo le dimensioni dell'estensione il più piccole possibile, viene prodotto un'estensione separata per Visual Studio 2013 mentre l'estensione originale continua a essere di destinazione sia Visual Studio 2010 che 2012.

A partire da NuGet 2.6, verranno pubblicate due estensioni come indicato di seguito:

1. [NuGet Gestione pacchetti](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (si applica Visual Studio 2010 e 2012)
1. [NuGet Gestione pacchetti per Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Con questa suddivisione, il pulsante "Installa NuGet" del nuget.org [home page](https://nuget.org) consente di accedere alla pagina di installazione di [NuGet,](../install-nuget-client-tools.md) in cui sono disponibili altre informazioni sull'installazione dei diversi client NuGet.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Supporto della trasformazione Web.config XDT

Una delle funzionalità più richieste per il client NuGet è stata il supporto di trasformazioni XML più potenti tramite il motore di trasformazione XDT usato nelle trasformazioni di configurazione Visual Studio compilazione.

Nel mese di aprile 2013 sono stati resi disponibili due annunci di grande grande livello relativi al supporto di NuGet per XDT. Il primo è che la libreria XDT stessa viene rilasciata come pacchetto [NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) e [open source in CodePlex.](http://xdt.codeplex.com/) Questo passaggio ha consentito al motore XDT di essere usato liberamente da altro software open source, incluso il client NuGet. Il secondo annuncio è il piano per supportare l'uso del motore XDT per le trasformazioni nel client NuGet. NuGet 2.6 include questa integrazione.

#### <a name="how-it-works"></a>Funzionamento

Per sfruttare il supporto XDT di NuGet, i meccanismi sono simili a quelli della funzionalità di trasformazione [della configurazione corrente.](../create-packages/source-and-config-file-transformations.md)
I file di trasformazione vengono aggiunti alla cartella del contenuto del pacchetto. Tuttavia, mentre le trasformazioni di configurazione usano un singolo file per l'installazione e la disinstallazione, le trasformazioni XDT consentono un controllo granulare su entrambi questi processi usando i file seguenti:

- Web.config.install.xdt
- Web.config.uninstall.xdt

NuGet usa inoltre il suffisso file per determinare quale motore eseguire per le trasformazioni, pertanto i pacchetti che usano il web.config.transforms esistente continueranno a funzionare. Le trasformazioni XDT possono essere applicate anche a qualsiasi file XML (non solo web.config), quindi è possibile sfruttare questo valore per altre applicazioni nel progetto.

#### <a name="what-you-can-do-with-xdt"></a>Cosa è possibile fare con XDT

Uno dei principali punti di forza di XDT è la [sintassi](/previous-versions/aspnet/dd465326(v=vs.110)) semplice ma potente per modificare la struttura di un DOM XML. Anziché sovrapporre semplicemente una struttura di documento fissa a un'altra struttura, XDT fornisce controlli per la corrispondenza degli elementi in diversi modi, dalla semplice corrispondenza dei nomi di attributo al supporto completo di XPath. Dopo aver trovato un elemento o un set di elementi corrispondente, XDT offre un set di funzioni avanzate per la modifica degli elementi, indipendentemente dal fatto che ciò significhi l'aggiunta, l'aggiornamento o la rimozione di attributi, l'inserimento di un nuovo elemento in una posizione specifica o la sostituzione o la rimozione dell'intero elemento e dei relativi elementi figlio.

### <a name="machine-wide-configuration"></a>Machine-Wide configurazione

Uno dei principali punti di forza di NuGet è che suddivide un eseguibile o una libreria altrimenti di grandi dimensioni in un set di componenti modulari che possono essere integrati e, soprattutto, gestiti e con controllo delle versioni in modo indipendente. Un effetto collaterale di questo, tuttavia, è che l'idea convenzionale di un prodotto o di una famiglia di prodotti diventa potenzialmente più frammentata.
La funzionalità di origine del pacchetto personalizzata di NuGet consente di organizzare i pacchetti. Tuttavia, le origini dei pacchetti personalizzati non sono individuabili di per sé.

NuGet 2.6 estende la logica per la configurazione di NuGet eseguendo una ricerca nella gerarchia di cartelle nel percorso %ProgramData%/NuGet/Config. I programmi di installazione del prodotto possono aggiungere file di configurazione NuGet personalizzati in questa cartella per registrare un'origine pacchetto personalizzata per i prodotti. Inoltre, la struttura di cartelle supporta la semantica per prodotto, versione e anche SKU dell'IDE. Le impostazioni di queste directory vengono applicate nell'ordine seguente con una strategia di precedenza "last in wins".

1. %ProgramData%\NuGet\Config.config \*
2. %ProgramData%\NuGet\Config \{ IDE} \* .config
3. %ProgramData%\NuGet\Config \{ IDE} \{ Versione} \* .config
4. %ProgramData%\NuGet\Config \{ IDE} \{ Versione} \{ SKU} \* .config

In questo elenco il segnaposto {IDE} è specifico dell'IDE in cui è in esecuzione NuGet, quindi nel caso di Visual Studio, sarà "VisualStudio". I segnaposto {Version} e {SKU} vengono forniti dall'IDE (ad esempio, "11.0" e "WDExpress", "VWDExpress" e "Pro", rispettivamente). La cartella può quindi contenere molti file *.config diversi.
Pertanto, la società di componenti ACME può, come parte del programma di installazione del prodotto, aggiungere un'origine pacchetto personalizzata che sarà visibile solo nelle versioni Professional e Ultimate di Visual Studio 2012 creando il percorso file seguente:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Anche se la struttura di cartelle rende più semplice per programmi come i programmi di installazione software aggiungere origini di pacchetti a livello di computer alla configurazione di NuGet, la finestra di dialogo di configurazione di NuGet è stata aggiornata anche per consentire la registrazione delle origini dei pacchetti come specifico dell'utente (ad esempio registrato in %AppData%/NuGet/NuGet.Config) o a livello di computer.

Questa funzionalità viene utilizzata da Visual Studio 2013, in cui viene installato un file in:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

All'interno di questo file viene configurata una nuova origine .NET Framework pacchetti.

![Impostazioni a livello di computer del file di configurazione NuGet](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contestualizzazione della ricerca

Poiché il numero di pacchetti serviti dalla raccolta NuGet continua a crescere a un ritmo esponenziale, il miglioramento della ricerca rimane sempre all'inizio dell'elenco di priorità NuGet. Una delle funzionalità pianificate per NuGet è la ricerca contestuale, ovvero NuGet userà informazioni sulla versione e sullo SKU di Visual Studio in uso e sul tipo di progetto che si sta creando come criteri per determinare la pertinenza dei potenziali risultati della ricerca.

A partire da NuGet 2.6, ogni volta che viene installato un pacchetto, il contesto per l'installazione viene registrato come parte dei dati dell'operazione di installazione.  Le ricerche inviano anche le stesse informazioni di contesto, che consentiranno a NuGet Gallery di aumentare i risultati della ricerca in base alle tendenze di installazione contestuale.  Un aggiornamento futuro di NuGet Gallery consentirà l'aumento della pertinenza sensibile al contesto.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Rilevamento delle installazioni dirette e delle installazioni delle dipendenze

Gli autori di pacchetti si basano sempre di più sulle statistiche [dei](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) pacchetti disponibili in NuGet Gallery.  Un punto dati significativo mancante richiesto dagli autori è una differenziazione tra le installazioni di pacchetti diretti e le installazioni delle dipendenze.  Fino ad ora, il client NuGet non ha inviato alcun contesto per l'operazione di installazione per indicare se lo sviluppatore ha installato direttamente il pacchetto o se è stato installato per soddisfare una dipendenza.
A partire da NuGet 2.6, i dati verranno ora inviati per l'operazione di installazione.  Le statistiche dei pacchetti nella raccolta NuGet esporranno i dati come operazioni di installazione separate, con un suffisso "-Dependency".

* Installazione
* Install-Dependency
* Update
* Update-Dependency
* Reinstallazione
* Reinstall-Dependency

Oltre al nome dell'operazione diverso, per l'installazione viene registrato anche l'ID pacchetto dipendente.  Un aggiornamento futuro di NuGet Gallery esporrà i dati all'interno dei report, consentendo agli autori di pacchetti di comprendere appieno il modo in cui gli sviluppatori installano i pacchetti.

## <a name="bug-fixes"></a>Correzioni di bug

NuGet 2.6 include anche diverse correzioni di bug. Per un elenco completo degli elementi di lavoro risolti in NuGet 2.6, vedere l'argomento [Relativo a NuGet Issue Tracker per questa versione.](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)