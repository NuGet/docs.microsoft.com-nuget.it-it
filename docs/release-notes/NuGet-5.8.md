---
title: Note sulla versione di NuGet 5,8
description: Note sulla versione per NuGet 5,8, incluse nuove funzionalità, correzioni di bug e DCR.
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: 329fdf6479d0799ae4b15cc3493848ba2d999853
ms.sourcegitcommit: 650c08f8bc3d48dfd206a111e5e2aaca3001f569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2020
ms.locfileid: "97523440"
---
# <a name="nuget-58-release-notes"></a>Note sulla versione di NuGet 5,8

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio | Disponibile in .NET SDK |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16,8](https://visualstudio.microsoft.com/downloads/) | [5,0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> installato con Visual Studio 2019 con carico di lavoro .NET Core
  
> [!NOTE]
> Visual Studio 16,8, MSBuild 16,8 e .NET 5,0 richiedono NuGet.exe 5,8 o versione successiva.


## <a name="summary-whats-new-in-58"></a>Riepilogo: novità di 5,8
🎉 **Questa è la prima versione per offrire supporto completo per la creazione e il ripristino dei pacchetti NuGet destinati a .net 5,0** 🎉

* Velocizzare l'estrazione del nupkg usando MMAP/CreateFileMapping- [#9807](https://github.com/NuGet/Home/issues/9807)

* Visualizzare i dettagli della vulnerabilità del pacchetto nel riquadro dei dettagli del pacchetto dell'interfaccia utente di gestione pacchetti- [#9850](https://github.com/NuGet/Home/issues/9850)

* Verificare i pacchetti NuGet firmati con il nuovo [`dotnet nuget verify`](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-verify) comando- [#8051](https://github.com/NuGet/Home/issues/8051)

* [`dotnet add package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) supporta `--prerelease` l'opzione per aggiungere la versione più recente di un pacchetto, incluse le versioni provvisorie- [#4699](https://github.com/NuGet/Home/issues/4699)

* Cercare i pacchetti nell'interfaccia della riga di comando con il [`nuget.exe search`](https://docs.microsoft.com/nuget/reference/cli-reference/cli-ref-search) comando- [#9704](https://github.com/NuGet/Home/issues/9704)

* [`dotnet list package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-list-package) il comando supporta l' `--verbosity` opzione- [#9600](https://github.com/NuGet/Home/issues/9600)

* Abilitare l'ottimizzazione del ripristino rapido No-Op per i progetti basati su PackageReference di tipo csproj in Visual Studio- [#9565](https://github.com/NuGet/Home/issues/9565)

* Le operazioni dell'interfaccia utente di gestione pacchetti a livello di soluzione, ad esempio le installazioni e gli aggiornamenti del pacchetto, sono [#6010](https://github.com/NuGet/Home/issues/6010) più veloci di 10

* Diversi altri miglioramenti alle prestazioni di NuGet in Visual Studio- [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984), [#10052](https://github.com/NuGet/Home/issues/10052) [#9903](https://github.com/NuGet/Home/issues/9903)


### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**DCR**

* .NET 5,0 TFM: regole di precedenza del Framework- [#9436](https://github.com/NuGet/Home/issues/9436)

* NuGet non deve dedurre la versione della piattaforma punti durante l'analisi di TargetFramework- [#9842](https://github.com/NuGet/Home/issues/9842)

* Usare TargetFrameworkMoniker & TargetPlatformMoniker per dedurre i Framework invece di usare singole proprietà TFI, TFV, TPI, TPV- [#9895](https://github.com/NuGet/Home/issues/9895)

* Aggiornamento `GetReferenceNearestTargetFrameworkTask()` per supportare i Framework di destinazione con piattaforme (ad esempio NET 5.0-Windows)- [#9894](https://github.com/NuGet/Home/issues/9894)

* API di Visual Studio per .NET 5,0- [#9650](https://github.com/NuGet/Home/issues/9650)

* Interfaccia utente di gestione pacchetti: le operazioni di consolidamento o di aggiornamento dei pacchetti non devono essere bloccate a causa di errori (downgrade del pacchetto e così via)- [#9224](https://github.com/NuGet/Home/issues/9224)

* Le funzionalità di NuGet dovrebbero essere ridotte per i progetti con funzionalità; "PackageReferences"- [#9957](https://github.com/NuGet/Home/issues/9957)

* Non visualizzare No-Op ripristinare i messaggi in Visual Studio- [#6384](https://github.com/NuGet/Home/issues/6384)

**Bug**

* Il costruttore OutputWindowTextWriter non deve essere chiamato sul thread in background [#9764](https://github.com/NuGet/Home/issues/9764)

* Ripristinare i pacchetti firmati sulle CPU big endian- [#9547](https://github.com/NuGet/Home/issues/9547)

* OutputConsoleLogger non deve chiamare metodi creata un'affinità nei costruttori MEF- [#9591](https://github.com/NuGet/Home/issues/9591)

* Bug nel metodo NuGet. CommandLine. Console `PrintJustified()` - [#9737](https://github.com/NuGet/Home/issues/9737)

* Perdita di memoria dell'interfaccia utente di gestione pacchetti quando i metadati del pacchetto vengono sottoposti a Garbage Collection a causa di un [#9757](https://github.com/NuGet/Home/issues/9757) binding non valido

* Firma Non viene visualizzato alcun avviso in Elenco errori durante l'installazione di un pacchetto firmato con packages.config formato nell'interfaccia utente di gestione pacchetti- [#9798](https://github.com/NuGet/Home/issues/9798)

* NuGet. CommandLine. XPlat non deve avere API pubbliche- [#9821](https://github.com/NuGet/Home/issues/9821)

* Ridurre la contesa di risorse in fase di caricamento della soluzione causata dal blocco di un thread del pool di thread con `BlockingCollection.Take()`  -  [#9822](https://github.com/NuGet/Home/issues/9822)

* Nel ripristino dalla riga di comando, con progetti con più destinazioni, NuGet dovrebbe leggere le informazioni correlate al Framework di destinazione dalla compilazione interna [#9869](https://github.com/NuGet/Home/issues/9869)

* Leggere il grafico dell'identificatore di runtime tramite l'elemento TargetFrameworkInformation- [#9874](https://github.com/NuGet/Home/issues/9874)

* Il ripristino statico del grafo non è coerente per quanto riguarda la proprietà CrossTargeting in rispetto a Visual Studio e il ripristino della valutazione MSBuild normale- [#9881](https://github.com/NuGet/Home/issues/9881)

* Nel ripristino statico a grafo, con progetti multitargeting, NuGet deve leggere le informazioni correlate al Framework di destinazione dalla compilazione interna. - [#9870](https://github.com/NuGet/Home/issues/9870)

* Consentire il `net5.0-platform` caricamento e il ripristino di progetti in Visual Studio: [#9863](https://github.com/NuGet/Home/issues/9863)

* Visualizzare la versione risolta nell'interfaccia utente di gestione pacchetti- [#9826](https://github.com/NuGet/Home/issues/9826)

* Interfaccia utente di gestione pacchetti: Esplora soluzioni non Visualizza tutte le dipendenze del pacchetto NuGet- [#9898](https://github.com/NuGet/Home/issues/9898)

* Aggiornare l'elenco di licenze SPDX- [#9946](https://github.com/NuGet/Home/issues/9946)

* Visual Studio 2019 si arresta in modo anomalo dopo l'apertura di Gestisci pacchetti NuGet: l'icona causa un'eccezione non gestita nell'immagine conversio- [#9696](https://github.com/NuGet/Home/issues/9696)

* NuGet. Packaging. Extraction richiede che ILMerge escluda Newtonsoft.Js[#9966](https://github.com/NuGet/Home/issues/9966)

* La compressione con ContinuePackingAfterGeneratingNuspec = false non deve avere esito negativo se non sono presenti errori- [#9786](https://github.com/NuGet/Home/issues/9786)

* Interfaccia utente di gestione pacchetti: le icone non invertono correttamente i colori- [#10017](https://github.com/NuGet/Home/issues/10017)

* Conteggi di progetti non corretti per i progetti aggiornati e No-Op in fase di ripristino- [#10026](https://github.com/NuGet/Home/issues/10026)

* L'utilizzo `/p:RestoreUseStaticGraphEvaluation=true` dei risultati in value non può essere Null [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` USA erroneamente l'alias per i progetti di libreria WPF- [#10020](https://github.com/NuGet/Home/issues/10020)

* Interfaccia utente di gestione pacchetti: NullReferenceException quando la convalida della firma ha esito negativo- [#10042](https://github.com/NuGet/Home/issues/10042)

* Codespaces: non usare il `object` tipo per i valori dei metadati del progetto- [#10055](https://github.com/NuGet/Home/issues/10055)

* Codespaces: se si salvano le origini del pacchetto nelle opzioni degli strumenti, le credenziali vengono sovrascritte [#9711](https://github.com/NuGet/Home/issues/9711)


**[Elenco di tutti i problemi risolti in questa versione-5,8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[Elenco di problemi/commit corretti in questa versione-5,8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>Contributi della community

Grazie a tutti i collaboratori che hanno contribuito a rendere questa versione di NuGet eccezionale.

|Chi|Richieste pull|Problemi|
|----|----|----|
[omajid](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | Errore di digitazione nel messaggio di errore. "amministratore" invece di "Administrator"- [#9662](https://github.com/NuGet/Home/issues/9662)
[odalet](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | Il pacchetto NuGet con i report AssemblyInformationalVersion non validi "descrizione è obbligatorio"- [#5548](https://github.com/NuGet/Home/issues/5548)
[campersau](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` non tiene conto delle proprietà del ramo e del commit- [#9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | Se si fa clic su Nu code nella finestra Elenco errori di Visual Studio, passare a https://docs.microsoft.com/nuget/reference/errors-and-warnings/  -  [#9934](https://github.com/NuGet/Home/issues/9934)
[ChrisMaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | Usare ' https://' durante l'aggiunta di una nuova origine del pacchetto tramite le opzioni di Visual Studio- [#9974](https://github.com/NuGet/Home/issues/9974)
[Therzok](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio` problemi di prestazioni in mono- [#9989](https://github.com/NuGet/Home/issues/9989)
[thomaslevesque](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | Aggiungere un oggetto TypeConverter per la classe SemanticVersion- [#9125](https://github.com/NuGet/Home/issues/9125)


## <a name="feedback-welcome"></a>Commenti e suggerimenti

I commenti degli utenti sono importanti.  Se si verificano problemi con questa versione, controllare i [problemi di GitHub](https://github.com/NuGet/Home/issues) e la [community degli sviluppatori di Visual Studio](https://developercommunity.visualstudio.com/) per i problemi esistenti.  Per i nuovi problemi in NuGet, segnalare un [problema di GitHub](https://github.com/NuGet/Home/issues/new).
Per informazioni generali sui problemi di NuGet, segnalare l'opzione [segnala un problema](https://docs.microsoft.com/visualstudio/ide/how-to-report-a-problem-with-visual-studio) nell'IDE preferito sotto la **Guida > segnalare un problema**.
