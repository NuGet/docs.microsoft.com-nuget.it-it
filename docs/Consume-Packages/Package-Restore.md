---
title: Ripristino dei pacchetti NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Descrizione della modalità di ripristino dei pacchetti NuGet da cui dipende un progetto, inclusa la procedura per disabilitare il ripristino e vincolare le versioni."
keywords: Ripristino di pacchetti NuGet, installazione di pacchetti NuGet, installazione pacchetto, ripristinare pacchetti, versioni con dipendenze, disabilitazione del ripristino automatico, vincolo delle versioni dei pacchetti
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4e819a2bb34bbe70f0f11d5adeed82b976a8cb65
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="package-restore"></a>Ripristino di pacchetti

Per ottenere un ambiente di sviluppo ordinato e ridurre le dimensioni dei repository, l'opzione **Ripristino pacchetto** NuGet installa tutti i pacchetti a cui fa riferimento un progetto prima di compilarlo. Questa funzionalità ampiamente usata garantisce che tutte le dipendenze siano disponibili in un progetto senza la necessità di archiviare tali pacchetti in un sistema di controllo del codice sorgente. Vedere [Pacchetti e controllo del codice sorgente](../consume-packages/packages-and-source-control.md) per informazioni su come configurare il repository per escludere i file binari dei pacchetti.

