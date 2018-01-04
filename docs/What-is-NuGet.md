---
title: "Che cos'è NuGet e cosa fa? | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/26/2017
ms.topic: hero-article
ms.prod: nuget
ms.technology: 
ms.assetid: c3faf278-4cbf-4733-96f6-9ee9f7203af9
description: "Un'introduzione completa a che cos'è NuGet e cosa fa."
keywords: Gestione pacchetti NuGet, utilizzo, creazione di pacchetti, hosting di pacchetti
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 29dcedf33a54e249fe0b6acf588e4aafde28304f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="an-introduction-to-nuget"></a>Introduzione a NuGet

Uno strumento essenziale per qualsiasi piattaforma di sviluppo moderna è un meccanismo attraverso il quale gli sviluppatori possono creare, condividere e utilizzare utili librerie di codice. Tali librerie sono in genere definite "pacchetti", perché possono contenere codice compilato (sotto forma di DLL) insieme ad altro contenuto che potrebbe essere necessario nei progetti che utilizzano tali librerie.

Per .NET, il meccanismo per la condivisione del codice è **NuGet**, che definisce in che modo vengono creati, ospitati e utilizzati i pacchetti per .NET e fornisce gli strumenti per ognuno di questi ruoli. 

In altri termini, un pacchetto NuGet è un singolo file ZIP con l'estensione `.nupkg` che contiene codice compilato (DLL), altri file correlati a tale codice e un manifesto descrittivo che include informazioni come il numero di versione del pacchetto. Gli sviluppatori di librerie creano i file di pacchetto e li pubblicano in un host. I consumer di pacchetti ricevono tali pacchetti, li aggiungono ai loro progetti e quindi chiamano le funzionalità di tale libreria nel codice dei progetti. NuGet gestisce tutti i dettagli intermedi.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Flusso dei pacchetti tra autori, host e consumer

