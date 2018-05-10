---
title: Configurazione del comportamento di NuGet
description: I file NuGet.Config controllano il comportamento di NuGet sia a livello globale che di progetto e vengono modificati con il comando nuget config.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: c8cc78be1bd48adc603b9447282a6c4bef7f942f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="configuring-nuget-behavior"></a><span data-ttu-id="f004f-103">Configurazione del comportamento di NuGet</span><span class="sxs-lookup"><span data-stu-id="f004f-103">Configuring NuGet behavior</span></span>

<span data-ttu-id="f004f-104">Il comportamento di NuGet si basa sulle impostazioni accumulate in uno o più file `NuGet.Config` (XML) che possono esistere a livello di progetto, di utente e di computer.</span><span class="sxs-lookup"><span data-stu-id="f004f-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="f004f-105">Un file `NuGetDefaults.Config` globale configura anche in particolare le origini dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f004f-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="f004f-106">Le impostazioni si applicano a tutti i comandi eseguiti nell'interfaccia della riga di comando, nella console di Gestione pacchetti e nell'interfaccia utente di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f004f-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="f004f-107">Percorsi e usi dei file di configurazione</span><span class="sxs-lookup"><span data-stu-id="f004f-107">Config file locations and uses</span></span>

| <span data-ttu-id="f004f-108">Ambito</span><span class="sxs-lookup"><span data-stu-id="f004f-108">Scope</span></span> | <span data-ttu-id="f004f-109">Percorso del file NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="f004f-109">NuGet.Config file location</span></span> | <span data-ttu-id="f004f-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f004f-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f004f-111">Progetto</span><span class="sxs-lookup"><span data-stu-id="f004f-111">Project</span></span> | <span data-ttu-id="f004f-112">Cartella corrente (ovvero la cartella di progetto) o qualsiasi cartella fino alla radice dell'unità</span><span class="sxs-lookup"><span data-stu-id="f004f-112">Current folder (aka Project folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="f004f-113">In una cartella di progetto le impostazioni si applicano solo a tale progetto.</span><span class="sxs-lookup"><span data-stu-id="f004f-113">In a project folder, settings apply only to that project.</span></span> <span data-ttu-id="f004f-114">Nelle cartelle padre contenenti più sottocartelle di progetto, le impostazioni si applicano a tutti i progetti in tali sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="f004f-114">In parent folders that contain multiple projects subfolders, settings apply to all projects in those subfolders.</span></span> |
| <span data-ttu-id="f004f-115">Utente</span><span class="sxs-lookup"><span data-stu-id="f004f-115">User</span></span> | <span data-ttu-id="f004f-116">Windows: `%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="f004f-116">Windows: `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="f004f-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` o `~/.nuget/NuGet/NuGet.Config` (a seconda della distribuzione del sistema operativo)</span><span class="sxs-lookup"><span data-stu-id="f004f-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> | <span data-ttu-id="f004f-118">Le impostazioni si applicano a tutte le operazioni, ma ne viene eseguito l'override dalle impostazioni a livello di progetto.</span><span class="sxs-lookup"><span data-stu-id="f004f-118">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="f004f-119">Computer</span><span class="sxs-lookup"><span data-stu-id="f004f-119">Computer</span></span> | <span data-ttu-id="f004f-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="f004f-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="f004f-121">Mac/Linux: `$XDG_DATA_HOME`.</span><span class="sxs-lookup"><span data-stu-id="f004f-121">Mac/Linux: `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="f004f-122">Se `$XDG_DATA_HOME` è null o vuoto, verrà usato `~/.local/share` o `/usr/local/share` (a seconda della distribuzione del sistema operativo)</span><span class="sxs-lookup"><span data-stu-id="f004f-122">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="f004f-123">Le impostazioni si applicano a tutte le operazioni sul computer, ma ne viene eseguito l'override dalle impostazioni a livello di utente o di progetto.</span><span class="sxs-lookup"><span data-stu-id="f004f-123">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="f004f-124">Note per versioni precedenti di NuGet:</span><span class="sxs-lookup"><span data-stu-id="f004f-124">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="f004f-125">NuGet 3.3 e versioni precedenti usavano una cartella `.nuget` per le impostazioni a livello di soluzione.</span><span class="sxs-lookup"><span data-stu-id="f004f-125">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="f004f-126">Questo file non viene usato in NuGet 3.4+.</span><span class="sxs-lookup"><span data-stu-id="f004f-126">This file is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="f004f-127">Per NuGet da 2.6 a 3.x, il file di configurazione a livello di computer in Windows si trovava in %ProgramData%\NuGet\Config[\\{IDE}[\\{Versione}[\\{SKU}]]]\NuGet.Config, dove *{IDE}* può essere *VisualStudio*, *{Versione}* era la versione di Visual Studio, ad esempio *14.0*, e *{SKU}* è *Community*, *Pro* o *Enterprise*.</span><span class="sxs-lookup"><span data-stu-id="f004f-127">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="f004f-128">Per eseguire la migrazione delle impostazioni a NuGet 4.0+, è sufficiente copiare il file di configurazione in %Programmi(x86)%\NuGet\Config. In Linux questo percorso precedente era /etc/opt e in Mac /Library/Application Support.</span><span class="sxs-lookup"><span data-stu-id="f004f-128">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="f004f-129">Modifica delle impostazioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="f004f-129">Changing config settings</span></span>

