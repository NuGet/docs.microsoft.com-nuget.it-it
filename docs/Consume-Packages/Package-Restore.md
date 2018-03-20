---
title: Ripristino dei pacchetti NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Panoramica della modalità di ripristino dei pacchetti NuGet da cui dipende un progetto, inclusa la procedura per disabilitare il ripristino e vincolare le versioni."
keywords: Ripristino di pacchetti NuGet, installazione di pacchetti NuGet, installazione pacchetto, ripristinare pacchetti, versioni con dipendenze, disabilitazione del ripristino automatico, vincolo delle versioni dei pacchetti
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 761ef86a70e0a681449dc9fe86d6a52ac2b19bb1
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/15/2018
---
# <a name="package-restore"></a>Ripristino di pacchetti

Per ottenere un ambiente di sviluppo ordinato e ridurre le dimensioni dei repository, l'opzione **Ripristino pacchetto** NuGet installa tutti i pacchetti a cui fa riferimento un progetto prima di compilarlo. Questa funzionalità &mdash;disponibile in Visual Studio, .NET Core 2.0+ e xbuild su Mono&mdash; garantisce che tutte le dipendenze siano disponibili in un progetto senza la necessità di archiviare tali pacchetti in un sistema di controllo del codice sorgente. Vedere [Pacchetti e controllo del codice sorgente](../consume-packages/packages-and-source-control.md) per informazioni su come configurare il repository per escludere i file binari dei pacchetti. È anche possibile ripristinare manualmente i pacchetti in qualsiasi momento.

Per ulteriori dettagli sul ripristino dei pacchetti nei server di compilazione, vedere [Package restore with TFBuild](../consume-packages/team-foundation-build.md) (Ripristino di pacchetti con TFBuild).

## <a name="package-restore-overview"></a>Panoramica del ripristino dei pacchetti

Con il ripristino dei pacchetti vengono prima di tutto installate le dipendenze dirette di un progetto in base alle esigenze, quindi vengono installate le eventuali dipendenze dei pacchetti per tutto il grafico dipendenze.

Se un pacchetto non è già installato, NuGet tenta innanzitutto di recuperarlo dalla [cache](../consume-packages/managing-the-nuget-cache.md). Se il pacchetto non è presente nella cache, NuGet tenta di scaricare il pacchetto (e memorizzarlo nella cache) da tutte le origini abilitate (vedere [Configurazione del comportamento di NuGet](Configuring-NuGet-Behavior.md)). Le origini vengono visualizzate anche nell'elenco **Strumenti > Opzioni > Gestione pacchetti NuGet > Origini pacchetti** in Visual Studio). NuGet ignora l'ordine delle origini dei pacchetti e usa il pacchetto da qualsiasi origine risponde per prima alle richieste.

> [!Note]
> NuGet non indica un errore di ripristino di un pacchetto fino a quando non sono state controllate tutte le origini. In quel momento, NuGet segnala l'errore solo per l'ultima origine nell'elenco. Questo tipo di errore implica che il pacchetto non era presente in *alcuna* delle origini, anche se gli errori non vengono visualizzati singolarmente per ognuna di tali origini.

Il ripristino del pacchetto viene attivato nei modi seguenti:

- **Interfaccia della riga di comando dotnet**: usare il comando [nuget restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), che consente di ripristinare i pacchetti elencati nel file di progetto (vedere [PackageReference](../consume-packages/package-references-in-project-files.md)). Con .NET Core 2.0 e versioni successive, il ripristino viene eseguito automaticamente con `dotnet build` e `dotnet run`.

- **Interfaccia utente di Gestione pacchetti (Visual Studio in Windows)**: i pacchetti vengono ripristinati automaticamente quando si crea un progetto da un modello e quando si compila un progetto (in base all'opzione descritta in [Abilitazione e disabilitazione del ripristino dei pacchetti](#enabling-and-disabling-package-restore)). In NuGet 4.0 +, il ripristino avviene automaticamente anche quando vengono apportate modifiche a un progetto basato su .NET Core SDK.

    Per eseguire il ripristino manualmente, fare clic con il pulsante destro del mouse sulla soluzione in Esplora soluzioni e scegliere **Ripristina pacchetti NuGet**. Se uno o più pacchetti singoli non vengono ancora installati correttamente (Esplora soluzioni mostra un'icona di errore), usare l'interfaccia utente di Gestione pacchetti per disinstallare e reinstallare i pacchetti interessati. Vedere [Reinstallazione e aggiornamento di pacchetti](../consume-packages/reinstalling-and-updating-packages.md)

    Se viene visualizzato l'errore "Questo progetto fa riferimento a uno o più pacchetti NuGet che non sono presenti in questo computer" o "Impossibile ripristinare uno o più pacchetti NuGet perché il consenso non è stato concesso", attivare il ripristino automatico seguendo le istruzioni in [Abilitazione e disabilitazione del ripristino dei pacchetti](#enabling-and-disabling-package-restore).

- **Interfaccia della riga di comando di NuGet**: usare il comando [nuget restore](../tools/cli-ref-restore.md), che consente di ripristinare i pacchetti elencati nel file di progetto (vedere [PackageReference](../consume-packages/package-references-in-project-files.md)) o in un file [packages.config](../reference/packages-config.md). È anche possibile specificare un file di soluzione.

- **MSBuild**: usare il comando [msbuild /t:restore](../reference/msbuild-targets.md#restore-target), che consente di ripristinare i pacchetti elencati nel file di progetto (vedere [PackageReference](../consume-packages/package-references-in-project-files.md)). Disponibile solo in NuGet 4.x+ e MSBuild 15.1 +, inclusi con Visual Studio 2017. Sia `nuget restore` che `dotnet restore` usano questo comando per i progetti applicabili.

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
    <br/>
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

In alcuni casi, uno sviluppatore o una società potrebbe avere l'esigenza di abilitare o disabilitare il ripristino dei pacchetti per tutti gli utenti in un computer. Questa operazione viene eseguita aggiungendo le stesse impostazioni sopra indicate al file di configurazione NuGet globale disponibile in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`. I singoli utenti possono quindi abilitare il ripristino in modo selettivo, in base alle esigenze a livello di progetto. Vedere [Configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) per informazioni dettagliate esatte su come NuGet assegna la priorità a più file di configurazione.

## <a name="constraining-package-versions-with-restore"></a>Vincolo delle versioni dei pacchetti con il ripristino

Durante il ripristino di pacchetti con qualsiasi metodo, NuGet rispetta gli eventuali vincoli specificati in `packages.config` o nel file di progetto:

- `packages.config`: specificare un intervallo di versioni nella proprietà `allowedVersion` della dipendenza. Vedere [Reinstallazione e aggiornamento di pacchetti](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Ad esempio:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- PackageReference: specificare un intervallo di versioni direttamente con il numero di versione della dipendenza. Ad esempio:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

In tutti i casi, usare la notazione descritta in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md).

## <a name="troubleshooting"></a>Risoluzione dei problemi

Vedere [Risoluzione degli errori relativi al ripristino dei pacchetti](package-restore-troubleshooting.md).