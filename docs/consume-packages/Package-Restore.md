---
title: Ripristino dei pacchetti NuGet
description: Panoramica della modalità di ripristino dei pacchetti NuGet da cui dipende un progetto, inclusa la procedura per disabilitare il ripristino e vincolare le versioni.
author: JonDouglas
ms.author: jodou
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: e5dfd9f8dd0439751ddd3863cad03f3b463e1487
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859239"
---
# <a name="restore-packages-using-package-restore"></a>Ripristinare i pacchetti con Ripristino pacchetto

Per ottenere un ambiente di sviluppo più ordinato e ridurre le dimensioni dei repository, l'opzione **Ripristino pacchetto** di NuGet installa tutte le dipendenze di un progetto elencate nel file di progetto o in `packages.config`. I comandi `dotnet build` e `dotnet run` di .NET Core 2.0 + eseguono un ripristino automatico dei pacchetti. Visual Studio può ripristinare i pacchetti automaticamente durante la compilazione di un progetto. È possibile ripristinare i pacchetti in qualsiasi momento usando Visual Studio, `nuget restore`, `dotnet restore`e xbuild in Mono.

Con l'opzione Ripristino pacchetto si garantisce che tutte le dipendenze di un progetto siano disponibili senza che sia necessario archiviare i pacchetti nel controllo del codice sorgente. Vedere [Pacchetti e controllo del codice sorgente](../consume-packages/packages-and-source-control.md) per configurare il repository del controllo del codice sorgente per escludere i file binari dei pacchetti. 

## <a name="package-restore-overview"></a>Panoramica del ripristino dei pacchetti

L'opzione Ripristino pacchetto installa prima di tutto le dipendenze dirette di un progetto in base alle esigenze, quindi installa eventuali dipendenze di tali pacchetti in tutto il grafico dipendenze.

