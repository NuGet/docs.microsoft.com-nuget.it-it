---
title: Ricerca e scelta di pacchetti NuGet
description: Panoramica delle modalità di ricerca e scelta dei pacchetti NuGet più appropriati per un progetto, inclusi i dettagli della sintassi di ricerca NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: f1bb145229b0db0e8fdb7fdb31a59aa50bd1d57b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817902"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Ricerca e valutazione di pacchetti NuGet per un progetto

Quando si avvia un progetto .NET o ogni volta che si identifica una richiesta di funzionalità per un'app o un servizio, è possibile risparmiare tempo ed evitare problemi usando pacchetti NuGet esistenti che consentono di soddisfare tale richiesta. Questi pacchetti possono provenire dalla raccolta pubblica su [nuget.org](http://www.nuget.org/packages/) o da un'origine privata fornita dall'organizzazione o da terze parti.

## <a name="finding-packages"></a>Ricerca di pacchetti

Quando si visita nuget.org o si apre l'interfaccia utente di Gestione pacchetti in Visual Studio, viene visualizzato un elenco di pacchetti ordinati in base al numero totale di download. In questo modo sarà possibile avere una visione immediata dei pacchetti più diffusi tra milioni di progetti .NET. È probabile quindi che almeno alcuni dei pacchetti elencati nelle prime pagine potranno essere utili per i propri progetti.

![Visualizzazione predefinita di nuget.org che mostra i pacchetti più diffusi](media/Finding-01-Popularity.png)

Si noti l'opzione **Include prerelease** (Includi versione preliminare) in alto a destra nella pagina. Quando questa casella di controllo è selezionata, nuget.org mostra tutte le versioni dei pacchetti incluse le versioni beta e altre versioni preliminari. Per mostrare solo le versioni rilasciate stabili, deselezionare questa opzione.

