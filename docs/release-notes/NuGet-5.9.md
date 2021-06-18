---
title: Note sulla versione di NuGet 5.9
description: Note sulla versione per NuGet 5.9, tra cui nuove funzionalità, correzioni di bug e controller di dominio.
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 1152af99cf1421918a42d0d1faa33f1452f54a8f
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323882"
---
# <a name="nuget-59-release-notes"></a>Note sulla versione di NuGet 5.9

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio | Disponibile in .NET SDK |
|:---|:---|:---|
| [**5.9.0**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0.200](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.9.1**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0.202](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1 Installato</sup> con Visual Studio 2019 con carico di lavoro .NET Core
  
> [!NOTE]
> Visual Studio 16.9, MSBuild 16.9 e .NET 5.0.200+ richiedono NuGet.exe 5.9 o versione successiva.

## <a name="summary-whats-new-in-59"></a>Riepilogo: Novità nella versione 5.9

* Aggiungere la voce di menu di scelta rapida "Aggiorna" per le dipendenze dei pacchetti che avvia Gestione pacchetti'interfaccia utente con pacchetti preselezionati da aggiornare [- #10378](https://github.com/NuGet/Home/issues/10378)

    ![Fare clic con il pulsante destro del mouse sull'esperienza di aggiornamento del pacchetto](media/releasenotes-59-update.png)

* Visualizzare la versione richiesta (inclusa la richiesta di versione mobile o intervallo di versioni) nella colonna "Versione" dell'elenco di progetti nell'interfaccia utente di Gestione pacchetti soluzione - [#9827](https://github.com/NuGet/Home/issues/9827)

    ![Versione richiesta nell'interfaccia utente di Gestione pacchetti soluzione](media/releasenotes-59-requested-version.png)

* Suggerimenti per i pacchetti IntelliCode nella Gestione pacchetti sfoglia dell'interfaccia utente rilasciata come test A/B - [#10053](https://github.com/NuGet/Home/issues/10053)

* Estendere il `.nupkg.metadata` file in modo da includere l'origine dell'#10354 [](https://github.com/NuGet/Home/issues/10354)

* Introduzione di una nuova proprietà msbuild per escludere l'output di compilazione per TFM specifici durante l'attività di tipo pack [- #10396](https://github.com/NuGet/Home/issues/10396)

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**CONTROLLER di dominio (richiesta di modifica progettazione):**

* L'icona a forma di icona verso il basso quando viene installata la versione più recente del pacchetto non è intuitiva. Il segno di graduazione verde precedente era [perfetto- #9789](https://github.com/NuGet/Home/issues/9789)

* Il livello di dettaglio del debug NuGet dovrebbe pronunciare la posizione di origine di un pacchetto [#3055](https://github.com/NuGet/Home/issues/3055)

* Il pacchetto NuGet dovrebbe rilevare l'omissione non corretta del punto nei numeri di versione [#9215](https://github.com/NuGet/Home/issues/9215)

* [CPVM] Disabilitare l'aggiunta delle dipendenze transitive centrali - [#10132](https://github.com/NuGet/Home/issues/10132)

* net5 TFM: genera un errore quando manca TPV - [#9441](https://github.com/NuGet/Home/issues/9441)

* Contenuto del pacchetto di loghash durante la registrazione del ripristino (durante [l'estrazione)](https://github.com/NuGet/Home/issues/10384) - #10384

* Implementare un meccanismo di pre-registrazione per i progetti di richiesta pull legacy che chiamano il ripristino all'apertura della [soluzione - #9986](https://github.com/NuGet/Home/issues/9986)

* Lo sconsigliatore di pacchetti NuGet dovrebbe funzionare quando si seleziona più di un'origine in Gestione pacchetti [- #10433](https://github.com/NuGet/Home/issues/10433)

* Quando si esegue il ripristino al livello di dettaglio normale, registrare l'origine da cui viene ripristinato un pacchetto [#10461](https://github.com/NuGet/Home/issues/10461)

**Bug:**

* INuGetPackageFileService - Recuperare le immagini e le licenze incorporate per codespace connessi e autonomi - [#10151](https://github.com/NuGet/Home/issues/10151)

* Vs OE: formattatore mancante IProjectMetadataContextInfo - [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM-Perf] Ridurre le informazioni scritte in centralTransitiveDependencyGroups - [#10002](https://github.com/NuGet/Home/issues/10002)

* Le operazioni di ripristino che generano un'eccezione a causa di un progetto non caricato vengono segnalate `NoOp` come nei dati di telemetria [#9985](https://github.com/NuGet/Home/issues/9985)

* Le icone con alcuni color palette causano l'arresto anomalo dell'interfaccia utente di Pm - [#10037](https://github.com/NuGet/Home/issues/10037)

* [CPVM-Perf] Ridurre il clone PackageSpec quando si aggiungono le informazioni cpvm - [#10003](https://github.com/NuGet/Home/issues/10003)

* Interfaccia utente di Pm: caricamento dell'icona asyncify - [#10009](https://github.com/NuGet/Home/issues/10009)

* Ritardo dell'interfaccia utente durante il caricamento degli URL delle icone nell'interfaccia utente di Pm - [#8505](https://github.com/NuGet/Home/issues/8505)

* Affinità di thread nei thread bitmapSource e dell'interfaccia utente WPF - [#9161](https://github.com/NuGet/Home/issues/9161)

* Avviso per l'avviso NU5128 quando packastool con alias targetframework - [#10097](https://github.com/NuGet/Home/issues/10097)

* La logica di OutputPath nelle destinazioni Pack in una compilazione personalizzata non funziona correttamente- [#9234](https://github.com/NuGet/Home/issues/9234)

* Vs OE: memorizzare nella cache l'istanza di IServiceBroker nel client - [#10141](https://github.com/NuGet/Home/issues/10141)

* Rendere la creazione di NuGetProjectActions per la disinstallazione dall'interfaccia utente di Pm un'operazione parallela - [#9956](https://github.com/NuGet/Home/issues/9956)

* Prestazioni: ridurre i valori UIDelays in GetPackageSpecsAsync per progetti legacy e progetti non pr - [#9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` non inserisce più di un file , [#4393](https://github.com/NuGet/Home/issues/4393)

* L'output viene incapsulato a 80 caratteri in macOS quando viene reindirizzato - [#10198](https://github.com/NuGet/Home/issues/10198)

* Il ripristino non riesce con -Source <Relative Path>  -  [#9406](https://github.com/NuGet/Home/issues/9406)

* netcoreapp5.0-windows non round trip e non analizza le informazioni sulla piattaforma [- #10177](https://github.com/NuGet/Home/issues/10177)

* I progetti CPS personalizzati richiedono la funzionalità di progetto AssemblyReferences per il ripristino. - [#8071](https://github.com/NuGet/Home/issues/8071)

* Il controllo dell'esistenza dei file di licenza e icona deve sempre usare un confronto con distinzione tra maiuscole e [minuscole, #9817](https://github.com/NuGet/Home/issues/9817)

* I ripristini dotnetCLiToolReference rendono difficile la motivazione del conteggio/uptodateprojectscount dei progetti no-op - [#10038](https://github.com/NuGet/Home/issues/10038)

* È difficile visualizzare la casella della linea tratteggiata in formato pacchetto quando si passa da una scheda all'altro tramite la finestra di dialogo "Scegli formato Gestione pacchetti NuGet" in Tema scuro - [#9729](https://github.com/NuGet/Home/issues/9729)

* Escludere i riferimenti transitivi al framework `CollectFrameworkReferences`  -  [#10314](https://github.com/NuGet/Home/issues/10314)

* Le proprietà statiche dell'operatore di confronto devono essere idempotenti - [#10339](https://github.com/NuGet/Home/issues/10339)

* risolvere il caricamento di assembly di contratti interni (correzione di RPS o ottenere [un'eccezione)](https://github.com/NuGet/Home/issues/9919) - #9919

* Sostituire GetService con GetServiceAsync in NuGet.Clients, parte 1 - [#10362](https://github.com/NuGet/Home/issues/10362)

* Le installazioni dell'interfaccia della riga di comando non devono installare pacchetti non in elenco [- #7466](https://github.com/NuGet/Home/issues/7466)

* Ripristino di grafi msbuild statici : registrazione non anoniva su MSBuildStartupDirectory - [#10335](https://github.com/NuGet/Home/issues/10335)

* Le dipendenze di progetto di ProjectReference contrassegnate come PrivateAssets non devono essere incluse nel controllo aggiornato del file di [blocco #8565](https://github.com/NuGet/Home/issues/8565)

* Progetti SDK con dati non validi che non visualizzano errori di ripristino in Visual Studio - [#10406](https://github.com/NuGet/Home/issues/10406)

* NU1004 durante il ripristino di una soluzione con progetti legacy e netstandard2 misti dalla riga di comando con LockedMode - [#9623](https://github.com/NuGet/Home/issues/9623)

* Pack include il contenuto inserito tramite pacchetti di dipendenze nel pacchetto del progetto corrente (solo progetti basati su SDK) - [#8867](https://github.com/NuGet/Home/issues/8867)

* Aggiungere dati di telemetria per gli errori dell'API di estendibilità di Vs NuGet - [#10062](https://github.com/NuGet/Home/issues/10062)

* Aggiungere GenerateRestoreGraphFile nel ripristino di grafi statici per migliorare la debugability.  - [#10365](https://github.com/NuGet/Home/issues/10365)

* Impossibile aprire Gestione pacchetti NuGet - [#10336](https://github.com/NuGet/Home/issues/10336)

* NVDA/Assistente vocale non legge l'etichetta "Licenza" per il collegamento "Apache-2.0" - [#10425](https://github.com/NuGet/Home/issues/10425)

* Il messaggio aggiornato sulla barra di stato non è ideale in Visual Studio - [#9402](https://github.com/NuGet/Home/issues/9402)

* packages.config package.lock.jsin usa un framework di destinazione non corretto - [#10257](https://github.com/NuGet/Home/issues/10257)

* Codespaces: correggere i dati di telemetria https://github.com/NuGet/NuGet.Client/pull/3786  -  [#10439](https://github.com/NuGet/Home/issues/10439)

* L'errore NU1004 scompare durante la compilazione della soluzione dopo l'abilitazione di "RestoreLockedMode" - [#8973](https://github.com/NuGet/Home/issues/8973)

* La tabulazione tramite PMUI inversa dovrebbe rispecchiare la direzione in avanti [#10234](https://github.com/NuGet/Home/issues/10234)

* Il debug di PMUI nell'istanza sperimentale talvolta genera InvalidCastException da SolutionView a ProjectView - [#10416](https://github.com/NuGet/Home/issues/10416)

* La versione predefinita è Null dopo aver fatto clic su un pacchetto deprecato nella scheda Sfoglia - [#10380](https://github.com/NuGet/Home/issues/10380)

* Gestione NuGet in Visual Studio ricarica quando lo stato attivo viene riacquisito - [#4176](https://github.com/NuGet/Home/issues/4176)

* Rimuovere IPackageSourceProvider2 e i tipi correlati - [#10098](https://github.com/NuGet/Home/issues/10098)

* Il pacchetto 'NameOfPackage' non è compatibile con i framework 'all' nel progetto - [#5127](https://github.com/NuGet/Home/issues/5127)

* CreateVersionsAsync esegue confronti nuGetVersion non necessari - [#10436](https://github.com/NuGet/Home/issues/10436)

* NuGet.Client deve sostituire l'uso di ManagedImageMonikers con KnownMonikers - [#9977](https://github.com/NuGet/Home/issues/9977)

* L'icona deprecata si sovrappone alla versione del pacchetto deprecato nella scheda Sfoglia - [#10452](https://github.com/NuGet/Home/issues/10452)

* La gestione degli errori NU1604 PackageReference è diversa in Visual Studio e nella riga di comando (interfaccia utente di ripristino & Gestione pacchetti) - [#9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces: formattatori necessari non registrati - [#10467](https://github.com/NuGet/Home/issues/10467)

* Rimuovere net45 come framework di destinazione da NuGet.Frameworks - [#10470](https://github.com/NuGet/Home/issues/10470)

* Implementazione: aggiungere nuovi dati di telemetria per tenere traccia degli eventi correlati all'utilizzo di PowerShell e PMC. - [#10142](https://github.com/NuGet/Home/issues/10142)

* Nella finestra Anteprima modifiche viene visualizzato un solo pacchetto quando sono disponibili più pacchetti da aggiornare nell'interfaccia utente di Gestione pacchetti- [#10483](https://github.com/NuGet/Home/issues/10483)

* I gruppi frameworkReferences vuoti devono essere generati [](https://github.com/NuGet/Home/issues/10218) durante la creazione di un pacchetto di progetti con più #10218

* La casella di controllo del pacchetto nella scheda "Aggiornamenti" è incentrata su una casella tratteggiata quando si passa alla scheda nei temi Blu/Blu (contrasto aggiuntivo)/Chiaro - [#8963](https://github.com/NuGet/Home/issues/8963)

* Le caselle di controllo della scheda Aggiornamenti non funzionano correttamente con le utilità per la lettura dello schermo [- #10449](https://github.com/NuGet/Home/issues/10449)

* L'aggiornamento in PMUI fa sì che il riferimento all'oggetto non sia impostato su un'istanza di un oggetto [#9882](https://github.com/NuGet/Home/issues/9882)

* Implementazione: aggiungere nuovi dati di telemetria per tenere traccia degli eventi correlati al follow-up dell'utilizzo di PowerShell e PMC. - [#10478](https://github.com/NuGet/Home/issues/10478)

* Errore di copia e incolla in V2FeedPackageInfo - [#10480](https://github.com/NuGet/Home/issues/10480)

* Correzione di NuGetPackageFileService : uso di per memorystream eliminabile - [#10503](https://github.com/NuGet/Home/issues/10503)

**[Elenco di tutti i problemi risolti in questa versione - 5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[Elenco dei commit in questa versione - 5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>Contributi della community

Grazie a tutti i collaboratori che hanno contribuito a rendere straordinaria questa versione di NuGet.

|Chi|Prs|Problemi|
|----|----|----|
[omajid](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | Errore di copia e incolla in V2FeedPackageInfo - [#10480](https://github.com/NuGet/Home/issues/10480)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | Test mancanti per il caso in cui si fa riferimento ai pacchetti con l'attributo PrivateAssets="All" [- #10397](https://github.com/NuGet/Home/issues/10397)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | Aggiunta del supporto per il push di più pacchetti [- #4393](https://github.com/NuGet/Home/issues/4393)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | La compilazione delle librerie NuGet viene interrotta quando la firma degli assembly è [disabilitata- #10173](https://github.com/NuGet/Home/issues/10173)
[kant2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | Pulire la documentazione che contribuisce - [#10399](https://github.com/NuGet/Home/issues/10399)
[Evasodavid](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | Il controllo dell'esistenza dei file di licenza e icona deve sempre usare un confronto con distinzione tra maiuscole e [minuscole, #9817](https://github.com/NuGet/Home/issues/9817)
[campersau](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | Usare BitmapCreateOptions.IgnoreColorProfile per risolvere un problema WPF quando si usa DecodePixelWidth - [#10037](https://github.com/NuGet/Home/issues/10037)
[bjorkstromm](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | Windows SDK collegamento 10 viene interrotto nella guida ai contributi di NuGet.Client - [#10099](https://github.com/NuGet/Home/issues/10099)
[bjorkstromm](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | I collegamenti relativi vengono interrotti nella guida al debug di NuGet.Client - [#10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | Migliorare le correzioni di test e il codice correlato - [#9996](https://github.com/NuGet/Home/issues/9996)
[rolfbjarne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | L'output viene incapsulato a 80 caratteri in macOS quando viene reindirizzato [- #10198](https://github.com/NuGet/Home/issues/10198)
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | Rendere disponibile NuGet.PackageManagement come pacchetto .NET Standard - [#6150](https://github.com/NuGet/Home/issues/6150)
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | Introdurre una nuova proprietà msbuild per escludere l'output di compilazione per tfms specifici durante l'attività pack [- #10396](https://github.com/NuGet/Home/issues/10396)

## <a name="summary-whats-new-in-591"></a>Riepilogo: Novità della versione 5.9.1

* "dotnet nuget remove source nuget.org" non funziona la prima volta- [#10745](https://github.com/NuGet/Home/issues/10745)
* Rendere disabilitata la convalida predefinita in Linux, ma abilitata per impostazione predefinita in Windows - [#10713](https://github.com/NuGet/Home/issues/10713)

**[Elenco di tutti i problemi risolti in questa versione - 5.9.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f42efd068017639b4036)**

**[Elenco dei commit in questa versione - 5.9.1](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.9.1.8)**

## <a name="known-issues"></a>Problemi noti

### <a name="nuget-59-pack-raises-null-reference-exception---10685"></a>Nuget 5.9 Pack genera `Null Reference` un'eccezione. - [#10685](https://github.com/NuGet/Home/issues/10685)

#### <a name="issue"></a>Problema
Quando si usa un file, la versione genera un'eccezione se vengono specificati riferimenti espliciti all'assembly senza aggiungere alcun elemento `pack` per i progetti che hanno come destinazione `.nuspec` `NuGet 5.9` `null reference` [](../reference/nuspec.md#explicit-assembly-references) `reference groups` `multiple frameworks` .

#### <a name="workaround"></a>Soluzione alternativa
Usare `nuget.exe` [la versione 5.8.1](https://dist.nuget.org/win-x86-commandline/v5.8.1/nuget.exe)  o la versione più recente diversa da `5.9.1` .

## <a name="feedback-welcome"></a>Commenti e suggerimenti

I commenti degli utenti sono importanti.  In caso di problemi con questa versione, controllare i problemi di [GitHub](https://github.com/NuGet/Home/issues) [e](https://developercommunity.visualstudio.com/) Developer Community di Visual Studio problemi esistenti.  Per i nuovi problemi all'interno di NuGet, segnalare un [problema di GitHub.](https://github.com/NuGet/Home/issues/new)
Per problemi generali relativi all'esperienza [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) NuGet, è possibile segnalarci tramite l'opzione Segnala un problema disponibile nell'IDE preferito in Guida > **segnalare un problema**.
