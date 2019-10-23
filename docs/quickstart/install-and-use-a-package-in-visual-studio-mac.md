---
title: Installare e usare un pacchetto NuGet in Visual Studio per Mac
description: Esercitazione dettagliata sul processo di installazione e uso di un pacchetto NuGet in un progetto Visual Studio per Mac.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/03/2019
ms.locfileid: "70238477"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a><span data-ttu-id="6e844-103">Avvio rapido: Installare e usare un pacchetto in Visual Studio per Mac</span><span class="sxs-lookup"><span data-stu-id="6e844-103">Quickstart: Install and use a package in Visual Studio for Mac</span></span>

<span data-ttu-id="6e844-104">I pacchetti NuGet contengono codice riutilizzabile che altri sviluppatori rendono disponibile per l'uso nei progetti.</span><span class="sxs-lookup"><span data-stu-id="6e844-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="6e844-105">Vedere [Che cos'è NuGet?](../What-is-NuGet.md) per le informazioni di base.</span><span class="sxs-lookup"><span data-stu-id="6e844-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="6e844-106">I pacchetti vengono installati in un progetto Visual Studio per Mac usando Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="6e844-106">Packages are installed into a Visual Studio for Mac project using the NuGet Package Manager.</span></span> <span data-ttu-id="6e844-107">Questo articolo illustra il processo con il popolare pacchetto [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) e un progetto console .NET Core.</span><span class="sxs-lookup"><span data-stu-id="6e844-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a .NET Core console project.</span></span> <span data-ttu-id="6e844-108">Lo stesso processo si applica a qualsiasi altro progetto Novell o .NET Core.</span><span class="sxs-lookup"><span data-stu-id="6e844-108">The same process applies to any other Xamarin or .NET Core project.</span></span>

<span data-ttu-id="6e844-109">Al termine dell'installazione, fare riferimento al pacchetto nel codice con `using <namespace>`, dove \<spazio dei nomi\> è specifico per il pacchetto in uso.</span><span class="sxs-lookup"><span data-stu-id="6e844-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="6e844-110">Dopo avere creato il riferimento, è possibile chiamare il pacchetto tramite la relativa API.</span><span class="sxs-lookup"><span data-stu-id="6e844-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="6e844-111">**Iniziare con nuget.org**: le ricerche in *nuget.org* sono il modo in cui gli sviluppatori di .NET individuano in genere componenti che possono riutilizzare nelle loro applicazioni.</span><span class="sxs-lookup"><span data-stu-id="6e844-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="6e844-112">È possibile eseguire una ricerca direttamente in *nuget.org* o trovare e installare pacchetti all'interno di Visual Studio, come illustrato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="6e844-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="6e844-113">Per informazioni generali, vedere [Trovare e valutare i pacchetti NuGet](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="6e844-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e844-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6e844-114">Prerequisites</span></span>

- <span data-ttu-id="6e844-115">Visual Studio 2019 per Mac.</span><span class="sxs-lookup"><span data-stu-id="6e844-115">Visual Studio 2019 for Mac.</span></span>