Per esigenze specifiche, la ricerca per tag (all'interno di Gestione pacchetti di Visual Studio o in un portale come nuget.org) è il metodo più comune per individuare un pacchetto appropriato. Ad esempio, una ricerca basata su "json" elenca tutti i pacchetti NuGet contrassegnati da questa parola chiave, che hanno quindi una relazione con il formato dati JSON.

![Risultati della ricerca per "json" su nuget.org](media/Finding-02-SearchResults.png)

È anche possibile eseguire una ricerca usando l'ID del pacchetto, se lo si conosce. Vedere [Sintassi di ricerca](#search-syntax) più avanti in questo articolo.

A questo punto, i risultati della ricerca sono ordinati solo per pertinenza, pertanto è consigliabile esaminare almeno le prime pagine dei risultati per individuare i pacchetti più appropriati alle specifiche esigenze o ridefinire i termini di ricerca per essere più precisi.

### <a name="does-the-package-support-my-projects-target-framework"></a>Il pacchetto supporta il framework di destinazione del progetto?

NuGet installa un pacchetto in un progetto solo se i framework supportati di tale pacchetto includono il framework di destinazione del progetto. Se il pacchetto non è compatibile, NuGet genera un errore.

Alcuni pacchetti elencano i framework supportati direttamente nella raccolta nuget.org, ma poiché questi dati non sono richiesti, molti pacchetti non includono tale elenco. Al momento, non è disponibile alcuna modalità di ricerca su nuget.org per i pacchetti che supportano un framework di destinazione specifico (la funzionalità è in fase di analisi, vedere il [problema NuGet 2936](https://github.com/NuGet/NuGetGallery/issues/2936)).

Fortunatamente, è possibile determinare i framework supportati in altri due modi:

1. Tentare di installare un pacchetto in un progetto usando il comando [`Install-Package`](../tools/ps-ref-install-package.md) nella console di Gestione pacchetti NuGet. Se il pacchetto non è compatibile, questo comando mostra i framework supportati del pacchetto.

1. Scaricare il pacchetto dalla relativa pagina su nuget.org tramite il collegamento **Manual download** (Download manuale) in **Info**. Modificare l'estensione da `.nupkg` in `.zip` e aprire il file per esaminare il contenuto della relativa cartella `lib`. Vengono elencate le sottocartelle per ognuno dei framework supportati, in cui ogni sottocartella è denominata con un moniker del framework di destinazione (vedere [Framework di destinazione](../reference/target-frameworks.md)). Se non vengono visualizzate sottocartelle in `lib` ed è visibile solo una singola DLL, sarà necessario tentare di installare il pacchetto nel progetto per individuarne la compatibilità.

## <a name="pre-release-packages"></a>Pacchetti in versione non definitiva

Molti autori di pacchetti rendono disponibili versioni beta e di anteprima a mano a mano che apportano miglioramenti e implementano i commenti e i suggerimenti ricevuti nelle revisioni più aggiornate.

Per impostazione predefinita, nuget.org mostra anche i pacchetti in versione non definitiva nei risultati della ricerca. Per eseguire la ricerca solo tra le versioni stabili, deselezionare l'opzione **Include prerelease** (Includi versione preliminare) in alto a destra nella pagina.

![Casella di controllo Include prerelease (Includi versione preliminare) su nuget.org](media/Finding-06-include-prerelease.png)

In Visual Studio e quando si usano le interfacce della riga di comando di NuGet e dotnet, NuGet non include le versioni non definitive per impostazione predefinita. Per modificare questo comportamento, attenersi alla procedura seguente:

- **Interfaccia utente di Gestione pacchetti in Visual Studio**: nell'interfaccia utente di **Gestisci pacchetti NuGet** selezionare la casella di controllo **Includi versione preliminare**. La selezione o la deselezione di questa casella di controllo aggiorna l'interfaccia utente di Gestione pacchetti e l'elenco delle versioni disponibili che è possibile installare.

    ![Casella di controllo Includi versione preliminare in Visual Studio](media/Prerelease_02-CheckPrerelease.png)

- **Console di Gestione pacchetti**: usare l'opzione `-IncludePrerelease` con i comandi `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` e `Update-Package`. Vedere [Informazioni di riferimento su PowerShell](../tools/powershell-reference.md).

- **Interfaccia della riga di comando nuget.exe**: usare l'opzione `-prerelease` con i comandi `install`, `update`, `delete` e `mirror`. Vedere [NuGet CLI reference](../tools/nuget-exe-cli-reference.md) (Informazioni di riferimento sull'interfaccia della riga di comando di NuGet).

- **Interfaccia della riga di comando dotnet.exe**: specificare l'esatta versione non definitiva tramite l'argomento `-v`. Vedere le [informazioni di riferimento su dotnet add package](/dotnet/core/tools/dotnet-add-package).

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Pacchetti C++ nativi

NuGet supporta pacchetti C++ nativi utilizzabili nei progetti C++ in Visual Studio. Ciò consente di usare il comando del menu di scelta rapida **Gestisci pacchetti NuGet** per i progetti, introduce un framework di destinazione `native` e fornisce l'integrazione con MSBuild.

Per trovare i pacchetti nativi su [nuget.org](https://www.nuget.org/packages), eseguire la ricerca usando `tag:native`. Tali pacchetti forniscono in genere file `.targets` e `.props`, che NuGet importa automaticamente quando il pacchetto viene aggiunto a un progetto.

## <a name="evaluating-packages"></a>Valutazione di pacchetti

Il modo migliore per valutare l'utilità di un pacchetto è scaricarlo e provarlo nel codice (si noti che in tutti i pacchetti in nuget.org viene eseguita regolarmente la ricerca di virus). Dopo tutto, ogni pacchetto ampiamente diffuso all'inizio è stato usato solo da pochi sviluppatori, i cosiddetti early adopter

Allo stesso tempo, usare un pacchetto NuGet implica la creazione di una dipendenza da tale pacchetto, pertanto occorre assicurarsi che sia efficace e affidabile. Poiché l'installazione e il test diretto di un pacchetto richiedono tempo, è anche possibile saperne di più sulla qualità di un pacchetto usando le informazioni riportate nella pagina di presentazione del pacchetto stesso:

- *Statistiche di download*: la sezione **Statistics** (Statistiche) nella pagina del pacchetto su nuget.org mostra il numero totale di download, i download della versione più recente e la media dei download al giorno. Numeri elevati indicano che molti altri sviluppatori hanno una dipendenza dal pacchetto, il che significa che la sua utilità è comprovata.

    ![Statistiche di download nella pagina di presentazione del pacchetto](media/Finding-03-Downloads.png)

- *Cronologia delle versioni*: nella pagina del pacchetto cercare in **Info** la data dell'ultimo aggiornamento ed esaminare la voce **Version History** (Cronologia versioni). Un pacchetto ben gestito ha aggiornamenti recenti e una cronologia versioni dettagliata. I pacchetti trascurati hanno pochi aggiornamenti e spesso non sono stati aggiornati da tempo.

    ![Cronologia delle versioni nella pagina di presentazione del pacchetto](media/Finding-04-VersionHistory.png)

- *Installazioni recenti*: nella pagina del pacchetto in **Statistics** (Statistiche) selezionare **View full stats** (Visualizza statistiche complete). La pagina delle statistiche complete mostra le installazioni del pacchetto nelle ultime sei settimane per numero di versione. Un pacchetto che altri sviluppatori usano attivamente in genere è preferibile rispetto a uno non in uso.

- *Supporto*: nella pagina del pacchetto in **Info** selezionare **Project Site** (Sito del progetto), se disponibile, per verificare le opzioni di supporto messe a disposizione dall'autore. Un progetto con un sito dedicato in genere è supportato in modo migliore.

- *Cronologia degli sviluppatori*: nella pagina del pacchetto in **Owners** (Proprietari) selezionare un proprietario per vedere quali altri pacchetti ha pubblicato. Gli autori di più pacchetti hanno più probabilità di continuare a fornire supporto per il proprio lavoro in futuro.

- *Contributi open source*: molti pacchetti vengono mantenuti in repository open source, rendendo possibile per gli sviluppatori che dipendono da tali pacchetti di contribuire direttamente alle correzioni dei bug e ai miglioramenti delle funzionalità. La cronologia dei contributi di un dato pacchetto è inoltre un ottimo indicatore di quanti sviluppatori sono attivamente coinvolti.

- *Contatti con i proprietari*: i nuovi sviluppatori dimostrano indiscutibilmente il loro impegno a realizzare ottimi pacchetti utilizzabili dall'utente, pertanto è opportuno dar loro la possibilità di dare il proprio contributo nell'ecosistema NuGet. Se si vuole, è possibile contattare direttamente lo sviluppatore di un pacchetto tramite l'opzione **Contact Owners** (Contatta proprietari) in **Info** nella pagina di presentazione del pacchetto. Ci sono buone probabilità che sia lieto di collaborare per soddisfare le esigenze dei suoi utenti.

- *Prefissi ID pacchetto riservati*: molti proprietari di pacchetti hanno richiesto e ottenuto un [prefisso ID pacchetto riservato](../reference/id-prefix-reservation.md). Un segno di spunta visualizzato accanto all'ID di un pacchetto in [nuget.org](https://www.nuget.org/) o in Visual Studio indica che il proprietario del pacchetto soddisfa i [criteri](../reference/id-prefix-reservation.md#id-prefix-reservation-criteria) stabiliti per la prenotazione del prefisso ID. Ciò significa che il proprietario del pacchetto renderà disponibile il suo identificativo e quello del pacchetto.

> [!Note]
> Tenere sempre in considerazione le condizioni di licenza di un pacchetto, che è possibile visualizzare selezionando **License Info** (Informazioni di licenza) nella pagina di presentazione di un pacchetto su nuget.org. Se per un pacchetto non sono specificate le condizioni di licenza, contattare il proprietario del pacchetto direttamente usando il collegamento **Contact owners** (Contatta proprietari) nella pagina del pacchetto. Microsoft non concede in licenza all'utente alcuna proprietà intellettuale dei provider di pacchetti di terze parti e non è responsabile per le informazioni fornite da terze parti.

## <a name="search-syntax"></a>Sintassi di ricerca

La modalità di ricerca di un pacchetto in NuGet è la stessa su nuget.org, dall'interfaccia della riga di comando di NuGet e all'interno dell'estensione Gestione pacchetti NuGet in Visual Studio. In generale, la ricerca viene applicata alle parole chiave e alle descrizioni dei pacchetti.

- **Parole chiave**: la ricerca mira a individuare i pacchetti pertinenti che contengono una qualsiasi delle parole chiave specificate. Esempio: `modern UI`. Per eseguire la ricerca per i pacchetti che contengono tutte le parole chiave fornite, usare "+" tra le condizioni, ad esempio `modern+UI`.
- **Frasi**: se si immettono i termini di ricerca tra virgolette, vengono rilevate le esatte corrispondenze senza distinzione tra maiuscole e minuscole con tali termini. Esempio: `"modern UI" package`
- **Filtro**: è possibile applicare un termine di ricerca a una proprietà specifica usando la sintassi `<property>:<term>`, dove `<property>` (senza distinzione tra maiuscole e minuscole) può essere `id`, `packageid`, `version`, `title`, `tags`, `author`, `description`, `summary` e `owner`. I termini di ricerca possono essere contenuti tra virgolette, se necessario, ed è possibile cercare più proprietà contemporaneamente. Inoltre, le ricerche nella proprietà `id` sono corrispondenze di sottostringhe, mentre `packageid` usa una corrispondenza esatta. Esempi:

    ```
    id:NuGet.Core                # Match any part of the id property
    Id:"Nuget.Core"
    ID:jQuery
    title:jquery                 # Searches title as shown on the package listing
    PackageId:jquery             # Match the package id exactly
    id:jquery id:ui              # Search for multiple terms in the id
    id:jquery tags:validation    # Search multiple properties
    id:"jquery.ui"               # Phrase search
    invalid:jquery ui            # Unsupported properties are ignored, so this
                                 # is the same as searching on jquery ui
    ```
