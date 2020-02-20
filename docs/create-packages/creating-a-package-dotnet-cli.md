---
title: Creare un pacchetto NuGet con l'interfaccia della riga di comando di dotnet
description: Guida dettagliata al processo di progettazione e creazione di un pacchetto NuGet, incluse le principali decisioni critiche, ad esempio quelle relative ai file e al controllo delle versioni.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: c198bb73f0e4f5a59826db905eaf4622fe8543bc
ms.sourcegitcommit: 1799d4ac23c8aacee7498fdc72c40dd1646d267b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77476256"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="f5338-103">Creare un pacchetto NuGet con l'interfaccia della riga di comando di dotnet</span><span class="sxs-lookup"><span data-stu-id="f5338-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="f5338-104">Indipendentemente dalle operazioni eseguite dal pacchetto o dal tipo di codice contenuto, è possibile usare uno degli strumenti dell'interfaccia della riga di comando, ovvero `nuget.exe` o `dotnet.exe`. per rendere disponibili tali funzionalità in un componente condivisibile e utilizzabile da altri sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="f5338-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="f5338-105">Questo articolo descrive come creare un pacchetto usando l'interfaccia della riga di comando di dotnet.</span><span class="sxs-lookup"><span data-stu-id="f5338-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="f5338-106">Per installare l' interfaccia della riga di comando di `dotnet`, vedere [Installare gli strumenti client di NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="f5338-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="f5338-107">A partire da Visual Studio 2017, l'interfaccia della riga di comando di dotnet è inclusa nei carichi di lavoro di .NET Core.</span><span class="sxs-lookup"><span data-stu-id="f5338-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="f5338-108">Per i progetti .NET Core e .NET Standard che usano il [formato di tipo SDK](../resources/check-project-format.md), e qualsiasi altro progetto di tipo SDK, NuGet usa le informazioni nel file di progetto direttamente per creare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f5338-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="f5338-109">Per esercitazioni dettagliate, vedere [Creare pacchetti .NET Standard con l'interfaccia della riga di comando di dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) o [Creare pacchetti .NET Standard con Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f5338-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) or [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="f5338-110">`msbuild -t:pack` dal punto di vista funzionale equivale a `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="f5338-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="f5338-111">Per eseguire la compilazione con MSBuild, vedere [Creare un pacchetto NuGet usando MSBuild](creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="f5338-111">To build with MSBuild, see [Create a NuGet package using MSBuild](creating-a-package-msbuild.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f5338-112">Questo argomento si applica ai progetti [di tipo SDK](../resources/check-project-format.md), in genere progetti .NET Core e .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="f5338-112">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="f5338-113">Impostare le proprietà</span><span class="sxs-lookup"><span data-stu-id="f5338-113">Set properties</span></span>

<span data-ttu-id="f5338-114">Per creare un pacchetto, sono necessarie le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="f5338-114">The following properties are required to create a package.</span></span>

- <span data-ttu-id="f5338-115">`PackageId`, ovvero l'identificatore del pacchetto, che deve essere univoco nella raccolta che ospita il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f5338-115">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="f5338-116">Se non è specificato, il valore predefinito è `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="f5338-116">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="f5338-117">`Version`, ovvero un numero di versione specifico nel formato *Principale.Secondaria.Patch[-Suffisso]* dove *-Suffisso* identifica le [versioni preliminari](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="f5338-117">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="f5338-118">Se non è specificato, il valore predefinito è 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="f5338-118">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="f5338-119">Titolo del pacchetto come deve essere visualizzato nell'host (ad esempio, nuget.org)</span><span class="sxs-lookup"><span data-stu-id="f5338-119">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="f5338-120">`Authors`, ovvero informazioni sull'autore e sul proprietario.</span><span class="sxs-lookup"><span data-stu-id="f5338-120">`Authors`, author and owner information.</span></span> <span data-ttu-id="f5338-121">Se non è specificato, il valore predefinito è `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="f5338-121">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="f5338-122">`Company`, ovvero il nome della società.</span><span class="sxs-lookup"><span data-stu-id="f5338-122">`Company`, your company name.</span></span> <span data-ttu-id="f5338-123">Se non è specificato, il valore predefinito è `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="f5338-123">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="f5338-124">In Visual Studio è possibile impostare questi valori nelle proprietà del progetto (fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni, scegliere **Proprietà** e selezionare la scheda **Pacchetto**).</span><span class="sxs-lookup"><span data-stu-id="f5338-124">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="f5338-125">È anche possibile impostare queste proprietà direttamente nei file di progetto (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="f5338-125">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="f5338-126">Assegnare al pacchetto un identificatore univoco in nuget.org o per l'origine di pacchetti in uso.</span><span class="sxs-lookup"><span data-stu-id="f5338-126">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="f5338-127">L'esempio seguente illustra un file di progetto semplice e completo con queste proprietà incluse.</span><span class="sxs-lookup"><span data-stu-id="f5338-127">The following example shows a simple, complete project file with these properties included.</span></span> <span data-ttu-id="f5338-128">È possibile creare un nuovo progetto predefinito usando il comando `dotnet new classlib`.</span><span class="sxs-lookup"><span data-stu-id="f5338-128">(You can create a new default project using the `dotnet new classlib` command.)</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="f5338-129">È anche possibile impostare le proprietà facoltative, ad esempio `Title`, `PackageDescription` e `PackageTags`, come descritto in [Destinazioni di pack per MSBuild](../reference/msbuild-targets.md#pack-target), [Controllo degli asset delle dipendenze](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) e [Proprietà dei metadati NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="f5338-129">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="f5338-130">Per i pacchetti compilati per uso pubblico, prestare particolare attenzione alla proprietà **PackageTags**, perché questi tag consentono ad altri utenti di trovare il pacchetto e di comprenderne le funzioni.</span><span class="sxs-lookup"><span data-stu-id="f5338-130">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="f5338-131">Per informazioni dettagliate sulla dichiarazione delle dipendenze e sulla specifica dei numeri di versione, vedere [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md) e [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="f5338-131">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="f5338-132">È anche possibile esporre gli asset dalle dipendenze direttamente nel pacchetto usando gli attributi `<IncludeAssets>` e `<ExcludeAssets>`.</span><span class="sxs-lookup"><span data-stu-id="f5338-132">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="f5338-133">Per altre informazioni, vedere [Controllo degli asset delle dipendenze](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="f5338-133">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="f5338-134">Scegliere un identificatore univoco del pacchetto e impostare il numero di versione</span><span class="sxs-lookup"><span data-stu-id="f5338-134">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a><span data-ttu-id="f5338-135">Eseguire il comando pack</span><span class="sxs-lookup"><span data-stu-id="f5338-135">Run the pack command</span></span>

<span data-ttu-id="f5338-136">Per compilare un pacchetto NuGet (un file `.nupkg`) dal progetto, eseguire il comando `dotnet pack`, che consente anche di compilare automaticamente il progetto:</span><span class="sxs-lookup"><span data-stu-id="f5338-136">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="f5338-137">L'output mostra il percorso del file `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="f5338-137">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="f5338-138">Generare automaticamente il pacchetto in fase di compilazione</span><span class="sxs-lookup"><span data-stu-id="f5338-138">Automatically generate package on build</span></span>

<span data-ttu-id="f5338-139">Per eseguire automaticamente `dotnet pack` quando si esegue `dotnet build`, aggiungere la riga seguente al file di progetto all'interno di `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="f5338-139">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="f5338-140">Quando si esegue `dotnet pack` per una soluzione, vengono inseriti nel pacchetto tutti i progetti nella soluzione che supportano i pacchetti (proprietà [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) impostata su `true`).</span><span class="sxs-lookup"><span data-stu-id="f5338-140">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="f5338-141">Quando si genera automaticamente il pacchetto, il tempo di creazione del pacchetto aumenta il tempo di compilazione per il progetto.</span><span class="sxs-lookup"><span data-stu-id="f5338-141">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="f5338-142">Testare l'installazione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="f5338-142">Test package installation</span></span>

<span data-ttu-id="f5338-143">Prima di pubblicare un pacchetto, in genere si preferisce testarne il processo di installazione in un progetto.</span><span class="sxs-lookup"><span data-stu-id="f5338-143">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="f5338-144">I test assicurano che i file necessari vengano inseriti nei percorsi corretti all'interno del progetto.</span><span class="sxs-lookup"><span data-stu-id="f5338-144">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="f5338-145">È possibile testare manualmente le installazioni in Visual Studio o dalla riga di comando seguendo i normali [passaggi di installazione del pacchetto](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="f5338-145">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f5338-146">I pacchetti non sono modificabili.</span><span class="sxs-lookup"><span data-stu-id="f5338-146">Packages are immutable.</span></span> <span data-ttu-id="f5338-147">Se si corregge un problema, modificare il contenuto del pacchetto e crearlo di nuovo. Quando si ripetono i test verrà comunque usata la versione precedente del pacchetto fino a quando non si [cancella la cartella dei pacchetti globali](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders).</span><span class="sxs-lookup"><span data-stu-id="f5338-147">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="f5338-148">Questo aspetto è particolarmente importante quando si testano pacchetti che non usano un'etichetta di versione preliminare univoca per ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="f5338-148">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5338-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f5338-149">Next Steps</span></span>

<span data-ttu-id="f5338-150">Dopo aver creato un pacchetto, ovvero un file `.nupkg`, è possibile pubblicarlo nella raccolta di propria scelta, come descritto in [Pubblicazione di un pacchetto](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="f5338-150">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="f5338-151">Potrebbe anche essere necessario estendere le funzionalità del pacchetto o supportare altri scenari, come descritto negli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5338-151">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="f5338-152">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="f5338-152">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="f5338-153">Supportare più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="f5338-153">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="f5338-154">Icona Aggiungi pacchetto</span><span class="sxs-lookup"><span data-stu-id="f5338-154">Add a package icon</span></span>](../reference/nuspec.md#icon)
- [<span data-ttu-id="f5338-155">Trasformazioni di file di origine e di configurazione</span><span class="sxs-lookup"><span data-stu-id="f5338-155">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="f5338-156">Localizzazione</span><span class="sxs-lookup"><span data-stu-id="f5338-156">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="f5338-157">Versioni non definitive</span><span class="sxs-lookup"><span data-stu-id="f5338-157">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="f5338-158">Impostare il tipo di pacchetto</span><span class="sxs-lookup"><span data-stu-id="f5338-158">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="f5338-159">Creare pacchetti con assembly di interoperabilità COM</span><span class="sxs-lookup"><span data-stu-id="f5338-159">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="f5338-160">Sono infine disponibili altri tipi di pacchetti da tenere presenti:</span><span class="sxs-lookup"><span data-stu-id="f5338-160">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="f5338-161">Pacchetti nativi</span><span class="sxs-lookup"><span data-stu-id="f5338-161">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="f5338-162">Pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="f5338-162">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
