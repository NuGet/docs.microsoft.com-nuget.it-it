---
title: note sulla versione di NuGet 5.8
description: Note sulla versione per NuGet 5.8, incluse nuove funzionalità, correzioni di bug e controller di dominio.
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: fca9d2d068aadec207bfbf12f3ea82af872825a5
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209930"
---
# <a name="nuget-58-release-notes"></a>note sulla versione di NuGet 5.8

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio | Disponibile in .NET SDK |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16.8](https://visualstudio.microsoft.com/downloads/) | [5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.8.1**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16.8.4](https://visualstudio.microsoft.com/downloads/) | |

<sup>1 Installato</sup> con Visual Studio 2019 con carico di lavoro .NET Core
  
> [!NOTE]
> Visual Studio 16.8, MSBuild 16.8 e .NET 5.0 richiedono NuGet.exe 5.8 o versione successiva.


## <a name="summary-whats-new-in-58"></a>Riepilogo: Novità nella versione 5.8
🎉 questa è la prima versione a offrire supporto completo per la creazione e il ripristino di pacchetti NuGet per **.NET 5.0** 🎉

* Velocizzare l'estrazione di nupkg usando mmap/CreateFileMapping - [#9807](https://github.com/NuGet/Home/issues/9807)

* Visualizzare i dettagli della vulnerabilità del pacchetto nel riquadro Gestione pacchetti dettagli del pacchetto dell'interfaccia utente - [#9850](https://github.com/NuGet/Home/issues/9850)

* Verificare i pacchetti NuGet firmati con il nuovo [`dotnet nuget verify`](/dotnet/core/tools/dotnet-nuget-verify) comando - [#8051](https://github.com/NuGet/Home/issues/8051)

* [`dotnet add package`](/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) supporta `--prerelease` l'opzione per aggiungere la versione più recente di un pacchetto, incluse le versioni non definitive - [#4699](https://github.com/NuGet/Home/issues/4699)

* Cercare i pacchetti nell'interfaccia della riga di comando [`nuget.exe search`](../reference/cli-reference/cli-ref-search.md) con il comando - [#9704](https://github.com/NuGet/Home/issues/9704)

* [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) il comando supporta `--verbosity` l'opzione [- #9600](https://github.com/NuGet/Home/issues/9600)

* Abilitare l'No-Op del ripristino rapido per progetti in stile csproj e basati su PackageReference in Visual Studio - [#9565](https://github.com/NuGet/Home/issues/9565)

* Le operazioni dell Gestione pacchetti dell'interfaccia utente a livello di soluzione, ad esempio le installazioni dei pacchetti e gli aggiornamenti, sono fino a 10 volte più veloci [#6010](https://github.com/NuGet/Home/issues/6010)

* Diversi altri miglioramenti NuGet prestazioni in Visual Studio- [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984), [#10052](https://github.com/NuGet/Home/issues/10052), [#9903](https://github.com/NuGet/Home/issues/9903)


### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**Controller di dominio:**

* TFM .NET 5.0: regole di precedenza del framework - [#9436](https://github.com/NuGet/Home/issues/9436)

* NuGet deve dedurre la versione della piattaforma dei punti durante l'analisi di TargetFramework - [#9842](https://github.com/NuGet/Home/issues/9842)

* Usare TargetFrameworkMoniker & TargetPlatformMoniker per dedurre i framework anziché usare singole proprietà TFI, TFV, TPI e TPV - [#9895](https://github.com/NuGet/Home/issues/9895)

* Aggiornamento `GetReferenceNearestTargetFrameworkTask()` per supportare framework di destinazione con piattaforme (ad esempio net5.0-windows) - [#9894](https://github.com/NuGet/Home/issues/9894)

* API di Visual Studio .NET 5.0 - [#9650](https://github.com/NuGet/Home/issues/9650)

* Gestione pacchetti Interfaccia utente: le operazioni di consolidamento o aggiornamento dei pacchetti non devono essere bloccate a causa di errori (downgrade dei pacchetti e così via) - [#9224](https://github.com/NuGet/Home/issues/9224)

* NuGet funzionalità devono essere accertate per i progetti che dispongono di tale funzionalità. "PackageReferences" - [#9957](https://github.com/NuGet/Home/issues/9957)

* Non No-Op i messaggi di ripristino Visual Studio - [#6384](https://github.com/NuGet/Home/issues/6384)

**Bug:**

* Il costruttore OutputWindowTextWriter non deve essere chiamato sul thread in background [#9764](https://github.com/NuGet/Home/issues/9764)

* Ripristinare i pacchetti firmati nelle CPU Big Endian - [#9547](https://github.com/NuGet/Home/issues/9547)

* OutputConsoleLogger non deve chiamare metodi con affinità nei costruttori MEF - [#9591](https://github.com/NuGet/Home/issues/9591)

* Bug in NuGet. Metodo CommandLine.Console `PrintJustified()` - [#9737](https://github.com/NuGet/Home/issues/9737)

* Gestione pacchetti Perdita di memoria dell'interfaccia utente quando i metadati del pacchetto vengono raccolti tramite Garbage Collection a causa di un'associazione non [#9757](https://github.com/NuGet/Home/issues/9757)

* [Firma] Non viene visualizzato alcun avviso nell'Elenco errori quando si installa un pacchetto firmato con packages.config nell'interfaccia utente di Gestione pacchetti - [#9798](https://github.com/NuGet/Home/issues/9798)

* NuGet. CommandLine.XPlat non deve avere API pubbliche - [#9821](https://github.com/NuGet/Home/issues/9821)

* Ridurre la contentione delle risorse in fase di caricamento della soluzione causata dal blocco di un thread del pool a thread `BlockingCollection.Take()`  -  [con #9822](https://github.com/NuGet/Home/issues/9822)

* Nel ripristino dalla riga di comando, con più progetti di destinazione, NuGet deve leggere le informazioni correlate al framework di destinazione dalla compilazione interna - [#9869](https://github.com/NuGet/Home/issues/9869)

* Leggere il grafico dell'identificatore di runtime tramite l'elemento TargetFrameworkInformation - [#9874](https://github.com/NuGet/Home/issues/9874)

* Il ripristino di grafi statici non è coerente per quanto riguarda la proprietà CrossTargeting in rispetto alla Visual Studio e al ripristino MSBuild valutazione regolare - [#9881](https://github.com/NuGet/Home/issues/9881)

* Nel ripristino di grafi statici, con più progetti di destinazione, NuGet devono leggere le informazioni correlate al framework di destinazione dalla compilazione interna. - [#9870](https://github.com/NuGet/Home/issues/9870)

* Consentire il caricamento e il ripristino dei progetti `net5.0-platform` in Visual Studio - [#9863](https://github.com/NuGet/Home/issues/9863)

* Visualizzare la versione risolta nell'interfaccia Gestione pacchetti interfaccia utente - [#9826](https://github.com/NuGet/Home/issues/9826)

* Gestione pacchetti Interfaccia utente: Esplora soluzioni non visualizza tutte le dipendenze NuGet pacchetto- [#9898](https://github.com/NuGet/Home/issues/9898)

* Aggiornare l'elenco di licenze SPDX - [#9946](https://github.com/NuGet/Home/issues/9946)

* Arresto anomalo di Visual Studio 2019 dopo l'apertura di Gestisci pacchetti NuGet: l'icona causa un'eccezione non gestita nel conversio di immagini - [#9696](https://github.com/NuGet/Home/issues/9696)

* NuGet. Packaging.Extraction richiede il ilmerge per escludere Newtonsoft.Jsin - [#9966](https://github.com/NuGet/Home/issues/9966)

* La creazione di un pacchetto con ContinuePackingAfterGeneratingNuspec=false non dovrebbe avere esito negativo se non sono presenti [errori #9786](https://github.com/NuGet/Home/issues/9786)

* Gestione pacchetti Interfaccia utente: le icone non inverteno correttamente i colori - [#10017](https://github.com/NuGet/Home/issues/10017)

* Conteggi dei progetti non corretti per i progetti aggiornati e No-Op in Ripristino - [#10026](https://github.com/NuGet/Home/issues/10026)

* `/p:RestoreUseStaticGraphEvaluation=true`L'uso di results in value non può essere Null - [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` usa erroneamente l'alias per i progetti di libreria WPF - [#10020](https://github.com/NuGet/Home/issues/10020)

* Gestione pacchetti Interfaccia utente: NullReferenceException quando la convalida della firma non riesce - [#10042](https://github.com/NuGet/Home/issues/10042)

* Codespaces: non usare il tipo `object` per i valori dei metadati del progetto - [#10055](https://github.com/NuGet/Home/issues/10055)

* Codespace: il salvataggio delle origini dei pacchetti nelle opzioni degli strumenti sovrascriverà le credenziali - [#9711](https://github.com/NuGet/Home/issues/9711)


**[Elenco di tutti i problemi risolti in questa versione - 5.8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[Elenco dei problemi in questa versione - 5.8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>Contributi della community

Grazie a tutti i collaboratori che hanno contribuito a rendere questa NuGet versione eccezionale.

|Chi|Prs|Problemi|
|----|----|----|
[omajid](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | Errore di digitazione nel messaggio di errore. "administator" anziché "administrator" - [#9662](https://github.com/NuGet/Home/issues/9662)
[odalet](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | NuGet Pack con report AssemblyInformationalVersion non validi "description is required" [-#5548](https://github.com/NuGet/Home/issues/5548)
[campersau](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` non è in considerazione per le proprietà Branch e Commit [- #9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | Facendo clic sul codice NU Visual Studio nella finestra Elenco errori si dovrebbe passare a [https://docs.microsoft.com/nuget/reference/errors-and-warnings/](/nuget/reference/errors-and-warnings/)  -  [#9934](https://github.com/NuGet/Home/issues/9934)
[ChrisMaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | Usare "https://" quando si aggiunge una nuova origine del pacchetto Visual Studio opzioni - [#9974](https://github.com/NuGet/Home/issues/9974)
[Therzok](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio` problema di prestazioni in Mono - [#9989](https://github.com/NuGet/Home/issues/9989)
[thomaslevesque](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | Aggiungere un typeconverter per la classe SemanticVersion - [#9125](https://github.com/NuGet/Home/issues/9125)

## <a name="summary-whats-new-in-581"></a>Riepilogo: Novità nella versione 5.8.1

* packages.config package.lock.jsin usa un framework di destinazione non corretto nella versione 5.8 - [#10257](https://github.com/NuGet/Home/issues/10257)

* 5.8 + 16.8 Non è possibile risolvere le dipendenze transitive del progetto quando si combinano PackageReference e packages.config - [#10326](https://github.com/NuGet/Home/issues/10326)

**[Elenco di tutti i problemi risolti in questa versione - 5.8.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**

**[Elenco dei commit in questa versione - 5.8.1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**

## <a name="feedback-welcome"></a>Commenti e suggerimenti

I commenti degli utenti sono importanti.  Se si verificano problemi con questa versione, vedere l'GitHub [problemi](https://github.com/NuGet/Home/issues) e Visual Studio [developer Community](https://developercommunity.visualstudio.com/) problemi esistenti.  Per nuovi problemi all'interno NuGet, segnalare un [GitHub problema](https://github.com/NuGet/Home/issues/new).
Per informazioni NuGet problemi di esperienza, è [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) possibile segnalarci tramite l'opzione Segnala un problema disponibile nell'IDE preferito in Guida > **segnala un problema**.