---
title: Note sulla versione per NuGet 3.5 RTM
description: Note sulla versione per NuGet 3,5, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776346"
---
# <a name="nuget-35-release-notes"></a>Note sulla versione di NuGet 3,5

Note sulla versione [di NuGet 3,5-RC](../release-notes/nuget-3.5-RC.md)  |  [Note sulla versione di NuGet 4,0 RC](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Correzioni di bug

* Pack non usa MSBuild 14,1 in mono- [#3550](https://github.com/NuGet/Home/issues/3550)

* Aggiornamento scheda non selezionare la versione disponibile più recente da aggiornare invece selezionare versione installata corrente- [#3498](https://github.com/NuGet/Home/issues/3498)

* Correzione dell'arresto anomalo dopo l'autenticazione di un feed MyGet privato V2 e facendo clic su "Mostra altri x risultati"- [#3469](https://github.com/NuGet/Home/issues/3469)

* I messaggi di log sembrano essere in ordine inverso per l'interfaccia utente- [#3446](https://github.com/NuGet/Home/issues/3446)

* v 3.4.4-il ripristino di NuGet genera "il formato del percorso specificato non è supportato"- [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet cmdLine 3,6 beta non rispetta-prop Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)

* Installazione lenta di NuGet IKVM in un progetto di grandi dimensioni- [#3428](https://github.com/NuGet/Home/issues/3428)

* Aggiornamento nuget.exe-self mantiene l'aggiornamento autonomo- [#3395](https://github.com/NuGet/Home/issues/3395)

* 3,5 l'installazione o il ripristino dalla condivisione UNC presenta una regressione delle prestazioni da 3.4.4- [#3355](https://github.com/NuGet/Home/issues/3355)

* Errore durante l'installazione di MOQ dall'interfaccia utente di gestione pacchetti per un progetto net451- [#3349](https://github.com/NuGet/Home/issues/3349)

* La scheda Installa a livello di soluzione non Mostra la versione del pacchetto [#3339](https://github.com/NuGet/Home/issues/3339)

* l' `project.json` aggiornamento di xproj dalla scheda installata perde lo stato [#3303](https://github.com/NuGet/Home/issues/3303)

* Il pacchetto NuGet in `.csproj` Ignora l'elemento file vuoti nel `.nuspec` file- [#3257](https://github.com/NuGet/Home/issues/3257)

* I progetti di siti Web ospitati in IIS non devono causare la mancata riuscita del ripristino [#3235](https://github.com/NuGet/Home/issues/3235)

* Le credenziali non vengono recuperate da Nuget.Config quando l'endpoint V3 viene reindirizzato alla versione v2- [#3179](https://github.com/NuGet/Home/issues/3179)

* Il pacchetto NuGet non riesce a risolvere l'assembly durante il recupero dei metadati dell'assembly portabile- [#3128](https://github.com/NuGet/Home/issues/3128)

* Impossibile trovare NuGet `msbuild.exe` in mono- [#3085](https://github.com/NuGet/Home/issues/3085)

* nuget.exe Pack non consente un tag di versione non definitiva che inizia con numeri- [#1743](https://github.com/NuGet/Home/issues/1743)

* l'installazione del pacchetto NuGet non riesce in VS2015E- [#1298](https://github.com/NuGet/Home/issues/1298)

* il filtro allowedVersions non funziona a livello di soluzione- [#333](https://github.com/NuGet/Home/issues/333)

* Il ripristino ha esito negativo in modo casuale ed è già stato aggiunto un elemento con la stessa chiave. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Impossibile installare NuGet. Common in `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* Quando si usa l'interfaccia utente per cercare un'origine V2, FindPackagesById viene chiamato due volte per ogni ID [#2517](https://github.com/NuGet/Home/issues/2517)

* I pacchetti non possono dipendere da progetti- [#2490](https://github.com/NuGet/Home/issues/2490)

* nuget.exe Pack-Exclude è documentato ma non supportato- [#2284](https://github.com/NuGet/Home/issues/2284)

* Problemi con i messaggi di errore quando la sezione ' contentFiles ' di `.nuspec` non è valida [#1686](https://github.com/NuGet/Home/issues/1686)

* Push invia sempre due volte l'intero pacchetto con le origini dei pacchetti autenticati- [#1501](https://github.com/NuGet/Home/issues/1501)

* Non sono state fornite informazioni durante la chiamata di nuget.exe Update *. csproj mentre il progetto non dispone di un `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` il ripristino non ritenta sui codici di stato di 5xx da V2 origini- [#1217](https://github.com/NuGet/Home/issues/1217)

* Il doppio punto nel file src in `.nuspec` non funziona [#2947](https://github.com/NuGet/Home/issues/2947)

* Il ripristino di CoreCLR deve ignorare i feed con la crittografia [#2942](https://github.com/NuGet/Home/issues/2942)

* Gestione nuget.exe push 403: richiesta non corretta per le credenziali- [#2910](https://github.com/NuGet/Home/issues/2910)

* L'aggiornamento di NuGet tramite Gestione pacchetti rimuove le proprietà dalla `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* NuGet. PackageManagement. VisualStudio tenta di caricare "NuGet. TeamFoundationServer14", ma il nome della DLL è stato modificato in "NuGet. TeamFoundationServer"- [#2857](https://github.com/NuGet/Home/issues/2857)

* L'interfaccia utente di gestione pacchetti non Mostra la nuova versione aggiornata- [#2828](https://github.com/NuGet/Home/issues/2828)

* Update-Package che tenta di usare PackageID, Version anziché Package. Version- [#2771](https://github.com/NuGet/Home/issues/2771)

* NuGet Restore csproj dovrebbe essere errore se il progetto non usa NuGet ( `packages.config` o `project.json` )- [#2766](https://github.com/NuGet/Home/issues/2766)

* Errore TFS "[file] non trovato nell'area di lavoro oppure non si dispone dell'autorizzazione per accedervi" durante l'aggiornamento o la disinstallazione quando soluzione/progetto è associato al controllo del codice sorgente TFS- [#2739](https://github.com/NuGet/Home/issues/2739)

* il pacchetto di aggiornamento non ottiene le dipendenze per i pacchetti non di destinazione- [#2724](https://github.com/NuGet/Home/issues/2724)

* Non è possibile impostare il livello di dettaglio dei log per le azioni dell'interfaccia utente di gestione pacchetti NuGet- [#2705](https://github.com/NuGet/Home/issues/2705)

* la configurazione di NuGet non è valida-VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource `NuGetDefaults.Config` ( `ProgramData\NuGet` ) non funziona- [#2653](https://github.com/NuGet/Home/issues/2653)

* versione di NuGet 3.4.3: il recupero del valore non può essere null nella compilazione del pacchetto: [#2648](https://github.com/NuGet/Home/issues/2648)

* il ripristino non usa le credenziali archiviate da Nuget.Config per i feed VSTS- [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet restore]--configfile è relativo alla directory del progetto anziché alla directory cmd- [#2639](https://github.com/NuGet/Home/issues/2639)

* Allocazioni eccessive nel codice di comparsing delle versioni- [#2632](https://github.com/NuGet/Home/issues/2632)

* Più istanze di nuget.exe tentativo di installare lo stesso pacchetto in parallelo causano una doppia scrittura [#2628](https://github.com/NuGet/Home/issues/2628)

* Le informazioni sulle dipendenze non vengono memorizzate nella cache per le operazioni multiprogetto- [#2619](https://github.com/NuGet/Home/issues/2619)

* Installare e aggiornare i pacchetti di download senza controllare prima la cartella Packages- [#2618](https://github.com/NuGet/Home/issues/2618)

* Se l'elenco di origine del pacchetto è vuoto, non è possibile aggiungere l'origine del pacchetto tramite l'interfaccia utente (NuGet 3.4. x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Errore fuorviante durante il tentativo di installare il pacchetto che dipende dalle facciate della fase di progettazione. [#2594](https://github.com/NuGet/Home/issues/2594)

* L'installazione di un pacchetto dalla console di PackageManager con l'impostazione "All" prova solo la prima origine- [#2557](https://github.com/NuGet/Home/issues/2557)

* Beta più recente non decomprimere ModernHttpClient- [#2518](https://github.com/NuGet/Home/issues/2518)

* Arresto anomalo VS2015 all'avvio con NuGet a compilazione automatica 3.4.1- [#2419](https://github.com/NuGet/Home/issues/2419)

* Il comando Update potrebbe essere leggermente più dettagliato se lo chiedo...- [#2418](https://github.com/NuGet/Home/issues/2418)

* Il progetto VSIX compilato localmente deve avere le stesse dll e file della compilazione CI. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Correggere gli avvisi di downgrade NuGet nel [#2396](https://github.com/NuGet/Home/issues/2396) di compilazione

* Non è possibile autenticare l'origine del pacchetto (3 volte). il blocco è sempre [#2362](https://github.com/NuGet/Home/issues/2362)

* Il contenuto del pacchetto non viene ripristinato correttamente quando si installa un pacchetto da un feed NuGet v 3.3 + con l'argomento-NoCache quando il pacchetto contiene `.nupkg` file- [#2354](https://github.com/NuGet/Home/issues/2354)

* L'installazione di NuGet con tutte le origini dei pacchetti, ma il pacchetto mancante da 1 origine, non riesce [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet. PackageManagement. VisualStudio. VSMSBuildNuGetProjectSystem + * lt; &gt; c__DisplayClass_0 + &lt; &lt; AddReference &gt; B__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)

* Installa i blocchi se un'unica origine non riesce a eseguire l'autorizzazione- [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` l'intervallo di versioni deve eseguire l'override della versione-IncludeReferencedProjects- [#1983](https://github.com/NuGet/Home/issues/1983)

* Update-Package Super Slow: "tentativo di raccogliere informazioni sulle dipendenze"- [#1909](https://github.com/NuGet/Home/issues/1909)

* Pacchetto di downgrade Stealth di NuGet quando batch Aggiorna le dipendenze- [#1903](https://github.com/NuGet/Home/issues/1903)

* nuget.exe aggiornamento elimina il nome sicuro e l'attributo privato dell'assembly. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Percorso file relativo per "DefaultPushSource"- [#1746](https://github.com/NuGet/Home/issues/1746)

* Migliorare i messaggi di errore del resolver- [#1373](https://github.com/NuGet/Home/issues/1373)

* Update-Package in V3 ha esito negativo con i pacchetti non inclusi nell'origine specificata: [#1013](https://github.com/NuGet/Home/issues/1013)

* L'uso di percorsi relativi per le origini dei pacchetti è problematico per l'uso di- [#865](https://github.com/NuGet/Home/issues/865)

* Dipendenza mancante nel file NUPKG generato dal progetto se esiste già una dipendenza indiretta con un requisito di versione inferiore- [#759](https://github.com/NuGet/Home/issues/759)

* L'eliminazione di un progetto chiude la finestra dell'interfaccia utente corrispondente, ma la ridenominazione di un progetto non Rinomina la finestra dell'interfaccia utente. Si noti che la console di gestione delle attività è in ascolto della ridenominazione del progetto e degli [#670](https://github.com/NuGet/Home/issues/670) eventi di rimozione

* [Carico di lavoro Web Willow] Creazione di blocchi WSP per Razor v3- [#3241](https://github.com/NuGet/Home/issues/3241)

* L'installazione/ripristino di un particolare pacchetto ha esito negativo con "il pacchetto contiene più file nuspec". - [#3231](https://github.com/NuGet/Home/issues/3231)

* Scenari con ID minuscolo & `packages.config` - [#3209](https://github.com/NuGet/Home/issues/3209)

* [3,5-beta2] Il ripristino del pacchetto non riesce a ripristinare i pacchetti "Legacy"- [#3208](https://github.com/NuGet/Home/issues/3208)

* il pacchetto NuGet aggiunge in modo forzato i file con estensione TT alla cartella del contenuto indipendentemente dalla [#3203](https://github.com/NuGet/Home/issues/3203)

* Update-Package dell'app Web ASP.NET genera un avviso relativo al file: Source- [#3194](https://github.com/NuGet/Home/issues/3194)

* NuGet Pack csproj (con `project.json` ) si arresta in modo anomalo se non sono presenti packOptions e Owner nel file JSON [#3180](https://github.com/NuGet/Home/issues/3180)

* il pacchetto NuGet per `project.json` Ignora i tag packOptions come Summary, authors, owners e così via [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException tramite NuGet. Packaging. PhysicalPackageFile. GetStream- [#3160](https://github.com/NuGet/Home/issues/3160)

* Il pacchetto NuGet ignora le dipendenze nell'output `.nuspec` per `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* L'aggiornamento di più pacchetti con rollback lascia il progetto in uno stato di interruzione- [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles in any non sono stati aggiunti per i progetti netstandard- [#3118](https://github.com/NuGet/Home/issues/3118)

* Non è possibile creare un pacchetto della libreria di destinazione .NET standard correttamente- [#3108](https://github.com/NuGet/Home/issues/3108)

* File > nuovo progetto-> progetto libreria di classi (portabile) non riesce in VS2015 e Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* errore nuGet-1.0.0-* non è una stringa di versione valida- [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package non viene visualizzato ma Install-Package funziona- [#3068](https://github.com/NuGet/Home/issues/3068)

* Errore durante "Install-Package jQuery. Validation" in dev15- [#3061](https://github.com/NuGet/Home/issues/3061)

* il pacchetto NuGet di xproj viene impostato per impostazione predefinita su percorso di destinazione non valido: [#3060](https://github.com/NuGet/Home/issues/3060)

* Quando si esegue l'installazione di Visual Studio 2015 Update 3 su un Visual Studio che usa la versione NuGet 3.5.0 si verifica un errore [#3053](https://github.com/NuGet/Home/issues/3053)

* Progetto "bloccato da packages.config" in `project.json` (UWP, a. k. a Build Integrated) [#3046](https://github.com/NuGet/Home/issues/3046)

* aggiornare l'interfaccia della riga di comando DotNet installata dallo script di compilazione in Preview2-003121, che è la compilazione Preview2 ufficiale. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Interfaccia utente di gestione pacchetti: non Visualizza la nuova versione dopo l'aggiornamento di un pacchetto- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey nella riga di comando DELETE non è stato letto/inviato in 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* Stringa non corretta: una versione stabile di un pacchetto non deve avere una dipendenza della versione provvisoria. - [#3030](https://github.com/NuGet/Home/issues/3030)

* La cache OptimizedZipPackage lascia cartelle vuote- [#3029](https://github.com/NuGet/Home/issues/3029)

* Creazione dell'eccezione NullRef del progetto PCL (' net46 e Windows 10). - [#3014](https://github.com/NuGet/Home/issues/3014)

* L'aggiornamento di NuGet deve fornire un messaggio informativo quando una versione più alta è limitata dal vincolo allowedVersions- [#3013](https://github.com/NuGet/Home/issues/3013)

* Problemi di ripristino di NuGet V3- [#2891](https://github.com/NuGet/Home/issues/2891)

* Il plug-in delle credenziali è stato terminato con errore-1/errore durante il download del pacchetto quando si usano i provider di credenziali con più origini [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` il ripristino di NuGet causa la ricompilazione quando non è stato modificato nulla [#2817](https://github.com/NuGet/Home/issues/2817)

* I pacchetti di simboli non devono mai essere usati in installazione o aggiornamento- [#2807](https://github.com/NuGet/Home/issues/2807)

* VS non supporta variabili di ambiente in repositoryPath (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)

* Etichettare gli UIElement senza etichetta nell'interfaccia utente di gestione pacchetti per l'accessibilità- [#2745](https://github.com/NuGet/Home/issues/2745)

* I Framework portabili con profili con sillabazione vengono rifiutati. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Gestione pacchetti NuGet dovrebbe rendere chiaro che l'elenco di opzioni nei pacchetti non si applica ai `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe push/Delete non userà la chiave API- [#2627](https://github.com/NuGet/Home/issues/2627)

* Rimuovere la proprietà Locked dal file di blocco- [#2379](https://github.com/NuGet/Home/issues/2379)

* L'aggiornamento di NuGet 3.3.0 ha esito negativo con ' un vincolo aggiuntivo... definito in packages.config impedisce questa operazione. - [#1816](https://github.com/NuGet/Home/issues/1816)

* L'installazione di un pacchetto da un'origine locale che non esiste genera un messaggio fasullo [#1674](https://github.com/NuGet/Home/issues/1674)

* Il filtro "aggiornamento disponibile" Mostra gli aggiornamenti che violano il vincolo di versione [#1094](https://github.com/NuGet/Home/issues/1094)

* Non è possibile aggiornare i pacchetti nativi- [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Funzionalità

* Supporto dell'impostazione di CopyLocal su false nei riferimenti aggiunti da NuGet- [#329](https://github.com/NuGet/Home/issues/329)

* Supporto nuget.exe per MSBuild 15- [#1937](https://github.com/NuGet/Home/issues/1937)

* Supporto di Pack per.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Disabilitare l'azione dell'utente quando sono in esecuzione azioni utente- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet dovrebbe aggiungere il supporto per `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* Aggiungere le compatibilità del Framework mancanti in NuGet 2. x (che sono già in 3. x)- [#2720](https://github.com/NuGet/Home/issues/2720)

* Supporto per le cartelle dei pacchetti di fallback- [#2899](https://github.com/NuGet/Home/issues/2899)

* Progettare e implementare una nozione di tipo di pacchetto per supportare pacchetti di strumenti- [#2476](https://github.com/NuGet/Home/issues/2476)

* Aggiungere un'API per ottenere il percorso della cartella dei pacchetti globali- [#2403](https://github.com/NuGet/Home/issues/2403)

* Abilitare SemVer 2.0.0 in Pack- [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>DCR

* nuget.exe parametro di timeout push non funziona- [#2785](https://github.com/NuGet/Home/issues/2785)

* Il testo della descrizione del pacchetto deve essere selezionabile- [#1769](https://github.com/NuGet/Home/issues/1769)

* Abilitare nuget.exe per produrre `.props` `.targets` i file e per i `.nuproj` progetti [#2711](https://github.com/NuGet/Home/issues/2711)

* Aggiungere l'API di estensibilità per confrontare i Framework con le importazioni- [#2633](https://github.com/NuGet/Home/issues/2633)

* Nascondi le opzioni di dipendenza quando si usa `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Stampare l'intestazione della versione nuget.exe nell'output dettagliato- [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet deve informare gli utenti che l'aggiornamento o l'installazione in una libreria PCL basata su DotNet TFM può causare problemi: [#3138](https://github.com/NuGet/Home/issues/3138)

* Avviso di installazione/aggiornamento errato per il progetto w/TFM = "DotNet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Risolvere i problemi di prestazioni con reshaping e NuGet per Update- [#3044](https://github.com/NuGet/Home/issues/3044)

* Aggiungere il supporto per netcoreapp11 e netstandard17- [#2998](https://github.com/NuGet/Home/issues/2998)

* Utilizzare l'attributo AssemblyMetadata per le `.nuspec` sostituzioni di token- [#2851](https://github.com/NuGet/Home/issues/2851)