<span data-ttu-id="f004f-130">Un file `NuGet.Config` è un semplice file di testo XML contenente coppie chiave/valore, come illustrato nell'argomento [Impostazioni di configurazione NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="f004f-130">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="f004f-131">Le impostazioni vengono gestite usando il [comando config](../tools/cli-ref-config.md) dell'interfaccia della riga di comando di NuGet:</span><span class="sxs-lookup"><span data-stu-id="f004f-131">Settings are managed using the NuGet CLI [config command](../tools/cli-ref-config.md):</span></span>
- <span data-ttu-id="f004f-132">Per impostazione predefinita, le modifiche vengono apportate al file di configurazione a livello di utente.</span><span class="sxs-lookup"><span data-stu-id="f004f-132">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="f004f-133">Per modificare le impostazioni in un file diverso, usare l'opzione `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="f004f-133">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="f004f-134">In questo caso i file possono usare qualsiasi nome.</span><span class="sxs-lookup"><span data-stu-id="f004f-134">In this case files can use any filename.</span></span>
- <span data-ttu-id="f004f-135">Per le chiavi la distinzione tra maiuscole e minuscole si applica sempre.</span><span class="sxs-lookup"><span data-stu-id="f004f-135">Keys are always case sensitive.</span></span>
- <span data-ttu-id="f004f-136">L'elevazione è necessaria per modificare le impostazioni nel file delle impostazioni a livello di computer.</span><span class="sxs-lookup"><span data-stu-id="f004f-136">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="f004f-137">Anche se è possibile modificare il file in qualsiasi editor di testo, NuGet (versioni 3.4.3 e successive) ignora senza avvisare l'intero file di configurazione se contiene XML non valido (tag non corrispondenti, virgolette non valide e così via).</span><span class="sxs-lookup"><span data-stu-id="f004f-137">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="f004f-138">Per questo motivo è preferibile gestire le impostazioni usando `nuget config`.</span><span class="sxs-lookup"><span data-stu-id="f004f-138">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="f004f-139">Impostazione di un valore</span><span class="sxs-lookup"><span data-stu-id="f004f-139">Setting a value</span></span>

<span data-ttu-id="f004f-140">Windows:</span><span class="sxs-lookup"><span data-stu-id="f004f-140">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\NuGet.Config
```

<span data-ttu-id="f004f-141">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="f004f-141">Mac/Linux:</span></span>

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
> <span data-ttu-id="f004f-142">In NuGet 3.4 e versioni successive è possibile usare le variabili di ambiente in qualsiasi valore, come in `repositoryPath=%PACKAGEHOME%` (Windows) e `repositoryPath=%PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="f004f-142">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=%PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="f004f-143">Rimozione di un valore</span><span class="sxs-lookup"><span data-stu-id="f004f-143">Removing a value</span></span>

