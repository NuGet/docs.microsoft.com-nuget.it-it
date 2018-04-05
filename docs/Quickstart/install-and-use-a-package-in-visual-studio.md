---
title: Guida introduttiva all'uso di pacchetti di NuGet da Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: quickstart
ms.prod: nuget
ms.technology: ''
description: Esercitazione dettagliata sul processo di installazione e uso di un pacchetto NuGet in un progetto di Visual Studio.
keywords: installare NuGet, utilizzo di un pacchetto NuGet, installazione di pacchetti NuGet, riferimenti ai pacchetti NuGet, uso di pacchetti NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4205893cc02cffff8926513a555393d10c046f43
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="5db73-104">Installare e usare un pacchetto in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5db73-104">Install and use a package in Visual Studio</span></span>

<span data-ttu-id="5db73-105">I pacchetti NuGet contengono codice riutilizzabile che altri sviluppatori rendono disponibile per l'uso nei progetti.</span><span class="sxs-lookup"><span data-stu-id="5db73-105">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="5db73-106">Vedere [Che cos'è NuGet?](../What-is-NuGet.md) per le informazioni di base.</span><span class="sxs-lookup"><span data-stu-id="5db73-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="5db73-107">I pacchetti vengono installati in un progetto di Visual Studio usando l'interfaccia utente o la console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5db73-107">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="5db73-108">Questo articolo illustra il processo usando il famoso pacchetto [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) e un progetto Universal Windows Platform (UWP).</span><span class="sxs-lookup"><span data-stu-id="5db73-108">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="5db73-109">Lo stesso processo si applica a qualsiasi altro progetto .NET o .NET Core.</span><span class="sxs-lookup"><span data-stu-id="5db73-109">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="5db73-110">Al termine dell'installazione, fare riferimento al pacchetto nel codice con `using <namespace>`, dove \<spazio dei nomi\> è specifico per il pacchetto in uso.</span><span class="sxs-lookup"><span data-stu-id="5db73-110">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="5db73-111">Dopo avere creato il riferimento, è possibile chiamare il pacchetto tramite la relativa API.</span><span class="sxs-lookup"><span data-stu-id="5db73-111">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="5db73-112">**Iniziare con nuget.org**: le ricerche in nuget.org sono il modo in cui gli sviluppatori di .NET individuano in genere componenti che possono riutilizzare nelle loro applicazioni.</span><span class="sxs-lookup"><span data-stu-id="5db73-112">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="5db73-113">È possibile eseguire una ricerca direttamente in nuget.org o trovare e installare pacchetti all'interno di Visual Studio, come illustrato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="5db73-113">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5db73-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5db73-114">Prerequisites</span></span>

- <span data-ttu-id="5db73-115">Visual Studio 2017 con il carico di lavoro Sviluppo di app per la piattaforma UWP (Universal Windows Platform) oppure</span><span class="sxs-lookup"><span data-stu-id="5db73-115">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="5db73-116">Visual Studio 2015 Update 3 con gli strumenti per app di Windows universali.</span><span class="sxs-lookup"><span data-stu-id="5db73-116">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="5db73-117">È possibile installare l'edizione 2017 Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/) o usare le edizioni Professional o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5db73-117">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="5db73-118">Creare un progetto</span><span class="sxs-lookup"><span data-stu-id="5db73-118">Create a project</span></span>

