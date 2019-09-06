---
title: Installare e usare un pacchetto NuGet in Visual Studio
description: Esercitazione dettagliata sul processo di installazione e uso di un pacchetto NuGet in un progetto di Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: d9937a2b087fd88c1e6fd9f07a513b5047bdcf2e
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235077"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a><span data-ttu-id="27a95-103">Avvio rapido: Installare e usare un pacchetto in Visual Studio (solo Windows)</span><span class="sxs-lookup"><span data-stu-id="27a95-103">Quickstart: Install and use a package in Visual Studio (Windows only)</span></span>

<span data-ttu-id="27a95-104">I pacchetti NuGet contengono codice riutilizzabile che altri sviluppatori rendono disponibile per l'uso nei progetti.</span><span class="sxs-lookup"><span data-stu-id="27a95-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="27a95-105">Vedere [Che cos'è NuGet?](../What-is-NuGet.md) per le informazioni di base.</span><span class="sxs-lookup"><span data-stu-id="27a95-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="27a95-106">I pacchetti vengono installati in un progetto di Visual Studio usando Gestione pacchetti NuGet o la console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="27a95-106">Packages are installed into a Visual Studio project using the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="27a95-107">Questo articolo illustra il processo usando il famoso pacchetto [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) e un progetto Windows Presentation Foundation (WPF).</span><span class="sxs-lookup"><span data-stu-id="27a95-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Windows Presentation Foundation (WPF) project.</span></span> <span data-ttu-id="27a95-108">Lo stesso processo si applica a qualsiasi altro progetto .NET o .NET Core.</span><span class="sxs-lookup"><span data-stu-id="27a95-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="27a95-109">Al termine dell'installazione, fare riferimento al pacchetto nel codice con `using <namespace>`, dove \<spazio dei nomi\> è specifico per il pacchetto in uso.</span><span class="sxs-lookup"><span data-stu-id="27a95-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="27a95-110">Dopo avere creato il riferimento, è possibile chiamare il pacchetto tramite la relativa API.</span><span class="sxs-lookup"><span data-stu-id="27a95-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="27a95-111">**Iniziare con nuget.org**: le ricerche in *nuget.org* sono il modo in cui gli sviluppatori di .NET individuano in genere componenti che possono riutilizzare nelle loro applicazioni.</span><span class="sxs-lookup"><span data-stu-id="27a95-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="27a95-112">È possibile eseguire una ricerca direttamente in *nuget.org* o trovare e installare pacchetti all'interno di Visual Studio, come illustrato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="27a95-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="27a95-113">Per informazioni generali, vedere [Trovare e valutare i pacchetti NuGet](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="27a95-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27a95-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="27a95-114">Prerequisites</span></span>

- <span data-ttu-id="27a95-115">Visual Studio 2019 con il carico di lavoro Sviluppo per desktop .NET.</span><span class="sxs-lookup"><span data-stu-id="27a95-115">Visual Studio 2019 with the .NET Desktop Development workload.</span></span>

