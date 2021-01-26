---
title: Note sulla versione di 3,5 beta2
description: Note sulla versione per NuGet 3,5 Beta 2, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776386"
---
# <a name="nuget-35-beta2-release-notes"></a>Note sulla versione di NuGet 3,5 beta2

Note sulla versione [di NuGet 3,5-beta](../release-notes/nuget-3.5-Beta.md)  |  [Note sulla versione di NuGet 3,5-RC](../release-notes/nuget-3.5-RC.md)

NuGet 3,5 Beta 2 RTM è stato rilasciato il 27 giugno 2016 per Visual Studio 2013 e nuget.exe

[Changelog completo](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Elenco dei problemi](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Correzioni di bug

* Messaggio di errore aggiornato per la mancanza di supporto per la password decrpytion in .NET Core per i feed autenticati- [#2942](https://github.com/NuGet/Home/issues/2942)

* La console di gestione pacchetti Get-Package ha esito negativo se il progetto .NET Core è aperto [#2932](https://github.com/NuGet/Home/issues/2932)

* Correzione della gestione errata di 403 nel comando Push NuGet [#2910](https://github.com/NuGet/Home/issues/2910)

* Risolvere i problemi di disinstallazione dei pacchetti in una soluzione associata al controllo del codice sorgente TFS quando disableSourceControlIntegration è impostato su true- [#2739](https://github.com/NuGet/Home/issues/2739)

* Correzione dell'aggiornamento del pacchetto per tenere conto dei pacchetti non di destinazione- [#2724](https://github.com/NuGet/Home/issues/2724)

* Usare il livello di dettaglio di MSBuild per impostare il livello del logger per le azioni dell'interfaccia utente di gestione pacchetti NuGet- [#2705](https://github.com/NuGet/Home/issues/2705)

* Correggi la configurazione NuGet non è un errore valido nei progetti di siti Web-VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)

* Risolvere i problemi di Pack da `.csproj` quando sono inclusi i file di contenuto- [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource `NuGetDefaults.Config` ( `ProgramData\NuGet` ) non funziona- [#2653](https://github.com/NuGet/Home/issues/2653)

* Correzione del problema nella versione di NuGet 3.4.3: il valore non può essere null durante la creazione del pacchetto: [#2648](https://github.com/NuGet/Home/issues/2648)

* Il ripristino usa le credenziali archiviate da Nuget.Config per i feed VSTS- [#2647](https://github.com/NuGet/Home/issues/2647)

* Prestazioni: correzione di allocazioni eccessive nel codice di comparizione delle versioni- [#2632](https://github.com/NuGet/Home/issues/2632)

* Risolvere i problemi quando più istanze di nuget.exe tentano di installare lo stesso pacchetto in parallelo- [#2628](https://github.com/NuGet/Home/issues/2628)

* Prestazioni: informazioni sulle dipendenze della cache per le operazioni multiprogetto- [#2619](https://github.com/NuGet/Home/issues/2619)

* Correzione del problema per cui le origini dei pacchetti Impossibile vengono aggiunte dalle impostazioni quando l'elenco di origine è vuoto [#2617](https://github.com/NuGet/Home/issues/2617)

* Correzione di un errore fuorviante durante il tentativo di installare il pacchetto che dipende dalle facciate della fase di progettazione- [#2594](https://github.com/NuGet/Home/issues/2594)

* L'installazione di un pacchetto dalla console di PackageManager con l'impostazione "All" prova solo la prima origine- [#2557](https://github.com/NuGet/Home/issues/2557)

* Risolvere i problemi relativi ai pacchetti con file con tempi di scrittura in futuro (mono)- [#2518](https://github.com/NuGet/Home/issues/2518)

* Visualizza l'eccezione quando si verifica un errore durante la ricerca di progetti nel comando Update- [#2418](https://github.com/NuGet/Home/issues/2418)

* Il contenuto del pacchetto non viene ripristinato correttamente quando si installa un pacchetto da un feed NuGet v 3.3 + con l'argomento-NoCache quando il pacchetto contiene `.nupkg` file- [#2354](https://github.com/NuGet/Home/issues/2354)

* Correzione di un problema con l'installazione del pacchetto (tutte le origini) quando manca il pacchetto da 1 origine- [#2322](https://github.com/NuGet/Home/issues/2322)

* Installa i blocchi se un'unica origine non riesce a eseguire l'autorizzazione- [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` l'intervallo di versioni deve eseguire l'override della versione-IncludeReferencedProjects- [#1983](https://github.com/NuGet/Home/issues/1983)

* L'aggiornamento di NuGet 3.3.0 ha esito negativo con ' un vincolo aggiuntivo... definito in packages.config impedisce questa operazione. - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe aggiornamento elimina il nome sicuro e l'attributo privato dell'assembly. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Risolvere i problemi relativi al percorso file relativo per "DefaultPushSource"- [#1746](https://github.com/NuGet/Home/issues/1746)

* Migliorare i messaggi di errore del resolver di aggiornamento- [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Funzionalità e modifiche funzionali

* nuget.exe parametro di timeout push non funziona- [#2785](https://github.com/NuGet/Home/issues/2785)

* nuget.exe Restore non `.props` produce `.targets` file e per i `.nuproj` progetti (regressione in v 3.4.3.855)- [#2711](https://github.com/NuGet/Home/issues/2711)

* È necessaria l'API di estendibilità per confrontare i Framework con le importazioni- [#2633](https://github.com/NuGet/Home/issues/2633)

* Nascondi le opzioni di dipendenza quando si usa `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Stampare l'intestazione della versione nuget.exe nell'output dettagliato- [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet dovrebbe aggiungere il supporto per/Runtimes/{RID}/nativeassets/{TXM}/- [#2782](https://github.com/NuGet/Home/issues/2782)