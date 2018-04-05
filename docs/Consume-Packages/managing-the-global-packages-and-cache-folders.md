---
title: Come gestire le cartelle dei pacchetti globale, della cache e temporanea in NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Come gestire la cartella di installazione dei pacchetti globale, la cartella della cache dei pacchetti e la cartella temporanea esistenti in un computer, usate durante l'installazione, il ripristino e l'aggiornamento dei pacchetti.
keywords: cartella dei pacchetti globale NuGet, cache dei pacchetti NuGet, memorizzazione nella cache dei pacchetti, cartella di installazione dei pacchetti, cache NuGet, gestione delle cache, cache NuGet locale, cache NuGet globale, comando locals NuGet, cancellazione di una cache
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e9f4383a3f1700b96e3d6fe9ea4c0a7c24daa45a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="588de-104">Gestione delle cartelle dei pacchetti globale, della cache e temporanea</span><span class="sxs-lookup"><span data-stu-id="588de-104">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="588de-105">Quando si installa, aggiorna o ripristina un pacchetto, NuGet gestisce i pacchetti e le informazioni sui pacchetti in varie cartelle all'esterno della struttura del progetto:</span><span class="sxs-lookup"><span data-stu-id="588de-105">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="588de-106">Nome</span><span class="sxs-lookup"><span data-stu-id="588de-106">Name</span></span> | <span data-ttu-id="588de-107">Descrizione e posizione (per utente)</span><span class="sxs-lookup"><span data-stu-id="588de-107">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="588de-108">global&#8209;packages</span><span class="sxs-lookup"><span data-stu-id="588de-108">global&#8209;packages</span></span> | <span data-ttu-id="588de-109">La cartella *global-packages* è la posizione in cui NuGet installa i pacchetti scaricati.</span><span class="sxs-lookup"><span data-stu-id="588de-109">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="588de-110">Ogni pacchetto viene espanso completamente in una sottocartella corrispondente all'identificatore del pacchetto e al numero di versione.</span><span class="sxs-lookup"><span data-stu-id="588de-110">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="588de-111">I progetti che usano il formato PackageReference usano sempre i pacchetti direttamente da questa cartella.</span><span class="sxs-lookup"><span data-stu-id="588de-111">Projects using the PackageReference format always use packages directly from this folder.</span></span> <span data-ttu-id="588de-112">Quando si usa il file `packages.config`, i pacchetti vengono installati nella cartella *global-packages* e quindi copiati nella cartella `packages` del progetto.</span><span class="sxs-lookup"><span data-stu-id="588de-112">When using the `packages.config`, packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="588de-113">Windows: `%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="588de-113">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="588de-114">Mac/Linux: `~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="588de-114">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="588de-115">Eseguire l'override usando la variabile di ambiente NUGET_PACKAGES, [le impostazioni di configurazione](../reference/nuget-config-file.md#config-section) `globalPackagesFolder` o `repositoryPath` (rispettivamente quando si usa PackageReference e `packages.config`) o la proprietà MSBuild `RestorePackagesPath` (solo MSBuild).</span><span class="sxs-lookup"><span data-stu-id="588de-115">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="588de-116">La variabile di ambiente ha la precedenza rispetto all'impostazione di configurazione.</span><span class="sxs-lookup"><span data-stu-id="588de-116">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="588de-117">http&#8209;cache</span><span class="sxs-lookup"><span data-stu-id="588de-117">http&#8209;cache</span></span> | <span data-ttu-id="588de-118">Gestione pacchetti di Visual Studio (NuGet 3.x+) e lo strumento `dotnet` archiviano copie dei pacchetti scaricati nella cache (salvati come file `.dat`), organizzati in sottocartelle per ogni origine di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="588de-118">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="588de-119">I pacchetti non vengono espansi e la cache ha una scadenza di 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="588de-119">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="588de-120">Windows: `%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="588de-120">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="588de-121">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="588de-121">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="588de-122">Eseguire l'override usando la variabile di ambiente NUGET_HTTP_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="588de-122">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="588de-123">temp</span><span class="sxs-lookup"><span data-stu-id="588de-123">temp</span></span> | <span data-ttu-id="588de-124">Cartella in cui NuGet archivia i file temporanei durante le varie operazioni.</span><span class="sxs-lookup"><span data-stu-id="588de-124">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="588de-125">Windows: `%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="588de-125">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="588de-126">Mac/Linux: `/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="588de-126">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="588de-127">NuGet 3.5 e versioni precedenti usano la cartella *packages-cache* invece di *http-cache*, che si trova in `%localappdata%\NuGet\Cache`.</span><span class="sxs-lookup"><span data-stu-id="588de-127">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="588de-128">Tramite le cartelle della cache e *global-packages*, NuGet evita in genere il download di pacchetti già esistenti nel computer, con conseguente miglioramento delle prestazioni di installazione, aggiornamento e ripristino.</span><span class="sxs-lookup"><span data-stu-id="588de-128">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="588de-129">Quando si usa PackageReference, la cartella *global-packages* consente anche di evitare di mantenere i pacchetti scaricati all'interno delle cartelle di progetto, da cui potrebbero essere inavvertitamente aggiunti al controllo del codice sorgente, nonché di ridurre l'impatto complessivo di NuGet sullo spazio di archiviazione del computer.</span><span class="sxs-lookup"><span data-stu-id="588de-129">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="588de-130">Quando viene richiesto di recuperare un pacchetto, NuGet controlla prima di tutto nella cartella *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="588de-130">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="588de-131">Se nella cartella non è disponibile la versione esatta del pacchetto, NuGet controlla tutte le origini di pacchetti non HTTP.</span><span class="sxs-lookup"><span data-stu-id="588de-131">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="588de-132">Se il pacchetto non viene trovato, NuGet cerca il pacchetto nella cartella *http-cache* a meno che non si specifichi `--no-cache` con i comandi `dotnet.exe` o `-NoCache` con i comandi `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="588de-132">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="588de-133">Se il pacchetto non è presente nella cache o la cache non viene usata, NuGet recupera il pacchetto tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="588de-133">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="588de-134">Per altre informazioni, vedere [Cosa accade quando viene installato un pacchetto](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).</span><span class="sxs-lookup"><span data-stu-id="588de-134">For more information, see [What happens when a package is installed](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="588de-135">Visualizzazione delle posizioni delle cartelle</span><span class="sxs-lookup"><span data-stu-id="588de-135">Viewing folder locations</span></span>

