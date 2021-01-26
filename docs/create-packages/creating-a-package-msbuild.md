---
title: Creare un pacchetto NuGet usando MSBuild
description: Guida dettagliata al processo di progettazione e creazione di un pacchetto NuGet, incluse le principali decisioni critiche, ad esempio quelle relative ai file e al controllo delle versioni.
author: JonDouglas
ms.author: jodou
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 48741668af932a532240f2796a9bf5d490ee8e35
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774436"
---
# <a name="create-a-nuget-package-using-msbuild"></a><span data-ttu-id="28603-103">Creare un pacchetto NuGet usando MSBuild</span><span class="sxs-lookup"><span data-stu-id="28603-103">Create a NuGet package using MSBuild</span></span>

<span data-ttu-id="28603-104">Quando si crea un pacchetto NuGet dal codice, si rendono disponibili tali funzionalità in un componente condivisibile e utilizzabile da altri sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="28603-104">When you create a NuGet package from your code, you package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="28603-105">Questo articolo descrive come creare un pacchetto usando MSBuild.</span><span class="sxs-lookup"><span data-stu-id="28603-105">This article describes how to create a package using MSBuild.</span></span> <span data-ttu-id="28603-106">MSBuild viene preinstallato con tutti i carichi di lavoro di Visual Studio che contengono NuGet.</span><span class="sxs-lookup"><span data-stu-id="28603-106">MSBuild comes preinstalled with every Visual Studio workload that contains NuGet.</span></span> <span data-ttu-id="28603-107">Inoltre, è possibile usare MSBuild anche tramite l'interfaccia della riga di comando DotNet con [DotNet MSBuild](/dotnet/core/tools/dotnet-msbuild).</span><span class="sxs-lookup"><span data-stu-id="28603-107">Additionally you can also use MSBuild through the dotnet CLI with [dotnet msbuild](/dotnet/core/tools/dotnet-msbuild).</span></span>

<span data-ttu-id="28603-108">Per i progetti .NET Core e .NET Standard che usano il [formato di tipo SDK](../resources/check-project-format.md), e qualsiasi altro progetto di tipo SDK, NuGet usa le informazioni nel file di progetto direttamente per creare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="28603-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span>  <span data-ttu-id="28603-109">Anche per un progetto di tipo non SDK che usa `<PackageReference>`, NuGet usa il file di progetto per creare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="28603-109">For a non-SDK-style project that uses `<PackageReference>`, NuGet also uses the project file to create a package.</span></span>

