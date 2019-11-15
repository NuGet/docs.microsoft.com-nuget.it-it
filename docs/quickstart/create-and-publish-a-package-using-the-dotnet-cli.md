---
title: Creare e pubblicare un pacchetto NuGet con l'interfaccia della riga di comando di dotnet
description: Esercitazione sulla creazione e pubblicazione di un pacchetto NuGet tramite l'interfaccia della riga di comando di .NET Core, ovvero dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 8727f67608593e6ae8b96daa81b7423782dfc219
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096936"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="20667-103">Guida introduttiva: Creare e pubblicare un pacchetto (interfaccia della riga di comando dotnet)</span><span class="sxs-lookup"><span data-stu-id="20667-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="20667-104">La creazione di un pacchetto NuGet da una libreria di classi .NET e la pubblicazione in nuget.org tramite l'interfaccia della riga di comando di `dotnet` sono un processo semplice.</span><span class="sxs-lookup"><span data-stu-id="20667-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20667-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="20667-105">Prerequisites</span></span>

1. <span data-ttu-id="20667-106">Installare [.NET Core SDK](https://www.microsoft.com/net/download/), che include l'interfaccia della riga di comando di `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="20667-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="20667-107">A partire da Visual Studio 2017, l'interfaccia della riga di comando di dotnet viene installata automaticamente con qualsiasi carico di lavoro .NET Core correlato.</span><span class="sxs-lookup"><span data-stu-id="20667-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="20667-108">[Registrarsi per ottenere un account gratuito in nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) se non è già disponibile.</span><span class="sxs-lookup"><span data-stu-id="20667-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="20667-109">Quando si crea un nuovo account, viene inviato un messaggio di posta elettronica di conferma.</span><span class="sxs-lookup"><span data-stu-id="20667-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="20667-110">È necessario confermare l'account prima di poter caricare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="20667-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="20667-111">Creare un progetto di libreria di classi</span><span class="sxs-lookup"><span data-stu-id="20667-111">Create a class library project</span></span>

<span data-ttu-id="20667-112">È possibile usare un progetto libreria di classi .NET esistente per il codice che si vuole includere in un pacchetto oppure creare un progetto semplice come segue:</span><span class="sxs-lookup"><span data-stu-id="20667-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="20667-113">Creare una cartella denominata `AppLogger`.</span><span class="sxs-lookup"><span data-stu-id="20667-113">Create a folder called `AppLogger`.</span></span>

1. <span data-ttu-id="20667-114">Aprire un prompt dei comandi e passare alla cartella `AppLogger`.</span><span class="sxs-lookup"><span data-stu-id="20667-114">Open a command prompt and switch to the `AppLogger` folder.</span></span>

1. <span data-ttu-id="20667-115">Digitare `dotnet new classlib`, che usa il nome della cartella corrente per il progetto.</span><span class="sxs-lookup"><span data-stu-id="20667-115">Type `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

   <span data-ttu-id="20667-116">Verrà creato il nuovo progetto.</span><span class="sxs-lookup"><span data-stu-id="20667-116">This creates the new project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="20667-117">Aggiungere i metadati del pacchetto al file di progetto</span><span class="sxs-lookup"><span data-stu-id="20667-117">Add package metadata to the project file</span></span>

<span data-ttu-id="20667-118">Per ogni pacchetto NuGet è necessario un manifesto che descrive i contenuti e le dipendenze del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="20667-118">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="20667-119">In un pacchetto finale, il manifesto è un file `.nuspec` generato dalle proprietà dei metadati NuGet incluse nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="20667-119">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="20667-120">Aprire il file di progetto (`.csproj`) e aggiungere le seguenti proprietà minime all'interno del tag `<PropertyGroup>` esistente, modificando i valori nel modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="20667-120">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="20667-121">Assegnare al pacchetto un identificatore univoco in nuget.org o per l'host in uso.</span><span class="sxs-lookup"><span data-stu-id="20667-121">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="20667-122">Per questa procedura dettagliata, si consiglia di includere "Sample" o "Test" nel nome, perché il passaggio di pubblicazione descritto più avanti rende il pacchetto visibile pubblicamente (nonostante sia improbabile che chiunque lo usi effettivamente).</span><span class="sxs-lookup"><span data-stu-id="20667-122">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="20667-123">Aggiungere eventuali proprietà facoltative descritte in [Proprietà dei metadati di NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="20667-123">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="20667-124">Per i pacchetti compilati per uso pubblico, prestare particolare attenzione alla proprietà **PackageTags**, perché questi tag consentono ad altri utenti di trovare il pacchetto e di comprenderne le funzioni.</span><span class="sxs-lookup"><span data-stu-id="20667-124">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="20667-125">Eseguire il comando pack</span><span class="sxs-lookup"><span data-stu-id="20667-125">Run the pack command</span></span>

<span data-ttu-id="20667-126">Per compilare un pacchetto NuGet (un file `.nupkg`) dal progetto, eseguire il comando `dotnet pack`, che consente anche di compilare automaticamente il progetto:</span><span class="sxs-lookup"><span data-stu-id="20667-126">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="20667-127">L'output mostra il percorso del file `.nupkg`:</span><span class="sxs-lookup"><span data-stu-id="20667-127">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="20667-128">Generare automaticamente il pacchetto in fase di compilazione</span><span class="sxs-lookup"><span data-stu-id="20667-128">Automatically generate package on build</span></span>

<span data-ttu-id="20667-129">Per eseguire automaticamente `dotnet pack` quando si esegue `dotnet build`, aggiungere la riga seguente al file di progetto all'interno di `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="20667-129">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="20667-130">Pubblicare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="20667-130">Publish the package</span></span>

<span data-ttu-id="20667-131">Dopo aver creato un file `.nupkg`, pubblicarlo in nuget.org usando il comando `dotnet nuget push` insieme a una chiave API acquisita da nuget.org.</span><span class="sxs-lookup"><span data-stu-id="20667-131">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="20667-132">Acquisire la chiave API</span><span class="sxs-lookup"><span data-stu-id="20667-132">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="20667-133">Pubblicare con dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="20667-133">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="20667-134">Errori di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="20667-134">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="20667-135">Gestire il pacchetto pubblicato</span><span class="sxs-lookup"><span data-stu-id="20667-135">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a><span data-ttu-id="20667-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="20667-136">Next steps</span></span>

<span data-ttu-id="20667-137">È stato creato il primo pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="20667-137">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="20667-138">Creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="20667-138">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)

<span data-ttu-id="20667-139">Per esplorare in modo più approfondito ciò che NuGet può offrire, selezionare i collegamenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="20667-139">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="20667-140">Pubblicare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="20667-140">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="20667-141">Pacchetti in versione non definitiva</span><span class="sxs-lookup"><span data-stu-id="20667-141">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="20667-142">Supportare più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="20667-142">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="20667-143">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="20667-143">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="20667-144">Creazione di pacchetti localizzati</span><span class="sxs-lookup"><span data-stu-id="20667-144">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="20667-145">Creazione di pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="20667-145">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="20667-146">Firma dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="20667-146">Signing packages</span></span>](../create-packages/Sign-a-package.md)
