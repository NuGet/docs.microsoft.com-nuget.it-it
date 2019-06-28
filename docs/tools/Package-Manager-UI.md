---
title: Installare e gestire pacchetti NuGet in Visual Studio
description: Istruzioni per l'uso di NuGet Package Manager UI in Visual Studio per l'uso di pacchetti NuGet.
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 97e5de3f07199cd3c6a645749c8f2f1603ca630e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426241"
---
# <a name="install-and-manage-packages-in-visual-studio"></a><span data-ttu-id="e3fbe-103">Installare e gestire pacchetti in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e3fbe-103">Install and manage packages in Visual Studio</span></span>

<span data-ttu-id="e3fbe-104">L'UI Gestione pacchetti NuGet in Visual Studio in Windows consente di installare, disinstallare e aggiornare i pacchetti NuGet in progetti e soluzioni.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="e3fbe-105">Per l'esperienza in Visual Studio per Mac, vedere [tra cui un pacchetto NuGet nel progetto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="e3fbe-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="e3fbe-106">Il Package Manager UI non è inclusa in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="e3fbe-107">Se sono necessari i pacchetti NuGet in Visual Studio 2015, controllare **strumenti > estensioni e aggiornamenti...**  e cercare la *Gestione pacchetti NuGet* estensione.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="e3fbe-108">Se non si riesce a usare il programma di installazione di estensioni in Visual Studio, scaricare l'estensione direttamente dal [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="e3fbe-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="e3fbe-109">A partire da Visual Studio 2017, NuGet e la gestione pacchetti NuGet vengono installati automaticamente con qualsiasi. Carichi di lavoro correlate alla rete.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="e3fbe-110">Installare singolarmente selezionando i **singoli componenti > strumenti per il codice > Gestione pacchetti NuGet** opzione nel programma di installazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="e3fbe-111">Ricerca e installazione di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="e3fbe-111">Finding and installing a package</span></span>

1. <span data-ttu-id="e3fbe-112">Nelle **Esplora soluzioni**, fare doppio clic su uno **riferimenti** o un progetto e selezionare **Gestisci pacchetti NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="e3fbe-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![I pacchetti NuGet dal menu Opzioni di gestione](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="e3fbe-114">Il **esplorare** scheda consente di visualizzare i pacchetti per popolarità dell'origine attualmente selezionata (vedere [origini di pacchetti](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="e3fbe-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="e3fbe-115">Ricerca di un pacchetto specifico usando la casella di ricerca in alto a sinistra.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="e3fbe-116">Selezionare un pacchetto dall'elenco per visualizzare informazioni, che abilita anche il **installare** pulsante insieme a un elenco a discesa-selezione della versione.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Gestione scheda Sfoglia di NuGet package finestra di dialogo](media/Search.png)

1. <span data-ttu-id="e3fbe-118">Selezionare la versione desiderata dall'elenco a discesa e selezionare **installare**.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="e3fbe-119">Visual Studio installa il pacchetto e le relative dipendenze nel progetto.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="e3fbe-120">Potrebbe essere richiesto di accettare le condizioni di licenza.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="e3fbe-121">Quando l'installazione è stata completata, i pacchetti aggiunti vengono visualizzati nella **Installed** scheda. I pacchetti sono elencati anche nella **riferimenti** nodo di Esplora soluzioni, che indica che è possibile farvi riferimento nel progetto con `using` istruzioni.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Riferimenti in Esplora soluzioni](media/References.png)

> [!Tip]
> <span data-ttu-id="e3fbe-123">Per includere le versioni non definitive nella ricerca e per rendere le versioni non definitive disponibili nella versione di elenco a discesa, selezionare la **Includi versione preliminare** opzione.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="e3fbe-124">Disinstallazione di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="e3fbe-124">Uninstalling a package</span></span>

1. <span data-ttu-id="e3fbe-125">Nelle **Esplora soluzioni**, fare doppio clic su uno **riferimenti** oppure il progetto desiderato e selezionare **Gestisci pacchetti NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="e3fbe-125">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="e3fbe-126">Selezionare il **Installed** scheda.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-126">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="e3fbe-127">Selezionare il pacchetto da disinstallare (uso di ricerca per filtrare l'elenco se necessario) e scegliere **Disinstalla**.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-127">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Disinstallazione di un pacchetto](media/UninstallPackage.png)

1. <span data-ttu-id="e3fbe-129">Si noti che il **Includi versione preliminare** e **origine pacchetto** controlli non hanno alcun effetto durante la disinstallazione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-129">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="e3fbe-130">Aggiorna un pacchetto</span><span class="sxs-lookup"><span data-stu-id="e3fbe-130">Updating a package</span></span>

