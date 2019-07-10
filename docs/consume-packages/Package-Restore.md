---
title: Ripristino dei pacchetti NuGet
description: Panoramica della modalità di ripristino dei pacchetti NuGet da cui dipende un progetto, inclusa la procedura per disabilitare il ripristino e vincolare le versioni.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 3b64c035886818496339fe1bdd8f9abce060278a
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467802"
---
# <a name="package-restore"></a>Ripristino di pacchetti

Per ottenere un ambiente di sviluppo più ordinato e ridurre le dimensioni dei repository, l'opzione **Ripristino pacchetto** di NuGet installa tutte le dipendenze di un progetto elencate nel file di progetto o in `packages.config`. I comandi `dotnet build` e `dotnet run` di .NET Core 2.0 + eseguono un ripristino automatico dei pacchetti. Visual Studio può ripristinare i pacchetti automaticamente durante la compilazione di un progetto. È possibile ripristinare i pacchetti in qualsiasi momento usando Visual Studio, `nuget restore`, `dotnet restore`e xbuild in Mono.

Con l'opzione Ripristino pacchetto si garantisce che tutte le dipendenze di un progetto siano disponibili senza che sia necessario archiviare i pacchetti nel controllo del codice sorgente. Vedere [Pacchetti e controllo del codice sorgente](../consume-packages/packages-and-source-control.md) per configurare il repository del controllo del codice sorgente per escludere i file binari dei pacchetti. 

## <a name="package-restore-overview"></a>Panoramica del ripristino dei pacchetti

L'opzione Ripristino pacchetto installa prima di tutto le dipendenze dirette di un progetto in base alle esigenze, quindi installa eventuali dipendenze di tali pacchetti in tutto il grafico dipendenze.

