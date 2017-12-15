---
title: 3.5 note sulla versione Beta2 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0b76064f-0607-438a-bbf8-dd862690f48e
description: "Note sulla versione per NuGet 3.5 Beta 2, inclusi i problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet 3.5 Beta 2 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6dd388e52308d2f3cd32d4d6c66c2868f0ae2a41
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="35-beta2-release-notes"></a>3.5 note sulla versione Beta2

[Note sulla versione 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md) | [note sulla versione 3.5 RC NuGet](../release-notes/nuget-3.5-RC.md)

Versione RTM di NuGet 3.5 Beta 2 è stato rilasciato il 27 giugno 2016 per Visual Studio 2013 e nuget.exe

[Log delle modifiche completo](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Elenco problemi](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

# <a name="notable-changes"></a>Modifiche significative

## <a name="bug-fixes"></a>Correzioni di bug

* Mancanza di supporto per password decrpytion in .NET Core per i feed autenticati - messaggio di errore aggiornato [&#2942;](https://github.com/NuGet/Home/issues/2942)

* Get-pacchetto Console di gestione pacchetti non riesce se il progetto .NET Core è aperto - [&#2932;](https://github.com/NuGet/Home/issues/2932)

* Correzione della gestione corretta di 403 nel comando push NuGet [&#2910;](https://github.com/NuGet/Home/issues/2910)

* Risolvere i problemi nel disinstallare i pacchetti in una soluzione associato al controllo del codice sorgente TFS quando disableSourceControlIntegration è impostata su true - [&#2739;](https://github.com/NuGet/Home/issues/2739)

* Correggere l'aggiornamento del pacchetto da eseguire in pacchetti bersaglio account - [&#2724;](https://github.com/NuGet/Home/issues/2724)

* Utilizzare il livello di dettaglio di MSBuild per impostare il livello di logger per Gestione pacchetti Nuget azioni dell'interfaccia utente - [&#2705;](https://github.com/NuGet/Home/issues/2705)

* Correggere la configurazione NuGet è un errore non valido nei progetti di sito Web - VS 2015 VSIX (v3.4.3) - [&#2667;](https://github.com/NuGet/Home/issues/2667)

* Risolvere i problemi di Service pack da `.csproj` quando i file di contenuto sono inclusi - [&#2658;](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) non funziona - [&#2653;](https://github.com/NuGet/Home/issues/2653)

* Risolvere un problema nella versione Nuget versione 3.4.3 - valore non può essere null per la creazione del pacchetto - [&#2648;](https://github.com/NuGet/Home/issues/2648)

* Ripristino utilizza le credenziali archiviate da NuGet. config per i feed di VSTS - [&#2647;](https://github.com/NuGet/Home/issues/2647)

* Prestazioni - correzione allocazioni eccessive nel codice di confronto versione - [&#2632;](https://github.com/NuGet/Home/issues/2632)

* Risolvere i problemi quando più istanze di nuget.exe tenta di installare lo stesso pacchetto in parallelo - [&#2628;](https://github.com/NuGet/Home/issues/2628)

* Prestazioni - Cache le informazioni sulle dipendenze per le operazioni multiprogetto - [&#2619;](https://github.com/NuGet/Home/issues/2619)

* Risolvere problema in cui non è possibile origini pacchetto aggiunte dall'impostazioni quando l'elenco di origine è vuota - [&#2617;](https://github.com/NuGet/Home/issues/2617)

* Correggere l'errore Misleading durante il tentativo di installare il pacchetto che dipende dalla fase di progettazione aspetti - [&#2594;](https://github.com/NuGet/Home/issues/2594)

* Installa un pacchetto dalla console PackageManager con l'impostazione "All" tenta prima origine - [&#2557;](https://github.com/NuGet/Home/issues/2557)

* Risolvere i problemi con i pacchetti che contengono file con tempi di scrittura in futuro (Mono) - [&#2518;](https://github.com/NuGet/Home/issues/2518)

* Visualizzare l'eccezione quando si verifica un errore per i progetti di ricerca nel comando update - [&#2418;](https://github.com/NuGet/Home/issues/2418)

* Contenuto del pacchetto non verrà ripristinato correttamente quando si installa un pacchetto da nuget 3.3 + feed con l'argomento - NoCache quando il pacchetto contiene `.nupkg` file - [&#2354;](https://github.com/NuGet/Home/issues/2354)

* Problema di correzione con pacchetto installa (tutte le origini) quando il pacchetto non è presente 1 origine - [&#2322;](https://github.com/NuGet/Home/issues/2322)

* Installare blocchi se una singola origine si verifica un errore di autorizzazione - [&#2034;](https://github.com/NuGet/Home/issues/2034)

* `.nuspec`versione intervallo deve eseguire l'override di versione - IncludeReferencedProjects - [&#1983;](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0 aggiornamento ha esito negativo con '... un vincolo aggiuntivo definito nel file Packages. config impedisce questa operazione.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* aggiornamento di NuGet.exe elimina il nome sicuro dell'assembly e l'attributo privata. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Risolvere i problemi con il percorso relativo del file per "DefaultPushSource" - [&#1746;](https://github.com/NuGet/Home/issues/1746)

* Migliorare i messaggi di errore di sistema di risoluzione Update - [&#1373;](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Funzionalità e modifiche del comportamento

* NuGet.exe push: parametro di timeout non funziona - [&#2785;](https://github.com/NuGet/Home/issues/2785)

* non produce NuGet.exe restore `.props` e `.targets` file per `.nuproj` progetti (regressione in v3.4.3.855) - [&#2711;](https://github.com/NuGet/Home/issues/2711)

* È necessario confrontare Framework con importazioni - l'API di estensibilità [&#2633;](https://github.com/NuGet/Home/issues/2633)

* Nascondere le opzioni di dipendenza quando si utilizza `project.json`  -  [&#2486;](https://github.com/NuGet/Home/issues/2486)

* Stampa l'intestazione di versione nuget.exe in output dettagliato - [&#1887;](https://github.com/NuGet/Home/issues/1887)

* NuGet è necessario aggiungere il supporto per /nativeassets/ /runtimes/ {rid} {txm} / - [&#2782;](https://github.com/NuGet/Home/issues/2782)