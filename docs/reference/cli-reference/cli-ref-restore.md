---
title: Comando di ripristino di NuGet CLI
description: Riferimento per il comando di ripristino di NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 8ba61fa87118108c36e9dc73f30d964380d02dab
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380463"
---
# <a name="restore-command-nuget-cli"></a>comando Restore (interfaccia della riga di comando di NuGet)

**Si applica a:** utilizzo pacchetti &bullet; **versioni supportate:** 2.7 +

Scarica e installa tutti i pacchetti mancanti dalla cartella `packages`. Se usato con NuGet 4.0 + e il formato PackageReference, genera un file di `<project>.nuget.props`, se necessario, nella cartella `obj`. Il file può essere omesso dal controllo del codice sorgente.

In Mac OSX e Linux con l'interfaccia della riga di comando in mono, il ripristino dei pacchetti non è supportato con PackageReference.

## <a name="usage"></a>Utilizzo

```cli
nuget restore <projectPath> [options]
```

dove `<projectPath>` specifica il percorso di una soluzione o di un file di `packages.config`. Per informazioni sui comportamenti, vedere la [sezione Osservazioni](#remarks) di seguito.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | File di configurazione NuGet da applicare. Se non specificato, viene usato `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| DirectDownload | *(4.0 +)* Scarica i pacchetti direttamente senza popolare le cache con i file binari o i metadati. |
| DisableParallelProcessing | Disabilita il ripristino di più pacchetti in parallelo. |
| FallbackSource | *(3.2 +)* Elenco di origini di pacchetti da usare come fallback nel caso in cui il pacchetto non venga trovato nell'origine primaria o predefinita. Utilizzare un punto e virgola per separare le voci dell'elenco. |
| ForceEnglishOutput | *(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| ? | Visualizza le informazioni della Guida per il comando. |
| MSBuildPath | *(4.0 +)* Specifica il percorso di MSBuild da usare con il comando, che ha la precedenza su `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)* Specifica la versione di MSBuild da usare con questo comando. I valori supportati sono 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Per impostazione predefinita, viene scelto MSBuild nel percorso; in caso contrario, per impostazione predefinita viene impostata la versione più recente di MSBuild. |
| NoCache | Impedisce a NuGet di usare pacchetti memorizzati nella cache. Vedere [gestione dei pacchetti globali e delle cartelle della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| Non interattiva | Evita la richiesta di input o conferme dell'utente. |
| OutputDirectory | Specifica la cartella in cui sono installati i pacchetti. Se non viene specificata alcuna cartella, viene utilizzata la cartella corrente. Obbligatorio quando si esegue il ripristino con un file di `packages.config` a meno che non venga utilizzato `PackagesDirectory` o `SolutionDirectory`.|
| PackageSaveMode | Specifica i tipi di file da salvare dopo l'installazione del pacchetto: uno dei `nuspec`, `nupkg` o `nuspec;nupkg`. |
| PackagesDirectory | Uguale a `OutputDirectory`. Obbligatorio quando si esegue il ripristino con un file di `packages.config` a meno che non venga utilizzato `OutputDirectory` o `SolutionDirectory`. |
| Project2ProjectTimeOut | Timeout in secondi per la risoluzione di riferimenti da progetto a progetto. |
| ricorsiva | *(4.0 +)* Ripristina tutti i progetti di riferimento per i progetti UWP e .NET Core. Non si applica ai progetti che usano `packages.config`. |
| RequireConsent | Verifica che il ripristino dei pacchetti sia abilitato prima di scaricare e installare i pacchetti. Per informazioni dettagliate, vedere [ripristino di pacchetti](../../consume-packages/package-restore.md). |
| SolutionDirectory | Specifica la cartella della soluzione. Non valido durante il ripristino dei pacchetti per una soluzione. Obbligatorio quando si esegue il ripristino con un file di `packages.config` a meno che non venga utilizzato `PackagesDirectory` o `OutputDirectory`. |
| Origine | Specifica l'elenco di origini di pacchetti (come URL) da usare per il ripristino. Se omesso, il comando usa le origini fornite nei file di configurazione, vedere [configurazione del comportamento di NuGet](../../consume-packages/configuring-nuget-behavior.md). Utilizzare un punto e virgola per separare le voci dell'elenco. |
| Forzare | Nei progetti basati su PackageReference, impone la risoluzione di tutte le dipendenze anche se l'ultimo ripristino ha avuto esito positivo. La specifica di questo flag è simile all'eliminazione del file `project.assets.json`. Questa operazione non consente di ignorare la cache HTTP. |
| Livello di dettaglio | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="remarks"></a>Note

Il comando RESTORE esegue i passaggi seguenti:

1. Determinare la modalità operativa del comando Restore.

   | tipo di file projectPath | Comportamento |
   | --- | --- |
   | Soluzione (cartella) | NuGet Cerca un file di `.sln` e lo usa se è stato trovato; in caso contrario, restituisce un errore. `(SolutionDir)\.nuget` viene utilizzata come cartella iniziale. |
   | file `.sln` | Ripristinare i pacchetti identificati dalla soluzione; Restituisce un errore se viene utilizzato `-SolutionDirectory`. `$(SolutionDir)\.nuget` viene utilizzata come cartella iniziale. |
   | `packages.config` o file di progetto | Ripristinare i pacchetti elencati nel file, risolvendo e installando le dipendenze. |
   | Altro tipo di file | Si presuppone che il file sia un file di `.sln` come sopra; Se non si tratta di una soluzione, NuGet restituisce un errore. |
   | (projectPath non specificato) | <ul><li>NuGet Cerca i file della soluzione nella cartella corrente. Se viene trovato un singolo file, viene usato per ripristinare i pacchetti; Se vengono rilevate più soluzioni, NuGet restituisce un errore.</li><li>Se non sono presenti file di soluzione, NuGet Cerca un `packages.config` e lo usa per ripristinare i pacchetti.</li><li>Se non viene trovato alcun file di soluzione o di `packages.config`, NuGet restituisce un errore.</ul> |

2. Determinare la cartella dei pacchetti usando l'ordine di priorità seguente (NuGet restituisce un errore se nessuna di queste cartelle viene trovata):

    - Cartella specificata con `-PackagesDirectory`.
    - Valore `repositoryPath` in `Nuget.Config`
    - Cartella specificata con `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Quando si ripristinano i pacchetti per una soluzione, NuGet esegue le operazioni seguenti:
    - Carica il file di soluzione.
    - Ripristina i pacchetti a livello di soluzione elencati in `$(SolutionDir)\.nuget\packages.config` nella cartella `packages`.
    - Ripristinare i pacchetti elencati in `$(ProjectDir)\packages.config` nella cartella `packages`. Per ogni pacchetto specificato, ripristinare il pacchetto in parallelo, a meno che non sia specificato `-DisableParallelProcessing`.

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
