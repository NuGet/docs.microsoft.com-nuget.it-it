---
title: Note sulla versione di NuGet 2,6
description: Note sulla versione per NuGet 2.6.1 per WebMatrix, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5f6504d180879f2e9140552e0d2e07e34a85a083
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236977"
---
# <a name="nuget-26-release-notes"></a>Note sulla versione di NuGet 2,6

Note sulla versione di [NuGet 2,5](../release-notes/nuget-2.5.md)  |  [Note sulla versione di NuGet 2.6.1 per WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2,6 è stato rilasciato il 26 giugno 2013.

## <a name="notable-features-in-the-release"></a>Funzionalità rilevanti della versione

### <a name="support-for-visual-studio-2013"></a>Supporto per Visual Studio 2013

NuGet 2,6 è la prima versione che fornisce supporto per Visual Studio 2013. Analogamente a Visual Studio 2012, l'estensione Gestione pacchetti NuGet è inclusa in tutte le edizioni di Visual Studio.

Per offrire il miglior supporto possibile per Visual Studio 2013 pur continuando a supportare sia Visual Studio 2010 che Visual Studio 2012, mantenendo le dimensioni di estensione più piccole possibile, viene produttrice un'estensione separata per Visual Studio 2013 mentre l'estensione originale continua a essere destinata a Visual Studio 2010 e 2012.

A partire da NuGet 2,6, vengono pubblicate due estensioni come indicato di seguito:

1. [Gestione pacchetti NuGet](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (si applica a Visual Studio 2010 e 2012)
1. [Gestione pacchetti NuGet per Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Con questa suddivisione, il pulsante "Install NuGet" del home page [NuGet.org](https://nuget.org) consente di accedere alla pagina di [installazione di NuGet](../install-nuget-client-tools.md) , in cui è possibile trovare altre informazioni sull'installazione dei diversi client NuGet.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Supporto della trasformazione Web.config XDT

Una delle funzionalità più richieste per il client NuGet è stata supportare le trasformazioni XML più potenti usando il motore di trasformazione XDT usato nelle trasformazioni di configurazione della compilazione di Visual Studio.

Nel 2013 aprile sono stati apportati due grandi annunci sul supporto NuGet per XDT. Il primo è che la libreria XDT è stata [rilasciata come pacchetto NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) e [Open Source su CodePlex](http://xdt.codeplex.com/). Questo passaggio ha consentito l'uso gratuito del motore XDT da parte di altri software open source, incluso il client NuGet. Il secondo annuncio era il piano per supportare l'uso del motore XDT per le trasformazioni nel client NuGet. NuGet 2,6 include questa integrazione.

#### <a name="how-it-works"></a>Come funziona

Per sfruttare i vantaggi del supporto XDT di NuGet, i meccanismi hanno un aspetto simile a quello della [funzionalità di trasformazione della configurazione corrente](../create-packages/source-and-config-file-transformations.md).
I file di trasformazione vengono aggiunti alla cartella del contenuto del pacchetto. Tuttavia, mentre le trasformazioni di configurazione utilizzano un singolo file per l'installazione e la disinstallazione, le trasformazioni XDT consentono un controllo con granularità fine su entrambi i processi utilizzando i file seguenti:

- Web.config. Install. XDT
- Web.config. Uninstall. XDT

Inoltre, NuGet usa il suffisso file per determinare il motore da eseguire per le trasformazioni, quindi i pacchetti che usano il web.config esistente. le trasformazioni continueranno a funzionare. Le trasformazioni XDT possono anche essere applicate a qualsiasi file XML (non solo web.config), in modo da poterlo utilizzare per altre applicazioni nel progetto.

#### <a name="what-you-can-do-with-xdt"></a>Cosa è possibile fare con XDT

Uno dei principali punti di forza di XDT è la [sintassi semplice ma potente](/previous-versions/aspnet/dd465326(v=vs.110)) per la modifica della struttura di un DOM XML. Anziché semplicemente sovrapporre una struttura di documenti fissa su un'altra struttura, XDT fornisce controlli per la corrispondenza di elementi in diversi modi, dal nome di attributo semplice corrispondente al supporto completo di XPath. Una volta individuato un elemento o un set di elementi corrispondente, XDT offre un set completo di funzioni per la modifica degli elementi, ovvero l'aggiunta, l'aggiornamento o la rimozione di attributi, l'inserimento di un nuovo elemento in un percorso specifico o la sostituzione o la rimozione dell'intero elemento e dei relativi elementi figlio.

### <a name="machine-wide-configuration"></a>Configurazione di Machine-Wide

Uno dei principali punti di forza di NuGet è che suddivide un eseguibile o una libreria di grandi dimensioni in un set di componenti modulari che possono essere integrati e gestiti e con versioni più importanti in modo indipendente. Un effetto collaterale di questo, tuttavia, è che l'idea convenzionale di un prodotto o di una famiglia di prodotti diventa potenzialmente più frammentata.
La funzionalità di origine del pacchetto personalizzata di NuGet fornisce un modo per organizzare i pacchetti; Tuttavia, le origini dei pacchetti personalizzate non sono individuabili autonomamente.

NuGet 2,6 estende la logica per la configurazione di NuGet eseguendo una ricerca nella gerarchia di cartelle nel percorso% ProgramData%/NuGet/Config. I programmi di installazione dei prodotti possono aggiungere file di configurazione NuGet personalizzati in questa cartella per registrare un'origine pacchetto personalizzata per i propri prodotti. Inoltre, la struttura di cartelle supporta la semantica per il prodotto, la versione e persino lo SKU dell'IDE. Le impostazioni di queste directory vengono applicate nell'ordine seguente con una strategia di precedenza "Last in WINS".

1. %ProgramData%\NuGet\Config \* . config
2. %ProgramData%\NuGet\Config \{ IDE} \* . config
3. %ProgramData%\NuGet\Config \{ IDE} \{ versione} \* . config
4. %ProgramData%\NuGet\Config \{ IDE} \{ versione} \{ SKU} \* . config

In questo elenco, il segnaposto {IDE} è specifico dell'IDE in cui è in esecuzione NuGet, quindi, nel caso di Visual Studio, sarà "VisualStudio". I segnaposto {Version} e {SKU} sono forniti dall'IDE, ad esempio "11,0" e "WDExpress", "VWDExpress" e "Pro", rispettivamente. La cartella può quindi contenere molti file *. config diversi.
Pertanto, l'azienda del componente ACME può, come parte del programma di installazione del prodotto, aggiungere un'origine pacchetto personalizzata che sarà visibile solo nelle versioni Professional e Ultimate di Visual Studio 2012 creando il seguente percorso di file:

% ProgramData% \NuGet\Config\VisualStudio\11.0\Pro\acme.config

Sebbene la struttura di cartelle renda più semplice per i programmi come i programmi di installazione software l'aggiunta di origini di pacchetti a livello di computer alla configurazione di NuGet, è stata aggiornata anche la finestra di dialogo di configurazione di NuGet per consentire la registrazione delle origini dei pacchetti come specifica dell'utente, ad esempio registrata in% AppData%/NuGet/NuGet.Config) o a livello di computer.

Questa funzionalità viene utilizzata da Visual Studio 2013, in cui un file viene installato in:

% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

All'interno di questo file è configurata una nuova origine del pacchetto denominata "pacchetti .NET Framework".

![Impostazioni a livello di computer del file di configurazione NuGet](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Ricerca contestualizzazione

Poiché il numero di pacchetti serviti dalla raccolta NuGet continua ad aumentare a ritmo esponenziale, il miglioramento della ricerca rimane sempre nella parte superiore dell'elenco delle priorità di NuGet. Una delle funzionalità pianificate per NuGet è la ricerca contestuale, ovvero NuGet utilizzerà le informazioni sulla versione e lo SKU di Visual Studio in uso e il tipo di progetto che si sta creando come criterio per determinare la pertinenza dei potenziali risultati della ricerca.

A partire da NuGet 2,6, ogni volta che viene installato un pacchetto, il contesto per l'installazione viene registrato come parte dei dati dell'operazione di installazione.  Le ricerche inviano anche le stesse informazioni di contesto, che consentiranno alla raccolta NuGet di migliorare i risultati della ricerca in base alle tendenze di installazione contestuale.  Un aggiornamento futuro della raccolta NuGet consentirà di incrementare questa rilevanza sensibile al contesto.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Rilevamento delle installazioni dirette e delle dipendenze

Gli autori di pacchetti si basano sempre più sulle [statistiche dei pacchetti](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) disponibili nella raccolta NuGet.  Un punto dati mancante significativo che gli autori hanno richiesto è una differenziazione tra l'installazione diretta dei pacchetti e l'installazione delle dipendenze.  Fino ad ora, il client NuGet non ha inviato alcun contesto per l'operazione di installazione per determinare se lo sviluppatore ha installato direttamente il pacchetto o se è stato installato per soddisfare una dipendenza.
A partire da NuGet 2,6, i dati verranno ora inviati per l'operazione di installazione.  Le statistiche dei pacchetti nella raccolta NuGet esporrà i dati come operazioni di installazione separate, con suffisso "-Dependency".

* Installazione
* Install-Dependency
* Aggiornamento
* Update-Dependency
* Reinstallazione
* Reinstall-Dependency

Oltre al nome diverso dell'operazione, viene registrato anche l'ID del pacchetto dipendente per l'installazione.  Un aggiornamento futuro della raccolta NuGet esporrà i dati all'interno dei report, consentendo agli autori di pacchetti di comprendere completamente come gli sviluppatori installano i pacchetti.

## <a name="bug-fixes"></a>Correzioni di bug

NuGet 2,6 include anche diverse correzioni di bug. Per un elenco completo degli elementi di lavoro corretti in NuGet 2,6, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).