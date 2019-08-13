---
title: Comando di ripristino di NuGet CLI
description: Riferimento per il comando di ripristino di NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 211f24ff67c06da00d6a014e679cc422d493d6d5
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959734"
---
# <a name="restore-command-nuget-cli"></a>comando Restore (interfaccia della riga di comando di NuGet)

**Si applica a:** &bullet; **versioni supportate** per l'utilizzo di pacchetti: 2.7+

Scarica e installa tutti i pacchetti mancanti nella `packages` cartella. Se usato con NuGet 4.0 + e il formato PackageReference, genera un `<project>.nuget.props` file, se necessario, `obj` nella cartella. Il file può essere omesso dal controllo del codice sorgente.

In Mac OSX e Linux con l'interfaccia della riga di comando in mono, il ripristino dei pacchetti non è supportato con PackageReference.

## <a name="usage"></a>Utilizzo

```cli
nuget restore <projectPath> [options]
```

dove `<projectPath>` specifica il percorso di una soluzione o di `packages.config` un file. Per informazioni sui comportamenti, vedere la [sezione Osservazioni](#remarks) di seguito.

## <a name="options"></a>Opzioni

| Opzione | DESCRIZIONE |
| --- | --- |
| ConfigFile | File di configurazione NuGet da applicare. Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| DirectDownload | *(4.0 +)* Scarica i pacchetti direttamente senza popolare le cache con i file binari o i metadati. |
| DisableParallelProcessing | Disabilita il ripristino di più pacchetti in parallelo. |
| FallbackSource | *(3.2 +)* Elenco di origini di pacchetti da usare come fallback nel caso in cui il pacchetto non venga trovato nell'origine primaria o predefinita. Utilizzare un punto e virgola per separare le voci dell'elenco. |
| ForceEnglishOutput | *(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| Help | Visualizza le informazioni della Guida per il comando. |
| MSBuildPath | *(4.0 +)* Specifica il percorso di MSBuild da usare con il comando, avendo la precedenza `-MSBuildVersion`su. |
| MSBuildVersion | *(3.2 +)* Specifica la versione di MSBuild da usare con questo comando. I valori supportati sono 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Per impostazione predefinita, viene scelto MSBuild nel percorso; in caso contrario, per impostazione predefinita viene impostata la versione più recente di MSBuild. |
| NoCache | Impedisce a NuGet di usare pacchetti memorizzati nella cache. Vedere [gestione dei pacchetti globali e delle cartelle della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Evita la richiesta di input o conferme dell'utente. |
| OutputDirectory | Specifica la cartella in cui sono installati i pacchetti. Se non viene specificata alcuna cartella, viene utilizzata la cartella corrente. Obbligatorio quando si esegue il `packages.config` ripristino con un `PackagesDirectory` file `SolutionDirectory` a meno che non venga usato o.|
| PackageSaveMode | Specifica i tipi di file da salvare dopo l'installazione del pacchetto: `nuspec`uno `nupkg`tra, `nuspec;nupkg`o. |
| PackagesDirectory | Uguale a `OutputDirectory`. Obbligatorio quando si esegue il `packages.config` ripristino con un `OutputDirectory` file `SolutionDirectory` a meno che non venga usato o. |
| Project2ProjectTimeOut | Timeout in secondi per la risoluzione di riferimenti da progetto a progetto. |
| Ricorsiva | *(4.0 +)* Ripristina tutti i progetti di riferimento per i progetti UWP e .NET Core. Non si applica ai progetti che `packages.config`usano. |
| RequireConsent | Verifica che il ripristino dei pacchetti sia abilitato prima di scaricare e installare i pacchetti. Per informazioni dettagliate, vedere [ripristino di pacchetti](../../consume-packages/package-restore.md). |
| SolutionDirectory | Specifica la cartella della soluzione. Non valido durante il ripristino dei pacchetti per una soluzione. Obbligatorio quando si esegue il `packages.config` ripristino con un `PackagesDirectory` file `OutputDirectory` a meno che non venga usato o. |
| Source | Specifica l'elenco di origini di pacchetti (come URL) da usare per il ripristino. Se omesso, il comando usa le origini fornite nei file di configurazione, vedere [configurazione del comportamento di NuGet](../../consume-packages/configuring-nuget-behavior.md). Utilizzare un punto e virgola per separare le voci dell'elenco. |
| Verbosity | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="remarks"></a>Note

Il comando RESTORE esegue i passaggi seguenti:

1. Determinare la modalità operativa del comando Restore.

   | tipo di file projectPath | Comportamento |
   | --- | --- |
   | Soluzione (cartella) | NuGet Cerca un `.sln` file e lo usa se è stato trovato; in caso contrario, restituisce un errore. `(SolutionDir)\.nuget`viene utilizzato come cartella iniziale. |
   | `.sln`file | Ripristinare i pacchetti identificati dalla soluzione; Restituisce un errore se `-SolutionDirectory` viene utilizzato. `$(SolutionDir)\.nuget`viene utilizzato come cartella iniziale. |
   | `packages.config`o file di progetto | Ripristinare i pacchetti elencati nel file, risolvendo e installando le dipendenze. |
   | Altro tipo di file | Si presuppone che il file sia `.sln` un file come sopra; se non è una soluzione, NuGet restituisce un errore. |
   | (projectPath non specificato) | <ul><li>NuGet Cerca i file della soluzione nella cartella corrente. Se viene trovato un singolo file, viene usato per ripristinare i pacchetti; Se vengono rilevate più soluzioni, NuGet restituisce un errore.</li><li>Se non sono presenti file di soluzione, NuGet Cerca un `packages.config` oggetto e lo usa per ripristinare i pacchetti.</li><li>Se non viene trovata `packages.config` alcuna soluzione o file, NuGet restituisce un errore.</ul> |

2. Determinare la cartella dei pacchetti usando l'ordine di priorità seguente (NuGet restituisce un errore se nessuna di queste cartelle viene trovata):

    - Cartella specificata con `-PackagesDirectory`.
    - Il `repositoryPath` valore in`Nuget.Config`
    - Cartella specificata con`-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Quando si ripristinano i pacchetti per una soluzione, NuGet esegue le operazioni seguenti:
    - Carica il file di soluzione.
    - Ripristina i `$(SolutionDir)\.nuget\packages.config` `packages` pacchetti a livello di soluzione elencati nella cartella.
    - Ripristinare i `$(ProjectDir)\packages.config` `packages` pacchetti elencati nella cartella. Per ogni pacchetto specificato, ripristinare il pacchetto in parallelo, a `-DisableParallelProcessing` meno che non sia specificato.

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