<span data-ttu-id="27a95-116">È possibile installare l'edizione 2019 Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/) o usare le edizioni Professional o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="27a95-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="27a95-117">Se si usa Visual Studio per Mac, vedere [installare e usare un pacchetto nel Visual Studio per Mac](install-and-use-a-package-in-visual-studio-mac.md).</span><span class="sxs-lookup"><span data-stu-id="27a95-117">If you're using Visual Studio for Mac, see [Install and use a package in Visual Studio for Mac](install-and-use-a-package-in-visual-studio-mac.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="27a95-118">Creare un progetto</span><span class="sxs-lookup"><span data-stu-id="27a95-118">Create a project</span></span>

<span data-ttu-id="27a95-119">I pacchetti NuGet possono essere installati in qualsiasi progetto .NET, a condizione che il pacchetto supporti lo stesso framework di destinazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="27a95-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="27a95-120">Per questa procedura dettagliata, usare una semplice app WPF.</span><span class="sxs-lookup"><span data-stu-id="27a95-120">For this walkthrough, use a simple WPF app.</span></span> <span data-ttu-id="27a95-121">Creare un progetto in Visual Studio: usare **File > Nuovo progetto**, digitare **.NET** nella casella di ricerca e quindi selezionare **App WPF (.NET Framework)** .</span><span class="sxs-lookup"><span data-stu-id="27a95-121">Create a project in Visual Studio using **File > New Project...**, typing **.NET** in the search box, and then selecting the **WPF App (.NET Framework)**.</span></span> <span data-ttu-id="27a95-122">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="27a95-122">Click **Next**.</span></span> <span data-ttu-id="27a95-123">Quando richiesto, accettare i valori predefiniti per **Framework**.</span><span class="sxs-lookup"><span data-stu-id="27a95-123">Accept the default values for **Framework** when prompted.</span></span>

<span data-ttu-id="27a95-124">Visual Studio crea il progetto, che viene aperto in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="27a95-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="27a95-125">Aggiungere il pacchetto NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="27a95-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="27a95-126">Per installare il pacchetto, è possibile usare Gestione pacchetti NuGet o la console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="27a95-126">To install the package, you can use either the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="27a95-127">Quando si installa un pacchetto, NuGet registra la dipendenza nel file di progetto o in un file `packages.config`, a seconda del formato del progetto.</span><span class="sxs-lookup"><span data-stu-id="27a95-127">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="27a95-128">Per altre informazioni, vedere [Flusso di lavoro dell'utilizzo di pacchetti](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="27a95-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="27a95-129">Gestione pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="27a95-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="27a95-130">In Esplora soluzioni fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="27a95-130">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Comando Gestisci pacchetti NuGet per i riferimenti del progetto](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="27a95-132">Scegliere "nuget.org" come **Origine pacchetto**, selezionare la scheda **Sfoglia**, cercare **Newtonsoft.Json**, selezionare il pacchetto nell'elenco e fare clic su **Installa**:</span><span class="sxs-lookup"><span data-stu-id="27a95-132">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Individuazione del pacchetto Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

    <span data-ttu-id="27a95-134">Per altre informazioni su Gestione pacchetti NuGet, vedere [Installare e gestire pacchetti con Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="27a95-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span></span>

1. <span data-ttu-id="27a95-135">Accettare eventuali richieste per la licenza.</span><span class="sxs-lookup"><span data-stu-id="27a95-135">Accept any license prompts.</span></span>

1. <span data-ttu-id="27a95-136">(Solo Visual Studio 2017) Se viene richiesto di selezionare un formato di gestione dei pacchetti, selezionare **PackageReference nel file di progetto**:</span><span class="sxs-lookup"><span data-stu-id="27a95-136">(Visual Studio 2017 only) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Selezione di un formato di gestione dei pacchetti](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="27a95-138">Se viene richiesto di rivedere le modifiche, selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="27a95-138">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="27a95-139">Console di Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="27a95-139">Package Manager Console</span></span>

1. <span data-ttu-id="27a95-140">Scegliere i comandi di menu **Strumenti > Gestione pacchetti NuGet > Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="27a95-140">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="27a95-141">Quando si apre la console, verificare che l'elenco a discesa **Progetto predefinito** mostri il progetto in cui si vuole installare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="27a95-141">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="27a95-142">Se la soluzione include un solo progetto, è già selezionato.</span><span class="sxs-lookup"><span data-stu-id="27a95-142">If you have a single project in the solution, it is already selected.</span></span>

    ![Individuazione del pacchetto Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="27a95-144">Immettere il comando `Install-Package Newtonsoft.Json` (vedere [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="27a95-144">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="27a95-145">Nella finestra della console viene mostrato l'output del comando.</span><span class="sxs-lookup"><span data-stu-id="27a95-145">The console window shows output for the command.</span></span> <span data-ttu-id="27a95-146">Gli errori indicano in genere che il pacchetto non è compatibile con il framework di destinazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="27a95-146">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

   <span data-ttu-id="27a95-147">Per altre informazioni sulla console di Gestione pacchetti, vedere [Installare e gestire pacchetti con la console di Gestione pacchetti](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="27a95-147">If you want more information on the Package Manager Console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="27a95-148">Usare l'API Newtonsoft.Json nell'app</span><span class="sxs-lookup"><span data-stu-id="27a95-148">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="27a95-149">Con il pacchetto Newtonsoft.Json nel progetto, è possibile chiamare il relativo metodo `JsonConvert.SerializeObject` per convertire un oggetto in una stringa leggibile.</span><span class="sxs-lookup"><span data-stu-id="27a95-149">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="27a95-150">Aprire `MainWindow.xaml` e sostituire l'elemento `Grid` esistente con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="27a95-150">Open `MainWindow.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="27a95-151">Aprire il file `MainWindow.xaml.cs` (disponibile in Esplora soluzioni nel nodo `MainWindow.xaml`) e inserire il codice seguente all'interno della classe `MainWindow`:</span><span class="sxs-lookup"><span data-stu-id="27a95-151">Open the `MainWindow.xaml.cs` file (located in Solution Explorer under the `MainWindow.xaml` node), and insert the following code inside the `MainWindow` class:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. <span data-ttu-id="27a95-152">Anche se il pacchetto Newtonsoft.Json è stato aggiunto al progetto, vengono visualizzate sottolineature a zigzag rosse sotto `JsonConvert` perché è richiesta un'istruzione `using` all'inizio del file di codice:</span><span class="sxs-lookup"><span data-stu-id="27a95-152">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="27a95-153">Compilare ed eseguire l'app premendo F5 o selezionando **Debug > Avvia debug**:</span><span class="sxs-lookup"><span data-stu-id="27a95-153">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![Output iniziale dell'app WPF](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="27a95-155">Selezionare il pulsante per visualizzare il contenuto del controllo TextBlock sostituito con testo JSON:</span><span class="sxs-lookup"><span data-stu-id="27a95-155">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Output dell'app WPF dopo la selezione del pulsante](media/QS_Use-07-AppEnd.png)

## <a name="next-steps"></a><span data-ttu-id="27a95-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="27a95-157">Next steps</span></span>

<span data-ttu-id="27a95-158">È stato installato e usato il primo pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="27a95-158">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="27a95-159">Installare e gestire pacchetti con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="27a95-159">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="27a95-160">Installare e gestire pacchetti con la console di Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="27a95-160">Install and manage packages using Package Manager Console</span></span>](../consume-packages/install-use-packages-powershell.md)

<span data-ttu-id="27a95-161">Per esplorare in modo più approfondito ciò che NuGet può offrire, selezionare i collegamenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="27a95-161">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="27a95-162">Panoramica e flusso di lavoro dell'utilizzo di pacchetti</span><span class="sxs-lookup"><span data-stu-id="27a95-162">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="27a95-163">Ricerca e scelta di pacchetti</span><span class="sxs-lookup"><span data-stu-id="27a95-163">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="27a95-164">Riferimenti ai pacchetti nei file di progetto</span><span class="sxs-lookup"><span data-stu-id="27a95-164">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