<span data-ttu-id="28603-110">Nei progetti di tipo SDK la funzionalità pack è disponibile per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="28603-110">SDK-style projects have the pack functionality available by default.</span></span> <span data-ttu-id="28603-111">Per i progetti PackageReference di tipo non SDK, è necessario aggiungere il pacchetto NuGet.Build.Tasks.Pack alle dipendenze del progetto.</span><span class="sxs-lookup"><span data-stu-id="28603-111">For non SDK-style PackageReference projects, you need to add the NuGet.Build.Tasks.Pack package to the project dependencies.</span></span> <span data-ttu-id="28603-112">Per informazioni dettagliate sulle destinazioni pack MSBuild, vedere [Pack e restore di NuGet come destinazioni MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="28603-112">For detailed information about MSBuild pack targets, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

<span data-ttu-id="28603-113">Il comando che crea un pacchetto, `msbuild -t:pack`, è una funzionalità equivalente a `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="28603-113">The command that creates a package, `msbuild -t:pack`, is functionality equivalent to `dotnet pack`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="28603-114">Questo argomento si applica ai progetti di [tipo SDK](../resources/check-project-format.md), in genere progetti .NET Core e .NET Standard, e ai progetti di tipo non SDK che usano PackageReference.</span><span class="sxs-lookup"><span data-stu-id="28603-114">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects, and to non-SDK-style projects that use PackageReference.</span></span>

## <a name="set-properties"></a><span data-ttu-id="28603-115">Impostare le proprietà</span><span class="sxs-lookup"><span data-stu-id="28603-115">Set properties</span></span>

<span data-ttu-id="28603-116">Per creare un pacchetto, sono necessarie le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="28603-116">The following properties are required to create a package.</span></span>

- <span data-ttu-id="28603-117">`PackageId`, ovvero l'identificatore del pacchetto, che deve essere univoco nella raccolta che ospita il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="28603-117">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="28603-118">Se non è specificato, il valore predefinito è `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="28603-118">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="28603-119">`Version`, ovvero un numero di versione specifico nel formato *Principale.Secondaria.Patch[-Suffisso]* dove *-Suffisso* identifica le [versioni preliminari](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="28603-119">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="28603-120">Se non è specificato, il valore predefinito è 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="28603-120">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="28603-121">Titolo del pacchetto come deve essere visualizzato nell'host (ad esempio, nuget.org)</span><span class="sxs-lookup"><span data-stu-id="28603-121">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="28603-122">`Authors`, ovvero informazioni sull'autore e sul proprietario.</span><span class="sxs-lookup"><span data-stu-id="28603-122">`Authors`, author and owner information.</span></span> <span data-ttu-id="28603-123">Se non è specificato, il valore predefinito è `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="28603-123">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="28603-124">`Company`, ovvero il nome della società.</span><span class="sxs-lookup"><span data-stu-id="28603-124">`Company`, your company name.</span></span> <span data-ttu-id="28603-125">Se non è specificato, il valore predefinito è `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="28603-125">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="28603-126">Inoltre, se si stanno comprimendo progetti di tipo non SDK che usano PackageReference, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="28603-126">Additionally if you are packing non-SDK-style projects that use PackageReference, the following is required:</span></span>

- <span data-ttu-id="28603-127">`PackageOutputPath`, la cartella di output per il pacchetto generato quando si chiama Pack.</span><span class="sxs-lookup"><span data-stu-id="28603-127">`PackageOutputPath`, the output folder for the package generated when calling pack.</span></span>

<span data-ttu-id="28603-128">In Visual Studio è possibile impostare questi valori nelle proprietà del progetto (fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni, scegliere **Proprietà** e selezionare la scheda **Pacchetto**).</span><span class="sxs-lookup"><span data-stu-id="28603-128">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="28603-129">È anche possibile impostare queste proprietà direttamente nei file di progetto (con estensione *csproj*).</span><span class="sxs-lookup"><span data-stu-id="28603-129">You can also set these properties directly in the project files (*.csproj*).</span></span>

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="28603-130">Assegnare al pacchetto un identificatore univoco in nuget.org o per l'origine di pacchetti in uso.</span><span class="sxs-lookup"><span data-stu-id="28603-130">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="28603-131">L'esempio seguente illustra un file di progetto semplice e completo con queste proprietà incluse.</span><span class="sxs-lookup"><span data-stu-id="28603-131">The following example shows a simple, complete project file with these properties included.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="28603-132">È anche possibile impostare le proprietà facoltative, ad esempio `Title`, `PackageDescription` e `PackageTags`, come descritto in [Destinazioni di pack per MSBuild](../reference/msbuild-targets.md#pack-target), [Controllo degli asset delle dipendenze](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) e [Proprietà dei metadati NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="28603-132">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="28603-133">Per i pacchetti compilati per uso pubblico, prestare particolare attenzione alla proprietà **PackageTags**, perché questi tag consentono ad altri utenti di trovare il pacchetto e di comprenderne le funzioni.</span><span class="sxs-lookup"><span data-stu-id="28603-133">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="28603-134">Per informazioni dettagliate sulla dichiarazione delle dipendenze e sulla specifica dei numeri di versione, vedere [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md) e [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="28603-134">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="28603-135">È anche possibile esporre gli asset dalle dipendenze direttamente nel pacchetto usando gli attributi `<IncludeAssets>` e `<ExcludeAssets>`.</span><span class="sxs-lookup"><span data-stu-id="28603-135">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="28603-136">Per altre informazioni, vedere [Controllo degli asset delle dipendenze](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="28603-136">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="28603-137">Aggiungere un campo di descrizione facoltativo</span><span class="sxs-lookup"><span data-stu-id="28603-137">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="28603-138">Scegliere un identificatore univoco del pacchetto e impostare il numero di versione</span><span class="sxs-lookup"><span data-stu-id="28603-138">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a><span data-ttu-id="28603-139">Aggiungere il pacchetto NuGet.Build.Tasks.Pack</span><span class="sxs-lookup"><span data-stu-id="28603-139">Add the NuGet.Build.Tasks.Pack package</span></span>

<span data-ttu-id="28603-140">Se si usa MSBuild con un progetto di tipo non SDK e PackageReference, aggiungere il pacchetto NuGet.Build.Tasks.Pack al progetto.</span><span class="sxs-lookup"><span data-stu-id="28603-140">If you are using MSBuild with a non-SDK-style project and PackageReference, add the NuGet.Build.Tasks.Pack package to your project.</span></span>

1. <span data-ttu-id="28603-141">Aprire il file di progetto e aggiungere quanto segue dopo l'elemento `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="28603-141">Open the project file and add the following after the `<PropertyGroup>` element:</span></span>

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="28603-142">Aprire un prompt dei comandi per gli sviluppatori digitando **Prompt dei comandi per gli sviluppatori** nella casella **Cerca**.</span><span class="sxs-lookup"><span data-stu-id="28603-142">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="28603-143">In genere, è consigliabile avviare il prompt dei comandi per gli sviluppatori per Visual Studio dal menu **Start**, in modo che venga configurato con tutti i percorsi necessari per MSBuild.</span><span class="sxs-lookup"><span data-stu-id="28603-143">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

3. <span data-ttu-id="28603-144">Passare alla cartella contenente il file di progetto e digitare il comando seguente per installare il pacchetto NuGet.Build.Tasks.Pack.</span><span class="sxs-lookup"><span data-stu-id="28603-144">Switch to the folder containing the project file and type the following command to install the NuGet.Build.Tasks.Pack package.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   <span data-ttu-id="28603-145">Verificare che l'output di MSBuild indichi che la compilazione è stata completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="28603-145">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="run-the-msbuild--tpack-command"></a><span data-ttu-id="28603-146">Eseguire il comando msbuild -t:pack</span><span class="sxs-lookup"><span data-stu-id="28603-146">Run the msbuild -t:pack command</span></span>

<span data-ttu-id="28603-147">Per compilare un pacchetto NuGet (un file `.nupkg`) dal progetto, eseguire il comando `msbuild -t:pack`, che consente anche di compilare automaticamente il progetto:</span><span class="sxs-lookup"><span data-stu-id="28603-147">To build a NuGet package (a `.nupkg` file) from the project, run the `msbuild -t:pack` command, which also builds the project automatically:</span></span>

<span data-ttu-id="28603-148">Al prompt dei comandi per gli sviluppatori per Visual Studio digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="28603-148">In the Developer command prompt for Visual Studio, type the following command:</span></span>

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

<span data-ttu-id="28603-149">L'output mostra il percorso del file `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="28603-149">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="28603-150">Generare automaticamente il pacchetto in fase di compilazione</span><span class="sxs-lookup"><span data-stu-id="28603-150">Automatically generate package on build</span></span>

<span data-ttu-id="28603-151">Per eseguire automaticamente `msbuild -t:pack` quando si compila o si ripristina il progetto, aggiungere la riga seguente al file di progetto all'interno di `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="28603-151">To automatically run `msbuild -t:pack` when you build or restore the project, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="28603-152">Quando si esegue `msbuild -t:pack` su una soluzione, questo comprime tutti i progetti nella soluzione che possono essere compressi (la [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) proprietà è impostata su `true` ).</span><span class="sxs-lookup"><span data-stu-id="28603-152">When you run `msbuild -t:pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="28603-153">Quando si genera automaticamente il pacchetto, il tempo di creazione del pacchetto aumenta il tempo di compilazione per il progetto.</span><span class="sxs-lookup"><span data-stu-id="28603-153">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="28603-154">Testare l'installazione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="28603-154">Test package installation</span></span>

<span data-ttu-id="28603-155">Prima di pubblicare un pacchetto, in genere si preferisce testarne il processo di installazione in un progetto.</span><span class="sxs-lookup"><span data-stu-id="28603-155">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="28603-156">I test assicurano che i file necessari vengano inseriti nei percorsi corretti all'interno del progetto.</span><span class="sxs-lookup"><span data-stu-id="28603-156">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="28603-157">È possibile testare manualmente le installazioni in Visual Studio o dalla riga di comando seguendo i normali [passaggi di installazione del pacchetto](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="28603-157">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="28603-158">I pacchetti non sono modificabili.</span><span class="sxs-lookup"><span data-stu-id="28603-158">Packages are immutable.</span></span> <span data-ttu-id="28603-159">Se si corregge un problema, modificare il contenuto del pacchetto e crearlo di nuovo. Quando si ripetono i test verrà comunque usata la versione precedente del pacchetto fino a quando non si [cancella la cartella dei pacchetti globali](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders).</span><span class="sxs-lookup"><span data-stu-id="28603-159">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="28603-160">Questo aspetto è particolarmente importante quando si testano pacchetti che non usano un'etichetta di versione preliminare univoca per ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="28603-160">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28603-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="28603-161">Next Steps</span></span>

<span data-ttu-id="28603-162">Dopo aver creato un pacchetto, ovvero un file `.nupkg`, è possibile pubblicarlo nella raccolta di propria scelta, come descritto in [Pubblicazione di un pacchetto](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="28603-162">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="28603-163">Potrebbe anche essere necessario estendere le funzionalità del pacchetto o supportare altri scenari, come descritto negli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="28603-163">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="28603-164">Pack e restore di NuGet come destinazioni MSBuild</span><span class="sxs-lookup"><span data-stu-id="28603-164">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
- [<span data-ttu-id="28603-165">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="28603-165">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="28603-166">Supportare più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="28603-166">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="28603-167">Trasformazioni di file di origine e di configurazione</span><span class="sxs-lookup"><span data-stu-id="28603-167">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="28603-168">Localizzazione</span><span class="sxs-lookup"><span data-stu-id="28603-168">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="28603-169">Versioni non definitive</span><span class="sxs-lookup"><span data-stu-id="28603-169">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="28603-170">Impostare il tipo di pacchetto</span><span class="sxs-lookup"><span data-stu-id="28603-170">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="28603-171">Creare pacchetti con assembly di interoperabilità COM</span><span class="sxs-lookup"><span data-stu-id="28603-171">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="28603-172">Sono infine disponibili altri tipi di pacchetti da tenere presenti:</span><span class="sxs-lookup"><span data-stu-id="28603-172">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="28603-173">Pacchetti nativi</span><span class="sxs-lookup"><span data-stu-id="28603-173">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="28603-174">Pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="28603-174">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)