---
title: Come gestire le cartelle dei pacchetti globale, della cache e temporanea in NuGet
description: Come gestire la cartella di installazione dei pacchetti globale, la cartella della cache dei pacchetti e la cartella temporanea esistenti in un computer, usate durante l'installazione, il ripristino e l'aggiornamento dei pacchetti.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e2672aa0bf57242526364639f0df74f9d1adb934
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428968"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Gestione delle cartelle dei pacchetti globale, della cache e temporanea

Quando si installa, aggiorna o ripristina un pacchetto, NuGet gestisce i pacchetti e le informazioni sui pacchetti in varie cartelle all'esterno della struttura del progetto:

| Nome | Descrizione e posizione (per utente)|
| --- | --- |
| global&#8209;packages | La cartella *global-packages* è la posizione in cui NuGet installa i pacchetti scaricati. Ogni pacchetto viene espanso completamente in una sottocartella corrispondente all'identificatore del pacchetto e al numero di versione. I progetti che usano il formato [PackageReference](package-references-in-project-files.md) usano sempre i pacchetti direttamente da questa cartella. Quando si usa il file [packages.config](../reference/packages-config.md), i pacchetti vengono installati nella cartella *global-packages* e quindi copiati nella cartella `packages` del progetto.<br/><ul><li>Windows: `%userprofile%\.nuget\packages`</li><li>Mac/Linux: `~/.nuget/packages`</li><li>Eseguire l'override usando la variabile di ambiente NUGET_PACKAGES, le [impostazioni di configurazione](../reference/nuget-config-file.md#config-section) `globalPackagesFolder` o `repositoryPath` (quando si usano PackageReference e `packages.config`rispettivamente) o la proprietà `RestorePackagesPath` MSBuild (solo MSBuild). La variabile di ambiente ha la precedenza rispetto all'impostazione di configurazione.</li></ul> |
| http&#8209;cache | Gestione pacchetti di Visual Studio (NuGet 3.x+) e lo strumento `dotnet` archiviano copie dei pacchetti scaricati nella cache (salvati come file `.dat`), organizzati in sottocartelle per ogni origine di pacchetti. I pacchetti non vengono espansi e la cache ha una scadenza di 30 minuti.<br/><ul><li>Windows: `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/v3-cache`</li><li>Eseguire l'override usando la variabile di ambiente NUGET_HTTP_CACHE_PATH.</li></ul> |
| temp | Cartella in cui NuGet archivia i file temporanei durante le varie operazioni.<br/><li>Windows: `%temp%\NuGetScratch`</li><li>Mac/Linux: `/tmp/NuGetScratch`</li></ul> |
| plugins-cache **4.8+** | Cartella in cui NuGet archivia i risultati dalla richiesta di attestazioni delle operazioni.<br/><ul><li>Windows: `%localappdata%\NuGet\plugins-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/plugins-cache`</li><li>Eseguire l'override usando la variabile di ambiente NUGET_PLUGINS_CACHE_PATH.</li></ul> |

> [!Note]
> NuGet 3.5 e versioni precedenti usano la cartella *packages-cache* invece di *http-cache*, che si trova in `%localappdata%\NuGet\Cache`.

Tramite le cartelle della cache e *global-packages*, NuGet evita in genere il download di pacchetti già esistenti nel computer, con conseguente miglioramento delle prestazioni di installazione, aggiornamento e ripristino. Quando si usa PackageReference, la cartella *global-packages* consente anche di evitare di mantenere i pacchetti scaricati all'interno delle cartelle di progetto, da cui potrebbero essere inavvertitamente aggiunti al controllo del codice sorgente, nonché di ridurre l'impatto complessivo di NuGet sullo spazio di archiviazione del computer.

Quando viene richiesto di recuperare un pacchetto, NuGet controlla prima di tutto nella cartella *global-packages*. Se nella cartella non è disponibile la versione esatta del pacchetto, NuGet controlla tutte le origini di pacchetti non HTTP. Se il pacchetto non viene trovato, NuGet cerca il pacchetto nella cartella *http-cache* a meno che non si specifichi `--no-cache` con i comandi `dotnet.exe` o `-NoCache` con i comandi `nuget.exe`. Se il pacchetto non è presente nella cache o la cache non viene usata, NuGet recupera il pacchetto tramite HTTP.

Per altre informazioni, vedere [Cosa accade quando viene installato un pacchetto](../concepts/package-installation-process.md).

## <a name="viewing-folder-locations"></a>Visualizzazione delle posizioni delle cartelle

È possibile visualizzare le posizioni con il [comando nuget locals](../reference/cli-reference/cli-ref-locals.md):

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

Output tipico (Windows; "user1" è il nome utente corrente):

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

(la cartella `package-cache` viene usata in NuGet 2.x e visualizzata con NuGet 3.5 e versioni precedenti.)

È anche possibile visualizzare le posizioni delle cartelle con il [comando dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals):

```dotnetcli
dotnet nuget locals all --list
```

Output tipico (Mac/Linux; "user1" è il nome utente corrente):

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

Per visualizzare la posizione di una singola cartella, usare `http-cache`, `global-packages`, `temp` o `plugins-cache` invece di `all`.

## <a name="clearing-local-folders"></a>Cancellazione delle cartelle locali

Se si verificano problemi di installazione dei pacchetti o si vuole essere certi di eseguire l'installazione dei pacchetti da una raccolta remota, usare l'opzione `locals --clear` (dotnet.exe) o `locals -clear` (nuget.exe), specificando la cartella da cancellare oppure `all` per cancellare tutte le cartelle:

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

Gli eventuali pacchetti usati dai progetti aperti in Visual Studio non vengono cancellati dalla cartella *global-packages*.

A partire da Visual Studio 2017, usare il comando di menu **Strumenti > Gestione pacchetti NuGet > Impostazioni di Gestione pacchetti**, quindi selezionare **Cancella tutte le cache NuGet**. La gestione delle cache non è attualmente disponibile tramite la console di Gestione pacchetti. In Visual Studio 2015 usare invece i comandi dell'interfaccia della riga di comando.

![Comando NuGet per la cancellazione delle cache](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Risoluzione dei problemi

Durante l'uso di `nuget locals` o `dotnet nuget locals` possono verificarsi gli errori seguenti:

- *Errore: Impossibile accedere al file <package> perché utilizzato da un altro processo* o *La cancellazione delle risorse locali non è riuscita. Non è possibile eliminare uno o più file*

    Uno o più file nella cartella sono in uso da un altro processo. Ad esempio, è aperto un progetto di Visual Studio che fa riferimento ai pacchetti nella cartella *global-packages*. Chiudere i processi e riprovare.

- *Errore: Accesso al percorso <path> negato* o *La directory non è vuota*

    Non si è autorizzati a eliminare i file nella cache. Modificare le autorizzazioni della cartella, se possibile, e riprovare. In caso contrario, contattare l'amministratore di sistema.

- *Errore: il percorso specificato, il nome file o entrambi sono troppo lunghi. Il nome completo del file deve essere inferiore a 260 caratteri e il nome della directory deve essere composto da meno di 248 caratteri.*

    Abbreviare i nomi delle cartelle e riprovare.
