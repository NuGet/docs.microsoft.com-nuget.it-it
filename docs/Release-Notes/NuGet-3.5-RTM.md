---
title: Note sulla versione Beta di NuGet 3.5 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per NuGet 3.5 incluso dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "3.5 NuGet note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ee78ceb2ff032c05c0f8ef9a6623b94cc56ee0a9
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-35-release-notes"></a>Note sulla versione 3.5 di NuGet

[Note sulla versione 3.5 RC NuGet](../release-notes/nuget-3.5-RC.md) | [note sulla versione RC NuGet 4.0](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Correzioni di bug

* Service Pack non utilizza MSBuild 14.1 su mono - [#3550](https://github.com/NuGet/Home/issues/3550)

* Scheda di aggiornamento non consente di selezionare la versione più recente versione installata corrente seleziona - invece di aggiornare [#3498](https://github.com/NuGet/Home/issues/3498)

* Correzione di arresto anomalo dopo l'autenticazione una privata v2 feed MyGet e facendo clic su "Show x più risultati"- [#3469](https://github.com/NuGet/Home/issues/3469)

* Messaggi di log sembrano essere in ordine inverso per l'interfaccia utente - [#3446](https://github.com/NuGet/Home/issues/3446)

* V3.4.4 - ripristino Nuget genera un'eccezione "il formato del percorso specificato non è supportato -" [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet cmdLine 3.6 beta non rispetta - Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)

* Installare NuGet IKVM lento nel progetto di grandi dimensioni - [#3428](https://github.com/NuGet/Home/issues/3428)

* Update - Self tiene in aggiornarsi - NuGet.exe [#3395](https://github.com/NuGet/Home/issues/3395)

* installazione e ripristino 3.5 da condivisione UNC offre prestazioni regressione da 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)

* Errore durante l'installazione di Moq dalla gestione dei pacchetti dell'interfaccia utente per un progetto net451 - [#3349](https://github.com/NuGet/Home/issues/3349)

* Installazione della scheda a livello di soluzione non mostra la versione del pacchetto - [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj `project.json` aggiornamento dalla scheda installato perde lo stato - [#3303](https://github.com/NuGet/Home/issues/3303)

* Pacchetto NuGet in `.csproj` Ignora elemento file vuoti in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)

* Progetti di siti Web ospitati in IIS non dovrebbero causare ripristino esito negativo - [#3235](https://github.com/NuGet/Home/issues/3235)

* Credenziali non recuperate da NuGet. config quando endpoint v3 reindirizza a v2 - [#3179](https://github.com/NuGet/Home/issues/3179)

* Pacchetto NuGet non riesce a risolvere l'assembly durante il recupero dei metadati dell'assembly portabile - [#3128](https://github.com/NuGet/Home/issues/3128)

* Impossibile trovare NuGet `msbuild.exe` su Mono - [#3085](https://github.com/NuGet/Home/issues/3085)

* NuGet.exe pack non consente un tag di pre-release che inizia con numeri - [#1743](https://github.com/NuGet/Home/issues/1743)

* installazione del pacchetto NuGet non riesce in VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)

* attributo allowedversions valido Filtra non lavorativi a livello di soluzione - [#333](https://github.com/NuGet/Home/issues/333)

* Ripristino non riesce in modo casuale con un elemento con la stessa chiave è già stato aggiunto. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Non è possibile installare Nuget.Common in `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* Quando si utilizza l'interfaccia utente per la ricerca di un'origine V2, FindPackagesById viene chiamato due volte per ogni ID - [#2517](https://github.com/NuGet/Home/issues/2517)

* Pacchetti non possono dipendere da progetti - [#2490](https://github.com/NuGet/Home/issues/2490)

* NuGet.exe pack - Exclude è documentato ma non supportato - [#2284](https://github.com/NuGet/Home/issues/2284)

* I messaggi di problemi con l'errore quando la sezione 'contentFiles' di `.nuspec` non è valido - [#1686](https://github.com/NuGet/Home/issues/1686)

* Push invia sempre l'intero pacchetto due volte con autenticato origini pacchetto - [#1501](https://github.com/NuGet/Home/issues/1501)

* È stata fornita alcuna informazione quando la chiamata a nuget.exe *. csproj update durante il progetto non dispone di un `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config`Restore non tenterà sui codici di stato 5xx da origini V2 - [#1217](https://github.com/NuGet/Home/issues/1217)

* Coppia di punti nel file src in `.nuspec` non funziona - [#2947](https://github.com/NuGet/Home/issues/2947)

* È necessario ignorare i feed con crittografia - ripristino CoreCLR [#2942](https://github.com/NuGet/Home/issues/2942)

* NuGet.exe push gestione 403 - richiesta in modo non corretto di credenziali - [#2910](https://github.com/NuGet/Home/issues/2910)

* Gestione pacchetti NuGet aggiornamento rimuove il `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* NuGet.PackageManagement.VisualStudio tenta di caricare "NuGet.TeamFoundationServer14", ma che il nome DLL modificato in "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)

* Pacchetto di gestione dell'interfaccia utente non viene visualizzato appena aggiornata versione - [#2828](https://github.com/NuGet/Home/issues/2828)

* pacchetto di aggiornamento sta tentando di utilizzare packageid, versione anziché package.version - [#2771](https://github.com/NuGet/Home/issues/2771)

* NuGet restore csproj deve errore se il progetto non usa nuget (`packages.config` o `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)

* Errore di TFS "[file] non venga rilevato nell'area di lavoro o non si dispone dell'autorizzazione per accedervi" durante l'aggiornamento o la disinstallazione quando soluzione/progetto è associato al controllo del codice sorgente TFS - [#2739](https://github.com/NuGet/Home/issues/2739)

* pacchetto di aggiornamento non ottiene le dipendenze per i pacchetti non-destinazione - [#2724](https://github.com/NuGet/Home/issues/2724)

* Non è possibile impostare il livello di dettaglio i log per le azioni dell'interfaccia utente di gestione del pacchetto Nuget - [#2705](https://github.com/NuGet/Home/issues/2705)

* la configurazione NuGet non è valida - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) non funziona - [#2653](https://github.com/NuGet/Home/issues/2653)

* ottenere valore non può essere null in fase di compilazione - pacchetto NuGet versione 3.4.3 versione - [#2648](https://github.com/NuGet/Home/issues/2648)

* ripristino non utilizza credenziali archiviate da NuGet. config per i feed di VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet ripristino] - configfile è relativo alla directory di progetto anziché il comando dir cmd - [#2639](https://github.com/NuGet/Home/issues/2639)

* Le allocazioni eccessive nel codice di confronto versione - [#2632](https://github.com/NuGet/Home/issues/2632)

* Più istanze di nuget.exe sta tentando di installare lo stesso pacchetto in paralleli fa sì che un'operazione di scrittura double - [#2628](https://github.com/NuGet/Home/issues/2628)

* Informazioni sulle dipendenze non è stato memorizzato nella cache per le operazioni multiprogetto - [#2619](https://github.com/NuGet/Home/issues/2619)

* Installare e aggiornare i pacchetti di download senza verificare la cartella pacchetti innanzitutto - [#2618](https://github.com/NuGet/Home/issues/2618)

* Se l'elenco di origine del pacchetto è vuoto, non è possibile aggiungere l'origine del pacchetto tramite l'interfaccia utente (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Fuorviante errore durante il tentativo di installare il pacchetto che dipende dalla fase di progettazione aspetti - [#2594](https://github.com/NuGet/Home/issues/2594)

* Installa un pacchetto dalla console PackageManager con l'impostazione "All" tenta prima origine - [#2557](https://github.com/NuGet/Home/issues/2557)

* Versione beta più recente non decompressione ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)

* Arresto anomalo di VS2015 all'avvio con NuGet self-compilato 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)

* Comando di aggiornamento potrebbe essere più dettagliato se i richiede che sia necessaria.... - [#2418](https://github.com/NuGet/Home/issues/2418)

* VSIX compilato localmente la compilazione di CI deve essere la stessa DLL e file. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Risolvere gli avvisi di downgrade di NuGet nella compilazione - [#2396](https://github.com/NuGet/Home/issues/2396)

* Impossibile autenticare l'origine del pacchetto (3 volte) è bloccato per sempre - [#2362](https://github.com/NuGet/Home/issues/2362)

* Contenuto del pacchetto non verrà ripristinato correttamente quando si installa un pacchetto da nuget 3.3 + feed con l'argomento - NoCache quando il pacchetto contiene `.nupkg` file - [#2354](https://github.com/NuGet/Home/issues/2354)

* Installazione di NuGet con tutte le origini del pacchetto, ma pacchetto mancante dall'1 origine, non viene completata - [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* Installare blocchi se una singola origine si verifica un errore di autorizzazione - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec`versione intervallo deve eseguire l'override di versione - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)

* Pacchetto di aggiornamento rallentare super - "il tentativo di raccogliere informazioni sulle dipendenze" - [#1909](https://github.com/NuGet/Home/issues/1909)

* Creare un pacchetto NuGet punta a downgrade quando batch l'aggiornamento delle relative dipendenze - [#1903](https://github.com/NuGet/Home/issues/1903)

* aggiornamento di NuGet.exe elimina il nome sicuro dell'assembly e l'attributo privata. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Percorso relativo del file per "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)

* Migliorare i messaggi di errore di sistema di risoluzione - [#1373](https://github.com/NuGet/Home/issues/1373)

* pacchetto di aggiornamento v3 non riesce con pacchetti non nell'origine specificata - [#1013](https://github.com/NuGet/Home/issues/1013)

* Utilizzando i percorsi relativi per le origini pacchetto risulta problematico per utilizzare - [#865](https://github.com/NuGet/Home/issues/865)

* Manca una dipendenza nel file NUPKG generato dal progetto se dipendenza indiretta esiste già con un requisito di versione inferiore - [#759](https://github.com/NuGet/Home/issues/759)

* Eliminazione di un progetto chiude una finestra dell'interfaccia utente corrispondente, ma la ridenominazione di un progetto non comporta la ridenominazione la finestra dell'interfaccia utente. Si noti che è in ascolto PMC ridenominazione del progetto e di eventi nei progetti remove - [#670](https://github.com/NuGet/Home/issues/670)

* [Willow carico di lavoro Web] Creazione Razor v3 WSP si blocca - [#3241](https://github.com/NuGet/Home/issues/3241)

* Installazione o il ripristino di un particolare pacchetto ha esito negativo con "Pacchetto contiene più file nuspec." - [#3231](https://github.com/NuGet/Home/issues/3231)

* Minuscolo ID & `packages.config` scenari - [#3209](https://github.com/NuGet/Home/issues/3209)

* [-beta2 3.5] Ripristino del pacchetto non riesce a ripristinare i pacchetti "legacy" - [#3208](https://github.com/NuGet/Home/issues/3208)

* pacchetto NuGet aggiunge in modo forzato file con estensione tt alla cartella del contenuto indipendentemente - [#3203](https://github.com/NuGet/Home/issues/3203)

* pacchetto di aggiornamento dell'app web ASP.NET genera l'avviso relativo al file: origine - [#3194](https://github.com/NuGet/Home/issues/3194)

* NuGet pack csproj (con `project.json`) si blocca se sono non presenti packOptions e proprietario nel file JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* pacchetto NuGet per `project.json` ignora i tag packOptions come riepilogo, gli autori e proprietari e così via - [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException tramite NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)

* Pacchetto NuGet ignora le dipendenze nell'output `.nuspec` per `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Aggiornamento di più pacchetti con rollback lascia il progetto in uno stato danneggiato - [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles in presenza non vengono aggiunti per i progetti di moniker netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* Impossibile creare pacchetto libreria per .net Standard correttamente - [#3108](https://github.com/NuGet/Home/issues/3108)

* File -> Nuovo progetto -> ha esito negativo al progetto libreria di classi (portabile) VS2015 e Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* Errore di NuGet - 1.0.0-* non è una stringa di versione valida - [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package ha esito negativo per la visualizzazione, ma il funzionamento di Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Errore quando "Install-Package jquery.validation" in dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* passa al percorso di destinazione non valida - pacchetto NuGet di xproj [#3060](https://github.com/NuGet/Home/issues/3060)

* Quando è installato Visual Studio 2015 update 3 in un Visual Studio che usa NuGet si verifica l'errore di versione 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)

* "Bloccata da Packages" in `project.json` (UWP, dette anche compilazione integrato) progetto - [#3046](https://github.com/NuGet/Home/issues/3046)

* aggiornare dotnet cli installato dallo script di compilazione per preview2-003121, la compilazione di preview2 ufficiale. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Pacchetto interfaccia utente di gestione: non visualizza una nuova versione dopo aver aggiornato un pacchetto- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey nella riga di comando di eliminazione non viene in lettura/inviata 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Stringa non corretto: una versione stabile di un pacchetto non deve avere in una versione non definitiva dipendenza. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Cache OptimizedZipPackage lascia le cartelle vuote - [#3029](https://github.com/NuGet/Home/issues/3029)

* Creazione di get progetto PCL (net46 e windows 10) NullRef eccezione. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Aggiornamento di NuGet deve fornire un messaggio informativo quando una versione successiva è limitata dal vincolo di attributo allowedversions valido - [#3013](https://github.com/NuGet/Home/issues/3013)

* Problemi di ripristino NuGet v3 - [#2891](https://github.com/NuGet/Home/issues/2891)

* Plug-in credenziali chiuso con errore -1 / errore di download del pacchetto quando si utilizzano provider di credenziali con più origini - [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json`ripristino NuGet comporta la ricompilazione quando non modificato - [#2817](https://github.com/NuGet/Home/issues/2817)

* Pacchetti di simboli non devono mai essere utilizzato nell'installazione o aggiornamento - [#2807](https://github.com/NuGet/Home/issues/2807)

* Visual Studio non supporta le variabili di ambiente in repositoryPath (nuget.exe non) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Etichetta di UIElement senza etichetta nel Package Manager UI per l'accessibilità - [#2745](https://github.com/NuGet/Home/issues/2745)

* Framework portabili con profili sillabati vengono rifiutate. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Gestione pacchetti NuGet deve mettere in evidenza tale elenco di opzioni in dettaglio non è valida per i pacchetti `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet.exe push/delete non utilizzano la chiave API - [#2627](https://github.com/NuGet/Home/issues/2627)

* Rimuovere la proprietà bloccata dal file di blocco - [#2379](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0 aggiornamento ha esito negativo con '... un vincolo aggiuntivo definito nel file Packages. config impedisce questa operazione.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* L'installazione del pacchetto da un'origine locale che non esiste genera un messaggio fittizio - [#1674](https://github.com/NuGet/Home/issues/1674)

* "Aggiornamento disponibile" filtro consente di visualizzare gli aggiornamenti che violano il vincolo di versione - [#1094](https://github.com/NuGet/Home/issues/1094)

* Impossibile aggiornare i pacchetti nativi - [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Funzionalità

* Supporta l'impostazione CopyLocal su false nei riferimenti aggiunti da NuGet - [#329](https://github.com/NuGet/Home/issues/329)

* il supporto per MSBuild 15 - NuGet.exe [#1937](https://github.com/NuGet/Home/issues/1937)

* Supporto per Pack.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Disabilitare l'intervento dell'utente quando sono presenti azioni dell'utente in esecuzione- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet è necessario aggiungere il supporto per `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* Compatibilità di framework mancante in NuGet aggiungere 2. x (che sono già in 3. x) - [#2720](https://github.com/NuGet/Home/issues/2720)

* Supporto per le cartelle pacchetto fallback - [#2899](https://github.com/NuGet/Home/issues/2899)

* Progettare e implementare una nozione di tipo di pacchetto per supportare i pacchetti strumento - [#2476](https://github.com/NuGet/Home/issues/2476)

* Aggiungere un'API per ottenere il percorso della cartella di pacchetti globale - [#2403](https://github.com/NuGet/Home/issues/2403)

* Abilitare SemVer 2.0.0 Pack - [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>DCR

* NuGet.exe push: parametro di timeout non funziona - [#2785](https://github.com/NuGet/Home/issues/2785)

* Testo della descrizione del pacchetto deve essere selezionabile - [#1769](https://github.com/NuGet/Home/issues/1769)

* Abilitare nuget.exe per produrre `.props` e `.targets` file per `.nuproj` progetti [#2711](https://github.com/NuGet/Home/issues/2711)

* Aggiungere l'API da confrontare con importazioni - Framework di estendibilità [#2633](https://github.com/NuGet/Home/issues/2633)

* Nascondere le opzioni di dipendenza quando si utilizza `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Stampa l'intestazione di versione nuget.exe in output dettagliato - [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet è necessario informare gli utenti che l'aggiornamento o l'installazione in un tfm dotnet basato su PCL potrebbe provocare problemi - [#3138](https://github.com/NuGet/Home/issues/3138)

* Installazione/aggiornamento non valido per il progetto con tfm Avvisa = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)

* Risolvere i problemi di prestazioni con ReShaper e NuGet per l'aggiornamento - [#3044](https://github.com/NuGet/Home/issues/3044)

* Aggiungere il supporto netcoreapp11 e netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Attributo AssemblyMetadata sfruttare per `.nuspec` token sostituzioni - [#2851](https://github.com/NuGet/Home/issues/2851)