Se un pacchetto non è già installato, NuGet tenta prima di tutto di recuperarlo dalla [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). Se il pacchetto non è presente nella cache, NuGet tenta di scaricarlo da tutte le origini abilitate nell'elenco in **Strumenti** > **Opzioni** > **Gestione pacchetti NuGet** > **Origine pacchetti** in Visual Studio. Durante il ripristino NuGet ignora l'ordine delle origini dei pacchetti e usa il pacchetto da una delle origini che per prima risponde alle richieste. Per altre informazioni sul comportamento di NuGet, vedere [Configurazioni comuni di NuGet](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet non indica un errore di ripristino di un pacchetto fino a quando non sono state controllate tutte le origini. In quel momento, NuGet segnala un errore solo per l'ultima origine nell'elenco. Questo tipo di errore implica che il pacchetto non era presente in *alcuna* delle origini, anche se gli errori non vengono visualizzati singolarmente per ogni origine.

È possibile attivare l'opzione Ripristino pacchetto in uno dei modi seguenti:

- **Interfaccia della riga di comando di dotnet**: usare il comando [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) per ripristinare i pacchetti elencati nel file di progetto con [PackageReference](../consume-packages/package-references-in-project-files.md). Con .NET Core 2.0 e versioni successive il ripristino viene eseguito automaticamente con i comandi `dotnet build` e `dotnet run`.  

- **Gestione pacchetti**: In Visual Studio in Windows il ripristino dei pacchetti viene eseguito automaticamente quando si crea un progetto da un modello o si compila un progetto. Tale comportamento è soggetto alle opzioni impostate in [Abilitare e disabilitare il ripristino dei pacchetti](#enable-and-disable-package-restore). In NuGet 4.0 + il ripristino avviene automaticamente anche quando vengono apportate modifiche a un progetto basato su .NET Core SDK.

    Per eseguire il ripristino dei pacchetti manualmente, fare clic con il pulsante destro del mouse in **Esplora soluzioni** e selezionare**Ripristina pacchetti NuGet**. Se uno o più pacchetti singoli non sono ancora installati correttamente, in **Esplora soluzioni** viene visualizzata un'icona di errore. Fare clic con il pulsante destro del mouse e selezionare **Gestisci pacchetti NuGet**. Usare **Gestione pacchetti** per disinstallare e reinstallare i pacchetti interessati. Per altre informazioni, vedere [Reinstallare e aggiornare pacchetti](../consume-packages/reinstalling-and-updating-packages.md)

    Se viene visualizzato l'errore "Questo progetto fa riferimento a uno o più pacchetti NuGet che non sono presenti in questo computer" o "Impossibile ripristinare uno o più pacchetti NuGet perché il consenso non è stato concesso", [abilitare il ripristino automatico](#enable-and-disable-package-restore). Vedere anche [Risoluzione degli errori relativi al ripristino dei pacchetti](Package-restore-troubleshooting.md).

- **Interfaccia della riga di comando di nuget.exe**: usare il comando [nuget restore](../tools/cli-ref-restore.md) per ripristinare i pacchetti elencati nel file di progetto o di soluzione, oppure in `packages.config`. 

- **MSBuild**: usare il comando [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) per ripristinare i pacchetti elencati nel file di progetto con PackageReference. Questo comando è disponibile solo in NuGet 4.x+ e MSBuild 15.1 +, inclusi con Visual Studio 2017 e versioni successive. Sia `nuget restore` che `dotnet restore` usano questo comando per i progetti applicabili.

- **Azure Pipelines**: quando si crea una definizione di compilazione in Azure Pipelines, includere l'attività di [ripristino](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) di NuGet o l'attività di [ripristino](/azure/devops/pipelines/tasks/build/dotnet-core#restore-nuget-packages) di .NET Core nella definizione prima di qualsiasi attività di compilazione. Alcuni modelli di compilazione includono l'attività di ripristino per impostazione predefinita.

- **Azure DevOps Server**: in Azure DevOps Server e TFS 2013 e versioni successive i pacchetti vengono ripristinati automaticamente durante la compilazione, a condizione che si usi un modello di Team Build per TFS 2013 o versioni successive. Per le versioni di TFS precedenti, è possibile includere un passaggio di compilazione per eseguire un'opzione di ripristino dalla riga di comando o eventualmente eseguire la migrazione del modello di compilazione a una versione successiva. Per altre informazioni, vedere [Configurare il ripristino dei pacchetti con Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="enable-and-disable-package-restore"></a>Abilitare e disabilitare il ripristino dei pacchetti

In Visual Studio il ripristino dei pacchetti viene controllato principalmente in **Strumenti** > **Opzioni** > **Gestione pacchetti NuGet**:

![Controllo di Ripristino pacchetto con le opzioni di Gestione pacchetti NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Consenti a NuGet di scaricare i pacchetti mancanti** controlla tutte le forme di ripristino dei pacchetti modificando l'impostazione `packageRestore/enabled` nella [sezione packageRestore](../reference/nuget-config-file.md#packagerestore-section) del file `NuGet.Config`, in `%AppData%\NuGet\` in Windows o in `~/.nuget/NuGet/` in Mac/Linux. Questa impostazione abilita anche il comando **Ripristina pacchetti NuGet** nel menu di scelta rapida della soluzione in Visual Studio.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    
  > [!Note]
  > Per sovrascrivere l'impostazione `packageRestore/enabled` a livello globale, impostare la variabile d'ambiente **EnableNuGetPackageRestore** con valore True o False prima di avviare Visual Studio o una compilazione.

- **Verificare in automatico i pacchetti mancanti durante il build in Visual Studio** controlla il ripristino automatico modificando l'impostazione `packageRestore/automatic` nella [sezione packageRestore](../reference/nuget-config-file.md#packagerestore-section) del file `NuGet.Config`. Quando questa opzione è impostata su True, l'esecuzione di una compilazione da Visual Studio ripristina automaticamente eventuali pacchetti mancanti. Questa impostazione non influisce sulle compilazioni eseguite dalla riga di comando di MSBuild.

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

Per abilitare o disabilitare l'opzione Ripristino pacchetto per tutti gli utenti in un computer, uno sviluppatore o un'azienda può aggiungere le impostazioni di configurazione al file globale `nuget.config`. In Windows il file globale `nuget.config` si trova in `%ProgramData%\NuGet\Config`, a volte in una cartella specifica `\{IDE}\{Version}\{SKU}\` di Visual Studio. In Mac/Linux si trova in `~/.local/share`. I singoli utenti possono quindi abilitare il ripristino in modo selettivo, in base alle esigenze a livello di progetto. Per informazioni dettagliate su come NuGet assegna la priorità a più file di configurazione, vedere [Configurazioni comuni di NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> Se si modificano le impostazioni `packageRestore` direttamente in `nuget.config`, riavviare Visual Studio per visualizzare i valori correnti nella finestra di dialogo **Opzioni**.

## <a name="constrain-package-versions-with-restore"></a>Vincolare le versioni dei pacchetti con il ripristino

Quando NuGet ripristina i pacchetti con un metodo qualsiasi, rispetta i vincoli specificati in `packages.config` o nel file di progetto:

- In `packages.config` è possibile specificare un intervallo di versioni nella proprietà `allowedVersion` della dipendenza. Vedere [Vincolare le versioni di aggiornamento](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) per altre informazioni. Ad esempio:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- In un file di progetto è possibile usare PackageReference per specificare direttamente un intervallo di dipendenza. Ad esempio:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

In tutti i casi, usare la notazione descritta in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md).

## <a name="force-restore-from-package-sources"></a>Forzare il ripristino dalle origini dei pacchetti

Per impostazione predefinita, le operazioni di ripristino di NuGet usano i pacchetti dalle cartelle *global-packages* e *http-cache*, descritte in [Gestire pacchetti globali e cartelle cache](managing-the-global-packages-and-cache-folders.md).

Per evitare di usare la cartella *global-packages*, eseguire una delle operazioni seguenti:

- Cancellare la cartella con `nuget locals global-packages -clear` o `dotnet nuget locals global-packages --clear`.
- Modificare temporaneamente la posizione della cartella *global-packages* prima dell'operazione di ripristino, usando uno dei metodi seguenti:
  - Impostare la variabile di ambiente NUGET_PACKAGES su una cartella diversa.
  - Creare un file `NuGet.Config` che imposta `globalPackagesFolder` (se si usa PackageReference) o `repositoryPath` (se si usa `packages.config`) in una cartella diversa. Per altre informazioni, vedere le [impostazioni di configurazione](../reference/nuget-config-file.md#config-section).
  - Solo MSBuild: specificare una cartella diversa con la proprietà `RestorePackagesPath`.

Per evitare di usare la cache per le origini HTTP, eseguire una delle operazioni seguenti:

- Usare l'opzione `-NoCache` con `nuget restore` o l'opzione `--no-cache` con `dotnet restore`. Queste opzioni non influiscono sulle operazioni di ripristino tramite l'interfaccia utente o la console di Gestione pacchetti di Visual Studio.
- Cancellare la cache con `nuget locals http-cache -clear` o `dotnet nuget locals http-cache --clear`.
- Impostare temporaneamente la variabile di ambiente NUGET_HTTP_CACHE_PATH in una cartella diversa.

## <a name="troubleshooting"></a>Risoluzione dei problemi

Vedere [Risolvere gli errori relativi al ripristino dei pacchetti](package-restore-troubleshooting.md).
