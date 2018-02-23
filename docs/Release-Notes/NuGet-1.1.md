---
title: Note sulla versione 1.0 e 1.1 di NuGet | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per NuGet 1.1 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "1.1 NuGet note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6a596e61f144e7269f703f2dba3dddb4fd338e6a
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-10-and-11-release-notes"></a>Note sulla versione 1.0 e 1.1 di NuGet

[Note sulla versione 1.2 di NuGet](../release-notes/nuget-1.2.md)

NuGet 1.0 è stato rilasciato il 13 gennaio 2011.  1.1 NuGet è stato rilasciato il 12 febbraio 2011.

## <a name="overview"></a>Panoramica

Questo documento contiene le note sulla versione per le diverse versioni di NuGet 1.0 raggruppati in base alla versione di anteprima principali.

NuGet include i componenti seguenti:

* *NuGet.Tools.vsix* * costituito da:
  * **Aggiungere una finestra di dialogo pacchetto libreria** * finestra all'interno di Visual Studio consentono di individuare e installare i pacchetti.
  * **Console di gestione pacchetti** * basati su Powershell console all'interno di Visual Studio.
* *Strumento da riga di comando NuGet* * strumento utilizzato per creare pacchetti (e infine pubblica).

NuGet strumenti di Visual Studio Extension (*NuGet.Tools.vsix*) richiede:

* Visual Studio 2010 o Visual Web Developer 2010 Express.

Lo strumento da riga di comando NuGet richiede:

* Versione di .NET framework 4

## <a name="installation"></a>Installazione