<span data-ttu-id="f004f-144">Per rimuovere un valore, specificare una chiave con un valore vuoto.</span><span class="sxs-lookup"><span data-stu-id="f004f-144">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="f004f-145">Creazione di un nuovo file di configurazione</span><span class="sxs-lookup"><span data-stu-id="f004f-145">Creating a new config file</span></span>

<span data-ttu-id="f004f-146">Copiare il modello seguente nel nuovo file e quindi usare `nuget config -configFile <filename>` per impostare i valori:</span><span class="sxs-lookup"><span data-stu-id="f004f-146">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="f004f-147">Come vengono applicate le impostazioni</span><span class="sxs-lookup"><span data-stu-id="f004f-147">How settings are applied</span></span>

<span data-ttu-id="f004f-148">Più file `NuGet.Config` consentono di archiviare le impostazioni in posizioni diverse in modo che vengano applicate a un progetto, a un gruppo di progetti o a tutti i progetti.</span><span class="sxs-lookup"><span data-stu-id="f004f-148">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="f004f-149">Queste impostazioni si applicano complessivamente a qualsiasi operazione NuGet richiamata dalla riga di comando o da Visual Studio. Hanno la precedenza le impostazioni che si trovano "più vicino" a un progetto o alla cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="f004f-149">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="f004f-150">In particolare, NuGet carica le impostazioni dai diversi file di configurazione nell'ordine seguente:</span><span class="sxs-lookup"><span data-stu-id="f004f-150">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="f004f-151">Il [file NuGetDefaults.Config](#nuget-defaults-file), che contiene le impostazioni relative solo alle origini dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f004f-151">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="f004f-152">Il file a livello di computer.</span><span class="sxs-lookup"><span data-stu-id="f004f-152">The computer-level file.</span></span>
1. <span data-ttu-id="f004f-153">Il file a livello di utente.</span><span class="sxs-lookup"><span data-stu-id="f004f-153">The user-level file.</span></span>
1. <span data-ttu-id="f004f-154">Il file specificato con `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="f004f-154">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="f004f-155">File presenti in ogni cartella del percorso dalla radice dell'unità alla cartella corrente (dove viene richiamato nuget.exe o la cartella contenente il progetto di Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="f004f-155">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="f004f-156">Se ad esempio un comando viene richiamato in c:\A\B\C, NuGet cerca e carica i file di configurazione in c:\, quindi in c:\A, poi in c:\A\B e infine in c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="f004f-156">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="f004f-157">Quando NuGet trova le impostazioni in questi file, le applica come segue:</span><span class="sxs-lookup"><span data-stu-id="f004f-157">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="f004f-158">Per gli elementi singoli, NuGet sostituisce i valori trovati in precedenza per la stessa chiave.</span><span class="sxs-lookup"><span data-stu-id="f004f-158">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="f004f-159">Questo significa che le impostazioni "più vicine" alla cartella o al progetto corrente eseguono l'override delle altre trovate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f004f-159">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="f004f-160">L'impostazione `defaultPushSource` in `NuGetDefaults.Config`, ad esempio, viene sostituita se esiste in un altro file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f004f-160">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="f004f-161">Per gli elementi delle raccolte (ad esempio, `<packageSources>`), NuGet combina i valori di tutti i file di configurazione in una singola raccolta.</span><span class="sxs-lookup"><span data-stu-id="f004f-161">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="f004f-162">Quando `<clear />` è presente per un determinato nodo, NuGet ignora i valori di configurazione definiti in precedenza per tale nodo.</span><span class="sxs-lookup"><span data-stu-id="f004f-162">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="f004f-163">Procedura dettagliata per le impostazioni</span><span class="sxs-lookup"><span data-stu-id="f004f-163">Settings walkthrough</span></span>

<span data-ttu-id="f004f-164">Si supponga di avere la struttura di cartelle seguente in due unità separate:</span><span class="sxs-lookup"><span data-stu-id="f004f-164">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="f004f-165">Si hanno poi quattro file `NuGet.Config` nelle posizioni seguenti con il contenuto indicato.</span><span class="sxs-lookup"><span data-stu-id="f004f-165">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="f004f-166">Il file a livello di computer non è incluso in questo esempio, ma il comportamento sarà simile a quello del file a livello di utente.</span><span class="sxs-lookup"><span data-stu-id="f004f-166">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="f004f-167">File A. File a livello di utente, (`%appdata%\NuGet\NuGet.Config` in Windows, `~/.config/NuGet/NuGet.Config` in Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="f004f-167">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="f004f-168">File B. disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="f004f-168">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="f004f-169">File C. disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="f004f-169">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="f004f-170">File D. disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="f004f-170">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="f004f-171">NuGet quindi carica e applica le impostazioni come segue, a seconda della posizione da dove viene eseguita la chiamata:</span><span class="sxs-lookup"><span data-stu-id="f004f-171">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="f004f-172">**Chiamata da disk_drive_1/users**: viene usato solo il repository predefinito elencato nel file di configurazione a livello di utente (A), perché è il solo file presente in disk_drive_1.</span><span class="sxs-lookup"><span data-stu-id="f004f-172">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="f004f-173">**Chiamata da disk_drive_2/ o disk_drive_/tmp**: prima viene caricato il file a livello di utente (A), quindi NuGet passa alla radice di disk_drive_2 e trova il file (B).</span><span class="sxs-lookup"><span data-stu-id="f004f-173">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="f004f-174">NuGet cerca anche un file di configurazione in /tmp, ma non lo trova.</span><span class="sxs-lookup"><span data-stu-id="f004f-174">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="f004f-175">Viene quindi usato il repository predefinito in nuget.org, viene abilitato il ripristino dei pacchetti e i pacchetti vengono espansi in disk_drive_2/tmp.</span><span class="sxs-lookup"><span data-stu-id="f004f-175">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="f004f-176">**Chiamata da disk_drive_2/Project1 o disk_drive_2/Project1/Source**: prima viene caricato il file a livello di utente (A), quindi NuGet carica il file (B) dalla radice di disk_drive_2, seguito dal file (C).</span><span class="sxs-lookup"><span data-stu-id="f004f-176">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="f004f-177">Le impostazioni in (C) eseguono l'override di quelle in (B) e (A), quindi i pacchetti vengono installati nel `repositoryPath` disk_drive_2/Project1/External/Packages invece che in *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="f004f-177">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="f004f-178">Inoltre, poiché (C) cancella `<packageSources>`, nuget.org non è più disponibile come origine e rimane solo `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="f004f-178">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="f004f-179">**Chiamata da disk_drive_2/Project2 o disk_drive_2/Project2/Source**: viene caricato prima il file a livello di utente (A) seguito dal file (B) e dal file (D).</span><span class="sxs-lookup"><span data-stu-id="f004f-179">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="f004f-180">Poiché `packageSources` non viene cancellato, sia `nuget.org` che `https://MyPrivateRepo/DQ/nuget` sono disponibili come origini.</span><span class="sxs-lookup"><span data-stu-id="f004f-180">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="f004f-181">I pacchetti vengono espansi in disk_drive_2/tmp, come specificato in (B).</span><span class="sxs-lookup"><span data-stu-id="f004f-181">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="f004f-182">File delle impostazioni predefinite di NuGet</span><span class="sxs-lookup"><span data-stu-id="f004f-182">NuGet defaults file</span></span>

