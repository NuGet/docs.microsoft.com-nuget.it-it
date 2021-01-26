---
title: Note sulla versione di NuGet 3,2 RC
description: Note sulla versione per NuGet 3,2 RC, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8132affb8273604ae79d4e1f85e6072d8eaf5ad6
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780288"
---
# <a name="nuget-32-rc-release-notes"></a>Note sulla versione di NuGet 3,2 RC

Note sulla versione di [NuGet 3.1.1](../release-notes/nuget-3.1.1.md)  |  [Note sulla versione di NuGet 3,2](../release-notes/nuget-3.2.md)

NuGet 3,2 Release Candidate è stato rilasciato il 2 settembre 2015 come una raccolta di miglioramenti e correzioni per la versione 3.1.1.  Inoltre, queste sono le prime versioni pubblicate prima nel nuovo repository dist.nuget.org.

## <a name="new-features"></a>Nuove funzioni e caratteristiche

* I progetti che risiedono nella stessa cartella possono ora avere `project.json` file diversi nella cartella specifica per ogni progetto.  Per ogni progetto, denominare il `project.json` file `{ProjectName}.project.json` e NuGet per fare riferimento a tale contenuto e utilizzarlo in modo appropriato per ogni progetto.  Supporta una nuova funzionalità  [1102](https://github.com/NuGet/Home/issues/1102)
* `NuGet.Config` supporta ora globalPackagesFolder come percorso relativo- [1062](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>Aggiornamenti da riga di comando

Questa è la prima versione del client nuget.exe che supporta i server NuGet V3 e il ripristino dei pacchetti per i progetti gestiti con un `project.json` file.

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>In questa versione sono stati risolti alcuni problemi relativi ai feed autenticati per migliorare le interazioni con il client.

* Le interazioni di installazione/ripristino inviano solo le credenziali per la richiesta iniziale al feed autenticato- [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Il comando push non risolve le credenziali dalla configurazione- [1248](https://github.com/NuGet/Home/issues/1248)
* Gli agenti utente e le intestazioni vengono ora inviati ai repository NuGet per semplificare il rilevamento delle statistiche- [929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>Sono stati apportati numerosi miglioramenti per gestire meglio gli errori di rete durante il tentativo di usare un repository NuGet remoto:

* Messaggi di errore migliorati quando non è possibile connettersi ai feed remoti- [1238](https://github.com/NuGet/Home/issues/1238)
* Correzione del comando di ripristino NuGet per restituire correttamente un valore 1 quando si verifica una condizione di errore- [1186](https://github.com/NuGet/Home/issues/1186)
* A questo punto, riprovare le connessioni di rete ogni 200ms per un massimo di 5 tentativi in caso di errori 5XX HTTP- [1120](https://github.com/NuGet/Home/issues/1120)
* Gestione migliorata delle risposte di reindirizzamento del server durante un comando Push- [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` supporta ora il nome dell'URL o del repository da Nuget.Config come argomento- [1046](https://github.com/NuGet/Home/issues/1046)
* I pacchetti mancanti che non si trovavano in un repository durante il ripristino vengono ora segnalati come errori invece degli avvisi [1038](https://github.com/NuGet/Home/issues/1038)
* Correzione della gestione multipartwebrequest di \r\n per scenari UNIX/Linux- [776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>Sono disponibili numerose correzioni per i problemi relativi ai vari comandi:

* Il comando push non esegue più un'operazione GET prima di un PUT su un'origine pacchetto- [1237](https://github.com/NuGet/Home/issues/1237)
* Il comando elenco non ripete più i numeri di versione- [1185](https://github.com/NuGet/Home/issues/1185)
* Pack con l'argomento-Build ora supporta correttamente C# 6,0- [1107](https://github.com/NuGet/Home/issues/1107)
* Problemi corretti durante il tentativo di comprimere un progetto F # compilato con Visual Studio 2015- [1048](https://github.com/NuGet/Home/issues/1048)
* Ripristinare ora no-Ops quando i pacchetti esistono già- [1040](https://github.com/NuGet/Home/issues/1040)
* Messaggi di errore migliorati quando il `packages.config` formato del file non è valido- [1034](https://github.com/NuGet/Home/issues/1034)
* Correzione del comando di ripristino con `-SolutionDirectory` Switch per lavorare con i percorsi relativi- [992](https://github.com/NuGet/Home/issues/992)
* Comando aggiornato migliorato per supportare l'aggiornamento a livello di soluzione- [924](https://github.com/NuGet/Home/issues/924)

Un elenco completo dei problemi risolti in questa versione è disponibile nell' [attività cardine della riga di comando](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)GitHub di NuGet.

## <a name="visual-studio-extension-updates"></a>Aggiornamenti delle estensioni di Visual Studio

### <a name="new-features-in-visual-studio"></a>Nuove funzionalità di Visual Studio

* È stata aggiunta una nuova voce di menu di scelta rapida al Esplora soluzioni sul nodo della soluzione che consente il ripristino dei pacchetti senza compilare la soluzione ([1274](https://github.com/NuGet/Home/issues/1274)).

![Nuova voce di menu di scelta rapida ' Ripristina pacchetti '](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Aggiornamenti e correzioni in Visual Studio

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>Le correzioni per i feed autenticati sono state sottoposte a rollup e risolte anche nell'estensione.  Nell'estensione sono stati inoltre risolti gli elementi di autenticazione seguenti:

* Ora è possibile trattare correttamente i feed autenticati di NuGet V3 correttamente, anziché come feed autenticati v2- [1216](https://github.com/NuGet/Home/issues/1216)
* Correzione della richiesta di credenziali di autenticazione nei progetti mediante `project.json` la comunicazione con i feed v2- [1082](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>La connettività di rete ha interessato l'interfaccia utente in Visual Studio ed è stato risolto con le correzioni seguenti:

* Miglioramento della manutenzione della cache locale delle versioni del pacchetto- [1096](https://github.com/NuGet/Home/issues/1096)
* Il comportamento dell'errore è stato modificato quando ci si connette a un feed V3 per non provare più a considerarlo come feed v2- [1253](https://github.com/NuGet/Home/issues/1253)
* Ora che impedisce errori di installazione durante l'installazione di un pacchetto con più origini pacchetti- [1183](https://github.com/NuGet/Home/issues/1183)

È stata migliorata la gestione delle interazioni con le operazioni di compilazione:

* A questo punto, continuare a compilare i progetti se il ripristino dei pacchetti per un singolo progetto non riesce- [1169](https://github.com/NuGet/Home/issues/1169)
* L'installazione di un pacchetto in un progetto che dipende da un altro progetto nella soluzione impone la ricompilazione di una soluzione- [981](https://github.com/NuGet/Home/issues/981)
* Correzione delle installazioni non riuscite per eseguire correttamente il rollback delle modifiche apportate a un progetto- [1265](https://github.com/NuGet/Home/issues/1265)
* Correzione della rimozione accidentale dell' `developmentDependency` attributo in un pacchetto in `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Le chiamate a `install.ps1` ora hanno un `$package.AssemblyReferences` oggetto appropriato passato- [1245](https://github.com/NuGet/Home/issues/1245)
* Non è più possibile impedire la disinstallazione dei pacchetti nei progetti UWP mentre il progetto è in uno stato non valido- [1128](https://github.com/NuGet/Home/issues/1128)
* Le soluzioni che contengono una combinazione di `packages.config` `project.json` progetti e sono ora compilate correttamente senza richiedere una seconda operazione di compilazione- [1122](https://github.com/NuGet/Home/issues/1122)
* Individuazione corretta dei file di app.config se sono collegati o posizionati in una cartella diversa- [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* I progetti UWP possono ora installare pacchetti non in elenco- [1109](https://github.com/NuGet/Home/issues/1109)
* Il ripristino del pacchetto è ora consentito mentre una soluzione non è in uno stato salvato- [1081](https://github.com/NuGet/Home/issues/1081)


Correzione degli aggiornamenti dei file di configurazione:

* Non è più possibile rimuovere un file di destinazioni recapitato da un pacchetto nelle compilazioni successive di un `project.json` progetto gestito- [1288](https://github.com/NuGet/Home/issues/1288)
* Non è più necessario modificare i file di Nuget.Config durante la compilazione della soluzione ASP.NET 5- [1201](https://github.com/NuGet/Home/issues/1201)
* Non è più necessario modificare il vincolo versioni consentite durante l'aggiornamento del pacchetto- [1130](https://github.com/NuGet/Home/issues/1130)
* I file di blocco ora rimangono bloccati durante la compilazione- [1127](https://github.com/NuGet/Home/issues/1127)
* A questo punto, è possibile modificarlo `packages.config` e non riscriverlo durante gli aggiornamenti- [585](https://github.com/NuGet/Home/issues/585)


Sono state migliorate le interazioni con il controllo del codice sorgente TFS:

* Non è più possibile eseguire l'installazione per i pacchetti associati a TFS- [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Correzione dell'interfaccia utente di NuGet per consentire l'integrazione di TFS 2013- [1071](https://github.com/NuGet/Home/issues/1071)
* Correzione dei riferimenti ai pacchetti ripristinati correttamente da una cartella Pacchetti- [1004](https://github.com/NuGet/Home/issues/1004)

Infine, sono stati migliorati anche gli elementi seguenti:

* Livello di dettaglio dei messaggi di log ridotti per i `project.json` progetti gestiti- [1163](https://github.com/NuGet/Home/issues/1163)
* Visualizzazione corretta della versione installata di un pacchetto nell'interfaccia utente- [1061](https://github.com/NuGet/Home/issues/1061)


Un elenco completo dei problemi risolti per l'estensione di Visual Studio è reperibile nell' [attività cardine](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2) di GitHub 3,2 di NuGet

## <a name="known-issues"></a>Problemi noti

Continuiamo a tenere traccia dei problemi nell'elenco dei problemi di GitHub disponibili all'indirizzo: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)