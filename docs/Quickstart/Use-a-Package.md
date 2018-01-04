---
title: Guida introduttiva all'uso di pacchetti NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: f31f8259-20a8-4617-880e-5819299372d2
description: Un'esercitazione dettagliata sul processo di installazione e uso di un pacchetto NuGet in un progetto.
keywords: installare NuGet, utilizzo di un pacchetto NuGet, installazione di pacchetti NuGet, riferimenti ai pacchetti NuGet, uso di pacchetti NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bcccc7139de31a8d07e9ed52abfd12fe9e6d687b
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="install-and-use-a-package"></a><span data-ttu-id="ced26-104">Installare e usare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="ced26-104">Install and use a package</span></span>

[!INCLUDE [install-methods](../includes/install-methods.md)]

<span data-ttu-id="ced26-105">Al termine dell'installazione, fare riferimento al pacchetto nel codice con `using <namespace>`, dove \<spazio dei nomi\> è specifico per il pacchetto in uso.</span><span class="sxs-lookup"><span data-stu-id="ced26-105">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="ced26-106">Dopo avere creato il riferimento, è possibile chiamare il pacchetto tramite la relativa API.</span><span class="sxs-lookup"><span data-stu-id="ced26-106">Once the reference is made, you can call the package through its API.</span></span>

<span data-ttu-id="ced26-107">La parte restante di questo argomento illustra il processo di utilizzo dell'interfaccia utente di Gestione pacchetti per installare il popolare pacchetto [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) in un progetto di piattaforma UWP (Universal Windows Platform).</span><span class="sxs-lookup"><span data-stu-id="ced26-107">The remainder of this topic walks through the process of using the Package Manager UI to install the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package in a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="ced26-108">Viene quindi illustrato un esempio di uso del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ced26-108">It then shows an example of using the package.</span></span> <span data-ttu-id="ced26-109">Si usa un flusso di lavoro analogo per quasi tutti i pacchetti NuGet usati in un progetto.</span><span class="sxs-lookup"><span data-stu-id="ced26-109">You use a similar same workflow for virtually every NuGet package you use in a project.</span></span>

