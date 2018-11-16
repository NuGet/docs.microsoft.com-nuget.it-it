---
title: Ripristino dei pacchetti NuGet
description: Panoramica della modalità di ripristino dei pacchetti NuGet da cui dipende un progetto, inclusa la procedura per disabilitare il ripristino e vincolare le versioni.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: da69181aebe3bebcea6acd6e15fde6b77dd33452
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580298"
---
# <a name="package-restore"></a>Ripristino di pacchetti

Per ottenere un ambiente di sviluppo ordinato e ridurre le dimensioni dei repository, l'opzione **Ripristino pacchetto** NuGet installa tutte le dipendenze di un progetto elencate nel file di progetto o in `packages.config`. Visual Studio consente di ripristinare automaticamente i pacchetti al momento della compilazione di un progetto. Anche i comandi `dotnet build` e `dotnet run` (.NET Core 2.0+) eseguono un ripristino automatico. È anche possibile ripristinare i pacchetti in qualsiasi momento tramite Visual Studio, `nuget restore`, `dotnet restore` e xbuild su Mono.

Il ripristino dei pacchetti garantisce che tutte le dipendenze di un progetto siano disponibili senza archiviare tali pacchetti nel controllo del codice sorgente. Vedere [Pacchetti e controllo del codice sorgente](../consume-packages/packages-and-source-control.md) per informazioni su come configurare il repository per escludere i file binari dei pacchetti.

## <a name="package-restore-overview"></a>Panoramica del ripristino dei pacchetti

Con il ripristino dei pacchetti vengono prima di tutto installate le dipendenze dirette di un progetto in base alle esigenze, quindi vengono installate le eventuali dipendenze dei pacchetti per tutto il grafico dipendenze.

Se un pacchetto non è già installato, NuGet tenta innanzitutto di recuperarlo dalla [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). Se il pacchetto non è presente nella cache, NuGet tenta di scaricare il pacchetto da tutte le origini abilitate (vedere [Configurazione del comportamento di NuGet](Configuring-NuGet-Behavior.md)). Le origini vengono visualizzate anche nell'elenco **Strumenti > Opzioni > Gestione pacchetti NuGet > Origini pacchetti** in Visual Studio. Durante il ripristino NuGet ignora l'ordine delle origini dei pacchetti e usa il pacchetto da qualsiasi origine risponde per prima alle richieste.

> [!Note]
> NuGet non indica un errore di ripristino di un pacchetto fino a quando non sono state controllate tutte le origini. In quel momento, NuGet segnala un errore solo per l'ultima origine nell'elenco. Questo tipo di errore implica che il pacchetto non era presente in *alcuna* delle origini, anche se gli errori non vengono visualizzati singolarmente per ognuna di tali origini.

Il ripristino del pacchetto viene attivato nei modi seguenti:

- **Interfaccia della riga di comando dotnet**: usare il comando [nuget restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), che consente di ripristinare i pacchetti elencati nel file di progetto (vedere [PackageReference](../consume-packages/package-references-in-project-files.md)). Con .NET Core 2.0 e versioni successive, il ripristino viene eseguito automaticamente con `dotnet build` e `dotnet run`.

