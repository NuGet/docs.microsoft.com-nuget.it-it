---
title: Configurazione del comportamento di NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c1e34826-d07d-4609-a0fd-123459ae89c5
description: I file NuGet.Config controllano il comportamento di NuGet sia a livello globale che di progetto e vengono modificati con il comando nuget config.
keywords: file di configurazione NuGet, configurazione NuGet, impostazioni del comportamento di NuGet, impostazioni NuGet, Nuget.Config, NuGetDefaults.Config, impostazioni predefinite
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f9e56b68f70387435cdaa1537db503abb912fd2a
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="configuring-nuget-behavior"></a><span data-ttu-id="dce62-104">Configurazione del comportamento di NuGet</span><span class="sxs-lookup"><span data-stu-id="dce62-104">Configuring NuGet behavior</span></span>

<span data-ttu-id="dce62-105">Il comportamento di NuGet si basa sulle impostazioni accumulate in uno o più file `NuGet.Config` (XML) che possono esistere a livello di progetto, di utente e di computer.</span><span class="sxs-lookup"><span data-stu-id="dce62-105">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="dce62-106">Un file `NuGetDefaults.Config` globale (2.7+) configura anche in particolare le origini dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="dce62-106">A global `NuGetDefaults.Config` file (2.7+) also specifically configures package sources.</span></span> <span data-ttu-id="dce62-107">Le impostazioni si applicano a tutti i comandi eseguiti nell'interfaccia della riga di comando, nella console di Gestione pacchetti e nell'interfaccia utente di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="dce62-107">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

<span data-ttu-id="dce62-108">Contenuto dell'argomento:</span><span class="sxs-lookup"><span data-stu-id="dce62-108">In this topic:</span></span>

