---
title: Note sulla versione di NuGet 5,9
description: Note sulla versione per NuGet 5,9, incluse nuove funzionalità, correzioni di bug e DCR.
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 24933ebb51851da2583b03e7fd3e55fade5e8a18
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859569"
---
# <a name="nuget-59-release-notes"></a>Note sulla versione di NuGet 5,9

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio | Disponibile in .NET SDK |
|:---|:---|:---|
| [**5.9**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16,9](https://visualstudio.microsoft.com/downloads/) | [5,0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> installato con Visual Studio 2019 con carico di lavoro .NET Core
  
> [!NOTE]
> Visual Studio 16,9, MSBuild 16,9 e .NET 5.0.3 + richiedono NuGet.exe 5,9 o versione successiva.

## <a name="summary-whats-new-in-59"></a>Riepilogo: novità di 5,9

* Aggiungere la voce di menu di scelta rapida "Aggiorna" per le dipendenze dei pacchetti che avvia l'interfaccia utente di gestione pacchetti con pacchetti preselezionati per aggiornare- [#10378](https://github.com/NuGet/Home/issues/10378)

    ![Fare clic con il pulsante destro del mouse sull'esperienza di aggiornamento del pacchetto](media/releasenotes-59-update.png)

* Mostra la versione richiesta (inclusa la versione mobile o la richiesta di intervallo di versioni) nella colonna "versione" dell'elenco di progetti nell'interfaccia utente di gestione pacchetti a livello di soluzione- [#9827](https://github.com/NuGet/Home/issues/9827)

    ![Versione richiesta nell'interfaccia utente di gestione pacchetti a livello di soluzione](media/releasenotes-59-requested-version.png)

* Suggerimenti del pacchetto IntelliCode nella scheda Sfoglia dell'interfaccia utente di gestione pacchetti rilasciata come test A/B [#10053](https://github.com/NuGet/Home/issues/10053)

* Estendere il `.nupkg.metadata` file per includere l'origine di installazione [#10354](https://github.com/NuGet/Home/issues/10354)

* Introduce una nuova proprietà MSBuild per escludere l'output di compilazione per TFM specifici durante l'attività Pack- [#10396](https://github.com/NuGet/Home/issues/10396)

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**DCR (progettazione richiesta di modifica):**

* L'icona dell'icona verso il basso quando è installata la versione più recente del pacchetto non è intuitiva. Il vecchio segno di verde è stato perfetto [#9789](https://github.com/NuGet/Home/issues/9789)

* Il livello di dettaglio del debug NuGet deve indicare da dove proviene un pacchetto- [#3055](https://github.com/NuGet/Home/issues/3055)

* Il pacchetto NuGet dovrebbe intercettare l'omissione non corretta del punto nei numeri di versione- [#9215](https://github.com/NuGet/Home/issues/9215)

* [CPVM] Disabilitare il blocco delle dipendenze transitive centrali- [#10132](https://github.com/NuGet/Home/issues/10132)

* NET5 TFM: genera un errore quando manca TPV- [#9441](https://github.com/NuGet/Home/issues/9441)

* Contenthash del pacchetto di log durante la registrazione del ripristino (durante l'estrazione)- [#10384](https://github.com/NuGet/Home/issues/10384)

* Implementare un meccanismo di pre-registrazione per i progetti pull legacy che chiamano il ripristino alla soluzione Open- [#9986](https://github.com/NuGet/Home/issues/9986)

* Il Recommender del pacchetto NuGet dovrebbe funzionare quando più di un'origine è selezionata in Gestione pacchetti- [#10433](https://github.com/NuGet/Home/issues/10433)

* Quando si esegue il ripristino in base al livello di dettaglio normale, registrare l'origine da cui viene ripristinato un pacchetto: [#10461](https://github.com/NuGet/Home/issues/10461)

**Bug**

* INuGetPackageFileService-recupera le immagini e le licenze incorporate per gli spazi dei nomi in modalità connessa e autonoma- [#10151](https://github.com/NuGet/Home/issues/10151)

* VS OE: IProjectMetadataContextInfo del formattatore mancante- [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM-Perf] Ridurre le informazioni scritte in centralTransitiveDependencyGroups- [#10002](https://github.com/NuGet/Home/issues/10002)

* Le operazioni di ripristino generate a causa di un progetto non caricato vengono segnalate come `NoOp` nei dati di telemetria: [#9985](https://github.com/NuGet/Home/issues/9985)

* Le icone con determinati pallet dei colori causano l'arresto anomalo dell'interfaccia utente e la [#10037](https://github.com/NuGet/Home/issues/10037)

* [CPVM-Perf] Ridurre il clone di PackageSpec quando si aggiungono le informazioni di CPVM- [#10003](https://github.com/NuGet/Home/issues/10003)

* Interfaccia utente PM-caricamento dell'icona asyncify- [#10009](https://github.com/NuGet/Home/issues/10009)

* Ritardo dell'interfaccia utente durante il caricamento degli URL delle icone nell'interfaccia utente di PM- [#8505](https://github.com/NuGet/Home/issues/8505)

* Affinità di thread nei thread dell'interfaccia utente di BitmapSource e WPF- [#9161](https://github.com/NuGet/Home/issues/9161)

* Avviso per l'avviso NU5128 quando packastool con alias TargetFramework- [#10097](https://github.com/NuGet/Home/issues/10097)

* La logica OutputPath nelle destinazioni di Pack in una compilazione personalizzata non funziona correttamente [#9234](https://github.com/NuGet/Home/issues/9234)

* VS OE: istanza cache IServiceBroker nel client- [#10141](https://github.com/NuGet/Home/issues/10141)

* Creazione di NuGetProjectActions per la disinstallazione dall'interfaccia utente di PM un'operazione parallela- [#9956](https://github.com/NuGet/Home/issues/9956)

* Prestazioni: ridurre i UIDelays in GetPackageSpecsAsync per progetti legacy e non PR- [#9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` non esegue il push di più di un file- [#4393](https://github.com/NuGet/Home/issues/4393)

* L'output viene incapsulato a 80 caratteri in macOS quando viene reindirizzato- [#10198](https://github.com/NuGet/Home/issues/10198)

* Il ripristino ha esito negativo con <Relative Path>  -  [#9406](https://github.com/NuGet/Home/issues/9406) origine

* netcoreapp 5.0: Windows non round trip e non analizza le informazioni sulla piattaforma- [#10177](https://github.com/NuGet/Home/issues/10177)

* Per il ripristino, i progetti CPS personalizzati richiedono la funzionalità del progetto elemento AssemblyReferences. - [#8071](https://github.com/NuGet/Home/issues/8071)

* Il controllo dell'esistenza di una licenza e di un'icona deve sempre usare un confronto con distinzione [#9817](https://github.com/NuGet/Home/issues/9817) tra maiuscole e minuscole

* I ripristini di DotnetCLiToolReference rendono difficile la motivazione dei progetti no-op count/uptodateprojectscount- [#10038](https://github.com/NuGet/Home/issues/10038)

* È difficile visualizzare la casella della linea tratteggiata del formato del pacchetto quando si passa dalla scheda nella finestra di dialogo "Scegli formato gestione pacchetti NuGet" con tema scuro- [#9729](https://github.com/NuGet/Home/issues/9729)

* Escludi riferimenti a Framework transitivi da `CollectFrameworkReferences`  -  [#10314](https://github.com/NuGet/Home/issues/10314)

* Le proprietà statiche dell'operatore di confronto devono essere idempotente- [#10339](https://github.com/NuGet/Home/issues/10339)

* risolvere il caricamento dell'assembly dei contratti interni (correzione RPS o get Exception)- [#9919](https://github.com/NuGet/Home/issues/9919)

* Sostituire GetService con GetServiceAsync in NuGet. clients, parte 1- [#10362](https://github.com/NuGet/Home/issues/10362)

* Le installazioni dell'interfaccia della riga di comando non devono installare pacchetti non in elenco- [#7466](https://github.com/NuGet/Home/issues/7466)

* Ripristino statico del grafo MSBuild-registrazione unnnecessary su MSBuildStartupDirectory- [#10335](https://github.com/NuGet/Home/issues/10335)

* Le dipendenze del progetto di ProjectReference contrassegnate come PrivateAssets non devono essere incluse nel controllo del file di blocco aggiornato [#8565](https://github.com/NuGet/Home/issues/8565)

* Progetti SDK con dati non validi che non mostrano errori di ripristino in Visual Studio [#10406](https://github.com/NuGet/Home/issues/10406)

* NU1004 durante il ripristino di una soluzione con progetti legacy e netstandard2 misti dalla riga cmd con LockedMode- [#9623](https://github.com/NuGet/Home/issues/9623)

* Pack include il contenuto introdotto tramite i pacchetti di dipendenze nel pacchetto del progetto corrente (solo per i progetti basati su SDK)- [#8867](https://github.com/NuGet/Home/issues/8867)

* Aggiungere dati di telemetria per gli errori dell'API di Visual Studio Extensibility di NuGet- [#10062](https://github.com/NuGet/Home/issues/10062)

* Aggiungere GenerateRestoreGraphFile nel ripristino statico del grafo per migliorare il debug.  - [#10365](https://github.com/NuGet/Home/issues/10365)

* Non è possibile aprire Gestione pacchetti NuGet- [#10336](https://github.com/NuGet/Home/issues/10336)

* NVDA/Assistente vocale non sta leggendo l'etichetta "License" per "Apache-2,0" link- [#10425](https://github.com/NuGet/Home/issues/10425)

* Il messaggio della barra di stato aggiornato non è eccezionale in Visual Studio [#9402](https://github.com/NuGet/Home/issues/9402)

* packages.config package.lock.jsusa un Framework di destinazione non corretto- [#10257](https://github.com/NuGet/Home/issues/10257)

* Codespaces: correzione dei dati di telemetria da https://github.com/NuGet/NuGet.Client/pull/3786  -  [#10439](https://github.com/NuGet/Home/issues/10439)

* Errore NU1004 scompare quando si compila la soluzione dopo l'abilitazione di "RestoreLockedMode"- [#8973](https://github.com/NuGet/Home/issues/8973)

* La tabulazione tramite PMUI in senso inverso deve essere riflessa in avanti [#10234](https://github.com/NuGet/Home/issues/10234)

* Il debug di PMUI nell'istanza sperimentale a volte genera InvalidCastException da SolutionView a ProjectView- [#10416](https://github.com/NuGet/Home/issues/10416)

* La versione predefinita è null dopo aver fatto clic su un pacchetto deprecato nella scheda Sfoglia [#10380](https://github.com/NuGet/Home/issues/10380)

* Gestione NuGet in Visual Studio viene ricaricato quando lo stato attivo viene riacquisito- [#4176](https://github.com/NuGet/Home/issues/4176)

* Rimuovere IPackageSourceProvider2 e i tipi correlati- [#10098](https://github.com/NuGet/Home/issues/10098)

* Il pacchetto ' NameOfPackage ' non è compatibile con i Framework ' all'in Project- [#5127](https://github.com/NuGet/Home/issues/5127)

* CreateVersionsAsync esegue il confronto di NuGetVersion non necessari- [#10436](https://github.com/NuGet/Home/issues/10436)

* NuGet. client sostituisce l'uso di ManagedImageMonikers con KnownMonikers- [#9977](https://github.com/NuGet/Home/issues/9977)

* L'icona deprecata si sovrappone alla versione del pacchetto deprecato nella scheda Sfoglia- [#10452](https://github.com/NuGet/Home/issues/10452)

* La gestione degli errori NU1604 di PackageReference è diversa in Visual Studio e dalla riga di comando (ripristinare & interfaccia utente di gestione pacchetti)- [#9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces: formattatori necessari non registrati- [#10467](https://github.com/NuGet/Home/issues/10467)

* Rimuovere Net45 come Framework di destinazione da NuGet. Frameworks- [#10470](https://github.com/NuGet/Home/issues/10470)

* Implementazione: aggiungere nuove telemetrie per tenere traccia degli eventi correlati all'uso di PMC e PowerShell. - [#10142](https://github.com/NuGet/Home/issues/10142)

* Nella finestra Anteprima modifiche viene visualizzato un solo pacchetto quando sono disponibili più pacchetti da aggiornare nell'interfaccia utente di gestione pacchetti- [#10483](https://github.com/NuGet/Home/issues/10483)

* Quando si comprimeno progetti con più destinazioni, è necessario generare gruppi frameworkReferences vuoti: [#10218](https://github.com/NuGet/Home/issues/10218)

* È difficile visualizzare la casella di controllo del pacchetto nella scheda ' aggiornamenti ' con lo stato attivo con una casella di linea tratteggiata quando si passa attraverso la scheda in blu/blu (contrasto aggiuntivo) Temi/Light- [#8963](https://github.com/NuGet/Home/issues/8963)

* Le caselle di controllo della scheda aggiornamenti non funzionano correttamente con i lettori dello schermo- [#10449](https://github.com/NuGet/Home/issues/10449)

* L'aggiornamento in PMUI fa sì che il riferimento all'oggetto non sia impostato su un'istanza di un oggetto [#9882](https://github.com/NuGet/Home/issues/9882)

* Implementazione: aggiungere nuovi dati di telemetria per tenere traccia degli eventi correlati all'uso di PMC e PowerShell. - [#10478](https://github.com/NuGet/Home/issues/10478)

* Errore di copia e incolla in V2FeedPackageInfo- [#10480](https://github.com/NuGet/Home/issues/10480)

* Correzione di NuGetPackageFileService-uso di per MemoryStream- [#10503](https://github.com/NuGet/Home/issues/10503)


**[Elenco di tutti i problemi risolti in questa versione-5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[Elenco dei commit in questa versione-5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>Contributi della community

Grazie a tutti i collaboratori che hanno contribuito a rendere questa versione di NuGet eccezionale.

|Chi|Richieste pull|Problemi|
|----|----|----|
[omajid](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | Errore di copia e incolla in V2FeedPackageInfo- [#10480](https://github.com/NuGet/Home/issues/10480)
[Marcin-krystianc](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | Test mancanti per il caso in cui viene fatto riferimento ai pacchetti con l'attributo PrivateAssets = "All" [#10397](https://github.com/NuGet/Home/issues/10397)
[Marcin-krystianc](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | Aggiunta del supporto per il push di più pacchetti- [#4393](https://github.com/NuGet/Home/issues/4393)
[Marcin-krystianc](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | La compilazione di librerie NuGet è interruppe quando la firma degli assembly è disabilitata- [#10173](https://github.com/NuGet/Home/issues/10173)
[kant2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | Pulisci la documentazione di contributo- [#10399](https://github.com/NuGet/Home/issues/10399)
[PathogenDavid](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | Il controllo dell'esistenza di una licenza e di un'icona deve sempre usare un confronto con distinzione [#9817](https://github.com/NuGet/Home/issues/9817) tra maiuscole e minuscole
[campersau](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | Usare BitmapCreateOptions. IgnoreColorProfile per aggirare il problema WPF quando si usa DecodePixelWidth- [#10037](https://github.com/NuGet/Home/issues/10037)
[bjorkstromm](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | Il collegamento Windows SDK 10 è stato suddiviso in NuGet. Guida ai contributi client- [#10099](https://github.com/NuGet/Home/issues/10099)
[bjorkstromm](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | I collegamenti relativi vengono interrotti in NuGet. Guida al debug client- [#10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | Migliorare i dispositivi di test e il codice correlato [#9996](https://github.com/NuGet/Home/issues/9996)
[rolfbjarne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | L'output viene incapsulato a 80 caratteri in macOS quando viene reindirizzato- [#10198](https://github.com/NuGet/Home/issues/10198)
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | Rendere NuGet. PackageManagement disponibile come pacchetto di .NET Standard- [#6150](https://github.com/NuGet/Home/issues/6150)
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | Introduce una nuova proprietà MSBuild per escludere l'output di compilazione per TFM specifici durante l'attività Pack- [#10396](https://github.com/NuGet/Home/issues/10396)

## <a name="feedback-welcome"></a>Commenti e suggerimenti

I commenti degli utenti sono importanti.  Se si verificano problemi con questa versione, controllare i [problemi di GitHub](https://github.com/NuGet/Home/issues) e la [community degli sviluppatori di Visual Studio](https://developercommunity.visualstudio.com/) per i problemi esistenti.  Per i nuovi problemi in NuGet, segnalare un [problema di GitHub](https://github.com/NuGet/Home/issues/new).
Per informazioni generali sui problemi di NuGet, segnalare l'opzione [segnala un problema](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) nell'IDE preferito sotto la **Guida > segnalare un problema**.
