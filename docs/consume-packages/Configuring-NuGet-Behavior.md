---
title: Configurazione del comportamento di NuGet
description: I file NuGet.Config controllano il comportamento di NuGet sia a livello globale che di progetto e vengono modificati con il comando nuget config.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: c23b464ca39fd8d872f21846a7d6d34edf9dce93
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/11/2018
ms.locfileid: "34817743"
---
# <a name="configuring-nuget-behavior"></a>Configurazione del comportamento di NuGet

Il comportamento di NuGet si basa sulle impostazioni accumulate in uno o più file `NuGet.Config` (XML) che possono esistere a livello di progetto, di utente e di computer. Un file `NuGetDefaults.Config` globale configura anche in particolare le origini dei pacchetti. Le impostazioni si applicano a tutti i comandi eseguiti nell'interfaccia della riga di comando, nella console di Gestione pacchetti e nell'interfaccia utente di Gestione pacchetti.

## <a name="config-file-locations-and-uses"></a>Percorsi e usi dei file di configurazione

| Ambito | Percorso del file NuGet.Config | Descrizione |
| --- | --- | --- |
| Progetto | Cartella corrente (ovvero la cartella di progetto) o qualsiasi cartella fino alla radice dell'unità| In una cartella di progetto le impostazioni si applicano solo a tale progetto. Nelle cartelle padre contenenti più sottocartelle di progetto, le impostazioni si applicano a tutti i progetti in tali sottocartelle. |
| Utente | Windows: `%appdata%\NuGet\NuGet.Config`<br/>Mac/Linux: `~/.config/NuGet/NuGet.Config` o `~/.nuget/NuGet/NuGet.Config` (a seconda della distribuzione del sistema operativo) | Le impostazioni si applicano a tutte le operazioni, ma ne viene eseguito l'override dalle impostazioni a livello di progetto. |
| Computer | Windows: `%ProgramFiles(x86)%\NuGet\Config`<br/>Mac/Linux: `$XDG_DATA_HOME`. Se `$XDG_DATA_HOME` è null o vuoto, verrà usato `~/.local/share` o `/usr/local/share` (a seconda della distribuzione del sistema operativo)  | Le impostazioni si applicano a tutte le operazioni sul computer, ma ne viene eseguito l'override dalle impostazioni a livello di utente o di progetto. |

Note per versioni precedenti di NuGet:
- NuGet 3.3 e versioni precedenti usavano una cartella `.nuget` per le impostazioni a livello di soluzione. Questo file non viene usato in NuGet 3.4+.
- Per NuGet da 2.6 a 3.x, il file di configurazione a livello di computer in Windows si trovava in %ProgramData%\NuGet\Config[\\{IDE}[\\{Versione}[\\{SKU}]]]\NuGet.Config, dove *{IDE}* può essere *VisualStudio*, *{Versione}* era la versione di Visual Studio, ad esempio *14.0*, e *{SKU}* è *Community*, *Pro* o *Enterprise*. Per eseguire la migrazione delle impostazioni a NuGet 4.0+, è sufficiente copiare il file di configurazione in %Programmi(x86)%\NuGet\Config. In Linux questo percorso precedente era /etc/opt e in Mac /Library/Application Support.

## <a name="changing-config-settings"></a>Modifica delle impostazioni di configurazione

Un file `NuGet.Config` è un semplice file di testo XML contenente coppie chiave/valore, come illustrato nell'argomento [Impostazioni di configurazione NuGet](../reference/nuget-config-file.md).

Le impostazioni vengono gestite usando il [comando config](../tools/cli-ref-config.md) dell'interfaccia della riga di comando di NuGet:
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