- [<span data-ttu-id="dce62-109">Percorsi e usi dei file NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="dce62-109">NuGet.Config file locations and uses</span></span>](#config-file-locations-and-uses)
- [<span data-ttu-id="dce62-110">Modifica delle impostazioni</span><span class="sxs-lookup"><span data-stu-id="dce62-110">Changing settings</span></span>](#changing-config-settings)
- [<span data-ttu-id="dce62-111">Come vengono applicate le impostazioni</span><span class="sxs-lookup"><span data-stu-id="dce62-111">How settings are applied</span></span>](#how-settings-are-applied)
- [<span data-ttu-id="dce62-112">File NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="dce62-112">NuGetDefaults.Config file</span></span>](#nuget-defaults-file)

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="dce62-113">Percorsi e usi dei file di configurazione</span><span class="sxs-lookup"><span data-stu-id="dce62-113">Config file locations and uses</span></span>

| <span data-ttu-id="dce62-114">Ambito</span><span class="sxs-lookup"><span data-stu-id="dce62-114">Scope</span></span> | <span data-ttu-id="dce62-115">Percorso del file NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="dce62-115">NuGet.Config file location</span></span> | <span data-ttu-id="dce62-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dce62-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dce62-117">Progetto</span><span class="sxs-lookup"><span data-stu-id="dce62-117">Project</span></span> | <span data-ttu-id="dce62-118">Cartella di progetto o qualsiasi cartella fino alla radice dell'unità</span><span class="sxs-lookup"><span data-stu-id="dce62-118">Project folder or any folder up to the drive root</span></span> | <span data-ttu-id="dce62-119">In una cartella di progetto le impostazioni si applicano solo a tale progetto.</span><span class="sxs-lookup"><span data-stu-id="dce62-119">In a project folder, settings apply only to that project.</span></span> <span data-ttu-id="dce62-120">Nelle cartelle padre contenenti più sottocartelle di progetto, le impostazioni si applicano a tutti i progetti in tali sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="dce62-120">In parent folders that contain multiple projects subfolders, settings apply to all projects in those subfolders.</span></span> |
| <span data-ttu-id="dce62-121">Utente</span><span class="sxs-lookup"><span data-stu-id="dce62-121">User</span></span> | <span data-ttu-id="dce62-122">Windows: %APPDATA%\NuGet\NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="dce62-122">Windows: %APPDATA%\NuGet\NuGet.Config</span></span><br/><span data-ttu-id="dce62-123">Mac/Linux: ~/.nuget/NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="dce62-123">Mac/Linux: ~/.nuget/NuGet.Config</span></span> | <span data-ttu-id="dce62-124">Le impostazioni si applicano a tutte le operazioni, ma ne viene eseguito l'override dalle impostazioni a livello di progetto.</span><span class="sxs-lookup"><span data-stu-id="dce62-124">Settings apply to all operations, but are overridden by any project-level settings.</span></span> <span data-ttu-id="dce62-125">Quando si usano i comandi dell'interfaccia della riga di comando, è possibile specificare un file di configurazione diverso usando l'opzione `-configFile` per ignorare le impostazioni nel file a livello di utente predefinito.</span><span class="sxs-lookup"><span data-stu-id="dce62-125">When using CLI commands, you can specify a different config file using the `-configFile` switch to ignore any settings in the default user-level file.</span></span> |
| <span data-ttu-id="dce62-126">Computer</span><span class="sxs-lookup"><span data-stu-id="dce62-126">Computer</span></span> | <span data-ttu-id="dce62-127">Windows: %Programmi(x86)%\NuGet\Config</span><span class="sxs-lookup"><span data-stu-id="dce62-127">Windows: %ProgramFiles(x86)%\NuGet\Config</span></span><br/><span data-ttu-id="dce62-128">Mac/Linux: $XDG_DATA_HOME (in genere ~/.local/share)</span><span class="sxs-lookup"><span data-stu-id="dce62-128">Mac/Linux: $XDG_DATA_HOME (typically ~/.local/share)</span></span> | <span data-ttu-id="dce62-129">Le impostazioni si applicano a tutte le operazioni sul computer, ma ne viene eseguito l'override dalle impostazioni a livello di utente o di progetto.</span><span class="sxs-lookup"><span data-stu-id="dce62-129">Settings apply to all operations on the computer, but are overriden by any user- or project-level settings.</span></span> |

<span data-ttu-id="dce62-130">Note per versioni precedenti di NuGet:</span><span class="sxs-lookup"><span data-stu-id="dce62-130">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="dce62-131">NuGet 3.3 e versioni precedenti usavano una cartella `.nuget` per le impostazioni a livello di soluzione.</span><span class="sxs-lookup"><span data-stu-id="dce62-131">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="dce62-132">Questo file non viene usato in NuGet 3.4+.</span><span class="sxs-lookup"><span data-stu-id="dce62-132">This file not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="dce62-133">Per NuGet da 2.6 a 3.x, il file di configurazione a livello di computer in Windows si trovava in %ProgramData%\NuGet\Config[\\{IDE}[\\{Versione}[\\{SKU}]]]\NuGet.Config, dove *{IDE}* può essere *VisualStudio*, *{Versione}* era la versione di Visual Studio, ad esempio *14.0*, e *{SKU}* è *Community*, *Pro* o *Enterprise*.</span><span class="sxs-lookup"><span data-stu-id="dce62-133">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="dce62-134">Per eseguire la migrazione delle impostazioni a NuGet 4.0+, è sufficiente copiare il file di configurazione in %Programmi(x86)%\NuGet\Config. In Linux questo percorso precedente era /etc/opt e in Mac /Library/Application Support.</span><span class="sxs-lookup"><span data-stu-id="dce62-134">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linus, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="dce62-135">Modifica delle impostazioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="dce62-135">Changing config settings</span></span>

<span data-ttu-id="dce62-136">Un file `NuGet.Config` è un semplice file di testo XML contenente coppie chiave/valore, come illustrato nell'argomento [Impostazioni di configurazione NuGet](../Schema/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="dce62-136">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../Schema/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="dce62-137">Le impostazioni vengono gestite usando il [comando config](../tools/cli-ref-config.md) dell'interfaccia della riga di comando di NuGet:</span><span class="sxs-lookup"><span data-stu-id="dce62-137">Settings are managed using the NuGet CLI [config command](../tools/cli-ref-config.md):</span></span>
- <span data-ttu-id="dce62-138">Per impostazione predefinita, le modifiche vengono apportate al file di configurazione a livello di utente.</span><span class="sxs-lookup"><span data-stu-id="dce62-138">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="dce62-139">Per modificare le impostazioni in un file diverso, usare l'opzione `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="dce62-139">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="dce62-140">In questo caso i file possono usare qualsiasi nome.</span><span class="sxs-lookup"><span data-stu-id="dce62-140">In this case files can use any filename.</span></span>
- <span data-ttu-id="dce62-141">Per le chiavi la distinzione tra maiuscole e minuscole si applica sempre.</span><span class="sxs-lookup"><span data-stu-id="dce62-141">Keys are always case sensitive.</span></span>
- <span data-ttu-id="dce62-142">L'elevazione è necessaria per modificare le impostazioni nel file delle impostazioni a livello di computer.</span><span class="sxs-lookup"><span data-stu-id="dce62-142">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="dce62-143">Anche se è possibile modificare il file in qualsiasi editor di testo, NuGet (versioni 3.4.3 e successive) ignora senza avvisare l'intero file di configurazione se contiene XML non valido (tag non corrispondenti, virgolette non valide e così via).</span><span class="sxs-lookup"><span data-stu-id="dce62-143">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="dce62-144">Per questo motivo è preferibile gestire le impostazioni usando `nuget config`.</span><span class="sxs-lookup"><span data-stu-id="dce62-144">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="dce62-145">Impostazione di un valore</span><span class="sxs-lookup"><span data-stu-id="dce62-145">Setting a value</span></span>

<span data-ttu-id="dce62-146">Windows:</span><span class="sxs-lookup"><span data-stu-id="dce62-146">Windows:</span></span>

```
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\NuGet.Config
```

<span data-ttu-id="dce62-147">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="dce62-147">Mac/Linux:</span></span>

```
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> <span data-ttu-id="dce62-148">In NuGet 3.4 e versioni successive è possibile usare le variabili di ambiente in qualsiasi valore, come in `repositoryPath=%PACKAGEHOME%` (Windows) e `repositoryPath=%PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="dce62-148">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=%PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="dce62-149">Rimozione di un valore</span><span class="sxs-lookup"><span data-stu-id="dce62-149">Removing a value</span></span>

<span data-ttu-id="dce62-150">Per rimuovere un valore, specificare una chiave con un valore vuoto.</span><span class="sxs-lookup"><span data-stu-id="dce62-150">To remove a value, specify a key with an empty value.</span></span>

```
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="dce62-151">Creazione di un nuovo file di configurazione</span><span class="sxs-lookup"><span data-stu-id="dce62-151">Creating a new config file</span></span>

<span data-ttu-id="dce62-152">Copiare il modello seguente nel nuovo file e quindi usare `nuget config --configFile <filename>` per impostare i valori:</span><span class="sxs-lookup"><span data-stu-id="dce62-152">Copy the template below into the new file and then use `nuget config --configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

<br/>

## <a name="how-settings-are-applied"></a><span data-ttu-id="dce62-153">Come vengono applicate le impostazioni</span><span class="sxs-lookup"><span data-stu-id="dce62-153">How settings are applied</span></span>

<span data-ttu-id="dce62-154">Più file `NuGet.Config` consentono di archiviare le impostazioni in posizioni diverse in modo che vengano applicate a un progetto, a un gruppo di progetti o a tutti i progetti.</span><span class="sxs-lookup"><span data-stu-id="dce62-154">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="dce62-155">Queste impostazioni si applicano complessivamente a qualsiasi operazione NuGet richiamata dalla riga di comando o da Visual Studio. Hanno la precedenza le impostazioni che si trovano "più vicino" a un progetto o alla cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="dce62-155">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="dce62-156">In particolare, NuGet carica le impostazioni dai diversi file di configurazione nell'ordine seguente:</span><span class="sxs-lookup"><span data-stu-id="dce62-156">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="dce62-157">Il [file NuGetDefaults.Config](#nuget-defaults-file), che contiene le impostazioni relative solo alle origini dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="dce62-157">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="dce62-158">Il file a livello di computer.</span><span class="sxs-lookup"><span data-stu-id="dce62-158">The computer-level file.</span></span>
1. <span data-ttu-id="dce62-159">Il file a livello di utente.</span><span class="sxs-lookup"><span data-stu-id="dce62-159">The user-level file.</span></span>
1. <span data-ttu-id="dce62-160">Il file specificato con `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="dce62-160">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="dce62-161">File presenti in ogni cartella del percorso dalla radice dell'unità alla cartella corrente (dove viene richiamato nuget.exe o la cartella contenente il progetto di Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="dce62-161">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="dce62-162">Se ad esempio un comando viene richiamato in c:\A\B\C, NuGet cerca e carica i file di configurazione in c:\, quindi in c:\A, poi in c:\A\B e infine in c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="dce62-162">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="dce62-163">Quando NuGet trova le impostazioni in questi file, le applica come segue:</span><span class="sxs-lookup"><span data-stu-id="dce62-163">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="dce62-164">Per gli elementi singoli, NuGet sostituisce i valori trovati in precedenza per la stessa chiave.</span><span class="sxs-lookup"><span data-stu-id="dce62-164">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="dce62-165">Questo significa che le impostazioni "più vicine" alla cartella o al progetto corrente eseguono l'override delle altre trovate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="dce62-165">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="dce62-166">L'impostazione `defaultPushSource` in `NuGetDefaults.Config`, ad esempio, viene sostituita se esiste in un altro file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="dce62-166">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="dce62-167">Per gli elementi delle raccolte (ad esempio, `<packageSources>`), NuGet combina i valori di tutti i file di configurazione in una singola raccolta.</span><span class="sxs-lookup"><span data-stu-id="dce62-167">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="dce62-168">Quando `<clear />` è presente per un determinato nodo, NuGet ignora i valori di configurazione definiti in precedenza per tale nodo.</span><span class="sxs-lookup"><span data-stu-id="dce62-168">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="dce62-169">Procedura dettagliata per le impostazioni</span><span class="sxs-lookup"><span data-stu-id="dce62-169">Settings walkthrough</span></span>

<span data-ttu-id="dce62-170">Si supponga di avere la struttura di cartelle seguente in due unità separate:</span><span class="sxs-lookup"><span data-stu-id="dce62-170">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="dce62-171">Si hanno poi quattro file `NuGet.Config` nelle posizioni seguenti con il contenuto indicato.</span><span class="sxs-lookup"><span data-stu-id="dce62-171">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="dce62-172">Il file a livello di computer non è incluso in questo esempio, ma il comportamento sarà simile a quello del file a livello di utente.</span><span class="sxs-lookup"><span data-stu-id="dce62-172">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="dce62-173">File A. File a livello di utente (%APPDATA%\NuGet\NuGet.Config in Windows, ~/.nuget/NuGet.Config in Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="dce62-173">File A. User-level file, (%APPDATA%\NuGet\NuGet.Config on Windows, ~/.nuget/NuGet.Config on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="dce62-174">File B. disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="dce62-174">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="dce62-175">File C. disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="dce62-175">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="dce62-176">File D. disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="dce62-176">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="dce62-177">NuGet quindi carica e applica le impostazioni come segue, a seconda della posizione da dove viene eseguita la chiamata:</span><span class="sxs-lookup"><span data-stu-id="dce62-177">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="dce62-178">**Chiamata da disk_drive_1/users**: viene usato solo il repository predefinito elencato nel file di configurazione a livello di utente (A), perché è il solo file presente in disk_drive_1.</span><span class="sxs-lookup"><span data-stu-id="dce62-178">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="dce62-179">**Chiamata da disk_drive_2/ o disk_drive_/tmp**: prima viene caricato il file a livello di utente (A), quindi NuGet passa alla radice di disk_drive_2 e trova il file (B).</span><span class="sxs-lookup"><span data-stu-id="dce62-179">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="dce62-180">NuGet cerca anche un file di configurazione in /tmp, ma non lo trova.</span><span class="sxs-lookup"><span data-stu-id="dce62-180">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="dce62-181">Viene quindi usato il repository predefinito in nuget.org, viene abilitato il ripristino dei pacchetti e i pacchetti vengono espansi in disk_drive_2/tmp.</span><span class="sxs-lookup"><span data-stu-id="dce62-181">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="dce62-182">**Chiamata da disk_drive_2/Project1 o disk_drive_2/Project1/Source**: prima viene caricato il file a livello di utente (A), quindi NuGet carica il file (B) dalla radice di disk_drive_2, seguito dal file (C).</span><span class="sxs-lookup"><span data-stu-id="dce62-182">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="dce62-183">Le impostazioni in (C) eseguono l'override di quelle in (B) e (A), quindi i pacchetti vengono installati nel `repositoryPath` disk_drive_2/Project1/External/Packages invece che in *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="dce62-183">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="dce62-184">Inoltre, poiché (C) cancella `<packageSources>`, nuget.org non è più disponibile come origine e rimane solo `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="dce62-184">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="dce62-185">**Chiamata da disk_drive_2/Project2 o disk_drive_2/Project2/Source**: viene caricato prima il file a livello di utente (A) seguito dal file (B) e dal file (D).</span><span class="sxs-lookup"><span data-stu-id="dce62-185">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="dce62-186">Poiché `packageSources` non viene cancellato, sia `nuget.org` che `https://MyPrivateRepo/DQ/nuget` sono disponibili come origini.</span><span class="sxs-lookup"><span data-stu-id="dce62-186">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="dce62-187">I pacchetti vengono espansi in disk_drive_2/tmp, come specificato in (B).</span><span class="sxs-lookup"><span data-stu-id="dce62-187">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="dce62-188">File delle impostazioni predefinite di NuGet</span><span class="sxs-lookup"><span data-stu-id="dce62-188">NuGet defaults file</span></span>

<span data-ttu-id="dce62-189">Lo scopo del file `NuGetDefaults.Config` è quello di specificare le origini da cui i pacchetti vengono installati e aggiornati e di controllare la destinazione predefinita per la pubblicazione dei pacchetti con `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="dce62-189">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="dce62-190">Poiché gli amministratori possono distribuire facilmente agli sviluppatori e ai computer di compilazione (ad esempio usando i Criteri di gruppo) file `NuGetDefaults.Config` coerenti, possono assicurarsi che tutti nell'organizzazione usino le origini dei pacchetti corrette invece di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="dce62-190">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensuring that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="dce62-191">Il file `NuGetDefaults.Config` non causa mai la rimozione di un pacchetto dalla configurazione NuGet di uno sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="dce62-191">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="dce62-192">Se dunque lo sviluppatore ha già usato NuGet e quindi l'origine del pacchetto nuget.org è già registrata, non verrà rimossa dopo la creazione di un file `NuGetDefaults.Config`.</span><span class="sxs-lookup"><span data-stu-id="dce62-192">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="dce62-193">Inoltre né `NuGetDefaults.Config` né altri meccanismi in NuGet possono impedire l'accesso alle origini dei pacchetti, ad esempio nuget.org. Se un'organizzazione vuole bloccare tale accesso, deve farlo in altro modo, ad esempio usando un firewall.</span><span class="sxs-lookup"><span data-stu-id="dce62-193">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it much use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="dce62-194">Percorso di NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="dce62-194">NuGetDefaults.Config location</span></span>

<span data-ttu-id="dce62-195">Windows: %Programmi(x86)%\NuGet\Config (da NuGet 2.7 a NuGet 3.x: %PROGRAMDATA%\NuGet\NuGetDefaults.Config) Mac/Linux: $XDG_DATA_HOME (in genere ~/.local/share)</span><span class="sxs-lookup"><span data-stu-id="dce62-195">Windows: %ProgramFiles(x86)%\NuGet\Config (NuGet 2.7 to NuGet 3.x: %PROGRAMDATA%\NuGet\NuGetDefaults.Config) Mac/Linux: $XDG_DATA_HOME (typically ~/.local/share)</span></span> 

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="dce62-196">Impostazioni di NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="dce62-196">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="dce62-197">`packageSources`: questa raccolta ha lo stesso significato di `packageSources` nei normali file di configurazione e specifica le origini predefinite nell'ordine preferito.</span><span class="sxs-lookup"><span data-stu-id="dce62-197">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources in their preferred order.</span></span> <span data-ttu-id="dce62-198">Se questa impostazione esiste in `NuGetDefaults.Config`, NuGet non usa nuget.org come origine dei pacchetti predefinita.</span><span class="sxs-lookup"><span data-stu-id="dce62-198">If this setting exists in `NuGetDefaults.Config`, then NuGet doesn't use nuget.org as a default package source.</span></span> <span data-ttu-id="dce62-199">Un amministratore può quindi fare in modo che tutti quelli che usano questo file si servano delle stesse origini ed evitino di usare nuget.org, se necessario.</span><span class="sxs-lookup"><span data-stu-id="dce62-199">An administrator can thus make sure that everyone using this file is working with the same sources and avoids using nuget.org if desired.</span></span>

- <span data-ttu-id="dce62-200">`disabledPackageSources`: questa raccolta ha anche lo stesso significato che nei file `NuGet.Config`, dove ogni origine interessata viene elencata per nome e un valore true/false indica se è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="dce62-200">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="dce62-201">In questo modo il nome e l'URL dell'origine possono rimanere in `packageSources` senza che debba essere attivata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="dce62-201">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="dce62-202">I singoli sviluppatori possono quindi riabilitare l'origine impostandone il valore su false negli altri file `NuGet.Config` senza dover trovare di nuovo l'URL corretto.</span><span class="sxs-lookup"><span data-stu-id="dce62-202">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="dce62-203">Questo è utile anche per fornire agli sviluppatori un elenco completo di URL delle origini interne per un'organizzazione, abilitando al contempo solo l'origine di un singolo team per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="dce62-203">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="dce62-204">`defaultPushSource`: specifica la destinazione predefinita per le operazioni `nuget push`, eseguendo l'override dell'impostazione predefinita di nuget.org. Gli amministratori possono distribuire questa impostazione per evitare la pubblicazione accidentale di pacchetti interni in nuget.org pubblico, perché gli sviluppatori devono specificamente usare `nuget push -Source` per eseguire la pubblicazione in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="dce62-204">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="dce62-205">Applicazione e NuGetDefaults.Config di esempio</span><span class="sxs-lookup"><span data-stu-id="dce62-205">Example NuGetDefaults.Config and application</span></span>

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
