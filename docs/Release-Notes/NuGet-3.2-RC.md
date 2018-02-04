---
title: Note sulla versione RC NuGet 3.2 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per NuGet 3.2 RC inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "NuGet 3.2 RC note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b19f62217ed79689ce067107dd64dfffe2c59291
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-32-rc-release-notes"></a>Note sulla versione RC NuGet 3.2

[Note sulla versione di NuGet 3.1.1](../release-notes/nuget-3.1.1.md) | [note sulla versione 3.2 NuGet](../release-notes/nuget-3.2.md)

3.2 NuGet versione finale candidata è stata rilasciata il 2 settembre 2015 come una raccolta di miglioramenti e correzioni per il 3.1.1 rilasciare.  Inoltre, sono le versioni prima che vengono pubblicate innanzitutto il nuovo repository dist.nuget.org.

## <a name="new-features"></a>Nuove funzionalità

* Progetti che risiedono nella stessa cartella ora possono avere diverse `project.json` file contenuti nella cartella specifica per ogni progetto.  Per ogni progetto, denominare il `project.json` file `{ProjectName}.project.json` e NuGet correttamente farà riferimento e usare tale contenuto per ogni progetto in modo appropriato.  Supporta una nuova funzionalità [1102](https://github.com/NuGet/Home/issues/1102)
* `NuGet.Config`supporta ora un oggetto globalPackagesFolder come percorso relativo - [1062](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>Aggiornamenti della riga di comando

Si tratta della prima versione del client che supporta i server NuGet in v3 nuget.exe e ripristino dei pacchetti per i progetti gestiti con un `project.json` file.

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>Si sono verificati alcuni problemi feed autenticati che sono stati risolti in questa versione per migliorare le interazioni con il client.

* Installare / ripristino interazioni inviare solo le credenziali per la richiesta iniziale per il feed autenticato - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Comando push non risolve le credenziali da configurazione - [1248](https://github.com/NuGet/Home/issues/1248)
* Agente utente e le intestazioni vengono ora inviate per i repository NuGet per semplificare il rilevamento di statistiche - [929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>Sono stati apportati numerosi miglioramenti per ottimizzare la gestione degli errori di rete durante il tentativo di usare un repository NuGet remoto:

* Migliorati i messaggi di errore quando non è possibile connettersi a feed remoto - [1238](https://github.com/NuGet/Home/issues/1238)
* Correzione di comando di ripristino NuGet correttamente restituire 1 quando si verifica una condizione di errore - [1186](https://github.com/NuGet/Home/issues/1186)
* Ora tentativi di connessione di rete ogni 200 ms per un massimo di 5 tentativi in caso di errori HTTP 5xx - [1120](https://github.com/NuGet/Home/issues/1120)
* La gestione di reindirizzamento delle risposte del server durante un comando push - migliorata [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source`supporta ora l'URL o repository nome da NuGet. config come argomento - [1046](https://github.com/NuGet/Home/issues/1046)
* I pacchetti mancanti che non risiedono in un repository durante un ripristino a questo punto vengono segnalati come errori anziché avvisi [1038](https://github.com/NuGet/Home/issues/1038)
* Correzione gestione multipartwebrequest di \r\n per gli scenari di Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>Esistono numerose correzioni a problemi relativi a vari comandi di:

* Comando push non esegue più una richiesta GET prima di un'operazione PUT su un'origine pacchetto - [1237](https://github.com/NuGet/Home/issues/1237)
* Comando di elenco non ripete non è più numeri di versione - [1185](https://github.com/NuGet/Home/issues/1185)
* Pack con il parametro - argomento compilazione ora correttamente supporta c# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)
* Problemi corretti tentativo di compattare un progetto F # compilata con Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)
* Ripristina ora no-ops quando i pacchetti sono già presenti - [1040](https://github.com/NuGet/Home/issues/1040)
* I messaggi di errore migliorati quando `packages.config` file non è valido - [1034](https://github.com/NuGet/Home/issues/1034)
* Il comando restore con correzione `-SolutionDirectory` commutatore per lavorare con i percorsi relativi - [992](https://github.com/NuGet/Home/issues/992)
* Comando aggiornato per supportare l'aggiornamento a livello di soluzione - migliorata [924](https://github.com/NuGet/Home/issues/924)

Un elenco completo dei problemi descritti in questa versione è reperibile in NuGet GitHub [attività cardine della riga di comando](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Aggiornamenti di estensione di Visual Studio

### <a name="new-features-in-visual-studio"></a>Nuove funzionalità in Visual Studio

* Una nuova voce di menu di contesto è stato aggiunto a Esplora soluzioni nel nodo della soluzione che consente ai pacchetti di essere ripristinato senza compilare la soluzione ([1274](https://github.com/NuGet/Home/issues/1274)).

![Nuovo 'Restore pacchetti' contesto voce di Menu](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Aggiornamenti e correzioni in Visual Studio

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>Le correzioni per i feed autenticati erano rollup e risolti in nonché l'estensione.  I seguenti elementi di autenticazione sono stati anche risolti nell'estensione:

* Ora correttamente considerarli NuGet v3 autenticato correttamente, i feed invece che come v2 autenticato feed - [1216](https://github.com/NuGet/Home/issues/1216)
* Richiesta corretto per le credenziali di autenticazione nei progetti utilizzando `project.json` e la comunicazione con il feed v2 - [1082](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>Connettività di rete ha interessato l'interfaccia utente in Visual Studio e viene risolto il problema con le correzioni seguenti:

* Migliorare la manutenzione della cache locale di versioni del pacchetto - [1096](https://github.com/NuGet/Home/issues/1096)
* Modificato il comportamento di un errore durante la connessione a un v3 feed non tenta di considerarlo come un feed v2 - [1253](https://github.com/NuGet/Home/issues/1253)
* Ora prevenzione degli errori di installazione quando si installa un pacchetto con più origini pacchetto - [1183](https://github.com/NuGet/Home/issues/1183)

La gestione delle interazioni con operazioni di compilazione è stata migliorata:

* Ora continuare compilare progetti se il ripristino dei pacchetti per un singolo progetto ha esito negativo - [1169](https://github.com/NuGet/Home/issues/1169)
* Installa un pacchetto in un progetto che dipende da un altro progetto nella soluzione impone una ricompilazione della soluzione - [981](https://github.com/NuGet/Home/issues/981)
* Correzione Installa pacchetto non riuscito per correttamente il rollback delle modifiche a un progetto - [1265](https://github.com/NuGet/Home/issues/1265)
* La rimozione accidentale di correzione di `developmentDependency` attributo in un pacchetto in `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Le chiamate a `install.ps1` dispone di una corretta `$package.AssemblyReferences` oggetto passato - [1245](https://github.com/NuGet/Home/issues/1245)
* Non impedisce più disinstallazione dei pacchetti in progetti UWP mentre il progetto è in uno stato non valido - [1128](https://github.com/NuGet/Home/issues/1128)
* Soluzioni che contengono una combinazione di `packages.config` e `project.json` progetti ora vengono compilati correttamente senza una seconda - operazione di compilazione [1122](https://github.com/NuGet/Home/issues/1122)
* Individuazione correttamente il file app. config se sono collegate o si trova in una cartella diversa - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Progetti UWP ora possono installare i pacchetti - [1109](https://github.com/NuGet/Home/issues/1109)
* Ripristino del pacchetto è ora consentito mentre una soluzione non è in uno stato salvato - [1081](https://github.com/NuGet/Home/issues/1081)


Gestione degli aggiornamenti sono stati corretti i file di configurazione:

* Non è più la rimozione di un file targets recapitati da un pacchetto le compilazioni successive di un `project.json` progetto gestito - [1288](https://github.com/NuGet/Home/issues/1288)
* Non modifica i file NuGet. config durante la compilazione di soluzioni di ASP.NET 5 - [1201](https://github.com/NuGet/Home/issues/1201)
* Non modifica non è più consentito vincolo versioni durante l'aggiornamento del pacchetto - [1130](https://github.com/NuGet/Home/issues/1130)
* File di blocco rimangono ora bloccati durante la compilazione - [1127](https://github.com/NuGet/Home/issues/1127)
* Ora modifica `packages.config` e non la riscrittura durante gli aggiornamenti - [585](https://github.com/NuGet/Home/issues/585)


Vengono aggiornate le interazioni con controllo del codice sorgente TFS:

* Non è più in mancanza di installazioni per i pacchetti che sono associati a TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Interfaccia utente di NuGet corretto per consentire l'integrazione di TFS 2013 - [1071](https://github.com/NuGet/Home/issues/1071)
* Correggere i riferimenti ai pacchetti ripristinati per correttamente provengono da una cartella di pacchetti - [1004](https://github.com/NuGet/Home/issues/1004)

Infine, è migliorata anche questi elementi:

* Livello di dettaglio dei messaggi di log ridotte per `project.json` gestiti progetti - [1163](https://github.com/NuGet/Home/issues/1163)
* Ora visualizzare correttamente la versione installata di un pacchetto nell'interfaccia utente - [1061](https://github.com/NuGet/Home/issues/1061)


Un elenco completo dei problemi descritti per l'estensione di Visual Studio è disponibile in NuGet GitHub [3.2 attività cardine](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Problemi noti

Continuiamo a tenere traccia dei problemi nell'elenco di problemi di GitHub in cui è reperibile in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)