---
title: Configurazioni comuni di NuGet
description: I file NuGet.Config controllano il comportamento di NuGet sia a livello globale che di progetto e vengono modificati con il comando nuget config.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: e81c380eab3f1a8635e50e62811c7ae463ec3653
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699777"
---
# <a name="common-nuget-configurations"></a><span data-ttu-id="1ce4b-103">Configurazioni comuni di NuGet</span><span class="sxs-lookup"><span data-stu-id="1ce4b-103">Common NuGet configurations</span></span>

<span data-ttu-id="1ce4b-104">Il comportamento di NuGet si basa sulle impostazioni accumulate in uno o più file `NuGet.Config` (XML) che possono esistere a livello di progetto, di utente e di computer.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="1ce4b-105">Un file `NuGetDefaults.Config` globale configura anche in particolare le origini dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="1ce4b-106">Le impostazioni si applicano a tutti i comandi eseguiti nell'interfaccia della riga di comando, nella console di Gestione pacchetti e nell'interfaccia utente di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="1ce4b-107">Percorsi e usi dei file di configurazione</span><span class="sxs-lookup"><span data-stu-id="1ce4b-107">Config file locations and uses</span></span>

| <span data-ttu-id="1ce4b-108">Scope</span><span class="sxs-lookup"><span data-stu-id="1ce4b-108">Scope</span></span> | <span data-ttu-id="1ce4b-109">Percorso del file NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="1ce4b-109">NuGet.Config file location</span></span> | <span data-ttu-id="1ce4b-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1ce4b-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1ce4b-111">Soluzione</span><span class="sxs-lookup"><span data-stu-id="1ce4b-111">Solution</span></span> | <span data-ttu-id="1ce4b-112">Cartella corrente (ovvero la cartella della soluzione) o qualsiasi cartella fino alla radice dell'unità.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-112">Current folder (aka Solution folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="1ce4b-113">Nella cartella di una soluzione le impostazioni si applicano a tutti i progetti presenti nelle sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-113">In a solution folder, settings apply to all projects in subfolders.</span></span> <span data-ttu-id="1ce4b-114">Si noti che se un file di configurazione viene inserito in una cartella di progetto, non ha alcun effetto su tale progetto.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-114">Note that if a config file is placed in a project folder, it has no effect on that project.</span></span> |
| <span data-ttu-id="1ce4b-115">Utente</span><span class="sxs-lookup"><span data-stu-id="1ce4b-115">User</span></span> | <span data-ttu-id="1ce4b-116">**Windows:**`%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="1ce4b-116">**Windows:** `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="1ce4b-117">**Mac/Linux:** `~/.config/NuGet/NuGet.Config` o `~/.nuget/NuGet/NuGet.Config` (varia in base alla distribuzione del sistema operativo)</span><span class="sxs-lookup"><span data-stu-id="1ce4b-117">**Mac/Linux:** `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> <br/><span data-ttu-id="1ce4b-118">Le configurazioni aggiuntive sono supportate in tutte le piattaforme.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-118">Additional configs are supported on all platforms.</span></span> <span data-ttu-id="1ce4b-119">Queste configurazioni non possono essere modificate dagli strumenti.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-119">These configs cannot be edited by the tooling.</span></span> </br> <span data-ttu-id="1ce4b-120">**Windows:**`%appdata%\NuGet\config\*.Config`</span><span class="sxs-lookup"><span data-stu-id="1ce4b-120">**Windows:** `%appdata%\NuGet\config\*.Config`</span></span> <br/><span data-ttu-id="1ce4b-121">**Mac/Linux:** `~/.config/NuGet/config/*.config` o `~/.nuget/config/*.config`</span><span class="sxs-lookup"><span data-stu-id="1ce4b-121">**Mac/Linux:** `~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span></span> | <span data-ttu-id="1ce4b-122">Le impostazioni si applicano a tutte le operazioni, ma ne viene eseguito l'override dalle impostazioni a livello di progetto.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-122">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="1ce4b-123">Computer</span><span class="sxs-lookup"><span data-stu-id="1ce4b-123">Computer</span></span> | <span data-ttu-id="1ce4b-124">**Windows:**`%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="1ce4b-124">**Windows:** `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="1ce4b-125">**Mac/Linux:** `$XDG_DATA_HOME` .</span><span class="sxs-lookup"><span data-stu-id="1ce4b-125">**Mac/Linux:** `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="1ce4b-126">Se `$XDG_DATA_HOME` è null o vuoto, verrà usato `~/.local/share` o `/usr/local/share` (a seconda della distribuzione del sistema operativo)</span><span class="sxs-lookup"><span data-stu-id="1ce4b-126">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="1ce4b-127">Le impostazioni si applicano a tutte le operazioni sul computer, ma ne viene eseguito l'override dalle impostazioni a livello di utente o di progetto.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-127">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="1ce4b-128">Note per versioni precedenti di NuGet:</span><span class="sxs-lookup"><span data-stu-id="1ce4b-128">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="1ce4b-129">NuGet 3.3 e versioni precedenti usavano una cartella `.nuget` per le impostazioni a livello di soluzione.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-129">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="1ce4b-130">Questa cartella non viene usata in NuGet 3.4 +.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-130">This folder is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="1ce4b-131">Per NuGet da 2.6 a 3.x, il file di configurazione a livello di computer in Windows si trovava in %ProgramData%\NuGet\Config[\\{IDE}[\\{Versione}[\\{SKU}]]]\NuGet.Config, dove *{IDE}* può essere *VisualStudio*, *{Versione}* era la versione di Visual Studio, ad esempio *14.0*, e *{SKU}* è *Community*, *Pro* o *Enterprise*.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-131">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="1ce4b-132">Per eseguire la migrazione delle impostazioni a NuGet 4.0 +, è sufficiente copiare il file di configurazione in% ProgramFiles (x86)% \ NuGet\Config. In Linux questo percorso precedente era/etc/opt e, in Mac, il supporto di/Libreria/Application.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-132">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="1ce4b-133">Modifica delle impostazioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="1ce4b-133">Changing config settings</span></span>

<span data-ttu-id="1ce4b-134">Un file `NuGet.Config` è un semplice file di testo XML contenente coppie chiave/valore, come illustrato nell'argomento [Impostazioni di configurazione NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="1ce4b-134">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="1ce4b-135">Le impostazioni vengono gestite usando il [comando config](../reference/cli-reference/cli-ref-config.md) dell'interfaccia della riga di comando di NuGet:</span><span class="sxs-lookup"><span data-stu-id="1ce4b-135">Settings are managed using the NuGet CLI [config command](../reference/cli-reference/cli-ref-config.md):</span></span>
- <span data-ttu-id="1ce4b-136">Per impostazione predefinita, le modifiche vengono apportate al file di configurazione a livello di utente.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-136">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="1ce4b-137">Per modificare le impostazioni in un file diverso, usare l'opzione `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-137">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="1ce4b-138">In questo caso i file possono usare qualsiasi nome.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-138">In this case files can use any filename.</span></span>
- <span data-ttu-id="1ce4b-139">Per le chiavi la distinzione tra maiuscole e minuscole si applica sempre.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-139">Keys are always case sensitive.</span></span>
- <span data-ttu-id="1ce4b-140">L'elevazione è necessaria per modificare le impostazioni nel file delle impostazioni a livello di computer.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-140">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="1ce4b-141">Anche se è possibile modificare il file in qualsiasi editor di testo, NuGet (versioni 3.4.3 e successive) ignora senza avvisare l'intero file di configurazione se contiene XML non valido (tag non corrispondenti, virgolette non valide e così via).</span><span class="sxs-lookup"><span data-stu-id="1ce4b-141">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="1ce4b-142">Per questo motivo è preferibile gestire le impostazioni usando `nuget config`.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-142">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="1ce4b-143">Impostazione di un valore</span><span class="sxs-lookup"><span data-stu-id="1ce4b-143">Setting a value</span></span>

<span data-ttu-id="1ce4b-144">Windows:</span><span class="sxs-lookup"><span data-stu-id="1ce4b-144">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="1ce4b-145">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="1ce4b-145">Mac/Linux:</span></span>

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
> <span data-ttu-id="1ce4b-146">In NuGet 3.4 e versioni successive è possibile usare le variabili di ambiente in qualsiasi valore, come in `repositoryPath=%PACKAGEHOME%` (Windows) e `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="1ce4b-146">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="1ce4b-147">Rimozione di un valore</span><span class="sxs-lookup"><span data-stu-id="1ce4b-147">Removing a value</span></span>

<span data-ttu-id="1ce4b-148">Per rimuovere un valore, specificare una chiave con un valore vuoto.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-148">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="1ce4b-149">Creazione di un nuovo file di configurazione</span><span class="sxs-lookup"><span data-stu-id="1ce4b-149">Creating a new config file</span></span>

<span data-ttu-id="1ce4b-150">Copiare il modello seguente nel nuovo file e quindi usare `nuget config -configFile <filename>` per impostare i valori:</span><span class="sxs-lookup"><span data-stu-id="1ce4b-150">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="1ce4b-151">Come vengono applicate le impostazioni</span><span class="sxs-lookup"><span data-stu-id="1ce4b-151">How settings are applied</span></span>

<span data-ttu-id="1ce4b-152">Più file `NuGet.Config` consentono di archiviare le impostazioni in posizioni diverse in modo che vengano applicate a un progetto, a un gruppo di progetti o a tutti i progetti.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-152">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="1ce4b-153">Queste impostazioni si applicano complessivamente a qualsiasi operazione NuGet richiamata dalla riga di comando o da Visual Studio. Hanno la precedenza le impostazioni che si trovano "più vicino" a un progetto o alla cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-153">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="1ce4b-154">In particolare, NuGet carica le impostazioni dai diversi file di configurazione nell'ordine seguente:</span><span class="sxs-lookup"><span data-stu-id="1ce4b-154">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="1ce4b-155">Il [file NuGetDefaults.Config](#nuget-defaults-file), che contiene le impostazioni relative solo alle origini dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-155">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="1ce4b-156">Il file a livello di computer.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-156">The computer-level file.</span></span>
1. <span data-ttu-id="1ce4b-157">Il file a livello di utente.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-157">The user-level file.</span></span>
1. <span data-ttu-id="1ce4b-158">Il file specificato con `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-158">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="1ce4b-159">File presenti in ogni cartella del percorso dalla radice dell'unità alla cartella corrente (dove viene richiamato nuget.exe o la cartella contenente il progetto di Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="1ce4b-159">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="1ce4b-160">Se ad esempio un comando viene richiamato in c:\A\B\C, NuGet cerca e carica i file di configurazione in c:\, quindi in c:\A, poi in c:\A\B e infine in c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-160">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="1ce4b-161">Quando NuGet trova le impostazioni in questi file, le applica come segue:</span><span class="sxs-lookup"><span data-stu-id="1ce4b-161">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="1ce4b-162">Per gli elementi singoli, NuGet sostituisce i valori trovati in precedenza per la stessa chiave.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-162">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="1ce4b-163">Questo significa che le impostazioni "più vicine" alla cartella o al progetto corrente eseguono l'override delle altre trovate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-163">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="1ce4b-164">L'impostazione `defaultPushSource` in `NuGetDefaults.Config`, ad esempio, viene sostituita se esiste in un altro file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-164">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="1ce4b-165">Per gli elementi delle raccolte (ad esempio, `<packageSources>`), NuGet combina i valori di tutti i file di configurazione in una singola raccolta.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-165">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="1ce4b-166">Quando `<clear />` è presente per un determinato nodo, NuGet ignora i valori di configurazione definiti in precedenza per tale nodo.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-166">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="1ce4b-167">Procedura dettagliata per le impostazioni</span><span class="sxs-lookup"><span data-stu-id="1ce4b-167">Settings walkthrough</span></span>

<span data-ttu-id="1ce4b-168">Si supponga di avere la struttura di cartelle seguente in due unità separate:</span><span class="sxs-lookup"><span data-stu-id="1ce4b-168">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="1ce4b-169">Si hanno poi quattro file `NuGet.Config` nelle posizioni seguenti con il contenuto indicato.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-169">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="1ce4b-170">Il file a livello di computer non è incluso in questo esempio, ma il comportamento sarà simile a quello del file a livello di utente.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-170">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="1ce4b-171">File A. File a livello di utente, (`%appdata%\NuGet\NuGet.Config` in Windows, `~/.config/NuGet/NuGet.Config` in Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="1ce4b-171">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="1ce4b-172">File B. disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="1ce4b-172">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="1ce4b-173">File C. disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="1ce4b-173">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="1ce4b-174">File D. disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="1ce4b-174">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="1ce4b-175">NuGet quindi carica e applica le impostazioni come segue, a seconda della posizione da dove viene eseguita la chiamata:</span><span class="sxs-lookup"><span data-stu-id="1ce4b-175">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="1ce4b-176">**Chiamata da disk_drive_1/users**: viene usato solo il repository predefinito elencato nel file di configurazione a livello di utente (A), perché è il solo file presente in disk_drive_1.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-176">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="1ce4b-177">**Chiamata da disk_drive_2/ o disk_drive_/tmp**: prima viene caricato il file a livello di utente (A), quindi NuGet passa alla radice di disk_drive_2 e trova il file (B).</span><span class="sxs-lookup"><span data-stu-id="1ce4b-177">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="1ce4b-178">NuGet cerca anche un file di configurazione in /tmp, ma non lo trova.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-178">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="1ce4b-179">Viene quindi usato il repository predefinito in nuget.org, viene abilitato il ripristino dei pacchetti e i pacchetti vengono espansi in disk_drive_2/tmp.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-179">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="1ce4b-180">**Chiamata da disk_drive_2/Project1 o disk_drive_2/Project1/Source**: prima viene caricato il file a livello di utente (A), quindi NuGet carica il file (B) dalla radice di disk_drive_2, seguito dal file (C).</span><span class="sxs-lookup"><span data-stu-id="1ce4b-180">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="1ce4b-181">Le impostazioni in (C) eseguono l'override di quelle in (B) e (A), quindi i pacchetti vengono installati nel `repositoryPath` disk_drive_2/Project1/External/Packages invece che in *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-181">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="1ce4b-182">Inoltre, poiché (C) cancella `<packageSources>`, nuget.org non è più disponibile come origine e rimane solo `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-182">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="1ce4b-183">**Chiamata da disk_drive_2/Project2 o disk_drive_2/Project2/Source**: viene caricato prima il file a livello di utente (A) seguito dal file (B) e dal file (D).</span><span class="sxs-lookup"><span data-stu-id="1ce4b-183">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="1ce4b-184">Poiché `packageSources` non viene cancellato, sia `nuget.org` che `https://MyPrivateRepo/DQ/nuget` sono disponibili come origini.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-184">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="1ce4b-185">I pacchetti vengono espansi in disk_drive_2/tmp, come specificato in (B).</span><span class="sxs-lookup"><span data-stu-id="1ce4b-185">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="additional-user-wide-configuration"></a><span data-ttu-id="1ce4b-186">Configurazione aggiuntiva a livello di utente</span><span class="sxs-lookup"><span data-stu-id="1ce4b-186">Additional user wide configuration</span></span>

<span data-ttu-id="1ce4b-187">A partire da 5,7, NuGet ha aggiunto il supporto per altri file di configurazione a livello di utente.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-187">Starting with 5.7, NuGet has added support for additional user wide configuration files.</span></span> <span data-ttu-id="1ce4b-188">Ciò consente ai fornitori di terze parti di aggiungere altri file di configurazione utente senza elevazione dei privilegi.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-188">This allows third-party vendors to add additional user configuration files without elevation.</span></span>
<span data-ttu-id="1ce4b-189">Questi file di configurazione si trovano nella cartella di configurazione a livello di utente standard all'interno di una `config` sottocartella.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-189">These configuration files are found in the standard user wide configuration folder within a `config` subfolder.</span></span>
<span data-ttu-id="1ce4b-190">Verranno considerati tutti i file che terminano con `.config` o `.Config` .</span><span class="sxs-lookup"><span data-stu-id="1ce4b-190">All files ending with `.config` or `.Config` will be considered.</span></span>
<span data-ttu-id="1ce4b-191">Questi file non possono essere modificati dagli strumenti standard.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-191">These files cannot be edited by the standard tooling.</span></span>

| <span data-ttu-id="1ce4b-192">Piattaforma del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="1ce4b-192">OS Platform</span></span>  | <span data-ttu-id="1ce4b-193">Configurazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1ce4b-193">Additional Configurations</span></span> |
| --- | --- |
| <span data-ttu-id="1ce4b-194">Windows</span><span class="sxs-lookup"><span data-stu-id="1ce4b-194">Windows</span></span>      | `%appdata%\NuGet\config\*.Config` |
| <span data-ttu-id="1ce4b-195">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="1ce4b-195">Mac/Linux</span></span>    | <span data-ttu-id="1ce4b-196">`~/.config/NuGet/config/*.config` o `~/.nuget/config/*.config`</span><span class="sxs-lookup"><span data-stu-id="1ce4b-196">`~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span></span> |

## <a name="nuget-defaults-file"></a><span data-ttu-id="1ce4b-197">File delle impostazioni predefinite di NuGet</span><span class="sxs-lookup"><span data-stu-id="1ce4b-197">NuGet defaults file</span></span>

<span data-ttu-id="1ce4b-198">Lo scopo del file `NuGetDefaults.Config` è quello di specificare le origini da cui i pacchetti vengono installati e aggiornati e di controllare la destinazione predefinita per la pubblicazione dei pacchetti con `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-198">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="1ce4b-199">Poiché gli amministratori possono distribuire facilmente file `NuGetDefaults.Config` coerenti agli sviluppatori e ai computer di compilazione (ad esempio usando Criteri di gruppo), possono assicurarsi che tutti nell'organizzazione usino le origini dei pacchetti corrette invece di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-199">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="1ce4b-200">Il file `NuGetDefaults.Config` non causa mai la rimozione di un pacchetto dalla configurazione NuGet di uno sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-200">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="1ce4b-201">Se dunque lo sviluppatore ha già usato NuGet e quindi l'origine del pacchetto nuget.org è già registrata, non verrà rimossa dopo la creazione di un file `NuGetDefaults.Config`.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-201">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="1ce4b-202">Inoltre, né `NuGetDefaults.Config` né alcun altro meccanismo in NuGet possono impedire l'accesso alle origini dei pacchetti, ad esempio NuGet.org. Se un'organizzazione desidera bloccare tale accesso, deve utilizzare altri mezzi, ad esempio i firewall, a tale scopo.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-202">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="1ce4b-203">Percorso di NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="1ce4b-203">NuGetDefaults.Config location</span></span>

<span data-ttu-id="1ce4b-204">La tabella seguente descrive la posizione di archiviazione prevista per il file `NuGetDefaults.Config`, a seconda del sistema operativo di destinazione:</span><span class="sxs-lookup"><span data-stu-id="1ce4b-204">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="1ce4b-205">Piattaforma del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="1ce4b-205">OS Platform</span></span>  | <span data-ttu-id="1ce4b-206">Percorso di NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="1ce4b-206">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="1ce4b-207">Windows</span><span class="sxs-lookup"><span data-stu-id="1ce4b-207">Windows</span></span>      | <span data-ttu-id="1ce4b-208">**Visual Studio 2017 o NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="1ce4b-208">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="1ce4b-209">**Visual Studio 2015 e versioni precedenti o NuGet 3.x e versioni precedenti:** `%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="1ce4b-209">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="1ce4b-210">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="1ce4b-210">Mac/Linux</span></span>    | <span data-ttu-id="1ce4b-211">`$XDG_DATA_HOME` (in genere `~/.local/share` o `/usr/local/share`, a seconda della distribuzione del sistema operativo)</span><span class="sxs-lookup"><span data-stu-id="1ce4b-211">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="1ce4b-212">Impostazioni di NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="1ce4b-212">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="1ce4b-213">`packageSources`: questa raccolta ha lo stesso significato di `packageSources` nei normali file di configurazione e specifica le origini predefinite.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-213">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="1ce4b-214">NuGet usa le origini in ordine durante l'installazione o l'aggiornamento di pacchetti nei progetti usando il formato di gestione `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-214">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="1ce4b-215">Per i progetti che usano il formato PackageReference, NuGet usa prima di tutto le origini locali, quindi le origini in condivisioni di rete, poi le origini HTTP, indipendentemente dall'ordine nei file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-215">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="1ce4b-216">NuGet Ignora sempre l'ordine delle origini con le operazioni di ripristino.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-216">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="1ce4b-217">`disabledPackageSources`: questa raccolta ha anche lo stesso significato che nei file `NuGet.Config`, dove ogni origine interessata viene elencata per nome e un valore true/false indica se è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-217">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="1ce4b-218">In questo modo il nome e l'URL dell'origine possono rimanere in `packageSources` senza che debba essere attivata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-218">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="1ce4b-219">I singoli sviluppatori possono quindi riabilitare l'origine impostandone il valore su false negli altri file `NuGet.Config` senza dover trovare di nuovo l'URL corretto.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-219">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="1ce4b-220">Questo è utile anche per fornire agli sviluppatori un elenco completo di URL delle origini interne per un'organizzazione, abilitando al contempo solo l'origine di un singolo team per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-220">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="1ce4b-221">`defaultPushSource`: specifica la destinazione predefinita per `nuget push` le operazioni, eseguendo l'override del valore predefinito predefinito di NuGet.org. Gli amministratori possono distribuire questa impostazione per evitare la pubblicazione di pacchetti interni in nuget.org pubblici per errore, in quanto gli sviluppatori devono usare `nuget push -Source` per pubblicare in NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="1ce4b-221">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="1ce4b-222">Applicazione e NuGetDefaults.Config di esempio</span><span class="sxs-lookup"><span data-stu-id="1ce4b-222">Example NuGetDefaults.Config and application</span></span>

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
