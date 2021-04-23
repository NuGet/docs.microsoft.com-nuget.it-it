---
title: Configurazioni comuni di NuGet
description: I file NuGet.Config controllano il comportamento di NuGet sia a livello globale che di progetto e vengono modificati con il comando nuget config.
author: JonDouglas
ms.author: jodou
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 18e3af7145495b5753b5900915ffb4b07942b856
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901473"
---
# <a name="common-nuget-configurations"></a>Configurazioni comuni di NuGet

Il comportamento di NuGet si basa sulle impostazioni accumulate in uno o più file `NuGet.Config` (XML) che possono esistere a livello di progetto, di utente e di computer. Un file `NuGetDefaults.Config` globale configura anche in particolare le origini dei pacchetti. Le impostazioni si applicano a tutti i comandi eseguiti nell'interfaccia della riga di comando, nella console di Gestione pacchetti e nell'interfaccia utente di Gestione pacchetti.

## <a name="config-file-locations-and-uses"></a>Percorsi e usi dei file di configurazione

| Ambito | `NuGet.Config` percorso del file | Descrizione |
| --- | --- | --- |
| Soluzione | Cartella corrente (ovvero la cartella della soluzione) o qualsiasi cartella fino alla radice dell'unità.| Nella cartella di una soluzione le impostazioni si applicano a tutti i progetti presenti nelle sottocartelle. Si noti che se un file di configurazione viene inserito in una cartella di progetto, non ha alcun effetto su tale progetto. |
| Utente | **Windows:**`%appdata%\NuGet\NuGet.Config`<br/>**Mac/Linux:** `~/.config/NuGet/NuGet.Config` o `~/.nuget/NuGet/NuGet.Config` (varia in base alla distribuzione del sistema operativo) <br/>Altre config sono supportate in tutte le piattaforme. Queste impostazioni di configurazione non possono essere modificate dagli strumenti. </br> **Windows:**`%appdata%\NuGet\config\*.Config` <br/>**Mac/Linux:** `~/.config/NuGet/config/*.config` O `~/.nuget/config/*.config` | Le impostazioni si applicano a tutte le operazioni, ma ne viene eseguito l'override dalle impostazioni a livello di progetto. |
| Computer | **Windows:**`%ProgramFiles(x86)%\NuGet\Config`<br/>**Mac/Linux:** `$XDG_DATA_HOME` . Se `$XDG_DATA_HOME` è null o vuoto, verrà usato `~/.local/share` o `/usr/local/share` (a seconda della distribuzione del sistema operativo)  | Le impostazioni si applicano a tutte le operazioni sul computer, ma ne viene eseguito l'override dalle impostazioni a livello di utente o di progetto. |

Note per versioni precedenti di NuGet:
- NuGet 3.3 e versioni precedenti usavano una cartella `.nuget` per le impostazioni a livello di soluzione. Questa cartella non viene usata in NuGet 3.4+.
- Per NuGet da 2.6 a 3.x, il file di configurazione a livello di computer in Windows si trova in , dove può essere , è la versione Visual Studio, ad esempio , e `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]\NuGet.Config` `{IDE}` è , o `VisualStudio` `{Version}` `14.0` `{SKU}` `Community` `Pro` `Enterprise` . Per eseguire la migrazione delle impostazioni a NuGet 4.0+, è sufficiente copiare il file di configurazione in `%ProgramFiles(x86)%\NuGet\Config` . In Linux, questo percorso precedente era `/etc/opt` , e in Mac, `/Library/Application Support` .

## <a name="changing-config-settings"></a>Modifica delle impostazioni di configurazione

Un file `NuGet.Config` è un semplice file di testo XML contenente coppie chiave/valore, come illustrato nell'argomento [Impostazioni di configurazione NuGet](../reference/nuget-config-file.md).