- **Interfaccia utente di Gestione pacchetti (Visual Studio in Windows)**: i pacchetti vengono ripristinati automaticamente quando si crea un progetto da un modello e quando si compila un progetto (in base all'opzione descritta in [Abilitazione e disabilitazione del ripristino dei pacchetti](#enabling-and-disabling-package-restore)). In NuGet 4.0 +, il ripristino avviene automaticamente anche quando vengono apportate modifiche a un progetto basato su .NET Core SDK.

    Per eseguire il ripristino manualmente, fare clic con il pulsante destro del mouse sulla soluzione in Esplora soluzioni e scegliere **Ripristina pacchetti NuGet**. Se uno o più pacchetti singoli non vengono ancora installati correttamente (Esplora soluzioni mostra un'icona di errore), usare l'interfaccia utente di Gestione pacchetti per disinstallare e reinstallare i pacchetti interessati. Vedere [Reinstallazione e aggiornamento di pacchetti](../consume-packages/reinstalling-and-updating-packages.md)

    Se viene visualizzato l'errore "Questo progetto fa riferimento a uno o più pacchetti NuGet che non sono presenti in questo computer" o "Impossibile ripristinare uno o più pacchetti NuGet perché il consenso non è stato concesso", attivare il ripristino automatico seguendo le istruzioni in [Abilitazione e disabilitazione del ripristino dei pacchetti](#enabling-and-disabling-package-restore). Vedere anche [Risoluzione degli errori relativi al ripristino dei pacchetti](Package-restore-troubleshooting.md).

- **Interfaccia della riga di comando NuGet**: usare il comando [nuget restore](../tools/cli-ref-restore.md), che consente di ripristinare i pacchetti elencati nel file di progetto o in `packages.config`. È anche possibile specificare un file di soluzione.

- **MSBuild**: usare il comando [msbuild /t:restore](../reference/msbuild-targets.md#restore-target), che consente di ripristinare i pacchetti elencati nel file di progetto (solo PackageReference). Disponibile solo in NuGet 4.x+ e MSBuild 15.1 +, inclusi con Visual Studio 2017. Sia `nuget restore` che `dotnet restore` usano questo comando per i progetti applicabili.

- **Visual Studio Team Services**: quando si crea una definizione di compilazione in Team Services, includere l'attività di [ripristino NuGet](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) o di [ripristino .NET Core](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) nella definizione prima di qualsiasi attività di compilazione. Questa attività è inclusa per impostazione predefinita in vari modelli di compilazione.

- **Team Foundation Server**: con TFS 2013 e versioni successive, i pacchetti vengono ripristinati automaticamente durante la compilazione, a condizione di usare un modello di Team Build per TFS 2013 o versioni successive. Per una versione precedente di TFS, è possibile includere un passaggio di compilazione per richiamare una delle opzioni di ripristino da riga di comando descritte in precedenza. Facoltativamente, è possibile eseguire la migrazione del modello di compilazione a TFS 2013. Per altre informazioni, vedere [Procedura dettagliata per il ripristino dei pacchetti con Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="enabling-and-disabling-package-restore"></a>Abilitazione e disabilitazione del ripristino dei pacchetti

Il ripristino dei pacchetti viene abilitato principalmente tramite **Strumenti > Opzioni > Gestione pacchetti NuGet** in Visual Studio:

![Controllo dei comportamenti di ripristino dei pacchetti tramite le opzioni di Gestione pacchetti NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Consenti a NuGet di scaricare i pacchetti mancanti**: controlla tutte le forme di ripristino dei pacchetti modificando l'impostazione `packageRestore/enabled` nel file `NuGet.Config` come illustrato di seguito (`%AppData%\NuGet\NuGet.Config` in Windows, `~/.nuget/NuGet/NuGet.Config` in Mac/Linux). In Visual Studio, questa impostazione consente il funzionamento del comando **Ripristina pacchetti NuGet** nel menu di scelta rapida della soluzione.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```

> [!Note]
>  L'impostazione `packageRestore/enabled` può essere sovrascritta a livello globale impostando una variabile d'ambiente denominata **EnableNuGetPackageRestore** con valore TRUE o FALSE prima di avviare Visual Studio o una compilazione.

- **Verificare in automatico i pacchetti mancanti durante il build in Visual Studio**: controlla il ripristino automatico modificando l'impostazione `packageRestore/automatic` nel file `NuGet.Config` come illustrato di seguito (`%AppData%\NuGet\NuGet.Config` in Windows, `~/.nuget/NuGet/NuGet.Config` in Mac/Linux). Quando questa opzione è impostata, l'esecuzione di una compilazione da Visual Studio ripristina automaticamente gli eventuali pacchetti mancanti. Questa opzione non ha effetti sulle compilazioni eseguite dalla riga di comando tramite MSBuild.

    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

Per riferimento, vedere il [file di configurazione di NuGet - sezione packageRestore](../reference/nuget-config-file.md#packagerestore-section).

In alcuni casi, uno sviluppatore o una società potrebbe avere l'esigenza di abilitare o disabilitare il ripristino dei pacchetti per tutti gli utenti in un computer. A tale scopo, aggiungere le stesse impostazioni di cui sopra al file di configurazione NuGet globale che si trova in `%ProgramData%\NuGet\Config` (Windows, potenzialmente in una cartella `\{IDE}\{Version}\{SKU}\` specifica per Visual Studio) o in `~/.local/share` (Mac/Linux). I singoli utenti possono quindi abilitare il ripristino in modo selettivo, in base alle esigenze a livello di progetto. Vedere [Configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) per informazioni dettagliate esatte su come NuGet assegna la priorità a più file di configurazione.

> [!Important]
> Se si modificano le impostazioni `packageRestore` direttamente in `nuget.config`, riavviare Visual Studio per visualizzare i valori correnti nella finestra di dialogo Opzioni.

## <a name="constraining-package-versions-with-restore"></a>Vincolo delle versioni dei pacchetti con il ripristino

Durante il ripristino di pacchetti con qualsiasi metodo, NuGet rispetta gli eventuali vincoli specificati in `packages.config` o nel file di progetto:

- `packages.config`: specificare un intervallo di versioni nella proprietà `allowedVersion` della dipendenza. Vedere [Reinstallazione e aggiornamento di pacchetti](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Ad esempio:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- File di progetto (PackageReference): specificare un intervallo di versioni direttamente con il numero di versione della dipendenza. Ad esempio:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

In tutti i casi, usare la notazione descritta in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md).

## <a name="forcing-restore-from-package-sources"></a>Forzare il ripristino dalle origini dei pacchetti

Per impostazione predefinita, le operazioni di ripristino NuGet usano i pacchetti dalle cartelle *global-packages* e *http-cache*, descritte in [Gestione delle cartelle dei pacchetti globali e della cache](managing-the-global-packages-and-cache-folders.md).

Per evitare di usare la cartella *global-packages*, eseguire una delle operazioni seguenti:

- Cancellare la cartella con `nuget locals global-packages -clear` o `dotnet nuget locals global-packages --clear`
- Modificare temporaneamente la posizione della cartella *global-packages* prima dell'operazione di ripristino usando uno dei metodi seguenti:
  - Impostare la variabile di ambiente NUGET_PACKAGES su una cartella diversa.
  - Creare un file `NuGet.Config` che imposta `globalPackagesFolder` (se si usa PackageReference) o `repositoryPath` (se si usa `packages.config`) su una cartella diversa. Vedere le [impostazioni di configurazione](../reference/nuget-config-file.md#config-section).
  - Solo MSBuild: specificare un'altra cartella con la proprietà `RestorePackagesPath`.

Per evitare di usare la cache per le origini HTTP, eseguire una delle operazioni seguenti:

- Usare l'opzione `-NoCache` con `nuget restore` o l'opzione `--no-cache` con `dotnet restore`. Queste opzioni non influiscono sulle operazioni di ripristino tramite l'interfaccia utente o la console di Gestione pacchetti di Visual Studio.
- Cancellare la cache con `nuget locals http-cache -clear` o `dotnet nuget locals http-cache --clear`.
- Impostare temporaneamente la variabile di ambiente NUGET_HTTP_CACHE_PATH su una cartella diversa.

## <a name="troubleshooting"></a>Risoluzione dei problemi

Vedere [Risoluzione degli errori relativi al ripristino dei pacchetti](package-restore-troubleshooting.md).
