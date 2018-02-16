---
title: Note sulla versione per NuGet 4.5 RTM | Microsoft Docs
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 12/4/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Note sulla versione per NuGet 4.5 RTM incluse informazioni su problemi noti, correzioni di bug e DCR.
keywords: "Note sulla versione per NuGet 4.5 RTM, correzioni di bug, problemi noti, funzionalità aggiunte, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: e4727d46812cbfeb2e7094ddf28bf4e738e8aeea
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-45-rtm-release-notes"></a>Note sulla versione per NuGet 4.5 RTM

[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) include [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).

## <a name="known-issues"></a>Problemi noti

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemi relativi a .NET 2.0 Standard con .NET Framework e NuGet 

.NET Standard e i relativi strumenti sono stati progettati in modo che i progetti destinati a .NET Framework 4.6.1 possano utilizzare pacchetti e progetti NuGet destinati a .NET Standard 2.0 o versioni precedenti. [Questo documento](https://github.com/dotnet/standard/issues/481) riepiloga i problemi relativi a questo scenario, i piani per risolverli e le soluzioni alternative implementabili allo stato attuale degli strumenti.

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

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Un pacchetto in un progetto .NET Core contenente un assembly con una firma non valida, può causare un ciclo infinito di ripristino

#### <a name="issue"></a>Problema

A volte, quando si usa un pacchetto contenente un assembly con una firma non valida o quando la versione del pacchetto è impostata con tick 'DateTime', è possibile che il processo di ripristino automatico del pacchetto entri in un ciclo infinito [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).

#### <a name="workaround"></a>Soluzione alternativa

Attualmente non esiste alcuna soluzione.

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>Problemi risolti nell'intervallo di tempo NuGet 4.5 RTM

Per i problemi risolti in NuGet 4.4 RTM, vedere le [Note sulla versione per NuGet 4.4 RTM](../release-notes/nuget-4.4-RTM.md) 

### <a name="features"></a>Funzionalità

- Disabilitare il push automatico del pacchetto di simboli - [#6113](https://github.com/NuGet/Home/issues/6113)

### <a name="bugs"></a>Bug

- [Regressione] in 15.5p1: Portable0.0 viene ignorato - [#6105](https://github.com/NuGet/Home/issues/6105)
- Asset dai pacchetti mancanti dopo il ripristino - [#5995](https://github.com/NuGet/Home/issues/5995)
- I provider di credenziali plug-in non funzionano con gli URI contenenti spazi - [#5982](https://github.com/NuGet/Home/issues/5982)
- Se il ripristino del pacchetto non riesce, l'errore deve comparire nell'output anche quando è attivo il livello di dettaglio minimo - [#5658](https://github.com/NuGet/Home/issues/5658)
- dotnet restore a livello di soluzione non segue ProjectReference con ReferenceOutputAssembly impostato su false, con conseguenti errori di compilazione casuali - [#5490](https://github.com/NuGet/Home/issues/5490)
- Il completamento automatico nella console di Gestione pacchetti non funziona correttamente con i metodi di oggetto - [#4800](https://github.com/NuGet/Home/issues/4800)
- Il ripristino di nuget.exe non funziona con il set di strumenti di Visual Studio 2015 - [#4713](https://github.com/NuGet/Home/issues/4713)
- Prestazioni: la creazione di istanze della console di Gestione pacchetti è onerosa in VS2017 - [#4205](https://github.com/NuGet/Home/issues/4205)
- Recupero di informazioni sulle dipendenze lento su connessione lenta - [#4089](https://github.com/NuGet/Home/issues/4089)
- uninstall-package con -RemoveDependencies avrà esito negativo se più pacchetti condividono una dipendenza in comune - [#4026](https://github.com/NuGet/Home/issues/4026)
- Finalizzare NuGet.Core.nupkg per la pubblicazione - [#3581](https://github.com/NuGet/Home/issues/3581)
- NuGet pack risolve l'ID di dipendenza dal nome di directory quando si usa -IncludeProjectReferences per csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)
- L'inizializzatore di tipo per 'NuGet.ProxyCache' ha generato un'eccezione - [#3144](https://github.com/NuGet/Home/issues/3144)
- Problema di prestazioni di nuget restore con kudu - [#3087](https://github.com/NuGet/Home/issues/3087)
- Il client dell'interfaccia utente non visualizza errori o avvisi quando la ricerca non è sincronizzata con i BLOB di registrazione - [#2149](https://github.com/NuGet/Home/issues/2149)
- Get-Packages-Updates genera una query non corretta - [#2135](https://github.com/NuGet/Home/issues/2135)

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>Collegamenti ai problemi di GitHub risolti nella versione 4.5 RTM

[Elenco dei problemi](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