Se un pacchetto non è già installato, NuGet tenta prima di tutto di recuperarlo dalla [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). Se il pacchetto non è presente nella cache, NuGet tenta di scaricare il pacchetto da tutte le origini abilitate nell'elenco in **strumenti**  >  **Opzioni Opzioni**  >  pacchetti di **Gestione pacchetti NuGet**  >   in Visual Studio. Durante il ripristino NuGet ignora l'ordine delle origini dei pacchetti e usa il pacchetto da una delle origini che per prima risponde alle richieste. Per altre informazioni sul comportamento di NuGet, vedere [Configurazioni comuni di NuGet](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet non indica un errore di ripristino di un pacchetto fino a quando non sono state controllate tutte le origini. In quel momento, NuGet segnala un errore solo per l'ultima origine nell'elenco. Questo tipo di errore implica che il pacchetto non era presente in *alcuna* delle origini, anche se gli errori non vengono visualizzati singolarmente per ogni origine.

## <a name="restore-packages"></a>Ripristinare pacchetti

Ripristino pacchetto tenta di installare tutte le dipendenze del pacchetto nello stato corretto che corrisponde ai riferimenti al pacchetto nel file di progetto (con estensione *csproj*) o nel file *packages.config*. In Visual Studio i riferimenti vengono visualizzati in Esplora soluzioni nel nodo **Dipendenze \ NuGet** o **Riferimenti**.

1. Se i riferimenti al pacchetto nel file di progetto sono corretti, usare lo strumento preferito per ripristinare i pacchetti.

   - [Visual Studio](#restore-using-visual-studio) ([ripristino automatico](#restore-packages-automatically-using-visual-studio) o [ripristino manuale](#restore-packages-manually-using-visual-studio))
   - [Interfaccia della riga di comando di dotnet](#restore-using-the-dotnet-cli)
   - [Interfaccia della riga di comando di nuget.exe](#restore-using-the-nugetexe-cli)
   - [MSBuild](#restore-using-msbuild)
   - [Azure Pipelines](#restore-using-azure-pipelines)
   - [Azure DevOps Server](#restore-using-azure-devops-server)

   Se i riferimenti al pacchetto nel file di progetto (con estensione *csproj*) o nel file *packages.config* non sono corretti (non corrispondono allo stato desiderato dopo il ripristino del pacchetto), è necessario installare o aggiornare i pacchetti.

   Per i progetti che usano PackageReference, dopo un ripristino riuscito il pacchetto dovrebbe essere presente nella cartella *global-packages* e il file `obj/project.assets.json` viene ricreato. Per i progetti che usano `packages.config`, il pacchetto dovrebbe essere visualizzato nella cartella `packages` del progetto. La compilazione del progetto dovrebbe ora avvenire senza problemi. 

2. Dopo l'esecuzione di Ripristino pacchetto, se si verificano ancora pacchetti mancanti o errori correlati al pacchetto (ad esempio, icone di errore in Esplora soluzioni in Visual Studio), potrebbe essere necessario seguire le istruzioni descritte in [Risoluzione degli errori relativi al ripristino dei pacchetti](package-restore-troubleshooting.md) o, in alternativa, [reinstallare e aggiornare i pacchetti](../consume-packages/reinstalling-and-updating-packages.md).

   In Visual Studio la console di gestione pacchetti offre diverse opzioni flessibili per la reinstallazione dei pacchetti. Vedere [Uso di Package-Update](reinstalling-and-updating-packages.md#using-update-package).

## <a name="restore-using-visual-studio"></a>Eseguire il ripristino con Visual Studio

In Visual Studio in Windows, eseguire una delle operazioni seguenti:

- Ripristinare automaticamente i pacchetti, oppure

- Ripristinare manualmente i pacchetti

### <a name="restore-packages-automatically-using-visual-studio"></a>Ripristinare automaticamente i pacchetti con Visual Studio

Il ripristino dei pacchetti viene eseguito automaticamente quando si crea un progetto da un modello o si compila un progetto. Tale comportamento è soggetto alle opzioni impostate in [Abilitare e disabilitare il ripristino dei pacchetti](#enable-and-disable-package-restore-in-visual-studio). In NuGet 4.0 +, il ripristino avviene automaticamente quando si apportano modifiche a un progetto di tipo SDK (in genere un progetto .NET Core o .NET Standard).

1. Abilitare il ripristino automatico dei pacchetti scegliendo **strumenti**  >  **Opzioni**  >  **Gestione pacchetti NuGet**, quindi selezionare **verifica automaticamente i pacchetti mancanti durante la compilazione in Visual Studio** in **ripristino pacchetto**.

   Per i progetti non in stile SDK, è prima di tutto necessario selezionare **Consenti a NuGet di scaricare i pacchetti mancanti** per abilitare l'opzione di ripristino automatico.

1. Compilare il progetto.

   Se uno o più pacchetti singoli non sono ancora installati correttamente, in **Esplora soluzioni** viene visualizzata un'icona di errore. Fare clic con il pulsante destro del mouse e selezionare **Gestisci pacchetti NuGet**. Usare **Gestione pacchetti** per disinstallare e reinstallare i pacchetti interessati. Per altre informazioni, vedere [Reinstallare e aggiornare pacchetti](../consume-packages/reinstalling-and-updating-packages.md)

   Se viene visualizzato l'errore "Questo progetto fa riferimento a uno o più pacchetti NuGet che non sono presenti in questo computer" o "Impossibile ripristinare uno o più pacchetti NuGet perché il consenso non è stato concesso", [abilitare il ripristino automatico](#enable-and-disable-package-restore-in-visual-studio). Per i progetti precedenti, vedere anche [Eseguire la migrazione al ripristino automatico dei pacchetti](#migrate-to-automatic-package-restore-visual-studio). Vedere anche [risoluzione dei problemi relativi al ripristino dei pacchetti](Package-restore-troubleshooting.md).

### <a name="restore-packages-manually-using-visual-studio"></a>Ripristinare i pacchetti manualmente con Visual Studio

1. Abilitare il ripristino del pacchetto scegliendo **strumenti**  >  **Opzioni**  >  **Gestione pacchetti NuGet**. Nelle opzioni di **Ripristino pacchetti** selezionare **Consenti a NuGet di scaricare i pacchetti mancanti**.

1. Fare clic con il pulsante destro del mouse sulla soluzione in **Esplora soluzioni** e scegliere **Ripristina pacchetti NuGet**.

   Se uno o più pacchetti singoli non sono ancora installati correttamente, in **Esplora soluzioni** viene visualizzata un'icona di errore. Fare clic con il pulsante destro del mouse e scegliere **Gestisci pacchetti NuGet**, quindi usare **Gestione pacchetti** per disinstallare e reinstallare i pacchetti interessati. Per altre informazioni, vedere [Reinstallare e aggiornare pacchetti](../consume-packages/reinstalling-and-updating-packages.md)

   Se viene visualizzato l'errore "Questo progetto fa riferimento a uno o più pacchetti NuGet che non sono presenti in questo computer" o "Impossibile ripristinare uno o più pacchetti NuGet perché il consenso non è stato concesso", [abilitare il ripristino automatico](#enable-and-disable-package-restore-in-visual-studio). Per i progetti precedenti, vedere anche [Eseguire la migrazione al ripristino automatico dei pacchetti](#migrate-to-automatic-package-restore-visual-studio). Vedere anche [risoluzione dei problemi relativi al ripristino dei pacchetti](Package-restore-troubleshooting.md).

### <a name="enable-and-disable-package-restore-in-visual-studio"></a>Abilitare e disabilitare il ripristino dei pacchetti in Visual Studio

In Visual Studio è possibile controllare il ripristino dei pacchetti principalmente tramite **strumenti**  >  **Opzioni**  >  **Gestione pacchetti NuGet**:

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

### <a name="choose-default-package-management-format"></a>Scegliere il formato di gestione pacchetti predefinito

![Controllare il formato di gestione pacchetti predefinito anche se le opzioni di gestione pacchetti NuGet](media/Restore-02-PackageFormatOptions.png)

NuGet presenta due formati in cui un progetto può usare i pacchetti: [`PackageReference`](package-references-in-project-files.md) e [`packages.config`](../reference/packages-config.md) . Il formato predefinito può essere selezionato nell'elenco a discesa sotto l'intestazione **Gestione pacchetti** . È disponibile anche un'opzione che indica quando è installato il primo pacchetto in un progetto.

> [!Note]
> Se un progetto non supporta entrambi i formati di gestione dei pacchetti, il formato di gestione dei pacchetti utilizzato sarà quello compatibile con il progetto e pertanto potrebbe non essere il set predefinito nelle opzioni. NuGet, inoltre, non richiede la selezione nella prima installazione del pacchetto, anche se l'opzione è selezionata nella finestra Opzioni.
>
> Se si usa la console di gestione pacchetti per installare il primo pacchetto in un progetto, NuGet non richiede la selezione del formato, anche se l'opzione è selezionata nella finestra Opzioni.

## <a name="restore-using-the-dotnet-cli"></a>Eseguire il ripristino usando l'interfaccia della riga di comando dotnet

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> Per aggiungere un riferimento al pacchetto mancante al file di progetto, usare [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x), che esegue anche il comando `restore`.

## <a name="restore-using-the-nugetexe-cli"></a>Eseguire il ripristino usando l'interfaccia della riga di comando nuget.exe

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> Il `restore` comando non modifica un file di progetto o *packages.config*. Per aggiungere una dipendenza, aggiungere un pacchetto tramite l'interfaccia utente o la console di gestione pacchetti in Visual Studio oppure modificare *packages.config* , quindi eseguire `install` o `restore` .

## <a name="restore-using-msbuild"></a>Eseguire il ripristino con MSBuild

Usare il comando [msbuild-t:Restore](../reference/msbuild-targets.md#restore-target) per ripristinare i pacchetti elencati nel file di progetto (vedere [PackageReference](package-references-in-project-files.md)) e a partire da MSBuild 16.5 +, `packages.config` progetti.

 Questo comando è disponibile solo in NuGet 4.x+ e MSBuild 15.1 +, inclusi con Visual Studio 2017 e versioni successive.
A partire da MSBuild 16.5 +, questo comando può anche ripristinare i `packages.config` progetti basati quando viene eseguito con `-p:RestorePackagesConfig=true` .

1. Aprire un prompt dei comandi per gli sviluppatori digitando **Prompt dei comandi per gli sviluppatori** nella casella **Cerca**.

   In genere, è consigliabile avviare il prompt dei comandi per gli sviluppatori per Visual Studio dal menu **Start**, in modo che venga configurato con tutti i percorsi necessari per MSBuild.

2. Passare alla cartella contenente il file di progetto e digitare il comando seguente.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

3. Digitare il comando seguente per ricompilare il progetto.

   ```cmd
   msbuild
   ```

   Verificare che l'output di MSBuild indichi che la compilazione è stata completata correttamente.
   
> [!Note]
> MSBuild dispone di un' `-restore` opzione che verrà eseguita `Restore` , ricaricare il progetto e quindi compilare. Vedere [ripristino e compilazione con un comando di MSBuild](../reference/msbuild-targets.md#restoring-and-building-with-one-msbuild-command).

```cmd
# Will restore the project, then build, since build is the default target.
msbuild -restore
```

## <a name="restore-using-azure-pipelines"></a>Eseguire il ripristino con Azure Pipelines

quando si crea una definizione di compilazione in Azure Pipelines, includere l'attività di [ripristino](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) di NuGet o l'attività di [ripristino](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) di .NET Core nella definizione prima di qualsiasi attività di compilazione. Alcuni modelli di compilazione includono l'attività di ripristino per impostazione predefinita.

## <a name="restore-using-azure-devops-server"></a>Eseguire il ripristino con Azure DevOps Server

in Azure DevOps Server e TFS 2013 e versioni successive i pacchetti vengono ripristinati automaticamente durante la compilazione, a condizione che si usi un modello di Team Build per TFS 2013 o versioni successive. Per le versioni di TFS precedenti, è possibile includere un passaggio di compilazione per eseguire un'opzione di ripristino dalla riga di comando o eventualmente eseguire la migrazione del modello di compilazione a una versione successiva. Per altre informazioni, vedere [Configurare il ripristino dei pacchetti con Team Foundation Build](../consume-packages/team-foundation-build.md).

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

In tutti i casi, usare la notazione descritta in [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md).

## <a name="force-restore-from-package-sources"></a>Forzare il ripristino dalle origini dei pacchetti

Per impostazione predefinita, le operazioni di ripristino di NuGet usano i pacchetti dalle cartelle *global-packages* e *http-cache*, descritte in [Gestire pacchetti globali e cartelle cache](managing-the-global-packages-and-cache-folders.md).

Per evitare di usare la cartella *global-packages*, eseguire una delle operazioni seguenti:

- Cancellare la cartella con `nuget locals global-packages -clear` o `dotnet nuget locals global-packages --clear`.
- Modificare temporaneamente il percorso della cartella *Global-Packages* prima dell'operazione di ripristino, usando uno dei metodi seguenti:
  - Impostare la variabile di ambiente NUGET_PACKAGES su una cartella diversa.
  - Creare un file `NuGet.Config` che imposta `globalPackagesFolder` (se si usa PackageReference) o `repositoryPath` (se si usa `packages.config`) in una cartella diversa. Per altre informazioni, vedere le [impostazioni di configurazione](../reference/nuget-config-file.md#config-section).
  - Solo MSBuild: specificare una cartella diversa con la `RestorePackagesPath` Proprietà.

Per evitare di usare la cache per le origini HTTP, eseguire una delle operazioni seguenti:

- Usare l'opzione `-NoCache` con `nuget restore` o l'opzione `--no-cache` con `dotnet restore`. Queste opzioni non influiscono sulle operazioni di ripristino tramite l'interfaccia utente o la console di Gestione pacchetti di Visual Studio.
- Cancellare la cache con `nuget locals http-cache -clear` o `dotnet nuget locals http-cache --clear`.
- Impostare temporaneamente la variabile di ambiente NUGET_HTTP_CACHE_PATH in una cartella diversa.

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>Eseguire la migrazione al ripristino dei pacchetti automatico (Visual Studio)

Per NuGet 2.6 e versioni precedenti era precedentemente supportato il ripristino dei pacchetti integrato in MSBuild, ma non è più così. In genere veniva abilitato facendo clic con il pulsante destro del mouse su una soluzione in Visual Studio e scegliendo **Enable NuGet Package Restore** (Abilita il ripristino dei pacchetti NuGet). Se il progetto usa il ripristino dei pacchetti integrato in MSBuild deprecato, eseguire la migrazione al ripristino dei pacchetti automatico.

I progetti che usano MSBuild-Integrated il ripristino dei pacchetti contengono in genere una cartella *. NuGet* con tre file: *NuGet.config*, *nuget.exe* e *NuGet. targets*. La presenza di un file *NuGet. targets* determina se NuGet continuerà a usare l'approccio integrato di MSBuild, in modo che questo file debba essere rimosso durante la migrazione.

Per eseguire la migrazione al ripristino dei pacchetti automatico:

1. Chiudere Visual Studio.
2. Eliminare *.nuget/nuget.exe* e *.nuget/NuGet.targets*.
3. Per ogni file di progetto rimuovere l'elemento `<RestorePackages>` e rimuovere qualsiasi riferimento a *NuGet.targets*.

Per testare il ripristino dei pacchetti automatico:

1. Rimuovere la cartella *packages* dalla soluzione.
2. Aprire la soluzione in Visual Studio e avviare una compilazione.

   Il ripristino dei pacchetti automatico dovrebbe scaricare e installare ogni pacchetto di dipendenze, senza aggiungerli al controllo del codice sorgente.

## <a name="troubleshooting"></a>Risoluzione dei problemi

Vedere [Risolvere gli errori relativi al ripristino dei pacchetti](Package-restore-troubleshooting.md).
