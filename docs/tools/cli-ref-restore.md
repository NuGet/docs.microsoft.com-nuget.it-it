---
title: Comando restore di NuGet CLI
description: Informazioni di riferimento per il comando restore nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3d7a4188de4fb6f812ca19e7f9e302a5a133c58b
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425963"
---
# <a name="restore-command-nuget-cli"></a>comando Restore (NuGet CLI)

**Si applica a:** consumo del pacchetto &bullet; **versioni supportate:** 2.7+

Scarica e installa tutti i pacchetti mancanti dal `packages` cartella. Quando usato con NuGet 4.0 + e il formato PackageReference, genera una `<project>.nuget.props` file, se necessario, nel `obj` cartella. (Il file può essere omesso dal controllo del codice sorgente).

In Mac OSX e Linux con l'interfaccia della riga di comando su Mono, il ripristino dei pacchetti non è supportato con PackageReference.

## <a name="usage"></a>Utilizzo

```cli
nuget restore <projectPath> [options]
```

in cui `<projectPath>` specifica il percorso di una soluzione o un `packages.config` file. Visualizzare [osservazioni](#remarks) seguito per informazioni dettagliate comportamentale.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | Il file di configurazione di NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.|
| DirectDownload | *(4.0 +)*  Scarica i pacchetti direttamente senza la compilazione di memorizzazione nella cache con tutti i file binari o i metadati. |
| DisableParallelProcessing | Disabilita il ripristino di più pacchetti in parallelo. |
| FallbackSource | *(3.2 +)*  Un elenco di origini dei pacchetti da usare come fallback nel caso in cui il pacchetto non viene trovato nel database primario o di un'origine predefinita. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese. |
| Help | Visualizza la Guida informazioni per il comando. |
| MSBuildPath | *(4.0 +)*  Specifica il percorso di MSBuild da usare con il comando, hanno la precedenza sui `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Specifica la versione di MSBuild da usare con questo comando. Valori supportati sono 4, 12, 14, 15.1, versione 15.3, versione 15.4, 15.5, 15.6, 15.7, 15.8, 15.9. Per impostazione predefinita che viene selezionato nel proprio percorso di MSBuild, in caso contrario, per impostazione predefinita la versione installata più recente di MSBuild. |
| NoCache | Impedisce l'uso di pacchetti memorizzati nella cache NuGet. Visualizzare [gestione dei pacchetti globali e le cartelle cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Elimina richieste di input o conferme dell'utente. |
| OutputDirectory | Specifica la cartella in cui sono installati i pacchetti. Se si specifica alcuna cartella, viene utilizzata la cartella corrente. Obbligatorio quando il ripristino con un `packages.config` file, a meno che `PackagesDirectory` o `SolutionDirectory` viene usato.|
| PackageSaveMode | Specifica i tipi di file da salvare dopo l'installazione del pacchetto: uno dei `nuspec`, `nupkg`, o `nuspec;nupkg`. |
| PackagesDirectory | Uguale a `OutputDirectory`. Obbligatorio quando il ripristino con un `packages.config` file, a meno che `OutputDirectory` o `SolutionDirectory` viene usato. |
| Project2ProjectTimeOut | Timeout in secondi per la risoluzione di riferimenti da progetto a progetto. |
| Ricorsivo | *(4.0 +)*  Ripristina tutti i riferimenti a progetti per i progetti UWP e .NET Core. Non si applica ai progetti che usano `packages.config`. |
| RequireConsent | Verifica che il ripristino dei pacchetti sia abilitato prima di scaricare e installare i pacchetti. Per informazioni dettagliate, vedere [ripristino dei pacchetti](../consume-packages/package-restore.md). |
| SolutionDirectory | Specifica la cartella della soluzione. Non è valido durante il ripristino dei pacchetti per una soluzione. Obbligatorio quando il ripristino con un `packages.config` file, a meno che `PackagesDirectory` o `OutputDirectory` viene usato. |
| Origine | Specifica l'elenco delle origini dei pacchetti (sotto forma di URL) da usare per il ripristino. Se omesso, il comando Usa le origini fornite nei file di configurazione, vedere [comportamento di configurazione NuGet](../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="remarks"></a>Note

Il comando restore esegue i passaggi seguenti:

1. Determinare la modalità operativa del comando restore.

   | tipo di file projectPath | Comportamento |
   | --- | --- |
   | Soluzione (cartella) | NuGet Cerca un `.sln` file e ne utilizza se presente; in caso contrario, restituisce un errore. `(SolutionDir)\.nuget` viene usato come cartella di avvio. |
   | `.sln` File | Ripristinare i pacchetti identificati per la soluzione. Restituisce un errore se `-SolutionDirectory` viene usato. `$(SolutionDir)\.nuget` viene usato come cartella di avvio. |
   | `packages.config` o file di progetto | Ripristinare i pacchetti elencati nel file, la risoluzione e installazione delle dipendenze. |
   | Altro tipo di file | File presuppone che sia un `.sln` file come illustrato in precedenza; se non è una soluzione, NuGet fornisce un errore. |
   | (projectPath non specificato) | <ul><li>NuGet cerca i file della soluzione nella cartella corrente. Se viene trovato un singolo file, che viene utilizzato per ripristinare i pacchetti; Se vengono trovate più soluzioni, NuGet restituisce un errore.</li><li>Se non sono presenti file di soluzione, NuGet Cerca un `packages.config` che verrà usata per ripristinare i pacchetti.</li><li>Se nessuna soluzione o `packages.config` file è stato trovato, NuGet genera un errore.</ul> |

2. Determinare la cartella dei pacchetti utilizzando il seguente ordine di priorità (NuGet restituisce un errore se nessuna di queste cartelle vengono rilevata):

    - La cartella specificata con `-PackagesDirectory`.
    - Il `repositoryPath` valore in `Nuget.Config`
    - La cartella specificata con `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Quando si ripristinano i pacchetti per una soluzione, NuGet esegue le operazioni seguenti:
    - Carica il file della soluzione.
    - Consente di ripristinare i pacchetti a livello di soluzione elencati nel `$(SolutionDir)\.nuget\packages.config` nella `packages` cartella.
    - Ripristinare i pacchetti elencati nel `$(ProjectDir)\packages.config` nella `packages` cartella. Per ogni pacchetto specificato, ripristinare il pacchetto in parallelo, a meno che `-DisableParallelProcessing` è specificato.

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
