---
title: Guida introduttiva all'uso di pacchetti NuGet tramite l'interfaccia della riga di comando di dotnet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: Esercitazione dettagliata sul processo di installazione e uso di un pacchetto NuGet in un progetto .NET Core.
keywords: installare NuGet, utilizzo di un pacchetto NuGet, installazione di pacchetti NuGet, riferimenti ai pacchetti NuGet, uso di pacchetti NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: accc6d7bb5abff43ffaa083fa55c13cd5b10ce10
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/08/2018
---
# <a name="install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="ac351-104">Installare e usare un pacchetto con l'interfaccia della riga di comando di dotnet</span><span class="sxs-lookup"><span data-stu-id="ac351-104">Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="ac351-105">I pacchetti NuGet contengono codice riutilizzabile che altri sviluppatori rendono disponibile per l'uso nei progetti.</span><span class="sxs-lookup"><span data-stu-id="ac351-105">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="ac351-106">Vedere [Che cos'è NuGet?](../What-is-NuGet.md) per le informazioni di base.</span><span class="sxs-lookup"><span data-stu-id="ac351-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="ac351-107">I pacchetti vengono installati in un progetto .NET Core usando il comando `dotnet add package`, come descritto in questo articolo per il famoso pacchetto [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).</span><span class="sxs-lookup"><span data-stu-id="ac351-107">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="ac351-108">Al termine dell'installazione, fare riferimento al pacchetto nel codice con `using <namespace>`, dove \<spazio dei nomi\> è specifico per il pacchetto in uso.</span><span class="sxs-lookup"><span data-stu-id="ac351-108">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="ac351-109">Dopo avere creato il riferimento, è possibile chiamare il pacchetto tramite la relativa API.</span><span class="sxs-lookup"><span data-stu-id="ac351-109">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="ac351-110">**Iniziare con nuget.org**: le ricerche in nuget.org sono il modo in cui gli sviluppatori di .NET individuano in genere componenti che possono riutilizzare nelle loro applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ac351-110">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="ac351-111">È possibile eseguire una ricerca direttamente in nuget.org o trovare e installare pacchetti all'interno di Visual Studio, come illustrato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="ac351-111">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac351-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ac351-112">Prerequisites</span></span>

- <span data-ttu-id="ac351-113">[.NET Core SDK](https://www.microsoft.com/net/download/), che fornisce lo strumento da riga di comando `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="ac351-113">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="ac351-114">Creare un progetto</span><span class="sxs-lookup"><span data-stu-id="ac351-114">Create a project</span></span>

<span data-ttu-id="ac351-115">I pacchetti NuGet possono essere installati in un progetto .NET di qualche tipo.</span><span class="sxs-lookup"><span data-stu-id="ac351-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="ac351-116">Per questa procedura dettagliata creare un progetto console .NET Core semplice come segue:</span><span class="sxs-lookup"><span data-stu-id="ac351-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="ac351-117">Creare una cartella per il progetto.</span><span class="sxs-lookup"><span data-stu-id="ac351-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="ac351-118">Creare il progetto usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ac351-118">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="ac351-119">Usare `dotnet run` per verificare che l'app sia stata creata correttamente.</span><span class="sxs-lookup"><span data-stu-id="ac351-119">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="ac351-120">Aggiungere il pacchetto NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="ac351-120">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="ac351-121">Usare il comando seguente per installare il pacchetto `Newtonsoft.json`.</span><span class="sxs-lookup"><span data-stu-id="ac351-121">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

1. <span data-ttu-id="ac351-122">Al termine dell'esecuzione del comando, aprire il file `.csproj` per vedere il riferimento aggiunto:</span><span class="sxs-lookup"><span data-stu-id="ac351-122">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
  </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="ac351-123">Usare l'API Newtonsoft.Json nell'app</span><span class="sxs-lookup"><span data-stu-id="ac351-123">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="ac351-124">Aprire il file `Program.cs` e aggiungere la riga seguente all'inizio del file:</span><span class="sxs-lookup"><span data-stu-id="ac351-124">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="ac351-125">Aggiungere il codice seguente prima della riga `class Program`:</span><span class="sxs-lookup"><span data-stu-id="ac351-125">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="ac351-126">Sostituire la funzione `Main` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="ac351-126">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="ac351-127">Compilare ed eseguire l'app usando il comando `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="ac351-127">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="ac351-128">L'output deve essere la rappresentazione JSON dell'oggetto `Account` nel codice:</span><span class="sxs-lookup"><span data-stu-id="ac351-128">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="ac351-129">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="ac351-129">Related articles</span></span>

- [<span data-ttu-id="ac351-130">Panoramica e flusso di lavoro dell'utilizzo di pacchetti</span><span class="sxs-lookup"><span data-stu-id="ac351-130">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="ac351-131">Ricerca e scelta di pacchetti</span><span class="sxs-lookup"><span data-stu-id="ac351-131">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="ac351-132">Modi per installare pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="ac351-132">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="ac351-133">Configurazione del comportamento di NuGet</span><span class="sxs-lookup"><span data-stu-id="ac351-133">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
