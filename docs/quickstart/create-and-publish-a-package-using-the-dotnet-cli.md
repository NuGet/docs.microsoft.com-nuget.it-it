---
title: Creazione e pubblicazione di un pacchetto NuGet con l'interfaccia della riga di comando di dotnet
description: Esercitazione sulla creazione e pubblicazione di un pacchetto NuGet tramite l'interfaccia della riga di comando di .NET Core, ovvero dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 051fcc355fb78c0ab208125c2295b6316236fd46
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426352"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="1bf15-103">Guida introduttiva: Creare e pubblicare un pacchetto (interfaccia della riga di comando dotnet)</span><span class="sxs-lookup"><span data-stu-id="1bf15-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="1bf15-104">La creazione di un pacchetto NuGet da una libreria di classi .NET e la pubblicazione in nuget.org tramite l'interfaccia della riga di comando di `dotnet` sono un processo semplice.</span><span class="sxs-lookup"><span data-stu-id="1bf15-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bf15-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1bf15-105">Prerequisites</span></span>

1. <span data-ttu-id="1bf15-106">Installare [.NET Core SDK](https://www.microsoft.com/net/download/), che include l'interfaccia della riga di comando di `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="1bf15-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span>

1. <span data-ttu-id="1bf15-107">[Registrarsi per ottenere un account gratuito in nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) se non è già disponibile.</span><span class="sxs-lookup"><span data-stu-id="1bf15-107">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="1bf15-108">Quando si crea un nuovo account, viene inviato un messaggio di posta elettronica di conferma.</span><span class="sxs-lookup"><span data-stu-id="1bf15-108">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="1bf15-109">È necessario confermare l'account prima di poter caricare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1bf15-109">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="1bf15-110">Creare un progetto di libreria di classi</span><span class="sxs-lookup"><span data-stu-id="1bf15-110">Create a class library project</span></span>

<span data-ttu-id="1bf15-111">È possibile usare un progetto libreria di classi .NET esistente per il codice che si vuole includere in un pacchetto oppure creare un progetto semplice come segue:</span><span class="sxs-lookup"><span data-stu-id="1bf15-111">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="1bf15-112">Creare una cartella denominata `AppLogger` e passare a tale cartella.</span><span class="sxs-lookup"><span data-stu-id="1bf15-112">Create a folder called `AppLogger` and change into it.</span></span>

1. <span data-ttu-id="1bf15-113">Creare il progetto con `dotnet new classlib`, che usa il nome della cartella corrente per il progetto.</span><span class="sxs-lookup"><span data-stu-id="1bf15-113">Create the project using `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="1bf15-114">Aggiungere i metadati del pacchetto al file di progetto</span><span class="sxs-lookup"><span data-stu-id="1bf15-114">Add package metadata to the project file</span></span>

<span data-ttu-id="1bf15-115">Per ogni pacchetto NuGet è necessario un manifesto che descrive i contenuti e le dipendenze del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1bf15-115">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="1bf15-116">In un pacchetto finale, il manifesto è un file `.nuspec` generato dalle proprietà dei metadati NuGet incluse nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="1bf15-116">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="1bf15-117">Aprire il file di progetto (`.csproj`) e aggiungere le seguenti proprietà minime all'interno del tag `<PropertyGroup>` esistente, modificando i valori nel modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="1bf15-117">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="1bf15-118">Assegnare al pacchetto un identificatore univoco in nuget.org o per l'host in uso.</span><span class="sxs-lookup"><span data-stu-id="1bf15-118">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="1bf15-119">Per questa procedura dettagliata, si consiglia di includere "Sample" o "Test" nel nome, perché il passaggio di pubblicazione descritto più avanti rende il pacchetto visibile pubblicamente (nonostante sia improbabile che chiunque lo usi effettivamente).</span><span class="sxs-lookup"><span data-stu-id="1bf15-119">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="1bf15-120">Aggiungere eventuali proprietà facoltative descritte in [Proprietà dei metadati di NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="1bf15-120">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="1bf15-121">Per i pacchetti compilati per uso pubblico, prestare particolare attenzione alla proprietà **PackageTags**, perché questi tag consentono ad altri utenti di trovare il pacchetto e di comprenderne le funzioni.</span><span class="sxs-lookup"><span data-stu-id="1bf15-121">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="1bf15-122">Eseguire il comando pack</span><span class="sxs-lookup"><span data-stu-id="1bf15-122">Run the pack command</span></span>

<span data-ttu-id="1bf15-123">Per compilare un pacchetto NuGet (un file `.nupkg`) dal progetto, eseguire il comando `dotnet pack`, che consente anche di compilare automaticamente il progetto:</span><span class="sxs-lookup"><span data-stu-id="1bf15-123">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="1bf15-124">L'output mostra il percorso del file `.nupkg`:</span><span class="sxs-lookup"><span data-stu-id="1bf15-124">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="1bf15-125">Generare automaticamente il pacchetto in fase di compilazione</span><span class="sxs-lookup"><span data-stu-id="1bf15-125">Automatically generate package on build</span></span>

<span data-ttu-id="1bf15-126">Per eseguire automaticamente `dotnet pack` quando si esegue `dotnet build`, aggiungere la riga seguente al file di progetto all'interno di `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="1bf15-126">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="1bf15-127">Pubblicare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="1bf15-127">Publish the package</span></span>

<span data-ttu-id="1bf15-128">Dopo aver creato un file `.nupkg`, pubblicarlo in nuget.org usando il comando `dotnet nuget push` insieme a una chiave API acquisita da nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1bf15-128">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="1bf15-129">Acquisire la chiave API</span><span class="sxs-lookup"><span data-stu-id="1bf15-129">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="1bf15-130">Pubblicare con dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="1bf15-130">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="1bf15-131">Errori di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="1bf15-131">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="1bf15-132">Gestire il pacchetto pubblicato</span><span class="sxs-lookup"><span data-stu-id="1bf15-132">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="1bf15-133">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="1bf15-133">Related topics</span></span>

- [<span data-ttu-id="1bf15-134">Creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="1bf15-134">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="1bf15-135">Pubblicare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="1bf15-135">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="1bf15-136">Pacchetti in versione non definitiva</span><span class="sxs-lookup"><span data-stu-id="1bf15-136">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="1bf15-137">Supportare più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="1bf15-137">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="1bf15-138">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="1bf15-138">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="1bf15-139">Creazione di pacchetti localizzati</span><span class="sxs-lookup"><span data-stu-id="1bf15-139">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="1bf15-140">Creazione di pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="1bf15-140">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="1bf15-141">Firma dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="1bf15-141">Signing packages</span></span>](../create-packages/Sign-a-package.md)
