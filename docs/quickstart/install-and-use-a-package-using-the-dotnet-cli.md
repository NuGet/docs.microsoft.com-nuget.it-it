---
title: Installare e usare un pacchetto NuGet con l'interfaccia della riga di comando di dotnet
description: Esercitazione dettagliata sul processo di installazione e uso di un pacchetto NuGet in un progetto .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: ee456fd49675db37fee78dc14502a897d84a2b99
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342465"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="95501-103">Guida introduttiva: Installare e usare un pacchetto con l'interfaccia della riga di comando di dotnet</span><span class="sxs-lookup"><span data-stu-id="95501-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="95501-104">I pacchetti NuGet contengono codice riutilizzabile che altri sviluppatori rendono disponibile per l'uso nei progetti.</span><span class="sxs-lookup"><span data-stu-id="95501-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="95501-105">Vedere [Che cos'è NuGet?](../What-is-NuGet.md) per le informazioni di base.</span><span class="sxs-lookup"><span data-stu-id="95501-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="95501-106">I pacchetti vengono installati in un progetto .NET Core usando il comando `dotnet add package`, come descritto in questo articolo per il famoso pacchetto [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).</span><span class="sxs-lookup"><span data-stu-id="95501-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="95501-107">Al termine dell'installazione, fare riferimento al pacchetto nel codice con `using <namespace>`, dove \<spazio dei nomi\> è specifico per il pacchetto in uso.</span><span class="sxs-lookup"><span data-stu-id="95501-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="95501-108">È quindi possibile usare l'API del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="95501-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="95501-109">**Iniziare con nuget.org**: le ricerche in nuget.org sono il modo in cui gli sviluppatori di .NET individuano in genere componenti che possono riutilizzare nelle loro applicazioni.</span><span class="sxs-lookup"><span data-stu-id="95501-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="95501-110">È possibile eseguire una ricerca direttamente in nuget.org o trovare e installare pacchetti all'interno di Visual Studio, come illustrato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="95501-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95501-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="95501-111">Prerequisites</span></span>

- <span data-ttu-id="95501-112">[.NET Core SDK](https://www.microsoft.com/net/download/), che fornisce lo strumento da riga di comando `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="95501-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="95501-113">A partire da Visual Studio 2017, l'interfaccia della riga di comando di dotnet viene installata automaticamente con qualsiasi carico di lavoro .NET Core correlato.</span><span class="sxs-lookup"><span data-stu-id="95501-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="95501-114">Creare un progetto</span><span class="sxs-lookup"><span data-stu-id="95501-114">Create a project</span></span>

<span data-ttu-id="95501-115">I pacchetti NuGet possono essere installati in un progetto .NET di qualche tipo.</span><span class="sxs-lookup"><span data-stu-id="95501-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="95501-116">Per questa procedura dettagliata creare un progetto console .NET Core semplice come segue:</span><span class="sxs-lookup"><span data-stu-id="95501-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="95501-117">Creare una cartella per il progetto.</span><span class="sxs-lookup"><span data-stu-id="95501-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="95501-118">Creare il progetto usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="95501-118">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="95501-119">Usare `dotnet run` per verificare che l'app sia stata creata correttamente.</span><span class="sxs-lookup"><span data-stu-id="95501-119">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="95501-120">Aggiungere il pacchetto NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="95501-120">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="95501-121">Usare il comando seguente per installare il pacchetto `Newtonsoft.json`.</span><span class="sxs-lookup"><span data-stu-id="95501-121">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="95501-122">Al termine dell'esecuzione del comando, aprire il file `.csproj` per vedere il riferimento aggiunto:</span><span class="sxs-lookup"><span data-stu-id="95501-122">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="95501-123">Usare l'API Newtonsoft.Json nell'app</span><span class="sxs-lookup"><span data-stu-id="95501-123">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="95501-124">Aprire il file `Program.cs` e aggiungere la riga seguente all'inizio del file:</span><span class="sxs-lookup"><span data-stu-id="95501-124">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="95501-125">Aggiungere il codice seguente prima della riga `class Program`:</span><span class="sxs-lookup"><span data-stu-id="95501-125">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="95501-126">Sostituire la funzione `Main` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="95501-126">Replace the `Main` function with the following:</span></span>

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. <span data-ttu-id="95501-127">Compilare ed eseguire l'app usando il comando `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="95501-127">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="95501-128">L'output deve essere la rappresentazione JSON dell'oggetto `Account` nel codice:</span><span class="sxs-lookup"><span data-stu-id="95501-128">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="95501-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="95501-129">Next steps</span></span>

<span data-ttu-id="95501-130">È stato installato e usato il primo pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="95501-130">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="95501-131">Installare e usare pacchetti tramite l'interfaccia della riga di comando di dotnet</span><span class="sxs-lookup"><span data-stu-id="95501-131">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)

<span data-ttu-id="95501-132">Per esplorare in modo più approfondito ciò che NuGet può offrire, selezionare i collegamenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="95501-132">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="95501-133">Panoramica e flusso di lavoro dell'utilizzo di pacchetti</span><span class="sxs-lookup"><span data-stu-id="95501-133">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="95501-134">Ricerca e scelta di pacchetti</span><span class="sxs-lookup"><span data-stu-id="95501-134">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="95501-135">Riferimenti ai pacchetti nei file di progetto</span><span class="sxs-lookup"><span data-stu-id="95501-135">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
