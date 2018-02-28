---
title: Guida alla Console di gestione pacchetti NuGet | Documenti Microsoft
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
f1_keywords:
- vs.nuget.packagemanager.console
description: Istruzioni per l'utilizzo della Console di gestione pacchetti NuGet in Visual Studio per l'utilizzo di pacchetti.
keywords: NuGet package manager console powershell di NuGet, gestire i pacchetti NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 60c7edd0497e162cc511424e9acfbbfd6f53fd46
ms.sourcegitcommit: a40a6ce6897b2d9411397b2e29b1be234eb6e50c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/27/2018
---
# <a name="package-manager-console"></a><span data-ttu-id="1daf8-104">Console di Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="1daf8-104">Package Manager Console</span></span>

<span data-ttu-id="1daf8-105">La Console di gestione pacchetti NuGet viene compilata in Visual Studio in Windows 2012 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="1daf8-105">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="1daf8-106">(Non è incluso in Visual Studio per Mac o codice di Visual Studio.)</span><span class="sxs-lookup"><span data-stu-id="1daf8-106">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="1daf8-107">La console consente di utilizzare [comandi PowerShell di NuGet](../tools/powershell-reference.md) per trovare, installare, disinstallare e aggiornare i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="1daf8-107">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="1daf8-108">Utilizzando la console è necessario nei casi in cui la UI Package Manager non fornisce un modo per eseguire un'operazione.</span><span class="sxs-lookup"><span data-stu-id="1daf8-108">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="1daf8-109">Per utilizzare `nuget.exe` comandi nella console, vedere [utilizzando nuget.exe CLI nella console di](#using-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="1daf8-109">To use `nuget.exe` commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="1daf8-110">Ricerca e l'installazione di un pacchetto, ad esempio, viene eseguita con tre semplici passaggi:</span><span class="sxs-lookup"><span data-stu-id="1daf8-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="1daf8-111">Aprire il progetto/soluzione in Visual Studio e aprire la console usando il **strumenti > Gestione pacchetti NuGet > Console di gestione pacchetti** comando.</span><span class="sxs-lookup"><span data-stu-id="1daf8-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="1daf8-112">Trovare il pacchetto che si desidera installare.</span><span class="sxs-lookup"><span data-stu-id="1daf8-112">Find the package you want to install.</span></span> <span data-ttu-id="1daf8-113">Se si conosce già questo, andare al passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="1daf8-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="1daf8-114">Eseguire il comando di installazione:</span><span class="sxs-lookup"><span data-stu-id="1daf8-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="1daf8-115">Tutte le operazioni che sono disponibili nella console possono essere eseguite anche con il [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="1daf8-115">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="1daf8-116">Tuttavia, i comandi della console operano all'interno del contesto di Visual Studio e una progetto/soluzione salvata e spesso eseguire più i comandi CLI equivalenti.</span><span class="sxs-lookup"><span data-stu-id="1daf8-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="1daf8-117">Ad esempio, l'installazione di un pacchetto tramite la console aggiunge un riferimento al progetto mentre il comando CLI non.</span><span class="sxs-lookup"><span data-stu-id="1daf8-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="1daf8-118">Per questo motivo, gli sviluppatori che lavorano in Visual Studio, in genere preferiscono utilizzando la console per l'interfaccia CLI.</span><span class="sxs-lookup"><span data-stu-id="1daf8-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="1daf8-119">Molte operazioni di console dipendono dalla presenza di una soluzione aperta in Visual Studio con un nome di percorso noto.</span><span class="sxs-lookup"><span data-stu-id="1daf8-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="1daf8-120">Se si dispone di una soluzione non salvata o alcuna soluzione, è possibile visualizzare l'errore, "soluzione non aperta o non salvata.</span><span class="sxs-lookup"><span data-stu-id="1daf8-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="1daf8-121">Assicurarsi che disporre di una soluzione aperta e salvata."</span><span class="sxs-lookup"><span data-stu-id="1daf8-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="1daf8-122">Indica che la console non è possibile determinare la cartella della soluzione.</span><span class="sxs-lookup"><span data-stu-id="1daf8-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="1daf8-123">Salvataggio di una soluzione non salvata, o la creazione e il salvataggio di una soluzione se non si dispone di uno aprire, deve correggere l'errore.</span><span class="sxs-lookup"><span data-stu-id="1daf8-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="1daf8-124">Apertura della console e i controlli di console</span><span class="sxs-lookup"><span data-stu-id="1daf8-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="1daf8-125">Aprire la console in Visual Studio usando il **strumenti > Gestione pacchetti NuGet > Console di gestione pacchetti** comando.</span><span class="sxs-lookup"><span data-stu-id="1daf8-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="1daf8-126">La console è una finestra di Visual Studio che può essere disposti e posizionata, tuttavia si desidera (vedere [personalizzare i layout delle finestre in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="1daf8-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="1daf8-127">Per impostazione predefinita, i comandi della console funzionano in un'origine pacchetto specifico e un progetto di cui il controllo nella parte superiore della finestra:</span><span class="sxs-lookup"><span data-stu-id="1daf8-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Controlli di Console di gestione pacchetti per l'origine del pacchetto e progetto](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="1daf8-129">La selezione di un'origine pacchetto diverso e/o il progetto modifica tali impostazioni predefinite per i comandi successivi.</span><span class="sxs-lookup"><span data-stu-id="1daf8-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="1daf8-130">La maggior parte dei comandi per esegue l'override queste impostazioni senza modificare le impostazioni predefinite, supportano `-Source` e `-ProjectName` opzioni.</span><span class="sxs-lookup"><span data-stu-id="1daf8-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="1daf8-131">Per gestire l'origine del pacchetto, selezionare l'icona dell'ingranaggio.</span><span class="sxs-lookup"><span data-stu-id="1daf8-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="1daf8-132">Si tratta di un collegamento per il **strumenti > Opzioni > Gestione pacchetti NuGet > origini pacchetti** come descritto nella finestra di dialogo di [UI Package Manager](package-manager-ui.md#package-sources) pagina.</span><span class="sxs-lookup"><span data-stu-id="1daf8-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="1daf8-133">Inoltre, il controllo a destra del selettore di progetto Cancella il contenuto della console:</span><span class="sxs-lookup"><span data-stu-id="1daf8-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Impostazioni della Console di gestione pacchetti e deselezionare i controlli](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="1daf8-135">Pulsante a destra consente di interrompere un comando a esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="1daf8-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="1daf8-136">Ad esempio, in esecuzione `Get-Package -ListAvailable -PageSize 500` Elenca i pacchetti superiore a 500 nell'origine predefinita (ad esempio nuget.org), che potrebbe richiedere alcuni minuti per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1daf8-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Controllo di arresto di Console di gestione pacchetti](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="1daf8-138">Installa un pacchetto</span><span class="sxs-lookup"><span data-stu-id="1daf8-138">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="1daf8-139">Vedere [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="1daf8-139">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="1daf8-140">Installa un pacchetto esegue le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="1daf8-140">Installing a package performs the following actions:</span></span>

- <span data-ttu-id="1daf8-141">Visualizza condizioni di licenza applicabili nella finestra della console con un contratto implicito.</span><span class="sxs-lookup"><span data-stu-id="1daf8-141">Displays applicable license terms in the console window with implied agreement.</span></span> <span data-ttu-id="1daf8-142">Se non si accettano le condizioni, è necessario disinstallare il pacchetto immediatamente.</span><span class="sxs-lookup"><span data-stu-id="1daf8-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="1daf8-143">Aggiunge un riferimento al progetto in qualsiasi formato di riferimento è in uso.</span><span class="sxs-lookup"><span data-stu-id="1daf8-143">Adds a reference to the project in whatever reference format is in use.</span></span> <span data-ttu-id="1daf8-144">In Esplora soluzioni e il file di formato di riferimento applicabili sono presenti riferimenti successivamente.</span><span class="sxs-lookup"><span data-stu-id="1daf8-144">References subsequently appear in Solution Explorer and the applicable reference format file.</span></span> <span data-ttu-id="1daf8-145">Si noti, tuttavia, con PackageReference, è necessario salvare il progetto per visualizzare le modifiche nel file di progetto direttamente.</span><span class="sxs-lookup"><span data-stu-id="1daf8-145">Note, however, that with PackageReference, you need to save the project to see the changes in the project file directly.</span></span>
- <span data-ttu-id="1daf8-146">Memorizza nella cache il pacchetto:</span><span class="sxs-lookup"><span data-stu-id="1daf8-146">Caches the package:</span></span>
  - <span data-ttu-id="1daf8-147">PackageReference: pacchetto memorizzato nella cache `%USERPROFILE%\.nuget\packages` e il blocco di file, ovvero `project.assets.json` viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="1daf8-147">PackageReference:  package is cached at `%USERPROFILE%\.nuget\packages` and the lock file i.e. `project.assets.json` is updated.</span></span>
  - <span data-ttu-id="1daf8-148">`packages.config`: crea un `packages` cartella radice della soluzione e copia il pacchetto di file in una sottocartella all'interno di esso.</span><span class="sxs-lookup"><span data-stu-id="1daf8-148">`packages.config`: creates a `packages` folder at the solution root and copies the package files into a subfolder within it.</span></span> <span data-ttu-id="1daf8-149">Il `package.config` file viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="1daf8-149">The `package.config` file is updated.</span></span>
- <span data-ttu-id="1daf8-150">Aggiornamenti `app.config` e/o `web.config` se il pacchetto utilizza [trasformazioni di file di origine e configurazione](../create-packages/source-and-config-file-transformations.md).</span><span class="sxs-lookup"><span data-stu-id="1daf8-150">Updates `app.config` and/or `web.config` if the package uses [source and config file transformations](../create-packages/source-and-config-file-transformations.md).</span></span>
- <span data-ttu-id="1daf8-151">Installa tutte le dipendenze, se non è già presente nel progetto.</span><span class="sxs-lookup"><span data-stu-id="1daf8-151">Installs any dependencies if not already present in the project.</span></span> <span data-ttu-id="1daf8-152">Questo potrebbe aggiornare versioni del pacchetto del processo, come descritto in [la risoluzione delle dipendenze](../consume-packages/dependency-resolution.md).</span><span class="sxs-lookup"><span data-stu-id="1daf8-152">This might update package versions in the process, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span>
- <span data-ttu-id="1daf8-153">Visualizza file readme del pacchetto, se disponibile, in una finestra di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1daf8-153">Displays the package's readme file, if available, in a Visual Studio window.</span></span>

> [!Tip]
> <span data-ttu-id="1daf8-154">Uno dei principali vantaggi dell'installazione di pacchetti con il `Install-Package` nella console di comando è come se è stata utilizzata la UI Package Manager, che aggiunge un riferimento al progetto.</span><span class="sxs-lookup"><span data-stu-id="1daf8-154">One of the primary advantages of installing packages with the `Install-Package` command in the console is that adds a reference to the project just as if you used the Package Manager UI.</span></span> <span data-ttu-id="1daf8-155">Al contrario, il `nuget install` comando CLI di solo download del pacchetto e non aggiunge automaticamente un riferimento.</span><span class="sxs-lookup"><span data-stu-id="1daf8-155">In contrast, the `nuget install` CLI command only downloads the package and does not automatically add a reference.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="1daf8-156">La disinstallazione di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="1daf8-156">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="1daf8-157">Vedere [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="1daf8-157">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="1daf8-158">Utilizzare [Get-Package](../tools/ps-ref-get-package.md) per visualizzare tutti i pacchetti installati nel progetto predefinito se è necessario trovare un identificatore.</span><span class="sxs-lookup"><span data-stu-id="1daf8-158">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="1daf8-159">La disinstallazione di un pacchetto esegue le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="1daf8-159">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="1daf8-160">Rimuove i riferimenti al pacchetto dal progetto (e qualsiasi formato di riferimento è in uso).</span><span class="sxs-lookup"><span data-stu-id="1daf8-160">Removes references to the package from the project (and whatever reference format is in use).</span></span> <span data-ttu-id="1daf8-161">Non sono presenti riferimenti in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="1daf8-161">References no longer appear in Solution Explorer.</span></span> <span data-ttu-id="1daf8-162">(Potrebbe essere necessario ricompilare il progetto per visualizzarlo rimossa la **Bin** cartella.)</span><span class="sxs-lookup"><span data-stu-id="1daf8-162">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="1daf8-163">Inverte le modifiche apportate al `app.config` o `web.config` quando il pacchetto è stato installato.</span><span class="sxs-lookup"><span data-stu-id="1daf8-163">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="1daf8-164">Dipendenze rimuove installato in precedenza, se i pacchetti rimanenti non utilizzano tali dipendenze.</span><span class="sxs-lookup"><span data-stu-id="1daf8-164">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

> [!Tip]
> <span data-ttu-id="1daf8-165">Ad esempio `Install-Package`, il `Uninstall-Package` comando ha il vantaggio di gestione dei riferimenti nel progetto, a differenza di `nuget uninstall` comando CLI.</span><span class="sxs-lookup"><span data-stu-id="1daf8-165">Like `Install-Package`, the `Uninstall-Package` command has the benefit of managing references in the project, unlike the `nuget uninstall` CLI command.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="1daf8-166">Aggiornamento di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="1daf8-166">Updating a package</span></span>

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

<span data-ttu-id="1daf8-167">Vedere [Get-Package](../tools/ps-ref-get-package.md) e [pacchetto di aggiornamento](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="1daf8-167">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="1daf8-168">Ricerca di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="1daf8-168">Finding a package</span></span>

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

<span data-ttu-id="1daf8-169">Vedere [Find-Package](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="1daf8-169">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="1daf8-170">In Visual Studio 2013 e versioni precedenti, utilizzare [Get-Package](../tools/ps-ref-get-package.md) invece.</span><span class="sxs-lookup"><span data-stu-id="1daf8-170">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="1daf8-171">Disponibilità della console di</span><span class="sxs-lookup"><span data-stu-id="1daf8-171">Availability of the console</span></span>

<span data-ttu-id="1daf8-172">In Visual Studio 2017, NuGet e gestione pacchetti NuGet vengono installati automaticamente quando si seleziona uno. Carichi di lavoro correlati alla rete; è possibile anche installare singolarmente controllando il **singoli componenti > codice strumenti > Gestione pacchetti NuGet** opzione nel programma di installazione di Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="1daf8-172">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="1daf8-173">Inoltre, assenza Gestione pacchetti NuGet in Visual Studio 2015 e versioni precedenti, controllare **strumenti > estensioni e aggiornamenti...**  e cercare l'estensione Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="1daf8-173">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="1daf8-174">Se non si riesce a usare il programma di installazione di estensioni in Visual Studio, è possibile scaricare l'estensione direttamente da [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="1daf8-174">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="1daf8-175">La Console di gestione pacchetti non è attualmente disponibile in Visual Studio per Mac.</span><span class="sxs-lookup"><span data-stu-id="1daf8-175">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="1daf8-176">I comandi equivalenti, tuttavia, sono disponibili tramite il [NuGet CLI](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="1daf8-176">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="1daf8-177">Visual Studio per Mac hanno un'interfaccia utente per la gestione dei pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="1daf8-177">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="1daf8-178">Vedere [pacchetto NuGet un inclusi nel progetto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="1daf8-178">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="1daf8-179">Console di gestione pacchetti non è inclusa in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="1daf8-179">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="1daf8-180">Estendere la Console di gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="1daf8-180">Extending the Package Manager Console</span></span>

<span data-ttu-id="1daf8-181">Alcuni pacchetti installare nuovi comandi per la console.</span><span class="sxs-lookup"><span data-stu-id="1daf8-181">Some packages install new commands for the console.</span></span> <span data-ttu-id="1daf8-182">Ad esempio, `MvcScaffolding` crea comandi come `Scaffold` illustrato di seguito, che genera l'errore ASP.NET MVC controller e visualizzazioni:</span><span class="sxs-lookup"><span data-stu-id="1daf8-182">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Installazione e utilizzo MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="1daf8-184">Impostazione di un profilo di PowerShell di NuGet</span><span class="sxs-lookup"><span data-stu-id="1daf8-184">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="1daf8-185">Un profilo di PowerShell consente di rendere disponibili i comandi di uso comune, ogni volta che è possibile usare PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1daf8-185">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="1daf8-186">NuGet supporta un profilo specifico di NuGet in genere disponibile nel percorso seguente:</span><span class="sxs-lookup"><span data-stu-id="1daf8-186">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="1daf8-187">Per trovare il profilo, digitare `$profile` nella console:</span><span class="sxs-lookup"><span data-stu-id="1daf8-187">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="1daf8-188">Per ulteriori informazioni, vedere [profili di Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="1daf8-188">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="1daf8-189">Tramite l'interfaccia CLI di nuget.exe nella console di</span><span class="sxs-lookup"><span data-stu-id="1daf8-189">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="1daf8-190">Per rendere il [ `nuget.exe` CLI](nuget-exe-cli-reference.md) disponibile nella Console di gestione pacchetti, installare il [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) pacchetto dalla console:</span><span class="sxs-lookup"><span data-stu-id="1daf8-190">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
