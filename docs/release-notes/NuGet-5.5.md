---
title: Note sulla versione di NuGet 5,5
description: Note sulla versione per NuGet 5,5, incluse nuove funzionalità, correzioni di bug e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0fde67dd03c31e986ed89f2f8627608e279ef908
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780106"
---
# <a name="nuget-55-release-notes"></a>Note sulla versione di NuGet 5,5

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio| Disponibile in .NET SDK|
|:---|:---|:---|
| [**5.5.0**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16,5](https://visualstudio.microsoft.com/downloads/) | [3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Installato con Visual Studio 2019 con carico di lavoro di .NET Core

## <a name="summary-whats-new-in-55"></a>Riepilogo: novità di 5,5

* Esperienza migliorata per l'accessibilità e la lettura dello schermo per l'interfaccia utente di gestione pacchetti NuGet in Visual Studio
    * Problemi di accessibilità nelle esperienze di lettura schermo, altText mancanti e nome accessibile per la casella di testo installata e così via,- [#9059](https://github.com/NuGet/Home/issues/9059)
    * Problemi di accessibilità nelle esperienze di lettura schermo nell'elenco dei pacchetti- [#9077](https://github.com/NuGet/Home/issues/9077)
    * Problemi di accessibilità nelle esperienze di lettura schermo correlate alle schede "Sfoglia", "Install", "Update"- [#9078](https://github.com/NuGet/Home/issues/9078)
    * Assistente vocale non annuncia l'etichetta di collegamento "blank", "No dependencies", "NuGet. org", "MIT" [#9157](https://github.com/NuGet/Home/issues/9157)

* Supporto per la visualizzazione di icone autosufficienti nell'interfaccia utente di gestione pacchetti di Visual Studio per i pacchetti ospitati nei feed locali- [#8189](https://github.com/NuGet/Home/issues/8189)

* Miglioramento significativo delle prestazioni di ripristino senza op mediante `RestoreUseStaticGraphEvaluation` la quale è possibile velocizzare le valutazioni chiamando API Graph statiche di MSBuild- [8791](https://github.com/NuGet/Home/issues/8791)

* Miglioramento dell'affidabilità dotnet.exe con i plug-in di autenticazione multipiattaforma
    * dotnet restore non riuscito con TaskCanceledException- [#7842](https://github.com/NuGet/Home/issues/7842)
    * Plug-in: "un'attività è stata annullata". problema con l'autenticazione ADO a causa di questo. - [#8528](https://github.com/NuGet/Home/issues/8528)

* Aggiungi `dotnet nuget <add|remove|update|disable|enable|list> source` [#4126](https://github.com/NuGet/Home/issues/4126) comando

* Eseguire il `--skip-duplicate`  push per l'uso di DotNet NuGet push- [#8778](https://github.com/NuGet/Home/issues/8778)

* Supporto `packages.config` con MSBuild/Restore- [#8506](https://github.com/NuGet/Home/issues/8506)

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**Bug**

* Rielaborare Self-Updater con le API V3- [#4197](https://github.com/NuGet/Home/issues/4197)

* Versione di dipendenza del pacchetto errata se la versione della dipendenza del pacchetto è impostata su' *'- [#6697](https://github.com/NuGet/Home/issues/6697)

* Il messaggio di errore ErrorUnsafePackageEntry non punta all'origine del problema [#7505](https://github.com/NuGet/Home/issues/7505)

* Il file di blocco non è rispettato negli scenari "*": [#8073](https://github.com/NuGet/Home/issues/8073)

* NuGet.exe non si risolve nella versione più recente di un pacchetto quando si usa * in PackageReference (MSBuild/DotNet/VS Restore do)- [#8432](https://github.com/NuGet/Home/issues/8432)

* pacchetto di elenco DotNet con il progetto WPF con più destinazioni- [#8463](https://github.com/NuGet/Home/issues/8463)

* Migliorare ConcurrencyUtilities (ridurre l'utilizzo della CPU)- [#8653](https://github.com/NuGet/Home/issues/8653)

* Le specifiche DG per gli scenari di progetto scaricati non devono essere scritte nei ripristini di anteprima [#8793](https://github.com/NuGet/Home/issues/8793)

* I pacchetti NuGet di Visual Studio (RestoreManagerPackage) devono essere caricati automaticamente sugli eventi di compilazione della soluzione- [#8796](https://github.com/NuGet/Home/issues/8796)

* Deadlock in VSSettings init- [#8842](https://github.com/NuGet/Home/issues/8842)

* La casella degli strumenti VisualStudio non viene popolata da un pacchetto NuGet se un progetto viene inserito in una cartella della soluzione [#8868](https://github.com/NuGet/Home/issues/8868)

* Visual Studio: il ripristino della soluzione ha esito negativo a causa della [#8881](https://github.com/NuGet/Home/issues/8881) race condition

* Costante "Loading.." nella scheda installata e "ricerca <term>.. "nella scheda aggiornamenti- [#8890](https://github.com/NuGet/Home/issues/8890)

* Icone incorporate mancanti nell'interfaccia utente di Visual Studio dopo la scadenza della cache- [#9069](https://github.com/NuGet/Home/issues/9069)

* Avvio interfaccia utente FireAndForget- [#9112](https://github.com/NuGet/Home/issues/9112)

* Restore: l'implementazione di IncludeExcludeFiles. Equals (...) non è corretta- [#9167](https://github.com/NuGet/Home/issues/9167)

* Restore: PackageSpec. Clone () crea un clone diverso- [#9211](https://github.com/NuGet/Home/issues/9211)

* Elenco errori visualizzato anche se "Mostra sempre Elenco errori se la compilazione termina con errori" non è selezionata- [#8190](https://github.com/NuGet/Home/issues/8190)

* Il ripristino statico del grafo non deve superare SolutionPath- [#9061](https://github.com/NuGet/Home/issues/9061) vuoti

* Ripristino: chiusura calcolata per ogni progetto 4 volte- [#9042](https://github.com/NuGet/Home/issues/9042)

* Restore: DependencyGraphSpec. Load (...) non necessita di JObject- [#9040](https://github.com/NuGet/Home/issues/9040)

* Restore: stringhe di grandi dimensioni create nell'heap degli oggetti grandi (LOH)- [#9031](https://github.com/NuGet/Home/issues/9031)

* nuget.exe personalizzati sul mono più recente potrebbero interrompersi a causa del sistema di risoluzione dell'SDK di MSBuild- [8848](https://github.com/NuGet/Home/issues/8848)

* il ripristino non riesce quando nuget.dgspec.jssu è "usato da un altro processo"- [8692](https://github.com/NuGet/Home/issues/8692)

**DCR**

* La logica in _GetRestoreProjectStyle deve trovarsi in un'attività- [#8804](https://github.com/NuGet/Home/issues/8804)

* Aggiungere le informazioni di deprecazione per impostazione predefinita nella scheda installato- [#8541](https://github.com/NuGet/Home/issues/8541)

**[Elenco di tutti i problemi risolti in questa versione-5,5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**
