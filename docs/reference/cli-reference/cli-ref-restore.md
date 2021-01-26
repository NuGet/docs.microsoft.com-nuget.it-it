---
title: Comando di ripristino di NuGet CLI
description: Riferimento per il comando nuget.exe Restore
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 49fabbd0ef0c1c0c16f13bdf741296575fa72359
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780033"
---
# <a name="restore-command-nuget-cli"></a>comando Restore (interfaccia della riga di comando di NuGet)

**Si applica a:** versioni supportate per l'utilizzo di pacchetti &bullet; **:** 2.7 +

Scarica e installa tutti i pacchetti mancanti nella `packages` cartella. Se usato con NuGet 4.0 + e il formato PackageReference, genera un `<project>.nuget.props` file, se necessario, nella `obj` cartella. Il file può essere omesso dal controllo del codice sorgente.

In Mac OSX e Linux con l'interfaccia della riga di comando in mono, il ripristino dei pacchetti non è supportato con PackageReference.

## <a name="usage"></a>Utilizzo

```cli
nuget restore <projectPath> [options]
```

dove `<projectPath>` specifica il percorso di una soluzione o di un `packages.config` file. Per informazioni sui comportamenti, vedere la [sezione Osservazioni](#remarks) di seguito.

## <a name="options"></a>Opzioni

- **`-ConfigFile`**

  File di configurazione NuGet da applicare. Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-DirectDownload`**

  *(4.0 +)* Scarica i pacchetti direttamente senza popolare le cache con i file binari o i metadati.

- **`-DisableParallelProcessing`**

   Disabilita il ripristino di più pacchetti in parallelo.

- **`-FallbackSource`**

  *(3.2 +)* Elenco di origini di pacchetti da usare come fallback nel caso in cui il pacchetto non venga trovato nell'origine primaria o predefinita. Utilizzare un punto e virgola per separare le voci dell'elenco.

- **`-Force`**

  Nei progetti basati su PackageReference, impone la risoluzione di tutte le dipendenze anche se l'ultimo ripristino ha avuto esito positivo. La specifica di questo flag è simile all'eliminazione del `project.assets.json` file. Questa operazione non consente di ignorare la cache HTTP.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.

- **`-ForceEvaluate`**

  Forza il ripristino per rivalutare tutte le dipendenze anche se un file di blocco esiste già.

- **`-?|-help`**

  Visualizza le informazioni della Guida per il comando.

- **`-LockFilePath`**

  Percorso di output in cui viene scritto il file di blocco del progetto. Per impostazione predefinita, tale valore è `PROJECT_ROOT\packages.lock.json`.

- **`-LockedMode`**

  Non consentire l'aggiornamento del file di blocco del progetto.

- **`-MSBuildPath`**

   *(4.0 +)* Specifica il percorso di MSBuild da usare con il comando, avendo la precedenza su `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 +)* Specifica la versione di MSBuild da usare con questo comando. I valori supportati sono 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Per impostazione predefinita, viene scelto MSBuild nel percorso; in caso contrario, per impostazione predefinita viene impostata la versione più recente di MSBuild.

