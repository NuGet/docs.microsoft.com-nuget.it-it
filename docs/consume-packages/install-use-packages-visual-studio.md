---
title: Installare e gestire pacchetti NuGet in Visual Studio
description: Istruzioni per l'uso dell'interfaccia utente di Gestione pacchetti NuGet in Visual Studio per utilizzare pacchetti NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 7e4ea59b9954e787e7ab060adc964f3097a8240b
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419980"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a><span data-ttu-id="38ef1-103">Installare e gestire i pacchetti in Visual Studio con Gestione pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="38ef1-103">Install and manage packages in Visual Studio using the NuGet Package Manager</span></span>

<span data-ttu-id="38ef1-104">L'interfaccia utente di Gestione pacchetti NuGet in Visual Studio in Windows consente di installare, disinstallare e aggiornare facilmente i pacchetti NuGet in progetti e soluzioni.</span><span class="sxs-lookup"><span data-stu-id="38ef1-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="38ef1-105">Per l'esperienza in Visual Studio per Mac, vedere [Inserimento di un pacchetto NuGet nel progetto](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span><span class="sxs-lookup"><span data-stu-id="38ef1-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span></span> <span data-ttu-id="38ef1-106">L'interfaccia utente di Gestione pacchetti non è inclusa in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="38ef1-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="38ef1-107">Se non si trova Gestione pacchetti NuGet in Visual Studio 2015, selezionare **Strumenti > Estensioni e aggiornamenti** e cercare l'estensione *Gestione pacchetti NuGet*.</span><span class="sxs-lookup"><span data-stu-id="38ef1-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="38ef1-108">Se non si è in grado di usare il programma di installazione delle estensioni in Visual Studio, scaricare l'estensione direttamente da [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="38ef1-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="38ef1-109">A partire da Visual Studio 2017, NuGet e Gestione pacchetti NuGet vengono installati automaticamente con qualsiasi carico di lavoro correlato a NET.</span><span class="sxs-lookup"><span data-stu-id="38ef1-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="38ef1-110">Per installarli singolarmente, selezionare **Singoli componenti > Strumenti per il codice > Gestione pacchetti NuGet** nel programma di installazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="38ef1-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="38ef1-111">Trovare e installare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="38ef1-111">Find and install a package</span></span>

1. <span data-ttu-id="38ef1-112">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Riferimenti** o su un progetto e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="38ef1-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Opzione di menu Gestisci pacchetti NuGet](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="38ef1-114">La scheda **Sfoglia** visualizza i pacchetti in base alla popolarità dall'origine attualmente selezionata (vedere [Origini dei pacchetti](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="38ef1-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="38ef1-115">Cercare un pacchetto specifico usando la casella di ricerca in alto a sinistra.</span><span class="sxs-lookup"><span data-stu-id="38ef1-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="38ef1-116">Selezionare un pacchetto nell'elenco per visualizzarne le informazioni. In questo modo viene anche abilitato il pulsante **Installa** insieme a un elenco a discesa per la selezione della versione.</span><span class="sxs-lookup"><span data-stu-id="38ef1-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Finestra di dialogo Gestisci pacchetti NuGet, scheda Sfoglia](media/Search.png)

1. <span data-ttu-id="38ef1-118">Selezionare la versione desiderata nell'elenco a discesa e selezionare **Installa**.</span><span class="sxs-lookup"><span data-stu-id="38ef1-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="38ef1-119">Visual Studio installa il pacchetto e le relative dipendenze nel progetto.</span><span class="sxs-lookup"><span data-stu-id="38ef1-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="38ef1-120">Potrebbe essere richiesto di accettare le condizioni di licenza.</span><span class="sxs-lookup"><span data-stu-id="38ef1-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="38ef1-121">Al termine dell'installazione, i pacchetti aggiunti verranno visualizzati nella scheda **Installati**. I pacchetti sono elencati anche nel nodo **Riferimenti** di Esplora soluzioni, a indicare che è possibile farvi riferimento nel progetto con istruzioni `using`.</span><span class="sxs-lookup"><span data-stu-id="38ef1-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Riferimenti in Esplora soluzioni](media/References.png)

> [!Tip]
> <span data-ttu-id="38ef1-123">Per includere le versioni preliminari nella ricerca e per rendere disponibili le versioni preliminari nell'elenco a discesa delle versioni, selezionare l'opzione **Includi versione preliminare**.</span><span class="sxs-lookup"><span data-stu-id="38ef1-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="38ef1-124">Disinstalla un pacchetto</span><span class="sxs-lookup"><span data-stu-id="38ef1-124">Uninstall a package</span></span>

1. <span data-ttu-id="38ef1-125">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Riferimenti** o sul progetto desiderato e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="38ef1-125">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="38ef1-126">Selezionare la scheda **Installati**.</span><span class="sxs-lookup"><span data-stu-id="38ef1-126">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="38ef1-127">Selezionare il pacchetto da disinstallare (usando la ricerca per filtrare l'elenco, se necessario) e selezionare **Disinstalla**.</span><span class="sxs-lookup"><span data-stu-id="38ef1-127">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Disinstallazione di un pacchetto](media/UninstallPackage.png)

1. <span data-ttu-id="38ef1-129">Si noti che i controlli **Includi versione preliminare** e **Origine pacchetto** non hanno effetto quando si disinstallano i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="38ef1-129">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="38ef1-130">Aggiornare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="38ef1-130">Update a package</span></span>

1. <span data-ttu-id="38ef1-131">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Riferimenti** o sul progetto desiderato e scegliere **Gestisci pacchetti NuGet**. (Nei progetti per siti Web fare clic con il pulsante destro del mouse sulla cartella **Bin**.)</span><span class="sxs-lookup"><span data-stu-id="38ef1-131">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="38ef1-132">Selezionare la scheda **Aggiornamenti** per visualizzare i pacchetti con aggiornamenti disponibili dalle origini dei pacchetti selezionate.</span><span class="sxs-lookup"><span data-stu-id="38ef1-132">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="38ef1-133">Selezionare **Includi versione preliminare** per includere i pacchetti di versioni preliminari nell'elenco degli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="38ef1-133">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="38ef1-134">Selezionare il pacchetto da aggiornare, selezionare la versione desiderata nell'elenco a discesa a destra e selezionare **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="38ef1-134">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Aggiornamento di un pacchetto](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="38ef1-136">Per alcuni pacchetti, il pulsante **Aggiorna** è disabilitato e viene visualizzato un messaggio che informa che "Un SDK vi fa riferimento in modo implicito" (o "con riferimento automatico").</span><span class="sxs-lookup"><span data-stu-id="38ef1-136">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="38ef1-137">Questo messaggio indica che il pacchetto fa parte di un framework o di un SDK più ampio e non deve essere aggiornato in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="38ef1-137">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="38ef1-138">(Questi pacchetti sono contrassegnati internamente con `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Ad esempio, `Microsoft.NETCore.App` fa parte di .NET Core SDK e la versione del pacchetto non corrisponde alla versione del framework di runtime usato dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="38ef1-138">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="38ef1-139">È necessario [aggiornare l'installazione di .NET Core](https://aka.ms/dotnet-download) per ottenere le nuove versioni del runtime di ASP.NET Core e .NET Core.</span><span class="sxs-lookup"><span data-stu-id="38ef1-139">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="38ef1-140">[Per informazioni dettagliate sui metapacchetti e sul controllo delle versioni di .NET Core, vedere questo documento](/dotnet/core/packages).</span><span class="sxs-lookup"><span data-stu-id="38ef1-140">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="38ef1-141">Si applica ai seguenti pacchetti di uso comune:</span><span class="sxs-lookup"><span data-stu-id="38ef1-141">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="38ef1-142">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="38ef1-142">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="38ef1-143">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="38ef1-143">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="38ef1-144">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="38ef1-144">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="38ef1-145">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="38ef1-145">NETStandard.Library</span></span>

    ![Pacchetto di esempio contrassegnato come con riferimento implicito o riferimento automatico](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="38ef1-147">Per aggiornare più pacchetti alle versioni più recenti, selezionarli nell'elenco e selezionare il pulsante **Aggiorna** sopra l'elenco.</span><span class="sxs-lookup"><span data-stu-id="38ef1-147">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="38ef1-148">È anche possibile aggiornare un singolo pacchetto dalla scheda **Installati**. In questo caso, i dettagli per il pacchetto includono un selettore di versione (soggetto all'opzione **Includi versione preliminare**) e un pulsante **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="38ef1-148">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="manage-packages-for-the-solution"></a><span data-ttu-id="38ef1-149">Gestisci i pacchetti per la soluzione</span><span class="sxs-lookup"><span data-stu-id="38ef1-149">Manage packages for the solution</span></span>

<span data-ttu-id="38ef1-150">La gestione dei pacchetti per una soluzione è un metodo pratico per utilizzare più progetti contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="38ef1-150">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="38ef1-151">Scegliere **Strumenti > Gestione pacchetti NuGet > Gestisci pacchetti NuGet per la soluzione** oppure fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Gestisci pacchetti NuGet**:</span><span class="sxs-lookup"><span data-stu-id="38ef1-151">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Gestisci pacchetti NuGet per la soluzione](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="38ef1-153">Quando si gestiscono i pacchetti per la soluzione, l'interfaccia utente consente di selezionare i progetti interessati dalle operazioni:</span><span class="sxs-lookup"><span data-stu-id="38ef1-153">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Selettore di progetto durante la gestione dei pacchetti per la soluzione](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="38ef1-155">Scheda Consolida</span><span class="sxs-lookup"><span data-stu-id="38ef1-155">Consolidate tab</span></span>

<span data-ttu-id="38ef1-156">Gli sviluppatori in genere considerano una procedura non corretta l'uso di versioni diverse dello stesso pacchetto NuGet in progetti diversi nella stessa soluzione.</span><span class="sxs-lookup"><span data-stu-id="38ef1-156">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="38ef1-157">Quando si sceglie di gestire i pacchetti per una soluzione, l'interfaccia utente di Gestione pacchetti include una scheda **Consolida** in cui è possibile visualizzare facilmente i pacchetti con numeri di versione distinti usati da progetti diversi nella soluzione:</span><span class="sxs-lookup"><span data-stu-id="38ef1-157">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Scheda Consolida dell'interfaccia utente di Gestione pacchetti](media/ConsolidateTab.png)

<span data-ttu-id="38ef1-159">In questo esempio, il progetto ClassLibrary1 usa EntityFramework 6.2.0, mentre ConsoleApp1 usa EntityFramework 6.1.0.</span><span class="sxs-lookup"><span data-stu-id="38ef1-159">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="38ef1-160">Per consolidare le versioni dei pacchetti, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="38ef1-160">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="38ef1-161">Selezionare i progetti da aggiornare nell'elenco dei progetti.</span><span class="sxs-lookup"><span data-stu-id="38ef1-161">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="38ef1-162">Selezionare la versione da usare in tutti i progetti nel controllo **Versione**, ad esempio EntityFramework 6.2.0.</span><span class="sxs-lookup"><span data-stu-id="38ef1-162">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="38ef1-163">Selezionare il pulsante **Installa**.</span><span class="sxs-lookup"><span data-stu-id="38ef1-163">Select the **Install** button.</span></span>

<span data-ttu-id="38ef1-164">Gestione pacchetti installa la versione del pacchetto selezionata in tutti i progetti selezionati e in seguito il pacchetto non compare più nella scheda **Consolida**.</span><span class="sxs-lookup"><span data-stu-id="38ef1-164">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="38ef1-165">Origini dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="38ef1-165">Package sources</span></span>

<span data-ttu-id="38ef1-166">Per modificare l'origine da cui Visual Studio ottiene i pacchetti, selezionarne una nel selettore delle origini:</span><span class="sxs-lookup"><span data-stu-id="38ef1-166">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Selettore delle origini dei pacchetti nell'interfaccia utente di Gestione pacchetti](media/PackageSourceDropDown.png)

<span data-ttu-id="38ef1-168">Per gestire le origini dei pacchetti:</span><span class="sxs-lookup"><span data-stu-id="38ef1-168">To manage package sources:</span></span>

1. <span data-ttu-id="38ef1-169">Selezionare l'icona **Impostazioni** nell'interfaccia utente di Gestione pacchetti illustrata di seguito oppure usare il comando **Strumenti > Opzioni** e scorrere fino a **Gestione pacchetti NuGet**:</span><span class="sxs-lookup"><span data-stu-id="38ef1-169">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Icona delle impostazioni dell'interfaccia utente di Gestione pacchetti](media/PackageSourceSettings.png)

1. <span data-ttu-id="38ef1-171">Selezionare il nodo **Origini pacchetti**:</span><span class="sxs-lookup"><span data-stu-id="38ef1-171">Select the **Package Sources** node:</span></span>

    ![Opzioni per le origini dei pacchetti](media/options.png)

1. <span data-ttu-id="38ef1-173">Per aggiungere un'origine, selezionare **+** , modificare il nome, immettere l'URL o il percorso nel controllo **Origine** e selezionare **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="38ef1-173">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="38ef1-174">L'origine viene ora visualizzata nell'elenco a discesa del selettore.</span><span class="sxs-lookup"><span data-stu-id="38ef1-174">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="38ef1-175">Per modificare un'origine di pacchetti, selezionarla, apportare modifiche nelle caselle **Nome** e **Origine** e selezionare **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="38ef1-175">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="38ef1-176">Per disabilitare un'origine di pacchetti, deselezionare la casella a sinistra del nome nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="38ef1-176">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="38ef1-177">Per rimuovere un'origine di pacchetti, selezionarla e quindi selezionare il pulsante **X**.</span><span class="sxs-lookup"><span data-stu-id="38ef1-177">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="38ef1-178">L'uso dei pulsanti freccia su e giù non cambia l'ordine di priorità delle origini dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="38ef1-178">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="38ef1-179">Visual Studio ignora l'ordine delle origini dei pacchetti e usa il pacchetto da qualsiasi origine risponde per prima alle richieste.</span><span class="sxs-lookup"><span data-stu-id="38ef1-179">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="38ef1-180">Per altre informazioni, vedere [Ripristino di pacchetti](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="38ef1-180">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="38ef1-181">Se un'origine di pacchetti viene visualizzata nuovamente dopo l'eliminazione, potrebbe essere elencata in un file `NuGet.Config` a livello di computer o di utente.</span><span class="sxs-lookup"><span data-stu-id="38ef1-181">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="38ef1-182">Vedere [Configurazioni NuGet comuni](../consume-packages/configuring-nuget-behavior.md) per il percorso di questi file, quindi rimuovere l'origine modificando manualmente i file o usando il [comando nuget sources](../reference/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="38ef1-182">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../reference/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="38ef1-183">Controllo Opzioni di Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="38ef1-183">Package manager Options control</span></span>

<span data-ttu-id="38ef1-184">Quando si seleziona un pacchetto, l'interfaccia utente di Gestione pacchetti visualizza un piccolo controllo **Opzioni** espandibile sotto il selettore della versione (visualizzato nella figura sia compresso che espanso).</span><span class="sxs-lookup"><span data-stu-id="38ef1-184">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="38ef1-185">Si noti che per alcuni tipi di progetto viene visualizzata solo l'opzione **Visualizza finestra di anteprima**.</span><span class="sxs-lookup"><span data-stu-id="38ef1-185">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Opzioni di Gestione pacchetti](media/PackageManagerUIOptions.png)

<span data-ttu-id="38ef1-187">Nelle sezioni seguenti vengono illustrate queste opzioni.</span><span class="sxs-lookup"><span data-stu-id="38ef1-187">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="38ef1-188">Visualizza finestra di anteprima</span><span class="sxs-lookup"><span data-stu-id="38ef1-188">Show preview window</span></span>

<span data-ttu-id="38ef1-189">Quando questa opzione è selezionata, una finestra modale visualizza le dipendenze di un pacchetto scelto prima dell'installazione del pacchetto:</span><span class="sxs-lookup"><span data-stu-id="38ef1-189">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Finestra di dialogo di anteprima di esempio](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="38ef1-191">Opzioni di installazione e aggiornamento</span><span class="sxs-lookup"><span data-stu-id="38ef1-191">Install and Update Options</span></span>

<span data-ttu-id="38ef1-192">(Non disponibile per tutti i tipi di progetto.)</span><span class="sxs-lookup"><span data-stu-id="38ef1-192">(Not available for all project types.)</span></span>

<span data-ttu-id="38ef1-193">**Comportamento dipendenza** configura il modo in cui NuGet decide quali versioni dei pacchetti dipendenti installare:</span><span class="sxs-lookup"><span data-stu-id="38ef1-193">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="38ef1-194">*Ignora dipendenze* ignora l'installazione di eventuali dipendenze, che in genere può causare problemi di funzionamento per il pacchetto da installare.</span><span class="sxs-lookup"><span data-stu-id="38ef1-194">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="38ef1-195">*Più bassa* [impostazione predefinita] installa la dipendenza con il numero di versione minimo che soddisfa i requisiti del pacchetto scelto primario.</span><span class="sxs-lookup"><span data-stu-id="38ef1-195">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="38ef1-196">*Patch più alta* installa la versione con gli stessi numeri di versione principale e secondaria, ma con il numero di patch più alto.</span><span class="sxs-lookup"><span data-stu-id="38ef1-196">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="38ef1-197">Ad esempio, se viene specificata la versione 1.2.2, verrà installata la versione più recente che inizia con 1.2</span><span class="sxs-lookup"><span data-stu-id="38ef1-197">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="38ef1-198">*Minore più alta* installa la versione con lo stesso numero di versione principale, ma con il numero di versione secondaria e il numero di patch più alti.</span><span class="sxs-lookup"><span data-stu-id="38ef1-198">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="38ef1-199">Se si specifica la versione 1.2.2 verrà installata la versione più recente che inizia con 1</span><span class="sxs-lookup"><span data-stu-id="38ef1-199">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="38ef1-200">*Più alta* installa la versione più alta disponibile del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="38ef1-200">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="38ef1-201">**Azione conflitto file** specifica il modo in cui NuGet deve gestire i pacchetti già esistenti nel progetto o nel computer locale:</span><span class="sxs-lookup"><span data-stu-id="38ef1-201">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="38ef1-202">*Chiedi conferma* indica a NuGet di richiedere se si vogliono mantenere o sovrascrivere i pacchetti esistenti.</span><span class="sxs-lookup"><span data-stu-id="38ef1-202">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="38ef1-203">*Ignora tutto* indica a NuGet di non sovrascrivere eventuali pacchetti esistenti.</span><span class="sxs-lookup"><span data-stu-id="38ef1-203">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="38ef1-204">*Sovrascrivi tutto* indica a NuGet di sovrascrivere eventuali pacchetti esistenti.</span><span class="sxs-lookup"><span data-stu-id="38ef1-204">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="38ef1-205">Opzioni di disinstallazione</span><span class="sxs-lookup"><span data-stu-id="38ef1-205">Uninstall Options</span></span>

<span data-ttu-id="38ef1-206">(Non disponibile per tutti i tipi di progetto.)</span><span class="sxs-lookup"><span data-stu-id="38ef1-206">(Not available for all project types.)</span></span>

<span data-ttu-id="38ef1-207">**Rimuovi dipendenze**: quando si seleziona questa opzione, eventuali pacchetti dipendenti vengono rimossi se non esistono riferimenti altrove nel progetto.</span><span class="sxs-lookup"><span data-stu-id="38ef1-207">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="38ef1-208">**Forza la disinstallazione anche se sono presenti dipendenze**: quando si seleziona questa opzione, un pacchetto viene disinstallato anche se sono ancora presenti riferimenti nel progetto.</span><span class="sxs-lookup"><span data-stu-id="38ef1-208">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="38ef1-209">Questa opzione viene in genere usata in combinazione con **Rimuovi dipendenze** per rimuovere un pacchetto e tutte le eventuali dipendenze installate.</span><span class="sxs-lookup"><span data-stu-id="38ef1-209">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="38ef1-210">L'uso di questa opzione può, tuttavia, causare riferimenti interrotti nel progetto.</span><span class="sxs-lookup"><span data-stu-id="38ef1-210">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="38ef1-211">In questi casi, potrebbe essere necessario [reinstallare gli altri pacchetti](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="38ef1-211">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
