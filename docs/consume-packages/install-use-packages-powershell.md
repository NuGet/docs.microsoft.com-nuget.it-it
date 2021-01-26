---
title: Installare e gestire i pacchetti NuGet usando la console in Visual Studio
description: Istruzioni per l'uso della console di Gestione pacchetti NuGet in Visual Studio per utilizzare i pacchetti.
author: JonDouglas
ms.author: jodou
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 119bf32426e5cbc179c3713e60688c691e133c5d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774901"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="de45a-103">Installare e gestire i pacchetti con la console di Gestione pacchetti in Visual Studio (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="de45a-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="de45a-104">La console di Gestione pacchetti NuGet consente di usare i [comandi di PowerShell di NuGet](../reference/powershell-reference.md) per trovare, installare, disinstallare e aggiornare i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="de45a-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../reference/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="de45a-105">L'uso della console è necessario nei casi in cui l'interfaccia utente di Gestione pacchetti non offre un modo per eseguire un'operazione.</span><span class="sxs-lookup"><span data-stu-id="de45a-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="de45a-106">Per usare i comandi dell'interfaccia della riga di comando di `nuget.exe` nella console, vedere [Uso dell'interfaccia della riga di comando di nuget.exe nella console](#use-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="de45a-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#use-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="de45a-107">La console è inclusa in Visual Studio in Windows.</span><span class="sxs-lookup"><span data-stu-id="de45a-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="de45a-108">Non è disponibile in Visual Studio per Mac o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="de45a-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

> [!Important]
> <span data-ttu-id="de45a-109">I comandi elencati di seguito sono specifici della console di gestione pacchetti in Visual Studio e si differenziano dai [comandi del modulo Gestione pacchetti](/powershell/module/packagemanagement/) disponibili in un ambiente PowerShell generale.</span><span class="sxs-lookup"><span data-stu-id="de45a-109">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="de45a-110">In particolare, in ogni ambiente sono presenti comandi che non sono disponibili nell'altra e i comandi con lo stesso nome potrebbero differire anche per gli argomenti specifici.</span><span class="sxs-lookup"><span data-stu-id="de45a-110">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="de45a-111">Quando si usa la console di Gestione pacchetti in Visual Studio, vengono applicati i comandi e gli argomenti illustrati in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="de45a-111">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="de45a-112">Trovare e installare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="de45a-112">Find and install a package</span></span>

<span data-ttu-id="de45a-113">La ricerca e l'installazione di un pacchetto, ad esempio, vengono eseguite con tre semplici passaggi:</span><span class="sxs-lookup"><span data-stu-id="de45a-113">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="de45a-114">Aprire il progetto o la soluzione in Visual Studio e aprire la console usando il comando **Strumenti > Gestione pacchetti NuGet > Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="de45a-114">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="de45a-115">Trovare il pacchetto che si vuole installare.</span><span class="sxs-lookup"><span data-stu-id="de45a-115">Find the package you want to install.</span></span> <span data-ttu-id="de45a-116">Se lo si conosce già, andare al passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="de45a-116">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="de45a-117">Eseguire il comando di installazione:</span><span class="sxs-lookup"><span data-stu-id="de45a-117">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="de45a-118">Tutte le operazioni disponibili nella console possono essere eseguite anche con l'[interfaccia della riga di comando di NuGet](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="de45a-118">All operations that are available in the console can also be done with the [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="de45a-119">Tuttavia, i comandi della console operano all'interno del contesto di Visual Studio e di un progetto o una soluzione salvati e spesso consentono di ottenere maggiori risultati rispetto ai comandi dell'interfaccia della riga di comando equivalenti.</span><span class="sxs-lookup"><span data-stu-id="de45a-119">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="de45a-120">Ad esempio, l'installazione di un pacchetto tramite la console aggiunge un riferimento al progetto, diversamente dal comando dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="de45a-120">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="de45a-121">Per questo motivo, gli sviluppatori che lavorano in Visual Studio in genere preferiscono usare la console rispetto all'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="de45a-121">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="de45a-122">Molte operazioni della console dipendono dalla presenza di una soluzione aperta in Visual Studio con un nome di percorso noto.</span><span class="sxs-lookup"><span data-stu-id="de45a-122">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="de45a-123">Se è aperta una soluzione non salvata o non è disponibile alcuna soluzione, è possibile che venga visualizzato l'errore "Soluzione non aperta o non salvata.</span><span class="sxs-lookup"><span data-stu-id="de45a-123">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="de45a-124">Assicurarsi di disporre di una soluzione aperta e salvata."</span><span class="sxs-lookup"><span data-stu-id="de45a-124">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="de45a-125">Ciò indica che la console non è in grado di determinare la cartella della soluzione.</span><span class="sxs-lookup"><span data-stu-id="de45a-125">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="de45a-126">Il salvataggio di una soluzione non salvata o la creazione e il salvataggio di una soluzione, se non ce n'è una aperta, dovrebbero risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="de45a-126">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="de45a-127">Apertura della console e dei controlli della console</span><span class="sxs-lookup"><span data-stu-id="de45a-127">Opening the console and console controls</span></span>

1. <span data-ttu-id="de45a-128">Aprire la console in Visual Studio usando il comando **Strumenti > Gestione pacchetti NuGet > Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="de45a-128">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="de45a-129">La console è una finestra di Visual Studio che può essere disposta e posizionata nel modo preferito (vedere [Personalizzare il layout delle finestre in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="de45a-129">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="de45a-130">Per impostazione predefinita, i comandi della console agiscono su un'origine e un progetto di pacchetto specifici impostati nel controllo nella parte superiore della finestra:</span><span class="sxs-lookup"><span data-stu-id="de45a-130">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Controlli della console di Gestione pacchetti per l'origine e il progetto del pacchetto](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="de45a-132">Se si seleziona un'origine e/o un progetto diverso per il pacchetto, verranno modificate le impostazioni predefinite per i comandi successivi.</span><span class="sxs-lookup"><span data-stu-id="de45a-132">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="de45a-133">Per sostituire queste impostazioni senza modificare le impostazioni predefinite, la maggior parte dei comandi supporta le opzioni `-Source` e `-ProjectName`.</span><span class="sxs-lookup"><span data-stu-id="de45a-133">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="de45a-134">Per gestire le origini dei pacchetti, selezionare l'icona a forma di ingranaggio.</span><span class="sxs-lookup"><span data-stu-id="de45a-134">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="de45a-135">Si tratta di un collegamento alla finestra di dialogo **Strumenti > Opzioni > Gestione pacchetti NuGet > Origini pacchetti**, come descritto nella pagina [Interfaccia utente di Gestione pacchetti](install-use-packages-visual-studio.md#package-sources).</span><span class="sxs-lookup"><span data-stu-id="de45a-135">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](install-use-packages-visual-studio.md#package-sources) page.</span></span> <span data-ttu-id="de45a-136">Inoltre, il controllo a destra del selettore del progetto cancella il contenuto della console:</span><span class="sxs-lookup"><span data-stu-id="de45a-136">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Impostazioni della console di Gestione pacchetti e controlli per cancellare](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="de45a-138">Il pulsante più a destra interrompe un comando con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="de45a-138">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="de45a-139">Ad esempio, l'esecuzione di `Get-Package -ListAvailable -PageSize 500` elenca i primi 500 pacchetti nell'origine predefinita, ad esempio nuget.org, un'operazione che potrebbe richiedere vari minuti per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="de45a-139">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Controllo di interruzione nella console di Gestione pacchetti](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a><span data-ttu-id="de45a-141">Installare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="de45a-141">Install a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="de45a-142">Vedere [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="de45a-142">See [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span></span>

<span data-ttu-id="de45a-143">L'installazione di un pacchetto nella console esegue gli stessi passaggi descritti in [Cosa accade quando viene installato un pacchetto](../concepts/package-installation-process.md), con le aggiunte seguenti:</span><span class="sxs-lookup"><span data-stu-id="de45a-143">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="de45a-144">Nella console vengono visualizzate le condizioni di licenza applicabili nella finestra con contratto implicito.</span><span class="sxs-lookup"><span data-stu-id="de45a-144">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="de45a-145">Se non si accettano le condizioni, è necessario disinstallare il pacchetto immediatamente.</span><span class="sxs-lookup"><span data-stu-id="de45a-145">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="de45a-146">Viene inoltre aggiunto un riferimento al pacchetto al file di progetto, visualizzato in **Esplora soluzioni** nel nodo **Riferimenti**. È necessario salvare il progetto per visualizzare direttamente le modifiche nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="de45a-146">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="de45a-147">Disinstalla un pacchetto</span><span class="sxs-lookup"><span data-stu-id="de45a-147">Uninstall a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="de45a-148">Vedere [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="de45a-148">See [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="de45a-149">Usare [Get-Package](../reference/ps-reference/ps-ref-get-package.md) per visualizzare tutti i pacchetti attualmente installati nel progetto predefinito, se è necessario trovare un identificatore.</span><span class="sxs-lookup"><span data-stu-id="de45a-149">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="de45a-150">Con la disinstallazione di un pacchetto vengono eseguite le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="de45a-150">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="de45a-151">Rimozione dei riferimenti al pacchetto dal progetto (qualsiasi sia il formato di gestione in uso).</span><span class="sxs-lookup"><span data-stu-id="de45a-151">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="de45a-152">I riferimenti non vengono più visualizzati in **Esplora soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="de45a-152">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="de45a-153">Potrebbe essere necessario ricompilare il progetto per verificarne la rimozione dalla cartella **Bin**.</span><span class="sxs-lookup"><span data-stu-id="de45a-153">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="de45a-154">Ripristino delle eventuali modifiche apportate a `app.config` o `web.config` al momento dell'installazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="de45a-154">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="de45a-155">Rimozione delle dipendenze installate in precedenza se nessun pacchetto rimanente usa tali dipendenze.</span><span class="sxs-lookup"><span data-stu-id="de45a-155">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="de45a-156">Aggiornare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="de45a-156">Update a package</span></span>

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

<span data-ttu-id="de45a-157">Vedere [Get-Package](../reference/ps-reference/ps-ref-get-package.md) e [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="de45a-157">See [Get-Package](../reference/ps-reference/ps-ref-get-package.md) and [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span></span>

## <a name="find-a-package"></a><span data-ttu-id="de45a-158">Trovare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="de45a-158">Find a package</span></span>

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

<span data-ttu-id="de45a-159">Vedere [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="de45a-159">See [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span></span> <span data-ttu-id="de45a-160">In Visual Studio 2013 e versioni precedenti usare invece [Get-Package](../reference/ps-reference/ps-ref-get-package.md).</span><span class="sxs-lookup"><span data-stu-id="de45a-160">In Visual Studio 2013 and earlier, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="de45a-161">Disponibilità della console</span><span class="sxs-lookup"><span data-stu-id="de45a-161">Availability of the console</span></span>

<span data-ttu-id="de45a-162">A partire da Visual Studio 2017, NuGet e Gestione pacchetti NuGet vengono installati automaticamente quando si seleziona uno dei carichi di lavoro correlati a NET. È anche possibile installarlo singolarmente selezionando **Singoli componenti >Strumenti per il codice > Gestione pacchetti NuGet** nel programma di installazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de45a-162">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="de45a-163">Inoltre, se non si trova Gestione pacchetti NuGet in Visual Studio 2015 e versioni precedenti, selezionare **Strumenti > Estensioni e aggiornamenti** e cercare l'estensione Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="de45a-163">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="de45a-164">Se non si è in grado di usare il programma di installazione delle estensioni in Visual Studio, è possibile scaricare l'estensione direttamente da [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) .</span><span class="sxs-lookup"><span data-stu-id="de45a-164">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="de45a-165">La console di Gestione pacchetti non è attualmente disponibile con Visual Studio per Mac.</span><span class="sxs-lookup"><span data-stu-id="de45a-165">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="de45a-166">I comandi equivalenti, tuttavia, sono disponibili tramite l'[interfaccia della riga di comando di NuGet](../reference/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="de45a-166">The equivalent commands, however, are available through the [NuGet CLI](../reference/nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="de45a-167">Visual Studio per Mac include un'interfaccia utente per la gestione dei pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="de45a-167">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="de45a-168">Vedere [Inserimento di un pacchetto NuGet nel progetto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="de45a-168">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="de45a-169">La console di Gestione pacchetti non è inclusa in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="de45a-169">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extend-the-package-manager-console"></a><span data-ttu-id="de45a-170">Estendere la console di Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="de45a-170">Extend the Package Manager Console</span></span>

<span data-ttu-id="de45a-171">Alcuni pacchetti installano nuovi comandi per la console.</span><span class="sxs-lookup"><span data-stu-id="de45a-171">Some packages install new commands for the console.</span></span> <span data-ttu-id="de45a-172">Ad esempio, `MvcScaffolding` crea comandi come `Scaffold` mostrato di seguito, che genera i controller e le visualizzazioni MVC ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="de45a-172">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Installazione e uso di MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a><span data-ttu-id="de45a-174">Configurare un profilo di PowerShell per NuGet</span><span class="sxs-lookup"><span data-stu-id="de45a-174">Set up a NuGet PowerShell profile</span></span>

<span data-ttu-id="de45a-175">Un profilo di PowerShell consente di rendere disponibili i comandi usati comunemente ogni volta che si usa PowerShell.</span><span class="sxs-lookup"><span data-stu-id="de45a-175">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="de45a-176">NuGet supporta un profilo specifico di NuGet disponibile in genere nel percorso seguente:</span><span class="sxs-lookup"><span data-stu-id="de45a-176">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

<span data-ttu-id="de45a-177">*% UserProfile% \Documents\WindowsPowerShell\NuGet_profile.ps1*</span><span class="sxs-lookup"><span data-stu-id="de45a-177">*%UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1*</span></span>

<span data-ttu-id="de45a-178">Per trovare il profilo, digitare `$profile` nella console:</span><span class="sxs-lookup"><span data-stu-id="de45a-178">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="de45a-179">Per altri dettagli, vedere [Profili di Windows PowerShell](/previous-versions//bb613488(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="de45a-179">For more details, refer to [Windows PowerShell Profiles](/previous-versions//bb613488(v=vs.85)).</span></span>

## <a name="use-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="de45a-180">Usare l'interfaccia della riga di comando di nuget.exe nella console</span><span class="sxs-lookup"><span data-stu-id="de45a-180">Use the nuget.exe CLI in the console</span></span>

<span data-ttu-id="de45a-181">Per rendere disponibile l' [ `nuget.exe` interfaccia](../reference/nuget-exe-cli-reference.md) della riga di comando nella console di gestione pacchetti, installare il pacchetto [NuGet. CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) dalla console di:</span><span class="sxs-lookup"><span data-stu-id="de45a-181">To make the [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