Nel proprio ruolo di host, NuGet gestisce il repository centrale di più di 60.000 pacchetti univoci disponibili pubblicamente su [nuget.org](https://www.nuget.org). Questi pacchetti vengono usati da milioni di sviluppatori .NET ogni giorno. NuGet consente anche di ospitare i pacchetti in modo privato nel cloud, in una rete privata o anche solo nel file system locale. In questo modo, i pacchetti sono disponibili solo per gli sviluppatori all'interno di una particolare organizzazione o gruppo di clienti. Le opzioni sono illustrate in [Hosting dei feed NuGet](Hosting-Packages/Overview.md).

Qualunque sia la sua natura, un host funge da punto di connessione tra gli *autori* e i *consumer* dei pacchetti. Gli autori compilano utili pacchetti NuGet e li pubblicano in un host. I consumer cercano quindi i pacchetti utili e compatibili negli host accessibili, scaricandoli e includendoli nei loro progetti. Una volta installate in un progetto, le API dei pacchetti sono disponibili per il resto del codice del progetto.

![Relazione tra autori, host e consumer dei pacchetti](media/nuget-roles.png)

In questo caso, un pacchetto "compatibile" significa che contiene gli assembly compilati per almeno un framework .NET di destinazione compatibile con il framework di destinazione del progetto che lo utilizza. Per rendere un pacchetto ampiamente compatibile, l'autore compila assembly distinti per diversi framework di destinazione e li include tutti nello stesso pacchetto. Quando un consumer installa il pacchetto, NuGet estrae solo gli assembly necessari per il progetto. Ciò contribuisce a ridurre al minimo il footprint del pacchetto nell'applicazione finale e/o gli assembly generati da tale progetto.

## <a name="nuget-tools"></a>Strumenti NuGet

Oltre a ospitare il supporto, NuGet fornisce anche un'ampia gamma di strumenti usati da autori e consumer:

| Strumento | Piattaforme | Scenari possibili | Descrizione |
| --- | --- | --- | --- |
| [Interfaccia della riga di comando di nuget.exe](Tools/nuget-exe-CLI-Reference.md) | Tutti | Creazione, utilizzo | Fornisce tutte le funzionalità di NuGet, con alcuni comandi applicabili in modo specifico agli autori dei pacchetti, altri applicabili solo ai consumer e altri ancora applicabili a entrambi. Ad esempio, gli autori dei pacchetti usano il comando `nuget pack` per creare un pacchetto da vari assembly e file correlati, i consumer dei pacchetti usano `nuget install` per includere i pacchetti in un progetto e tutti gli utenti usano `nuget config` per impostare le variabili di configurazione di NuGet.  |
| [Interfaccia utente di Gestione pacchetti](Tools/Package-Manager-UI.md) | Visual Studio su Windows | Utilizzo | Fornisce un'interfaccia utente di semplice utilizzo per l'installazione e la gestione dei pacchetti nei progetti .NET. | 
| [Interfaccia utente di Gestisci pacchetti NuGet](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough) | Visual Studio per Mac | Utilizzo | Fornisce un'interfaccia utente di semplice utilizzo per l'installazione e la gestione dei pacchetti nei progetti .NET. |
| [Console di Gestione pacchetti](Tools/Package-Manager-Console.md) | Visual Studio su Windows | Utilizzo | Fornisce i [comandi di PowerShell](Tools/Powershell-Reference.md) per l'installazione e la gestione dei pacchetti nei progetti .NET. | 
| [Interfaccia della riga di comando di dotnet](Tools/dotnet-Commands.md) | Tutti | Creazione, utilizzo | Fornisce determinate funzionalità dell'interfaccia della riga di comando di NuGet direttamente all'interno della toolchain di .NET Core. |
| [MSBuild](Schema/msbuild-targets.md) | Windows | Creazione, utilizzo | Fornisce la possibilità di creare pacchetti e ripristinare quelli usati in un progetto direttamente tramite la toolchain di MSBuild. |

Come si può notare, gli strumenti con cui si usa NuGet variano notevolmente in base al fatto che si stiano creando (e pubblicando) pacchetti o si stiano semplicemente utilizzando, oltre che in base alla piattaforma in uso. Informazioni più dettagliate sono disponibili negli argomenti [Flusso di lavoro della creazione di pacchetti](Create-Packages/Overview-and-Workflow.md) e [Flusso di lavoro dell'utilizzo di pacchetti](Consume-Packages/Overview-and-Workflow.md), oltre che in altri argomenti di quelle sezioni. 

Gli autori dei pacchetti in genere sono anche consumer, dal momento che compilano sulla base di funzionalità disponibili in altri pacchetti NuGet. E tali pacchetti, naturalmente, possono dipendere a loro volta da altri.

## <a name="managing-dependencies"></a>Gestione delle dipendenze

La possibilità di compilare facilmente sulla base del lavoro di altri utenti è uno degli aspetti che determina l'efficacia di un sistema di gestione pacchetti. Di conseguenza, la maggior parte delle operazioni eseguite da NuGet è correlata alla gestione di tale albero delle dipendenze, o "grafico", per conto del progetto in uso. Detto in parole più semplici, sarà necessario preoccuparsi solo dei pacchetti che si usano direttamente in un progetto. Se uno di questi pacchetti utilizza altri pacchetti (che possono a loro volta utilizzare pacchetti), NuGet si occupa di tutte queste dipendenze di livello inferiore.

La figura seguente mostra un progetto che dipende da cinque pacchetti, che a loro volta dipendono da un numero di altri pacchetti.  

![Esempio di grafico dipendenze di NuGet per un progetto .NET](media/dependency-graph.png)

Si noti che alcuni pacchetti compaiono più volte nel grafico dipendenze. Ad esempio, sono visibili tre diversi consumer del pacchetto B e ogni consumer potrebbe anche specificare una versione diversa per tale pacchetto (non riportato nella figura). Poiché si tratta di una situazione comune, fortunatamente NuGet esegue tutte le operazioni necessarie per determinare esattamente quale versione del pacchetto B soddisfi tutti i relativi consumer. Quindi NuGet fa lo stesso per tutti gli altri pacchetti, indipendentemente dal livello di profondità del grafico dipendenze.

Per maggiori dettagli sul funzionamento di questo servizio in NuGet, vedere [Risoluzione delle dipendenze](Consume-Packages/Dependency-Resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Rilevamento dei riferimenti e ripristino dei pacchetti

Dal momento che i progetti possono passare facilmente tra computer degli sviluppatori, repository del controllo del codice sorgente, server di compilazione e così via, è estremamente poco pratico mantenere gli assembly binari dei pacchetti NuGet associati direttamente a un progetto. Ciò non solo causerebbe inutilmente un aumento eccessivo di ogni copia del progetto (comportando di conseguenza uno spreco di spazio nel repository del controllo del codice sorgente), ma renderebbe anche estremamente difficile aggiornare i file binari dei pacchetti a versioni più recenti, dal momento che tale operazione dovrebbe essere eseguita in tutte le copie del progetto. 

Al contrario, NuGet mantiene semplicemente un elenco dei riferimenti dei pacchetti da cui dipende un progetto (incluse le dipendenze di livello superiore e inferiore) e fornisce gli strumenti per ripristinare tutti i pacchetti con riferimenti su richiesta come descritto in [Ripristino di pacchetti](Consume-Packages/Package-Restore.md). Ovvero, quando si installa un pacchetto da un host in un progetto, NuGet registra l'identificatore del pacchetto e il numero di versione in questo elenco di riferimenti. La disinstallazione di un pacchetto, naturalmente, ne comporta la rimozione dall'elenco. 

![Nell'installazione del pacchetto viene creato un elenco di riferimenti NuGet che può essere usato per ripristinare i pacchetti in un'altra posizione.](media/nuget-restore.png)

Con solo questo elenco di riferimenti, NuGet potrà quindi reinstallare, ovvero ripristinare, successivamente tutti questi pacchetti da host pubblici e/o privati. Per questo motivo, nuget.org non consente l'eliminazione permanente dei pacchetti pubblicati, anche se possono essere nascosti; vedere [Eliminazione di pacchetti](Policies/deleting-packages.md). Quando si esegue il commit di un progetto in un controllo del codice sorgente o lo si condivide in qualsiasi altro modo, è necessario includere solo l'elenco dei riferimenti e non occorre includere eventuali file binari dei pacchetti (vedere [Pacchetti e controllo del codice sorgente](Consume-Packages/Packages-and-Source-Control.md)).

Il computer che riceve un progetto, ad esempio un server di compilazione che ottiene una copia del progetto come parte di un sistema di distribuzione automatica, chiede semplicemente a NuGet di ripristinare le dipendenze ogni volta che sono necessarie. Sistemi di compilazione come Visual Studio Team Services forniscono passaggi di "ripristino NuGet" per questo esatto scopo. Analogamente, quando gli sviluppatori ottengono una copia di un progetto (ad esempio durante la clonazione di un repository) e quindi aprono il progetto in Visual Studio ed eseguono una compilazione, Visual Studio ripristina automaticamente i pacchetti NuGet necessari. Gli sviluppatori possono anche specificare a NuGet di ripristinare i pacchetti in qualsiasi momento usando il comando dell'interfaccia della riga di comando `nuget restore` o il cmdlet `Install-Package` nella console di Gestione pacchetti.

Chiaramente, quindi, il ruolo primario di NuGet in cui gli sviluppatori sono coinvolti è la gestione di tale elenco di riferimenti per conto del progetto e la disponibilità di strumenti per ripristinare (e aggiornare) in modo efficiente tali pacchetti con riferimenti.

La modalità esatta di esecuzione di questa operazione si è evoluta nelle diverse versioni di NuGet, comportando diversi *formati di gestione dei pacchetti*, come vengono chiamati:

- [`packages.config`](Schema/packages-config.md): *(NuGet 1.0+)* File XML che gestisce un elenco completo di tutte le dipendenze nel progetto, incluse le dipendenze di altri pacchetti installati. 
- [`project.json`](Schema/project-json.md): *(NuGet 3.0+)* File JSON che gestisce un elenco delle dipendenze del progetto con un grafico di pacchetto complessivo in un file associato, `project.lock.json`. Questa struttura offre prestazioni migliori rispetto a `packages.config` come descritto in [Risoluzione delle dipendenze](Consume-Packages/Dependency-Resolution.md), incluso il ripristino transitivo, ma è stata generalmente sostituita da PackageReference, illustrato di seguito.
- [Riferimenti ai pacchetti nei file di progetto](Consume-Packages/Package-References-in-Project-Files.md) (noti anche come "PackageReference") | *(NuGet 4.0+)* Gestisce un elenco di dipendenze di livello superiore del progetto direttamente all'interno del file di progetto, pertanto non sono necessari file separati. Un file associato, `project.assets.json`, viene generato dinamicamente come `project.lock.json` per gestire il grafico dipendenze complessivo.

Il formato di gestione dei pacchetti usato in un determinato progetto dipende dal tipo di progetto e dalla versione di Visual Studio e NuGet disponibile. Per verificare il formato in uso, è sufficiente cercare `packages.config` o `project.json` nella radice del progetto dopo l'installazione del primo pacchetto. Se non viene visualizzato alcun file, cercare direttamente nel file di progetto un elemento &lt;PackageReference&gt;.

In Visual Studio 2017, ad esempio, la maggior parte dei tipi di progetto usa `packages.config`, ad eccezione dei progetti UWP in C# e .NET Core che usano PackageReference. 

## <a name="what-else-does-nuget-do"></a>Che cos'altro fa NuGet?

Per riepilogare gli argomenti trattati finora, NuGet fornisce (nel suo ruolo di host) il repository nuget.org centrale e supporta l'hosting privato. NuGet offre gli strumenti di cui gli sviluppatori hanno bisogno per creare, pubblicare e utilizzare i pacchetti. E cosa ancora più importante, NuGet gestisce un elenco dei riferimenti dei pacchetti usati in un progetto, consentendo di ripristinare e aggiornare i pacchetti da tale elenco.

Per assicurare l'efficienza di questi processi, NuGet esegue alcune ottimizzazioni in background. In particolare, NuGet gestisce cache dei pacchetti sia a livello di computer che specifiche dei progetti per l'installazione e la reinstallazione rapide. In caso di cache a livello di computer, i pacchetti scaricati e installati in un progetto vengono archiviati nella cache, in modo che l'installazione dello stesso pacchetto in un altro progetto non richieda nuovamente il download. Questa funzionalità è chiaramente molto utile quando si esegue con frequenza il ripristino di un numero più elevato di pacchetti, come in un server di compilazione. Per maggiori dettagli sul meccanismo e su come usarlo, vedere [Gestione delle cache NuGet](Consume-Packages/Managing-the-Nuget-Cache.md).

All'interno di un singolo progetto NuGet svolge buona parte del lavoro per gestire il grafico dipendenze complessivo (quando si usa `project.json` o &lt;PackageReference&gt;, NuGet conserva queste informazioni in un file secondario chiamato `project.lock.json` e `project.assets.json`, rispettivamente). Ciò include ancora una volta la risoluzione di più riferimenti a diverse versioni dello stesso pacchetto.

Ovvero, è piuttosto comune che un progetto abbia una dipendenza da uno o più pacchetti che a loro volta hanno le stesse dipendenze. Ad esempio, alcuni dei pacchetti di utilità più utili su nuget.org vengono usati da molti altri pacchetti. Nell'intero grafico dipendenze si potrebbe facilmente disporre di dieci diversi riferimenti a versioni differenti dello stesso pacchetto. Tuttavia, non è consigliabile includere più versioni di tale pacchetto nell'applicazione stessa, pertanto NuGet determina la singola versione che tutti possono usare (vedere [Risoluzione delle dipendenze](Consume-Packages/Dependency-Resolution.md) per altre informazioni su questo argomento).

Oltre a ciò, NuGet gestisce tutte le specifiche relative a come sono strutturati i pacchetti (tra cui [localizzazione](Create-Packages/Creating-Localized-Packages.md) e [simboli di debug](Create-Packages/Symbol-Packages.md)) e a come viene fatto riferimento a tali pacchetti (tra cui [intervalli di versione](reference/package-versioning.md#version-ranges-and-wildcards) e [versioni non definitive](create-packages/Prerelease-Packages.md)). NuGet fornisce inoltre le API per i provider di credenziali (per l'accesso a host privati) e per gli sviluppatori che scrivono modelli di progetti ed estensioni di Visual Studio.

Dedicare alcuni minuti all'analisi del sommario di questa documentazione: si ritroveranno tutte le funzionalità presentate in questo articolo, insieme alle note sulla versione risalenti agli albori di NuGet.

## <a name="comments-contributions-and-issues"></a>Commenti, contributi e problemi

I commenti e i contributi a questa documentazione sono ben accetti. Basta selezionare i comandi **Commenti** e **Modifica** in qualsiasi pagina oppure visitare il [repository docs](https://github.com/NuGet/docs.microsoft.com-nuget/) e l'[elenco dei problemi docs](https://github.com/NuGet/docs.microsoft.com-nuget/issues) su GitHub.

Sono ben accetti anche i contributi a NuGet tramite i [vari repository GitHub](https://github.com/NuGet/Home); i problemi relativi a NuGet sono reperibili in [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues).

Buon divertimento con NuGet!
