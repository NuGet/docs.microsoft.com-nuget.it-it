---
title: Che cos'è NuGet e cosa fa?
description: Un'introduzione completa a che cos'è NuGet e cosa fa.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: overview
ms.openlocfilehash: e8e806e0a893d62d9d3189396dc47250ae9c8cf3
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68420022"
---
# <a name="an-introduction-to-nuget"></a>Introduzione a NuGet

Uno strumento essenziale per qualsiasi piattaforma di sviluppo moderna è un meccanismo attraverso il quale gli sviluppatori possano creare, condividere e utilizzare codice utile. Spesso questo codice viene incluso in "pacchetti" che contengono codice compilato, ad esempio file DLL, insieme ad altri contenuti necessari nei progetti che utilizzano questi pacchetti.

Per .NET (incluso .NET Core), il meccanismo supportato da Microsoft per la condivisione del codice è **NuGet**, che definisce in che modo vengono creati, ospitati e utilizzati i pacchetti per .NET e [fornisce gli strumenti](install-nuget-client-tools.md) per ognuno di questi ruoli.

In altri termini, un pacchetto NuGet è un singolo file ZIP con l'estensione `.nupkg` che contiene codice compilato (DLL), altri file correlati a tale codice e un manifesto descrittivo che include informazioni come il numero di versione del pacchetto. Gli sviluppatori con codice da condividere creano pacchetti e li pubblicano in un host pubblico o privato. I consumer di pacchetti ottengono tali pacchetti dagli host appropriati, li aggiungono ai loro progetti e quindi chiamano le funzionalità di un pacchetto nel codice dei progetti. NuGet gestisce tutti i dettagli intermedi.

Dato che NuGet supporta gli host privati oltre all'host nuget.org pubblico, è possibile usare i pacchetti NuGet per condividere codice esclusivo per un'organizzazione o un gruppo di lavoro. È anche possibile usare i pacchetti NuGet come un modo pratico per eseguire il factoring del codice per usarlo esclusivamente nei progetti personali. In breve, un pacchetto NuGet è un'unità di codice condivisibile, ma non richiede né implica un modo particolare di condivisione.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Flusso dei pacchetti tra autori, host e consumer

