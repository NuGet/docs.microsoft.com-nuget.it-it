---
title: Note sulla versione di NuGet 1,0 e 1,1
description: Note sulla versione per NuGet 1,1, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4f90888eae4d039c99d6f6879a06107ec5a31a82
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384697"
---
# <a name="nuget-10-and-11-release-notes"></a>Note sulla versione di NuGet 1,0 e 1,1

[Note sulla versione di NuGet 1,2](../release-notes/nuget-1.2.md)

NuGet 1,0 è stato rilasciato il 13 gennaio 2011.  NuGet 1,1 è stato rilasciato il 12 febbraio 2011.

## <a name="overview"></a>Panoramica di

Questo documento contiene le note sulla versione per le varie versioni di NuGet 1,0 raggruppate in base alla versione di anteprima principale.

NuGet include i componenti seguenti:

* *NuGet. Tools. vsix* * che è costituito da:
  * Finestra di dialogo **Aggiungi pacchetto di libreria** * in Visual Studio utilizzata per esplorare e installare i pacchetti.
  * **Console di gestione pacchetti** * console basata su PowerShell in Visual Studio.
* Strumento da *riga di comando NuGet* * usato per creare (e infine pubblicare) pacchetti.

L'estensione di Visual Studio degli strumenti NuGet (*NuGet. Tools. vsix*) richiede:

* Visual Studio 2010 o Visual Web Developer 2010 Express.

Lo strumento da riga di comando NuGet richiede:

* .NET Framework versione 4

## <a name="installation"></a>Installazione di

