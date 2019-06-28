---
title: Installare e gestire i pacchetti NuGet usando PowerShell in Visual Studio
description: Istruzioni per l'utilizzo della Console di gestione pacchetti NuGet in Visual Studio per l'uso di pacchetti.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 11ec25598d3110ba84dec5044642e205e13346af
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426210"
---
# <a name="install-and-manage-packages-using-powershell-in-visual-studio"></a><span data-ttu-id="f06c8-103">Installare e gestire i pacchetti con PowerShell in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f06c8-103">Install and manage packages using PowerShell in Visual Studio</span></span>

<span data-ttu-id="f06c8-104">La Console di gestione pacchetti NuGet consente di usare [comandi di PowerShell di NuGet](../tools/powershell-reference.md) per trovare, installare, disinstallare e aggiornare i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="f06c8-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="f06c8-105">Utilizzo della console è necessario nei casi in cui il Package Manager UI non fornisce un modo per eseguire un'operazione.</span><span class="sxs-lookup"><span data-stu-id="f06c8-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="f06c8-106">Per utilizzare `nuget.exe` comandi dell'interfaccia della riga nella console, vedere [tramite la CLI nuget.exe nella console di](#using-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="f06c8-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="f06c8-107">La console viene compilata in Visual Studio in Windows.</span><span class="sxs-lookup"><span data-stu-id="f06c8-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="f06c8-108">Non è incluso in Visual Studio per Mac o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f06c8-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="f06c8-109">Trovare e installare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="f06c8-109">Find and install a package</span></span>