Utilizzare questo [versione più recente](http://nuget.codeplex.com/releases/view/52018):

* Disinstallare prima della compilazione precedente. È necessario eseguire Visual Studio come amministratore per eseguire questa operazione.
* Rimuovere tutti i feed esistenti che è necessario.
* Aggiungere un nuovo feed che punta a [http://go.microsoft.com/fwlink/?LinkId=206669](http://go.microsoft.com/fwlink/?LinkId=206669).

## <a name="nuget-11"></a>1.1 NuGet

L'elenco di problemi risolti in questa versione [è reperibile qui](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

Un problema è stato risolto per RTM perché la versione RC.

* [Problema 474: Rimozione dei pacchetti interessa tutti i progetti nella soluzione](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Versione finale candidata

Di seguito sono le modifiche apportate in questa versione finale candidata CTP 2. Visitare Issue Tracker per visualizzare l'elenco completo dei bug.

* [Aggiornamento pacchetto dalla Console di non aggiornare le dipendenze.](http://nuget.codeplex.com/workitem/443)
* [Aggiunta del pacchetto preleva bin non del pacchetto (CTP1)](http://nuget.codeplex.com/workitem/442)
* [Aggiornamento di un pacchetto lascia ai riferimenti interrotti](http://nuget.codeplex.com/workitem/440)
* [Get-Package-gli aggiornamenti si verifica un errore nella finestra di dialogo, o quando l'origine di aggregazione 'Tutte' è selezionato nella console di](http://nuget.codeplex.com/workitem/439)
* [Recupero di errori di verifica del pacchetto](http://nuget.codeplex.com/workitem/426)
* [Avvisare gli utenti quando non è installato un pacchetto dalla finestra di dialogo Aggiungi pacchetto](http://nuget.codeplex.com/workitem/425)
* [Get-Package-Aggiorna genera un'eccezione durante l'aggiornamento di un numero elevato di pacchetti](http://nuget.codeplex.com/workitem/424)
* [Migliorare la gestione degli errori quando il file nuspec vengono creato in modo non corretto](http://nuget.codeplex.com/workitem/423)
* [Pacchetto NuGet Ignora file specificati](http://nuget.codeplex.com/workitem/422)
* [Rimuovendo l'origine del pacchetto al secondo-ultima e quindi fare clic su "Sposta giù" arresto anomalo di Visual Studio](http://nuget.codeplex.com/workitem/418)
* [Rimuovere un riferimento all'assembly durante l'installazione dei pacchetti](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException quando si apre una finestra di dialogo Impostazioni](http://nuget.codeplex.com/workitem/411)
* [Chiave di accesso per l'origine del pacchetto nella Console di gestione pacchetti non funziona](http://nuget.codeplex.com/workitem/410)
* [Chiavi di accesso di finestra di dialogo Impostazioni NuGet VS assegnare lo stato attivo per i campi non corretti](http://nuget.codeplex.com/workitem/409)
* [Intellisense ID pacchetto non deve eseguire una query troppi elementi](http://nuget.codeplex.com/workitem/404)
* [Errore durante l'aggiunta del pacchetto al progetto con un carattere punto nel nome del progetto](http://nuget.codeplex.com/workitem/403)
* [Problema con i file specificati in nuspec](http://nuget.codeplex.com/workitem/400)
* [Feed ufficiale corretta deve ottenere registrato quando si utilizza la compilazione più recente](http://nuget.codeplex.com/workitem/399)
* [Tag devono utilizzare spazi anziché #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata mancano alcune informazioni utili](http://nuget.codeplex.com/workitem/388)
* [Aggiungi collegamento alla finestra di dialogo](http://nuget.codeplex.com/workitem/386)
* [Utilizzo di App_Data per decomprimere le interruzioni di pacchetti in Visual Studio](http://nuget.codeplex.com/workitem/380)
* [Implementare tag](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder consente a un pacchetto vuoto senza dipendenze da creare](http://nuget.codeplex.com/workitem/373)
* [Aggiungere il campo di proprietari per il pacchetto](http://nuget.codeplex.com/workitem/365)
* [Aggiornare il manifesto VSIX per indicare che Gestione pacchetti NuGet anziché strumenti VSIX](http://nuget.codeplex.com/workitem/364)
* [Comando Get-Package genera l'errore quando si seleziona tutto il codice sorgente](http://nuget.codeplex.com/workitem/359)
* [Consente l'ordinamento delle origini pacchetto nella finestra di dialogo Opzioni](http://nuget.codeplex.com/workitem/356)
* [Pacchetto di aggiornamento non comporta la rimozione versione precedente](http://nuget.codeplex.com/workitem/352)
* [Specifica di intervallo di versioni di implementare le dipendenze](http://nuget.codeplex.com/workitem/347)
* [Visual Studio si blocca quando facendo clic su "Aggiungi nuovo pacchetto"](http://nuget.codeplex.com/workitem/346)
* [Visualizzare la finestra di dialogo Aggiungi pacchetto download e classificazioni](http://nuget.codeplex.com/workitem/345)
* [Modifica tra l'origine del pacchetto nella finestra di dialogo non aggiorna l'origine attiva](http://nuget.codeplex.com/workitem/344)
* [Rimuovere l'associazione di chiavi per la finestra della Console di gestione pacchetti](http://nuget.codeplex.com/workitem/339)
* [Pacchetto di installazione non è riconosciuto come nome di un cmdlet...](http://nuget.codeplex.com/workitem/338)
* [Installa un pacchetto da un feed le dipendenze sui feed regolare locale non sono stati risolti](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies deve ignorare le dipendenze che sono ancora in uso](http://nuget.codeplex.com/workitem/331)
* [Se l'annullamento di navigazione a pagina, l'utente non è possibile passare a una pagina diversa mentre la richiesta della pagina originale restituisce](http://nuget.codeplex.com/workitem/325)
* [Esaminare le prestazioni di NuPack.Server per servire i feed con un numero elevato di pacchetti.](http://nuget.codeplex.com/workitem/324)
* [La seconda volta che filtrare per un pacchetto utilizza l'origine del pacchetto "Nuovo", anziché l'origine selezionata in precedenza.](http://nuget.codeplex.com/workitem/321)
* [È necessario selezionare l'origine del pacchetto predefinito quando si seleziona la scheda "Online" nella finestra di dialogo.](http://nuget.codeplex.com/workitem/320)
* [Pacchetto dell'elenco deve visualizzare i pacchetti installati per impostazione predefinita](http://nuget.codeplex.com/workitem/309)
* [HintPaths di riferimento di assembly](http://nuget.codeplex.com/workitem/294)
* [Eccezione durante l'apertura delle Console di gestione pacchetti](http://nuget.codeplex.com/workitem/268)
* [Intellisense console Scarica intero feed](http://nuget.codeplex.com/workitem/259)
* [Origine del pacchetto 'Default' deve essere rinominato in 'Active'](http://nuget.codeplex.com/workitem/258)
* [Pacchetto origini dell'interfaccia utente: fare clic su OK deve aggiungere la nuova origine se i campi di origine/nome non vuoto](http://nuget.codeplex.com/workitem/257)
* [Finestra di dialogo diventa super lenta quando il numero di pacchetti installati è di grandi dimensioni](http://nuget.codeplex.com/workitem/243)
* [Supportano il reindirizzamento di associazione di assembly con nome sicuro](http://nuget.codeplex.com/workitem/238)
* [Aggiungi riferimento al pacchetto... Interfaccia utente da includere rilascio verso il basso per l'origine del pacchetto](http://nuget.codeplex.com/workitem/226)
* [NuPack deve supportare la trasformazione di configurazione agnostically del nome del file di configurazione](http://nuget.codeplex.com/workitem/224)
* [Consente di BasePath per essere sottoposto a override in NuPack.exe](http://nuget.codeplex.com/workitem/222)
* [Comportamento di Fallback origine pacchetto](http://nuget.codeplex.com/workitem/204)
* [Un arresto anomalo all'interfaccia utente grafica](http://nuget.codeplex.com/workitem/201)
* [Aggiungi le opzioni di finestra di dialogo Aggiungi pacchetto di ordinamento](http://nuget.codeplex.com/workitem/179)
* [tasto di scelta rapida per chiudere la Console di gestione pacchetti](http://nuget.codeplex.com/workitem/174)
* [PowerConsole causa NuPack Console esito negativo](http://nuget.codeplex.com/workitem/166)
* [Console e finestra di dialogo Aggiungi pacchetto deve impostare l'agente utente nelle richieste](http://nuget.codeplex.com/workitem/141)
* [Impostare il numero di versione del progetto VSIX e NuPack.exe nella compilazione.](http://nuget.codeplex.com/workitem/134)
* [Nascondere parametri PowerShell comuni da-?](http://nuget.codeplex.com/workitem/118)
* [Add - Guida dettagliata per i comandi della console](http://nuget.codeplex.com/workitem/110)
* [Aggiungere una finestra di dialogo pacchetto deve consentire la scelta dell'origine pacchetto corrente](http://nuget.codeplex.com/workitem/88)
* [Sposta classi NuPack.Core in diversi spazi dei nomi](http://nuget.codeplex.com/workitem/50)
* [Aggiungere la Guida per i cmdlet](http://nuget.codeplex.com/workitem/23)
* [Verificare l'hash dal feed dopo il download del pacchetto](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Di seguito sono le modifiche più significative apportate nella versione CTP 2.

* Passa il pacchetto di feed di dati a un endpoint di servizio OData da ATOM: se esegue l'aggiornamento alla versione CTP2 di NuGet, assicurarsi di aggiungere il seguente URL come origine del pacchetto: https://feed.nuget.org/ctp2/odata/v1/.
* Rinominare il comando Add-Package per *Install-Package*.
* Aggiornare il `.nuspec` formato. Il `.nuspec` formato include ora il *iconUrl* campo per specificare un'icona di 32 x 32 png verrà visualizzati nella finestra di dialogo Aggiungi pacchetto. Sarà necessario impostare che per distinguere il pacchetto. Il `.nuspec` formato include anche il nuovo *projectUrl* campo che è possibile utilizzare in modo che punti a una pagina web che fornisce ulteriori informazioni sul pacchetto.

Questa compilazione non funzionerà con precedenti `.nupkg` file. Se si verificano eccezioni di riferimento null, si utilizza un vecchio `.nupkg` necessario ricompilarlo con l'aggiornamento e file [strumento da riga di comando NuGet](http://nuget.codeplex.com/releases/52017/download/165468).

Di seguito è riportato un elenco delle funzionalità e i bug risolti per NuGet CTP 2 (non includono i bug per unità di allocazione di codice e così via).

* [Assembly di errore decompressione del pacchetto quando si specifica il TargetFramework per un assembly.](http://nuget.codeplex.com/workitem/10)
* [Rendere più facilmente individuabili finestra della NuPack Console](http://nuget.codeplex.com/workitem/14)
* [La versione nupack.exe ILMerge](http://nuget.codeplex.com/workitem/19)
* [Gestione migliorata di errore o eccezione.](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager deve gestire correttamente gli errori relativi al feed](http://nuget.codeplex.com/workitem/28)
* [È necessario per la console di una nuova icona](http://nuget.codeplex.com/workitem/29)
* [Localizzare stringhe nella finestra di dialogo](http://nuget.codeplex.com/workitem/38)
* [Cache NuPack .nupack i file scaricati in memoria](http://nuget.codeplex.com/workitem/40)
* [NuPack Console: Modificare lo scelta rapida predefinita per la visualizzazione di console](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem deve supportare i valori predefiniti per le proprietà comuni](http://nuget.codeplex.com/workitem/49)
* [Esecuzione nupack.exe in una cartella con un solo file nuspec deve utilizzare tale nuspec](http://nuget.codeplex.com/workitem/52)
* [Dal Menu progetto viene visualizzato anche quando non viene caricata alcun progetto/soluzione](http://nuget.codeplex.com/workitem/54)
* [Build.cmd non riesce in un clone del codebase pulito](http://nuget.codeplex.com/workitem/56)
* [Funzionalità di disponibilità di aggiornamenti](http://nuget.codeplex.com/workitem/57)
* [Finestra di dialogo: Aggiunta di un pacchetto tramite la finestra di dialogo consente di rimuovere il prompt dei comandi nella console di](http://nuget.codeplex.com/workitem/73)
* [Aggiunta di un pacchetto, fare clic su 'Installa' spesso è lenta, con alcun feedback visivo](http://nuget.codeplex.com/workitem/80)
* [Non è possibile individuare quale dei pacchetti installati sono gli aggiornamenti.](http://nuget.codeplex.com/workitem/82)
* [Non è possibile aggiornare un pacchetto installato nella finestra di dialogo.](http://nuget.codeplex.com/workitem/83)
* [Non è possibile disinstallare un pacchetto installato nella finestra di dialogo](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Aggiungi riferimento al pacchetto&hellip; &rdquo; viene visualizzato il menu di scelta rapida di riferimenti installati](http://nuget.codeplex.com/workitem/85)
* [Dopo aver aggiornato un pacchetto dalla console di, questo viene visualizzato sia la versione precedente e la nuova versione come installato](http://nuget.codeplex.com/workitem/86)
* [L'attività nella console, quando si utilizza la finestra di dialogo scomparirà dopo l'utilizzo](http://nuget.codeplex.com/workitem/87)
* [L'analisi in nupack.exe riga di comando di pulitura](http://nuget.codeplex.com/workitem/89)
* [Aggiungere un nome descrittivo per l'origine del pacchetto](http://nuget.codeplex.com/workitem/98)
* [. Nuspec di aggiornamento per supportare tra le icone di pacchetto](http://nuget.codeplex.com/workitem/103)
* [Feed dell'interfaccia utente non consente di copiare l'URL](http://nuget.codeplex.com/workitem/105)
* [Migliore gestione degli errori di pacchetto di installazione.](http://nuget.codeplex.com/workitem/107)
* [Digitare nella finestra della Console varia a seconda dello stato attivo del cursore](http://nuget.codeplex.com/workitem/112)
* [I messaggi di errore esaminare varie](http://nuget.codeplex.com/workitem/116)
* [Le prestazioni del pacchetto di installazione per un pacchetto che non è installato non sono valida](http://nuget.codeplex.com/workitem/117)
* [Rimozione di un pacchetto ha esito negativo quando non sono presenti origini pacchetto](http://nuget.codeplex.com/workitem/119)
* [Pacchetto di installazione ha esito negativo quando l'origine del pacchetto non è disponibile](http://nuget.codeplex.com/workitem/120)
* [Aggiungere il titolo nei metadati del pacchetto e il feed.](http://nuget.codeplex.com/workitem/125)
* [Aggiungi-parametro origine Add-Package](http://nuget.codeplex.com/workitem/127)
* [Elenco pacchetto dovrà avere-parametro di origine](http://nuget.codeplex.com/workitem/128)
* [NuPack.Server di aggiornamento per richiedere NuPack utente agente per il Download del pacchetto](http://nuget.codeplex.com/workitem/142)
* [Finestra di dialogo accettazione licenza necessario elencare le licenze per tutte le dipendenze che richiedono l'accettazione](http://nuget.codeplex.com/workitem/145)
* [Registrare un errore quando si genera un pacchetto nel feed](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe non deve consentire vuota &lt;licenseurl&gt; elemento](http://nuget.codeplex.com/workitem/152)
* [Rinominare elenco pacchetto a Get-pacchetto, aggiungere-pacchetto Install-Package e Remove-Package Uninstall-Package](http://nuget.codeplex.com/workitem/155)
* [Utilizzando la voce di menu Aggiungi riferimento al pacchetto dal Navigatore soluzione arresto anomalo di Visual Studio](http://nuget.codeplex.com/workitem/158)
* [Etichetta "origini pacchetti disponibili" manca un virgola.](http://nuget.codeplex.com/workitem/160)
* [Rendere. nuspec xml elemento maiuscole e minuscole in modo coerente le maiuscole/minuscole](http://nuget.codeplex.com/workitem/161)
* [Manifesto di NuPack VSIX deve attivare il bit 'admin'](http://nuget.codeplex.com/workitem/162)
* [Se si esegue l'elenco pacchetto con nessun feed, viene visualizzato l'errore di riferimento null](http://nuget.codeplex.com/workitem/164)
* [NuGet.exe: specificare il percorso di destinazione](http://nuget.codeplex.com/workitem/171)
* [Errori di PowerShell aprendo la Console di gestione del pacchetto in Windows XP](http://nuget.codeplex.com/workitem/175)
* [Visual Studio si blocca durante il tentativo di caricare l'elenco dei pacchetti](http://nuget.codeplex.com/workitem/176)
* [consentire i pacchetti di meta (nessun file, solo le dipendenze)](http://nuget.codeplex.com/workitem/180)
* [Convertire uno Script di Powershell per il modulo di Powershell 2.0](http://nuget.codeplex.com/workitem/181)
* [PathResolver dovrebbe ignorare i caratteri jolly che precedono parte di percorso quando si specifica destinazione](http://nuget.codeplex.com/workitem/183)
* [Nessuna dipendenza](http://nuget.codeplex.com/workitem/186)
* [Errore durante l'installazione Elmah](http://nuget.codeplex.com/workitem/192)
* [Trasformazioni di configurazione non funzionano correttamente con &lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [La variabile ' $globale: projectCache' non può essere recuperato perché non è stato impostato](http://nuget.codeplex.com/workitem/203)
* [Aggiungere attività di MSBuild per la creazione di pacchetti NuPack](http://nuget.codeplex.com/workitem/205)
* [pacchetto dell'elenco deve supportare la ricerca di filtro](http://nuget.codeplex.com/workitem/206)
* [Sempre visualizzato un collegamento a licenza se l'autore del pacchetto fornisce un URL di licenza](http://nuget.codeplex.com/workitem/208)
* [Eccezione di "Accesso negato" occasionali con Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Unit test non superati: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Consentono di un set di fallback/predefinito dei file se non viene trovata una versione di framework specifico](http://nuget.codeplex.com/workitem/223)
* [Aggiungi riferimento al pacchetto... Interfaccia utente non è possibile rimuovere un pacchetto](http://nuget.codeplex.com/workitem/225)
* [Aggiungi riferimento al pacchetto di arresti anomali studio quando uno o più progetto viene scaricato](http://nuget.codeplex.com/workitem/228)
* [Trasformazione di configurazione non viene visualizzata per lavorare su file web.debug.config](http://nuget.codeplex.com/workitem/229)
* [non è stato attivato nel pacchetto personalizzato Init.ps1](http://nuget.codeplex.com/workitem/237)
* [Quando si aggiunge il feedlist percorsi, il pulsante predefinito è impostato su OK, pertanto se si preme INVIO viene chiuso automaticamente](http://nuget.codeplex.com/workitem/240)
* [Tentare di disinstallare una dipendenza verificherà un arresto anomalo e se ha tentato di 2 volte in una riga](http://nuget.codeplex.com/workitem/241)
* [Visualizzare l'URL di progetto nella finestra di dialogo Aggiungi pacchetto](http://nuget.codeplex.com/workitem/253)
* [Impostazione predefinita la finestra di dialogo Aggiungi pacchetto di pacchetti installati](http://nuget.codeplex.com/workitem/254)
* [Modificare la voce di menu finestra di dialogo Aggiungi pacchetto.](http://nuget.codeplex.com/workitem/261)
* [Rinominare gli spazi dei nomi e assembly](http://nuget.codeplex.com/workitem/274)
* [Rinominare il progetto NuPack in NuGet](http://nuget.codeplex.com/workitem/282)
* [Aggiungere il seguente testo sotto l'elenco delle dipendenze](http://nuget.codeplex.com/workitem/288)
* [Modificare il testo di accettazione licenza nella finestra di dialogo accettazione licenza](http://nuget.codeplex.com/workitem/291)
* [Modificare il testo nella finestra di dialogo di accettazione licenza sopra l'elenco dei pacchetti](http://nuget.codeplex.com/workitem/292)
* [OData non funziona con un URL fwlink](http://nuget.codeplex.com/workitem/304)
* [Gestione pacchetti UI: tramite il caching ripetuto del conteggio di pacchetto utilizzato per il paging](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet -&gt; errore Console di gestione pacchetti](http://nuget.codeplex.com/workitem/335)
* [Aggiungere una che finestra di dialogo pacchetto Mostra licenza accettazione per già installato in pacchetto](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

Di seguito è riportato un elenco delle funzionalità e i bug risolti per NuGet CTP 1.

* [Estensione pacchetto deve essere rinominato in .nupack](http://nuget.codeplex.com/workitem/1)
* [Spostare il file del pacchetto nella cartella](http://nuget.codeplex.com/workitem/2)
* [Installazione di tipo merge &amp; comandi aggiungere PS](http://nuget.codeplex.com/workitem/3)
* [Creare alias di cmdlet verbo-nome](http://nuget.codeplex.com/workitem/4)
* [NuPack confusione quando si passa una soluzione in Visual Studio](http://nuget.codeplex.com/workitem/6)
* [Nascondere la cartella della soluzione 'packages' per impostazione predefinita](http://nuget.codeplex.com/workitem/11)
* [Aggiungere il supporto per la sostituzione dei token negli elementi di contenuto.](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI deve usare l'API di PackageSource](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager indica che i pacchetti installati prima di eseguirne l'installazione](http://nuget.codeplex.com/workitem/27)
* [Il progetto eliminato dalla soluzione di eliminazione del progetto predefinito comunque visualizzata come predefinito](http://nuget.codeplex.com/workitem/30)
* [Nuovo pacchetto ha esito negativo con "Non è possibile aggiungere parte per l'URI specificato perché è già nel pacchetto."](http://nuget.codeplex.com/workitem/32)
* [Rimuovere le stringhe "NuPack" dall'interfaccia utente grafica di Visual Studio](http://nuget.codeplex.com/workitem/35)
* [Aggiungere file Apache intestazione a un copyright. txt](http://nuget.codeplex.com/workitem/36)
* [Rimuovere il comando Update-PackageSource](http://nuget.codeplex.com/workitem/37)
* [Gestione di pacchetti inutilizzabile quando il caricamento del profilo genera un'eccezione](http://nuget.codeplex.com/workitem/39)
* [Init.ps1, install.ps1 e uninstall.ps1 devono ricevere lo stato aggiuntivo](http://nuget.codeplex.com/workitem/41)
* [Combinare Console e pacchetti GUI in un pacchetto](http://nuget.codeplex.com/workitem/42)
* [Logica di trasformazione XML non funziona se applicato al file XML non nella directory principale](http://nuget.codeplex.com/workitem/43)
* [Gestire origini impostazioni finestra di dialogo pacchetto non aggiornare la console NuPack](http://nuget.codeplex.com/workitem/44)
* [Interfaccia utente della NuPack Console: Rinominare 'Package feed' elenco a discesa elenco 'Origine del pacchetto'](http://nuget.codeplex.com/workitem/45)
* [Opzioni di NuPack Console: Rinominare 'Repository UI' siano coerenti con la NuPack Console](http://nuget.codeplex.com/workitem/46)
* [Aggiungi-pacchetto ha esito negativo con un sito Web che è stato aperto da IIS o un URL](http://nuget.codeplex.com/workitem/53)
* [Origine di gestione pacchetti non funziona con FwLink](http://nuget.codeplex.com/workitem/55)
* [Impostare l'origine del pacchetto predefinito](http://nuget.codeplex.com/workitem/59)
* [Durante l'aggiunta dell'origine del pacchetto nell'opzione, quando viene fornita solo un'origine, si supponga che il valore predefinito è.](http://nuget.codeplex.com/workitem/60)
* [La finestra di dialogo dell'interfaccia utente sono falsi package "recenti"](http://nuget.codeplex.com/workitem/62)
* [Opzioni: Fare clic su Annulla non annullare le modifiche](http://nuget.codeplex.com/workitem/63)
* [Aggiungere che la ricerca di finestra di dialogo Riferimenti pacchetto deve essere fatta distinzione tra maiuscole e minuscole](http://nuget.codeplex.com/workitem/65)
* [Correggere i metadati della società nel file AssemblyInfo.cs](http://nuget.codeplex.com/workitem/67)
* [Numero di versione per il progetto VSIX](http://nuget.codeplex.com/workitem/71)
* [Pacchetto di installazione: Con il-? Visualizza la Guida due volte](http://nuget.codeplex.com/workitem/72)
* [Esecuzione di pacchetti di installazione o disinstallazione per i pacchetti a livello di progetto](http://nuget.codeplex.com/workitem/74)
* [Server non è possibile creare feed quando una nupack convalida non riuscita](http://nuget.codeplex.com/workitem/90)
* [È necessario sostituire le icone NuPack](http://nuget.codeplex.com/workitem/94)
* [Il proxy http NTLM autenticarsi presso il pacchetto del feed.](http://nuget.codeplex.com/workitem/96)
* [La finestra di dialogo non viene sempre avviato centrato nella finestra di Visual Studio](http://nuget.codeplex.com/workitem/100)
* [Molti dei campi in un dettagli pacchetti vengono popolati non nella finestra di dialogo](http://nuget.codeplex.com/workitem/102)
* [Finestra di dialogo dell'interfaccia utente non visualizza i nomi degli autori](http://nuget.codeplex.com/workitem/108)
* [Motivo per cui - versione per il pacchetto di installazione](http://nuget.codeplex.com/workitem/113)
* [Rimuovere la scheda recente nella finestra di dialogo dell'interfaccia utente](http://nuget.codeplex.com/workitem/115)
* [Arresto anomalo di Visual Studio quando destro fare clic sulla cartella di soluzione dopo l'apertura dell'interfaccia utente di finestra di dialogo almeno uno.](http://nuget.codeplex.com/workitem/126)
* [Modifica-parametro locale del pacchetto dell'elenco per - installato](http://nuget.codeplex.com/workitem/129)
* [Rinominare packages.xml NuPack.config](http://nuget.codeplex.com/workitem/132)
* [Console forza cursore alla fine della riga](http://nuget.codeplex.com/workitem/135)
* [Remove-Package intellisense è interrotta](http://nuget.codeplex.com/workitem/136)
* [Aggiungere Flag RequireLicenseAcceptance. nuspec e Feed](http://nuget.codeplex.com/workitem/137)
* [Aggiunta di Feed LicenseUrl al formato. nuspec e del pacchetto](http://nuget.codeplex.com/workitem/138)
* [Fare clic su Installa per il pacchetto che richiede l'accettazione deve Mostra finestra di dialogo di accettazione](http://nuget.codeplex.com/workitem/139)
* [Aggiungere il testo di declinazione di responsabilità per la finestra di dialogo Aggiungi pacchetto](http://nuget.codeplex.com/workitem/140)
* [Aggiungere una dichiarazione di non responsabilità quando il pacchetto Console viene eseguita la prima volta](http://nuget.codeplex.com/workitem/143)
* [Visualizzare una dichiarazione di non responsabilità dopo l'installazione del pacchetto nella Console di](http://nuget.codeplex.com/workitem/144)
* [Rinominare l'estensione .nupack .nupkg](http://nuget.codeplex.com/workitem/146)