- **`-NoCache`**

  Impedisce a NuGet di usare pacchetti memorizzati nella cache. Vedere [gestione dei pacchetti globali e delle cartelle della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-NonInteractive`**

  Evita la richiesta di input o conferme dell'utente.

- **`-OutputDirectory`**

  Specifica la cartella in cui sono installati i pacchetti. Se non viene specificata alcuna cartella, viene utilizzata la cartella corrente. Obbligatorio quando si esegue il ripristino con un `packages.config` file a meno che non `PackagesDirectory` `SolutionDirectory` venga usato o.

- **`-PackageSaveMode`**

  Specifica i tipi di file da salvare dopo l'installazione del pacchetto: uno tra `nuspec` , `nupkg` o `nuspec;nupkg` .

- **`-PackagesDirectory`**

  Uguale a `OutputDirectory`. Obbligatorio quando si esegue il ripristino con un `packages.config` file a meno che non `OutputDirectory` `SolutionDirectory` venga usato o.

- **`-Project2ProjectTimeOut`**

  Timeout in secondi per la risoluzione di riferimenti da progetto a progetto.

- **`-Recursive`**

  *(4.0 +)* Ripristina tutti i progetti di riferimento per i progetti UWP e .NET Core. Non si applica ai progetti che usano `packages.config` .

- **`-RequireConsent`**

  Verifica che il ripristino dei pacchetti sia abilitato prima di scaricare e installare i pacchetti. Per informazioni dettagliate, vedere [ripristino di pacchetti](../../consume-packages/package-restore.md).

- **`-SolutionDirectory`**

  Specifica la cartella della soluzione. Non valido durante il ripristino dei pacchetti per una soluzione. Obbligatorio quando si esegue il ripristino con un `packages.config` file a meno che non `PackagesDirectory` `OutputDirectory` venga usato o.

- **`-Source`**

  Specifica l'elenco di origini di pacchetti (come URL) da usare per il ripristino. Se omesso, il comando usa le origini fornite nei file di configurazione, vedere [configurazione del comportamento di NuGet](../../consume-packages/configuring-nuget-behavior.md). Utilizzare un punto e virgola per separare le voci dell'elenco.

- **`-UseLockFile`**

  Consente la generazione e l'utilizzo del file di blocco del progetto con il ripristino.

- **`-Verbosity [normal|quiet|detailed]`**

  Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="remarks"></a>Osservazioni

Il comando RESTORE esegue i passaggi seguenti:

1. Determinare la modalità operativa del comando Restore.

   | tipo di file projectPath | Comportamento |
   | --- | --- |
   | Soluzione (cartella) | NuGet Cerca un `.sln` file e lo usa se è stato trovato; in caso contrario, restituisce un errore. `(SolutionDir)\.nuget` viene utilizzato come cartella iniziale. |
   | File `.sln` | Ripristinare i pacchetti identificati dalla soluzione; Restituisce un errore se `-SolutionDirectory` viene utilizzato. `$(SolutionDir)\.nuget` viene utilizzato come cartella iniziale. |
   | `packages.config` o file di progetto | Ripristinare i pacchetti elencati nel file, risolvendo e installando le dipendenze. |
   | Altro tipo di file | Si presuppone che il file sia un `.sln` file come sopra; se non è una soluzione, NuGet restituisce un errore. |
   | (projectPath non specificato) | <ul><li>NuGet Cerca i file della soluzione nella cartella corrente. Se viene trovato un singolo file, viene usato per ripristinare i pacchetti; Se vengono rilevate più soluzioni, NuGet restituisce un errore.</li><li>Se non sono presenti file di soluzione, NuGet Cerca un oggetto `packages.config` e lo usa per ripristinare i pacchetti.</li><li>Se non viene trovata alcuna soluzione o `packages.config` file, NuGet restituisce un errore.</ul> |

2. Determinare la cartella dei pacchetti usando l'ordine di priorità seguente (NuGet restituisce un errore se nessuna di queste cartelle viene trovata):

    - Cartella specificata con `-PackagesDirectory` .
    - Il `repositoryPath` valore in `Nuget.Config`
    - Cartella specificata con `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Quando si ripristinano i pacchetti per una soluzione, NuGet esegue le operazioni seguenti:
    - Carica il file di soluzione.
    - Ripristina i pacchetti a livello di soluzione elencati nella `$(SolutionDir)\.nuget\packages.config` `packages` cartella.
    - Ripristinare i pacchetti elencati nella `$(ProjectDir)\packages.config` `packages` cartella. Per ogni pacchetto specificato, ripristinare il pacchetto in parallelo, a meno che non `-DisableParallelProcessing` sia specificato.

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
