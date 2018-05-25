---
title: Note sulla versione per NuGet 4.6 RTM
description: Note sulla versione per NuGet 4.6.0 incluse informazioni su problemi noti, correzioni di bug e DCR.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: 11e604ad9a28ac2b22880a13ef9d8b41d8c09507
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2018
---
# <a name="nuget-46-rtm-release-notes"></a>Note sulla versione per NuGet 4.6 RTM

[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) include [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).

## <a name="summary-whats-new-in-this-release"></a>Riepilogo: Novità di questa versione

* È stato aggiunto il supporto per [firma dei pacchetti](../create-packages/sign-a-package.md).
* Visual Studio 2017 e nuget.exe ora verificano l'integrità dei pacchetti prima dell'installazione, ripristinando i [pacchetti firmati](../reference/signed-packages-reference.md).
* Sono state migliorate le prestazioni dei ripristini successivi.

## <a name="known-issues"></a>Problemi noti

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemi relativi a .NET 2.0 Standard con .NET Framework e NuGet 

.NET Standard e i relativi strumenti sono stati progettati in modo che i progetti destinati a .NET Framework 4.6.1 possano utilizzare pacchetti e progetti NuGet destinati a .NET Standard 2.0 o versioni precedenti. [Questo documento](https://github.com/dotnet/standard/issues/481) riepiloga i problemi relativi a questo scenario, i piani per risolverli e le soluzioni alternative implementabili allo stato attuale degli strumenti.

## <a name="top-issues-fixed-in-this-release"></a>Problemi principali corretti in questa versione

**Correzioni per le prestazioni**

* Non scrivere file di asset in assenza di modifiche - [#6491](https://github.com/NuGet/Home/issues/6491)
* Il ripristino causa valutazioni MSBuild aggiuntive quando il TFM dei progetti figlio non corrisponde a quello del padre del progetto - [#6311](https://github.com/NuGet/Home/issues/6311)
* Migliorare le prestazioni di ripristino NoOp ottimizzando la creazione della specifica del grafico delle dipendenze - [#6252](https://github.com/NuGet/Home/issues/6252)

**Bug**

* Il push in una cartella locale lascia nupkg bloccato - [#6325](https://github.com/NuGet/Home/issues/6325)
* Implementazione di plug-in NuGet: più problemi - [#6149](https://github.com/NuGet/Home/issues/6149)
* UIHang - Rimuovere la chiamata del servizio query dall'inizializzazione MEF in VSSolutionManager - [#6110](https://github.com/NuGet/Home/issues/6110)
* Eccezione di segnalazione errori per l'attività di download del pacchetto annullata - [#6096](https://github.com/NuGet/Home/issues/6096)
* NuGet.exe sostituisce '+' con '%2B' nel nome di assembly - [#5956](https://github.com/NuGet/Home/issues/5956)
* Fn+F1 non porta alla pagina della Guida corretta per l'interfaccia utente e la console di Gestione pacchetti - [#5912](https://github.com/NuGet/Home/issues/5912)
* VS NuGet scrive percorsi assoluti nei file di progetto in determinate circostanze - [#5888](https://github.com/NuGet/Home/issues/5888)
* Correzione regressione 4.3 - I segnaposto $product$ e $ $AssemblyGuid non vengono sostituiti nel file di contenuto tramite la trasformazione - [#5880](https://github.com/NuGet/Home/issues/5880)
* Arresto anomalo di dotnet restore con più origini - [#5817](https://github.com/NuGet/Home/issues/5817)
* Il comando pack deve valutare nuovamente le versioni di progetto per consentire il controllo delle versioni git - [#4790](https://github.com/NuGet/Home/issues/4790)
* Migliorare errori difficili da capire quando si installa un pacchetto incompatibile - [#4555](https://github.com/NuGet/Home/issues/4555)
* Opzione necessaria in TemplateWizard per installare i pacchetti come PackageReferences - [#4549](https://github.com/NuGet/Home/issues/4549)
* I file props forniti dal pacchetto vengono ignorati quando MSBuild.exe viene eseguito all'esterno di un prompt dei comandi per sviluppatori - [#4530](https://github.com/NuGet/Home/issues/4530)
* Correggere il messaggio di errore poco comprensibile quando si fa riferimento a una libreria .NET Standard non applicabile al progetto - [#4423](https://github.com/NuGet/Home/issues/4423)
* Il comando dotnet add package non riesce per un pacchetto destinato a un profilo portatile con scarse indicazioni - [#4349](https://github.com/NuGet/Home/issues/4349)
* dotnet pack - suffisso version mancante da ProjectReference - [#4337](https://github.com/NuGet/Home/issues/4337)
* Errori di compilazione e arresto anomalo di Visual Studio con modello .NET Core - [#3973](https://github.com/NuGet/Home/issues/3973)
* Impossibile caricare l'indice del servizio per l'origine https:* - [#3681](https://github.com/NuGet/Home/issues/3681)
* nuget.exe list -allversions non funziona - [#3441](https://github.com/NuGet/Home/issues/3441)
* Messaggio di errore fuorviante per la risoluzione delle dipendenze - [2984 #](https://github.com/NuGet/Home/issues/2984)
* nuget.exe restore non produce file con estensione props e targets per msbuildproj (regressione nell'aggiornamento v3.3.0-3.4.4) - [#2921](https://github.com/NuGet/Home/issues/2921)
* Ritardo dell'interfaccia utente quando si aggiorna un pacchetto NuGet con apri file XAML - [#2878](https://github.com/NuGet/Home/issues/2878)
* Errore del progetto di sito Web da IIS con caratteri non validi nel percorso - [#2798](https://github.com/NuGet/Home/issues/2798)
* Blocco di nuget add in CentOS - [#2708](https://github.com/NuGet/Home/issues/2708)
* Il ripristino con packagesavemode -nupkg non riesce per json.net - [#2706](https://github.com/NuGet/Home/issues/2706)
* Filtro di Gestione pacchetti non disponibile nella finestra di output di Visual Studio per il comando restore - [#2704](https://github.com/NuGet/Home/issues/2704)

[Elenco di tutti i problemi corretti in questa versione](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
