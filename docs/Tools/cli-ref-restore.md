---
title: Comando di ripristino NuGet CLI | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando di ripristino di nuget.exe
keywords: NuGet riferimento di ripristino, ripristinare il comando di pacchetti
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 93d7b6967d9297ee822df1583351385210775173
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="restore-command-nuget-cli"></a>comando di ripristino (NuGet CLI)

**Si applica a:** pacchetto consumo &bullet; **le versioni supportate:** 2.7 +

Scarica e installa tutti i pacchetti manca il `packages` cartella. Se utilizzato con NuGet 4.0 + e il formato PackageReference, genera un `<project>.nuget.props` file, se necessario, nel `obj` cartella. (Il file può essere omesso dal controllo del codice sorgente).

In Mac OSX e Linux con l'interfaccia CLI su Mono, il ripristino di pacchetti non è supportato con PackageReference.

## <a name="usage"></a>Utilizzo

```cli
nuget restore <projectPath> [options]
```

dove `<projectPath>` specifica il percorso di una soluzione o un `packages.config` file. Vedere [osservazioni](#remarks) sotto per informazioni dettagliate di comportamento.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | Il file di configurazione NuGet da applicare. Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato. |
| DirectDownload | *(4.0 +)*  Scarica i pacchetti direttamente senza popolamento della cache con qualsiasi file binari o metadati. |
| DisableParallelProcessing | Disabilita il ripristino di più pacchetti in parallelo. |
| FallbackSource | *(3.2 +)*  Un elenco delle origini pacchetto da utilizzare come fallback nel caso in cui il pacchetto non viene trovato nel database primario o di origine predefinita. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| MSBuildPath | *(4.0 +)*  Specifica il percorso di MSBuild da usare con il comando, che avrà la precedenza `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Specifica la versione di MSBuild da usare con questo comando. Valori supportati sono 4, 12, 14, 15. Per impostazione predefinita che viene selezionato il percorso di MSBuild, in caso contrario il valore predefinito la versione più aggiornata di MSBuild. |
| NoCache | Impedisce l'utilizzo di pacchetti dalla cache locale NuGet. |
| NonInteractive | Elimina richieste per l'input dell'utente o le conferme. |
| OutputDirectory | Specifica la cartella in cui sono installati i pacchetti. Se viene specificata alcuna cartella, viene utilizzata la cartella corrente. |
| PackageSaveMode | Specifica i tipi di file da salvare dopo l'installazione del pacchetto: uno dei `nuspec`, `nupkg`, o `nuspec;nupkg`. |
| PackagesDirectory | Uguale a `OutputDirectory`. |
| Project2ProjectTimeOut | Timeout in secondi per la risoluzione di riferimenti da progetto a progetto. |
| Ricorsivo | *(4.0 +)*  Ripristina tutti i riferimenti a progetti per i progetti UWP e .NET Core. Non si applica ai progetti mediante `packages.config`. |
| RequireConsent | Verifica che il ripristino dei pacchetti è abilitato prima di scaricare e installare i pacchetti. Per informazioni dettagliate, vedere [il ripristino del pacchetto](../consume-packages/package-restore.md). |
| SolutionDirectory | Specifica la cartella della soluzione. Non è valido durante il ripristino dei pacchetti per una soluzione. |
| Origine | Specifica l'elenco delle origini pacchetto (come URL) da usare per il ripristino. Se omesso, il comando Usa le origini disponibili in file di configurazione, vedere [il comportamento di configurazione NuGet](../Consume-Packages/Configuring-NuGet-Behavior.md). |
| Livello di dettaglio |> specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="remarks"></a>Note

Il comando di ripristino esegue la procedura seguente:

1. Determinare la modalità operativa del comando restore.
    tipo di file projectPath | Comportamento
    | --- | --- |
    Soluzione (cartella) | NuGet Cerca un `.sln` file e ne utilizza se trovato; in caso contrario, restituisce un errore. `(SolutionDir)\.nuget`viene utilizzata come cartella di avvio.
    `.sln`file | Ripristino dei pacchetti identificati dalla soluzione. Se si verifica un errore `-SolutionDirectory` viene utilizzato. `$(SolutionDir)\.nuget`viene utilizzata come cartella di avvio.
    `packages.config`o file di progetto | Ripristino dei pacchetti elencati nel file, risoluzione e installazione delle dipendenze.
    Altro tipo di file | File viene considerato un `.sln` file sopra; se non è una soluzione, NuGet consente un errore.
    (projectPath non specificato) | -NuGet cerca i file di soluzione nella cartella corrente. Se viene trovato un singolo file, che viene utilizzato per ripristinare i pacchetti; Se vengono trovate più soluzioni, NuGet consente di un errore.
    |-Se non sono presenti file di soluzione, NuGet esegue la ricerca di un `packages.config` e utilizza quello per il ripristino dei pacchetti.
    |-Se nessuna soluzione o `packages.config` file è stato trovato, NuGet restituisce un errore.

1. Determinare la cartella di pacchetti utilizzando il seguente ordine di priorità (NuGet restituisce un errore se nessuna di queste cartelle si trovano):

    - La cartella specificata con `-PackagesDirectory`.
    - Il `repositoryPath` valore in`Nuget.Config`
    - La cartella specificata con`-SolutionDirectory`
    - `$(SolutionDir)\packages`

1. Durante il ripristino dei pacchetti per una soluzione, NuGet esegue le operazioni seguenti:
    - Carica il file della soluzione.
    - Ripristina i pacchetti della soluzione livello elencati in `$(SolutionDir)\.nuget\packages.config` nel `packages` cartella.
    - Ripristino dei pacchetti elencati in `$(ProjectDir)\packages.config` nel `packages` cartella. Per ogni pacchetto specificato, ripristinare il pacchetto in parallelo, a meno che non `-DisableParallelProcessing` specificato.

## <a name="examples"></a>Esempi

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