Nel proprio ruolo di host pubblico, NuGet gestisce il repository centrale di più di 100.000 pacchetti univoci su [nuget.org](https://www.nuget.org). Questi pacchetti vengono usati da milioni di sviluppatori .NET/.NET Core ogni giorno. NuGet consente anche di ospitare i pacchetti in modo privato nel cloud (ad esempio in Azure DevOps), in una rete privata o anche solo nel file system locale. In questo modo, i pacchetti sono disponibili solo per gli sviluppatori che hanno accesso all'host, offrendo la possibilità di rendere disponibili i pacchetti a uno specifico gruppo di consumer. Le opzioni sono illustrate in [Hosting dei feed NuGet](hosting-packages/overview.md). Tramite le opzioni di configurazione, è anche possibile controllare esattamente quali host sono accessibili da qualsiasi computer specificato, in modo da assicurare che i pacchetti vengano ottenuti da origini specifiche anziché da un repository pubblico come nuget.org.

Qualunque sia la sua natura, un host funge da punto di connessione tra gli *autori* e i *consumer* dei pacchetti. Gli autori compilano utili pacchetti NuGet e li pubblicano in un host. I consumer cercano quindi i pacchetti utili e compatibili negli host accessibili, scaricandoli e includendoli nei loro progetti. Una volta installate in un progetto, le API dei pacchetti sono disponibili per il resto del codice del progetto.

![Relazione tra autori, host e consumer dei pacchetti](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>Pacchetto per la compatibilità

Con pacchetto "compatibile" si intende un pacchetto che contiene gli assembly compilati per almeno un framework .NET di destinazione compatibile con il framework di destinazione del progetto che lo utilizza. Gli sviluppatori possono creare pacchetti specifici per un framework, come per i controlli UWP o possono supportare una gamma più ampia di destinazioni. Per ottimizzare la compatibilità di un pacchetto, gli sviluppatori scelgono la destinazione [.NET Standard](/dotnet/standard/net-standard), utilizzabile da tutti i progetti .NET e .NET Core. Questo è il modo più efficiente sia per gli autori che per i consumer, perché un singolo pacchetto (in genere contenente un singolo assembly) funziona per tutti i progetti che lo utilizzano.

Gli sviluppatori di pacchetti che devono usare API al di fuori di .NET Standard, d'altra parte, creano assembly separati per i diversi framework di destinazione che vogliono supportare e includono tutti gli assembly nello stesso pacchetto (operazione nota come "multitargeting"). Quando un consumer installa un pacchetto di questo tipo, NuGet estrae solo gli assembly necessari per il progetto. Ciò contribuisce a ridurre al minimo il footprint del pacchetto nell'applicazione finale e/o gli assembly generati da tale progetto. Un pacchetto multitargeting è naturalmente più difficile da gestire per l'autore.

> [!Note]
> La scelta di .NET Standard come destinazione sostituisce l'approccio precedente che prevede l'uso di varie destinazioni libreria di classi portabile (PCL). Questa documentazione è quindi incentrata sulla creazione di pacchetti per .NET Standard.

## <a name="nuget-tools"></a>Strumenti NuGet

Oltre a ospitare il supporto, NuGet fornisce anche un'ampia gamma di strumenti usati da autori e consumer. Vedere [Installazione degli strumenti client di NuGet](install-nuget-client-tools.md) per istruzioni su come ottenere strumenti specifici.

| Strumento | Piattaforme | Scenari possibili | DESCRIZIONE |
| --- | --- | --- | --- |
| [Interfaccia della riga di comando di dotnet](consume-packages/install-use-packages-dotnet-cli.md) | Tutti | Creazione, utilizzo | Strumento della riga di comando per librerie .NET Core e .NET Standard e per progetti in stile SDK destinati a .NET Framework (vedere [Attributo Sdk](/dotnet/core/tools/csproj#additions)). Fornisce determinate funzionalità dell'interfaccia della riga di comando di NuGet direttamente all'interno della toolchain di .NET Core. Come per l'interfaccia della riga di comando di `nuget.exe`, l'interfaccia della riga di comando di dotnet non interagisce con i progetti di Visual Studio. |
| [Interfaccia della riga di comando di nuget.exe](consume-packages/install-use-packages-nuget-cli.md) | Tutti | Creazione, utilizzo | Strumento della riga di comando per librerie .NET Framework e per i progetti non in stile SDK destinati alle librerie .NET Standard. Fornisce tutte le funzionalità di NuGet, con alcuni comandi applicabili in modo specifico agli autori dei pacchetti, altri applicabili solo ai consumer e altri ancora applicabili a entrambi. Ad esempio, gli autori dei pacchetti usano il comando `nuget pack` per creare un pacchetto da vari assembly e file correlati, i consumer dei pacchetti usano `nuget install` per includere i pacchetti in una cartella di progetto e tutti gli utenti usano `nuget config` per impostare le variabili di configurazione di NuGet. In quanto strumento indipendente dalla piattaforma, l'interfaccia della riga di comando di NuGet non interagisce con i progetti di Visual Studio. |
| [Console di Gestione pacchetti](consume-packages/install-use-packages-powershell.md) | Visual Studio su Windows | Utilizzo | Fornisce i [comandi di PowerShell](reference/Powershell-Reference.md) per l'installazione e la gestione dei pacchetti nei progetti Visual Studio. |
| [Interfaccia utente di Gestione pacchetti](consume-packages/install-use-packages-visual-studio.md) | Visual Studio su Windows | Utilizzo | Fornisce un'interfaccia utente di facile utilizzo per l'installazione e la gestione dei pacchetti nei progetti Visual Studio. |
| [Interfaccia utente di Gestisci pacchetti NuGet](/visualstudio/mac/nuget-walkthrough) | Visual Studio per Mac | Utilizzo | Fornisce un'interfaccia utente di semplice utilizzo per l'installazione e la gestione dei pacchetti nei progetti di Visual Studio per Mac. |
| [MSBuild](reference/msbuild-targets.md) | WINDOWS | Creazione, utilizzo | Fornisce la possibilità di creare pacchetti e ripristinare quelli usati in un progetto direttamente tramite la toolchain di MSBuild. |

Come si può notare, gli strumenti NuGet da usare variano notevolmente in base al fatto che si stiano creando, utilizzando o pubblicando i pacchetti, oltre che in base alla piattaforma in uso. Gli autori dei pacchetti in genere sono anche consumer, dal momento che compilano sulla base di funzionalità disponibili in altri pacchetti NuGet. E tali pacchetti, naturalmente, possono dipendere a loro volta da altri.

Per altre informazioni, iniziare con gli articoli [Flusso di lavoro della creazione di pacchetti](create-packages/Overview-and-Workflow.md) e [Flusso di lavoro dell'utilizzo di pacchetti](consume-packages/Overview-and-Workflow.md).

## <a name="managing-dependencies"></a>Gestione delle dipendenze

La possibilità di riutilizzare facilmente il lavoro di altri utenti è una delle funzionalità più utili di un sistema di gestione pacchetti. Di conseguenza, la maggior parte delle operazioni eseguite da NuGet è correlata alla gestione di tale albero delle dipendenze, o "grafico", per conto di un progetto. Detto in parole più semplici, sarà necessario preoccuparsi solo dei pacchetti che si usano direttamente in un progetto. Se uno di questi pacchetti utilizza altri pacchetti (che possono a loro volta utilizzare altri pacchetti), NuGet si occupa di tutte queste dipendenze di livello inferiore.

La figura seguente mostra un progetto che dipende da cinque pacchetti, che a loro volta dipendono da un numero di altri pacchetti.

![Esempio di grafico dipendenze di NuGet per un progetto .NET](media/dependency-graph.png)

Si noti che alcuni pacchetti compaiono più volte nel grafico dipendenze. Ad esempio, sono visibili tre diversi consumer del pacchetto B e ogni consumer potrebbe anche specificare una versione diversa per tale pacchetto (non riportato nella figura). Si tratta di una situazione comune, in particolare per i pacchetti usati diffusamente. Fortunatamente NuGet esegue tutte le operazioni necessarie per determinare esattamente quale versione del pacchetto B soddisfi tutti i consumer. NuGet fa quindi lo stesso per tutti gli altri pacchetti, indipendentemente dal livello di profondità del grafico dipendenze.

Per maggiori dettagli sul funzionamento di questo servizio in NuGet, vedere [Risoluzione delle dipendenze](consume-packages/dependency-resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Rilevamento dei riferimenti e ripristino dei pacchetti

Dal momento che i progetti possono essere spostati facilmente tra computer degli sviluppatori, repository del controllo del codice sorgente, server di compilazione e così via, è estremamente poco pratico mantenere gli assembly binari dei pacchetti NuGet associati direttamente a un progetto. In questo modo, ogni copia del progetto avrebbe dimensioni inutilmente molto grandi, con conseguente spreco di spazio nei repository del controllo del codice sorgente. Risulterebbe anche molto difficile aggiornare i file binari del pacchetto a versioni più recenti, perché gli aggiornamenti dovrebbero essere applicati a tutte le copie del progetto.

NuGet gestisce invece un semplice elenco di riferimento dei pacchetti da cui dipende un progetto, incluse sia le dipendenze di primo livello che quelle di livello inferiore. Ovvero, quando si installa un pacchetto da un host in un progetto, NuGet registra l'identificatore del pacchetto e il numero di versione nell'elenco di riferimento. La disinstallazione di un pacchetto, naturalmente, ne comporta la rimozione dall'elenco. NuGet offre quindi un modo per ripristinare tutti i pacchetti a cui si fa riferimento su richiesta, come descritto in [Ripristino di pacchetti](consume-packages/package-restore.md).

![Nell'installazione del pacchetto viene creato un elenco di riferimenti NuGet che può essere usato per ripristinare i pacchetti in un'altra posizione.](media/nuget-restore.png)

Con solo questo elenco di riferimenti, NuGet può quindi reinstallare, ovvero *ripristinare*, successivamente tutti questi pacchetti da host pubblici e/o privati. Quando si esegue il commit di un progetto nel controllo del codice sorgente o lo si condivide in qualsiasi altro modo, è necessario includere solo l'elenco dei riferimenti e non occorre escludere eventuali file binari dei pacchetti (vedere [Pacchetti e controllo del codice sorgente](consume-packages/packages-and-source-control.md)).

Il computer che riceve un progetto, ad esempio un server di compilazione che ottiene una copia del progetto come parte di un sistema di distribuzione automatica, chiede semplicemente a NuGet di ripristinare le dipendenze ogni volta che sono necessarie. Sistemi di compilazione come Azure DevOps prevedono passaggi di "ripristino NuGet" per questo esatto scopo. Analogamente, quando gli sviluppatori ottengono una copia di un progetto (come avviene nel caso della clonazione di un repository), possono richiamare un comando come `nuget restore` (interfaccia della riga di comando di NuGet), `dotnet restore` (interfaccia della riga di comando di dotnet), o `Install-Package` (console di Gestione pacchetti) per ottenere tutti i pacchetti necessari. Visual Studio, per la propria parte, ripristina automaticamente i pacchetti quando compila un progetto, a condizione che il ripristino automatico sia abilitato, come descritto in [Ripristino di pacchetti](consume-packages/package-restore.md).

Chiaramente, quindi, il ruolo primario di NuGet in cui gli sviluppatori sono coinvolti è la gestione di tale elenco di riferimenti per conto del progetto e la disponibilità di strumenti per ripristinare (e aggiornare) in modo efficiente tali pacchetti con riferimenti. Questo elenco viene mantenuto in uno di due *formati di gestione dei pacchetti*:

- [PackageReference](consume-packages/package-references-in-project-files.md) (o "riferimenti ai pacchetti nei file di progetto") | *(NuGet 4.0+)* Gestisce un elenco di dipendenze di livello superiore di un progetto direttamente all'interno del file di progetto, pertanto non occorre un file separato. Un file associato, `obj/project.assets.json`, viene generato dinamicamente per gestire il grafico delle dipendenze complessive dei pacchetti usati da un progetto insieme a tutte le dipendenze di livello inferiore. PackageReference viene sempre usato dai progetti .NET Core.

- [`packages.config`](reference/packages-config.md): *(NuGet 1.0+)* File XML che gestisce un elenco completo di tutte le dipendenze nel progetto, incluse le dipendenze di altri pacchetti installati. I pacchetti installati o ripristinati vengono archiviati in una cartella `packages`.

Il formato di gestione dei pacchetti usato in un determinato progetto dipende dal tipo di progetto e dalla versione di NuGet (e/o Visual Studio) disponibile. Per verificare il formato in uso, è sufficiente cercare `packages.config` nella radice del progetto dopo l'installazione del primo pacchetto. Se tale file non è disponibile, cercare direttamente un elemento \<PackageReference\> nel file di progetto.

Se è possibile scegliere, è consigliabile usare PackageReference. Il file `packages.config` viene mantenuto per applicazioni legacy e non è più in fase di sviluppo attivo.

> [!Tip]
> Vari comandi dell'interfaccia della riga di comando `nuget.exe`, ad esempio `nuget install`, non aggiungono automaticamente il pacchetto all'elenco di riferimenti. L'elenco viene aggiornato quando si installa un pacchetto con Gestione pacchetti di Visual Studio (interfaccia utente o console) e con l'interfaccia della riga di comando `dotnet.exe`.

## <a name="what-else-does-nuget-do"></a>Che cos'altro fa NuGet?

Finora sono state presentate le caratteristiche seguenti di NuGet:

- NuGet offre il repository centrale nuget.org con supporto per l'hosting privato.
- NuGet offre gli strumenti di cui gli sviluppatori hanno bisogno per creare, pubblicare e utilizzare i pacchetti.
- Cosa ancora più importante, NuGet gestisce un elenco dei riferimenti dei pacchetti usati in un progetto, consentendo di ripristinare e aggiornare i pacchetti da tale elenco.

Per assicurare l'efficienza di questi processi, NuGet esegue alcune ottimizzazioni in background. In particolare, NuGet gestisce una cache dei pacchetti e una cartella globale dei pacchetti per velocizzare le operazioni di installazione e reinstallazione. La cache consente di evitare il download di un pacchetto già installato nel computer. La cartella dei pacchetti globale consente a più progetti di condividere lo stesso pacchetto installato, riducendo così l'impatto complessivo di NuGet nel computer. La cache e la cartella dei pacchetti globale sono anche molto utili quando si esegue con frequenza il ripristino di un numero più elevato di pacchetti, come in un server di compilazione. Per altri dettagli su questi meccanismi, vedere [Gestione delle cartelle dei pacchetti globali e della cache](consume-packages/managing-the-global-packages-and-cache-folders.md).

All'interno di un singolo progetto, NuGet gestisce l'intero grafico dipendenze, operazione che ancora una volta include la risoluzione di più riferimenti a versioni diverse dello stesso pacchetto. È piuttosto comune che un progetto abbia una dipendenza da uno o più pacchetti che a loro volta hanno le stesse dipendenze. Alcuni dei pacchetti di utilità più utili su nuget.org vengono usati da molti altri pacchetti. Nell'intero grafico dipendenze potrebbero facilmente esistere dieci diversi riferimenti a versioni differenti dello stesso pacchetto. Per evitare di includere più versioni dello stesso pacchetto nell'applicazione stessa, NuGet determina la singola versione utilizzabile da tutti i consumer. Per altre informazioni, vedere [Risoluzione delle dipendenze](consume-packages/dependency-resolution.md).

Oltre a ciò, NuGet gestisce tutte le specifiche relative a come sono strutturati i pacchetti (tra cui [localizzazione](create-packages/creating-localized-packages.md) e [simboli di debug](create-packages/symbol-packages.md)) e a come viene fatto riferimento a tali pacchetti (tra cui [intervalli di versione](reference/package-versioning.md#version-ranges-and-wildcards) e [versioni non definitive](create-packages/prerelease-packages.md)). NuGet offre anche varie API per l'utilizzo dei relativi servizi a livello di codice, oltre a supportare gli sviluppatori che scrivono estensioni e modelli di progetto di Visual Studio.

Dedicare alcuni minuti all'analisi del sommario di questa documentazione per vedere tutte le funzionalità presentate, insieme alle note sulla versione risalenti agli albori di NuGet.

## <a name="comments-contributions-and-issues"></a>Commenti, contributi e problemi

I commenti e i contributi a questa documentazione sono ben accetti. Basta selezionare i comandi **Feedback** e **Modifica** nella parte superiore di qualsiasi pagina oppure visitare il [repository docs](https://github.com/NuGet/docs.microsoft.com-nuget/) e l'[elenco dei problemi di docs](https://github.com/NuGet/docs.microsoft.com-nuget/issues) su GitHub.

Sono ben accetti anche i contributi a NuGet tramite i [vari repository GitHub](https://github.com/NuGet/Home). I problemi relativi a NuGet sono reperibili in [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues).

Buon divertimento con NuGet!
