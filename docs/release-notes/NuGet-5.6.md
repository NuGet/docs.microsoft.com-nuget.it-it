---
title: Note sulla versione di NuGet 5,6
description: Note sulla versione per NuGet 5,6, incluse nuove funzionalità, correzioni di bug e DCR.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727821"
---
# <a name="nuget-56-release-notes"></a>Note sulla versione di NuGet 5,6

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio| Disponibile in .NET SDK|
|:---|:---|:---|
| [**5.6.0**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16,6](https://visualstudio.microsoft.com/downloads/) | [3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Installato con Visual Studio 2019 con carico di lavoro di .NET Core

## <a name="summary-whats-new-in-56"></a>Riepilogo: novità di 5,6

* Supporta i pacchetti di versioni non definitive con versioni mobili. `Version="*-*"`, `Version="1.*-*"` e float analogo alle versioni più recenti, incluse le versioni provvisorie, entro l'intervallo specificato- [#912](https://github.com/NuGet/Home/issues/912)

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**Bug**

* `nuget push *.nupkg`ha esito negativo se snupkg non esiste- [#8148](https://github.com/NuGet/Home/issues/8148)

* Pack e diversi altri percorsi di codice non riescono a dipendere dalle impostazioni locali. Usare RegexOptions. CultureInvariant- [#8246](https://github.com/NuGet/Home/issues/8246)

* Prestazioni: le specifiche DG per gli scenari di progetto scaricati non devono essere scritte nei ripristini di anteprima [#8793](https://github.com/NuGet/Home/issues/8793)

* Ripristino: migliorare le prestazioni memorizzando nella cache le specifiche del grafico delle dipendenze della soluzione- [#9201](https://github.com/NuGet/Home/issues/9201)

* L'interfaccia utente PM non funziona per i progetti di stile SDK dopo l'installazione di un pacchetto con la console PM- [#9203](https://github.com/NuGet/Home/issues/9203)

* Non è possibile visualizzare l'icona incorporata nell'interfaccia utente di PM con il feed di pacchetti locale, a seconda di/vs [#9225](https://github.com/NuGet/Home/issues/9225)

* NuGetVersion. TryParseStrict () deve restituire false se l'analisi non riesce. [#9255](https://github.com/NuGet/Home/issues/9255)

* `nuget.exe push`Guida per `-source` , deve suggerire l'uso del nome di origine, non dell'URL di origine- [#9265](https://github.com/NuGet/Home/issues/9265)

* `dotnet nuget add package SourceUri`Crea il nome di origine del pacchetto predefinito non valido- [#9277](https://github.com/NuGet/Home/issues/9277)

* La lettura dello schermo non annuncia "ricerca..." messaggio durante il cambio di schede- [#9307](https://github.com/NuGet/Home/issues/9307)

* Accessibilità: stato attivo-colore rettangolo non accessibile per le schede dell'interfaccia utente nel tema scuro- [#9336](https://github.com/NuGet/Home/issues/9336)

* il ripristino di NuGet. exe 5,5 non riesce con MSBuild 14 o versioni precedenti [#9458](https://github.com/NuGet/Home/issues/9458)

* Non registrare i millisecondi per i messaggi di ripristino- [#8977](https://github.com/NuGet/Home/issues/8977)

* Make IOutputConsole Async- [#9268](https://github.com/NuGet/Home/issues/9268)

* La selezione della versione di MSBuild non funziona in alcune culture non in lingua inglese, [#9322](https://github.com/NuGet/Home/issues/9322)

* Formato predefinito mancante `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)

* Prestazioni: RestoreOperationLogger con affinità di thread non necessaria- [#9288](https://github.com/NuGet/Home/issues/9288)

* Creazione automatica di documenti per i `dotnet nuget` comandi- [#9146](https://github.com/NuGet/Home/issues/9146)

* Il livello di dettaglio predefinito non deve segnalare il ripristino NOOP di ogni progetto- [#8792](https://github.com/NuGet/Home/issues/8792)

* `-DependencyVersion`Parametro di supporto per `NuGet.exe update` , simile a install command- [#7694](https://github.com/NuGet/Home/issues/7694)


**DCR**

* Aggiungere il supporto iniziale per il Framework di destinazione NET 5.0- [#9584](https://github.com/NuGet/Home/issues/9584)

* Ordinare i pacchetti in base all'ID nella scheda aggiornamenti dell'interfaccia utente di PM- [#9278](https://github.com/NuGet/Home/issues/9278)


**[Elenco di tutti i problemi risolti in questa versione-5,6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**