Per usare questa [versione più recente](http://nuget.codeplex.com/releases/view/52018):

* Disinstallare innanzitutto la compilazione precedente. Per eseguire questa operazione, è necessario eseguire Visual Studio come amministratore.
* Rimuovere tutti i feed esistenti disponibili.
* Aggiungere un nuovo feed che punta a <https://go.microsoft.com/fwlink/?LinkId=206669>.

## <a name="nuget-11"></a>NuGet 1.1

L'elenco dei problemi risolti in questa versione [è disponibile qui](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1,0 RTM

Un problema è stato risolto per la versione RTM dalla versione RC.

* [Problema 474: la rimozione dei pacchetti influiscono su tutti i progetti nella soluzione](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Release Candidate

Di seguito sono riportate le modifiche apportate in questa versione finale candidata dalla versione CTP 2. Per visualizzare l'elenco completo dei bug, visitare il monitoraggio dei problemi.

* [L'aggiornamento del pacchetto dalla console non aggiorna le dipendenze.](http://nuget.codeplex.com/workitem/443)
* [L'aggiunta del pacchetto preleva i riferimenti al pacchetto non (CTP1)](http://nuget.codeplex.com/workitem/442)
* [L'aggiornamento di un pacchetto lascia riferimenti interrotti](http://nuget.codeplex.com/workitem/440)
* [Get-Package-Updates ha esito negativo nella finestra di dialogo o quando l'origine aggregata ' all'è selezionata nella console](http://nuget.codeplex.com/workitem/439)
* [Recupero degli errori di verifica del pacchetto](http://nuget.codeplex.com/workitem/426)
* [Avvisare gli utenti quando un pacchetto non può essere installato dalla finestra di dialogo Aggiungi pacchetto](http://nuget.codeplex.com/workitem/425)
* [Get-Package-Updates genera un'eccezione durante l'aggiornamento di un numero elevato di pacchetti](http://nuget.codeplex.com/workitem/424)
* [Migliorare la gestione degli errori quando i file nuspec vengono creati in modo non corretto](http://nuget.codeplex.com/workitem/423)
* [Il pacchetto NuGet ignora i file specificati](http://nuget.codeplex.com/workitem/422)
* [Rimozione dell'origine del pacchetto dal secondo all'ultimo e quindi facendo clic su "Sposta giù" in arresto anomalo rispetto a](http://nuget.codeplex.com/workitem/418)
* [Rimuovi riferimento all'assembly durante l'installazione dei pacchetti](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException durante l'apertura della finestra di dialogo Impostazioni](http://nuget.codeplex.com/workitem/411)
* [La chiave di accesso per l'origine del pacchetto nella console di gestione pacchetti non funziona](http://nuget.codeplex.com/workitem/410)
* [Le chiavi di accesso della finestra di dialogo Impostazioni di NuGet e attivano i campi non corretti](http://nuget.codeplex.com/workitem/409)
* [L'ID pacchetto IntelliSense non deve eseguire query su un numero eccessivo di elementi](http://nuget.codeplex.com/workitem/404)
* [Errore durante l'aggiunta del pacchetto al progetto con un carattere punto nel nome del progetto](http://nuget.codeplex.com/workitem/403)
* [Problema con i file specificati in NuSpec](http://nuget.codeplex.com/workitem/400)
* [Il feed ufficiale corretto dovrebbe essere registrato quando si usa la build più recente](http://nuget.codeplex.com/workitem/399)
* [I tag devono usare spazi anziché #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata non dispone di informazioni utili](http://nuget.codeplex.com/workitem/388)
* [Aggiungere il collegamento report abuse alla finestra di dialogo](http://nuget.codeplex.com/workitem/386)
* [Uso di App_Data per decomprimere interruzioni dei pacchetti in Visual Studio](http://nuget.codeplex.com/workitem/380)
* [Implementa Tag](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder consente la creazione di un pacchetto vuoto senza dipendenze](http://nuget.codeplex.com/workitem/373)
* [Campo Aggiungi proprietari per il pacchetto](http://nuget.codeplex.com/workitem/365)
* [Aggiornare il manifesto VSIX per indicare gestione pacchetti NuGet anziché gli strumenti VSIX](http://nuget.codeplex.com/workitem/364)
* [Il comando Get-Package genera un errore quando viene selezionata l'opzione All Source](http://nuget.codeplex.com/workitem/359)
* [Consenti ordinamento delle origini pacchetti nella finestra di dialogo Opzioni](http://nuget.codeplex.com/workitem/356)
* [Update-Package non rimuove la versione precedente](http://nuget.codeplex.com/workitem/352)
* [Implementare la specifica dell'intervallo di versione per le dipendenze](http://nuget.codeplex.com/workitem/347)
* [Arresto anomalo di Visual Studio quando si fa clic su "Aggiungi nuovo pacchetto"](http://nuget.codeplex.com/workitem/346)
* [Visualizzare i download e le classificazioni nella finestra di dialogo Aggiungi pacchetto](http://nuget.codeplex.com/workitem/345)
* [La modifica tra le origini dei pacchetti nella finestra di dialogo non aggiorna l'origine attiva](http://nuget.codeplex.com/workitem/344)
* [Rimuovi chiave di associazione per la finestra della console di gestione pacchetti](http://nuget.codeplex.com/workitem/339)
* [Install-Package non è riconosciuto come nome di un cmdlet...](http://nuget.codeplex.com/workitem/338)
* [Installazione di un pacchetto da un feed locale le dipendenze dai feed normali non vengono risolte](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies deve ignorare le dipendenze ancora in uso](http://nuget.codeplex.com/workitem/331)
* [Se si annulla la navigazione tra le pagine, l'utente non può passare a una pagina diversa mentre la richiesta di pagina originale restituisce](http://nuget.codeplex.com/workitem/325)
* [Esaminare le prestazioni di NuPack. Server per servire i feed con un numero elevato di pacchetti.](http://nuget.codeplex.com/workitem/324)
* [La seconda volta che filtro per un pacchetto usa l'origine del pacchetto "New", anziché l'origine selezionata in precedenza.](http://nuget.codeplex.com/workitem/321)
* [Quando si seleziona la scheda "online" della finestra di dialogo, è necessario selezionare l'origine del pacchetto predefinita.](http://nuget.codeplex.com/workitem/320)
* [List-Package dovrebbe visualizzare i pacchetti installati per impostazione predefinita](http://nuget.codeplex.com/workitem/309)
* [Riferimento all'assembly HintPaths](http://nuget.codeplex.com/workitem/294)
* [Eccezione durante l'apertura della console di gestione pacchetti](http://nuget.codeplex.com/workitem/268)
* [L'intero feed viene scaricato da IntelliSense console](http://nuget.codeplex.com/workitem/259)
* [L'origine del pacchetto ' default ' deve essere rinominata ' Active '](http://nuget.codeplex.com/workitem/258)
* [Interfaccia utente di origini pacchetti: se si preme OK, aggiungere la nuova origine se i campi nome/origine non sono vuoti](http://nuget.codeplex.com/workitem/257)
* [La finestra di dialogo diventa molto lenta quando il numero di pacchetti installati è elevato](http://nuget.codeplex.com/workitem/243)
* [Supporto dei reindirizzamenti di binding per gli assembly con nome sicuro](http://nuget.codeplex.com/workitem/238)
* [Aggiungi riferimento al pacchetto... Interfaccia utente da includere nell'elenco a discesa per l'origine del pacchetto](http://nuget.codeplex.com/workitem/226)
* [NuPack deve supportare la trasformazione configurazione in modo indipendente dal nome del file di configurazione](http://nuget.codeplex.com/workitem/224)
* [Consente di eseguire l'override di BasePath in NuPack. exe](http://nuget.codeplex.com/workitem/222)
* [Comportamento del fallback di origine del pacchetto](http://nuget.codeplex.com/workitem/204)
* [Arresto anomalo della GUI](http://nuget.codeplex.com/workitem/201)
* [Aggiungi opzioni di ordinamento alla finestra di dialogo Aggiungi pacchetto](http://nuget.codeplex.com/workitem/179)
* [tasto di scelta rapida per cancellare la console di gestione pacchetti](http://nuget.codeplex.com/workitem/174)
* [PowerConsole causa la mancata riuscita della console NuPack](http://nuget.codeplex.com/workitem/166)
* [La finestra di dialogo Console e Aggiungi pacchetto deve impostare l'agente utente nelle richieste](http://nuget.codeplex.com/workitem/141)
* [Impostare il numero di versione di VSIX e NuPack. exe nella compilazione.](http://nuget.codeplex.com/workitem/134)
* [Nascondi parametri comuni di PowerShell da-?](http://nuget.codeplex.com/workitem/118)
* [Aggiungere la guida dettagliata per i comandi della console](http://nuget.codeplex.com/workitem/110)
* [La finestra di dialogo Aggiungi pacchetto deve consentire la scelta dell'origine del pacchetto corrente](http://nuget.codeplex.com/workitem/88)
* [Spostare le classi NuPack. Core in spazi dei nomi diversi](http://nuget.codeplex.com/workitem/50)
* [Aggiungere la guida ai cmdlet](http://nuget.codeplex.com/workitem/23)
* [Verifica hash dal feed dopo il download del pacchetto](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Di seguito sono riportate le modifiche più significative apportate in CTP 2:

* Passaggio del feed del pacchetto da ATOM a un endpoint del servizio OData: se si esegue l'aggiornamento alla versione CTP2 di NuGet, assicurarsi di aggiungere l'URL seguente come origine del pacchetto: `https://feed.nuget.org/ctp2/odata/v1/`.
* Il comando Add-Package è stato rinominato in *Install-Package*.
* Il formato `.nuspec` è stato aggiornato. Il formato `.nuspec` ora include il campo *iconUrl* per specificare un'icona png 32x32 che verrà visualizzata nella finestra di dialogo Aggiungi pacchetto. Quindi, assicurarsi di impostarlo per distinguere il pacchetto. Il formato `.nuspec` include anche il nuovo campo *projectUrl* , che può essere usato per puntare a una pagina Web che fornisce ulteriori informazioni sul pacchetto.

Questa compilazione non funzionerà con i file di `.nupkg` precedenti. Se si ricevono eccezioni di riferimento null, si sta usando un vecchio file di `.nupkg` ed è necessario ricompilarlo con lo [strumento da riga di comando NuGet](http://nuget.codeplex.com/releases/52017/download/165468)aggiornato.

Di seguito è riportato un elenco di funzionalità e bug corretti per NuGet CTP 2 (non include bug per le pulizie di codice secondarie e così via).

* [Errore durante la decompressione degli assembly del pacchetto quando si specifica TargetFramework per un assembly.](http://nuget.codeplex.com/workitem/10)
* [Rendere più individuabile la finestra della console NuPack](http://nuget.codeplex.com/workitem/14)
* [ILMerge la versione di nupack. exe](http://nuget.codeplex.com/workitem/19)
* [Migliore gestione errori/eccezioni](http://nuget.codeplex.com/workitem/24)
* [[Nupack. core]: PackageManager deve gestire correttamente gli errori correlati ai feed](http://nuget.codeplex.com/workitem/28)
* [È necessaria una nuova icona per la console](http://nuget.codeplex.com/workitem/29)
* [Localizzare le stringhe nella finestra di dialogo](http://nuget.codeplex.com/workitem/38)
* [NuPack memorizza nella cache i file NuPack scaricati in memoria](http://nuget.codeplex.com/workitem/40)
* [Console di NuPack: modificare il collegamento predefinito per la visualizzazione della console](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem deve supportare i valori predefiniti per le proprietà comuni](http://nuget.codeplex.com/workitem/49)
* [L'esecuzione di nupack. exe in una cartella con un solo file nuspec deve usare tale NuSpec](http://nuget.codeplex.com/workitem/52)
* [Il menu progetto viene visualizzato anche quando non è caricato alcun progetto/soluzione](http://nuget.codeplex.com/workitem/54)
* [Build. cmd ha esito negativo in un clone pulito della codebase](http://nuget.codeplex.com/workitem/56)
* [Aggiornamenti della funzionalità disponibile](http://nuget.codeplex.com/workitem/57)
* [Finestra di dialogo: l'aggiunta di un pacchetto tramite la finestra di dialogo consente di rimuovere il prompt nella console](http://nuget.codeplex.com/workitem/73)
* [L'aggiunta di un pacchetto facendo clic su' Installa ' è spesso lenta, senza commenti visivi](http://nuget.codeplex.com/workitem/80)
* [Non è possibile individuare i pacchetti installati con aggiornamenti.](http://nuget.codeplex.com/workitem/82)
* [Non è possibile aggiornare un pacchetto installato nella finestra di dialogo.](http://nuget.codeplex.com/workitem/83)
* [Non è possibile disinstallare un pacchetto installato nella finestra di dialogo](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Aggiungi riferimento al pacchetto&hellip;&rdquo; viene visualizzato nel menu di scelta rapida dei riferimenti installati](http://nuget.codeplex.com/workitem/85)
* [Dopo l'aggiornamento di un pacchetto dalla console, viene visualizzata la versione precedente e la nuova versione installata](http://nuget.codeplex.com/workitem/86)
* [L'attività nella console, quando si usa la finestra di dialogo, scompare dopo l'uso](http://nuget.codeplex.com/workitem/87)
* [Analisi della riga di comando di pulizia in nupack. exe](http://nuget.codeplex.com/workitem/89)
* [Aggiungere un nome descrittivo alle origini del pacchetto](http://nuget.codeplex.com/workitem/98)
* [Aggiornare. nuspec per supportare l'inclusione delle icone del pacchetto](http://nuget.codeplex.com/workitem/103)
* [L'interfaccia utente del feed non consente la copia dell'URL](http://nuget.codeplex.com/workitem/105)
* [Miglioramento della gestione degli errori di Remove-Package.](http://nuget.codeplex.com/workitem/107)
* [Digitando nella finestra della console dipende dallo stato attivo del cursore](http://nuget.codeplex.com/workitem/112)
* [Messaggi di errore sembrano terribili](http://nuget.codeplex.com/workitem/116)
* [Le prestazioni di Remove-Package per un pacchetto non installato non sono valide](http://nuget.codeplex.com/workitem/117)
* [La rimozione di un pacchetto ha esito negativo se non sono presenti origini pacchetti](http://nuget.codeplex.com/workitem/119)
* [Remove-Package ha esito negativo se l'origine del pacchetto non è disponibile](http://nuget.codeplex.com/workitem/120)
* [Aggiungere titolo ai metadati del pacchetto e al feed.](http://nuget.codeplex.com/workitem/125)
* [Aggiungere di nuovo il parametro-source a Add-Package](http://nuget.codeplex.com/workitem/127)
* [List-package deve avere un parametro-source](http://nuget.codeplex.com/workitem/128)
* [Aggiornare NuPack. Server in modo da richiedere all'agente utente di NuPack di scaricare il pacchetto](http://nuget.codeplex.com/workitem/142)
* [La finestra di dialogo accettazione licenza deve elencare le licenze per tutte le dipendenze che richiedono accettazione](http://nuget.codeplex.com/workitem/145)
* [Registra un errore quando viene generato un pacchetto nel feed](http://nuget.codeplex.com/workitem/150)
* [NuPack. exe non deve consentire un elemento vuoto &lt;licenseUrl&gt;](http://nuget.codeplex.com/workitem/152)
* [Rinominare list-package in Get-Package, Add-Package to Install-Package e Remove-Package per Uninstall-Package](http://nuget.codeplex.com/workitem/155)
* [Usare la voce di menu Aggiungi riferimento al pacchetto dallo strumento di spostamento della soluzione in modo anomalo in Visual Studio](http://nuget.codeplex.com/workitem/158)
* [Nell'etichetta "origini pacchetti disponibili" mancano i due punti](http://nuget.codeplex.com/workitem/160)
* [Make. NuSpec elemento XML con maiuscole e minuscole camel](http://nuget.codeplex.com/workitem/161)
* [Il manifesto di NuPack VSIX deve attivare il bit ' admin '](http://nuget.codeplex.com/workitem/162)
* [Se si esegue list-package senza feed, viene ricevuto un errore ref null](http://nuget.codeplex.com/workitem/164)
* [NuGet. exe: specificare il percorso di destinazione](http://nuget.codeplex.com/workitem/171)
* [Errori di PowerShell durante l'apertura della console Gestione pacchetti su WinXP](http://nuget.codeplex.com/workitem/175)
* [Visual Studio si blocca durante il tentativo di caricare l'elenco dei pacchetti](http://nuget.codeplex.com/workitem/176)
* [Consenti i metadati (nessun file, solo dipendenze)](http://nuget.codeplex.com/workitem/180)
* [Convertire uno script di PowerShell in un modulo PowerShell 2,0](http://nuget.codeplex.com/workitem/181)
* [PathResolver deve eliminare i caratteri jolly della porzione di percorso precedente quando viene specificata la destinazione](http://nuget.codeplex.com/workitem/183)
* [Nessuna dipendenza](http://nuget.codeplex.com/workitem/186)
* [Errore durante l'installazione di ELMAH](http://nuget.codeplex.com/workitem/192)
* [Le trasformazioni di configurazione non funzionano correttamente con &lt;configSections&gt;](http://nuget.codeplex.com/workitem/194)
* [Impossibile recuperare la variabile ' $global:p rojectCache ' perché non è stata impostata](http://nuget.codeplex.com/workitem/203)
* [Aggiungi attività MSBuild per la creazione di pacchetti NuPack](http://nuget.codeplex.com/workitem/205)
* [List-package deve supportare la ricerca e il filtro](http://nuget.codeplex.com/workitem/206)
* [Visualizza sempre un collegamento alla licenza se l'autore del pacchetto fornisce un URL di licenza](http://nuget.codeplex.com/workitem/208)
* [Eccezione occasionale "accesso negato" con Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Unit test non riusciti: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Consente un set di fallback o un set predefinito di file se non è possibile trovare una versione di specifico Framework](http://nuget.codeplex.com/workitem/223)
* [Aggiungi riferimento al pacchetto... L'interfaccia utente non è in grado di rimuovere un pacchetto](http://nuget.codeplex.com/workitem/225)
* [L'aggiunta di un riferimento al pacchetto si arresta in modo anomalo quando uno o più progetti vengono scaricati](http://nuget.codeplex.com/workitem/228)
* [La trasformazione configurazione non sembra funzionare nel file Web. debug. config](http://nuget.codeplex.com/workitem/229)
* [Impossibile generare init. ps1 in un pacchetto personalizzato](http://nuget.codeplex.com/workitem/237)
* [Quando si aggiungono i percorsi all'oggetto feed, il pulsante predefinito è impostato su OK, quindi se si preme INVIO viene chiusa automaticamente](http://nuget.codeplex.com/workitem/240)
* [Il tentativo di disinstallazione di una dipendenza verrà arrestato in modo anomalo rispetto a quando si tenta di eseguire 2 volte](http://nuget.codeplex.com/workitem/241)
* [Visualizzare l'URL del progetto nella finestra di dialogo Aggiungi pacchetto](http://nuget.codeplex.com/workitem/253)
* [Impostazione predefinita della finestra di dialogo Aggiungi pacchetto per i pacchetti installati](http://nuget.codeplex.com/workitem/254)
* [Modifica la voce di menu della finestra di dialogo Aggiungi pacchetto.](http://nuget.codeplex.com/workitem/261)
* [Rinominare gli spazi dei nomi e gli assembly](http://nuget.codeplex.com/workitem/274)
* [Rinominare il progetto NuPack in NuGet](http://nuget.codeplex.com/workitem/282)
* [Aggiungere il testo seguente nell'elenco delle dipendenze](http://nuget.codeplex.com/workitem/288)
* [Modificare il testo di accettazione della licenza nella finestra di dialogo accettazione della licenza](http://nuget.codeplex.com/workitem/291)
* [Modificare il testo nella finestra di dialogo accettazione della licenza sopra l'elenco di pacchetti](http://nuget.codeplex.com/workitem/292)
* [OData non funziona con un URL fwlink](http://nuget.codeplex.com/workitem/304)
* [Interfaccia utente di gestione pacchetti: la memorizzazione nella cache aggressiva del numero di pacchetti utilizzato per il paging](http://nuget.codeplex.com/workitem/317)
* [NuPack/NuGet-errore console di gestione pacchetti&gt;](http://nuget.codeplex.com/workitem/335)
* [Finestra di dialogo Aggiungi pacchetto Mostra l'accettazione della licenza per il pacchetto già installato](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

Di seguito è riportato un elenco di funzionalità e bug corretti per NuGet CTP 1.

* [L'estensione del pacchetto deve essere rinominata. nupack](http://nuget.codeplex.com/workitem/1)
* [Spostare il file del pacchetto nella cartella](http://nuget.codeplex.com/workitem/2)
* [Merge install &amp; aggiungere comandi PS](http://nuget.codeplex.com/workitem/3)
* [Creare alias per i cmdlet Verb-Noun](http://nuget.codeplex.com/workitem/4)
* [NuPack viene confuso quando si passa dalla soluzione in Visual Studio](http://nuget.codeplex.com/workitem/6)
* [Per impostazione predefinita, è necessario nascondere la cartella della soluzione ' Packages '](http://nuget.codeplex.com/workitem/11)
* [Aggiunta del supporto per la sostituzione dei token negli elementi di contenuto.](http://nuget.codeplex.com/workitem/12)
* [NuPack. UI deve usare l'API PackageSource](http://nuget.codeplex.com/workitem/26)
* [[Nupack. core]: PackageManager contrassegna i pacchetti come installati prima di installarli](http://nuget.codeplex.com/workitem/27)
* [L'eliminazione del progetto predefinito dalla soluzione Mostra ancora il progetto eliminato come predefinito](http://nuget.codeplex.com/workitem/30)
* [New-Package ha esito negativo con "Impossibile aggiungere parte per l'URI specificato perché è già presente nel pacchetto".](http://nuget.codeplex.com/workitem/32)
* [Rimuovere le stringhe "NuPack" dall'interfaccia utente grafica di Visual Studio](http://nuget.codeplex.com/workitem/35)
* [Aggiungere un'intestazione Apache a un file COPYRIGHT. txt](http://nuget.codeplex.com/workitem/36)
* [Rimuovere il comando Update-PackageSource](http://nuget.codeplex.com/workitem/37)
* [Gestione pacchetti inutilizzabile quando il profilo di caricamento genera un'eccezione](http://nuget.codeplex.com/workitem/39)
* [init. ps1, install. ps1 e Uninstall. ps1 devono ricevere lo stato aggiuntivo](http://nuget.codeplex.com/workitem/41)
* [Combinare pacchetti console e GUI in un unico pacchetto](http://nuget.codeplex.com/workitem/42)
* [La logica di trasformazione XML non funziona se applicata a XML che non si trovi alla radice](http://nuget.codeplex.com/workitem/43)
* [Finestra di dialogo Gestisci impostazioni origini pacchetti che non aggiorna la console NuPack](http://nuget.codeplex.com/workitem/44)
* [Interfaccia utente della console di NuPack: rinominare l'elenco a discesa ' feed pacchetto ' nell'elenco a discesa ' Package Source '](http://nuget.codeplex.com/workitem/45)
* [Opzioni della console NuPack: rinominare ' repository UI ' in modo che sia coerente con la console di NuPack](http://nuget.codeplex.com/workitem/46)
* [Errore di Add-Package in un sito Web aperto da IIS o un URL](http://nuget.codeplex.com/workitem/53)
* [L'origine di gestione pacchetti non funziona con FwLink](http://nuget.codeplex.com/workitem/55)
* [Imposta l'origine del pacchetto predefinita](http://nuget.codeplex.com/workitem/59)
* [Quando si aggiungono origini pacchetto nell'opzione, quando viene fornita una sola origine, si supponga che sia il valore predefinito.](http://nuget.codeplex.com/workitem/60)
* [L'interfaccia utente della finestra di dialogo Mostra pacchetti "recenti" falsi](http://nuget.codeplex.com/workitem/62)
* [Opzioni: se si fa clic su Annulla non vengono annullate modifiche](http://nuget.codeplex.com/workitem/63)
* [La ricerca della finestra di dialogo Aggiungi riferimento al pacchetto non deve essere applicata](http://nuget.codeplex.com/workitem/65)
* [Correzione dei metadati aziendali nei file AssemblyInfo.cs](http://nuget.codeplex.com/workitem/67)
* [Numero di versione per VSIX](http://nuget.codeplex.com/workitem/71)
* [Remove-Package: uso di-? Visualizza la guida due volte](http://nuget.codeplex.com/workitem/72)
* [Esegui pacchetti di installazione/disinstallazione per i pacchetti a livello di progetto](http://nuget.codeplex.com/workitem/74)
* [Il server non riesce a creare il feed quando la convalida di una nupack non riesce](http://nuget.codeplex.com/workitem/90)
* [È necessario sostituire le icone NuPack](http://nuget.codeplex.com/workitem/94)
* [Il proxy http NTLM non esegue l'autenticazione nel feed del pacchetto.](http://nuget.codeplex.com/workitem/96)
* [La finestra di dialogo non viene sempre avviata al centro nella finestra di Visual Studio](http://nuget.codeplex.com/workitem/100)
* [Molti dei campi nei dettagli di un pacchetto non vengono popolati nella finestra di dialogo](http://nuget.codeplex.com/workitem/102)
* [L'interfaccia utente di dialogo non Mostra i nomi degli autori](http://nuget.codeplex.com/workitem/108)
* [Motivo-versione per Remove-Package](http://nuget.codeplex.com/workitem/113)
* [Rimuovere la scheda recenti nell'interfaccia utente della finestra di dialogo](http://nuget.codeplex.com/workitem/115)
* [VS crash quando si fa clic con il pulsante destro del mouse sulla cartella della soluzione dopo aver aperto l'interfaccia utente della finestra](http://nuget.codeplex.com/workitem/126)
* [Modificare il parametro-local di List-package in-installato](http://nuget.codeplex.com/workitem/129)
* [Rinominare Packages. XML in NuPack. config](http://nuget.codeplex.com/workitem/132)
* [La console forza il cursore alla fine della riga](http://nuget.codeplex.com/workitem/135)
* [Remove-Package IntelliSense è interruppe](http://nuget.codeplex.com/workitem/136)
* [Aggiungi flag RequireLicenseAcceptance a. NuSpec e feed](http://nuget.codeplex.com/workitem/137)
* [Aggiungere LicenseUrl al formato. NuSpec e al feed del pacchetto](http://nuget.codeplex.com/workitem/138)
* [Fare clic su Installa per il pacchetto che richiede l'accettazione dovrebbe visualizzare la finestra di dialogo accettazione](http://nuget.codeplex.com/workitem/139)
* [Aggiungere il testo della dichiarazione di non responsabilità alla finestra di dialogo Aggiungi pacchetto](http://nuget.codeplex.com/workitem/140)
* [Aggiungere una dichiarazione di non responsabilità quando la console del pacchetto viene eseguita per la prima volta](http://nuget.codeplex.com/workitem/143)
* [Visualizza la dichiarazione di non responsabilità dopo l'installazione del pacchetto nella console](http://nuget.codeplex.com/workitem/144)
* [Rinominare l'estensione nupack in. nupkg](http://nuget.codeplex.com/workitem/146)