- [<span data-ttu-id="ced26-110">Installare i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ced26-110">Install pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="ced26-111">Creare un progetto</span><span class="sxs-lookup"><span data-stu-id="ced26-111">Create a project</span></span>](#create-a-project)
- [<span data-ttu-id="ced26-112">Aggiungere il pacchetto NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="ced26-112">Add the Newtonsoft.Json NuGet package</span></span>](#add-the-newtonsoftjson-nuget-package)
- [<span data-ttu-id="ced26-113">Usare l'API Newtonsoft.Json nell'app</span><span class="sxs-lookup"><span data-stu-id="ced26-113">Use the Newtonsoft.Json API in the app</span></span>](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> <span data-ttu-id="ced26-114">**Iniziare con nuget.org**: l'installazione di pacchetti da nuget.org è un flusso di lavoro comune che gli sviluppatori .NET usano per trovare componenti riutilizzabili nelle loro applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ced26-114">**Start with nuget.org**: Installing packages from nuget.org is a common workflow that .NET developers use to find components they can reuse in their own applications.</span></span> <span data-ttu-id="ced26-115">È sempre possibile eseguire una ricerca direttamente su nuget.org o trovare e installare pacchetti all'interno di Visual Studio, come illustrato in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="ced26-115">You can always search nuget.org directly or find and install packages within Visual Studio as shown in this topic.</span></span>

## <a name="install-pre-requisites"></a><span data-ttu-id="ced26-116">Installare i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ced26-116">Install pre-requisites</span></span>

<span data-ttu-id="ced26-117">Questa esercitazione richiede Visual Studio 2015 Update 3 con Strumenti per app di Windows universale o Visual Studio 2017 con il carico di lavoro Sviluppo di app per la piattaforma UWP (Universal Windows Platform).</span><span class="sxs-lookup"><span data-stu-id="ced26-117">This tutorial requires Visual Studio 2015 Update 3 with Tools for Universal Windows Apps, or Visual Studio 2017 with the Universal Windows Platform development workload.</span></span> <span data-ttu-id="ced26-118">Se Visual Studio è già installato, è possibile eseguire nuovamente il programma di installazione per aggiungere gli strumenti per la piattaforma UWP.</span><span class="sxs-lookup"><span data-stu-id="ced26-118">If you already have Visual Studio installed, you can run the installer again to add the UWP tools.</span></span>

<span data-ttu-id="ced26-119">È possibile installare l'edizione Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/) o usare le edizioni Professional o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="ced26-119">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span> 

## <a name="create-a-project"></a><span data-ttu-id="ced26-120">Creare un progetto</span><span class="sxs-lookup"><span data-stu-id="ced26-120">Create a project</span></span>

<span data-ttu-id="ced26-121">Per installare un pacchetto NuGet, è necessario un progetto basato su .NET in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ced26-121">To install a NuGet package, you need some kind of .NET-based project in Visual Studio.</span></span> <span data-ttu-id="ced26-122">Per questa procedura dettagliata è possibile usare una semplice app di Windows Presentation Foundation (WPF) o di Windows universale (UWP):</span><span class="sxs-lookup"><span data-stu-id="ced26-122">For this walkthrough, you can use use a simple Windows Presentation Foundation (WPF) or Universal Windows (UWP) app:</span></span>

- <span data-ttu-id="ced26-123">Per WPF (Windows 7+), scegliere **File > Nuovo > Progetto**, espandere **Visual C#**, selezionare **Desktop classico di Windows > App WPF (.NET Framework)** e scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="ced26-123">For WPF (Windows 7+), choose **File > New > Project**, expand **Visual C#**, select **Windows Classic Desktop > WPF App (.NET Framework)**, and select **OK**.</span></span>
- <span data-ttu-id="ced26-124">Per UWP (Windows 10), usare invece **Universale di Windows > App vuota (Windows universale)**.</span><span class="sxs-lookup"><span data-stu-id="ced26-124">For UWP (Windows 10), use the **Windows Universal > Blank App (Universal Windows)** instead.</span></span> <span data-ttu-id="ced26-125">Accettare i valori predefiniti per Versione di destinazione e Versione minima quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="ced26-125">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="ced26-126">Aggiungere il pacchetto NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="ced26-126">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="ced26-127">In Esplora soluzioni fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ced26-127">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Comando Gestisci pacchetti NuGet per i riferimenti del progetto](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="ced26-129">Scegliere "nuget.org" come **Origine pacchetto**, selezionare la scheda **Sfoglia**, cercare **Newtonsoft.Json**, selezionare il pacchetto nell'elenco e fare clic su **Installa**:</span><span class="sxs-lookup"><span data-stu-id="ced26-129">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Individuazione del pacchetto Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="ced26-131">Se viene richiesto di selezionare un formato di gestione del pacchetto, scegliere tra PackageReference (scelta consigliata) e `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="ced26-131">If prompted to select a package management format, choose between PackageReference (recommended) and `packages.config`:</span></span>

    ![Selezione di un formato di riferimento del pacchetto](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="ced26-133">Se viene richiesto di rivedere le modifiche, selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="ced26-133">If prompted to review changes, select **OK**.</span></span>

1. <span data-ttu-id="ced26-134">Fare clic con il pulsante destro del mouse sulla soluzione in Esplora soluzioni e selezionare **Compila soluzione**.</span><span class="sxs-lookup"><span data-stu-id="ced26-134">Right-click the solution in Solution Explorer and select **Build Solution**.</span></span> <span data-ttu-id="ced26-135">Ciò consente di ripristinare i pacchetti NuGet elencati in **Riferimenti**.</span><span class="sxs-lookup"><span data-stu-id="ced26-135">This restores any NuGet packages listed under **References**.</span></span> <span data-ttu-id="ced26-136">Per maggiori dettagli, vedere [Ripristino di pacchetti](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="ced26-136">For more details, see [Package Restore](../consume-packages/package-restore.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="ced26-137">Usare l'API Newtonsoft.Json nell'app</span><span class="sxs-lookup"><span data-stu-id="ced26-137">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="ced26-138">Con il pacchetto Newtonsoft.Json nel progetto, è possibile chiamare il relativo metodo `JsonConvert.SerializeObject` per convertire un oggetto in una stringa leggibile.</span><span class="sxs-lookup"><span data-stu-id="ced26-138">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="ced26-139">Aprire `MainWindow.xaml` (WPF) o `MainPage.xaml` (UWP) e sostituire l'elemento `Grid` esistente con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="ced26-139">Open `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="ced26-140">Espandere il nodo `MainWindow.xaml` (WPF) o `MainPage.xaml` (UWP) in Esplora soluzioni, aprire il file `.cs` e inserire il codice seguente all'interno della classe `MainWindow` o `MainPage`, dopo il costruttore:</span><span class="sxs-lookup"><span data-stu-id="ced26-140">Expand the `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) node in Solution Explorer, open the `.cs` file, and insert the following code inside the `MainWindow` or `MainPage` class, after the constructor:</span></span>

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

1. <span data-ttu-id="ced26-141">Anche se il pacchetto Newtonsoft.Json è stato aggiunto al progetto, vengono visualizzate sottolineature a zigzag rosse sotto `JsonConvert` perché è richiesta un'istruzione `using`.</span><span class="sxs-lookup"><span data-stu-id="ced26-141">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement.</span></span> <span data-ttu-id="ced26-142">Passare il mouse sulla sottolineatura di `JsonConvert`: verrà visualizzato un indicatore Lampadina con l'opzione **Mostra possibili correzioni**:</span><span class="sxs-lookup"><span data-stu-id="ced26-142">Hover over the underlined `JsonConvert` and you'll see the Lightbulb and the option to **Show potential fixes**:</span></span>

    ![Indicatore Lampadina con il comando Mostra possibili correzioni](media/QS_Use-04-ShowPotentialFixes.png)


1. <span data-ttu-id="ced26-144">Fare clic su **Mostra possibili correzioni** (o sull'indicatore Lampadina) e selezionare la prima correzione suggerita, `using Newtonsoft.Json;`.</span><span class="sxs-lookup"><span data-stu-id="ced26-144">Click on **Show potential fixes** (or the Lightbulb) and select the first suggested fix, `using Newtonsoft.Json;`.</span></span> <span data-ttu-id="ced26-145">La riga necessaria verrà aggiunta all'inizio del file.</span><span class="sxs-lookup"><span data-stu-id="ced26-145">This adds the necessary line to the top of the file.</span></span>

    ![Indicatore Lampadina con l'opzione per l'aggiunta di un'istruzione Using](media/QS_Use-05-AddUsing.png)

1. <span data-ttu-id="ced26-147">Compilare ed eseguire l'app premendo F5 o selezionando **Debug > Avvia debug** (in questa immagine è illustrato UWP, per WPF la schermata è simile):</span><span class="sxs-lookup"><span data-stu-id="ced26-147">Build and run the app by pressing F5 or selecting **Debug > Start Debugging** (UWP shown here; WPF is similar):</span></span>

    ![Output iniziale dell'app UWP](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="ced26-149">Selezionare il pulsante per visualizzare il contenuto del controllo TextBlock sostituito con testo JSON:</span><span class="sxs-lookup"><span data-stu-id="ced26-149">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Output dell'app UWP dopo la selezione del pulsante](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a><span data-ttu-id="ced26-151">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="ced26-151">Related topics</span></span>

- [<span data-ttu-id="ced26-152">Panoramica e flusso di lavoro dell'utilizzo di pacchetti</span><span class="sxs-lookup"><span data-stu-id="ced26-152">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="ced26-153">Ricerca e scelta di pacchetti</span><span class="sxs-lookup"><span data-stu-id="ced26-153">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="ced26-154">Configurazione del comportamento di NuGet</span><span class="sxs-lookup"><span data-stu-id="ced26-154">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
