---
title: 3.5 note sulla versione RC
description: Note sulla versione per NuGet 3.5 RC, tra cui i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548538"
---
# <a name="nuget-35-rc-release-notes"></a>Note sulla versione per NuGet 3.5 RC

[Note sulla versione per NuGet 3.5-Beta2](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-note sulla versione RTM](../release-notes/nuget-3.5-RTM.md)

versione 3.5 è incentrata sul miglioramento della qualità e prestazioni dei client di NuGet. Abbiamo, inoltre, abbiamo fornito alcune funzionalità, come il supporto [cartelle di Fallback](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) supportare in `.nuspec` e altro ancora.

[Elenco dei problemi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Correzioni di bug

* Installazione e il ripristino di un pacchetto ha esito negativo con "pacchetto contiene più `.nuspec` file." - [#3231](https://github.com/NuGet/Home/issues/3231)

* pacchetto NuGet aggiunge in modo forzato `.tt` i file di contenuto cartella indipendentemente - [#3203](https://github.com/NuGet/Home/issues/3203)

* NuGet pack csproj (con `project.json`) si blocca se sono non presenti packOptions e proprietario nel file JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* pacchetto NuGet per `project.json` ignora i tag packOptions come riepilogo, gli autori e proprietari e così via - [#3161](https://github.com/NuGet/Home/issues/3161)

* pacchetto NuGet ignora le dipendenze nell'output `.nuspec` per `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Aggiornamento di più pacchetti con rollback lascia il progetto in uno stato danneggiato - [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles in presenza non vengono aggiunti per i progetti di moniker netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* Impossibile creare pacchetto libreria per .net Standard correttamente - [#3108](https://github.com/NuGet/Home/issues/3108)

* File -> Nuovo progetto -> ha esito negativo al progetto libreria di classi (portabile) VS2015 e Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* Errore di NuGet - 1.0.0-* non è una stringa di versione valida - [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package ha esito negativo per la visualizzazione, ma il funzionamento di Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Errore quando "Install-Package jquery.validation" in dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* Quando è installato Visual Studio 2015 update 3 in un Visual Studio che usa NuGet si verifica l'errore di versione 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)

* Pacchetto interfaccia utente di gestione: non visualizza una nuova versione dopo aver aggiornato un pacchetto- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey nella riga di comando di eliminazione non viene in lettura/inviata 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Stringa non corretto: una versione stabile di un pacchetto non deve avere in una versione non definitiva dipendenza. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Creazione di get di progetto libreria di classi Portabile (destinazione net46 e windows 10) l'eccezione NullRef. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Aggiornamento di NuGet deve fornire un messaggio informativo quando una versione successiva è limitata dal vincolo di attributo allowedversions valido - [#3013](https://github.com/NuGet/Home/issues/3013)

* Plug-in credenziali chiuso con errore -1 / errore di download del pacchetto quando si utilizzano provider di credenziali con più origini - [#2885](https://github.com/NuGet/Home/issues/2885)

* pacchetto NuGet - dipendenza di pacchetto mancante newtonsoft - [#2876](https://github.com/NuGet/Home/issues/2876)

* Bug in ExecuteSynchronizedCore su Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)

* Visual Studio non supporta le variabili di ambiente in repositoryPath (nuget.exe non) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Risolvere i problemi di accessibilità - [#2745](https://github.com/NuGet/Home/issues/2745)

* Framework portabili con i profili con trattini sono rifiutate. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Gestione pacchetti NuGet deve mettere in evidenza tale elenco di opzioni in dettaglio non è valida per i pacchetti `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 aggiornamento ha esito negativo con '... un ulteriore vincolo definito in Packages. config impedisce l'operazione.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* L'installazione del pacchetto da un'origine locale che non esiste genera un messaggio fittizio - [#1674](https://github.com/NuGet/Home/issues/1674)

* "Aggiornamento disponibile" filtro consente di visualizzare gli aggiornamenti che violano il vincolo di versione - [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Miglioramenti delle prestazioni

* Prestazioni: Miglioramento ContentModel destinazione framework analisi - [#3162](https://github.com/NuGet/Home/issues/3162)

* Prestazioni: Evitare la lettura `runtime.json` file per i ripristini che non dispongono di RID [#3150](https://github.com/NuGet/Home/issues/3150). Nei computer di integrazione continua, il ripristino di un esempio di che applicazione Web ASP.NET ridotta da più di 15 secondi per 3 secondi.

* Prestazioni: Tempo di caricamento Package Manager Console init.ps1 [#2956](https://github.com/NuGet/Home/issues/2956). Tempo di apertura PackageManagerConsole migliorata in alcuni casi da 132s a 10 secondi.

* Risolvere i problemi di prestazioni ReSharper in aggiornamento NuGet - [#3044](https://github.com/NuGet/Home/issues/3044): in un progetto di esempio, tempo impiegato per installare i pacchetti ridotto da 140s a 68s.

## <a name="dcrs"></a>DCR

* NuGet è necessario informare gli utenti che l'aggiornamento o l'installazione in un tfm dotnet basato su PCL potrebbe provocare problemi - [#3138](https://github.com/NuGet/Home/issues/3138)

* Installazione/aggiornamento non valido per il progetto con tfm Avvisa = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)

* Aggiungere il supporto netcoreapp11 e netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Stampare il contenuto dell'intestazione NuGet avviso alla console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)

* Attributo AssemblyMetadata sfrutta `.nuspec` token sostituzioni - [#2851](https://github.com/NuGet/Home/issues/2851)

* Rimuovere la proprietà bloccata dal file di blocco - [#2379](https://github.com/NuGet/Home/issues/2379)

* Pacchetti dei simboli non devono mai essere utilizzati nell'installare o aggiornare #2807

## <a name="features"></a>Funzionalità

* Supporto per le cartelle pacchetto fallback - [#2899](https://github.com/NuGet/Home/issues/2899)

* Progettare e implementare una nozione di tipo di pacchetto per supportare i pacchetti strumento - [#2476](https://github.com/NuGet/Home/issues/2476)

* API per ottenere il percorso della cartella di pacchetti globale - [#2403](https://github.com/NuGet/Home/issues/2403)

* Supporto - aggiornare i pacchetti nativi [#1291](https://github.com/NuGet/Home/issues/1291)
