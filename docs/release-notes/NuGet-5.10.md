---
title: Note sulla versione di NuGet 5.10
description: Note sulla versione per NuGet 5.10, tra cui nuove funzionalità, correzioni di bug e controller di dominio.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356539"
---
# <a name="nuget-510-release-notes"></a>Note sulla versione di NuGet 5.10

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio | Disponibile in .NET SDK |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16.10](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1 Installato</sup> con Visual Studio 2019 con carico di lavoro .NET Core
  
> [!NOTE]
> Visual Studio 16.10, MSBuild 16.10 e .NET 5.0.300+ richiede NuGet.exe 5.10 o versione successiva.

## <a name="summary-whats-new-in-510"></a>Riepilogo: Novità della versione 5.10

* Firma: implementare il comando dotnet trusted-signers - [#8053](https://github.com/NuGet/Home/issues/8053)

* Rendere disabilitata la convalida predefinita in Linux, ma abilitata per impostazione predefinita in Windows - [#10713](https://github.com/NuGet/Home/issues/10713)

* Aggiungere una variabile ENV per la verifica della firma dei pacchetti in .NET 5+ Linux/MAC - [#10742](https://github.com/NuGet/Home/issues/10742)

* Migliorare le prestazioni di installazione del nuovo pacchetto per soluzioni di grandi dimensioni - [#10166](https://github.com/NuGet/Home/issues/10166)

* Aggiungere il tipo di progetto `nfproj` all'elenco di supportedProjectExtensions per l'interfaccia della riga di comando di Nuget. - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

* Eliminare <requireLicenseAcceptance> l'elemento durante la creazione di un pacchetto di un [progetto - #5133](https://github.com/NuGet/Home/issues/5133)

* L'avviso di anteprima [CPVM] deve essere visualizzato nell'interfaccia della riga di comando dotnet - [#10226](https://github.com/NuGet/Home/issues/10226)

* Aggiornare i token di colore di sfondo e primo piano di PMUI a CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)

* [Bash bug] L'errore "operazione annullata dall'utente" viene visualizzato nella finestra Elenco errori quando si passa rapidamente da una scheda all'altra nell'interfaccia utente di PM - [#10671](https://github.com/NuGet/Home/issues/10671)

* Interfaccia utente di Pm: migliorare le prestazioni di installazione dei pacchetti a livello di soluzione - [#10210](https://github.com/NuGet/Home/issues/10210)

* Sostituire GetService con GetServiceAsync ovunque in NuGet.Clients - [#3784](https://github.com/NuGet/Home/issues/3784)

* NuGet.exe problema di prestazioni del pacchetto con `..` percorso relativo - [#5016](https://github.com/NuGet/Home/issues/5016)

* Le prestazioni del "pacchetto nuget" diminuiscono con l'aumento dei livelli nei percorsi di origine [#5706](https://github.com/NuGet/Home/issues/5706)

* NuGet non genera errori durante la creazione del pacchetto nuspec con file duplicati. - [#6941](https://github.com/NuGet/Home/issues/6941)

* Pacchetto NuGet "Il valore DateTimeOffset specificato non può essere convertito in un timestamp di file ZIP" - [#7001](https://github.com/NuGet/Home/issues/7001)

* I timestamp del file del pacchetto pack vengono spostati in base al fuso orario , [#7395](https://github.com/NuGet/Home/issues/7395)

* NU1004 deve contenere informazioni più utili- [#7696](https://github.com/NuGet/Home/issues/7696)

* [Bash bug] [Test non riuscito] Il file di blocco vuoto/in formato non valido non deve essere aggiornato quando si esegue 'dotnet restore --use-lock-file --locked-mode' - [#8640](https://github.com/NuGet/Home/issues/8640)

* NuGetVersionRange consente l'analisi di intervalli logicamente non [corretti- #9145](https://github.com/NuGet/Home/issues/9145)

* L'interfaccia utente di Pm non può mostrare un colore di sfondo distinguibile tra le origini del pacchetto selezionate e le origini del pacchetto [#9538](https://github.com/NuGet/Home/issues/9538)

* La casella di controllo per la selezione dei progetti in cui eseguire l'installazione non viene letta dall'utilità per la lettura dello [schermo- #9578](https://github.com/NuGet/Home/issues/9578)

* La selezione predefinita dell'elenco a discesa Versioni del riquadro dei dettagli deve essere Installato/Più recenteStabile nelle schede Installati/Aggiornamenti [- #9887](https://github.com/NuGet/Home/issues/9887)

* Rimuovere l'account della soluzione alternativa per alcuni SDK .NET 5 report TargetPlatformMoniker ` ,Version= `  -  [di #9913](https://github.com/NuGet/Home/issues/9913)

* Dotnet nuget verify is too quiet - [#10316](https://github.com/NuGet/Home/issues/10316)

* VersionRange non è in grado di analizzare intervalli a cifra singola [- #10342](https://github.com/NuGet/Home/issues/10342)

* Vs Solution Manager genera un'eccezione Null per durante il debug - [#10352](https://github.com/NuGet/Home/issues/10352)

* Spostare i messaggi di eccezione dell'interfaccia della riga di comando in file di risorse stringa - [#10392](https://github.com/NuGet/Home/issues/10392)

* Rimuovere il codice non valido (TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)

* Il menu di scelta rapida Aggiorna deve scorrere fino alla prima voce [selezionata- #10498](https://github.com/NuGet/Home/issues/10498)

* Dettagli PMUI della soluzione con barra orizzontale sovrapposta- [#10533](https://github.com/NuGet/Home/issues/10533)

* Firma: i dettagli della firma primaria non vengono visualizzati quando il certificato è scaduto e il timestamp non attendibile - [#10535](https://github.com/NuGet/Home/issues/10535)

* La presenza di origini non abilitate impedisce la visualizzazione dell'interfaccia utente di [PM #10541](https://github.com/NuGet/Home/issues/10541)

* I metadati del pacchetto (dettagli, deprecazione) talvolta non vengono estratti nuget.org in CodeSpaces - [#10549](https://github.com/NuGet/Home/issues/10549)

* L'inizializzazione di PMUI ha esito negativo con eccezione durante la sessione di debug [- #10559](https://github.com/NuGet/Home/issues/10559)

* Il ripristino nuget comporta un errore di controllo dell'integrità del pacchetto big endian sistema - [#10567](https://github.com/NuGet/Home/issues/10567)

* Viene generata un'eccezione FormatException anziché PackagingException - [#10595](https://github.com/NuGet/Home/issues/10595)

* CPVM - Problemi di concorrenza nell'algoritmo di grafi walking - [#10598](https://github.com/NuGet/Home/issues/10598)

* Aggiungere i dati di telemetria della versione di PowerShell [PMC](https://github.com/NuGet/Home/issues/10609) - #10609

* Migliorare le prestazioni di ordinamento di NuGetVersion - [#10611](https://github.com/NuGet/Home/issues/10611)

* Trusted-signers Add ha argomenti incoerenti- [#10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 v16.9.0: il passaggio delle schede in NuGet Gestione pacchetti da "Aggiornamenti" a "Installato" non aggiorna il frame. - [#10654](https://github.com/NuGet/Home/issues/10654)

* Rimuovere la "v" dal numero di versione in PMUI - [#10677](https://github.com/NuGet/Home/issues/10677)

* INuGetProjectService.GetInstalledPackagesAsync genera un'eccezione prima di ricevere la candidatura del sistema del progetto CPS [- #10681](https://github.com/NuGet/Home/issues/10681)

* Le icone incorporate causano l'accesso negato dall'origine "Microsoft Visual Studio pacchetti offline" nella scheda Sfoglia [- #10687](https://github.com/NuGet/Home/issues/10687)

* INuGetProjectService.GetInstalledPackagesAsync genera un'eccezione quando MSBuildProjectExtensionsPath non è impostato- [#10739](https://github.com/NuGet/Home/issues/10739)

* "dotnet nuget remove source nuget.org" non funziona la prima [volta- #10745](https://github.com/NuGet/Home/issues/10745)

* Nuget blocca un thread di pool di thread in un metodo asincrono effettuando una chiamata sincrona al thread dell'interfaccia utente [#10775](https://github.com/NuGet/Home/issues/10775)

* Strumenti -> Opzioni -> la stringa Gestione pacchetti NuGet viene troncata [- #10779](https://github.com/NuGet/Home/issues/10779)

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` è codice non valido e danneggia le prestazioni - [#10790](https://github.com/NuGet/Home/issues/10790)

* Usare l'icona incorporata nei pacchetti NuGet SDK - [#10795](https://github.com/NuGet/Home/issues/10795)

* Aggiornare l'elenco di licenze SPDX - [#10806](https://github.com/NuGet/Home/issues/10806)

**[Elenco di tutti i problemi risolti in questa versione - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[Elenco dei commit in questa versione - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>Contributi della community

Grazie a tutti i collaboratori che hanno contribuito a rendere straordinaria questa versione di NuGet.

|Chi|Prs|Problemi|
|----|----|----|
[louis-z](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | VersionRange non è in grado di analizzare intervalli a cifra singola [- #10342](https://github.com/NuGet/Home/issues/10342)
[omajid](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | L'build.sh NuGet.Client è interrotta - [#10139](https://github.com/NuGet/Home/issues/10139)
[Nirmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | L'build.sh NuGet.Client è interrotta - [#10139](https://github.com/NuGet/Home/issues/10139)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | Le prestazioni del "pacchetto nuget" diminuiscono con l'aumento dei livelli nei percorsi di origine [#5706](https://github.com/NuGet/Home/issues/5706)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | NuGet.exe problema di prestazioni del pacchetto con . percorso relativo - [#5016](https://github.com/NuGet/Home/issues/5016)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | CPVM - Problemi di concorrenza nell'algoritmo di grafi walking - [#10598](https://github.com/NuGet/Home/issues/10598)
[josesimoes](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | Aggiungere il tipo di progetto nfproj all'elenco di supportedProjectExtensions per l'interfaccia della riga di comando di Nuget. - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>Commenti e suggerimenti

I commenti degli utenti sono importanti.  Se si verificano problemi con questa versione, controllare i problemi [di GitHub](https://github.com/NuGet/Home/issues) [e](https://developercommunity.visualstudio.com/) Developer Community di Visual Studio problemi esistenti.  Per i nuovi problemi all'interno di NuGet, segnalare un [problema di GitHub.](https://github.com/NuGet/Home/issues/new)
Per problemi generali relativi all'esperienza [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) NuGet, **segnalarci** tramite l'opzione Segnala un problema disponibile nell'IDE preferito in Guida > segnalare un problema .
