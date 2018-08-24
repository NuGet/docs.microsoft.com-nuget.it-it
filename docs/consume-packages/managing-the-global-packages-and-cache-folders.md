---
title: Come gestire le cartelle dei pacchetti globale, della cache e temporanea in NuGet
description: Come gestire la cartella di installazione dei pacchetti globale, la cartella della cache dei pacchetti e la cartella temporanea esistenti in un computer, usate durante l'installazione, il ripristino e l'aggiornamento dei pacchetti.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: 545e658d26b557f27d6534bf677f467e65a315b4
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/23/2018
ms.locfileid: "42793618"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="7c83a-103">Gestione delle cartelle dei pacchetti globale, della cache e temporanea</span><span class="sxs-lookup"><span data-stu-id="7c83a-103">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="7c83a-104">Quando si installa, aggiorna o ripristina un pacchetto, NuGet gestisce i pacchetti e le informazioni sui pacchetti in varie cartelle all'esterno della struttura del progetto:</span><span class="sxs-lookup"><span data-stu-id="7c83a-104">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="7c83a-105">nome</span><span class="sxs-lookup"><span data-stu-id="7c83a-105">Name</span></span> | <span data-ttu-id="7c83a-106">Descrizione e posizione (per utente)</span><span class="sxs-lookup"><span data-stu-id="7c83a-106">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="7c83a-107">global&#8209;packages</span><span class="sxs-lookup"><span data-stu-id="7c83a-107">global&#8209;packages</span></span> | <span data-ttu-id="7c83a-108">La cartella *global-packages* è la posizione in cui NuGet installa i pacchetti scaricati.</span><span class="sxs-lookup"><span data-stu-id="7c83a-108">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="7c83a-109">Ogni pacchetto viene espanso completamente in una sottocartella corrispondente all'identificatore del pacchetto e al numero di versione.</span><span class="sxs-lookup"><span data-stu-id="7c83a-109">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="7c83a-110">I progetti che usano il formato PackageReference usano sempre i pacchetti direttamente da questa cartella.</span><span class="sxs-lookup"><span data-stu-id="7c83a-110">Projects using the PackageReference format always use packages directly from this folder.</span></span> <span data-ttu-id="7c83a-111">Quando si usa il file `packages.config`, i pacchetti vengono installati nella cartella *global-packages* e quindi copiati nella cartella `packages` del progetto.</span><span class="sxs-lookup"><span data-stu-id="7c83a-111">When using the `packages.config`, packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="7c83a-112">Windows: `%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="7c83a-112">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="7c83a-113">Mac/Linux: `~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="7c83a-113">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="7c83a-114">Eseguire l'override usando la variabile di ambiente NUGET_PACKAGES, [le impostazioni di configurazione](../reference/nuget-config-file.md#config-section) `globalPackagesFolder` o `repositoryPath` (rispettivamente quando si usa PackageReference e `packages.config`) o la proprietà MSBuild `RestorePackagesPath` (solo MSBuild).</span><span class="sxs-lookup"><span data-stu-id="7c83a-114">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="7c83a-115">La variabile di ambiente ha la precedenza rispetto all'impostazione di configurazione.</span><span class="sxs-lookup"><span data-stu-id="7c83a-115">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="7c83a-116">http&#8209;cache</span><span class="sxs-lookup"><span data-stu-id="7c83a-116">http&#8209;cache</span></span> | <span data-ttu-id="7c83a-117">Gestione pacchetti di Visual Studio (NuGet 3.x+) e lo strumento `dotnet` archiviano copie dei pacchetti scaricati nella cache (salvati come file `.dat`), organizzati in sottocartelle per ogni origine di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="7c83a-117">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="7c83a-118">I pacchetti non vengono espansi e la cache ha una scadenza di 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="7c83a-118">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="7c83a-119">Windows: `%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="7c83a-119">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="7c83a-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="7c83a-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="7c83a-121">Eseguire l'override usando la variabile di ambiente NUGET_HTTP_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="7c83a-121">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="7c83a-122">temp</span><span class="sxs-lookup"><span data-stu-id="7c83a-122">temp</span></span> | <span data-ttu-id="7c83a-123">Cartella in cui NuGet archivia i file temporanei durante le varie operazioni.</span><span class="sxs-lookup"><span data-stu-id="7c83a-123">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="7c83a-124">Windows: `%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="7c83a-124">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="7c83a-125">Mac/Linux: `/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="7c83a-125">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |
| <span data-ttu-id="7c83a-126">plugins-cache **4.8+**</span><span class="sxs-lookup"><span data-stu-id="7c83a-126">plugins-cache **4.8+**</span></span> | <span data-ttu-id="7c83a-127">Cartella in cui NuGet archivia i risultati dalla richiesta di attestazioni delle operazioni.</span><span class="sxs-lookup"><span data-stu-id="7c83a-127">A folder where NuGet stores the results from the operation claims request.</span></span><br/><ul><li><span data-ttu-id="7c83a-128">Windows: `%localappdata%\NuGet\plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="7c83a-128">Windows: `%localappdata%\NuGet\plugins-cache`</span></span></li><li><span data-ttu-id="7c83a-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="7c83a-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span></span></li><li><span data-ttu-id="7c83a-130">Eseguire l'override usando la variabile di ambiente NUGET_PLUGINS_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="7c83a-130">Override using the NUGET_PLUGINS_CACHE_PATH environment variable.</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="7c83a-131">NuGet 3.5 e versioni precedenti usano la cartella *packages-cache* invece di *http-cache*, che si trova in `%localappdata%\NuGet\Cache`.</span><span class="sxs-lookup"><span data-stu-id="7c83a-131">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="7c83a-132">Tramite le cartelle della cache e *global-packages*, NuGet evita in genere il download di pacchetti già esistenti nel computer, con conseguente miglioramento delle prestazioni di installazione, aggiornamento e ripristino.</span><span class="sxs-lookup"><span data-stu-id="7c83a-132">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="7c83a-133">Quando si usa PackageReference, la cartella *global-packages* consente anche di evitare di mantenere i pacchetti scaricati all'interno delle cartelle di progetto, da cui potrebbero essere inavvertitamente aggiunti al controllo del codice sorgente, nonché di ridurre l'impatto complessivo di NuGet sullo spazio di archiviazione del computer.</span><span class="sxs-lookup"><span data-stu-id="7c83a-133">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="7c83a-134">Quando viene richiesto di recuperare un pacchetto, NuGet controlla prima di tutto nella cartella *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="7c83a-134">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="7c83a-135">Se nella cartella non è disponibile la versione esatta del pacchetto, NuGet controlla tutte le origini di pacchetti non HTTP.</span><span class="sxs-lookup"><span data-stu-id="7c83a-135">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="7c83a-136">Se il pacchetto non viene trovato, NuGet cerca il pacchetto nella cartella *http-cache* a meno che non si specifichi `--no-cache` con i comandi `dotnet.exe` o `-NoCache` con i comandi `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="7c83a-136">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="7c83a-137">Se il pacchetto non è presente nella cache o la cache non viene usata, NuGet recupera il pacchetto tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="7c83a-137">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="7c83a-138">Per altre informazioni, vedere [Cosa accade quando viene installato un pacchetto](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).</span><span class="sxs-lookup"><span data-stu-id="7c83a-138">For more information, see [What happens when a package is installed](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="7c83a-139">Visualizzazione delle posizioni delle cartelle</span><span class="sxs-lookup"><span data-stu-id="7c83a-139">Viewing folder locations</span></span>

<span data-ttu-id="7c83a-140">È possibile visualizzare le posizioni con il [comando nuget locals](../tools/cli-ref-locals.md):</span><span class="sxs-lookup"><span data-stu-id="7c83a-140">You can view locations using the [nuget locals command](../tools/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

<span data-ttu-id="7c83a-141">Output tipico (Windows; "user1" è il nome utente corrente):</span><span class="sxs-lookup"><span data-stu-id="7c83a-141">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

<span data-ttu-id="7c83a-142">(la cartella `package-cache` viene usata in NuGet 2.x e visualizzata con NuGet 3.5 e versioni precedenti.)</span><span class="sxs-lookup"><span data-stu-id="7c83a-142">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

<span data-ttu-id="7c83a-143">È anche possibile visualizzare le posizioni delle cartelle con il [comando dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals):</span><span class="sxs-lookup"><span data-stu-id="7c83a-143">You can also view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```cli
dotnet nuget locals all --list
```

<span data-ttu-id="7c83a-144">Output tipico (Mac/Linux; "user1" è il nome utente corrente):</span><span class="sxs-lookup"><span data-stu-id="7c83a-144">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

<span data-ttu-id="7c83a-145">Per visualizzare la posizione di una singola cartella, usare `http-cache`, `global-packages`, `temp` o `plugins-cache` invece di `all`.</span><span class="sxs-lookup"><span data-stu-id="7c83a-145">To display the location of a single folder, use `http-cache`, `global-packages`, `temp`, or `plugins-cache` instead of `all`.</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="7c83a-146">Cancellazione delle cartelle locali</span><span class="sxs-lookup"><span data-stu-id="7c83a-146">Clearing local folders</span></span>

<span data-ttu-id="7c83a-147">Se si verificano problemi di installazione dei pacchetti o si vuole essere certi di eseguire l'installazione dei pacchetti da una raccolta remota, usare l'opzione `locals --clear` (dotnet.exe) o `locals -clear` (nuget.exe), specificando la cartella da cancellare oppure `all` per cancellare tutte le cartelle:</span><span class="sxs-lookup"><span data-stu-id="7c83a-147">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

<span data-ttu-id="7c83a-148">Gli eventuali pacchetti usati dai progetti aperti in Visual Studio non vengono cancellati dalla cartella *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="7c83a-148">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="7c83a-149">In Visual Studio 2017 usare il comando di menu **Strumenti > Gestione pacchetti NuGet > Impostazioni di Gestione pacchetti** e quindi selezionare **Cancella tutte le cache NuGet**.</span><span class="sxs-lookup"><span data-stu-id="7c83a-149">In Visual Studio 2017, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="7c83a-150">La gestione delle cache non è attualmente disponibile tramite la console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="7c83a-150">Managing the cache isn't presently available through the Package Manager Console.</span></span> <span data-ttu-id="7c83a-151">In Visual Studio 2015 usare invece i comandi dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="7c83a-151">In Visual Studio 2015, use the CLI commands instead.</span></span>

![Comando NuGet per la cancellazione delle cache](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="7c83a-153">Risoluzione degli errori</span><span class="sxs-lookup"><span data-stu-id="7c83a-153">Troubleshooting errors</span></span>

<span data-ttu-id="7c83a-154">Durante l'uso di `nuget locals` o `dotnet nuget locals` possono verificarsi gli errori seguenti:</span><span class="sxs-lookup"><span data-stu-id="7c83a-154">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="7c83a-155">*Errore: Impossibile accedere al file <package> perché utilizzato da un altro processo* o *La cancellazione delle risorse locali non è riuscita. Non è possibile eliminare uno o più file*</span><span class="sxs-lookup"><span data-stu-id="7c83a-155">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="7c83a-156">Uno o più file nella cartella sono in uso da un altro processo. Ad esempio, è aperto un progetto di Visual Studio che fa riferimento ai pacchetti nella cartella *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="7c83a-156">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="7c83a-157">Chiudere i processi e riprovare.</span><span class="sxs-lookup"><span data-stu-id="7c83a-157">Close those processes and try again.</span></span>

- <span data-ttu-id="7c83a-158">*Errore: Accesso al percorso <path> negato* o *La directory non è vuota*</span><span class="sxs-lookup"><span data-stu-id="7c83a-158">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="7c83a-159">Non si è autorizzati a eliminare i file nella cache.</span><span class="sxs-lookup"><span data-stu-id="7c83a-159">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="7c83a-160">Modificare le autorizzazioni della cartella, se possibile, e riprovare.</span><span class="sxs-lookup"><span data-stu-id="7c83a-160">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="7c83a-161">In caso contrario, contattare l'amministratore di sistema.</span><span class="sxs-lookup"><span data-stu-id="7c83a-161">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="7c83a-162">*Errore: Percorso e/o nome di file specificato troppo lungo. Il nome di file completo deve contenere meno di 260 caratteri, mentre il nome di directory deve contenere meno di 248 caratteri.*</span><span class="sxs-lookup"><span data-stu-id="7c83a-162">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="7c83a-163">Abbreviare i nomi delle cartelle e riprovare.</span><span class="sxs-lookup"><span data-stu-id="7c83a-163">Shorten the folder names and try again.</span></span>