1. <span data-ttu-id="e3fbe-131">Nelle **Esplora soluzioni**, fare doppio clic su uno **riferimenti** oppure il progetto desiderato e selezionare **Gestisci pacchetti NuGet...** . (In progetti di siti web, fare doppio clic il **Bin** cartella.)</span><span class="sxs-lookup"><span data-stu-id="e3fbe-131">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="e3fbe-132">Selezionare il **aggiornamenti** scheda per visualizzare i pacchetti sono disponibili aggiornamenti dalle origini pacchetto selezionato.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-132">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="e3fbe-133">Selezionare **Includi versione preliminare** per includere i pacchetti di versione non definitivo nel relativo elenco.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-133">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="e3fbe-134">Selezionare il pacchetto da aggiornare, selezionare la versione desiderata dall'elenco a discesa a destra e selezionare **aggiornare**.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-134">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Aggiorna un pacchetto](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="e3fbe-136">Per alcuni pacchetti, la **Update** pulsante è disabilitato e viene visualizzato un messaggio che informa che è "in modo implicito fa un SDK" (o "AutoReferenced").</span><span class="sxs-lookup"><span data-stu-id="e3fbe-136">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="e3fbe-137">Questo messaggio indica che il pacchetto fa parte di un framework o SDK di dimensioni superiori e non deve essere aggiornato in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-137">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="e3fbe-138">(Tali pacchetti internamente sono contrassegnati con `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Ad esempio, `Microsoft.NETCore.App` fa parte di .NET Core SDK e la versione del pacchetto non è la stessa versione di framework runtime usati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-138">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="e3fbe-139">Devi [aggiornare l'installazione di .NET Core](https://aka.ms/dotnet-download) per ottenere nuove versioni del runtime di ASP.NET Core e .NET Core.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-139">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="e3fbe-140">[Vedere questo documento per altri dettagli sulla metapacchetti .NET Core e controllo delle versioni](/dotnet/core/packages).</span><span class="sxs-lookup"><span data-stu-id="e3fbe-140">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="e3fbe-141">Questo vale per i pacchetti di usati comune seguenti:</span><span class="sxs-lookup"><span data-stu-id="e3fbe-141">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="e3fbe-142">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="e3fbe-142">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="e3fbe-143">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="e3fbe-143">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="e3fbe-144">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="e3fbe-144">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="e3fbe-145">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="e3fbe-145">NETStandard.Library</span></span>

    ![Pacchetto di esempio viene contrassegnato come in modo implicito i riferimenti o AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="e3fbe-147">Per aggiornare più pacchetti alle corrispondenti versioni più recenti, selezionarli nell'elenco e selezionare il **aggiornare** pulsante sopra l'elenco.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-147">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="e3fbe-148">È anche possibile aggiornare un pacchetto singolo dal **Installed** scheda. In questo caso, i dettagli per il pacchetto includono un selettore di versione (soggetto al **Includi versione preliminare** opzione) e un **Update** pulsante.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-148">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="e3fbe-149">La gestione dei pacchetti per la soluzione</span><span class="sxs-lookup"><span data-stu-id="e3fbe-149">Managing packages for the solution</span></span>

<span data-ttu-id="e3fbe-150">La gestione dei pacchetti per una soluzione è un modo pratico per lavorare con più progetti contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-150">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="e3fbe-151">Selezionare il **strumenti > Gestione pacchetti NuGet > Gestisci pacchetti NuGet per la soluzione...**  dal menu di comando, o la soluzione e scegliere **Gestisci pacchetti NuGet...** :</span><span class="sxs-lookup"><span data-stu-id="e3fbe-151">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Gestisci pacchetti NuGet per la soluzione](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="e3fbe-153">Quando si gestiscono i pacchetti per la soluzione, l'interfaccia utente consente di selezionare i progetti che sono interessati dalle operazioni:</span><span class="sxs-lookup"><span data-stu-id="e3fbe-153">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Selettore progetti durante la gestione dei pacchetti per la soluzione](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="e3fbe-155">Consolidare scheda</span><span class="sxs-lookup"><span data-stu-id="e3fbe-155">Consolidate tab</span></span>

<span data-ttu-id="e3fbe-156">Gli sviluppatori considerano in genere una buona prassi di usare versioni diverse dello stesso pacchetto NuGet in progetti diversi nella stessa soluzione.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-156">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="e3fbe-157">Quando si sceglie di gestire i pacchetti per una soluzione, il Package Manager UI offre una **consolida** scheda in cui è possibile visualizzare facilmente in cui i pacchetti con numeri di versione distinti vengono utilizzati da diversi progetti nella soluzione:</span><span class="sxs-lookup"><span data-stu-id="e3fbe-157">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Scheda di consolidamento dell'interfaccia utente di gestione pacchetti](media/ConsolidateTab.png)

<span data-ttu-id="e3fbe-159">In questo esempio, il progetto ClassLibrary1 Usa EntityFramework 6.2.0, considerando che utilizza EntityFramework 6.1.0 ConsoleApp1.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-159">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="e3fbe-160">Per consolidare le versioni dei pacchetti, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e3fbe-160">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="e3fbe-161">Selezionare i progetti da aggiornare nell'elenco di progetti.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-161">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="e3fbe-162">Selezionare la versione da usare in tutti i progetti nel **versione** controllo, ad esempio EntityFramework 6.2.0.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-162">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="e3fbe-163">Selezionare il **installare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-163">Select the **Install** button.</span></span>

<span data-ttu-id="e3fbe-164">La gestione dei pacchetti consente di installare la versione del pacchetto selezionato in tutti i progetti selezionati, dopo il quale il pacchetto non viene più visualizzata nella **consolida** scheda.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-164">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="e3fbe-165">Origini dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="e3fbe-165">Package sources</span></span>

<span data-ttu-id="e3fbe-166">Per modificare l'origine da cui Visual Studio Ottiene i pacchetti, selezionare uno dal selettore di origine:</span><span class="sxs-lookup"><span data-stu-id="e3fbe-166">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Selettore di origine del pacchetto in package manager UI](media/PackageSourceDropDown.png)

<span data-ttu-id="e3fbe-168">Gestire le origini pacchetto:</span><span class="sxs-lookup"><span data-stu-id="e3fbe-168">To manage package sources:</span></span>

1. <span data-ttu-id="e3fbe-169">Selezionare il **le impostazioni** icona nel Package Manager UI descritti di seguito oppure utilizzare il **strumenti > Opzioni** comando e scorrere fino alla **Gestione pacchetti NuGet**:</span><span class="sxs-lookup"><span data-stu-id="e3fbe-169">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Icona delle impostazioni dell'interfaccia utente di gestione pacchetti](media/PackageSourceSettings.png)

1. <span data-ttu-id="e3fbe-171">Selezionare il **origini dei pacchetti** nodo:</span><span class="sxs-lookup"><span data-stu-id="e3fbe-171">Select the **Package Sources** node:</span></span>

    ![Opzioni di origini dei pacchetti](media/options.png)

1. <span data-ttu-id="e3fbe-173">Per aggiungere un'origine, selezionare **+** , modificare il nome, immettere l'URL o percorso nel **origine** controllare, quindi selezionare **Update**.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-173">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="e3fbe-174">L'origine viene ora visualizzato nel selettore di elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-174">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="e3fbe-175">Per modificare un'origine del pacchetto, selezionarlo, apportare modifiche nel **Name** e **origine** caselle, quindi selezionare **Update**.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-175">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="e3fbe-176">Per disabilitare un'origine del pacchetto, deselezionare la casella a sinistra del nome nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-176">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="e3fbe-177">Per rimuovere un'origine del pacchetto, selezionarlo e quindi selezionare il **X** pulsante.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-177">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="e3fbe-178">Utilizzando la freccia giù e freccia giù pulsanti non viene modificato l'ordine di priorità le origini pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-178">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="e3fbe-179">Visual Studio ignora l'ordine delle origini dei pacchetti, Usa il pacchetto da qualsiasi origine prima di rispondere alle richieste.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-179">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="e3fbe-180">Per altre informazioni, vedere [ripristino del pacchetto](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="e3fbe-180">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="e3fbe-181">Se un'origine del pacchetto viene nuovamente visualizzato dopo l'eliminazione, potrebbe essere presente in un livello di computer o utente `NuGet.Config` file.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-181">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="e3fbe-182">Visualizzare [configurazioni comuni per NuGet](../consume-packages/configuring-nuget-behavior.md) per il percorso di questi file, quindi rimuovere l'origine modificando i file manualmente o tramite il [nuget origini comando](../tools/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="e3fbe-182">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="e3fbe-183">Controllano le opzioni di gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="e3fbe-183">Package manager Options control</span></span>

<span data-ttu-id="e3fbe-184">Quando viene selezionato un pacchetto, il Package Manager UI viene visualizzato un piccolo, espandibile **opzioni** controllo sotto il selettore di versione (illustrato di seguito entrambe compresse ed espanse).</span><span class="sxs-lookup"><span data-stu-id="e3fbe-184">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="e3fbe-185">Si noti che per alcuni progetti solo con tipi, il **Visualizza finestra di anteprima** opzione è disponibile.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-185">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Opzioni di gestione pacchetti](media/PackageManagerUIOptions.png)

<span data-ttu-id="e3fbe-187">Le sezioni seguenti illustrano queste opzioni.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-187">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="e3fbe-188">Visualizzare la finestra di anteprima</span><span class="sxs-lookup"><span data-stu-id="e3fbe-188">Show preview window</span></span>

<span data-ttu-id="e3fbe-189">Quando selezionata, una finestra modale Visualizza che le dipendenze di un pacchetto scelta prima di installata il pacchetto:</span><span class="sxs-lookup"><span data-stu-id="e3fbe-189">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Finestra di anteprima di esempio](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="e3fbe-191">Installare e aggiornare le opzioni</span><span class="sxs-lookup"><span data-stu-id="e3fbe-191">Install and Update Options</span></span>

<span data-ttu-id="e3fbe-192">(Non disponibile per tutti i tipi di progetto).</span><span class="sxs-lookup"><span data-stu-id="e3fbe-192">(Not available for all project types.)</span></span>

<span data-ttu-id="e3fbe-193">**Comportamento di dipendenza** configura come NuGet decide quali versioni dei pacchetti dipendenti da installare:</span><span class="sxs-lookup"><span data-stu-id="e3fbe-193">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="e3fbe-194">*Ignora le dipendenze* ignora l'installazione di eventuali dipendenze, creando in genere un'interruzione del pacchetto da installare.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-194">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="e3fbe-195">*Più basso* [Default] la dipendenza viene installato con il numero di versione minima che soddisfi i requisiti del pacchetto primario scelto.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-195">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="e3fbe-196">*Più alto Patch* viene installata la versione con gli stessi numeri di versione principale e secondaria, ma il numero più alto di patch.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-196">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="e3fbe-197">Ad esempio, se viene specificata una versione 1.2.2 quindi la versione più recente che inizia con 1.2 verrà installata</span><span class="sxs-lookup"><span data-stu-id="e3fbe-197">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="e3fbe-198">*Minore più alto* viene installata la versione con lo stesso numero di versione principale, ma il numero di patch e il numero minore.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-198">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="e3fbe-199">Se la versione 1.2.2 è specificata, verrà installata la versione più alto che inizia con 1</span><span class="sxs-lookup"><span data-stu-id="e3fbe-199">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="e3fbe-200">*Più alto* installa la versione disponibile più recente del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-200">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="e3fbe-201">**Azione di conflitti di file** specifica come NuGet deve gestire i pacchetti già esistenti nel progetto o nel computer locale:</span><span class="sxs-lookup"><span data-stu-id="e3fbe-201">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="e3fbe-202">*Messaggio di richiesta* indica a NuGet per chiedere se mantenere o sovrascrivere i pacchetti esistenti.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-202">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="e3fbe-203">*Ignora tutto* indica a NuGet a saltare la sovrascrittura di tutti i pacchetti esistenti.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-203">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="e3fbe-204">*Sovrascrivi tutto* indica a NuGet per sovrascrivere tutti i pacchetti esistenti.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-204">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="e3fbe-205">Opzioni di disinstallazione</span><span class="sxs-lookup"><span data-stu-id="e3fbe-205">Uninstall Options</span></span>

<span data-ttu-id="e3fbe-206">(Non disponibile per tutti i tipi di progetto).</span><span class="sxs-lookup"><span data-stu-id="e3fbe-206">(Not available for all project types.)</span></span>

<span data-ttu-id="e3fbe-207">**Rimuovere le dipendenze**: quando è selezionata, consente di rimuovere eventuali pacchetti dipendenti se non si viene fatto riferimento in un' posizione nel progetto.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-207">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="e3fbe-208">**Forza la disinstallazione anche se sono presenti dipendenze su di esso**: quando è selezionata, consente di disinstallare un pacchetto anche se vi fanno ancora riferimento nel progetto.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-208">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="e3fbe-209">Viene in genere utilizzato in combinazione con **rimuovere le dipendenze** per rimuovere un pacchetto e tutti i valori delle dipendenze è installato.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-209">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="e3fbe-210">Utilizzo di questa opzione potrebbe, tuttavia, causare ai riferimenti interrotti nel progetto.</span><span class="sxs-lookup"><span data-stu-id="e3fbe-210">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="e3fbe-211">In questi casi, potrebbe essere necessario [reinstallare tali altri pacchetti](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="e3fbe-211">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
