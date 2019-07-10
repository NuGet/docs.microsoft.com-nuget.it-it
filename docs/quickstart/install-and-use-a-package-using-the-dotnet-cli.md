---
title: Guida introduttiva all'uso di pacchetti NuGet tramite l'interfaccia della riga di comando di dotnet
description: Esercitazione dettagliata sul processo di installazione e uso di un pacchetto NuGet in un progetto .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 1060d98278fed89ac63ee17c1896ae8bdce72a9e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426160"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="17394-103">Guida introduttiva: Installare e usare un pacchetto con l'interfaccia della riga di comando di dotnet</span><span class="sxs-lookup"><span data-stu-id="17394-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="17394-104">I pacchetti NuGet contengono codice riutilizzabile che altri sviluppatori rendono disponibile per l'uso nei progetti.</span><span class="sxs-lookup"><span data-stu-id="17394-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="17394-105">Vedere [Che cos'è NuGet?](../What-is-NuGet.md) per le informazioni di base.</span><span class="sxs-lookup"><span data-stu-id="17394-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="17394-106">I pacchetti vengono installati in un progetto .NET Core usando il comando `dotnet add package`, come descritto in questo articolo per il famoso pacchetto [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).</span><span class="sxs-lookup"><span data-stu-id="17394-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="17394-107">Al termine dell'installazione, fare riferimento al pacchetto nel codice con `using <namespace>`, dove \<spazio dei nomi\> è specifico per il pacchetto in uso.</span><span class="sxs-lookup"><span data-stu-id="17394-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="17394-108">È quindi possibile usare l'API del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="17394-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="17394-109">**Iniziare con nuget.org**: le ricerche in nuget.org sono il modo in cui gli sviluppatori di .NET individuano in genere componenti che possono riutilizzare nelle loro applicazioni.</span><span class="sxs-lookup"><span data-stu-id="17394-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="17394-110">È possibile eseguire una ricerca direttamente in nuget.org o trovare e installare pacchetti all'interno di Visual Studio, come illustrato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="17394-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17394-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="17394-111">Prerequisites</span></span>

- <span data-ttu-id="17394-112">[.NET Core SDK](https://www.microsoft.com/net/download/), che fornisce lo strumento da riga di comando `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="17394-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="17394-113">Creare un progetto</span><span class="sxs-lookup"><span data-stu-id="17394-113">Create a project</span></span>

<span data-ttu-id="17394-114">I pacchetti NuGet possono essere installati in un progetto .NET di qualche tipo.</span><span class="sxs-lookup"><span data-stu-id="17394-114">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="17394-115">Per questa procedura dettagliata creare un progetto console .NET Core semplice come segue:</span><span class="sxs-lookup"><span data-stu-id="17394-115">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="17394-116">Creare una cartella per il progetto.</span><span class="sxs-lookup"><span data-stu-id="17394-116">Create a folder for the project.</span></span>

1. <span data-ttu-id="17394-117">Creare il progetto usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="17394-117">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="17394-118">Usare `dotnet run` per verificare che l'app sia stata creata correttamente.</span><span class="sxs-lookup"><span data-stu-id="17394-118">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="17394-119">Aggiungere il pacchetto NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="17394-119">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="17394-120">Usare il comando seguente per installare il pacchetto `Newtonsoft.json`.</span><span class="sxs-lookup"><span data-stu-id="17394-120">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="17394-121">Al termine dell'esecuzione del comando, aprire il file `.csproj` per vedere il riferimento aggiunto:</span><span class="sxs-lookup"><span data-stu-id="17394-121">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="17394-122">Usare l'API Newtonsoft.Json nell'app</span><span class="sxs-lookup"><span data-stu-id="17394-122">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="17394-123">Aprire il file `Program.cs` e aggiungere la riga seguente all'inizio del file:</span><span class="sxs-lookup"><span data-stu-id="17394-123">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="17394-124">Aggiungere il codice seguente prima della riga `class Program`:</span><span class="sxs-lookup"><span data-stu-id="17394-124">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="17394-125">Sostituire la funzione `Main` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="17394-125">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="17394-126">Compilare ed eseguire l'app usando il comando `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="17394-126">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="17394-127">L'output deve essere la rappresentazione JSON dell'oggetto `Account` nel codice:</span><span class="sxs-lookup"><span data-stu-id="17394-127">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="17394-128">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="17394-128">Related articles</span></span>

- [<span data-ttu-id="17394-129">Installare e usare pacchetti tramite l'interfaccia della riga di comando di dotnet</span><span class="sxs-lookup"><span data-stu-id="17394-129">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)
- [<span data-ttu-id="17394-130">Panoramica e flusso di lavoro dell'utilizzo di pacchetti</span><span class="sxs-lookup"><span data-stu-id="17394-130">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="17394-131">Ricerca e scelta di pacchetti</span><span class="sxs-lookup"><span data-stu-id="17394-131">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="17394-132">Configurazioni comuni di NuGet</span><span class="sxs-lookup"><span data-stu-id="17394-132">Common NuGet configurations</span></span>](../consume-packages/configuring-nuget-behavior.md)