Le impostazioni vengono gestite usando il [comando config](../reference/cli-reference/cli-ref-config.md) dell'interfaccia della riga di comando di NuGet:
- Per impostazione predefinita, le modifiche vengono apportate al file di configurazione a livello di utente.
- Per modificare le impostazioni in un file diverso, usare l'opzione `-configFile`. In questo caso i file possono usare qualsiasi nome.
- Per le chiavi la distinzione tra maiuscole e minuscole si applica sempre.
- L'elevazione è necessaria per modificare le impostazioni nel file delle impostazioni a livello di computer.

> [!Warning]
> Anche se è possibile modificare il file in qualsiasi editor di testo, NuGet (versioni 3.4.3 e successive) ignora senza avvisare l'intero file di configurazione se contiene XML non valido (tag non corrispondenti, virgolette non valide e così via). Per questo motivo è preferibile gestire le impostazioni usando `nuget config`.

### <a name="setting-a-value"></a>Impostazione di un valore

Windows:

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

Mac/Linux:

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> In NuGet 3.4 e versioni successive è possibile usare le variabili di ambiente in qualsiasi valore, come in `repositoryPath=%PACKAGEHOME%` (Windows) e `repositoryPath=$PACKAGEHOME` (Mac/Linux).

### <a name="removing-a-value"></a>Rimozione di un valore

Per rimuovere un valore, specificare una chiave con un valore vuoto.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Creazione di un nuovo file di configurazione

Copiare il modello seguente nel nuovo file e quindi usare `nuget config -configFile <filename>` per impostare i valori:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Come vengono applicate le impostazioni

Più file `NuGet.Config` consentono di archiviare le impostazioni in posizioni diverse in modo che vengano applicate a un progetto, a un gruppo di progetti o a tutti i progetti. Queste impostazioni si applicano complessivamente a qualsiasi operazione NuGet richiamata dalla riga di comando o da Visual Studio. Hanno la precedenza le impostazioni che si trovano "più vicino" a un progetto o alla cartella corrente.

In particolare, NuGet carica le impostazioni dai diversi file di configurazione nell'ordine seguente:

