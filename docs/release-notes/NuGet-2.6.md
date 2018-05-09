---
title: Note sulla versione 2.6 di NuGet
description: Note sulla versione per NuGet 2.6.1 per WebMatrix, inclusi i problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39ce6ac3d36464d26966b0dabb0893f09ad4afdc
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-26-release-notes"></a>Note sulla versione 2.6 di NuGet

[Note sulla versione di NuGet 2.5](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 per le note sulla versione di WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)

2.6 NuGet è stato rilasciato il 26 giugno 2013.

## <a name="notable-features-in-the-release"></a>Importanti funzionalità nella versione

### <a name="support-for-visual-studio-2013"></a>Supporto per Visual Studio 2013

2.6 NuGet è il primo rilascio che fornisce il supporto per Visual Studio 2013. E come Visual Studio 2012, l'estensione Gestione pacchetti NuGet è incluso in ogni edizione di Visual Studio.

Per garantire il miglior supporto possibile per Visual Studio 2013, mentre supporto sia Visual Studio 2010 e Visual Studio 2012 e mantenendo le dimensioni di estensione più piccole possibile, si sta producendo un'estensione diversa per Visual Studio 2013, durante il estensione originale continua a fare riferimento sia Visual Studio 2010 e 2012.

A partire da NuGet 2.6, verranno pubblicate due estensioni, come indicato di seguito:

1. [Gestione pacchetti NuGet](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (si applica a Visual Studio 2010 e 2012)
1. [Gestione pacchetti NuGet per Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Con questa suddivisione, il [nuget.org](https://nuget.org) consente di accedere al pulsante "Installa NuGet" della home page di [l'installazione di NuGet](../install-nuget-client-tools.md) pagina, in cui è possibile trovare ulteriori informazioni sull'installazione di client NuGet diversi.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Supporto per le trasformazioni di Web. config XDT

Una delle funzionalità più elevata richiesta per il client di NuGet è stato per supportare più potente trasformazioni XML tramite il motore di trasformazione XDT utilizzata nelle trasformazioni di configurazione di compilazione Visual Studio.

In aprile 2013, sono stati creati due big annunci relativi al supporto di NuGet per XDT. Il primo è che è stato in corso la stessa libreria XDT stesso [rilasciata come pacchetto NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) e [open source su CodePlex](http://xdt.codeplex.com/). Questo passaggio è abilitato il motore XDT liberamente utilizzabile da altri software open source, incluso il client NuGet. L'annuncio secondo è il piano per supportare l'utilizzo del motore di XDT per le trasformazioni del client NuGet. 2.6 NuGet include questa integrazione.

#### <a name="how-it-works"></a>Come funziona

Per sfruttare i vantaggi del supporto XDT NuGet, i meccanismi simili a quelli del [funzionalità di trasformazione configurazione corrente](../create-packages/source-and-config-file-transformations.md).
File di trasformazione vengono aggiunti alla cartella del contenuto del pacchetto. Tuttavia, mentre le trasformazioni di configurazione utilizzano un singolo file per l'installazione e la disinstallazione, trasformazioni XDT attivare un controllo accurato entrambi i processi utilizzando i seguenti file:

- Web.config.install.xdt
- Web.config.uninstall.xdt

Inoltre, NuGet utilizza il suffisso del file per stabilire quale motore di esecuzione per le trasformazioni, in modo pacchetti utilizzando il web.config.transforms esistenti continueranno a funzionare. Le trasformazioni XDT possono anche essere applicate a qualsiasi file XML (non solo Web. config), pertanto è possibile sfruttare questa per altre applicazioni nel progetto.

#### <a name="what-you-can-do-with-xdt"></a>Operazioni eseguibili con XDT

Uno dei maggiori punti di forza del XDT relativo [sintassi semplice ma potente](http://msdn.microsoft.com/library/dd465326.aspx) per la modifica della struttura di un DOM. XML Anziché semplicemente la sovrapposizione di una struttura di documenti fissi sulla struttura di un altro, XDT fornisce controlli per la corrispondenza di elementi in diversi modi, dal nome di attributo semplice corrispondente per il supporto di XPath completo. Una volta che viene trovato un elemento corrispondente o un set di elementi, XDT fornisce un'ampia gamma di funzioni per la modifica di elementi, indipendentemente dal fatto che questa aggiunta, l'aggiornamento, o la rimozione di attributi, l'inserimento di un nuovo elemento in una posizione specifica, o la sostituzione o rimozione dell'intero elemento e i relativi elementi figlio.

### <a name="machine-wide-configuration"></a>Configurazione a livello di computer

Uno dei punti di forza ottimale di NuGet è che suddivide un eseguibile in caso contrario di grandi dimensioni o della libreria in un set di componenti modulari che può essere integrato, soprattutto mantenuta attiva e con controllo delle versioni in modo indipendente. Un effetto collaterale di questa operazione, tuttavia, è che l'idea convenzionale di un prodotto o una famiglia di prodotti potenzialmente diventa più frammentato.
Funzionalità di origine pacchetto NuGet fornisce un modo per organizzare pacchetti; Tuttavia, origini pacchetto personalizzato non possono essere individuate in modo autonomo.

2.6 NuGet estende la logica per la configurazione NuGet cercando la gerarchia di cartelle nel percorso % ProgramData%/NuGet/Config. Programmi di installazione del prodotto è possibile aggiungere file di configurazione NuGet personalizzati in questa cartella per registrare un'origine pacchetto personalizzato per i loro prodotti. Inoltre, la struttura di cartelle supporta la semantica per prodotto, versione e persino SKU dell'IDE. Le impostazioni di queste directory vengono applicate nell'ordine seguente con una strategia di precedenza "last in wins".

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config

In questo elenco, il segnaposto {IDE} è specifico per l'IDE in cui è in esecuzione NuGet, pertanto nel caso di Visual Studio, sarà "Visual Studio". {Version} e il segnaposto {SKU} è fornito dall'IDE (ad esempio, "11.0" e "WDExpress", "VWDExpress" e "Pro", rispettivamente). La cartella può quindi contenere molti file config diversi.
Pertanto, la società componente ACME possibile, come parte del programma di installazione di prodotto, aggiungere un'origine pacchetto personalizzato che sarà visibile solo nelle versioni di Visual Studio 2012 Professional e Ultimate creando il seguente percorso del file:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Mentre la struttura di cartelle rende più semplice per applicazioni come programmi di installazione per aggiungere origini pacchetti a livello di computer per la configurazione NuGet, la finestra di dialogo di configurazione NuGet è stato inoltre aggiornato per consentire la registrazione delle origini pacchetto come utente specifica (ad esempio registrato in % AppData%/NuGet/NuGet.Config) o a livello di computer.

Questa funzionalità è usata da Visual Studio 2013, in cui è installato un file in:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

In questo file, una nuova origine pacchetto chiamata "Pacchetti di .NET Framework" è configurata.

![Impostazioni a livello di File di configurazione NuGet macchina](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Ricerca contextualizing

Come il numero di pacchetti fornito dal raccolta NuGet continua a crescere a un ritmo esponenziale, miglioramento della ricerca rimane sempre nella parte superiore dell'elenco di priorità di NuGet. Una delle funzionalità pianificate per NuGet è l'esigenza di ricercare, vale a dire che NuGet utilizzerà informazioni sulla SKU di Visual Studio in uso e la versione e il tipo di progetto che si sta compilando come criterio per determinare la rilevanza della ricerca di potenziali risultati.

A partire da NuGet 2.6, ogni volta che viene installato un pacchetto, il contesto per l'installazione viene registrato come parte dei dati dell'operazione di installazione.  Ricerche anche inviare le stesse informazioni di contesto, che consentono la raccolta di NuGet per migliorare i risultati della ricerca delle tendenze installazione contestuale.  Un aggiornamento futuro a raccolta NuGet abiliterà questo boosting pertinenza sensibile al contesto.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Registrazione diretta consente di installare Visual Studio. Installazioni di dipendenza

Gli autori di pacchetti si basano più sul [pacchetto statistiche](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) specificato nella raccolta NuGet.  Uno dei punti dati di mancanti significativi che hanno richiesto autori è una differenza tra Installa pacchetto diretta e le installazioni di dipendenza.  Fino ad ora, il client NuGet non ha alcun contesto per l'operazione di installazione per lo sviluppatore se installati direttamente il pacchetto o se è stato installato per soddisfare una dipendenza.
A partire da NuGet 2.6, verranno ora inviati dati per l'operazione di installazione.  Le statistiche di pacchetto per la raccolta NuGet dovrà esporre dati come le operazioni di installazione separato, con una "-dipendenza" suffisso.

* Installazione di
* Dipendenza di installazione
* Aggiorna
* Dipendenza di aggiornamento
* Reinstallazione
* Dipendenza reinstallare

Oltre al nome di operazione diversa, l'id di pacchetto dipendente viene anche registrato per l'installazione.  Un aggiornamento futuro a raccolta NuGet esporrà i dati all'interno dei report, consentendo agli autori di pacchetti comprendere appieno come gli sviluppatori installa i pacchetti.

## <a name="bug-fixes"></a>Correzioni di bug

2.6 NuGet include anche diverse correzioni di bug. Per un elenco completo di lavoro gli elementi corretti in NuGet 2.6,. visualizzazione di [NuGet Issue Tracker per questa versione](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).