1. Il [file NuGetDefaults.Config](#nuget-defaults-file), che contiene le impostazioni relative solo alle origini dei pacchetti.
1. Il file a livello di computer.
1. Il file a livello di utente.
1. Il file specificato con `-configFile`.
1. File presenti in ogni cartella del percorso dalla radice dell'unità alla cartella corrente (dove viene richiamato nuget.exe o la cartella contenente il progetto di Visual Studio). Se ad esempio un comando viene richiamato in c:\A\B\C, NuGet cerca e carica i file di configurazione in c:\, quindi in c:\A, poi in c:\A\B e infine in c:\A\B\C.

Quando NuGet trova le impostazioni in questi file, le applica come segue:

1. Per gli elementi singoli, NuGet sostituisce i valori trovati in precedenza per la stessa chiave. Questo significa che le impostazioni "più vicine" alla cartella o al progetto corrente eseguono l'override delle altre trovate in precedenza. L'impostazione `defaultPushSource` in `NuGetDefaults.Config`, ad esempio, viene sostituita se esiste in un altro file di configurazione.

1. Per gli elementi delle raccolte (ad esempio, `<packageSources>`), NuGet combina i valori di tutti i file di configurazione in una singola raccolta.

1. Quando `<clear />` è presente per un determinato nodo, NuGet ignora i valori di configurazione definiti in precedenza per tale nodo.

### <a name="settings-walkthrough"></a>Procedura dettagliata per le impostazioni

Si supponga di avere la struttura di cartelle seguente in due unità separate:

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

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

File B. disk_drive_2/NuGet.Config:

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

File C. disk_drive_2/Project1/NuGet.Config:

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

File D. disk_drive_2/Project2/NuGet.Config:

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

- **Chiamata da disk_drive_1/users**: viene usato solo il repository predefinito elencato nel file di configurazione a livello di utente (A), perché è il solo file presente in disk_drive_1.

- **Chiamata da disk_drive_2/ o disk_drive_/tmp**: prima viene caricato il file a livello di utente (A), quindi NuGet passa alla radice di disk_drive_2 e trova il file (B). NuGet cerca anche un file di configurazione in /tmp, ma non lo trova. Viene quindi usato il repository predefinito in nuget.org, viene abilitato il ripristino dei pacchetti e i pacchetti vengono espansi in disk_drive_2/tmp.

- **Chiamata da disk_drive_2/Project1 o disk_drive_2/Project1/Source**: prima viene caricato il file a livello di utente (A), quindi NuGet carica il file (B) dalla radice di disk_drive_2, seguito dal file (C). Le impostazioni in (C) eseguono l'override di quelle in (B) e (A), quindi i pacchetti vengono installati nel `repositoryPath` disk_drive_2/Project1/External/Packages invece che in *disk_drive_2/tmp*. Inoltre, poiché (C) cancella `<packageSources>`, nuget.org non è più disponibile come origine e rimane solo `https://MyPrivateRepo/ES/nuget`.

- **Chiamata da disk_drive_2/Project2 o disk_drive_2/Project2/Source**: viene caricato prima il file a livello di utente (A) seguito dal file (B) e dal file (D). Poiché `packageSources` non viene cancellato, sia `nuget.org` che `https://MyPrivateRepo/DQ/nuget` sono disponibili come origini. I pacchetti vengono espansi in disk_drive_2/tmp, come specificato in (B).

## <a name="nuget-defaults-file"></a>File delle impostazioni predefinite di NuGet

Lo scopo del file `NuGetDefaults.Config` è quello di specificare le origini da cui i pacchetti vengono installati e aggiornati e di controllare la destinazione predefinita per la pubblicazione dei pacchetti con `nuget push`. Poiché gli amministratori possono distribuire facilmente agli sviluppatori e ai computer di compilazione (ad esempio usando i Criteri di gruppo) file `NuGetDefaults.Config` coerenti, possono assicurarsi che tutti nell'organizzazione usino le origini dei pacchetti corrette invece di nuget.org.

> [!Important]
> Il file `NuGetDefaults.Config` non causa mai la rimozione di un pacchetto dalla configurazione NuGet di uno sviluppatore. Se dunque lo sviluppatore ha già usato NuGet e quindi l'origine del pacchetto nuget.org è già registrata, non verrà rimossa dopo la creazione di un file `NuGetDefaults.Config`.
>
> Inoltre né `NuGetDefaults.Config` né altri meccanismi in NuGet possono impedire l'accesso alle origini dei pacchetti, ad esempio nuget.org. Se un'organizzazione vuole bloccare tale accesso, deve farlo in altro modo, ad esempio usando un firewall.

### <a name="nugetdefaultsconfig-location"></a>Percorso di NuGetDefaults.Config

La tabella seguente descrive la posizione di archiviazione prevista per il file `NuGetDefaults.Config`, a seconda del sistema operativo di destinazione:

| Piattaforma del sistema operativo  | Percorso di NuGetDefaults.Config |
| --- | --- |
| WINDOWS      | **Visual Studio 2017 o NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 e versioni precedenti o NuGet 3.x e versioni precedenti:** `%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME` (in genere `~/.local/share` o `/usr/local/share`, a seconda della distribuzione del sistema operativo)|

### <a name="nugetdefaultsconfig-settings"></a>Impostazioni di NuGetDefaults.Config

- `packageSources`: questa raccolta ha lo stesso significato di `packageSources` nei normali file di configurazione e specifica le origini predefinite. NuGet usa le origini in ordine durante l'installazione o l'aggiornamento di pacchetti nei progetti usando il formato di gestione `packages.config`. Per i progetti che usano il formato PackageReference, NuGet usa prima di tutto le origini locali, quindi le origini in condivisioni di rete, poi le origini HTTP, indipendentemente dall'ordine nei file di configurazione. NuGet Ignora sempre l'ordine delle origini con le operazioni di ripristino.

- `disabledPackageSources`: questa raccolta ha anche lo stesso significato che nei file `NuGet.Config`, dove ogni origine interessata viene elencata per nome e un valore true/false indica se è disabilitata. In questo modo il nome e l'URL dell'origine possono rimanere in `packageSources` senza che debba essere attivata per impostazione predefinita. I singoli sviluppatori possono quindi riabilitare l'origine impostandone il valore su false negli altri file `NuGet.Config` senza dover trovare di nuovo l'URL corretto. Questo è utile anche per fornire agli sviluppatori un elenco completo di URL delle origini interne per un'organizzazione, abilitando al contempo solo l'origine di un singolo team per impostazione predefinita.

- `defaultPushSource`: specifica la destinazione predefinita per le operazioni `nuget push`, eseguendo l'override dell'impostazione predefinita di nuget.org. Gli amministratori possono distribuire questa impostazione per evitare la pubblicazione accidentale di pacchetti interni in nuget.org pubblico, perché gli sviluppatori devono specificamente usare `nuget push -Source` per eseguire la pubblicazione in nuget.org.

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
