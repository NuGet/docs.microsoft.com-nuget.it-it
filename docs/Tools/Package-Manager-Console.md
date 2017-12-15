---
title: Guida alla Console di gestione pacchetti NuGet | Documenti Microsoft
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2b92b119-6861-406c-82af-9d739af230e4
description: Istruzioni per l'utilizzo della Console di gestione pacchetti NuGet in Visual Studio per l'utilizzo di pacchetti.
keywords: NuGet package manager console powershell di NuGet, gestire i pacchetti NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d9df514c6f92a3ea0841503d86c44271e70f95f2
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="package-manager-console"></a><span data-ttu-id="262ab-104">Console di gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="262ab-104">Package Manager Console</span></span>

<span data-ttu-id="262ab-105">La Console di gestione pacchetti NuGet viene compilata in Visual Studio in Windows 2012 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="262ab-105">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="262ab-106">(Non è incluso in Visual Studio per Mac o codice di Visual Studio.)</span><span class="sxs-lookup"><span data-stu-id="262ab-106">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="262ab-107">La console consente di utilizzare [comandi PowerShell di NuGet](../tools/powershell-reference.md) per trovare, installare, disinstallare e aggiornare i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="262ab-107">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="262ab-108">Utilizzando la console è necessario nei casi in cui la UI Package Manager non fornisce un modo per eseguire un'operazione.</span><span class="sxs-lookup"><span data-stu-id="262ab-108">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span>

<span data-ttu-id="262ab-109">Ricerca e l'installazione di un pacchetto, ad esempio, viene eseguita con tre semplici passaggi:</span><span class="sxs-lookup"><span data-stu-id="262ab-109">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="262ab-110">Aprire il progetto/soluzione in Visual Studio e aprire la console usando il **strumenti > Gestione pacchetti NuGet > Console di gestione pacchetti** comando.</span><span class="sxs-lookup"><span data-stu-id="262ab-110">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="262ab-111">Trovare il pacchetto che si desidera installare.</span><span class="sxs-lookup"><span data-stu-id="262ab-111">Find the package you want to install.</span></span> <span data-ttu-id="262ab-112">Se si conosce già questo, andare al passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="262ab-112">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="262ab-113">Eseguire il comando di installazione:</span><span class="sxs-lookup"><span data-stu-id="262ab-113">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

<span data-ttu-id="262ab-114">Contenuto dell'argomento:</span><span class="sxs-lookup"><span data-stu-id="262ab-114">In this topic:</span></span>