<span data-ttu-id="f06c8-110">Ad esempio, ricerca e installazione di un pacchetto avviene in tre semplici passaggi:</span><span class="sxs-lookup"><span data-stu-id="f06c8-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="f06c8-111">Aprire il progetto/soluzione in Visual Studio e aprire la console usando il **strumenti > Gestione pacchetti NuGet > Console di gestione pacchetti** comando.</span><span class="sxs-lookup"><span data-stu-id="f06c8-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="f06c8-112">Trovare il pacchetto da installare.</span><span class="sxs-lookup"><span data-stu-id="f06c8-112">Find the package you want to install.</span></span> <span data-ttu-id="f06c8-113">Se si conosce già questo, andare al passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="f06c8-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="f06c8-114">Eseguire il comando di installazione:</span><span class="sxs-lookup"><span data-stu-id="f06c8-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="f06c8-115">Tutte le operazioni disponibili nella console possono essere eseguite anche con il [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="f06c8-115">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="f06c8-116">Tuttavia, i comandi della console operano all'interno del contesto di Visual Studio e una progetto/soluzione salvata e spesso a una maggiore rispetto i comandi equivalenti di CLI.</span><span class="sxs-lookup"><span data-stu-id="f06c8-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="f06c8-117">Ad esempio, installazione di un pacchetto tramite la console aggiunge un riferimento al progetto mentre la riga di comando non le supporta.</span><span class="sxs-lookup"><span data-stu-id="f06c8-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="f06c8-118">Per questo motivo, gli sviluppatori che lavorano in genere in Visual Studio preferiscono usare la console per l'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="f06c8-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="f06c8-119">Molte operazioni di console dipendono da una soluzione aperta in Visual Studio con un nome di percorso noto.</span><span class="sxs-lookup"><span data-stu-id="f06c8-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="f06c8-120">Se si dispone di una soluzione non sono stata salvata o alcuna soluzione, è possibile visualizzare l'errore, "soluzione non è aperto o non salvate.</span><span class="sxs-lookup"><span data-stu-id="f06c8-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="f06c8-121">Assicurarsi di che avere una soluzione aperta e viene salvata."</span><span class="sxs-lookup"><span data-stu-id="f06c8-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="f06c8-122">Ciò indica che la console non è possibile determinare la cartella della soluzione.</span><span class="sxs-lookup"><span data-stu-id="f06c8-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="f06c8-123">Salvataggio di una soluzione non sono stata salvata, o creando e salvando una soluzione se non è aperto, deve correggere l'errore.</span><span class="sxs-lookup"><span data-stu-id="f06c8-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="f06c8-124">Aprire la console e i controlli di console</span><span class="sxs-lookup"><span data-stu-id="f06c8-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="f06c8-125">Aprire la console in Visual Studio usando il **strumenti > Gestione pacchetti NuGet > Console di gestione pacchetti** comando.</span><span class="sxs-lookup"><span data-stu-id="f06c8-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="f06c8-126">La console è una finestra di Visual Studio che può essere disposti e posizionata, tuttavia si desidera che (vedere [personalizzare i layout delle finestre in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="f06c8-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="f06c8-127">Per impostazione predefinita, i comandi della console funzionano su un'origine di pacchetto specifico e un progetto come impostato nel controllo nella parte superiore della finestra:</span><span class="sxs-lookup"><span data-stu-id="f06c8-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Controlli di Console di gestione pacchetti per l'origine del pacchetto e progetto](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="f06c8-129">Selezione un'origine dei pacchetti diversi e/o progetto comporta la modifica i valori predefiniti per i comandi successivi.</span><span class="sxs-lookup"><span data-stu-id="f06c8-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="f06c8-130">La maggior parte dei comandi per esegue l'override queste impostazioni senza dover modificare le impostazioni predefinite, supportano `-Source` e `-ProjectName` opzioni.</span><span class="sxs-lookup"><span data-stu-id="f06c8-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="f06c8-131">Per la gestione di origini dei pacchetti, selezionare l'icona a forma di ingranaggio.</span><span class="sxs-lookup"><span data-stu-id="f06c8-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="f06c8-132">Si tratta di un collegamento per il **strumenti > Opzioni > Gestione pacchetti NuGet > origini pacchetti** come descritto nella finestra di dialogo il [Package Manager UI](package-manager-ui.md#package-sources) pagina.</span><span class="sxs-lookup"><span data-stu-id="f06c8-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="f06c8-133">Inoltre, il controllo a destra del selettore di progetto Cancella il contenuto della console:</span><span class="sxs-lookup"><span data-stu-id="f06c8-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Controlli non crittografati e le impostazioni della Console di gestione pacchetti](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="f06c8-135">Il pulsante all'estrema destra consente di interrompere un comando a esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="f06c8-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="f06c8-136">Ad esempio, l'esecuzione `Get-Package -ListAvailable -PageSize 500` Elenca i primi 500 pacchetti sull'origine predefinita (ad esempio, nuget.org), che potrebbe richiedere alcuni minuti per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f06c8-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Controllo stop Console di gestione pacchetti](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="f06c8-138">Installazione di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="f06c8-138">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="f06c8-139">Visualizzare [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="f06c8-139">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="f06c8-140">Installazione di un pacchetto nella console esegue gli stessi passaggi come descritto nella [cosa accade quando viene installato un pacchetto](../concepts/package-installation-process.md), con le aggiunte seguenti:</span><span class="sxs-lookup"><span data-stu-id="f06c8-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="f06c8-141">La Console Visualizza condizioni di licenza applicabili nella relativa finestra con un contratto implicito.</span><span class="sxs-lookup"><span data-stu-id="f06c8-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="f06c8-142">Se si accettano le condizioni, è necessario disinstallare il pacchetto immediatamente.</span><span class="sxs-lookup"><span data-stu-id="f06c8-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="f06c8-143">Anche un riferimento al pacchetto viene aggiunto al file di progetto e viene visualizzato nella **Esplora soluzioni** sotto il **riferimenti** nodo, è necessario salvare il progetto per visualizzare le modifiche nel file di progetto direttamente.</span><span class="sxs-lookup"><span data-stu-id="f06c8-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="f06c8-144">Disinstallazione di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="f06c8-144">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="f06c8-145">Visualizzare [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="f06c8-145">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="f06c8-146">Uso [Get-Package](../tools/ps-ref-get-package.md) per visualizzare tutti i pacchetti attualmente installati nel progetto predefinito se è necessario trovare un identificatore.</span><span class="sxs-lookup"><span data-stu-id="f06c8-146">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="f06c8-147">Disinstallazione di un pacchetto esegue le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f06c8-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="f06c8-148">Rimuove i riferimenti al pacchetto dal progetto (e qualsiasi formato di gestione è in uso).</span><span class="sxs-lookup"><span data-stu-id="f06c8-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="f06c8-149">I riferimenti non siano più presenti **Esplora soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="f06c8-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="f06c8-150">(Potrebbe essere necessario ricompilare il progetto per visualizzarne il rimosso dal **Bin** cartella.)</span><span class="sxs-lookup"><span data-stu-id="f06c8-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="f06c8-151">Le eventuali modifiche apportate al `app.config` o `web.config` quando è stato installato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f06c8-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="f06c8-152">Dipendenze rimuove installata in precedenza, se non ci sono pacchetti rimanenti usano tali dipendenze.</span><span class="sxs-lookup"><span data-stu-id="f06c8-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="f06c8-153">Aggiorna un pacchetto</span><span class="sxs-lookup"><span data-stu-id="f06c8-153">Updating a package</span></span>

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

<span data-ttu-id="f06c8-154">Visualizzare [Get-Package](../tools/ps-ref-get-package.md) e [Update-Package](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="f06c8-154">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="f06c8-155">Ricerca di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="f06c8-155">Finding a package</span></span>

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

<span data-ttu-id="f06c8-156">Visualizzare [Find-Package](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="f06c8-156">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="f06c8-157">In Visual Studio 2013 e versioni precedenti, usare [Get-Package](../tools/ps-ref-get-package.md) invece.</span><span class="sxs-lookup"><span data-stu-id="f06c8-157">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="f06c8-158">Disponibilità della console</span><span class="sxs-lookup"><span data-stu-id="f06c8-158">Availability of the console</span></span>

<span data-ttu-id="f06c8-159">A partire da Visual Studio 2017, NuGet e la gestione pacchetti NuGet vengono installati automaticamente quando si seleziona uno. Carichi di lavoro correlati NET; è possibile anche installare singolarmente controllando il **singoli componenti > strumenti per il codice > Gestione pacchetti NuGet** opzione nel programma di installazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f06c8-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="f06c8-160">Inoltre, se sono necessari i pacchetti NuGet in Visual Studio 2015 e versioni precedenti, controllare **strumenti > estensioni e aggiornamenti...**  e cercare l'estensione Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="f06c8-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="f06c8-161">Se non si riesce a usare il programma di installazione di estensioni in Visual Studio, è possibile scaricare l'estensione direttamente dal [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="f06c8-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="f06c8-162">La Console di gestione pacchetti non è attualmente disponibile in Visual Studio per Mac.</span><span class="sxs-lookup"><span data-stu-id="f06c8-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="f06c8-163">I comandi equivalenti, tuttavia, sono disponibili tramite il [NuGet CLI](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="f06c8-163">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="f06c8-164">Visual Studio per Mac ha un'interfaccia utente per la gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="f06c8-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="f06c8-165">Visualizzare [tra cui un pacchetto NuGet nel progetto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="f06c8-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="f06c8-166">Console di gestione pacchetti non è inclusa in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f06c8-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="f06c8-167">Estendere la Console di gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="f06c8-167">Extending the Package Manager Console</span></span>

<span data-ttu-id="f06c8-168">Alcuni pacchetti installati nuovi comandi per la console.</span><span class="sxs-lookup"><span data-stu-id="f06c8-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="f06c8-169">Ad esempio, `MvcScaffolding` consente di creare comandi, ad esempio `Scaffold` illustrato di seguito, che genera le visualizzazioni e controller ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="f06c8-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Installazione e l'utilizzo MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="f06c8-171">Configurazione di un profilo di PowerShell di NuGet</span><span class="sxs-lookup"><span data-stu-id="f06c8-171">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="f06c8-172">Un profilo di PowerShell consente di rendere disponibili i comandi di uso comune, ogni volta che si usa PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f06c8-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="f06c8-173">NuGet supporta un profilo specifico di NuGet in genere disponibile nel percorso seguente:</span><span class="sxs-lookup"><span data-stu-id="f06c8-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="f06c8-174">Per trovare il profilo, digitare `$profile` nella console:</span><span class="sxs-lookup"><span data-stu-id="f06c8-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="f06c8-175">Per altri dettagli, consultare [profili di Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="f06c8-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="f06c8-176">Tramite la CLI nuget.exe nella console di</span><span class="sxs-lookup"><span data-stu-id="f06c8-176">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="f06c8-177">Per rendere il [ `nuget.exe` CLI](nuget-exe-cli-reference.md) disponibile nella Console di gestione pacchetti, installare il [NuGet. CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) pacchetto dalla console:</span><span class="sxs-lookup"><span data-stu-id="f06c8-177">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
