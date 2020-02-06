---
title: Comando di installazione CLI NuGet
description: Riferimento per il comando di installazione di NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6c49b2406462eae6ce45c65dfd8b3a9eb1077e73
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036942"
---
# <a name="install-command-nuget-cli"></a>Comando install (interfaccia della riga di comando di NuGet)

**Si applica a:** utilizzo pacchetti &bullet; **versioni supportate:** tutti

Consente di scaricare e installare un pacchetto in un progetto, per impostazione predefinita la cartella corrente, utilizzando le origini di pacchetti specificate.

> [!Tip]
> Per scaricare un pacchetto direttamente al di fuori del contesto di un progetto, visitare la pagina del pacchetto in [NuGet.org](https://www.nuget.org) e selezionare il collegamento per il **download** .

Se non viene specificata alcuna origine, vengono usati quelli elencati nel file di configurazione globale, `%appdata%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux). Per ulteriori informazioni, vedere [configurazioni NuGet comuni](../../consume-packages/configuring-nuget-behavior.md) .

Se non vengono specificati pacchetti specifici, `install` installa tutti i pacchetti elencati nel file di `packages.config` del progetto, rendendoli simili a [`restore`](cli-ref-restore.md).

Il comando `install` non modifica un file di progetto o `packages.config`; in questo modo, è simile a `restore` in quanto aggiunge solo pacchetti al disco, ma non modifica le dipendenze di un progetto.

Per aggiungere una dipendenza, aggiungere un pacchetto tramite l'interfaccia utente o la console di gestione pacchetti in Visual Studio oppure modificare `packages.config`, quindi eseguire `install` o `restore`.

## <a name="usage"></a>Utilizzo

```cli
nuget install <packageID | configFilePath> [options]
```

dove `<packageID>` denomina il pacchetto da installare (usando la versione più recente) o `<configFilePath>` identifica il file di `packages.config` che elenca i pacchetti da installare. È possibile indicare una versione specifica con l'opzione `-Version`.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | File di configurazione NuGet da applicare. Se non specificato, viene usato `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| DependencyVersion | *(4.4 +)* Versione dei pacchetti di dipendenze da usare. i possibili tipi sono i seguenti:<br/><ul><li>*Minimo* (impostazione predefinita): versione più bassa</li><li>*HighestPatch*: versione con la patch principale più bassa, minore minore, più alta</li><li>*HighestMinor*: versione con la patch principale più bassa, minore più elevata</li><li>*Massimo*: la versione più recente</li><li>*Ignora*: non verrà usato alcun pacchetto di dipendenza</li></ul> |
| DisableParallelProcessing | Disabilita l'installazione di più pacchetti in parallelo. |
| ExcludeVersion | Installa il pacchetto in una cartella denominata solo con il nome del pacchetto e non con il numero di versione. |
| FallbackSource | *(3.2 +)* Elenco di origini di pacchetti da usare come fallback nel caso in cui il pacchetto non venga trovato nell'origine primaria o predefinita. |
| ForceEnglishOutput | *(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| Framework | *(4.4 +)* Framework di destinazione usato per la selezione delle dipendenze. Se non è specificato, il valore predefinito è' any '. |
| ? | Visualizza le informazioni della Guida per il comando. |
| NoCache | Impedisce a NuGet di usare pacchetti memorizzati nella cache. Vedere [gestione dei pacchetti globali e delle cartelle della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Evita la richiesta di input o conferme dell'utente. |
| OutputDirectory | Specifica la cartella in cui sono installati i pacchetti. Se non viene specificata alcuna cartella, viene utilizzata la cartella corrente. |
| PackageSaveMode | Specifica i tipi di file da salvare dopo l'installazione del pacchetto: uno dei `nuspec`, `nupkg`o `nuspec;nupkg`. |
| PreRelease | Consente l'installazione dei pacchetti di versioni non definitive. Questo flag non è obbligatorio quando si ripristinano i pacchetti con `packages.config`. |
| RequireConsent | Verifica che il ripristino dei pacchetti sia abilitato prima di scaricare e installare i pacchetti. Per informazioni dettagliate, vedere [ripristino di pacchetti](../../consume-packages/package-restore.md). |
| SolutionDirectory | Specifica la cartella radice della soluzione per cui ripristinare i pacchetti. |
| Origine | Specifica l'elenco di origini di pacchetti (come URL) da usare. Se omesso, il comando usa le origini fornite nei file di configurazione, vedere [configurazioni comuni di NuGet](../../consume-packages/configuring-nuget-behavior.md). |
| Livello di dettaglio | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |
| Versione | Specifica la versione del pacchetto da installare. |

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