<span data-ttu-id="f004f-183">Lo scopo del file `NuGetDefaults.Config` è quello di specificare le origini da cui i pacchetti vengono installati e aggiornati e di controllare la destinazione predefinita per la pubblicazione dei pacchetti con `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="f004f-183">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="f004f-184">Poiché gli amministratori possono distribuire facilmente agli sviluppatori e ai computer di compilazione (ad esempio usando i Criteri di gruppo) file `NuGetDefaults.Config` coerenti, possono assicurarsi che tutti nell'organizzazione usino le origini dei pacchetti corrette invece di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f004f-184">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensuring that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="f004f-185">Il file `NuGetDefaults.Config` non causa mai la rimozione di un pacchetto dalla configurazione NuGet di uno sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="f004f-185">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="f004f-186">Se dunque lo sviluppatore ha già usato NuGet e quindi l'origine del pacchetto nuget.org è già registrata, non verrà rimossa dopo la creazione di un file `NuGetDefaults.Config`.</span><span class="sxs-lookup"><span data-stu-id="f004f-186">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="f004f-187">Inoltre né `NuGetDefaults.Config` né altri meccanismi in NuGet possono impedire l'accesso alle origini dei pacchetti, ad esempio nuget.org. Se un'organizzazione vuole bloccare tale accesso, deve farlo in altro modo, ad esempio usando un firewall.</span><span class="sxs-lookup"><span data-stu-id="f004f-187">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it much use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="f004f-188">Percorso di NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="f004f-188">NuGetDefaults.Config location</span></span>

<span data-ttu-id="f004f-189">La tabella seguente descrive la posizione di archiviazione prevista per il file `NuGetDefaults.Config`, a seconda del sistema operativo di destinazione:</span><span class="sxs-lookup"><span data-stu-id="f004f-189">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="f004f-190">Piattaforma del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="f004f-190">OS Platform</span></span>  | <span data-ttu-id="f004f-191">Percorso di NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="f004f-191">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="f004f-192">WINDOWS</span><span class="sxs-lookup"><span data-stu-id="f004f-192">Windows</span></span>      | <span data-ttu-id="f004f-193">**Visual Studio 2017 o NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="f004f-193">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="f004f-194">**Visual Studio 2015 e versioni precedenti o NuGet 3.x e versioni precedenti:** `%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="f004f-194">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="f004f-195">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="f004f-195">Mac/Linux</span></span>    | <span data-ttu-id="f004f-196">`$XDG_DATA_HOME` (in genere `~/.local/share` o `/usr/local/share`, a seconda della distribuzione del sistema operativo)</span><span class="sxs-lookup"><span data-stu-id="f004f-196">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="f004f-197">Impostazioni di NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="f004f-197">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="f004f-198">`packageSources`: questa raccolta ha lo stesso significato di `packageSources` nei normali file di configurazione e specifica le origini predefinite.</span><span class="sxs-lookup"><span data-stu-id="f004f-198">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="f004f-199">NuGet usa le origini in ordine durante l'installazione o l'aggiornamento di pacchetti nei progetti usando il formato di gestione `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="f004f-199">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="f004f-200">Per i progetti che usano il formato PackageReference, NuGet usa prima di tutto le origini locali, quindi le origini in condivisioni di rete, poi le origini HTTP, indipendentemente dall'ordine nei file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f004f-200">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="f004f-201">NuGet Ignora sempre l'ordine delle origini con le operazioni di ripristino.</span><span class="sxs-lookup"><span data-stu-id="f004f-201">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="f004f-202">`disabledPackageSources`: questa raccolta ha anche lo stesso significato che nei file `NuGet.Config`, dove ogni origine interessata viene elencata per nome e un valore true/false indica se è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="f004f-202">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="f004f-203">In questo modo il nome e l'URL dell'origine possono rimanere in `packageSources` senza che debba essere attivata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f004f-203">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="f004f-204">I singoli sviluppatori possono quindi riabilitare l'origine impostandone il valore su false negli altri file `NuGet.Config` senza dover trovare di nuovo l'URL corretto.</span><span class="sxs-lookup"><span data-stu-id="f004f-204">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="f004f-205">Questo è utile anche per fornire agli sviluppatori un elenco completo di URL delle origini interne per un'organizzazione, abilitando al contempo solo l'origine di un singolo team per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f004f-205">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="f004f-206">`defaultPushSource`: specifica la destinazione predefinita per le operazioni `nuget push`, eseguendo l'override dell'impostazione predefinita di nuget.org. Gli amministratori possono distribuire questa impostazione per evitare la pubblicazione accidentale di pacchetti interni in nuget.org pubblico, perché gli sviluppatori devono specificamente usare `nuget push -Source` per eseguire la pubblicazione in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f004f-206">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="f004f-207">Applicazione e NuGetDefaults.Config di esempio</span><span class="sxs-lookup"><span data-stu-id="f004f-207">Example NuGetDefaults.Config and application</span></span>

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
