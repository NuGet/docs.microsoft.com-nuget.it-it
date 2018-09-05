---
title: Note sulla versione di NuGet 1.0 e 1.1
description: Note sulla versione per NuGet 1.1 inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6222a996f2fdcaaa81a1b16d1c6da2749936712a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547021"
---
# <a name="nuget-10-and-11-release-notes"></a>Note sulla versione di NuGet 1.0 e 1.1

[Note sulla versione 1.2 di NuGet](../release-notes/nuget-1.2.md)

NuGet 1.0 è stato rilasciato il 13 gennaio 2011.  NuGet 1.1 è stato rilasciato il 12 febbraio 2011.

## <a name="overview"></a>Panoramica

Questo documento contiene le note sulla versione per le diverse versioni di NuGet 1.0 raggruppati in base alla versione di anteprima principali.

NuGet include i componenti seguenti:

* *NuGet.Tools.vsix* * costituito da:
  * **Aggiungi finestra di dialogo pacchetto libreria** * finestra di dialogo di Visual Studio consente di sfogliare e installare i pacchetti.
  * **Console di gestione pacchetti** * console all'interno di Visual Studio basati su Powershell.
* *Strumento da riga di comando NuGet* * lo strumento consente di creare (e verrà pubblicato) i pacchetti.

NuGet gli strumenti di Visual Studio Extension (*NuGet.Tools.vsix*) richiede:

* Visual Studio 2010 o Visual Web Developer 2010 Express.

Lo strumento da riga di comando NuGet richiede:

* Versione di .NET framework 4

## <a name="installation"></a>Installazione