In questo argomento
- [Guida rapida al ripristino dei pacchetti](#quick-guide-to-package-restore)
- [Panoramica del ripristino dei pacchetti](#package-restore-overview)
- [Abilitazione e disabilitazione del ripristino dei pacchetti](#enabling-and-disabling-package-restore)
- [Vincolo delle versioni dei pacchetti con il ripristino](#constraining-package-versions-with-restore)
- [Ripristino dalla riga di comando](#command-line-restore), per tutte le versioni di NuGet
- [Ripristino automatico in Visual Studio](#automatic-restore-in-visual-studio), per NuGet 2.7 e versioni successive.
- [Ripristino integrato con MSBuild in Visual Studio](#msbuild-integrated-restore), per NuGet 2.6 e versioni precedenti.
- [Ripristino dei pacchetti con Team Foundation Build](#package-restore-with-team-foundation-build)

Il comportamento di ripristino varia in base alla versione. Per controllare la versione di NuGet, è sufficiente eseguire `nuget.exe` dalla riga di comando e guardare la prima riga dell'output.

Per ulteriori dettagli sul ripristino dei pacchetti nei server di compilazione, vedere [Package restore with TFBuild](../consume-packages/team-foundation-build.md) (Ripristino di pacchetti con TFBuild).

> [!Note]
> I progetti configurati per il ripristino dei pacchetti funzionano anche con xbuild su Mono.

## <a name="quick-guide-to-package-restore"></a>Guida rapida al ripristino dei pacchetti

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> Se viene visualizzato l'errore "Questo progetto fa riferimento a uno o più pacchetti NuGet che non sono presenti in questo computer" o "Impossibile ripristinare uno o più pacchetti NuGet perché il consenso non è stato concesso", attivare il ripristino automatico seguendo le istruzioni in [Abilitazione e disabilitazione del ripristino dei pacchetti](#enabling-and-disabling-package-restore).

## <a name="package-restore-overview"></a>Panoramica del ripristino dei pacchetti

In primo luogo, i riferimenti ai pacchetti vengono gestiti in uno dei seguenti formati di gestione dei pacchetti, in base al tipo di progetto e alla versione di NuGet. Si noti che NuGet 4 e MSBuild 15.1 vengono installati con Visual Studio 2017.

| Metodo | Versione di NuGet | Descrizione | 
| --- | --- | --- |
| `packages.config` | 2.x+ | Elenca il set completo di dipendenze. I pacchetti aggiunti a `packages.config` devono essere aggiunti anche al file di progetto e anche le destinazioni e le proprietà devono essere aggiunte al file di progetto. Questo è il metodo di base per tutte le versioni di NuGet, ma con prestazioni inferiori rispetto alle altre opzioni. (Vedere lo [schema di packages.config](../schema/packages-config.md).) | 
| `project.json` | 3.x+ | Usato solo per impostazione predefinita con progetti UWP, ma i progetti possono essere convertiti da `packages.config`. `project.json` elenca solo le dipendenze di livello superiore. I riferimenti, le destinazioni e le proprietà vengono aggiunti dinamicamente al progetto durante la compilazione, con prestazioni di conseguenza migliori rispetto a `packages.config`. (Vedere lo [schema di project.json](../schema/project-json.md).)|
| PackageReference | 4.x+ | Elenca le dipendenze direttamente nel file di progetto nel nodo `<PackageReference>`, insieme a `<Reference>` e `<ProjectReference>`. Funzionamento analogo a `project.json`. Vedere [Riferimenti ai pacchetti nei file di progetto](../Consume-Packages/Package-References-in-Project-Files.md). |

In secondo luogo, si avvia un ripristino usando l'elenco di riferimenti in svariati modi:

Dalla riga di comando o dalla [console di Gestione pacchetti](../tools/Package-Manager-Console.md):

| Comando | Scenari possibili |
| --- | --- | 
| `nuget restore` | Tutte le versioni di NuGet e tutti i tipi di riferimento. Vedere [Ripristino dalla riga di comando](#command-line-restore) di seguito. | 
| `dotnet restore` | Come `nuget restore` per i progetti .NET Core. Vedere [dotnet restore](/dotnet/articles/core/tools/dotnet-restore). |
| `msbuild /t:restore` | Nuget 4.x+ e MSBuild 15.1+ con [riferimenti ai pacchetti solo nei file di progetto](../Consume-Packages/Package-References-in-Project-Files.md). Sia `nuget restore` che `dotnet restore` usano questo comando per i progetti applicabili. Vedere [Pack e restore di NuGet come destinazioni MSBuild - Destinazione di restore](../schema/msbuild-targets.md#restore-target).|

Anche Visual Studio stesso ripristina i pacchetti in momenti diversi:

| Tipo | Quando viene eseguito il ripristino |
| --- | --- |
| Ripristino di modello | Durante la creazione di un nuovo progetto, dato che alcuni modelli dipendono da pacchetti esterni. |
| Ripristino in fase di compilazione | Come primo passaggio di una compilazione. |
| Ripristino di soluzione | Quando l'utente fa clic con il pulsante destro del mouse su una soluzione e sceglie **Ripristina pacchetti NuGet**. |
| Ripristino in seguito a modifiche del progetto | *(Solo NuGet 4.x)*  Quando si usa un progetto basato su .NET Core SDK, incluso quando cambia lo stato del progetto. |

## <a name="enabling-and-disabling-package-restore"></a>Abilitazione e disabilitazione del ripristino dei pacchetti

Il ripristino dei pacchetti viene abilitato principalmente tramite **Strumenti > Opzioni > Gestione pacchetti NuGet** in Visual Studio:

![Controllo dei comportamenti di ripristino dei pacchetti tramite le opzioni di Gestione pacchetti NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Consenti a NuGet di scaricare i pacchetti mancanti**: controlla tutte le forme di ripristino dei pacchetti modificando l'impostazione `packageRestore/enabled` nel file `%AppData%\NuGet\NuGet.Config` come illustrato di seguito.

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
    

- **Verificare in automatico i pacchetti mancanti durante il build in Visual Studio**: controlla il ripristino automatico per NuGet 2.7 e versioni successive modificando l'impostazione `packageRestore/automatic` nel file `%AppData%\NuGet\NuGet.Config` come illustrato di seguito.
            
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

Per riferimento, vedere il [file di configurazione di NuGet - sezione packageRestore](../Schema/nuget-config-file.md#packagerestore-section).

In alcuni casi, uno sviluppatore o una società potrebbe avere l'esigenza di abilitare o disabilitare il ripristino dei pacchetti in un computer per impostazione predefinita per tutti gli utenti. Questa operazione può essere eseguita aggiungendo le stesse impostazioni sopra indicate al file di configurazione NuGet globale disponibile in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`. I singoli utenti possono quindi abilitare il ripristino in modo selettivo, in base alle esigenze a livello di progetto. Vedere [Configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) per informazioni dettagliate esatte su come NuGet assegna la priorità a più file di configurazione.

## <a name="constraining-package-versions-with-restore"></a>Vincolo delle versioni dei pacchetti con il ripristino

Quando NuGet ripristina pacchetti con qualsiasi metodo, rispetta i vincoli specificati in `packages.config`, `project.json` o nel file di progetto:

- `packages.config`: specificare un intervallo di versioni nella proprietà `allowedVersion` della dipendenza. Vedere [Reinstallazione e aggiornamento di pacchetti](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Ad esempio:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- `project.json`: specificare un intervallo di versioni direttamente con il numero di versione della dipendenza. Ad esempio:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- Riferimenti ai pacchetti nei file di progetto: specificare un intervallo di versioni direttamente con il numero di versione della dipendenza. Ad esempio:
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

In tutti i casi, usare la notazione descritta in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md).

## <a name="command-line-restore"></a>Ripristino dalla riga di comando

Per NuGet 2.7 e versioni successive, usare il comando [Restore](../tools/cli-ref-restore.md) per ripristinare tutti i pacchetti in una soluzione, indipendentemente dal fatto che usi `packages.config`, `project.json` o riferimenti ai pacchetti nei file di progetto. Per una determinata cartella di progetto, ad esempio `c:\proj\app`, ognuna delle varianti comuni di seguito consente di ripristinare i pacchetti:

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

Per NuGet 4.0+ e MSBuild 15.1+ è anche possibile usare `MSBuild /t:restore`, come descritto in [Pack e restore di NuGet come destinazioni MSBuild](../schema/msbuild-targets.md).

## <a name="build-time-restore-in-visual-studio"></a>Ripristino in fase di compilazione in Visual Studio

Visual Studio consente di ripristinare automaticamente i pacchetti mancanti per impostazione predefinita all'inizio di una compilazione. Questo comportamento può essere modificato deselezionando **Strumenti > Opzioni > Gestione pacchetti NuGet > Generale > Verificare in automatico i pacchetti mancanti durante il build in Visual Studio**.

Quando è abilitato, il ripristino automatico funziona nel modo seguente:

1. All'avvio di una compilazione, Visual Studio indica a NuGet di ripristinare i pacchetti.
1. NuGet cerca in modo ricorsivo tutti i file `packages.config` nella soluzione, cerca `project.json` oppure cerca nel file di progetto.
1. Per ogni pacchetto elencato nei file di riferimento, NuGet controlla se esiste già nella soluzione (a cartella `packages`, `project.lock.json` o `project.assets.json` a seconda che il progetto usi `packages.config`, `project.json` o riferimenti ai pacchetti nei file di progetto).
1. Se il pacchetto non viene trovato, NuGet tenta prima di tutto di recuperare il pacchetto dalla cache (vedere [Gestione delle cache NuGet](../consume-packages/managing-the-nuget-cache.md). Se il pacchetto non è presente nella cache, NuGet tenta di scaricare il pacchetto dalle origini abilitate elencate in **Strumenti > Opzioni > Gestione pacchetti NuGet > Origini pacchetti**, nell'ordine di visualizzazione delle origini. In questo caso, NuGet non indica un errore per la ricerca del pacchetto fino al completamento del controllo in tutte le origini, quindi segnala l'errore solo per l'ultima origine nell'elenco. Implicitamente, questo tipo di errore significa anche che il pacchetto non era presente in alcuna delle origini, anche se gli errori non vengono visualizzati singolarmente per tali origini.
1. Se il download ha esito positivo, NuGet memorizza il pacchetto nella cache e lo installa nella soluzione (ancora una volta, nella cartella `packages`, in `project.lock.json` o in `project.assets.json`). In caso contrario NuGet segnala un errore e anche la compilazione non riesce.

Durante questo processo viene visualizzata una finestra di dialogo di stato con l'opzione per annullare il ripristino del pacchetto.

## <a name="package-restore-with-team-foundation-build"></a>Ripristino dei pacchetti con Team Foundation Build

La funzionalità di ripristino dei pacchetti viene comunemente usata durante la compilazione di progetti nei server di compilazione, come con Team Foundation Server (TFS) e Visual Studio Team Services, nonché altri sistemi di compilazione non trattati in questo articolo.

### <a name="visual-studio-team-services"></a>Visual Studio Team Services

Quando si crea una definizione di compilazione in Team Services, includere semplicemente l'attività di ripristino dei pacchetti NuGet nella definizione prima di qualsiasi attività di compilazione. Questa attività è inclusa per impostazione predefinita in vari modelli di compilazione.

![Attività di ripristino dei pacchetti NuGet in una definizione di compilazione di Visual Studio Team Services](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a>Team Foundation Server

Con TFS 2013 e versioni successive, i pacchetti vengono ripristinati automaticamente per impostazione predefinita durante la compilazione, a condizione di usare un modello di Team Build per Team Foundation Server 2013 o versioni successive.

Se si usa una versione precedente dei modelli di compilazione, ad esempio in un progetto di cui è stata eseguita la migrazione da versioni precedenti di TFS, sarà necessario eseguire la migrazione anche di questi modelli di compilazione a TFS 2013. Questo significa essenzialmente ricreare le parti personalizzate dei modelli di compilazione usando il modello appropriato per il controllo del codice sorgente (controllo della versione di Team Foundation o Git).

Per una versione precedente di TFS, è sufficiente includere un passaggio di compilazione per richiamare il comando di [ripristino della riga di comando](#command-line-restore), come descritto in precedenza.

Per altri dettagli, vedere [Procedura dettagliata per il ripristino dei pacchetti con Team Foundation Build](../consume-packages/team-foundation-build.md).    
