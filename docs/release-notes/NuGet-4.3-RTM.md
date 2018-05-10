---
title: Note sulla versione per NuGet 4.3 RTM
description: Note sulla versione per NuGet 4.3 RTM incluse informazioni su problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: cb44f47ef0b3bd086f0a681cb2fedc7c5afc42fa
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-43-rtm-release-notes"></a>Note sulla versione per NuGet 4.3 RTM

[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) include NuGet 4.3 RTM, che aggiunge il supporto per nuovi scenari, ad esempio.NET Standard 2.0/.NET Core 2.0, contiene varie correzioni di qualità e migliora le prestazioni. Questa versione introduce anche vari miglioramenti, come il supporto della versione 2.0.0 del versionamento semantico, l'integrazione in MSBuild degli avvisi e degli errori di NuGet e altro ancora.

## <a name="known-issues"></a>Problemi noti

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>In determinati casi il ripristino di NuGet gestisce le origini pacchetto disabilitate come se fossero abilitate

#### <a name="issue"></a>Problema

Le seguenti tecniche della riga di comando per il ripristino gestiscono le origini dei pacchetti disabilitate come abilitate. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore` (con il file dotnet.exe incluso con Visual Studio o con il file incluso con NetCore SDK 2.0.0)

#### <a name="workaround"></a>Soluzione alternativa

1. Usare Visual Studio (2017 15.3 o versioni successive) o NuGet.exe (v4.3.0 o versioni successive)
1. Eliminare l'origine disabilitata e continuare a usare msbuild o dotnet.exe.
1. Per la soluzione è possibile usare "Clear" in NuGet.config e quindi definire le origini necessarie per la soluzione.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Durante l'uso della console di Gestione pacchetti è possibile che il tasto 'INVIO' non funzioni

#### <a name="issue"></a>Problema

A volte, nella console di Gestione pacchetti il tasto INVIO non funziona. Se si riscontra questo problema, controllare lo stato di avanzamento della correzione e fornire altre informazioni utili sui passaggi per riprodurre la condizione di errore. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Soluzione alternativa

Riavviare Visual Studio e aprire la console di Gestione pacchetti prima di aprire la soluzione. In alternativa, provare a eliminare `project.lock.json` e ripetere il ripristino.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Non è possibile visualizzare, aggiungere o aggiornare DotNetCLITools usando Gestione pacchetti NuGet

#### <a name="issue"></a>Problema

Gestione pacchetti NuGet non visualizza e non consente l'aggiunta e/o l'aggiornamento di DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Soluzione alternativa

È necessario modificare manualmente DotNetCLIToolReferences nel file di progetto.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>La ridestinazione della versione framework di destinazione può portare a informazioni Intellisense incomplete

#### <a name="issue"></a>Problema

Se in Visual Studio si ridefinisce la destinazione della versione framework di destinazione, le informazioni Intellisense possono risultare incomplete. Questo accade quando si usa PackageReferences come formato di gestione dei pacchetti. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Soluzione alternativa

Eseguire un ripristino manuale.

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>Problemi risolti nell'intervallo di tempo NuGet 4.3 RTM

[Note sulla versione per NuGet 4.0 RTM](../release-notes/nuget-4.0-RTM.md) - Vengono elencati tutti i problemi risolti per NuGet 4.0 RTM

### <a name="features"></a>Funzionalità

- Miglioramento delle prestazioni del ripristino NuGet - Implementazione di NoOp più intelligente per i ripristini dalla riga di comando e VS - [#5080](https://github.com/NuGet/Home/issues/5080)

- NET Core 2.0: l'interfaccia della riga di comando di VS/Dotnet deve iniziare a usare funzionalità NuGet esistenti: cartelle di fallback - [#4939](https://github.com/NuGet/Home/issues/4939)

- NET Core 2.0: consentire agli utenti di ignorare avvisi di ripristino specifici (o elevarli a errore) - [#4898](https://github.com/NuGet/Home/issues/4898)

- NET Core 2.0: assembly localizzati dell'interfaccia della riga di comando - [#4896](https://github.com/NuGet/Home/issues/4896)

- NET Core 2.0: registrare tutti gli avvisi/errori nel file degli asset (incluso PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)

- Abilitare il supporto del moniker TFM: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)

- Ridurre il numero di progetti NuGet.Core e NuGet.Client (quindi di DLL) - [#2446](https://github.com/NuGet/Home/issues/2446)

- Aggiungere la possibilità di contrassegnare gli avvisi NuGet come errori - [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>Bug

- Errore di msbuild /t:pack con il parametro "DevelopmentDependency" non supportato dall'attività "PackTask" - [#5584](https://github.com/NuGet/Home/issues/5584)

- La struttura di directory per i file di contenuto diventa flat se non si aggiunge il separatore di directory Windows alla fine di PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)

- I progetti netcore non supportano l'impostazione come developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)

- RestoreManagerPackage viene caricato in modo sincrono con conseguente blocco del thread dell'interfaccia utente e deadlock di VS - [#4679](https://github.com/NuGet/Home/issues/4679)

- dotnet
  - dotnetcore Restore (e quindi msbuild /t:restore) ignora i progetti con una dipendenza esplicita da un progetto nella soluzione [#4578](https://github.com/NuGet/Home/issues/4578)

- Se la soluzione contiene ProjectReference che fanno riferimento allo stesso progetto, con combinazioni di maiuscole/minuscole diverse, il ripristino potrebbe non funzionare. Questo problema riguarda anche percorsi relativi diversi, senza differenze nella combinazione di maiuscole/minuscole - [#4574](https://github.com/NuGet/Home/issues/4574)

- Gli eseguibili ripristinati da pacchetti NuGet non sono più eseguibili con .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)

- NuGet.exe non visualizza tutti i dettagli dell'eccezione durante l'analisi del file di soluzione - [#4411](https://github.com/NuGet/Home/issues/4411)

- Pack inserisce i file di contenuto nella posizione errata se ContentTargetFolders contiene un percorso che termina con '/' in Windows - [#4407](https://github.com/NuGet/Home/issues/4407)

- Non è possibile ripristinare un DotNetCliToolReference per un pacchetto di strumenti con destinazione netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)

- L'interfaccia della riga di comando per l'aggiornamento di NuGet lascia la condizione della versione del pacchetto precedente nel file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>DCR

- Lettura di DotnetCliToolTargetFramework dai nomi CPS - [#5397](https://github.com/NuGet/Home/issues/5397)

- Il controllo TPMinV dovrebbe funzionare per progetti UWP - [#4763](https://github.com/NuGet/Home/issues/4763)

- Migliorare la descrizione dell'interfaccia utente per i pacchetti AutoReferenced - [#4471](https://github.com/NuGet/Home/issues/4471)

- Il ripristino di NuGet seleziona gli asset di compilazione dalla sezione di runtime. - [#4207](https://github.com/NuGet/Home/issues/4207)

- Inserire la diagnostica per le dipendenze nel file di blocco - [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>Collegamenti ai problemi di GitHub risolti nella versione 4.3 RTM

[Elenco dei problemi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