Per utilizzare questo oggetto [versione più recente](http://nuget.codeplex.com/releases/view/52018):

* Disinstallare prima la compilazione precedente. È necessario eseguire Visual Studio come amministratore per eseguire questa operazione.
* Rimuovere tutti i feed esistenti che è necessario.
* Aggiungere un nuovo feed che punta al [ http://go.microsoft.com/fwlink/?LinkId=206669 ](http://go.microsoft.com/fwlink/?LinkId=206669).

## <a name="nuget-11"></a>NuGet 1.1

L'elenco dei problemi risolti in questa versione [sono disponibili qui](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

È stato risolto un problema per la versione RTM dopo la versione RC.

* [Problema 474: Rimozione di pacchetti interessati tutti i progetti nella soluzione](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Versione finale candidata

Di seguito sono le modifiche apportate in questa versione finale candidata dopo CTP 2. Visitare Issue Tracker per visualizzare l'elenco completo dei bug.

* [Aggiornamento del pacchetto dalla Console non vengono aggiornate le dipendenze.](http://nuget.codeplex.com/workitem/443)
* [Aggiunta pacchetto preleva bin del pacchetto non riferimento (CTP1)](http://nuget.codeplex.com/workitem/442)
* [Aggiorna un pacchetto lascia ai riferimenti interrotti](http://nuget.codeplex.com/workitem/440)
* [Get-Package-aggiornamenti ha esito negativo nella finestra di dialogo o quando viene selezionata l'origine 'Tutti' aggregata nella console di](http://nuget.codeplex.com/workitem/439)
* [Recupero di errori di verifica del pacchetto](http://nuget.codeplex.com/workitem/426)
* [Avvisare gli utenti quando un pacchetto non può essere installato nella finestra di dialogo pacchetto aggiungere](http://nuget.codeplex.com/workitem/425)
* [Get-Package-Aggiorna genera un'eccezione durante l'aggiornamento di un numero elevato di pacchetti](http://nuget.codeplex.com/workitem/424)
* [Migliorare la gestione degli errori quando i file nuspec vengono creati in modo non corretto](http://nuget.codeplex.com/workitem/423)
* [Pacchetto NuGet ignora i file specificati](http://nuget.codeplex.com/workitem/422)
* [Rimuovendo l'origine del pacchetto secondo all'ultima e quindi facendo clic su "Sposta giù" arresto anomalo di Visual Studio](http://nuget.codeplex.com/workitem/418)
* [Rimuovi riferimento all'assembly durante l'installazione dei pacchetti](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException quando si apre una finestra di dialogo Impostazioni](http://nuget.codeplex.com/workitem/411)
* [Chiave di accesso per l'origine del pacchetto nella Console di gestione pacchetti non funziona](http://nuget.codeplex.com/workitem/410)
* [Chiavi di accesso di NuGet, Visual Studio le impostazioni della finestra di attivare i campi non corretti](http://nuget.codeplex.com/workitem/409)
* [Intellisense ID pacchetto non deve eseguire una query troppi elementi](http://nuget.codeplex.com/workitem/404)
* [Errore durante l'aggiunta del pacchetto al progetto con un carattere punto nel nome del progetto](http://nuget.codeplex.com/workitem/403)
* [Problema con i file specificati nel file nuspec](http://nuget.codeplex.com/workitem/400)
* [Feed ufficiali corretto deve ottenere registrato quando si usano build più recente](http://nuget.codeplex.com/workitem/399)
* [I tag devono usare spazi anziché &](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata mancano alcune informazioni utili](http://nuget.codeplex.com/workitem/388)
* [Aggiungi collegamento alla finestra di dialogo](http://nuget.codeplex.com/workitem/386)
* [Uso di App_Data per decomprimere le interruzioni di pacchetti in Visual Studio](http://nuget.codeplex.com/workitem/380)
* [Implementare i tag](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder consente a un pacchetto vuoto senza dipendenze da creare](http://nuget.codeplex.com/workitem/373)
* [Aggiungere il campo di proprietari per il pacchetto](http://nuget.codeplex.com/workitem/365)
* [Aggiornare il manifesto VSIX, ad esempio, Gestione pacchetti NuGet invece gli strumenti di VSIX](http://nuget.codeplex.com/workitem/364)
* [Comando Get-Package genera l'errore quando viene selezionato tutto il codice sorgente](http://nuget.codeplex.com/workitem/359)
* [Consente l'ordinamento delle origini dei pacchetti nella finestra di dialogo Opzioni](http://nuget.codeplex.com/workitem/356)
* [Pacchetto di aggiornamento non comporta la rimozione versione meno recente](http://nuget.codeplex.com/workitem/352)
* [Specifica di intervallo di versioni di implementare le dipendenze](http://nuget.codeplex.com/workitem/347)
* [Visual Studio si blocca quando si fa clic "Aggiungi nuovo pacchetto"](http://nuget.codeplex.com/workitem/346)
* [Visualizzare le classificazioni e i download nella finestra di dialogo Aggiungi pacchetto](http://nuget.codeplex.com/workitem/345)
* [Modifica tra origini dei pacchetti nella finestra di dialogo non viene aggiornata origine attiva](http://nuget.codeplex.com/workitem/344)
* [Rimuovere i tasti di scelta rapida per la finestra della Console di gestione pacchetti](http://nuget.codeplex.com/workitem/339)
* [Pacchetto di installazione non è riconosciuto come nome di un cmdlet di...](http://nuget.codeplex.com/workitem/338)
* [Installazione di un pacchetto da un feed le dipendenze in un feed regolare locale non sono stati risolti](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies deve ignorare le dipendenze che sono ancora in uso](http://nuget.codeplex.com/workitem/331)
* [Se l'annullamento navigazione tra le pagine, utente non è possibile passare a una pagina diversa mentre la richiesta della pagina originale restituisce](http://nuget.codeplex.com/workitem/325)
* [Analizzare le prestazioni di NuPack.Server per servire i feed con numero elevato di pacchetti.](http://nuget.codeplex.com/workitem/324)
* [La seconda volta che filtrare per un pacchetto Usa l'origine del pacchetto "Nuovo", anziché l'origine selezionata in precedenza.](http://nuget.codeplex.com/workitem/321)
* [Origine del pacchetto predefinito deve essere selezionata quando si seleziona la scheda "Online" nella finestra di dialogo.](http://nuget.codeplex.com/workitem/320)
* [Elenco-Package deve visualizzare i pacchetti installati per impostazione predefinita](http://nuget.codeplex.com/workitem/309)
* [HintPaths riferimento assembly](http://nuget.codeplex.com/workitem/294)
* [Eccezione durante l'apertura della Console di gestione pacchetti](http://nuget.codeplex.com/workitem/268)
* [Download di console intellisense intero feed](http://nuget.codeplex.com/workitem/259)
* [Origine del pacchetto 'Default' deve essere rinominato in 'Active'](http://nuget.codeplex.com/workitem/258)
* [Le origini pacchetto dell'interfaccia utente: fare clic su OK deve essere aggiunta la nuova origine i campi di origine/nome risultano non vuote](http://nuget.codeplex.com/workitem/257)
* [Finestra di dialogo diventa molto lento quando il numero di pacchetti installati è di grandi dimensioni](http://nuget.codeplex.com/workitem/243)
* [Supporto di reindirizzamenti di Binding per assembly con nome sicuro](http://nuget.codeplex.com/workitem/238)
* [Aggiungi riferimento al pacchetto... Interfaccia utente da includere drop down per origine pacchetto](http://nuget.codeplex.com/workitem/226)
* [NuPack deve supportare la trasformazione di configurazione agnostically del nome del file di configurazione](http://nuget.codeplex.com/workitem/224)
* [Consente l'oggetto BasePath per eseguire l'override in NuPack.exe](http://nuget.codeplex.com/workitem/222)
* [Comportamento di Fallback origine pacchetto](http://nuget.codeplex.com/workitem/204)
* [Arresto anomalo nella GUI](http://nuget.codeplex.com/workitem/201)
* [Aggiungi l'ordinamento delle opzioni di finestra di dialogo Aggiungi pacchetto](http://nuget.codeplex.com/workitem/179)
* [tasto di scelta rapida per chiudere la Console di gestione pacchetti](http://nuget.codeplex.com/workitem/174)
* [PowerConsole provoca NuPack Console esito negativo](http://nuget.codeplex.com/workitem/166)
* [Console e finestra di dialogo Aggiungi pacchetto deve impostare l'agente utente nelle richieste](http://nuget.codeplex.com/workitem/141)
* [Impostare il numero di versione del progetto VSIX e NuPack.exe nella compilazione.](http://nuget.codeplex.com/workitem/134)
* [Nascondere parametri PowerShell comuni da-?](http://nuget.codeplex.com/workitem/118)
* [Add - una Guida dettagliata per i comandi della console](http://nuget.codeplex.com/workitem/110)
* [Aggiungi finestra di dialogo pacchetto deve consentire la scelta dell'origine pacchetto corrente](http://nuget.codeplex.com/workitem/88)
* [Sposta classi NuPack.Core in diversi spazi dei nomi](http://nuget.codeplex.com/workitem/50)
* [Aggiungere una Guida ai cmdlet](http://nuget.codeplex.com/workitem/23)
* [Verificare l'hash da feed dopo il download del pacchetto](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Di seguito sono le modifiche più significative apportate nella versione CTP 2.

* Passa il feed dal formato ATOM a un endpoint di servizio OData di pacchetti: se esegue l'aggiornamento alla versione CTP2 di NuGet, assicurarsi di aggiungere il seguente URL come origine pacchetto: `https://feed.nuget.org/ctp2/odata/v1/`.
* Il comando Add Package per rinominare *Install-Package*.
* Aggiornato il `.nuspec` formato. Il `.nuspec` formato di ora include le *iconUrl* campo per specificare un'icona di 32 x 32 png che verrà visualizzata nella finestra di dialogo di pacchetto aggiungere. Pertanto, assicurarsi di impostare che per distinguere il pacchetto. Il `.nuspec` formato include anche il nuovo *projectUrl* campo che è possibile usare in modo che punti a una pagina web che fornisce ulteriori informazioni sul pacchetto.

Questa compilazione non funzionerà con vecchia `.nupkg` file. Se si verificano eccezioni di riferimento null, si usa una vecchia `.nupkg` del file ed è necessario ricompilarla con aggiornato [strumento da riga di comando NuGet](http://nuget.codeplex.com/releases/52017/download/165468).

Di seguito è riportato un elenco delle funzionalità e i bug risolti per NuGet CTP 2 (non includere i bug per la pulizia di code secondarie e così via.).

* [Decompressione assembly dei pacchetti errore quando si specifica di TargetFramework per un assembly.](http://nuget.codeplex.com/workitem/10)
* [Rendere più facilmente individuabile finestra della NuPack Console](http://nuget.codeplex.com/workitem/14)
* [ILMerge il rilascio nupack.exe](http://nuget.codeplex.com/workitem/19)
* [Migliore gestione delle eccezioni/errore](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager deve gestire normalmente gli errori correlati al feed](http://nuget.codeplex.com/workitem/28)
* [Necessaria una nuova icona per la console di](http://nuget.codeplex.com/workitem/29)
* [Localizzare le stringhe nella finestra di dialogo](http://nuget.codeplex.com/workitem/38)
* [Le cache NuPack .nupack i file scaricati in memoria](http://nuget.codeplex.com/workitem/40)
* [NuPack Console: Modificare lo scelta rapida predefiniti per la visualizzazione delle console](http://nuget.codeplex.com/workitem/48)
* [Project System devono supportare i valori predefiniti per le proprietà comuni](http://nuget.codeplex.com/workitem/49)
* [Esecuzione nupack.exe in una cartella con un solo file nuspec deve usare tale file nuspec](http://nuget.codeplex.com/workitem/52)
* [Menu progetto viene visualizzato anche quando non viene caricato alcun progetto/soluzione](http://nuget.codeplex.com/workitem/54)
* [Build. cmd ha esito negativo su un clone pulito della codebase](http://nuget.codeplex.com/workitem/56)
* [Funzionalità di disponibilità di aggiornamenti](http://nuget.codeplex.com/workitem/57)
* [Finestra di dialogo: Aggiunta di un pacchetto tramite la finestra di dialogo rimuove i prompt nella console di](http://nuget.codeplex.com/workitem/73)
* [Aggiunta di un pacchetto facendo clic su 'Installa' spesso è lento, con alcun feedback visivo](http://nuget.codeplex.com/workitem/80)
* [Non è possibile individuare quali my pacchetti installati hanno aggiornamenti.](http://nuget.codeplex.com/workitem/82)
* [Non è possibile aggiornare un pacchetto installato nella finestra di dialogo.](http://nuget.codeplex.com/workitem/83)
* [Non è possibile disinstallare un pacchetto installato nella finestra di dialogo](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Aggiungi riferimento al pacchetto&hellip; &rdquo; viene visualizzato nel menu di scelta rapida di riferimenti installati](http://nuget.codeplex.com/workitem/85)
* [Dopo aver aggiornato un pacchetto dalla console di, questo viene visualizzato sia la versione precedente e la nuova versione come installato](http://nuget.codeplex.com/workitem/86)
* [L'attività nella console, quando si usa la finestra di dialogo scomparirà dopo l'uso](http://nuget.codeplex.com/workitem/87)
* [Pulizia della riga di comando di analisi in nupack.exe](http://nuget.codeplex.com/workitem/89)
* [Aggiungere un nome descrittivo a origini dei pacchetti](http://nuget.codeplex.com/workitem/98)
* [Aggiornare i file con estensione nuspec di supporto includere le icone di pacchetto](http://nuget.codeplex.com/workitem/103)
* [Feed dell'interfaccia utente non consente la copia dell'URL](http://nuget.codeplex.com/workitem/105)
* [Migliore gestione degli errori di remove-package.](http://nuget.codeplex.com/workitem/107)
* [Digitare nella finestra della Console varia a seconda dello stato attivo del cursore](http://nuget.codeplex.com/workitem/112)
* [Messaggi di errore hanno un aspetto terribili](http://nuget.codeplex.com/workitem/116)
* [Le prestazioni di Remove-pacchetto per un pacchetto che non è installato non sono valida](http://nuget.codeplex.com/workitem/117)
* [Rimozione di un pacchetto ha esito negativo quando non sono presenti origini pacchetto](http://nuget.codeplex.com/workitem/119)
* [Remove-pacchetto ha esito negativo quando l'origine del pacchetto non è disponibile](http://nuget.codeplex.com/workitem/120)
* [Aggiungere il titolo del feed e metadati del pacchetto.](http://nuget.codeplex.com/workitem/125)
* [Add-parametro di origine al Aggiungi pacchetto](http://nuget.codeplex.com/workitem/127)
* [Pacchetto di elenco deve avere un - parametro di origine](http://nuget.codeplex.com/workitem/128)
* [NuPack.Server Update in modo da richiedere NuPack utente dell'agente per scaricare il pacchetto](http://nuget.codeplex.com/workitem/142)
* [Finestra di dialogo accettazione della licenza necessario elencare le licenze per tutte le dipendenze che richiedono l'accettazione](http://nuget.codeplex.com/workitem/145)
* [Registrare un errore quando si genera un pacchetto nel feed](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe non deve consentire a un oggetto vuoto &lt;licenseurl&gt; elemento](http://nuget.codeplex.com/workitem/152)
* [Rinominare elenco-Package con Get-pacchetto, aggiungere-Install-Package e Remove-Package di Uninstall-Package](http://nuget.codeplex.com/workitem/155)
* [Usando la voce di menu Aggiungi riferimento al pacchetto dalla struttura della soluzione arresto anomalo di Visual Studio](http://nuget.codeplex.com/workitem/158)
* [Etichetta "origini pacchetti disponibili" manca un carattere due punti](http://nuget.codeplex.com/workitem/160)
* [Verificare con estensione nuspec xml elemento maiuscole/minuscole camel in modo coerente le maiuscole/minuscole](http://nuget.codeplex.com/workitem/161)
* [Manifesto di NuPack VSIX deve attivare il bit "admin"](http://nuget.codeplex.com/workitem/162)
* [Se si esegue elenco-Package con alcun feed, viene visualizzato errore ref null](http://nuget.codeplex.com/workitem/164)
* [NuGet.exe: specificare il percorso di destinazione](http://nuget.codeplex.com/workitem/171)
* [Errori di PowerShell aprendo la Console di gestione pacchetti in Windows XP](http://nuget.codeplex.com/workitem/175)
* [Visual Studio si blocca durante il tentativo di caricare l'elenco di pacchetti](http://nuget.codeplex.com/workitem/176)
* [consentire ai pacchetti di meta (nessun file, solo le dipendenze)](http://nuget.codeplex.com/workitem/180)
* [Convertire Script di Powershell al modulo di Powershell 2.0](http://nuget.codeplex.com/workitem/181)
* [PathResolver deve eliminare i caratteri jolly che precede parte di percorso quando si specifica destinazione](http://nuget.codeplex.com/workitem/183)
* [Nessuna dipendenza](http://nuget.codeplex.com/workitem/186)
* [Errore durante l'installazione Elmah](http://nuget.codeplex.com/workitem/192)
* [Trasformazioni di configurazione non funzionano correttamente con &lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [La variabile ' $global: projectCache' non può essere recuperato perché non è stato impostato](http://nuget.codeplex.com/workitem/203)
* [Aggiungere attività di MSBuild per la creazione di pacchetti NuPack](http://nuget.codeplex.com/workitem/205)
* [pacchetto dell'elenco deve supportare la ricerca/filtro](http://nuget.codeplex.com/workitem/206)
* [Sempre visualizzato un collegamento alla licenza, se l'autore del pacchetto fornisce un URL di licenza](http://nuget.codeplex.com/workitem/208)
* [Eccezione "Accesso negato" occasionale con Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Gli unit test non superati: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Consenti per un set di file fallback/predefinito se non è stata trovata una versione di framework specifico](http://nuget.codeplex.com/workitem/223)
* [Aggiungi riferimento al pacchetto... Interfaccia utente non è possibile rimuovere un pacchetto](http://nuget.codeplex.com/workitem/225)
* [Aggiungi riferimento al pacchetto di arresti anomali studio quando uno o più progetto viene scaricato](http://nuget.codeplex.com/workitem/228)
* [Trasformazione di configurazione non viene visualizzata per lavorare sui file di debug](http://nuget.codeplex.com/workitem/229)
* [Init.ps1 non attivazione su pacchetto personalizzato](http://nuget.codeplex.com/workitem/237)
* [Quando si aggiunge il feedlist percorsi, il pulsante predefinito è impostato su OK, quindi se preme INVIO deve essere chiuso automaticamente](http://nuget.codeplex.com/workitem/240)
* [Tentare di disinstallare una dipendenza si arresterà Visual Studio se si tenta di 2 volte in una riga](http://nuget.codeplex.com/workitem/241)
* [Visualizzare l'URL del progetto nella finestra di dialogo Aggiungi pacchetto](http://nuget.codeplex.com/workitem/253)
* [Impostazione predefinita la finestra di dialogo Aggiungi pacchetto per i pacchetti installati](http://nuget.codeplex.com/workitem/254)
* [Modificare la voce di menu finestra di dialogo Aggiungi pacchetto.](http://nuget.codeplex.com/workitem/261)
* [Rinominare gli spazi dei nomi e assembly](http://nuget.codeplex.com/workitem/274)
* [Rinominare il progetto NuPack in NuGet](http://nuget.codeplex.com/workitem/282)
* [Aggiungere il testo seguente sotto l'elenco di dipendenze](http://nuget.codeplex.com/workitem/288)
* [Modificare il testo di accettazione della licenza nella finestra di dialogo accettazione della licenza](http://nuget.codeplex.com/workitem/291)
* [Modificare il testo nella finestra di dialogo accettazione della licenza sopra l'elenco dei pacchetti](http://nuget.codeplex.com/workitem/292)
* [OData non funziona con un URL fwlink](http://nuget.codeplex.com/workitem/304)
* [Package Manager UI: tramite il caching ripetuto del conteggio di pacchetto utilizzata per il paging](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet -&gt; errore Console di gestione pacchetti](http://nuget.codeplex.com/workitem/335)
* [Aggiungi che finestra di dialogo pacchetto Mostra licenza accettazione per già installato in pacchetto](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

Di seguito è riportato un elenco delle funzionalità e i bug risolti per NuGet CTP 1.

* [Estensione del pacchetto deve essere rinominato per .nupack](http://nuget.codeplex.com/workitem/1)
* [Spostare file del pacchetto nella cartella](http://nuget.codeplex.com/workitem/2)
* [Installazione di tipo merge &amp; comandi Aggiungi PS](http://nuget.codeplex.com/workitem/3)
* [Creare alias per i cmdlet di verbo-nome](http://nuget.codeplex.com/workitem/4)
* [NuPack può creare confusione quando si passa a soluzioni in Visual Studio](http://nuget.codeplex.com/workitem/6)
* [È necessario nascondere la cartella della soluzione 'package' per impostazione predefinita](http://nuget.codeplex.com/workitem/11)
* [Aggiungere il supporto per la sostituzione dei token negli elementi di contenuto.](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI devono usare l'API PackageSource](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager contrassegna i pacchetti installati prima di eseguirne l'installazione](http://nuget.codeplex.com/workitem/27)
* [Eliminazione del progetto predefinito dalla soluzione progetto eliminato viene ancora visualizzato come predefinito](http://nuget.codeplex.com/workitem/30)
* [Nuovo pacchetto ha esito negativo con "Non è possibile aggiungere parte per l'URI specificato perché è già nel pacchetto."](http://nuget.codeplex.com/workitem/32)
* [Rimuovere le stringhe "NuPack" dall'interfaccia utente grafica di Visual Studio](http://nuget.codeplex.com/workitem/35)
* [Aggiungere file di Apache intestazione a un copyright. txt](http://nuget.codeplex.com/workitem/36)
* [Rimuovere il comando Update-PackageSource](http://nuget.codeplex.com/workitem/37)
* [Inutilizzabile durante il caricamento del profilo di gestione pacchetti genera un'eccezione](http://nuget.codeplex.com/workitem/39)
* [devono ricevere lo stato aggiuntivo Init.ps1, install.ps1 e uninstall.ps1](http://nuget.codeplex.com/workitem/41)
* [Combinare Console e i pacchetti di interfaccia utente grafica in un unico pacchetto](http://nuget.codeplex.com/workitem/42)
* [Logica di trasformazione XML non funziona se applicato al codice XML che non è in corrispondenza della radice](http://nuget.codeplex.com/workitem/43)
* [Gestire i pacchetti origini finestra di dialogo Impostazioni non aggiornare la console NuPack](http://nuget.codeplex.com/workitem/44)
* [Interfaccia utente della NuPack Console: Rinominare 'Feed di pacchetti' riepilogo 'Origine del pacchetto'](http://nuget.codeplex.com/workitem/45)
* [Opzioni della NuPack Console: Rinomina "del Repository dell'interfaccia utente' siano coerenti con NuPack Console](http://nuget.codeplex.com/workitem/46)
* [Aggiungi-pacchetto ha esito negativo con un sito Web che è stato aperto da IIS o un URL](http://nuget.codeplex.com/workitem/53)
* [Origine di gestione pacchetti non funziona con FwLink](http://nuget.codeplex.com/workitem/55)
* [Impostare l'origine del pacchetto predefinito](http://nuget.codeplex.com/workitem/59)
* [Quando si aggiungono origini dei pacchetti nell'opzione, quando viene fornita una sola origine, si supponga che è il valore predefinito.](http://nuget.codeplex.com/workitem/60)
* [La finestra di dialogo dell'interfaccia utente mostra fittizi pacchetti "recenti"](http://nuget.codeplex.com/workitem/62)
* [Opzioni: Facendo clic su Annulla non Annulla le modifiche](http://nuget.codeplex.com/workitem/63)
* [Aggiungi che ricerca di finestra di dialogo riferimento pacchetto deve essere maiuscole e minuscole](http://nuget.codeplex.com/workitem/65)
* [Correggere i metadati della società nel file AssemblyInfo.cs](http://nuget.codeplex.com/workitem/67)
* [Numero di versione per il progetto VSIX](http://nuget.codeplex.com/workitem/71)
* [Remove-Package: Utilizzo-? Visualizza la Guida due volte](http://nuget.codeplex.com/workitem/72)
* [Eseguire i pacchetti di installazione/disinstallazione per i pacchetti a livello di progetto](http://nuget.codeplex.com/workitem/74)
* [Server non è possibile creare feed quando una nupack convalida non è riuscita](http://nuget.codeplex.com/workitem/90)
* [È necessario sostituire le icone NuPack](http://nuget.codeplex.com/workitem/94)
* [Il proxy http NTLM non esegue l'autenticazione per il feed del pacchetto.](http://nuget.codeplex.com/workitem/96)
* [La finestra di dialogo non sempre inizia centrato nella finestra di Visual Studio](http://nuget.codeplex.com/workitem/100)
* [Molti dei campi in un dettagli pacchetti non in corso il popolamento della finestra di dialogo](http://nuget.codeplex.com/workitem/102)
* [Finestra di dialogo dell'interfaccia utente non visualizza i nomi degli autori](http://nuget.codeplex.com/workitem/108)
* [Il motivo per cui - versione per Remove-Package](http://nuget.codeplex.com/workitem/113)
* [Rimuovere la scheda recenti nella finestra di dialogo dell'interfaccia utente](http://nuget.codeplex.com/workitem/115)
* [Arresto anomalo di Visual Studio quando a destra fare clic sulla cartella soluzione dopo l'apertura dell'interfaccia utente della finestra almeno uno.](http://nuget.codeplex.com/workitem/126)
* [Modifica-parametro locale del pacchetto dell'elenco-installato](http://nuget.codeplex.com/workitem/129)
* [Rinominare packages.xml NuPack.config](http://nuget.codeplex.com/workitem/132)
* [Console forza cursore alla fine della riga](http://nuget.codeplex.com/workitem/135)
* [Remove-Package intellisense viene interrotta](http://nuget.codeplex.com/workitem/136)
* [Aggiungere il flag RequireLicenseAcceptance Flag al file con estensione nuspec e Feed](http://nuget.codeplex.com/workitem/137)
* [Aggiungi Feed LicenseUrl al formato con estensione nuspec e pacchetto](http://nuget.codeplex.com/workitem/138)
* [Facendo clic su Installa per il pacchetto che richiede l'accettazione dovrebbe mostrare l'accettazione della finestra di dialogo](http://nuget.codeplex.com/workitem/139)
* [Aggiungere testo declinazione di responsabilità per la finestra di dialogo Aggiungi pacchetto](http://nuget.codeplex.com/workitem/140)
* [Aggiungere una dichiarazione di non responsabilità quando il pacchetto Console è eseguita la prima volta](http://nuget.codeplex.com/workitem/143)
* [Visualizzare una dichiarazione di non responsabilità dopo l'installazione del pacchetto nella Console di](http://nuget.codeplex.com/workitem/144)
* [Rinominare l'estensione .nupack al pacchetto. nupkg](http://nuget.codeplex.com/workitem/146)