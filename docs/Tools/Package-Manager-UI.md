---
title: Riferimento all'interfaccia utente di gestione pacchetti di NuGet | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
description: Istruzioni per l'utilizzo di UI Gestione pacchetti NuGet in Visual Studio per l'utilizzo di pacchetti NuGet.
keywords: UI NuGet, Gestione pacchetti NuGet dell'interfaccia utente, NuGet in Visual Studio, la gestione pacchetti NuGet, interfaccia utente di NuGet, gestione di pacchetti in Visual Studio
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 35bb856ccff43c77af7eac67da4614d83dcdc533
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/08/2018
---
# <a name="nuget-package-manager-ui"></a><span data-ttu-id="5ac47-104">Interfaccia utente di gestione pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="5ac47-104">NuGet Package Manager UI</span></span>

<span data-ttu-id="5ac47-105">L'UI Gestione pacchetti NuGet in Visual Studio in Windows consente di installare, disinstallare e aggiornare i pacchetti NuGet in progetti e soluzioni.</span><span class="sxs-lookup"><span data-stu-id="5ac47-105">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="5ac47-106">Per l'esperienza in Visual Studio per Mac, vedere [pacchetto NuGet un inclusi nel progetto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="5ac47-106">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="5ac47-107">L'UI Package Manager non è inclusa in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="5ac47-107">The Package Manager UI is not included with Visual Studio Code.</span></span>

<span data-ttu-id="5ac47-108">In questo argomento</span><span class="sxs-lookup"><span data-stu-id="5ac47-108">In this topic:</span></span>

- [<span data-ttu-id="5ac47-109">Ricerca e l'installazione di un pacchetto (scheda Sfoglia)</span><span class="sxs-lookup"><span data-stu-id="5ac47-109">Finding and installing a package (Browse tab)</span></span>](#finding-and-installing-a-package)
- [<span data-ttu-id="5ac47-110">La disinstallazione di un pacchetto (scheda installato)</span><span class="sxs-lookup"><span data-stu-id="5ac47-110">Uninstalling a package (Installed tab)</span></span>](#uninstalling-a-package)
- <span data-ttu-id="5ac47-111">[Aggiornamento di un pacchetto (installazione e aggiornamenti schede)](#updating-a-package) (include il ["In modo implicito a cui fa riferimento un SDK" o "AutoReferenced" messaggio](#implicit_reference))</span><span class="sxs-lookup"><span data-stu-id="5ac47-111">[Updating a package (Installed and Updates tabs)](#updating-a-package) (includes the ["Implicitly referenced by an SDK" or "AutoReferenced" message](#implicit_reference))</span></span>
- <span data-ttu-id="5ac47-112">[La gestione dei pacchetti per la soluzione](#managing-packages-for-the-solution) (utilizzo di più progetti contemporaneamente).</span><span class="sxs-lookup"><span data-stu-id="5ac47-112">[Managing packages for the solution](#managing-packages-for-the-solution) (working with multiple projects at the same time).</span></span>
- [<span data-ttu-id="5ac47-113">Origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="5ac47-113">Package sources</span></span>](#package-sources)
- [<span data-ttu-id="5ac47-114">Controllano le opzioni di gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="5ac47-114">Package manager Options control</span></span>](#package-manager-options-control)

> [!Note]
> <span data-ttu-id="5ac47-115">Assenza di gestione pacchetti NuGet in Visual Studio 2015, controllare **strumenti > estensioni e aggiornamenti...**  e cercare il *Gestione pacchetti NuGet* estensione.</span><span class="sxs-lookup"><span data-stu-id="5ac47-115">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="5ac47-116">Se non si riesce a usare il programma di installazione di estensioni in Visual Studio, scaricare l'estensione direttamente da [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="5ac47-116">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="5ac47-117">In Visual Studio 2017, vengano automaticamente installati con NuGet e gestione pacchetti NuGet. Carichi di lavoro correlati alla rete.</span><span class="sxs-lookup"><span data-stu-id="5ac47-117">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="5ac47-118">Installare singolarmente selezionando il **singoli componenti > codice strumenti > Gestione pacchetti NuGet** opzione nel programma di installazione di Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="5ac47-118">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="5ac47-119">Ricerca e l'installazione di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="5ac47-119">Finding and installing a package</span></span>

1. <span data-ttu-id="5ac47-120">In **Esplora**, fare doppio clic su uno **riferimenti** o un progetto e selezionare **Gestisci pacchetti NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="5ac47-120">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Gestire l'opzione di menu pacchetti NuGet](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="5ac47-122">Il **Sfoglia** scheda Visualizza pacchetti di popolarità dall'origine attualmente selezionata (vedere [origini del pacchetto](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="5ac47-122">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="5ac47-123">Ricerca di un pacchetto specifico tramite la casella di ricerca in alto a sinistra.</span><span class="sxs-lookup"><span data-stu-id="5ac47-123">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="5ac47-124">Selezionare un pacchetto dall'elenco per visualizzare le informazioni, che consente anche di **installare** pulsante insieme a un elenco a discesa selezione della versione.</span><span class="sxs-lookup"><span data-stu-id="5ac47-124">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Gestisci NuGet pacchetti finestra di dialogo Sfoglia scheda](media/Search.png)

1. <span data-ttu-id="5ac47-126">Selezionare la versione desiderata dall'elenco a discesa e selezionare **installare**.</span><span class="sxs-lookup"><span data-stu-id="5ac47-126">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="5ac47-127">Visual Studio installa il pacchetto e le relative dipendenze nel progetto.</span><span class="sxs-lookup"><span data-stu-id="5ac47-127">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="5ac47-128">Potrebbe essere richiesto di accettare le condizioni di licenza.</span><span class="sxs-lookup"><span data-stu-id="5ac47-128">You may be asked to accept license terms.</span></span> <span data-ttu-id="5ac47-129">Quando l'installazione è stata completata, i pacchetti aggiunti vengono visualizzati di **installato** scheda. Vengono inoltre elencati i pacchetti nel **riferimenti** nodo di Esplora soluzioni, che indica che è possibile farvi riferimento nel progetto con `using` istruzioni.</span><span class="sxs-lookup"><span data-stu-id="5ac47-129">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Riferimenti in Esplora soluzioni](media/References.png)

> [!Tip]
    > <span data-ttu-id="5ac47-131">Per includere le versioni non definitive nella ricerca e che le versioni non definitive disponibili nella versione di riepilogo a discesa, selezionare il **Includi versione preliminare** opzione.</span><span class="sxs-lookup"><span data-stu-id="5ac47-131">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="5ac47-132">La disinstallazione di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="5ac47-132">Uninstalling a package</span></span>

1. <span data-ttu-id="5ac47-133">In **Esplora**, fare doppio clic su uno **riferimenti** o il progetto desiderato e scegliere **Gestisci pacchetti NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="5ac47-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="5ac47-134">Selezionare il **installato** scheda.</span><span class="sxs-lookup"><span data-stu-id="5ac47-134">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="5ac47-135">Selezionare il pacchetto da disinstallare (utilizzo della ricerca per filtrare l'elenco, se necessario) e selezionare **Disinstalla**.</span><span class="sxs-lookup"><span data-stu-id="5ac47-135">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![La disinstallazione di un pacchetto](media/UninstallPackage.png)

1. <span data-ttu-id="5ac47-137">Si noti che il **versione provvisoria di inclusione** e **origine pacchetto** controlli non hanno alcun effetto durante la disinstallazione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5ac47-137">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="5ac47-138">Aggiornamento di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="5ac47-138">Updating a package</span></span>

1. <span data-ttu-id="5ac47-139">In **Esplora**, fare doppio clic su uno **riferimenti** o il progetto desiderato e scegliere **Gestisci pacchetti NuGet...** . (In progetti di siti web, fare clic di **Bin** cartella.)</span><span class="sxs-lookup"><span data-stu-id="5ac47-139">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="5ac47-140">Selezionare il **aggiornamenti** scheda per visualizzare i pacchetti con aggiornamenti disponibili dalle origini del pacchetto selezionato.</span><span class="sxs-lookup"><span data-stu-id="5ac47-140">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="5ac47-141">Selezionare **Includi versione preliminare** per includere i pacchetti con versione non definitiva nel relativo elenco.</span><span class="sxs-lookup"><span data-stu-id="5ac47-141">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="5ac47-142">Selezionare il pacchetto da aggiornare, selezionare la versione desiderata dall'elenco a discesa a destra e selezionare **aggiornare**.</span><span class="sxs-lookup"><span data-stu-id="5ac47-142">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Aggiornamento di un pacchetto](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="5ac47-144">Per alcuni pacchetti, il **aggiornamento** pulsante è disabilitato e viene visualizzato un messaggio che informa che "in modo implicito fa riferimento un SDK" (o "AutoReferenced").</span><span class="sxs-lookup"><span data-stu-id="5ac47-144">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="5ac47-145">Il messaggio indica che il pacchetto, ad esempio Microsoft.NETCore.App o Microsoft.NETStandard.Library, fa parte di un SDK o di framework più grande e non deve essere aggiornato in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="5ac47-145">The message indicates that the package, such as Microsoft.NETCore.App or Microsoft.NETStandard.Library, is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="5ac47-146">(Tali pacchetti internamente sono contrassegnati con `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Per aggiornare il pacchetto, aggiornare il SDK a cui appartiene.</span><span class="sxs-lookup"><span data-stu-id="5ac47-146">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) To update the package, update the SDK to which it belongs.</span></span>

    ![Pacchetto di esempio è stato contrassegnato come in modo implicito i riferimenti o AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="5ac47-148">Per aggiornare più pacchetti con le versioni più recenti, selezionarli nell'elenco e selezionare il **aggiornare** pulsante sopra l'elenco.</span><span class="sxs-lookup"><span data-stu-id="5ac47-148">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="5ac47-149">È inoltre possibile aggiornare un singolo pacchetto dal **installato** scheda. In questo caso, i dettagli per il pacchetto includono un selettore di versione (soggetto al **versione provvisoria di inclusione** opzione) e un **aggiornamento** pulsante.</span><span class="sxs-lookup"><span data-stu-id="5ac47-149">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="5ac47-150">La gestione dei pacchetti per la soluzione</span><span class="sxs-lookup"><span data-stu-id="5ac47-150">Managing packages for the solution</span></span>

<span data-ttu-id="5ac47-151">La gestione dei pacchetti per una soluzione è un modo pratico per più progetti contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="5ac47-151">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="5ac47-152">Selezionare il **strumenti > Gestione pacchetti NuGet > Gestisci pacchetti NuGet per la soluzione...**  menu comando o la soluzione e scegliere **Gestisci pacchetti NuGet...** :</span><span class="sxs-lookup"><span data-stu-id="5ac47-152">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Gestisci pacchetti NuGet per la soluzione](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="5ac47-154">Quando la gestione dei pacchetti per la soluzione, l'interfaccia utente consente di selezionare i progetti che sono interessati dalle operazioni:</span><span class="sxs-lookup"><span data-stu-id="5ac47-154">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Selettore di progetto per la gestione di pacchetti per la soluzione](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="5ac47-156">Consolidare scheda</span><span class="sxs-lookup"><span data-stu-id="5ac47-156">Consolidate tab</span></span>

<span data-ttu-id="5ac47-157">Gli sviluppatori in genere viene considerano una prassi sbagliata utilizzare versioni diverse dello stesso pacchetto NuGet in progetti diversi nella stessa soluzione.</span><span class="sxs-lookup"><span data-stu-id="5ac47-157">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="5ac47-158">Quando si sceglie di gestire i pacchetti per una soluzione, la UI Package Manager fornisce un **consolida** scheda in cui è possibile visualizzare facilmente in cui i pacchetti con numeri di versione diversi vengono utilizzati da diversi progetti nella soluzione:</span><span class="sxs-lookup"><span data-stu-id="5ac47-158">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Scheda consolidare dell'interfaccia utente di gestione pacchetti](media/ConsolidateTab.png)

<span data-ttu-id="5ac47-160">In questo esempio, il progetto ClassLibrary1 utilizza EntityFramework 6.2.0, considerando che utilizza EntityFramework 6.1.0 ConsoleApp1.</span><span class="sxs-lookup"><span data-stu-id="5ac47-160">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="5ac47-161">Per consolidare versioni del pacchetto, effettuare le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="5ac47-161">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="5ac47-162">Selezionare i progetti da aggiornare nell'elenco di progetto.</span><span class="sxs-lookup"><span data-stu-id="5ac47-162">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="5ac47-163">Selezionare la versione da utilizzare in tutti i progetti nel **versione** controllo, ad esempio EntityFramework 6.2.0.</span><span class="sxs-lookup"><span data-stu-id="5ac47-163">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="5ac47-164">Selezionare il **installare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="5ac47-164">Select the **Install** button.</span></span>

<span data-ttu-id="5ac47-165">Package Manager installa la versione del pacchetto selezionato in tutti i progetti selezionati, dopo il quale il pacchetto non viene più visualizzata sul **consolida** scheda.</span><span class="sxs-lookup"><span data-stu-id="5ac47-165">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="5ac47-166">Origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="5ac47-166">Package sources</span></span>

<span data-ttu-id="5ac47-167">Per modificare l'origine da cui Visual Studio Ottiene i pacchetti, selezionare uno dal selettore di origine:</span><span class="sxs-lookup"><span data-stu-id="5ac47-167">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Selettore di origine del pacchetto nella gestione dei pacchetti dell'interfaccia utente](media/PackageSourceDropDown.png)

<span data-ttu-id="5ac47-169">Per gestire l'origine del pacchetto:</span><span class="sxs-lookup"><span data-stu-id="5ac47-169">To manage package sources:</span></span>

1. <span data-ttu-id="5ac47-170">Selezionare il **impostazioni** icona nell'UI Package Manager descritti di seguito oppure utilizzare il **strumenti > Opzioni** comando e scorrere fino a **Gestione pacchetti NuGet**:</span><span class="sxs-lookup"><span data-stu-id="5ac47-170">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Icona di impostazioni dell'interfaccia utente Gestione pacchetto](media/PackageSourceSettings.png)

1. <span data-ttu-id="5ac47-172">Selezionare il **origini pacchetti** nodo:</span><span class="sxs-lookup"><span data-stu-id="5ac47-172">Select the **Package Sources** node:</span></span>

    ![Opzioni di origini del pacchetto](media/options.png)

1. <span data-ttu-id="5ac47-174">Per aggiungere un'origine, selezionare  **+** , modificare il nome, immettere l'URL o percorso di **origine** controllo e scegliere **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="5ac47-174">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="5ac47-175">L'origine verrà visualizzato nell'elenco a discesa del selettore.</span><span class="sxs-lookup"><span data-stu-id="5ac47-175">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="5ac47-176">Per modificare un'origine del pacchetto, selezionarlo, apportare le modifiche apportate nel **nome** e **origine** finestre e selezionare **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="5ac47-176">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="5ac47-177">Per disabilitare un'origine del pacchetto, deselezionare la casella a sinistra del nome nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="5ac47-177">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="5ac47-178">Per rimuovere un'origine del pacchetto, selezionarlo e quindi selezionare il **X** pulsante.</span><span class="sxs-lookup"><span data-stu-id="5ac47-178">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="5ac47-179">Utilizzare le frecce su e freccia giù per modificare l'ordine di priorità delle origini pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5ac47-179">Use the up and down arrow buttons to change the priority order of the package sources.</span></span> <span data-ttu-id="5ac47-180">Durante il ripristino dei pacchetti per un progetto, Visual Studio cerca queste origini in ordine di priorità.</span><span class="sxs-lookup"><span data-stu-id="5ac47-180">Visual Studio searches these sources in the priority order when restoring packages for a project.</span></span> <span data-ttu-id="5ac47-181">Per ulteriori informazioni, vedere [ripristino del pacchetto](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="5ac47-181">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="5ac47-182">Se un'origine del pacchetto viene nuovamente visualizzato dopo l'eliminazione, potrebbe essere elencato in un livello di computer o utente `NuGet.Config` file.</span><span class="sxs-lookup"><span data-stu-id="5ac47-182">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="5ac47-183">Vedere [il comportamento di configurazione NuGet](../consume-packages/configuring-nuget-behavior.md) per il percorso di questi file, quindi rimuovere l'origine modificando i file manualmente o utilizzando il [nuget origini comando](../tools/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="5ac47-183">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="5ac47-184">Controllano le opzioni di gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="5ac47-184">Package manager Options control</span></span>

<span data-ttu-id="5ac47-185">Quando si seleziona un pacchetto, la UI Package Manager consente di visualizzare una piccola, espandibile **opzioni** controllo sotto il selettore di versione (illustrato di seguito sia compresso ed esteso).</span><span class="sxs-lookup"><span data-stu-id="5ac47-185">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="5ac47-186">Si noti che per un progetto solo tipi di **finestra di anteprima mostra** opzione è disponibile.</span><span class="sxs-lookup"><span data-stu-id="5ac47-186">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Opzioni di gestione pacchetti](media/PackageManagerUIOptions.png)

<span data-ttu-id="5ac47-188">Le sezioni seguenti illustrano queste opzioni.</span><span class="sxs-lookup"><span data-stu-id="5ac47-188">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="5ac47-189">Mostra finestra di anteprima</span><span class="sxs-lookup"><span data-stu-id="5ac47-189">Show preview window</span></span>

<span data-ttu-id="5ac47-190">Quando selezionata, una finestra modale Visualizza che le dipendenze di un pacchetto scelto prima di installata il pacchetto:</span><span class="sxs-lookup"><span data-stu-id="5ac47-190">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Finestra di dialogo Anteprima esempio](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="5ac47-192">Installazione e le opzioni di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="5ac47-192">Install and Update Options</span></span>

<span data-ttu-id="5ac47-193">(Non disponibile per tutti i tipi di progetto).</span><span class="sxs-lookup"><span data-stu-id="5ac47-193">(Not available for all project types.)</span></span>

<span data-ttu-id="5ac47-194">**Comportamento di dipendenza** Configura modalità NuGet decide quali versioni dei pacchetti dipendenti da installare:</span><span class="sxs-lookup"><span data-stu-id="5ac47-194">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="5ac47-195">*Ignorare le dipendenze* ignora l'installazione di tutte le dipendenze, che in genere si interrompe il pacchetto da installare.</span><span class="sxs-lookup"><span data-stu-id="5ac47-195">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="5ac47-196">*Più basso* [Default] consente di installare la dipendenza con il numero di versione minima che soddisfi i requisiti del pacchetto scelto primario.</span><span class="sxs-lookup"><span data-stu-id="5ac47-196">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="5ac47-197">*Più alto Patch* installa la versione con gli stessi numeri di versione principale e secondaria, ma il numero più alto di patch.</span><span class="sxs-lookup"><span data-stu-id="5ac47-197">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="5ac47-198">Ad esempio, se la versione 1.2.2 è specificata la versione più recente che inizia con 1.2 verrà quindi installata</span><span class="sxs-lookup"><span data-stu-id="5ac47-198">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="5ac47-199">*Minore più alto* installa la versione con lo stesso numero di versione principale, ma il numero di patch e il numero minore più alto.</span><span class="sxs-lookup"><span data-stu-id="5ac47-199">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="5ac47-200">Se la versione 1.2.2 è specificata, verrà installata la versione più recente che inizia con 1</span><span class="sxs-lookup"><span data-stu-id="5ac47-200">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="5ac47-201">*Più alto* installa la versione disponibile più recente del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5ac47-201">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="5ac47-202">**Azione di conflitti di file** specifica come NuGet deve gestire i pacchetti già esistenti nel progetto o nel computer locale:</span><span class="sxs-lookup"><span data-stu-id="5ac47-202">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="5ac47-203">*Prompt dei comandi* indica NuGet chiedere se mantenere o sovrascrivere i pacchetti esistenti.</span><span class="sxs-lookup"><span data-stu-id="5ac47-203">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="5ac47-204">*Ignora tutto* indica NuGet per ignorare la sovrascrittura di tutti i pacchetti esistenti.</span><span class="sxs-lookup"><span data-stu-id="5ac47-204">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="5ac47-205">*Sovrascrivi tutto* indica NuGet per sovrascrivere i pacchetti esistenti.</span><span class="sxs-lookup"><span data-stu-id="5ac47-205">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="5ac47-206">Opzioni di disinstallazione</span><span class="sxs-lookup"><span data-stu-id="5ac47-206">Uninstall Options</span></span>

<span data-ttu-id="5ac47-207">(Non disponibile per tutti i tipi di progetto).</span><span class="sxs-lookup"><span data-stu-id="5ac47-207">(Not available for all project types.)</span></span>

<span data-ttu-id="5ac47-208">**Rimuovere le dipendenze**: quando è selezionata, rimuove tutti i pacchetti dipendenti se non si viene fatto riferimento in un' posizione nel progetto.</span><span class="sxs-lookup"><span data-stu-id="5ac47-208">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="5ac47-209">**Forza la disinstallazione anche se sono presenti dipendenze**: quando è selezionata, disinstalla un pacchetto anche se vi fa ancora riferimento nel progetto.</span><span class="sxs-lookup"><span data-stu-id="5ac47-209">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="5ac47-210">In genere viene utilizzato in combinazione con **rimuovere le dipendenze** per rimuovere un pacchetto e dalle dipendenze è installato.</span><span class="sxs-lookup"><span data-stu-id="5ac47-210">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="5ac47-211">Questa opzione può tuttavia causare ai riferimenti interrotti nel progetto.</span><span class="sxs-lookup"><span data-stu-id="5ac47-211">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="5ac47-212">In questi casi, potrebbe essere necessario [reinstallare tali altri pacchetti](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="5ac47-212">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
