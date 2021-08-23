---
title: note sulla versione di NuGet 5.10
description: Note sulla versione per NuGet 5.10, incluse nuove funzionalità, correzioni di bug e controller di dominio.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 80a372074604f5c0073f78927b84de00e78acc74
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726951"
---
# <a name="nuget-510-release-notes"></a>note sulla versione di NuGet 5.10

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio | Disponibile in .NET SDK |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16.10](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1 Installato</sup> con Visual Studio 2019 con carico di lavoro .NET Core
  
> [!NOTE]
> Visual Studio 16.10, MSBuild 16.10 e .NET 5.0.300+ richiedono NuGet.exe 5.10 o versione successiva.

## <a name="summary-whats-new-in-510"></a>Riepilogo: Novità nella versione 5.10

* Firma: implementare il comando dotnet trusted-signers - [#8053](https://github.com/NuGet/Home/issues/8053)

* Rendere la convalida predefinita disabilitata in Linux, ma abilitata per impostazione predefinita Windows - [#10713](https://github.com/NuGet/Home/issues/10713)

* Aggiungere una variabile ENV per la verifica della firma dei pacchetti in .NET 5+ Linux/MAC - [#10742](https://github.com/NuGet/Home/issues/10742)

* Migliorare le prestazioni di installazione di nuovi pacchetti per soluzioni di grandi dimensioni - [#10166](https://github.com/NuGet/Home/issues/10166)

* Aggiungere il tipo di progetto `nfproj` all'elenco di supportedProjectExtensions per l'interfaccia della riga di comando di NuGet. - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

* Eliminare `<requireLicenseAcceptance>` l'elemento durante la creazione di un pacchetto di un progetto - [#5133](https://github.com/NuGet/Home/issues/5133)

* L'avviso di anteprima di [CPVM] deve essere visualizzato nell'interfaccia della riga di comando dotnet - [#10226](https://github.com/NuGet/Home/issues/10226)

* Aggiornare i token di colore di sfondo e primo piano dell'interfaccia PMUI a CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)

* [Bug Bash] L'errore "Operazione annullata dall'utente" viene visualizzato nella finestra Elenco errori quando si passa rapidamente da una scheda all'altra nell'interfaccia utente di Gestione [#10671](https://github.com/NuGet/Home/issues/10671)

* Interfaccia utente di Gestione pacchetti: migliorare le prestazioni di installazione dei pacchetti a livello di soluzione - [#10210](https://github.com/NuGet/Home/issues/10210)

* Sostituire GetService con GetServiceAsync ovunque NuGet. Client - [#3784](https://github.com/NuGet/Home/issues/3784)

* NuGet.exe problema di prestazioni del pacchetto con `..` il percorso relativo - [#5016](https://github.com/NuGet/Home/issues/5016)

* Le prestazioni di "nuget pack" diminuiscono con livelli crescenti nei percorsi di [origine, #5706](https://github.com/NuGet/Home/issues/5706)

* NuGet non si verifica un errore durante la creazione del pacchetto nuspec con file duplicati. - [#6941](https://github.com/NuGet/Home/issues/6941)

* NuGet pack "The DateTimeOffset specified cannot be converted into a Zip file timestamp" [-#7001](https://github.com/NuGet/Home/issues/7001)

* I timestamp del file del pacchetto di cui è stato fatto il pacchetto vengono spostati in base al fuso orario, [#7395](https://github.com/NuGet/Home/issues/7395)

* NU1004 deve contenere informazioni più utilizzabili - [#7696](https://github.com/NuGet/Home/issues/7696)

* [Bug Bash] [Test non riuscito] Il file di blocco vuoto/in formato non valido non deve essere aggiornato quando si esegue 'dotnet restore --use-lock-file --locked-mode' - [#8640](https://github.com/NuGet/Home/issues/8640)

* NuGetVersionRange consente l'analisi di intervalli logicamente non corretti [#9145](https://github.com/NuGet/Home/issues/9145)

* L'interfaccia utente di Gestione pacchetti non può mostrare un colore di sfondo distinguibile tra le origini pacchetto selezionate e le origini dei pacchetti con passaggio del [mouse- #9538](https://github.com/NuGet/Home/issues/9538)

* La casella di controllo per la selezione dei progetti in cui eseguire l'installazione non viene letta dall'utilità per la lettura dello schermo [- #9578](https://github.com/NuGet/Home/issues/9578)

* La selezione predefinita dell'elenco a discesa Versioni del riquadro dei dettagli deve essere Installata/Più recenteSabilita nelle schede Installati/Aggiornamenti - [#9887](https://github.com/NuGet/Home/issues/9887)

* Rimuovere l'account della soluzione alternativa per alcuni SDK .NET 5 che segnalano TargetPlatformMoniker ` ,Version= `  -  [di #9913](https://github.com/NuGet/Home/issues/9913)

* dotnet nuget verify is too quiet - [#10316](https://github.com/NuGet/Home/issues/10316)

* VersionRange non è in grado di analizzare intervalli a una cifra [- #10342](https://github.com/NuGet/Home/issues/10342)

* Gestione soluzioni di Visual Studio genera un'eccezione Null per durante il debug - [#10352](https://github.com/NuGet/Home/issues/10352)

* Spostare i messaggi di eccezione dell'interfaccia della riga di comando in file [di risorse di tipo stringa](https://github.com/NuGet/Home/issues/10392) - #10392

* Rimuovere il codice non gestito (TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)

* Il menu di scelta rapida Aggiorna dovrebbe scorrere fino al primo elemento selezionato [- #10498](https://github.com/NuGet/Home/issues/10498)

* Dettagli PMUI soluzione con barra orizzontale sovrapposta - [#10533](https://github.com/NuGet/Home/issues/10533)

* Firma: i dettagli della firma primaria non vengono visualizzati quando il certificato è scaduto e timestamp non attendibile - [#10535](https://github.com/NuGet/Home/issues/10535)

* L'assenza di origini abilitate impedisce la visualizzazione dell'interfaccia utente di Pm [- #10541](https://github.com/NuGet/Home/issues/10541)

* I metadati del pacchetto (dettagli, deprecazione) talvolta non vengono estratti da nuget.org in CodeSpaces - [#10549](https://github.com/NuGet/Home/issues/10549)

* L'inizializzazione di PMUI ha esito negativo con eccezione durante la sessione di debug [- #10559](https://github.com/NuGet/Home/issues/10559)

* nuget restore genera un errore di controllo dell'integrità del pacchetto big endian sistema - [#10567](https://github.com/NuGet/Home/issues/10567)

* Viene generata un'eccezione FormatException anziché PackagingException - [#10595](https://github.com/NuGet/Home/issues/10595)

* CPVM - Problemi di concorrenza nell'algoritmo di grafi walking - [#10598](https://github.com/NuGet/Home/issues/10598)

* Aggiungere i dati di telemetria della versione di PowerShell PMC - [#10609](https://github.com/NuGet/Home/issues/10609)

* Migliorare le prestazioni di ordinamento di NuGetVersion - [#10611](https://github.com/NuGet/Home/issues/10611)

* Trusted-signers Add ha argomenti incoerenti - [#10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 v16.9.0: il passaggio delle schede in NuGet Gestione pacchetti da "Aggiornamenti" a "Installato" non aggiorna il frame. - [#10654](https://github.com/NuGet/Home/issues/10654)

* Rimuovere "v" dal numero di versione in PMUI - [#10677](https://github.com/NuGet/Home/issues/10677)

* INuGetProjectService.GetInstalledPackagesAsync genera un'eccezione prima di ricevere la candidatura del sistema di progetto CPS - [#10681](https://github.com/NuGet/Home/issues/10681)

* Le icone incorporate causano l'accesso negato dall'origine Microsoft Visual Studio pacchetti offline nella scheda Sfoglia - [#10687](https://github.com/NuGet/Home/issues/10687)

* INuGetProjectService.GetInstalledPackagesAsync genera un'eccezione quando MSBuildProjectExtensionsPath non è impostato - [#10739](https://github.com/NuGet/Home/issues/10739)

* "dotnet nuget remove source nuget.org" non funziona la prima volta- [#10745](https://github.com/NuGet/Home/issues/10745)

* NuGet blocca un thread di pool di thread in un metodo asincrono effettuando una chiamata sincrona al thread dell'interfaccia utente [#10775](https://github.com/NuGet/Home/issues/10775)

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` è un codice in dead code che danneggia le prestazioni - [#10790](https://github.com/NuGet/Home/issues/10790)

* Usare l'icona incorporata NuGet pacchetti SDK - [#10795](https://github.com/NuGet/Home/issues/10795)

* Aggiornare l'elenco di licenze SPDX - [#10806](https://github.com/NuGet/Home/issues/10806)

**[Elenco di tutti i problemi risolti in questa versione - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[Elenco dei commit in questa versione - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>Contributi della community

Grazie a tutti i collaboratori che hanno contribuito a rendere NuGet rilascio straordinario.

|Chi|Prs|Problemi|
|----|----|----|
[z z](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | VersionRange non è in grado di analizzare intervalli a una cifra [- #10342](https://github.com/NuGet/Home/issues/10342)
[omajid](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | NuGet. L'build.sh client è interrotta [- #10139](https://github.com/NuGet/Home/issues/10139)
[Nirmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | NuGet. L'build.sh client è interrotta [- #10139](https://github.com/NuGet/Home/issues/10139)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | Le prestazioni di "nuget pack" diminuiscono con livelli crescenti nei percorsi di [origine, #5706](https://github.com/NuGet/Home/issues/5706)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | NuGet.exe problema di prestazioni del pacchetto con . percorso relativo - [#5016](https://github.com/NuGet/Home/issues/5016)
[centro-krystianc](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | CPVM - Problemi di concorrenza nell'algoritmo di grafi walking - [#10598](https://github.com/NuGet/Home/issues/10598)
[josesimoes](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | Aggiungere il tipo di progetto nfproj all'elenco di supportedProjectExtensions per l'interfaccia della riga di comando di NuGet. - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>Commenti e suggerimenti

I commenti degli utenti sono importanti.  Se si verificano problemi con questa versione, vedere l'GitHub [problemi](https://github.com/NuGet/Home/issues) e Visual Studio [developer Community](https://developercommunity.visualstudio.com/) problemi esistenti.  Per nuovi problemi all'interno NuGet, segnalare un [GitHub problema](https://github.com/NuGet/Home/issues/new).
Per informazioni NuGet problemi di esperienza, [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) segnalarci tramite l'opzione Segnala un problema disponibile nell'IDE preferito in Guida > **segnalare un problema**.
