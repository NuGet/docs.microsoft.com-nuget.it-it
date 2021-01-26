---
title: Installare e usare un pacchetto NuGet in Visual Studio
description: Esercitazione dettagliata sul processo di installazione e uso di un pacchetto NuGet in un progetto di Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 55f6a64d90ce8ca628d1ac5c68f8133872a214e0
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775532"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a><span data-ttu-id="e40ff-103">Guida introduttiva: installare e usare un pacchetto in Visual Studio (solo Windows)</span><span class="sxs-lookup"><span data-stu-id="e40ff-103">Quickstart: Install and use a package in Visual Studio (Windows only)</span></span>

<span data-ttu-id="e40ff-104">I pacchetti NuGet contengono codice riutilizzabile che altri sviluppatori rendono disponibile per l'uso nei progetti.</span><span class="sxs-lookup"><span data-stu-id="e40ff-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="e40ff-105">Vedere [Che cos'è NuGet?](../What-is-NuGet.md) per le informazioni di base.</span><span class="sxs-lookup"><span data-stu-id="e40ff-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="e40ff-106">I pacchetti vengono installati in un progetto di Visual Studio usando Gestione pacchetti NuGet, la [console di gestione pacchetti](../consume-packages/install-use-packages-powershell.md)o l'interfaccia della riga di comando [DotNet](install-and-use-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e40ff-106">Packages are installed into a Visual Studio project using the NuGet Package Manager, the [Package Manager Console](../consume-packages/install-use-packages-powershell.md), or the [dotnet CLI](install-and-use-a-package-using-the-dotnet-cli.md).</span></span> <span data-ttu-id="e40ff-107">Questo articolo illustra il processo usando il famoso pacchetto [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) e un progetto Windows Presentation Foundation (WPF).</span><span class="sxs-lookup"><span data-stu-id="e40ff-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Windows Presentation Foundation (WPF) project.</span></span> <span data-ttu-id="e40ff-108">Lo stesso processo si applica a qualsiasi altro progetto .NET o .NET Core.</span><span class="sxs-lookup"><span data-stu-id="e40ff-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="e40ff-109">Al termine dell'installazione, fare riferimento al pacchetto nel codice con `using <namespace>` dove \<namespace\> è specifico del pacchetto in uso.</span><span class="sxs-lookup"><span data-stu-id="e40ff-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="e40ff-110">Dopo avere creato il riferimento, è possibile chiamare il pacchetto tramite la relativa API.</span><span class="sxs-lookup"><span data-stu-id="e40ff-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="e40ff-111">**Iniziare con NuGet.org**: l'esplorazione di *NuGet.org* è il modo in cui gli sviluppatori .NET trovano in genere i componenti che possono riutilizzare nelle proprie applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e40ff-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="e40ff-112">È possibile eseguire una ricerca direttamente in *nuget.org* o trovare e installare pacchetti all'interno di Visual Studio, come illustrato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e40ff-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="e40ff-113">Per informazioni generali, vedere [Trovare e valutare i pacchetti NuGet](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="e40ff-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e40ff-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e40ff-114">Prerequisites</span></span>

- <span data-ttu-id="e40ff-115">Visual Studio 2019 con il carico di lavoro Sviluppo per desktop .NET.</span><span class="sxs-lookup"><span data-stu-id="e40ff-115">Visual Studio 2019 with the .NET Desktop Development workload.</span></span>