<span data-ttu-id="588de-136">Per visualizzare le posizioni delle cartelle, è possibile usare il [comando dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals):</span><span class="sxs-lookup"><span data-stu-id="588de-136">You can view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```cli
dotnet nuget locals all --list
```

<span data-ttu-id="588de-137">Output tipico (Mac/Linux; "user1" è il nome utente corrente):</span><span class="sxs-lookup"><span data-stu-id="588de-137">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
```

<span data-ttu-id="588de-138">Per visualizzare la posizione di una singola cartella, usare `http-cache`, `global-packages` o `temp` invece di `all`.</span><span class="sxs-lookup"><span data-stu-id="588de-138">To display the location of a single folder, use `http-cache`, `global-packages`, or `temp` instead of `all`.</span></span> 

<span data-ttu-id="588de-139">È anche possibile visualizzare le posizioni con il [comando nuget locals](../tools/cli-ref-locals.md):</span><span class="sxs-lookup"><span data-stu-id="588de-139">You also view locations using the [nuget locals command](../tools/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, cache, and temp
nuget locals all -list
```

<span data-ttu-id="588de-140">Output tipico (Windows; "user1" è il nome utente corrente):</span><span class="sxs-lookup"><span data-stu-id="588de-140">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
```

<span data-ttu-id="588de-141">(la cartella `package-cache` viene usata in NuGet 2.x e visualizzata con NuGet 3.5 e versioni precedenti.)</span><span class="sxs-lookup"><span data-stu-id="588de-141">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="588de-142">Cancellazione delle cartelle locali</span><span class="sxs-lookup"><span data-stu-id="588de-142">Clearing local folders</span></span>

<span data-ttu-id="588de-143">Se si verificano problemi di installazione dei pacchetti o si vuole essere certi di eseguire l'installazione dei pacchetti da una raccolta remota, usare l'opzione `locals --clear` (dotnet.exe) o `locals -clear` (nuget.exe), specificando la cartella da cancellare oppure `all` per cancellare tutte le cartelle:</span><span class="sxs-lookup"><span data-stu-id="588de-143">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

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

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

<span data-ttu-id="588de-144">Gli eventuali pacchetti usati dai progetti aperti in Visual Studio non vengono cancellati dalla cartella *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="588de-144">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="588de-145">In Visual Studio, usare il comando di menu **Strumenti > Gestione pacchetti NuGet > Impostazioni di Gestione pacchetti** e quindi selezionare **Cancella tutte le cache NuGet**.</span><span class="sxs-lookup"><span data-stu-id="588de-145">In Visual Studio, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="588de-146">La gestione delle cache non è attualmente disponibile tramite la console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="588de-146">Managing the cache isn't presently available through the Package Manager Console.</span></span>

![Comando NuGet per la cancellazione delle cache](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="588de-148">Risoluzione degli errori</span><span class="sxs-lookup"><span data-stu-id="588de-148">Troubleshooting errors</span></span>

<span data-ttu-id="588de-149">Durante l'uso di `nuget locals` o `dotnet nuget locals` possono verificarsi gli errori seguenti:</span><span class="sxs-lookup"><span data-stu-id="588de-149">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="588de-150">*Errore: Impossibile accedere al file <package> perché utilizzato da un altro processo* o *La cancellazione delle risorse locali non è riuscita. Non è possibile eliminare uno o più file*</span><span class="sxs-lookup"><span data-stu-id="588de-150">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="588de-151">Uno o più file nella cartella sono in uso da un altro processo. Ad esempio, è aperto un progetto di Visual Studio che fa riferimento ai pacchetti nella cartella *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="588de-151">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="588de-152">Chiudere i processi e riprovare.</span><span class="sxs-lookup"><span data-stu-id="588de-152">Close those processes and try again.</span></span>

- <span data-ttu-id="588de-153">*Errore: Accesso al percorso <path> negato* o *La directory non è vuota*</span><span class="sxs-lookup"><span data-stu-id="588de-153">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="588de-154">Non si è autorizzati a eliminare i file nella cache.</span><span class="sxs-lookup"><span data-stu-id="588de-154">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="588de-155">Modificare le autorizzazioni della cartella, se possibile, e riprovare.</span><span class="sxs-lookup"><span data-stu-id="588de-155">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="588de-156">In caso contrario, contattare l'amministratore di sistema.</span><span class="sxs-lookup"><span data-stu-id="588de-156">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="588de-157">*Errore: Percorso e/o nome di file specificato troppo lungo. Il nome di file completo deve contenere meno di 260 caratteri, mentre il nome di directory deve contenere meno di 248 caratteri.*</span><span class="sxs-lookup"><span data-stu-id="588de-157">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="588de-158">Abbreviare i nomi delle cartelle e riprovare.</span><span class="sxs-lookup"><span data-stu-id="588de-158">Shorten the folder names and try again.</span></span>
