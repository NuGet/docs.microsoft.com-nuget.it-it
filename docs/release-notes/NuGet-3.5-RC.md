---
title: Note sulla versione di 3,5 RC
description: Note sulla versione per NuGet 3,5 RC, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780197"
---
# <a name="nuget-35-rc-release-notes"></a>Note sulla versione di NuGet 3,5 RC

Note sulla versione [di NuGet 3,5-beta2](../release-notes/nuget-3.5-Beta2.md)  |  [Note sulla versione di NuGet 3,5-RTM](../release-notes/nuget-3.5-RTM.md)

3,5 versione è incentrata sul miglioramento della qualità e delle prestazioni dei client NuGet. Sono state inoltre fornite alcune funzionalità come il supporto per le [cartelle di fallback](https://github.com/NuGet/Home/issues/2899), il supporto [PackageType](https://github.com/NuGet/Home/issues/2476) in `.nuspec` e altro ancora.

[Elenco dei problemi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Correzioni di bug

* L'installazione o il ripristino di un pacchetto ha esito negativo con "il pacchetto contiene più `.nuspec` file". - [#3231](https://github.com/NuGet/Home/issues/3231)

* il pacchetto NuGet aggiunge `.tt` in modo forzato i file alla cartella del contenuto indipendentemente dalla [#3203](https://github.com/NuGet/Home/issues/3203)

* NuGet Pack csproj (con `project.json` ) si arresta in modo anomalo se non sono presenti packOptions e Owner nel file JSON [#3180](https://github.com/NuGet/Home/issues/3180)

* il pacchetto NuGet per `project.json` Ignora i tag packOptions come Summary, authors, owners e così via [#3161](https://github.com/NuGet/Home/issues/3161)

* il pacchetto NuGet ignora le dipendenze nell'output `.nuspec` per `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* L'aggiornamento di più pacchetti con rollback lascia il progetto in uno stato di interruzione- [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles in any non sono stati aggiunti per i progetti netstandard- [#3118](https://github.com/NuGet/Home/issues/3118)

* Non è possibile creare un pacchetto della libreria di destinazione .NET standard correttamente- [#3108](https://github.com/NuGet/Home/issues/3108)

* File > nuovo progetto-> progetto libreria di classi (portabile) non riesce in VS2015 e Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* Errore NuGet-1.0.0-* non è una stringa di versione valida- [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package non viene visualizzato ma Install-Package funziona- [#3068](https://github.com/NuGet/Home/issues/3068)

* Errore durante "Install-Package jQuery. Validation" in dev15- [#3061](https://github.com/NuGet/Home/issues/3061)

* Quando si esegue l'installazione di Visual Studio 2015 Update 3 su un Visual Studio che usa la versione NuGet 3.5.0 si verifica un errore [#3053](https://github.com/NuGet/Home/issues/3053)

* Interfaccia utente di gestione pacchetti: non Visualizza la nuova versione dopo l'aggiornamento di un pacchetto- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey nella riga di comando DELETE non è stato letto/inviato in 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* Stringa non corretta: una versione stabile di un pacchetto non deve avere una dipendenza della versione provvisoria. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Creazione dell'eccezione NullRef del progetto PCL (' net46 e Windows 10). - [#3014](https://github.com/NuGet/Home/issues/3014)

* L'aggiornamento di NuGet deve fornire un messaggio informativo quando una versione più alta è limitata dal vincolo allowedVersions- [#3013](https://github.com/NuGet/Home/issues/3013)

* Il plug-in delle credenziali è stato terminato con errore-1/errore durante il download del pacchetto quando si usano i provider di credenziali con più origini [#2885](https://github.com/NuGet/Home/issues/2885)

* pacchetto NuGet-mancata Newtonsoft.Jssulla dipendenza del pacchetto- [#2876](https://github.com/NuGet/Home/issues/2876)

* Bug in ExecuteSynchronizedCore in Linux/MacOS + mono- [#2860](https://github.com/NuGet/Home/issues/2860)

* VS non supporta variabili di ambiente in repositoryPath (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)

* Risolvere i problemi di accessibilità- [#2745](https://github.com/NuGet/Home/issues/2745)

* I Framework portabili con profili con sillabazione vengono rifiutati. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Gestione pacchetti NuGet dovrebbe rendere chiaro che l'elenco di opzioni nei pacchetti non si applica ai `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* L'aggiornamento di NuGet 3.3.0 ha esito negativo con ' un vincolo aggiuntivo... definito in packages.config impedisce questa operazione. - [#1816](https://github.com/NuGet/Home/issues/1816)

* L'installazione di un pacchetto da un'origine locale che non esiste genera un messaggio fasullo [#1674](https://github.com/NuGet/Home/issues/1674)

* Il filtro "Aggiorna disponibili" Mostra gli aggiornamenti che violano il vincolo di versione [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Miglioramenti alle prestazioni

* Prestazioni: migliorare l'analisi del Framework di destinazione ContentModel- [#3162](https://github.com/NuGet/Home/issues/3162)

* Prestazioni: evitare `runtime.json` di leggere i file per i ripristini che non dispongono di rid [#3150](https://github.com/NuGet/Home/issues/3150). Nei computer CI, il ripristino di un'applicazione Web ASP.NET di esempio è ridotto da oltre 15 secondi a 3 secondi.

* Prestazioni: la console di gestione pacchetti init.ps1 [#2956](https://github.com/NuGet/Home/issues/2956)tempi di caricamento. Il tempo necessario per aprire PackageManagerConsole è migliorato in alcuni casi da 132S a 10s.

* Risolvere i problemi di prestazioni più nitidi nell'aggiornamento [#3044](https://github.com/NuGet/Home/issues/3044)di NuGet: in un progetto di esempio, il tempo necessario per installare i pacchetti è ridotto da 140S a 68S.

## <a name="dcrs"></a>DCR

* NuGet deve informare gli utenti che l'aggiornamento o l'installazione in una libreria PCL basata su DotNet TFM può causare problemi: [#3138](https://github.com/NuGet/Home/issues/3138)

* Avviso di installazione/aggiornamento errato per il progetto w/TFM = "DotNet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Aggiungere il supporto per netcoreapp11 e netstandard17- [#2998](https://github.com/NuGet/Home/issues/2998)

* Stampa il contenuto dell'intestazione NuGet-Warning nella console di nuget.exe- [#2934](https://github.com/NuGet/Home/issues/2934)

* Utilizzare l'attributo AssemblyMetadata per le `.nuspec` sostituzioni di token- [#2851](https://github.com/NuGet/Home/issues/2851)

* Rimuovere la proprietà Locked dal file di blocco- [#2379](https://github.com/NuGet/Home/issues/2379)

* I pacchetti di simboli non devono mai essere usati in installazione o aggiornamento #2807

## <a name="features"></a>Funzionalità

* Supporto per le cartelle dei pacchetti di fallback- [#2899](https://github.com/NuGet/Home/issues/2899)

* Progettare e implementare una nozione di tipo di pacchetto per supportare pacchetti di strumenti- [#2476](https://github.com/NuGet/Home/issues/2476)

* API per ottenere il percorso della cartella dei pacchetti globali- [#2403](https://github.com/NuGet/Home/issues/2403)

* Supporto per l'aggiornamento dei pacchetti nativi- [#1291](https://github.com/NuGet/Home/issues/1291)
