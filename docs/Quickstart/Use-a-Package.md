---
title: Guida introduttiva all'uso di pacchetti NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: Un'esercitazione dettagliata sul processo di installazione e uso di un pacchetto NuGet in un progetto.
keywords: installare NuGet, utilizzo di un pacchetto NuGet, installazione di pacchetti NuGet, riferimenti ai pacchetti NuGet, uso di pacchetti NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 897419d1e49f12d54fbb996a2462e06e32933e65
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2018
---
# <a name="install-and-use-a-package"></a><span data-ttu-id="a27d9-104">Installare e usare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="a27d9-104">Install and use a package</span></span>

<span data-ttu-id="a27d9-105">I pacchetti NuGet sono unità di codice riutilizzabile che altri sviluppatori rendono disponibili per l'uso nei progetti.</span><span class="sxs-lookup"><span data-stu-id="a27d9-105">NuGet packages are units of reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="a27d9-106">Vedere [Che cos'è NuGet?](../What-is-NuGet.md) per le informazioni di base.</span><span class="sxs-lookup"><span data-stu-id="a27d9-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span>

[!INCLUDE [install-methods](../includes/install-methods.md)]

<span data-ttu-id="a27d9-107">Al termine dell'installazione, fare riferimento al pacchetto nel codice con `using <namespace>`, dove \<spazio dei nomi\> è specifico per il pacchetto in uso.</span><span class="sxs-lookup"><span data-stu-id="a27d9-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="a27d9-108">Dopo avere creato il riferimento, è possibile chiamare il pacchetto tramite la relativa API.</span><span class="sxs-lookup"><span data-stu-id="a27d9-108">Once the reference is made, you can call the package through its API.</span></span>

<span data-ttu-id="a27d9-109">La parte restante di questo argomento illustra il processo di utilizzo dell'interfaccia utente di Gestione pacchetti per installare il popolare pacchetto [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) in un progetto di piattaforma UWP (Universal Windows Platform).</span><span class="sxs-lookup"><span data-stu-id="a27d9-109">The remainder of this topic walks through the process of using the Package Manager UI to install the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package in a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="a27d9-110">Viene quindi illustrato un esempio di uso del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a27d9-110">It then shows an example of using the package.</span></span> <span data-ttu-id="a27d9-111">Il flusso di lavoro da usare è simile a quello per altri pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="a27d9-111">You use a similar workflow for other NuGet packages.</span></span>

