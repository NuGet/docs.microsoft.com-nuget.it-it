---
title: Note sulla versione per NuGet 4.0 RC | Microsoft Docs
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 906cc4dd-7948-4e86-a093-21df830ce8c3
description: Note sulla versione per NuGet 4.0 RTM incluse informazioni su problemi noti, correzioni di bug e DCR.
keywords: "Note sulla versione per NuGet 4.0 RTM, correzioni di bug, problemi noti, funzionalità aggiunte, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2cdee8b736fa2c651da803be9a10a6114936134a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="40-rtm-release-notes"></a>Note sulla versione per 4.0 RTM

[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) include NuGet 4.0, che aggiunge il supporto per .NET Core, oltre a varie correzioni per la qualità e miglioramenti delle prestazioni. Questa versione offre anche diversi miglioramenti come il supporto di PackageReference, i comandi NuGet come destinazioni di MSBuild, il ripristino dei pacchetti in background e altro ancora.

## <a name="known-issues"></a>Problemi noti

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a>Il ripristino di NuGet può avere esito negativo quando in una soluzione sono presenti più progetti che fanno riferimento a un altro progetto

#### <a name="issue"></a>Problema:
Il ripristino di NuGet può avere esito negativo se, in una soluzione, sono presenti riferimenti allo stesso progetto con una diversa combinazione di maiuscole e minuscole o con percorsi relativi differenti. [NuGet#4574](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a>Soluzione alternativa:
Correggere la combinazione di maiuscole e minuscole o i percorsi relativi in modo che siano identici per tutti i riferimenti al progetto.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Durante l'uso della console di Gestione pacchetti è possibile che il tasto 'INVIO' non funzioni
#### <a name="issue"></a>Problema:
A volte, nella console di Gestione pacchetti il tasto INVIO non funziona. Se si riscontra questo problema, controllare lo stato di avanzamento della correzione e fornire altre informazioni utili sui passaggi per riprodurre la condizione di errore. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Soluzione alternativa:
Riavviare Visual Studio e aprire la console di Gestione pacchetti prima di aprire la soluzione. In alternativa, provare a eliminare `project.lock.json` e ripetere il ripristino.

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>Nei progetti .NET Core, quando si usa un pacchetto contenente un assembly con una firma non valida, si verifica un ciclo infinito di ripristino
#### <a name="issue"></a>Problema:
In alcune occasioni, quando si usa un pacchetto contenente un assembly con una firma non valida o quando la versione del pacchetto è impostata con il titolo 'DateTime', è possibile che il processo di ripristino automatico del pacchetto entri in un ciclo infinito. [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>Soluzione alternativa:
Attualmente non esiste alcuna soluzione.

### <a name="you-will-be-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Non è possibile visualizzare, aggiungere o aggiornare DotNetCLITools usando Gestione pacchetti NuGet
#### <a name="issue"></a>Problema:
Gestione pacchetti NuGet non visualizza e non consente l'aggiunta e/o l'aggiornamento di DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

* #### <a name="workaround"></a>Soluzione alternativa:
È necessario modificare manualmente DotNetCLIToolReferences nel file di progetto.

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a>Quando si imposta la proprietà PackageId per i progetti, il ripristino di NuGet ha esito negativo
#### <a name="issue"></a>Problema:
Per i progetti .NET Core, il ripristino di NuGet in Visual Studio non rispetta la proprietà PackageId. [NuGet#4586](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a>Soluzione alternativa:
Eseguire il ripristino dalla riga di comando.

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a>Se nel progetto non è presente la cartella 'obj', è possibile che il ripristino abbia esito negativo
#### <a name="issue"></a>Problema:
Se la cartella 'obj' è stata eliminata, Visual Studio non è in grado di ripristinare PackageReferences. [NuGet#4528](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a>Soluzione alternativa:
Creare manualmente la cartella 'obj'. Il ripristino dovrebbe avere esito positivo. 

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a>L'aggiornamento manuale dei pacchetti usando Aggiorna pacchetto nella console può avere esito negativo
#### <a name="issue"></a>Problema:
L'aggiornamento manuale nella console mediante Aggiorna pacchetto funziona una sola volta per i progetti PackageReferences appena convertiti. [NuGet#4431](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a>Soluzione alternativa:
Attualmente non esiste alcuna soluzione.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>La ridestinazione della versione framework di destinazione può portare a informazioni Intellisense incomplete
#### <a name="issue"></a>Problema:
Se in Visual Studio si ridefinisce la destinazione della versione framework di destinazione, le informazioni Intellisense possono risultare incomplete. Questo accade quando si usa PackageReferences come formato di gestione dei pacchetti. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Soluzione alternativa:
Eseguire un ripristino manuale.

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a>`msbuild /t:restore` può avere esito negativo quando un progetto destinato a .NET461 fa riferimento a un altro progetto destinato a .NETStandard

#### <a name="issue"></a>Problema:
msbuild /t:restore può avere esito negativo quando un progetto basato su PackageReferenece e destinato a .NET461 fa riferimento a un altro progetto basato su PackageReferenece e destinato a .NETStandard.  [NuGet#4532](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a>Soluzione alternativa:
Attualmente non esiste alcuna soluzione.

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>Problemi risolti nell'intervallo di tempo NuGet 4.0 RTM

[Note sulla versione per NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md) - Vengono elencati tutti i problemi risolti per NuGet 4.0 RC

**Bug:**

* Il ripristino di NuGet in Visual Studio non rispetta la proprietà PackageId dei progetti - [#4586](https://github.com/NuGet/Home/issues/4586)

* Errore NuGet ProjectSystemCache durante l'aggiunta di un pacchetto nel pacchetto VSIX - [#4545](https://github.com/NuGet/Home/issues/4545)

* Il comando pack genera eccezioni se si usa IncludeSource in un progetto con più moniker TFM - [#4536](https://github.com/NuGet/Home/issues/4536)

* Arresti anomali di VS 2017 RC3 durante l'aggiornamento dalla gestione dei pacchetti per la soluzione - [#4474](https://github.com/NuGet/Home/issues/4474)

* Impossibile disinstallare un pacchetto appena installato - [#4435](https://github.com/NuGet/Home/issues/4435)

* Durante la migrazione a PackageRef, le soluzioni ibride hanno un comportamento strano per il ripristino - [#4433](https://github.com/NuGet/Home/issues/4433)

* L'avvio di una compilazione poco dopo aver avviato un'operazione NuGet (install, update, restore), può causare il blocco di VS - [#4420](https://github.com/NuGet/Home/issues/4420)

* Blocco dell'interfaccia utente - Deadlock durante l'inizializzazione di NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)

* Il comando add package deve aggiungere la versione come attributo anziché come elemento - [#4325](https://github.com/NuGet/Home/issues/4325)

* Dotnet restore foo.sln -- non riesce quando le configurazioni nella soluzione causano progetti duplicati (ma configurazioni diverse) nel grafico di ripristino - [#4316](https://github.com/NuGet/Home/issues/4316)

* Pacchetti di solo contenuto - [#3668](https://github.com/NuGet/Home/issues/3668)

* Per impostazione predefinita rifiuto esplicito dell'opzione per il selettore del formato del pacchetto - [#4468](https://github.com/NuGet/Home/issues/4468)

* Prestazioni: CreateUAP_CSharp_VS.01.1.Create regressione progetto Duration_TotalElapsedTime di 3.153.570 ms (149,1%). Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)

* Prestazioni: ManagedLangs_CS_DDRIT.0300.Rebuild regressione soluzione Duration_TotalElapsedTime di 1,5 sec. Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)

* Errore di denominazione in progetti con più moniker TFM - [#4419](https://github.com/NuGet/Home/issues/4419)

* Prestazioni: WebForms_DDRIT.1200.Close regressione soluzione VM_ImagesInMemory_Total_devenv di 3.000 conteggi (0,5%). Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)

* vsfeedback - Avvisi di pack con destinazione netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)

* PathTooLongException quando si tenta di aggiungere un pacchetto NuGet a un'applicazione Web ASP.NET Core vuota - [#4391](https://github.com/NuGet/Home/issues/4391)

* Esecuzione troppo frequente di pack -- dotnet pack non riesce con l'errore È presente una dipendenza circolare nel grafico di dipendenze che utilizza la destinazione "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)

* Esecuzione troppo frequente di pack - La generazione del pacchetto NuGet non include tutte le configurazioni  - [#4380](https://github.com/NuGet/Home/issues/4380)

* NullReferenceException durante l'aggiunta di nuget con packageref in un progetto C++ - [#4378](https://github.com/NuGet/Home/issues/4378)

* Accessibilità: Assistente vocale non indica la casella di controllo per selezionare i progetti in cui installare il pacchetto - [#4366](https://github.com/NuGet/Home/issues/4366)

* NuGet VS17 non riesce sporadicamente a connettersi a feed VSO/VSTS - Bug VS 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)

* L'output di contentFiles va nella posizione sbagliata se PackagePath specifica il percorso come "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)

* La destinazione della generazione del pacchetto aggiunge la proprietà PackageVersion con VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)

* La specifica del percorso del pacchetto non funziona con dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)

* NuGet genera vari avvisi per importazioni duplicate durante il ripristino - [#4304](https://github.com/NuGet/Home/issues/4304)

* La finestra di dialogo per scegliere il formato di Gestione pacchetti NuGet non ha un aspetto corretto con il tema scuro - [#4300](https://github.com/NuGet/Home/issues/4300)

* Arresto anomalo di Visual Studio durante il ripristino - [#4298](https://github.com/NuGet/Home/issues/4298)

* Deadlock di Visual Studio se si aggiunge un moniker TFM in targetframeworks, si salva e quindi si compila. 10% delle volte - [#4295](https://github.com/NuGet/Home/issues/4295)

* nuget pack non restituisce un messaggio di completamento dell'operazione per la creazione corretta del pacchetto di un progetto - [#4294](https://github.com/NuGet/Home/issues/4294)

* Errore di PackTask perché impossibile trovare System.IO.Compression 4.1 - [#4290](https://github.com/NuGet/Home/issues/4290)

* Esecuzione troppo frequente di pack - PackTask ha spesso esito negativo con conflitti di accesso al file - [#4289](https://github.com/NuGet/Home/issues/4289)

* NuGet apre la finestra di output durante il ripristino in background - [#4274](https://github.com/NuGet/Home/issues/4274)

* Eliminare ServiceProvider in quanto modello di codifica pericoloso (che può causare blocchi) - [#4268](https://github.com/NuGet/Home/issues/4268)

* Prestazioni/blocco interfaccia utente - Migliorare le letture DownloadTimeoutStream - [#4266](https://github.com/NuGet/Home/issues/4266)

* Deadlock di Visual Studio se si tenta di chiudere un progetto prima del completamento del ripristino di NuGet - [#4257](https://github.com/NuGet/Home/issues/4257)

* Problemi relativi a PackTask e alla creazione di `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)

* [vsfeedback] Impossibile risolvere pacchetti nuget per un nuovo progetto (è necessario riavviare Visual Studio) - [#4217](https://github.com/NuGet/Home/issues/4217)

* [vsfeedback] L'elenco a discesa "Versione" che mostra le versioni dei pacchetti disponibili non è ben sincronizzato con il pacchetto NuGet selezionato...  - [#4198](https://github.com/NuGet/Home/issues/4198)

* Nuget.Client deve usare CPS JoinableTaskFactory per le interazioni con CPS per evitare deadlock - [#4185](https://github.com/NuGet/Home/issues/4185)

* NuGet 3.5.0 non estrae il file `.targets` dal pacchetto - [#4171](https://github.com/NuGet/Home/issues/4171)

* dotnet pack non supporta title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)

* Install-Package genera una finestra di dialogo di errore in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)

* L'aggiornamento di un pacchetto per il progetto .NET Core sembra non funzionare, perché l'interfaccia utente non ottiene l'aggiornamento di CPS dal nominato. - [#4035](https://github.com/NuGet/Home/issues/4035)

* Migliorare l'avviso di riferimento non risolto - [#3955](https://github.com/NuGet/Home/issues/3955)

* dotnet pack - ProjectReference perde le informazioni sulla versione - [#3953](https://github.com/NuGet/Home/issues/3953)

* Regressioni del tempo totale trascorso per creare un progetto di app UWP e ricompilare - [#3873](https://github.com/NuGet/Home/issues/3873)

* Viene visualizzato un messaggio di ripristino completato anche dopo un errore durante il ripristino. - [#3799](https://github.com/NuGet/Home/issues/3799)

* Ripubblicare Nuget.CommandLine 3.4.4 in Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)

* Durante la migrazione i progetti passano da `project.json` a `.csproj` --- Il ripristino non riesce - [#4297](https://github.com/NuGet/Home/issues/4297)

* Ripristino non riuscito per un nuovo progetto di test xUnit  - [#4296](https://github.com/NuGet/Home/issues/4296)

* I progetti Core possono bloccarsi, blocco dell'interfaccia utente all'apertura - [#4269](https://github.com/NuGet/Home/issues/4269)

* Correggere il file targets per le attività di compilazione - [#4267](https://github.com/NuGet/Home/issues/4267)

* L'elenco degli errori deve includere un errore dopo la compilazione di una soluzione che scarica il progetto di riferimento - [#4208](https://github.com/NuGet/Home/issues/4208)

* MSB4057: la destinazione "_GenerateRestoreGraphProjectEntry" non è presente nel progetto. - [#4194](https://github.com/NuGet/Home/issues/4194)

* vsfeedback: arresto anomalo dell'interfaccia utente di Gestione pacchetti NuGet per la soluzione quando si selezionano tutti i progetti - [#4191](https://github.com/NuGet/Home/issues/4191)

* Errore di nuget.exe msbuildpath in presenza di una barra finale - [#4180](https://github.com/NuGet/Home/issues/4180)

* vsfeedback: NuGet restore genera vari avvisi di riferimenti al progetto per il progetto LinqToTwitter - [#4156](https://github.com/NuGet/Home/issues/4156)

* La creazione del pacchetto da `.csproj` non include l'attributo minClientVersion - [#4135](https://github.com/NuGet/Home/issues/4135)

* NuGet.Build.Tasks.Pack.dll fornito in ritardo con firma in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)

* VSFeedback: il ripristino non riesce per un progetto di VS 2015 generato con CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)

* VSFeedback: gli errori di ripristino possono nascondere i messaggi di errore più completi generati dalla compilazione - [#4113](https://github.com/NuGet/Home/issues/4113)

* [VSFeedback] Errore durante il ripristino dei pacchetti NuGet per il progetto di sito Web: Il valore non può essere null. - [#4092](https://github.com/NuGet/Home/issues/4092)

* La migrazione genera un'eccezione di riferimento a oggetto in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)

* dotnet pack deve includere nel pacchetto strumenti con le versioni usate per la compilazione del pacchetto - [#4063](https://github.com/NuGet/Home/issues/4063)

* Il nuovo ripristino in background scrive millisecondi nella barra di stato ma per il ripristino sono richiesti secondi - [#4036](https://github.com/NuGet/Home/issues/4036)

* Errore di ortografia nel messaggio di errore sulla risoluzione di tutti i riferimenti al progetto - [#4018](https://github.com/NuGet/Home/issues/4018)

* Abilitare i flussi di lavoro PCM negli scenari di riferimento ai pacchetti - [#4016](https://github.com/NuGet/Home/issues/4016)

* Impossibile trovare i pacchetti installati nell'interfaccia utente di Gestione pacchetti - [#4015](https://github.com/NuGet/Home/issues/4015)

* Errore di dotnet pack quando PackagePath è vuoto - [#3993](https://github.com/NuGet/Home/issues/3993)

* L'attività di ripristino ha esito negativo in uno scenario multiutente - [#3897](https://github.com/NuGet/Home/issues/3897)

* Impossibile modificare il tipo di contenuto quando si crea un pacchetto con l'attività nuget pack - [#3895](https://github.com/NuGet/Home/issues/3895)

* La copia predefinita di ContentFiles non è corretta per MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)

* Il ripristino di pacchetti con installazione registra due volte il messaggio di ripristino dei pacchetti - [#3785](https://github.com/NuGet/Home/issues/3785)

* Rimuovere i confini - Il ripristino della sezione "runtimes" deve essere applicato solo al progetto corrente - [#3768](https://github.com/NuGet/Home/issues/3768)

* L'attività pack posiziona i file di contenuto sia in 'content/' che in 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)

* dotnet pack3 aggiunge elementi di divisione per i tag - [#3701](https://github.com/NuGet/Home/issues/3701)

* dotnet pack: la creazione di un pacchetto di progetti con riferimenti ai pacchetti causa un avviso di importazione duplicata - [#3665](https://github.com/NuGet/Home/issues/3665)

* La registrazione del ripristino in VS non sempre viene visualizzata - [#3633](https://github.com/NuGet/Home/issues/3633)

* Il testo della Guida di nuget locals menziona ancora la cache dei pacchetti - [#3592](https://github.com/NuGet/Home/issues/3592)

* Restore3 associa PackageReferences a TargetFrameworks. - [#3504](https://github.com/NuGet/Home/issues/3504)

* Nuget sceglie una versione imprevista di MSBuild nel prompt dei comandi per gli sviluppatori in VS "15" Preview 4 - [#3408](https://github.com/NuGet/Home/issues/3408)

* Scrivere i file di destinazioni/proprietà per il ripristino non riuscito - [#3399](https://github.com/NuGet/Home/issues/3399)

* NuGet durante il ripristino non rispetta lo stesso shim di compatibilità di MSBuild durante l'esecuzione nel prompt dei comandi di VS 15 - [#3387](https://github.com/NuGet/Home/issues/3387)

* Riabilitare PackFromProjectWithDevelopmentDependencySet per VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)

* Problemi di Blend con NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)

* Integrare la versione 4.0.0.2067 nei repository CLI e SDK per includerla in RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)

* VS si blocca quando si crea una nuova app console Core, si chiude la soluzione, di apre la soluzione e si chiude la soluzione  - [#4008](https://github.com/NuGet/Home/issues/4008)

* Blocco durante l'apertura di un progetto in d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)

* Correggere il messaggio della Guida/documentazione di dotnet/nuget.exe locals - [#3919](https://github.com/NuGet/Home/issues/3919)

* Esaminare PackTask per i problemi con gli spazi vuoti iniziali o finali - [#3906](https://github.com/NuGet/Home/issues/3906)

* dotnet pack crea il pacchetto da obj e non da bin - [#3880](https://github.com/NuGet/Home/issues/3880)

* dotnet pack sembra impostare sempre la versione di ProjectReference su 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)

* dotnet pack non riesce con riferimenti a progetti e <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)

* LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)

* Tagliare lo spazio vuoto dalle proprietà di MSBuild - [#3819](https://github.com/NuGet/Home/issues/3819)

* Consolidare i due eventi di progetto generati al caricamento del progetto - [#3759](https://github.com/NuGet/Home/issues/3759)

* Versione non corretta per le librerie P2P nel file `project.assets.json` - [#3748](https://github.com/NuGet/Home/issues/3748)

* Arresto anomalo del ripristino a causa di feed che non risponde e pacchetto non disponibile - [#3672](https://github.com/NuGet/Home/issues/3672)

* nuget.exe potrebbe bloccarsi in presenza di una grande quantità di errori nell'output di MSBuild - [#3572](https://github.com/NuGet/Home/issues/3572)

* Il ripristino in fase di compilazione per Blend non riesce la prima volta, ma riesce la seconda (scenario VS corretto) - [#2121](https://github.com/NuGet/Home/issues/2121)

**DCR:**

* Eseguire la migrazione di VSIX da VSIX v2 a VSIX v3 - [#4196](https://github.com/NuGet/Home/issues/4196)

* NuGet deve disporre di un meccanismo per ottenere il percorso del file di blocco in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)

* Aggiungere gli asset di compilazione al controllo di compatibilità dei moniker TFM e al file di asset - [#3296](https://github.com/NuGet/Home/issues/3296)

* Definire un nuovo "Pack" ProjectCapability nelle destinazioni della creazione del pacchetto per abilitare le funzionalità correlate al pacchetto - [#4146](https://github.com/NuGet/Home/issues/4146)

* Eseguire pack come destinazione di post compilazione usando una condizione basata sulla proprietà di MSBuild "GeneratePackageOnBuild" - [#4145](https://github.com/NuGet/Home/issues/4145)

* Usare la proprietà NuGet RestoreProjectStyle per creare un progetto NuGet specifico - [#4134](https://github.com/NuGet/Home/issues/4134)

* Adattare il ripristino per la modifica dei riferimenti a progetti transitivi - [#4076](https://github.com/NuGet/Home/issues/4076)

* Aggiungere le proprietà NuGet nel file di destinazione per i progetti non UWP - [#4030](https://github.com/NuGet/Home/issues/4030)

* Supporto di TargetPlatformVersion UWP - [#3923](https://github.com/NuGet/Home/issues/3923)

* Comunicare i metadati dei riferimenti a progetti al sistema di progetto NuGet - [#3922](https://github.com/NuGet/Home/issues/3922)

* Aggiungere l'interfaccia utente per la modalità di creazione di pacchetti - [#3921](https://github.com/NuGet/Home/issues/3921)

* Per il file `.csproj` legacy è necessario impostare NugetTargetMoniker e RuntimeIdentifiers in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)

* L'installazione del pacchetto può sovrapporsi al ripristino automatico - [#3836](https://github.com/NuGet/Home/issues/3836)

* Lo stato dei comandi del menu di scelta rapida non viene controllato fino al caricamento di VSPackage - [#3835](https://github.com/NuGet/Home/issues/3835)

* Per il ripristino di soluzione e il ripristino di compilazione vengono ancora visualizzate finestre di dialogo - [#3789](https://github.com/NuGet/Home/issues/3789)

* Isolare la versione di VSSDK nella compilazione di soluzione NuGet.Clients - [#3890](https://github.com/NuGet/Home/issues/3890)

**Funzionalità:**

* Stringhe da localizzare in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)

* Nuget forza il caricamento dei progetti di applicazione Web in modalità di caricamento leggero delle soluzioni - [#4258](https://github.com/NuGet/Home/issues/4258)

* PackageReference con riferimenti automatici deve supportare il blocco delle modifiche di versione nell'interfaccia utente per i pacchetti installati da SDK - [#4044](https://github.com/NuGet/Home/issues/4044)

* Comunicare correttamente il valore di PackageSpec.Version per qualsiasi dipendenza di progetto (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)

* Supporto per la rimozione di riferimenti in `.csproj` dalla riga di comando - [#4101](https://github.com/NuGet/Home/issues/4101)

* Supporto del ripristino per i progetti PackageReference (normali e xplat) e il caricamento leggero delle soluzioni - [#4003](https://github.com/NuGet/Home/issues/4003)

* Supporto per l'aggiunta di riferimenti in `.csproj` dalla riga di comando - [#3751](https://github.com/NuGet/Home/issues/3751)

* Supporto del ripristino NuGet per il caricamento leggero delle soluzioni per `packages.config` o `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)

* Supporto di contentFiles nel file target generato da nuget - [#3683](https://github.com/NuGet/Home/issues/3683)

* Stabilire CI Mono per la convalida di nuget.exe su Mac con MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)

* Togliere NuGet dalle dipendenze v2 di NuGet.Core - [#3645](https://github.com/NuGet/Home/issues/3645)


## <a name="links-to-github-issues-fixed-in-rtm"></a>Collegamento ai problemi di GitHub risolti nella versione RTM
[Elenco di problemi 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RTM")  
[Elenco di problemi 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC4")  
[Elenco di problemi 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC3")  
[Elenco di problemi 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC2")  
[Elenco di problemi 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC")

