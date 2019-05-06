---
title: Note sulla versione 3.2 di NuGet
description: Note sulla versione per NuGet 3.2, inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5bdd2aa5621eead9ce79794052663cc2f8a63d45
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549522"
---
# <a name="nuget-32-release-notes"></a>Note sulla versione 3.2 di NuGet

[Note sulla versione 3.2-RC di NuGet](../release-notes/nuget-3.2-RC.md) | [note sulla versione di NuGet 3.2.1](../release-notes/nuget-3.2.1.md)

NuGet 3.2 è stato rilasciato il 16 settembre 2015 come una raccolta di miglioramenti e correzioni per il 3.1.1 di rilascio ed è disponibile sia da [dist.nuget.org](http://dist.nuget.org/index.html) e il [Visual Studio Gallery](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015).

## <a name="new-features"></a>Nuove funzionalità

* I progetti che si trovano nella stessa cartella ora possono avere diversi `project.json` file nella cartella specifica di ogni progetto.  Per ogni progetto, denominare il `project.json` file `{ProjectName}.project.json` e NuGet restituirà preferenza per tale configurazione per ogni progetto in modo appropriato.  È supportata solo con gli strumenti di Windows 10 v1.1 installato - [1102](https://github.com/NuGet/Home/issues/1102)
* I client NuGet supportano la specifica di una variabile di ambiente NUGET_PACKAGES globale per specificare il percorso della cartella condivisa globale dei pacchetti usato in `project.json` progetti con la versione 1.1 gli strumenti di Windows 10 gestiti.

## <a name="command-line-updates"></a>Aggiornamenti della riga di comando

Si tratta della prima versione del client nuget.exe che supporta i server di NuGet v3 e il ripristino dei pacchetti per i progetti gestiti con un `project.json` file.

Si sono verificati alcuni problemi di feed autenticati che sono stati risolti in questa versione per migliorare le interazioni con il client.

* Installare / ripristino interazioni inviare solo le credenziali per la richiesta iniziale per i feed autenticati - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Comando di push non viene risolto le credenziali di configurazione - [1248](https://github.com/NuGet/Home/issues/1248)
* Agente utente e le intestazioni vengono ora inviate ai repository NuGet per facilitare il rilevamento delle statistiche - [929](https://github.com/NuGet/Home/issues/929)

Sono stati apportati numerosi miglioramenti per gestire meglio gli errori di rete durante il tentativo di usare un repository remoto di NuGet:

* Messaggi di errore quando non è possibile connettersi ai feed remoto - migliorati [1238](https://github.com/NuGet/Home/issues/1238)
* Comando restore di NuGet per correttamente restituisce 1 quando si verifica una condizione di errore - correggere [1186](https://github.com/NuGet/Home/issues/1186)
* A questo punto tentativi di connessione di rete ogni 200 ms per un massimo di 5 tentativi in caso di errori 5xx HTTP - [1120](https://github.com/NuGet/Home/issues/1120)
* La gestione di reindirizzamento delle risposte del server durante un comando push - migliorata [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` supporta ora l'URL o repository il nome da NuGet. config come argomento - [1046](https://github.com/NuGet/Home/issues/1046)
* I pacchetti mancanti che non risiedono in un repository durante un'operazione di ripristino vengono ora segnalati come errori anziché avvisi [1038](https://github.com/NuGet/Home/issues/1038)
* Corretta gestione multipartwebrequest di \r\n per gli scenari di Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)

Esistono una serie di correzioni per problemi con vari comandi:

* Comando di push non è più consente di eseguire un'operazione GET prima un'operazione PUT su un'origine pacchetto - [1237](https://github.com/NuGet/Home/issues/1237)
* Comando Elenca non ripete non è più numeri di versione - [1185](https://github.com/NuGet/Home/issues/1185)
* Pack argumentem-build ora correttamente supporta C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)
* Corretti problemi di tentativo di compattare un progetto F # compilate con Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)
* Ripristinare questo punto non esegue nessuna operazione quando i pacchetti sono già presenti - [1040](https://github.com/NuGet/Home/issues/1040)
* I messaggi di errore migliorato quando `packages.config` file non è valido - [1034](https://github.com/NuGet/Home/issues/1034)
* Correzione di comando di ripristino con l'opzione - SolutionDirectory per lavorare con i percorsi relativi - [992](https://github.com/NuGet/Home/issues/992)
* Comando aggiornato per supportare l'aggiornamento a livello di soluzione - migliorata [924](https://github.com/NuGet/Home/issues/924)

Un elenco completo dei problemi risolti in questa versione sono disponibili in GitHub di NuGet [attività cardine della riga di comando](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Aggiornamenti di estensione di Visual Studio

### <a name="new-features-in-visual-studio"></a>Nuove funzionalità di Visual Studio

* Una nuova voce di menu di contesto è stato aggiunto a Esplora soluzioni nel nodo della soluzione che consente ai pacchetti da ripristinare senza compilare la soluzione ([1274](https://github.com/NuGet/Home/issues/1274)).

![Nuovo 'Ripristina pacchetti' Menu di scelta rapida](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Aggiornamenti e correzioni in Visual Studio

Le correzioni per i feed autenticati erano rollup e risolti in anche l'estensione.  Gli elementi di autenticazione seguenti sono stati anche risolti nell'estensione:

* A questo punto correttamente considerando NuGet v3 i feed con autenticazione in modo corretto, anziché come versione 2 autenticato feed - [1216](https://github.com/NuGet/Home/issues/1216)
* Con correzione richiesta per le credenziali di autenticazione nei progetti che usano `project.json` e la comunicazione con i feed v2 - [1082](https://github.com/NuGet/Home/issues/1082)

Connettività di rete ha interessato l'interfaccia utente in Visual Studio e abbiamo risolto il problema con le correzioni seguenti:

* Migliorata la manutenzione della cache locale di versioni del pacchetto - [1096](https://github.com/NuGet/Home/issues/1096)
* Modificato il comportamento di un errore durante la connessione a un v3 feed non è più tentativi di considerarlo come un feed v2 - [1253](https://github.com/NuGet/Home/issues/1253)
* A questo punto prevenzione degli errori di installazione quando si installa un pacchetto con più origini dei pacchetti - [1183](https://github.com/NuGet/Home/issues/1183)

La gestione delle interazioni con operazioni di compilazione è stata migliorata:

* Ora continuare compilare progetti se il ripristino dei pacchetti per un singolo progetto ha esito negativo - [1169](https://github.com/NuGet/Home/issues/1169)
* Installazione di un pacchetto in un progetto che dipende da un altro progetto nella soluzione impone una ricompilazione di soluzione - [981](https://github.com/NuGet/Home/issues/981)
* Correggere le installazioni del pacchetto non riuscita a correttamente il rollback delle modifiche a un progetto - [1265](https://github.com/NuGet/Home/issues/1265)
* Correzione dalla rimozione accidentale del `developmentDependency` attributo su un pacchetto in `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Le chiamate a `install.ps1` disporrà di una corretta `$package.AssemblyReferences` oggetto passato - [1245](https://github.com/NuGet/Home/issues/1245)
* Non impedisce più disinstallazione dei pacchetti nei progetti UWP mentre il progetto si trova in uno stato non valido - [1128](https://github.com/NuGet/Home/issues/1128)
* Soluzioni che contengono una combinazione di `packages.config` e `project.json` progetti ora siano compilati correttamente senza richiedere una seconda operazione - di compilazione [1122](https://github.com/NuGet/Home/issues/1122)
* Corretta individuazione dei file app. config se sono collegati o che si trova in una cartella diversa - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* I progetti UWP possono ora installare i pacchetti rimossi dall'elenco - [1109](https://github.com/NuGet/Home/issues/1109)
* Ripristino del pacchetto è consentito usare mentre una soluzione non è in uno stato salvato - [1081](https://github.com/NuGet/Home/issues/1081)

Gestione degli aggiornamenti sono stati corretti i file di configurazione:

* Non è più la rimozione di un file di destinazioni recapitate da un pacchetto nelle compilazioni successive di un `project.json` progetto gestito - [1288](https://github.com/NuGet/Home/issues/1288)
* Non è più modifica dei file NuGet. config durante la compilazione di soluzioni di ASP.NET 5 - [1201](https://github.com/NuGet/Home/issues/1201)
* La modifica non è più consentita vincolo delle versioni durante l'aggiornamento del pacchetto - [1130](https://github.com/NuGet/Home/issues/1130)
* Bloccare i file rimangono ora bloccati durante la compilazione - [1127](https://github.com/NuGet/Home/issues/1127)
* È in corso `packages.config` e non doverlo riscrivere durante gli aggiornamenti - [585](https://github.com/NuGet/Home/issues/585)

Le interazioni con controllo del codice sorgente TFS sono state migliorate:

* Non è più esito negativo per i pacchetti che sono associati a TFS, le installazioni [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Interfaccia utente di NuGet corretto per consentire l'integrazione di TFS 2013 - [1071](https://github.com/NuGet/Home/issues/1071)
* Correzione di riferimenti a pacchetti ripristinati per correttamente provengono da una cartella packages - [1004](https://github.com/NuGet/Home/issues/1004)

Infine, è migliorato anche questi elementi:

* Livello di dettaglio dei messaggi di log ridotti per `project.json` gestiti i progetti - [1163](https://github.com/NuGet/Home/issues/1163)
* A questo punto visualizzare correttamente la versione installata di un pacchetto nell'interfaccia utente - [1061](https://github.com/NuGet/Home/issues/1061)
* Pacchetti con intervalli di dipendenza specificati nelle loro nuspec ora dispongono di versioni non definitive di tali dipendenze installate per una versione stabile del pacchetto - [1304](https://github.com/NuGet/Home/issues/1304)

Un elenco completo dei problemi risolti per l'estensione di Visual Studio è disponibili in GitHub di NuGet [3,2 attività cardine](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Problemi noti

Continuiamo a tenere traccia dei problemi nel nostro elenco di problemi di GitHub che può trovarsi in: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)