- [<span data-ttu-id="a27d9-112">Installare i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a27d9-112">Install pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="a27d9-113">Creare un progetto</span><span class="sxs-lookup"><span data-stu-id="a27d9-113">Create a project</span></span>](#create-a-project)
- [<span data-ttu-id="a27d9-114">Aggiungere il pacchetto NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="a27d9-114">Add the Newtonsoft.Json NuGet package</span></span>](#add-the-newtonsoftjson-nuget-package)
- [<span data-ttu-id="a27d9-115">Usare l'API Newtonsoft.Json nell'app</span><span class="sxs-lookup"><span data-stu-id="a27d9-115">Use the Newtonsoft.Json API in the app</span></span>](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> <span data-ttu-id="a27d9-116">**Iniziare con nuget.org**: l'installazione di pacchetti da nuget.org è un flusso di lavoro comune usato dagli sviluppatori .NET per trovare componenti utilizzabili nelle loro applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a27d9-116">**Start with nuget.org**: Installing packages from nuget.org is a common workflow that .NET developers use to find components they can use in their own applications.</span></span> <span data-ttu-id="a27d9-117">È sempre possibile eseguire una ricerca direttamente su nuget.org o trovare e installare pacchetti all'interno di Visual Studio, come illustrato in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="a27d9-117">You can always search nuget.org directly or find and install packages within Visual Studio as shown in this topic.</span></span>

## <a name="install-pre-requisites"></a><span data-ttu-id="a27d9-118">Installare i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a27d9-118">Install pre-requisites</span></span>

<span data-ttu-id="a27d9-119">Questa esercitazione richiede Visual Studio 2015 Update 3 con Strumenti per app di Windows universale o Visual Studio 2017 con il carico di lavoro Sviluppo di app per la piattaforma UWP (Universal Windows Platform).</span><span class="sxs-lookup"><span data-stu-id="a27d9-119">This tutorial requires Visual Studio 2015 Update 3 with Tools for Universal Windows Apps, or Visual Studio 2017 with the Universal Windows Platform development workload.</span></span> <span data-ttu-id="a27d9-120">Se Visual Studio è già installato, è possibile eseguire nuovamente il programma di installazione per aggiungere gli strumenti per la piattaforma UWP.</span><span class="sxs-lookup"><span data-stu-id="a27d9-120">If you already have Visual Studio installed, you can run the installer again to add the UWP tools.</span></span>

<span data-ttu-id="a27d9-121">È possibile installare l'edizione Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/) o usare le edizioni Professional o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="a27d9-121">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span> 

## <a name="create-a-project"></a><span data-ttu-id="a27d9-122">Creare un progetto</span><span class="sxs-lookup"><span data-stu-id="a27d9-122">Create a project</span></span>

<span data-ttu-id="a27d9-123">Per installare un pacchetto NuGet, è necessario un progetto basato su .NET in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a27d9-123">To install a NuGet package, you need some kind of .NET-based project in Visual Studio.</span></span> <span data-ttu-id="a27d9-124">Per questa procedura dettagliata è possibile usare una semplice app di Windows Presentation Foundation (WPF) o di Windows universale (UWP):</span><span class="sxs-lookup"><span data-stu-id="a27d9-124">For this walkthrough, you can use use a simple Windows Presentation Foundation (WPF) or Universal Windows (UWP) app:</span></span>

- <span data-ttu-id="a27d9-125">Per WPF (Windows 7+), scegliere **File > Nuovo > Progetto**, espandere **Visual C#**, selezionare **Desktop classico di Windows > App WPF (.NET Framework)** e scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-125">For WPF (Windows 7+), choose **File > New > Project**, expand **Visual C#**, select **Windows Classic Desktop > WPF App (.NET Framework)**, and select **OK**.</span></span>
- <span data-ttu-id="a27d9-126">Per UWP (Windows 10), usare invece **Universale di Windows > App vuota (Windows universale)**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-126">For UWP (Windows 10), use the **Windows Universal > Blank App (Universal Windows)** instead.</span></span> <span data-ttu-id="a27d9-127">Accettare i valori predefiniti per Versione di destinazione e Versione minima quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="a27d9-127">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="a27d9-128">Aggiungere il pacchetto NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="a27d9-128">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="a27d9-129">In Esplora soluzioni fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-129">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Comando Gestisci pacchetti NuGet per i riferimenti del progetto](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="a27d9-131">Scegliere "nuget.org" come **Origine pacchetto**, selezionare la scheda **Sfoglia**, cercare **Newtonsoft.Json**, selezionare il pacchetto nell'elenco e fare clic su **Installa**:</span><span class="sxs-lookup"><span data-stu-id="a27d9-131">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Individuazione del pacchetto Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="a27d9-133">Se viene richiesto di selezionare un formato di gestione del pacchetto, scegliere tra PackageReference (scelta consigliata) e `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="a27d9-133">If prompted to select a package management format, choose between PackageReference (recommended) and `packages.config`:</span></span>

    ![Selezione di un formato di riferimento del pacchetto](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="a27d9-135">Se viene richiesto di rivedere le modifiche, selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-135">If prompted to review changes, select **OK**.</span></span>

1. <span data-ttu-id="a27d9-136">Fare clic con il pulsante destro del mouse sulla soluzione in Esplora soluzioni e selezionare **Compila soluzione**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-136">Right-click the solution in Solution Explorer and select **Build Solution**.</span></span> <span data-ttu-id="a27d9-137">Ciò consente di ripristinare i pacchetti NuGet elencati in **Riferimenti**.</span><span class="sxs-lookup"><span data-stu-id="a27d9-137">This restores any NuGet packages listed under **References**.</span></span> <span data-ttu-id="a27d9-138">Per maggiori dettagli, vedere [Ripristino di pacchetti](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="a27d9-138">For more details, see [Package Restore](../consume-packages/package-restore.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="a27d9-139">Usare l'API Newtonsoft.Json nell'app</span><span class="sxs-lookup"><span data-stu-id="a27d9-139">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="a27d9-140">Con il pacchetto Newtonsoft.Json nel progetto, è possibile chiamare il relativo metodo `JsonConvert.SerializeObject` per convertire un oggetto in una stringa leggibile.</span><span class="sxs-lookup"><span data-stu-id="a27d9-140">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="a27d9-141">Aprire `MainWindow.xaml` (WPF) o `MainPage.xaml` (UWP) e sostituire l'elemento `Grid` esistente con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="a27d9-141">Open `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="a27d9-142">Espandere il nodo `MainWindow.xaml` (WPF) o `MainPage.xaml` (UWP) in Esplora soluzioni, aprire il file `.cs` e inserire il codice seguente all'interno della classe `MainWindow` o `MainPage`, dopo il costruttore:</span><span class="sxs-lookup"><span data-stu-id="a27d9-142">Expand the `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) node in Solution Explorer, open the `.cs` file, and insert the following code inside the `MainWindow` or `MainPage` class, after the constructor:</span></span>

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

1. <span data-ttu-id="a27d9-143">Anche se il pacchetto Newtonsoft.Json è stato aggiunto al progetto, vengono visualizzate sottolineature a zigzag rosse sotto `JsonConvert` perché è richiesta un'istruzione `using`.</span><span class="sxs-lookup"><span data-stu-id="a27d9-143">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement.</span></span> <span data-ttu-id="a27d9-144">Passare il mouse sulla sottolineatura di `JsonConvert`: verrà visualizzato un indicatore Lampadina con l'opzione **Mostra possibili correzioni**:</span><span class="sxs-lookup"><span data-stu-id="a27d9-144">Hover over the underlined `JsonConvert` and you'll see the Lightbulb and the option to **Show potential fixes**:</span></span>

    ![Indicatore Lampadina con il comando Mostra possibili correzioni](media/QS_Use-04-ShowPotentialFixes.png)


1. <span data-ttu-id="a27d9-146">Fare clic su **Mostra possibili correzioni** (o sull'indicatore Lampadina) e selezionare la prima correzione suggerita, `using Newtonsoft.Json;`.</span><span class="sxs-lookup"><span data-stu-id="a27d9-146">Click on **Show potential fixes** (or the Lightbulb) and select the first suggested fix, `using Newtonsoft.Json;`.</span></span> <span data-ttu-id="a27d9-147">La riga necessaria verrà aggiunta all'inizio del file.</span><span class="sxs-lookup"><span data-stu-id="a27d9-147">This adds the necessary line to the top of the file.</span></span>

    ![Indicatore Lampadina con l'opzione per l'aggiunta di un'istruzione Using](media/QS_Use-05-AddUsing.png)

1. <span data-ttu-id="a27d9-149">Compilare ed eseguire l'app premendo F5 o selezionando **Debug > Avvia debug** (in questa immagine è illustrato UWP, per WPF la schermata è simile):</span><span class="sxs-lookup"><span data-stu-id="a27d9-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging** (UWP shown here; WPF is similar):</span></span>

    ![Output iniziale dell'app UWP](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="a27d9-151">Selezionare il pulsante per visualizzare il contenuto del controllo TextBlock sostituito con testo JSON:</span><span class="sxs-lookup"><span data-stu-id="a27d9-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Output dell'app UWP dopo la selezione del pulsante](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a><span data-ttu-id="a27d9-153">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="a27d9-153">Related topics</span></span>

- [<span data-ttu-id="a27d9-154">Panoramica e flusso di lavoro dell'utilizzo di pacchetti</span><span class="sxs-lookup"><span data-stu-id="a27d9-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="a27d9-155">Ricerca e scelta di pacchetti</span><span class="sxs-lookup"><span data-stu-id="a27d9-155">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="a27d9-156">Configurazione del comportamento di NuGet</span><span class="sxs-lookup"><span data-stu-id="a27d9-156">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
