---
title: Note sulla versione 2.6 di NuGet
description: Note sulla versione per NuGet 2.6.1 per WebMatrix, inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f011a8db7ac2067a2ed7db67849d63f7dd40d1ce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551943"
---
# <a name="nuget-26-release-notes"></a>Note sulla versione 2.6 di NuGet

[Note sulla versione di NuGet 2.5](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 per WebMatrix note](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 è stato rilasciato il 26 giugno 2013.

## <a name="notable-features-in-the-release"></a>Funzionalità di rilievo nella versione

### <a name="support-for-visual-studio-2013"></a>Supporto per Visual Studio 2013

NuGet 2.6 è la prima versione che fornisce il supporto per Visual Studio 2013. E, ad esempio Visual Studio 2012, l'estensione Gestione pacchetti NuGet è incluso in tutte le edizioni di Visual Studio.

Per offrire il miglior supporto possibile per Visual Studio 2013, mentre il supporto sia Visual Studio 2010 e Visual Studio 2012 e mantenendo le dimensioni di estensione più piccole possibile, si sta producendo un'estensione separata per Visual Studio 2013, mentre il estensione originale continua a fare riferimento sia Visual Studio 2010 e 2012.

A partire da NuGet 2.6, verranno pubblicate due estensioni come indicato di seguito:

1. [Gestione pacchetti NuGet](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (si applica a Visual Studio 2010 e 2012)
1. [Gestione pacchetti NuGet per Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Con questa suddivisione, la [nuget.org](https://nuget.org) visualizzata sul pulsante "Installa NuGet" della home page di [installazione di NuGet](../install-nuget-client-tools.md) pagina, in cui è possibile trovare ulteriori informazioni sull'installazione di diversi client di NuGet.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Supporto per le trasformazioni XDT Web. config

Una delle funzionalità altamente richieste per il client di NuGet è stata per supportare più potente trasformazioni XML utilizzando il motore di trasformazione XDT che viene utilizzato per le trasformazioni di configurazione di compilazione di Visual Studio.

Ad aprile 2013 sono stati apportati due big annunci relativi al supporto di NuGet per XDT. Il primo era che la stessa libreria di XDT è stato in corso se stesso [rilasciata come pacchetto NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) e [reso open source su CodePlex](http://xdt.codeplex.com/). Questo passaggio è abilitato il motore di XDT liberamente utilizzabile da altri software open source, tra cui il client di NuGet. L'annuncio del secondo è il piano per supportare l'uso del motore di XDT per le trasformazioni del client NuGet. NuGet 2.6 include questa integrazione.

#### <a name="how-it-works"></a>Come funziona

Per sfruttare i vantaggi del supporto XDT di NuGet, i meccanismi simili a quelle del [funzionalità di trasformazione configurazione corrente](../create-packages/source-and-config-file-transformations.md).
File di trasformazione vengono aggiunti alla cartella del contenuto del pacchetto. Tuttavia, durante le trasformazioni di configurazione usano un singolo file per installazione e alla disinstallazione, trasformazioni XDT abilitare il controllo con granularità fine su entrambi i processi tramite i file seguenti:

- Web.config.install.xdt
- Web.config.uninstall.xdt

Inoltre, NuGet Usa il suffisso del file per determinare quali motore di esecuzione per le trasformazioni, in modo che i pacchetti usando il web.config.transforms esistenti continueranno a funzionare. Trasformazioni XDT possono anche essere applicate a qualsiasi file XML (non solo Web. config), è possibile pertanto sfruttare questo per le altre applicazioni nel progetto.

#### <a name="what-you-can-do-with-xdt"></a>Operazioni eseguibili con XDT

Uno dei maggiori punti di forza di XDT è relativi [semplice ma potente sintassi](http://msdn.microsoft.com/library/dd465326.aspx) per la modifica della struttura di un DOM. XML Invece di sovrapporre semplicemente una struttura del documento fisso in un'altra struttura, XDT fornisce controlli per la corrispondenza di elementi in diversi modi: dall'attributo semplice corrispondenza dei nomi per il supporto XPath completo. Dopo aver trovato un elemento corrispondente o un set di elementi, XDT fornisce un'ampia gamma di funzioni per la modifica degli elementi, indipendentemente dal fatto che questa aggiunta, l'aggiornamento, o la rimozione di attributi, l'inserimento di un nuovo elemento in una posizione specifica, o la sostituzione o rimozione dell'intero elemento e i relativi elementi figlio.

### <a name="machine-wide-configuration"></a>Configurazione a livello di computer

Uno dei punti di forza di NuGet ideale è che viene suddivisa in un file eseguibile di grandi dimensioni in caso contrario, o una raccolta in un set di componenti modulari che può essere integrata e cosa ancora più importante gestita e con controllo delle versioni in modo indipendente. Uno degli effetti collaterali, tuttavia, è che il concetto tradizionale di un prodotto o famiglia di prodotti potenzialmente diventa più frammentato.
Funzionalità dell'origine pacchetto personalizzato di NuGet fornisce un modo per organizzare i pacchetti; Tuttavia, origini dei pacchetti personalizzati non possono essere individuate in modo indipendente.

NuGet 2.6 estende la logica per la configurazione di NuGet da una ricerca nella gerarchia di cartelle nel percorso % ProgramData%/NuGet/Config. Programmi di installazione del prodotto possono aggiungere file di configurazione NuGet personalizzati in questa cartella per registrare un'origine di pacchetto personalizzato per i loro prodotti. Inoltre, la struttura di cartelle supporta la semantica per prodotto, versione e anche lo SKU dell'IDE. Da queste directory vengono applicate nell'ordine seguente con una strategia di precedenza "last in wins".

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config

In questo elenco, il segnaposto {IDE} è specifico per l'IDE in cui è in esecuzione NuGet, pertanto nel caso di Visual Studio, sarà "Visual Studio". {Versione} e il segnaposto {SKU} viene fornito dall'IDE (ad esempio, "11.0" e "WDExpress", "VWDExpress" e "Plus", rispettivamente). La cartella può quindi contenere molti file *.config diversi.
Pertanto, la società componente ACME possibile, come parte del programma di installazione prodotti, aggiungere un'origine pacchetto personalizzato che sarà visibile solo nelle versioni di Visual Studio 2012 Professional e Ultimate creando il percorso del file seguente:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Mentre la struttura di cartelle rende più semplice per i programmi, ad esempio programmi di installazione del software necessario aggiungere origini dei pacchetti a livello di computer alla configurazione di NuGet, la finestra di dialogo di configurazione di NuGet è stata aggiornata anche per consentire la registrazione delle origini dei pacchetti come entrambi specifiche dell'utente (ad esempio, registrato nel % AppData%/NuGet/NuGet.Config) o a livello di computer.

Questa funzionalità viene usata da Visual Studio 2013, in cui un file viene installato in:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

All'interno di questo file, viene configurata una nuova origine pacchetto denominata "Pacchetti di .NET Framework".

![Impostazioni a livello di computer il File di configurazione NuGet](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contestualizzazione delle ricerca

Il numero di pacchetti servite da NuGet gallery continua a crescere a un ritmo esponenziale e miglioramento della ricerca rimane sempre nella parte superiore dell'elenco di priorità di NuGet. Una delle funzionalità pianificate per NuGet è ricerche contestuali, vale a dire che NuGet utilizzerà informazioni sulla versione e lo SKU di Visual Studio che si sta utilizzando e il tipo di progetto che si sta compilando come criterio per determinare la rilevanza della ricerca di potenziali risultati.

A partire da NuGet 2.6, ogni volta che viene installato un pacchetto, il contesto per l'installazione viene registrato come parte dei dati dell'operazione di installazione.  Le ricerche inviare anche le stesse informazioni di contesto, in modo da permettere la raccolta NuGet migliorare i risultati della ricerca delle tendenze di installazione rapida.  Un aggiornamento futuro a NuGet Gallery abiliterà questo boosting pertinenza sensibile al contesto.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Registrazione diretta consente di installare Visual Studio. Installazione delle dipendenze

Gli autori di pacchetti dipende più il [statistiche pacchetto](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) fornito nella raccolta NuGet.  Uno dei punti dati mancanti significativi che gli autori hanno richiesto è un fattore di differenziazione tra le installazioni delle dipendenze e dell'installazione pacchetto diretto.  Fino ad ora, il client di NuGet non ha inviato alcun contesto per l'operazione di installazione per lo sviluppatore se installato direttamente il pacchetto o se è stato installato per soddisfare una dipendenza.
A partire da NuGet 2.6, che ora i dati verranno inviati per l'operazione di installazione.  Le statistiche di pacchetto nella raccolta NuGet esporrà i dati come operazioni di installazione separata, con un "-dipendenza" suffisso.

* Installazione di
* Installazione delle dipendenze
* Aggiorna
* Aggiornamento delle dipendenze
* Reinstallazione
* Dipendenza reinstallare

Oltre al nome di operazione diversa, l'id pacchetto dipendente viene anche registrato per l'installazione.  Un aggiornamento futuro a NuGet Gallery esporrà i dati all'interno dei report, che consente agli autori di aiutino a comprendere appieno come gli sviluppatori installa i propri pacchetti.

## <a name="bug-fixes"></a>Correzioni di bug

NuGet 2.6 include anche diverse correzioni di bug. Per un elenco completo di lavoro elementi di risolti in NuGet 2.6, vista la [NuGet Issue Tracker per questa versione](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).