<span data-ttu-id="e40ff-116">È possibile installare l'edizione 2019 Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/) o usare le edizioni Professional o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e40ff-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="e40ff-117">Se si usa Visual Studio per Mac, vedere [installare e usare un pacchetto nel Visual Studio per Mac](install-and-use-a-package-in-visual-studio-mac.md).</span><span class="sxs-lookup"><span data-stu-id="e40ff-117">If you're using Visual Studio for Mac, see [Install and use a package in Visual Studio for Mac](install-and-use-a-package-in-visual-studio-mac.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="e40ff-118">Creare un progetto</span><span class="sxs-lookup"><span data-stu-id="e40ff-118">Create a project</span></span>

<span data-ttu-id="e40ff-119">I pacchetti NuGet possono essere installati in qualsiasi progetto .NET, a condizione che il pacchetto supporti lo stesso framework di destinazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="e40ff-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="e40ff-120">Per questa procedura dettagliata, usare una semplice app WPF.</span><span class="sxs-lookup"><span data-stu-id="e40ff-120">For this walkthrough, use a simple WPF app.</span></span> <span data-ttu-id="e40ff-121">Creare un progetto in Visual Studio usando **file**  >  **nuovo progetto**, digitando **.NET** nella casella di ricerca e quindi selezionando l' **app WPF (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="e40ff-121">Create a project in Visual Studio using **File** > **New Project**, typing **.NET** in the search box, and then selecting the **WPF App (.NET Framework)**.</span></span> <span data-ttu-id="e40ff-122">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e40ff-122">Click **Next**.</span></span> <span data-ttu-id="e40ff-123">Quando richiesto, accettare i valori predefiniti per **Framework**.</span><span class="sxs-lookup"><span data-stu-id="e40ff-123">Accept the default values for **Framework** when prompted.</span></span>

<span data-ttu-id="e40ff-124">Visual Studio crea il progetto, che viene aperto in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="e40ff-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="e40ff-125">Aggiungere il pacchetto NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="e40ff-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="e40ff-126">Per installare il pacchetto, è possibile usare Gestione pacchetti NuGet o la console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="e40ff-126">To install the package, you can use either the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="e40ff-127">Quando si installa un pacchetto, NuGet registra la dipendenza nel file di progetto o in un file `packages.config`, a seconda del formato del progetto.</span><span class="sxs-lookup"><span data-stu-id="e40ff-127">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="e40ff-128">Per altre informazioni, vedere [Flusso di lavoro dell'utilizzo di pacchetti](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="e40ff-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="e40ff-129">Gestione pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="e40ff-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="e40ff-130">In Esplora soluzioni fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e40ff-130">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Comando Gestisci pacchetti NuGet per i riferimenti del progetto](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="e40ff-132">Scegliere "nuget.org" come **Origine pacchetto**, selezionare la scheda **Sfoglia**, cercare **Newtonsoft.Json**, selezionare il pacchetto nell'elenco e fare clic su **Installa**:</span><span class="sxs-lookup"><span data-stu-id="e40ff-132">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Individuazione del pacchetto Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

    <span data-ttu-id="e40ff-134">Per altre informazioni su Gestione pacchetti NuGet, vedere [Installare e gestire pacchetti con Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="e40ff-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span></span>

1. <span data-ttu-id="e40ff-135">Accettare eventuali richieste per la licenza.</span><span class="sxs-lookup"><span data-stu-id="e40ff-135">Accept any license prompts.</span></span>

1. <span data-ttu-id="e40ff-136">(Solo Visual Studio 2017) Se viene richiesto di selezionare un formato di gestione dei pacchetti, selezionare **PackageReference nel file di progetto**:</span><span class="sxs-lookup"><span data-stu-id="e40ff-136">(Visual Studio 2017 only) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Selezione di un formato di gestione dei pacchetti](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="e40ff-138">Se viene richiesto di rivedere le modifiche, selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="e40ff-138">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="e40ff-139">Console di Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="e40ff-139">Package Manager Console</span></span>

1. <span data-ttu-id="e40ff-140">Selezionare il comando di menu **strumenti** gestione pacchetti  >  **NuGet**  >  **console** di gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="e40ff-140">Select the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="e40ff-141">Quando si apre la console, verificare che l'elenco a discesa **Progetto predefinito** mostri il progetto in cui si vuole installare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e40ff-141">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="e40ff-142">Se la soluzione include un solo progetto, è già selezionato.</span><span class="sxs-lookup"><span data-stu-id="e40ff-142">If you have a single project in the solution, it is already selected.</span></span>

    ![Selezionare un progetto per il pacchetto](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="e40ff-144">Immettere il comando `Install-Package Newtonsoft.Json` (vedere [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="e40ff-144">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="e40ff-145">Nella finestra della console viene mostrato l'output del comando.</span><span class="sxs-lookup"><span data-stu-id="e40ff-145">The console window shows output for the command.</span></span> <span data-ttu-id="e40ff-146">Gli errori indicano in genere che il pacchetto non è compatibile con il framework di destinazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="e40ff-146">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

   <span data-ttu-id="e40ff-147">Per altre informazioni sulla console di Gestione pacchetti, vedere [Installare e gestire pacchetti con la console di Gestione pacchetti](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e40ff-147">If you want more information on the Package Manager Console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="e40ff-148">Usare l'API Newtonsoft.Json nell'app</span><span class="sxs-lookup"><span data-stu-id="e40ff-148">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="e40ff-149">Con il pacchetto Newtonsoft.Json nel progetto, è possibile chiamare il relativo metodo `JsonConvert.SerializeObject` per convertire un oggetto in una stringa leggibile.</span><span class="sxs-lookup"><span data-stu-id="e40ff-149">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="e40ff-150">Aprire `MainWindow.xaml` e sostituire l'elemento `Grid` esistente con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="e40ff-150">Open `MainWindow.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="e40ff-151">Aprire il file `MainWindow.xaml.cs` (disponibile in Esplora soluzioni nel nodo `MainWindow.xaml`) e inserire il codice seguente all'interno della classe `MainWindow`:</span><span class="sxs-lookup"><span data-stu-id="e40ff-151">Open the `MainWindow.xaml.cs` file (located in Solution Explorer under the `MainWindow.xaml` node), and insert the following code inside the `MainWindow` class:</span></span>

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

1. <span data-ttu-id="e40ff-152">Anche se il pacchetto Newtonsoft.Json è stato aggiunto al progetto, vengono visualizzate sottolineature a zigzag rosse sotto `JsonConvert` perché è richiesta un'istruzione `using` all'inizio del file di codice:</span><span class="sxs-lookup"><span data-stu-id="e40ff-152">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="e40ff-153">Compilare ed eseguire l'app premendo F5 o selezionando **debug**  >  **Avvia debug**:</span><span class="sxs-lookup"><span data-stu-id="e40ff-153">Build and run the app by pressing F5 or selecting **Debug** > **Start Debugging**:</span></span>

    ![Output iniziale dell'app WPF](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="e40ff-155">Selezionare il pulsante per visualizzare il contenuto del controllo TextBlock sostituito con testo JSON:</span><span class="sxs-lookup"><span data-stu-id="e40ff-155">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Output dell'app WPF dopo la selezione del pulsante](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a><span data-ttu-id="e40ff-157">Video correlato</span><span class="sxs-lookup"><span data-stu-id="e40ff-157">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

<span data-ttu-id="e40ff-158">Trova altri video su NuGet su [Channel 9](https://channel9.msdn.com/Series/NuGet-101) e [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="e40ff-158">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e40ff-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e40ff-159">Next steps</span></span>

<span data-ttu-id="e40ff-160">È stato installato e usato il primo pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="e40ff-160">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e40ff-161">Installare e gestire pacchetti con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e40ff-161">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="e40ff-162">Installare e gestire pacchetti con la console di Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="e40ff-162">Install and manage packages using Package Manager Console</span></span>](../consume-packages/install-use-packages-powershell.md)

<span data-ttu-id="e40ff-163">Per esplorare in modo più approfondito ciò che NuGet può offrire, selezionare i collegamenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="e40ff-163">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="e40ff-164">Panoramica e flusso di lavoro dell'utilizzo di pacchetti</span><span class="sxs-lookup"><span data-stu-id="e40ff-164">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="e40ff-165">Ricerca e scelta di pacchetti</span><span class="sxs-lookup"><span data-stu-id="e40ff-165">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="e40ff-166">Riferimenti ai pacchetti nei file di progetto</span><span class="sxs-lookup"><span data-stu-id="e40ff-166">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