<span data-ttu-id="6e844-116">È possibile installare l'edizione 2019 Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/) o usare le edizioni Professional o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="6e844-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="6e844-117">Se si usa Visual Studio in Windows, vedere [installare e usare un pacchetto in Visual Studio (solo Windows)](install-and-use-a-package-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="6e844-117">If you're using Visual Studio on Windows, see [Install and use a package in Visual Studio (Windows Only)](install-and-use-a-package-in-visual-studio.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="6e844-118">Creare un progetto</span><span class="sxs-lookup"><span data-stu-id="6e844-118">Create a project</span></span>

<span data-ttu-id="6e844-119">I pacchetti NuGet possono essere installati in qualsiasi progetto .NET, a condizione che il pacchetto supporti lo stesso framework di destinazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="6e844-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="6e844-120">Per questa procedura dettagliata, usare una semplice app console .NET Core.</span><span class="sxs-lookup"><span data-stu-id="6e844-120">For this walkthrough, use a simple .NET Core Console app.</span></span> <span data-ttu-id="6e844-121">Creare un progetto in Visual Studio per Mac usando **File > nuova soluzione...** , selezionare il modello **applicazione console di > .NET Core > app** .</span><span class="sxs-lookup"><span data-stu-id="6e844-121">Create a project in Visual Studio for Mac using **File > New Solution...**, select the **.NET Core > App > Console Application** template.</span></span> <span data-ttu-id="6e844-122">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="6e844-122">Click **Next**.</span></span> <span data-ttu-id="6e844-123">Quando richiesto, accettare i valori predefiniti per **Framework di destinazione** .</span><span class="sxs-lookup"><span data-stu-id="6e844-123">Accept the default values for **Target Framework** when prompted.</span></span>

<span data-ttu-id="6e844-124">Visual Studio crea il progetto, che viene aperto in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="6e844-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="6e844-125">Aggiungere il pacchetto NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="6e844-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="6e844-126">Per installare il pacchetto, usare Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="6e844-126">To install the package, you use the NuGet Package Manager.</span></span> <span data-ttu-id="6e844-127">Quando si installa un pacchetto, NuGet registra la dipendenza nel file di progetto o in un `packages.config` file (a seconda del formato del progetto).</span><span class="sxs-lookup"><span data-stu-id="6e844-127">When you install a package, NuGet records the dependency in  either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="6e844-128">Per altre informazioni, vedere [Flusso di lavoro dell'utilizzo di pacchetti](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="6e844-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="6e844-129">Gestione pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="6e844-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="6e844-130">In Esplora soluzioni fare clic con il pulsante destro del mouse su **dipendenze** e scegliere **Aggiungi pacchetti...** .</span><span class="sxs-lookup"><span data-stu-id="6e844-130">In Solution Explorer, right-click **Dependencies** and choose **Add Packages...**.</span></span>

    ![Comando Gestisci pacchetti NuGet per i riferimenti del progetto](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. <span data-ttu-id="6e844-132">Scegliere "nuget.org" come **origine del pacchetto** nell'angolo superiore sinistro della finestra di dialogo e cercare **Newtonsoft. JSON**, selezionare il pacchetto nell'elenco e selezionare **Aggiungi pacchetti...** :</span><span class="sxs-lookup"><span data-stu-id="6e844-132">Choose "nuget.org" as the **Package source** in the top left corner of the dialog, and search for **Newtonsoft.Json**, select that package in the list, and select **Add Packages...**:</span></span>

    ![Individuazione del pacchetto Newtonsoft.Json](media/QS_Use_Mac-03-NewtonsoftJson.png)

    <span data-ttu-id="6e844-134">Per ulteriori informazioni su Gestione pacchetti NuGet, vedere [Install and Manage Packages using Visual Studio per Mac](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="6e844-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="6e844-135">Usare l'API Newtonsoft.Json nell'app</span><span class="sxs-lookup"><span data-stu-id="6e844-135">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="6e844-136">Con il pacchetto Newtonsoft.Json nel progetto, è possibile chiamare il relativo metodo `JsonConvert.SerializeObject` per convertire un oggetto in una stringa leggibile.</span><span class="sxs-lookup"><span data-stu-id="6e844-136">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="6e844-137">Aprire il `Program.cs` file (situato nella riquadro della soluzione) e sostituire il contenuto del file con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="6e844-137">Open the `Program.cs` file (located in the Solution Pad) and replace the file contents with the following code:</span></span>

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. <span data-ttu-id="6e844-138">Compilare ed eseguire l'app selezionando **esegui > avviare il debug**:</span><span class="sxs-lookup"><span data-stu-id="6e844-138">Build and run the app by selecting **Run > Start Debugging**:</span></span>

1. <span data-ttu-id="6e844-139">Una volta eseguita l'app, verrà visualizzato l'output JSON serializzato nella console:</span><span class="sxs-lookup"><span data-stu-id="6e844-139">Once the app runs, you'll see the serialized JSON output appear in the console:</span></span>

  ![Output dell'app console](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a><span data-ttu-id="6e844-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6e844-141">Next steps</span></span>
<span data-ttu-id="6e844-142">È stato installato e usato il primo pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="6e844-142">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6e844-143">Installare e gestire i pacchetti tramite Visual Studio per Mac</span><span class="sxs-lookup"><span data-stu-id="6e844-143">Install and manage packages using Visual Studio for Mac</span></span>](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

<span data-ttu-id="6e844-144">Per esplorare in modo più approfondito ciò che NuGet può offrire, selezionare i collegamenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="6e844-144">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="6e844-145">Panoramica e flusso di lavoro dell'utilizzo di pacchetti</span><span class="sxs-lookup"><span data-stu-id="6e844-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="6e844-146">Riferimenti ai pacchetti nei file di progetto</span><span class="sxs-lookup"><span data-stu-id="6e844-146">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)