1. Il [ `NuGetDefaults.Config` file](#nuget-defaults-file), che contiene le impostazioni correlate solo alle origini del pacchetto.
1. Il file a livello di computer.
1. Il file a livello di utente.
1. Il file specificato con `-configFile`.
1. File trovati in ogni cartella nel percorso dalla radice dell'unità alla cartella corrente (dove viene richiamato o la cartella contenente il `nuget.exe` Visual Studio progetto). Ad esempio, se un comando viene richiamato in , NuGet cerca e carica i file `c:\A\B\C` di configurazione in , quindi , e infine `c:\` `c:\A` `c:\A\B` `c:\A\B\C` .

Quando NuGet trova le impostazioni in questi file, le applica come segue:

1. Per gli elementi singoli, NuGet sostituisce i valori trovati in precedenza per la stessa chiave. Questo significa che le impostazioni "più vicine" alla cartella o al progetto corrente eseguono l'override delle altre trovate in precedenza. L'impostazione `defaultPushSource` in `NuGetDefaults.Config`, ad esempio, viene sostituita se esiste in un altro file di configurazione.
1. Per gli elementi delle raccolte (ad esempio, `<packageSources>`), NuGet combina i valori di tutti i file di configurazione in una singola raccolta.
1. Quando `<clear />` è presente per un determinato nodo, NuGet ignora i valori di configurazione definiti in precedenza per tale nodo.

### <a name="settings-walkthrough"></a>Procedura dettagliata per le impostazioni

Si supponga di avere la struttura di cartelle seguente in due unità separate:

```
disk_drive_1
    User
disk_drive_2
    Project1
        Source
    Project2
        Source
    tmp
```

Si hanno poi quattro file `NuGet.Config` nelle posizioni seguenti con il contenuto indicato. Il file a livello di computer non è incluso in questo esempio, ma il comportamento sarà simile a quello del file a livello di utente.

File A. File a livello di utente, (`%appdata%\NuGet\NuGet.Config` in Windows, `~/.config/NuGet/NuGet.Config` in Mac/Linux):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

File B. `disk_drive_2/NuGet.Config` :

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="disk_drive_2/tmp" />
    </config>
    <packageRestore>
        <add key="enabled" value="True" />
    </packageRestore>
</configuration>
```

File C. `disk_drive_2/Project1/NuGet.Config` :

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="External/Packages" />
        <add key="defaultPushSource" value="https://MyPrivateRepo/ES/api/v2/package" />
    </config>
    <packageSources>
        <clear /> <!-- ensure only the sources defined below are used -->
        <add key="MyPrivateRepo - ES" value="https://MyPrivateRepo/ES/nuget" />
    </packageSources>
</configuration>
```

File D. `disk_drive_2/Project2/NuGet.Config` :

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

NuGet quindi carica e applica le impostazioni come segue, a seconda della posizione da dove viene eseguita la chiamata:

- **Richiamato `disk_drive_1/users` da**: viene usato solo il repository predefinito elencato nel file di configurazione a livello di utente (A), perché è l'unico file trovato in `disk_drive_1` .

- **Richiamato da `disk_drive_2/` o `disk_drive_/tmp`**: il file a livello di utente (A) viene caricato per primo, quindi NuGet passa alla radice di e trova il file `disk_drive_2` (B). NuGet cerca anche un file di configurazione in `/tmp` ma non ne trova uno. Di conseguenza, viene usato il repository predefinito in , il ripristino dei pacchetti è abilitato `nuget.org` e i pacchetti vengono espansi in `disk_drive_2/tmp` .

- **Richiamato da `disk_drive_2/Project1` o `disk_drive_2/Project1/Source`**: il file a livello di utente (A) viene caricato per primo, quindi NuGet carica il file (B) dalla radice di , seguito dal file `disk_drive_2` (C). Le impostazioni in (C) sostituiscono quelle in (B) e (A), quindi la posizione in cui vengono installati i `repositoryPath` pacchetti è invece di `disk_drive_2/Project1/External/Packages` `disk_drive_2/tmp` . Inoltre, poiché (C) cancella `<packageSources>`, nuget.org non è più disponibile come origine e rimane solo `https://MyPrivateRepo/ES/nuget`.

- **Richiamato da `disk_drive_2/Project2` o `disk_drive_2/Project2/Source`**: il file a livello di utente (A) viene caricato per primo seguito da file (B) e file (D). Poiché `packageSources` non viene cancellato, sia `nuget.org` che `https://MyPrivateRepo/DQ/nuget` sono disponibili come origini. I pacchetti vengono espansi in `disk_drive_2/tmp` come specificato in (B).

## <a name="additional-user-wide-configuration"></a>Configurazione aggiuntiva a livello di utente

A partire dalla versione 5.7, NuGet ha aggiunto il supporto per altri file di configurazione a livello di utente. In questo modo i fornitori di terze parti possono aggiungere altri file di configurazione utente senza elevazione dei privilegi.
Questi file di configurazione si trovano nella cartella di configurazione standard a livello di utente all'interno di una `config` sottocartella.
Verranno considerati tutti i `.config` file `.Config` che terminano con o .
Questi file non possono essere modificati dagli strumenti standard.

| Piattaforma del sistema operativo  | Configurazioni aggiuntive |
| --- | --- |
| Windows      | `%appdata%\NuGet\config\*.Config` |
| Mac/Linux    | `~/.config/NuGet/config/*.config` o `~/.nuget/config/*.config` |

## <a name="nuget-defaults-file"></a>File delle impostazioni predefinite di NuGet

Lo scopo del file `NuGetDefaults.Config` è quello di specificare le origini da cui i pacchetti vengono installati e aggiornati e di controllare la destinazione predefinita per la pubblicazione dei pacchetti con `nuget push`. Poiché gli amministratori possono distribuire facilmente file `NuGetDefaults.Config` coerenti agli sviluppatori e ai computer di compilazione (ad esempio usando Criteri di gruppo), possono assicurarsi che tutti nell'organizzazione usino le origini dei pacchetti corrette invece di nuget.org.

> [!Important]
> Il file `NuGetDefaults.Config` non causa mai la rimozione di un pacchetto dalla configurazione NuGet di uno sviluppatore. Se dunque lo sviluppatore ha già usato NuGet e quindi l'origine del pacchetto nuget.org è già registrata, non verrà rimossa dopo la creazione di un file `NuGetDefaults.Config`.
>
> Inoltre, né né altri meccanismi in NuGet possono impedire `NuGetDefaults.Config` l'accesso alle origini dei pacchetti come nuget.org. Se un'organizzazione vuole bloccare tale accesso, deve usare altri mezzi, ad esempio i firewall.

### <a name="nugetdefaultsconfig-location"></a>`NuGetDefaults.Config` Posizione

La tabella seguente descrive la posizione di archiviazione prevista per il file `NuGetDefaults.Config`, a seconda del sistema operativo di destinazione:

| Piattaforma del sistema operativo  | `NuGetDefaults.Config` Percorso |
| --- | --- |
| Windows      | **Visual Studio 2017 o NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 e versioni precedenti o NuGet 3.x e versioni precedenti:** `%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME` (in genere `~/.local/share` o `/usr/local/share`, a seconda della distribuzione del sistema operativo)|

### <a name="nugetdefaultsconfig-settings"></a>Impostazioni di NuGetDefaults.Config

- `packageSources`: questa raccolta ha lo stesso significato di `packageSources` nei normali file di configurazione e specifica le origini predefinite. NuGet usa le origini in ordine durante l'installazione o l'aggiornamento di pacchetti nei progetti usando il formato di gestione `packages.config`. Per i progetti che usano il formato PackageReference, NuGet usa prima di tutto le origini locali, quindi le origini in condivisioni di rete, poi le origini HTTP, indipendentemente dall'ordine nei file di configurazione. NuGet Ignora sempre l'ordine delle origini con le operazioni di ripristino.

- `disabledPackageSources`: questa raccolta ha anche lo stesso significato dei file, in cui ogni origine interessata è elencata in base al nome e un valore che indica se `NuGet.Config` `true` / `false` è disabilitata. In questo modo il nome e l'URL dell'origine possono rimanere in `packageSources` senza che debba essere attivata per impostazione predefinita. I singoli sviluppatori possono quindi ri abilitare l'origine impostando il valore dell'origine su in altri file senza dover trovare nuovamente `false` `NuGet.Config` l'URL corretto. Questo è utile anche per fornire agli sviluppatori un elenco completo di URL delle origini interne per un'organizzazione, abilitando al contempo solo l'origine di un singolo team per impostazione predefinita.

- `defaultPushSource`: specifica la destinazione predefinita per le `nuget push` operazioni , eseguendo l'override del valore predefinito predefinito di `nuget.org` . Gli amministratori possono distribuire questa impostazione per evitare la pubblicazione accidentale di pacchetti interni al pubblico, in quanto gli sviluppatori devono usare in modo specifico `nuget.org` `nuget push -Source` per pubblicare in `nuget.org` .

### <a name="example-nugetdefaultsconfig-and-application"></a>Applicazione e NuGetDefaults.Config di esempio

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!-- defaultPushSource key works like the 'defaultPushSource' key of NuGet.Config files. -->
    <!-- This can be used by administrators to prevent accidental publishing of packages to nuget.org. -->
    <config>
        <add key="defaultPushSource" value="https://contoso.com/packages/" />
    </config>

    <!-- Default Package Sources; works like the 'packageSources' section of NuGet.Config files. -->
    <!-- This collection cannot be deleted or modified but can be disabled/enabled by users. -->
    <packageSources>
        <add key="Contoso Package Source" value="https://contoso.com/packages/" />
        <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
    </packageSources>

    <!-- Default Package Sources that are disabled by default. -->
    <!-- Works like the 'disabledPackageSources' section of NuGet.Config files. -->
    <!-- Sources cannot be modified or deleted either but can be enabled/disabled by users. -->
    <disabledPackageSources>
        <add key="nuget.org" value="true" />
    </disabledPackageSources>
</configuration>
```