<span data-ttu-id="5db73-119">I pacchetti NuGet possono essere installati in qualsiasi progetto .NET, a condizione che il pacchetto supporti lo stesso framework di destinazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="5db73-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="5db73-120">Per questa procedura dettagliata viene usata una semplice app di Windows universale (UWP).</span><span class="sxs-lookup"><span data-stu-id="5db73-120">For this walkthrough, use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="5db73-121">Creare un progetto in Visual Studio scegliendo **File > Nuovo progetto** e selezionando **Universale di Windows > App vuota (Windows universale)**.</span><span class="sxs-lookup"><span data-stu-id="5db73-121">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="5db73-122">Accettare i valori predefiniti per Versione di destinazione e Versione minima quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="5db73-122">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="5db73-123">Aggiungere il pacchetto NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="5db73-123">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="5db73-124">Per installare il pacchetto, è possibile usare l'interfaccia utente di Gestione pacchetti o la console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5db73-124">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="5db73-125">Quando si installa un pacchetto, NuGet registra la dipendenza nel file di progetto o in un `packages.config` file.</span><span class="sxs-lookup"><span data-stu-id="5db73-125">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="5db73-126">Per altre informazioni, vedere [Flusso di lavoro dell'utilizzo di pacchetti](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="5db73-126">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="5db73-127">Interfaccia utente di Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="5db73-127">Package Manager UI</span></span>

1. <span data-ttu-id="5db73-128">In Esplora soluzioni fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5db73-128">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Comando Gestisci pacchetti NuGet per i riferimenti del progetto](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="5db73-130">Scegliere "nuget.org" come **Origine pacchetto**, selezionare la scheda **Sfoglia**, cercare **Newtonsoft.Json**, selezionare il pacchetto nell'elenco e fare clic su **Installa**:</span><span class="sxs-lookup"><span data-stu-id="5db73-130">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Individuazione del pacchetto Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="5db73-132">Accettare eventuali richieste per la licenza.</span><span class="sxs-lookup"><span data-stu-id="5db73-132">Accept any license prompts.</span></span>

1. <span data-ttu-id="5db73-133">(Visual Studio 2017) Se viene richiesto di selezionare un formato di gestione dei pacchetti, selezionare **Riferimenti al pacchetto nel file di progetto**:</span><span class="sxs-lookup"><span data-stu-id="5db73-133">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Selezione di un formato di gestione dei pacchetti](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="5db73-135">Se viene richiesto di rivedere le modifiche, selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="5db73-135">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="5db73-136">Console di Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="5db73-136">Package Manager Console</span></span>

1. <span data-ttu-id="5db73-137">Scegliere i comandi di menu **Strumenti > Gestione pacchetti NuGet > Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="5db73-137">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="5db73-138">Quando si apre la console, verificare che l'elenco a discesa **Progetto predefinito** mostri il progetto in cui si vuole installare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5db73-138">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="5db73-139">Se la soluzione include un solo progetto, è già selezionato.</span><span class="sxs-lookup"><span data-stu-id="5db73-139">If you have a single project in the solution, it is already selected.</span></span>

    ![Individuazione del pacchetto Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="5db73-141">Immettere il comando `Install-Package Newtonsoft.json` (vedere [Install-Package](../tools/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="5db73-141">Enter the command `Install-Package Newtonsoft.json` (see [Install-Package](../tools/ps-ref-install-package.md)).</span></span> <span data-ttu-id="5db73-142">Nella finestra della console viene mostrato l'output del comando.</span><span class="sxs-lookup"><span data-stu-id="5db73-142">The console window shows output for the command.</span></span> <span data-ttu-id="5db73-143">Gli errori indicano in genere che il pacchetto non è compatibile con il framework di destinazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="5db73-143">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="5db73-144">Usare l'API Newtonsoft.Json nell'app</span><span class="sxs-lookup"><span data-stu-id="5db73-144">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="5db73-145">Con il pacchetto Newtonsoft.Json nel progetto, è possibile chiamare il relativo metodo `JsonConvert.SerializeObject` per convertire un oggetto in una stringa leggibile.</span><span class="sxs-lookup"><span data-stu-id="5db73-145">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="5db73-146">Aprire `MainPage.xaml` e sostituire l'elemento `Grid` esistente con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="5db73-146">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="5db73-147">Aprire il file `MainPage.xaml.cs` (disponibile in Esplora soluzioni nel nodo `MainPage.xaml`) e inserire il codice seguente all'interno del costruttore `MainPage`:</span><span class="sxs-lookup"><span data-stu-id="5db73-147">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

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

1. <span data-ttu-id="5db73-148">Anche se il pacchetto Newtonsoft.Json è stato aggiunto al progetto, vengono visualizzate sottolineature a zigzag rosse sotto `JsonConvert` perché è richiesta un'istruzione `using` all'inizio del file di codice:</span><span class="sxs-lookup"><span data-stu-id="5db73-148">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.json;
    ```

1. <span data-ttu-id="5db73-149">Compilare ed eseguire l'app premendo F5 o selezionando **Debug > Avvia debug**:</span><span class="sxs-lookup"><span data-stu-id="5db73-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![Output iniziale dell'app UWP](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="5db73-151">Selezionare il pulsante per visualizzare il contenuto del controllo TextBlock sostituito con testo JSON:</span><span class="sxs-lookup"><span data-stu-id="5db73-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Output dell'app UWP dopo la selezione del pulsante](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="5db73-153">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="5db73-153">Related articles</span></span>

- [<span data-ttu-id="5db73-154">Panoramica e flusso di lavoro dell'utilizzo di pacchetti</span><span class="sxs-lookup"><span data-stu-id="5db73-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="5db73-155">Ricerca e scelta di pacchetti</span><span class="sxs-lookup"><span data-stu-id="5db73-155">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="5db73-156">Modi per installare pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="5db73-156">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="5db73-157">Configurazione del comportamento di NuGet</span><span class="sxs-lookup"><span data-stu-id="5db73-157">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