- [<span data-ttu-id="262ab-115">Aprire la console di</span><span class="sxs-lookup"><span data-stu-id="262ab-115">Opening the console</span></span>](#opening-the-console-and-console-controls)
- [<span data-ttu-id="262ab-116">Installa un pacchetto</span><span class="sxs-lookup"><span data-stu-id="262ab-116">Installing a package</span></span>](#installing-a-package)
- [<span data-ttu-id="262ab-117">La disinstallazione di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="262ab-117">Uninstalling a package</span></span>](#uninstalling-a-package)
- [<span data-ttu-id="262ab-118">Ricerca di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="262ab-118">Finding a package</span></span>](#finding-a-package)
- [<span data-ttu-id="262ab-119">Aggiornamento di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="262ab-119">Updating a package</span></span>](#updating-a-package)
- [<span data-ttu-id="262ab-120">Disponibilità della console di</span><span class="sxs-lookup"><span data-stu-id="262ab-120">Availability of the console</span></span>](#availability-of-the-console)
- [<span data-ttu-id="262ab-121">Estendere la Console di gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="262ab-121">Extending the Package Manager Console</span></span>](#extending-the-package-manager-console)
- [<span data-ttu-id="262ab-122">Impostazione di un profilo di PowerShell di NuGet</span><span class="sxs-lookup"><span data-stu-id="262ab-122">Setting up a NuGet PowerShell profile</span></span>](#setting-up-a-nuget-powershell-profile)

> [!Important]
> <span data-ttu-id="262ab-123">Tutte le operazioni che sono disponibili nella console possono essere eseguite anche con il [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="262ab-123">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="262ab-124">Tuttavia, i comandi della console operano all'interno del contesto di Visual Studio e una progetto/soluzione salvata e spesso eseguire più i comandi CLI equivalenti.</span><span class="sxs-lookup"><span data-stu-id="262ab-124">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="262ab-125">Ad esempio, l'installazione di un pacchetto tramite la console aggiunge un riferimento al progetto mentre il comando CLI non.</span><span class="sxs-lookup"><span data-stu-id="262ab-125">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="262ab-126">Per questo motivo, gli sviluppatori che lavorano in Visual Studio, in genere preferiscono utilizzando la console per l'interfaccia CLI.</span><span class="sxs-lookup"><span data-stu-id="262ab-126">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="262ab-127">Molte operazioni di console dipendono dalla presenza di una soluzione aperta in Visual Studio con un nome di percorso noto.</span><span class="sxs-lookup"><span data-stu-id="262ab-127">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="262ab-128">Se si dispone di una soluzione non salvata o alcuna soluzione, è possibile visualizzare l'errore, "soluzione non aperta o non salvata.</span><span class="sxs-lookup"><span data-stu-id="262ab-128">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="262ab-129">Assicurarsi che disporre di una soluzione aperta e salvata."</span><span class="sxs-lookup"><span data-stu-id="262ab-129">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="262ab-130">Indica che la console non è possibile determinare la cartella della soluzione.</span><span class="sxs-lookup"><span data-stu-id="262ab-130">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="262ab-131">Salvataggio di una soluzione non salvata, o la creazione e il salvataggio di una soluzione se non si dispone di uno aprire, deve correggere l'errore.</span><span class="sxs-lookup"><span data-stu-id="262ab-131">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="262ab-132">Apertura della console e i controlli di console</span><span class="sxs-lookup"><span data-stu-id="262ab-132">Opening the console and console controls</span></span>

1. <span data-ttu-id="262ab-133">Aprire la console in Visual Studio usando il **strumenti > Gestione pacchetti NuGet > Console di gestione pacchetti** comando.</span><span class="sxs-lookup"><span data-stu-id="262ab-133">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="262ab-134">La console è una finestra di Visual Studio che può essere disposti e posizionata, tuttavia si desidera (vedere [personalizzare i layout delle finestre in Visual Studio](https://docs.microsoft.com/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="262ab-134">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](https://docs.microsoft.com/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="262ab-135">Per impostazione predefinita, i comandi della console funzionano in un'origine pacchetto specifico e un progetto di cui il controllo nella parte superiore della finestra:</span><span class="sxs-lookup"><span data-stu-id="262ab-135">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Controlli di Console di gestione pacchetti per l'origine del pacchetto e progetto](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="262ab-137">La selezione di un'origine pacchetto diverso e/o il progetto modifica tali impostazioni predefinite per i comandi successivi.</span><span class="sxs-lookup"><span data-stu-id="262ab-137">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="262ab-138">La maggior parte dei comandi per esegue l'override queste impostazioni senza modificare le impostazioni predefinite, supportano `-Source` e `-ProjectName` opzioni.</span><span class="sxs-lookup"><span data-stu-id="262ab-138">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="262ab-139">Per gestire l'origine del pacchetto, selezionare l'icona dell'ingranaggio.</span><span class="sxs-lookup"><span data-stu-id="262ab-139">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="262ab-140">Si tratta di un collegamento per il **strumenti > Opzioni > Gestione pacchetti NuGet > origini pacchetti** come descritto nella finestra di dialogo di [UI Package Manager](Package-Manager-UI.md#package-sources) pagina.</span><span class="sxs-lookup"><span data-stu-id="262ab-140">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](Package-Manager-UI.md#package-sources) page.</span></span> <span data-ttu-id="262ab-141">Inoltre, il controllo a destra del selettore di progetto Cancella il contenuto della console:</span><span class="sxs-lookup"><span data-stu-id="262ab-141">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Impostazioni della Console di gestione pacchetti e deselezionare i controlli](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="262ab-143">Pulsante a destra consente di interrompere un comando a esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="262ab-143">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="262ab-144">Ad esempio, in esecuzione `Get-Package -ListAvailable -PageSize 500` Elenca i pacchetti superiore a 500 nell'origine predefinita (ad esempio nuget.org), che potrebbe richiedere alcuni minuti per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="262ab-144">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Controllo di arresto di Console di gestione pacchetti](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="262ab-146">Installa un pacchetto</span><span class="sxs-lookup"><span data-stu-id="262ab-146">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="262ab-147">Vedere [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="262ab-147">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="262ab-148">Installa un pacchetto esegue le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="262ab-148">Installing a package performs the following actions:</span></span>

- <span data-ttu-id="262ab-149">Visualizza condizioni di licenza applicabili nella finestra della console con un contratto implicito.</span><span class="sxs-lookup"><span data-stu-id="262ab-149">Displays applicable license terms in the console window with implied agreement.</span></span> <span data-ttu-id="262ab-150">Se non si accettano le condizioni, è necessario disinstallare il pacchetto immediatamente.</span><span class="sxs-lookup"><span data-stu-id="262ab-150">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="262ab-151">Aggiunge un riferimento al progetto in qualsiasi formato di riferimento è in uso.</span><span class="sxs-lookup"><span data-stu-id="262ab-151">Adds a reference to the project in whatever reference format is in use.</span></span> <span data-ttu-id="262ab-152">In Esplora soluzioni e il file di formato di riferimento applicabili sono presenti riferimenti successivamente.</span><span class="sxs-lookup"><span data-stu-id="262ab-152">References subsequently appear in Solution Explorer and the applicable reference format file.</span></span> <span data-ttu-id="262ab-153">Si noti, tuttavia, con PackageReference, è necessario salvare il progetto per visualizzare le modifiche nel file di progetto direttamente.</span><span class="sxs-lookup"><span data-stu-id="262ab-153">Note, however, that with PackageReference, you need to save the project to see the changes in the project file directly.</span></span>
- <span data-ttu-id="262ab-154">Memorizza nella cache il pacchetto:</span><span class="sxs-lookup"><span data-stu-id="262ab-154">Caches the package:</span></span>
    - <span data-ttu-id="262ab-155">PackageReference: pacchetto memorizzato nella cache `%USERPROFILE%\.nuget\packages` e il blocco di file, ovvero `project.assets.json` viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="262ab-155">PackageReference:  package is cached at `%USERPROFILE%\.nuget\packages` and the lock file i.e. `project.assets.json` is updated.</span></span>
    - <span data-ttu-id="262ab-156">`packages.config`: crea un `packages` cartella radice della soluzione e copia il pacchetto di file in una sottocartella all'interno di esso.</span><span class="sxs-lookup"><span data-stu-id="262ab-156">`packages.config`: creates a `packages` folder at the solution root and copies the package files into a subfolder within it.</span></span> <span data-ttu-id="262ab-157">Il `package.config` file viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="262ab-157">The `package.config` file is updated.</span></span>
- <span data-ttu-id="262ab-158">Aggiornamenti `app.config` e/o `web.config` se il pacchetto utilizza [trasformazioni di file di origine e configurazione](../create-packages/source-and-config-file-transformations.md).</span><span class="sxs-lookup"><span data-stu-id="262ab-158">Updates `app.config` and/or `web.config` if the package uses [source and config file transformations](../create-packages/source-and-config-file-transformations.md).</span></span>
- <span data-ttu-id="262ab-159">Installa tutte le dipendenze, se non è già presente nel progetto.</span><span class="sxs-lookup"><span data-stu-id="262ab-159">Installs any dependencies if not already present in the project.</span></span> <span data-ttu-id="262ab-160">Questo potrebbe aggiornare versioni del pacchetto del processo, come descritto in [la risoluzione delle dipendenze](../consume-packages/dependency-resolution.md).</span><span class="sxs-lookup"><span data-stu-id="262ab-160">This might update package versions in the process, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span>
- <span data-ttu-id="262ab-161">Visualizza file readme del pacchetto, se disponibile, in una finestra di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="262ab-161">Displays the package's readme file, if available, in a Visual Studio window.</span></span>

> [!Tip]
> <span data-ttu-id="262ab-162">Uno dei principali vantaggi dell'installazione di pacchetti con il `Install-Package` nella console di comando è come se è stata utilizzata la UI Package Manager, che aggiunge un riferimento al progetto.</span><span class="sxs-lookup"><span data-stu-id="262ab-162">One of the primary advantages of installing packages with the `Install-Package` command in the console is that adds a reference to the project just as if you used the Package Manager UI.</span></span> <span data-ttu-id="262ab-163">Al contrario, il `nuget install` comando CLI di solo download del pacchetto e non aggiunge automaticamente un riferimento.</span><span class="sxs-lookup"><span data-stu-id="262ab-163">In contrast, the `nuget install` CLI command only downloads the package and does not automatically add a reference.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="262ab-164">La disinstallazione di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="262ab-164">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="262ab-165">Vedere [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="262ab-165">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="262ab-166">Utilizzare [Get-Package](../tools/ps-ref-get-package.md) per visualizzare tutti i pacchetti installati nel progetto predefinito se è necessario trovare un identificatore.</span><span class="sxs-lookup"><span data-stu-id="262ab-166">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="262ab-167">La disinstallazione di un pacchetto esegue le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="262ab-167">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="262ab-168">Rimuove i riferimenti al pacchetto dal progetto (e qualsiasi formato di riferimento è in uso).</span><span class="sxs-lookup"><span data-stu-id="262ab-168">Removes references to the package from the project (and whatever reference format is in use).</span></span> <span data-ttu-id="262ab-169">Non sono presenti riferimenti in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="262ab-169">References no longer appear in Solution Explorer.</span></span> <span data-ttu-id="262ab-170">(Potrebbe essere necessario ricompilare il progetto per visualizzarlo rimossa la **Bin** cartella.)</span><span class="sxs-lookup"><span data-stu-id="262ab-170">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="262ab-171">Inverte le modifiche apportate al `app.config` o `web.config` quando il pacchetto è stato installato.</span><span class="sxs-lookup"><span data-stu-id="262ab-171">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="262ab-172">Dipendenze rimuove installato in precedenza, se i pacchetti rimanenti non utilizzano tali dipendenze.</span><span class="sxs-lookup"><span data-stu-id="262ab-172">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

> [!Tip]
> <span data-ttu-id="262ab-173">Ad esempio `Install-Package`, il `Uninstall-Package` comando ha il vantaggio di gestione dei riferimenti nel progetto, a differenza di `nuget uninstall` comando CLI.</span><span class="sxs-lookup"><span data-stu-id="262ab-173">Like `Install-Package`, the `Uninstall-Package` command has the benefit of managing references in the project, unlike the `nuget uninstall` CLI command.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="262ab-174">Aggiornamento di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="262ab-174">Updating a package</span></span>

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

<span data-ttu-id="262ab-175">Vedere [Get-Package](../tools/ps-ref-get-package.md) e [pacchetto di aggiornamento](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="262ab-175">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="262ab-176">Ricerca di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="262ab-176">Finding a package</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

<span data-ttu-id="262ab-177">Vedere [Find-Package](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="262ab-177">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="262ab-178">In Visual Studio 2013 e versioni precedenti, utilizzare [Get-Package](../tools/ps-ref-get-package.md) invece.</span><span class="sxs-lookup"><span data-stu-id="262ab-178">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="262ab-179">Disponibilità della console di</span><span class="sxs-lookup"><span data-stu-id="262ab-179">Availability of the console</span></span>

<span data-ttu-id="262ab-180">In Visual Studio 2017, NuGet e gestione pacchetti NuGet vengono installati automaticamente quando si seleziona uno. Carichi di lavoro correlati alla rete; è possibile anche installare singolarmente controllando il **singoli componenti > codice strumenti > Gestione pacchetti NuGet** opzione nel programma di installazione di Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="262ab-180">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="262ab-181">Inoltre, assenza Gestione pacchetti NuGet in Visual Studio 2015 e versioni precedenti, controllare **strumenti > estensioni e aggiornamenti...**  e cercare l'estensione Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="262ab-181">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="262ab-182">Se non si riesce a usare il programma di installazione di estensioni in Visual Studio, è possibile scaricare l'estensione direttamente da [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="262ab-182">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="262ab-183">La Console di gestione pacchetti non è attualmente disponibile in Visual Studio per Mac.</span><span class="sxs-lookup"><span data-stu-id="262ab-183">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="262ab-184">I comandi equivalenti, tuttavia, sono disponibili tramite il [NuGet CLI](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="262ab-184">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="262ab-185">Visual Studio per Mac hanno un'interfaccia utente per la gestione dei pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="262ab-185">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="262ab-186">Vedere [pacchetto NuGet un inclusi nel progetto](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="262ab-186">See [Including a NuGet package in your project](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="262ab-187">Console di gestione pacchetti non è inclusa in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="262ab-187">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="262ab-188">Estendere la Console di gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="262ab-188">Extending the Package Manager Console</span></span>

<span data-ttu-id="262ab-189">Alcuni pacchetti installare nuovi comandi per la console.</span><span class="sxs-lookup"><span data-stu-id="262ab-189">Some packages install new commands for the console.</span></span> <span data-ttu-id="262ab-190">Ad esempio, `MvcScaffolding` crea comandi come `Scaffold` illustrato di seguito, che genera l'errore ASP.NET MVC controller e visualizzazioni:</span><span class="sxs-lookup"><span data-stu-id="262ab-190">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Installazione e utilizzo MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="262ab-192">Impostazione di un profilo di PowerShell di NuGet</span><span class="sxs-lookup"><span data-stu-id="262ab-192">Setting up a NuGet PowerShell Profile</span></span>

<span data-ttu-id="262ab-193">Un profilo di PowerShell consente di rendere disponibili i comandi di uso comune, ogni volta che è possibile usare PowerShell.</span><span class="sxs-lookup"><span data-stu-id="262ab-193">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="262ab-194">NuGet supporta un profilo specifico di NuGet in genere disponibile nel percorso seguente:</span><span class="sxs-lookup"><span data-stu-id="262ab-194">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

```
%UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="262ab-195">Per trovare il profilo, digitare `$profile` nella console:</span><span class="sxs-lookup"><span data-stu-id="262ab-195">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="262ab-196">Per ulteriori informazioni, vedere [profili di Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="262ab-196">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>
