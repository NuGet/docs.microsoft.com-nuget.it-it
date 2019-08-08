---
title: Creare un pacchetto NuGet con l'interfaccia della riga di comando di dotnet
description: Guida dettagliata al processo di progettazione e creazione di un pacchetto NuGet, incluse le principali decisioni critiche, ad esempio quelle relative ai file e al controllo delle versioni.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: da5dbc8b1659cef66e8439b9a3c3bb2c9205cbe6
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68462461"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="36881-103">Creare un pacchetto NuGet con l'interfaccia della riga di comando di dotnet</span><span class="sxs-lookup"><span data-stu-id="36881-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="36881-104">Indipendentemente dalle operazioni eseguite dal pacchetto o dal tipo di codice contenuto, è possibile usare uno degli strumenti dell'interfaccia della riga di comando, ovvero `nuget.exe` o `dotnet.exe`. per rendere disponibili tali funzionalità in un componente condivisibile e utilizzabile da altri sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="36881-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="36881-105">Questo articolo descrive come creare un pacchetto usando l'interfaccia della riga di comando di dotnet.</span><span class="sxs-lookup"><span data-stu-id="36881-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="36881-106">Per installare l' interfaccia della riga di comando di `dotnet`, vedere [Installare gli strumenti client di NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="36881-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="36881-107">A partire da Visual Studio 2017, l'interfaccia della riga di comando di dotnet è inclusa nei carichi di lavoro di .NET Core.</span><span class="sxs-lookup"><span data-stu-id="36881-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="36881-108">Per i progetti .NET Core e .NET Standard che usano il [formato di tipo SDK](../resources/check-project-format.md), e qualsiasi altro progetto di tipo SDK, NuGet usa le informazioni nel file di progetto direttamente per creare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="36881-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="36881-109">Per esercitazioni dettagliate, vedere [Creare pacchetti .NET Standard con l'interfaccia della riga di comando di dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) e [Creare pacchetti .NET Standard con Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="36881-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md), [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="36881-110">`msbuild -t:pack` dal punto di vista funzionale equivale a `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="36881-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="36881-111">Per lo sviluppo con MSBuild, i concetti sono gli stessi descritti in questo articolo, ma i comandi della riga di comando sono leggermente diversi.</span><span class="sxs-lookup"><span data-stu-id="36881-111">To build with MSBuild, the concepts are the same as described in this article, but the command line commands are slightly different.</span></span> <span data-ttu-id="36881-112">Analogamente, con un progetto non di tipo SDK e `<PackageReference>`, è possibile usare `msbuild /t:pack`.</span><span class="sxs-lookup"><span data-stu-id="36881-112">Similarly, with a non-SDK-style project and `<PackageReference>`, you can use `msbuild /t:pack`.</span></span> <span data-ttu-id="36881-113">In questi scenari è necessario aggiungere il pacchetto NuGet.Build.Tasks.Pack alle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="36881-113">In these scenarios, you need to add the NuGet.Build.Tasks.Pack package to their dependencies.</span></span> <span data-ttu-id="36881-114">Vedere [Pack e restore di NuGet come destinazioni MSBuild.](../reference/msbuild-targets.md)</span><span class="sxs-lookup"><span data-stu-id="36881-114">See [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36881-115">Questo argomento si applica ai progetti [di tipo SDK](../resources/check-project-format.md), in genere progetti .NET Core e .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="36881-115">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="36881-116">Impostare le proprietà</span><span class="sxs-lookup"><span data-stu-id="36881-116">Set properties</span></span>

<span data-ttu-id="36881-117">Per creare un pacchetto, sono necessarie le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="36881-117">The following properties are required to create a package.</span></span>

- <span data-ttu-id="36881-118">`PackageId`, ovvero l'identificatore del pacchetto, che deve essere univoco nella raccolta che ospita il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="36881-118">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="36881-119">Se non è specificato, il valore predefinito è `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="36881-119">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="36881-120">`Version`, ovvero un numero di versione specifico nel formato *Principale.Secondaria.Patch[-Suffisso]* dove *-Suffisso* identifica le [versioni preliminari](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="36881-120">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="36881-121">Se non è specificato, il valore predefinito è 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="36881-121">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="36881-122">Titolo del pacchetto come deve essere visualizzato nell'host (ad esempio, nuget.org)</span><span class="sxs-lookup"><span data-stu-id="36881-122">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="36881-123">`Authors`, ovvero informazioni sull'autore e sul proprietario.</span><span class="sxs-lookup"><span data-stu-id="36881-123">`Authors`, author and owner information.</span></span> <span data-ttu-id="36881-124">Se non è specificato, il valore predefinito è `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="36881-124">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="36881-125">`Company`, ovvero il nome della società.</span><span class="sxs-lookup"><span data-stu-id="36881-125">`Company`, your company name.</span></span> <span data-ttu-id="36881-126">Se non è specificato, il valore predefinito è `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="36881-126">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="36881-127">In Visual Studio è possibile impostare questi valori nelle proprietà del progetto (fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni, scegliere **Proprietà** e selezionare la scheda **Pacchetto**).</span><span class="sxs-lookup"><span data-stu-id="36881-127">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="36881-128">È anche possibile impostare queste proprietà direttamente nei file di progetto (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="36881-128">You can also set these properties directly in the project files (`.csproj`).</span></span>

    ```xml
    <PropertyGroup>
      ...
      <PackageId>AppLogger</PackageId>
      <Version>1.0.0</Version>
      <Authors>your_name</Authors>
      <Company>your_company</Company>
    </PropertyGroup>
    ```

> [!Important]
> <span data-ttu-id="36881-129">Assegnare al pacchetto un identificatore univoco in nuget.org o per l'origine di pacchetti in uso.</span><span class="sxs-lookup"><span data-stu-id="36881-129">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="36881-130">È anche possibile impostare le proprietà facoltative, ad esempio `Title`, `PackageDescription` e `PackageTags`, come descritto in [Destinazioni di pack per MSBuild](../reference/msbuild-targets.md#pack-target), [Controllo degli asset delle dipendenze](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) e [Proprietà dei metadati NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="36881-130">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="36881-131">Per i pacchetti compilati per uso pubblico, prestare particolare attenzione alla proprietà **PackageTags**, perché questi tag consentono ad altri utenti di trovare il pacchetto e di comprenderne le funzioni.</span><span class="sxs-lookup"><span data-stu-id="36881-131">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="36881-132">Per informazioni dettagliate sulla dichiarazione delle dipendenze e sulla specifica dei numeri di versione, vedere [Controllo delle versioni dei pacchetti](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="36881-132">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="36881-133">È anche possibile esporre gli asset dalle dipendenze direttamente nel pacchetto usando gli attributi `<IncludeAssets>` e `<ExcludeAssets>`.</span><span class="sxs-lookup"><span data-stu-id="36881-133">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="36881-134">Per altre informazioni, vedere [Controllo degli asset delle dipendenze](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="36881-134">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="36881-135">Scegliere un identificatore univoco del pacchetto e impostare il numero di versione</span><span class="sxs-lookup"><span data-stu-id="36881-135">Choose a unique package identifier and set the version number</span></span>

<span data-ttu-id="36881-136">L'identificatore del pacchetto e il numero di versione sono i due valori più importanti del progetto perché identificano in modo univoco il codice esatto contenuto nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="36881-136">The package identifier and the version number are the two most important values in the project because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="36881-137">**Procedure consigliate per l'identificatore del pacchetto:**</span><span class="sxs-lookup"><span data-stu-id="36881-137">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="36881-138">**Univocità**: l'identificatore deve essere univoco in nuget.org o in qualsiasi raccolta che ospita il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="36881-138">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="36881-139">Prima di scegliere un identificatore, eseguire una ricerca nella raccolta applicabile per controllare se il nome è già in uso.</span><span class="sxs-lookup"><span data-stu-id="36881-139">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="36881-140">Per evitare conflitti, è consigliabile usare il nome della società come prima parte dell'identificatore, ad esempio `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="36881-140">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="36881-141">**Nomi simili a spazi dei nomi**: seguono un modello simile a quello degli spazi dei nomi in .NET, usando la notazione con punto invece dei trattini.</span><span class="sxs-lookup"><span data-stu-id="36881-141">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="36881-142">Usare, ad esempio, `Contoso.Utility.UsefulStuff` invece di `Contoso-Utility-UsefulStuff` o `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="36881-142">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="36881-143">Per gli utenti è anche utile che l'identificatore del pacchetto corrisponda agli spazi dei nomi usati nel codice.</span><span class="sxs-lookup"><span data-stu-id="36881-143">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="36881-144">**Pacchetti di esempio**: se si produce un pacchetto di codice di esempio che illustra come usare un altro pacchetto, aggiungere `.Sample` come suffisso all'identificatore, come in `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="36881-144">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="36881-145">Il pacchetto di esempio avrà naturalmente una dipendenza dall'altro pacchetto. Quando si crea un pacchetto di esempio, usare il valore `contentFiles` in `<IncludeAssets>`.</span><span class="sxs-lookup"><span data-stu-id="36881-145">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the `contentFiles` value in `<IncludeAssets>`.</span></span> <span data-ttu-id="36881-146">Nella cartella `content` inserire il codice di esempio in una cartella denominata `\Samples\<identifier>` come in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="36881-146">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="36881-147">**Procedure consigliate per la versione del pacchetto:**</span><span class="sxs-lookup"><span data-stu-id="36881-147">**Best practices for the package version:**</span></span>

- <span data-ttu-id="36881-148">In generale, impostare la versione del pacchetto in modo che corrisponda al progetto (o all'assembly), anche se non è strettamente necessario.</span><span class="sxs-lookup"><span data-stu-id="36881-148">In general, set the version of the package to match the project (or assembly), though this is not strictly required.</span></span> <span data-ttu-id="36881-149">Si tratta di un'operazione semplice quando si limita un pacchetto a un singolo assembly.</span><span class="sxs-lookup"><span data-stu-id="36881-149">This is a simple matter when you limit a package to a single assembly.</span></span> <span data-ttu-id="36881-150">In generale, tenere presente che, durante la risoluzione delle dipendenze, di per sé NuGet gestisce le versioni dei pacchetti, non le versioni degli assembly.</span><span class="sxs-lookup"><span data-stu-id="36881-150">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="36881-151">Quando si usa uno schema della versione non standard, tenere in considerazione le regole di controllo delle versioni di NuGet, come illustrato in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="36881-151">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="36881-152">NuGet è in gran parte [conforme a semver 2](../reference/package-versioning.md#semantic-versioning-200).</span><span class="sxs-lookup"><span data-stu-id="36881-152">NuGet is mostly [semver 2 compliant](../reference/package-versioning.md#semantic-versioning-200).</span></span>

> <span data-ttu-id="36881-153">Per informazioni sulla risoluzione delle dipendenze, vedere [Risoluzione delle dipendenze con PackageReference](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).</span><span class="sxs-lookup"><span data-stu-id="36881-153">For information on dependency resolution, see [Dependency resolution with PackageReference](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).</span></span> <span data-ttu-id="36881-154">Per informazioni meno recenti che possono essere utili anche per comprendere meglio il controllo delle versioni, vedere questa serie di post di blog.</span><span class="sxs-lookup"><span data-stu-id="36881-154">For older information that may also be helpful to better understand versioning, see this series of blog posts.</span></span>
>
> - <span data-ttu-id="36881-155">[Parte 1. Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html) (Parte 1: Affrontare l'inferno delle DLL)</span><span class="sxs-lookup"><span data-stu-id="36881-155">[Part 1: Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)</span></span>
> - <span data-ttu-id="36881-156">[Parte 2. The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html) (Parte 2: L'algoritmo principale)</span><span class="sxs-lookup"><span data-stu-id="36881-156">[Part 2: The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)</span></span>
> - <span data-ttu-id="36881-157">[Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html) (Parte 3: Unificazione tramite i reindirizzamenti di binding)</span><span class="sxs-lookup"><span data-stu-id="36881-157">[Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="36881-158">Eseguire il comando pack</span><span class="sxs-lookup"><span data-stu-id="36881-158">Run the pack command</span></span>

<span data-ttu-id="36881-159">Per compilare un pacchetto NuGet (un file `.nupkg`) dal progetto, eseguire il comando `dotnet pack`, che consente anche di compilare automaticamente il progetto:</span><span class="sxs-lookup"><span data-stu-id="36881-159">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="36881-160">L'output mostra il percorso del file `.nupkg`:</span><span class="sxs-lookup"><span data-stu-id="36881-160">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="36881-161">Generare automaticamente il pacchetto in fase di compilazione</span><span class="sxs-lookup"><span data-stu-id="36881-161">Automatically generate package on build</span></span>

<span data-ttu-id="36881-162">Per eseguire automaticamente `dotnet pack` quando si esegue `dotnet build`, aggiungere la riga seguente al file di progetto all'interno di `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="36881-162">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="36881-163">Quando si esegue `dotnet pack` per una soluzione, vengono inseriti nel pacchetto tutti i progetti nella soluzione che supportano i pacchetti (proprietà [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) impostata su `true`).</span><span class="sxs-lookup"><span data-stu-id="36881-163">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="36881-164">Quando si genera automaticamente il pacchetto, il tempo di creazione del pacchetto aumenta il tempo di compilazione per il progetto.</span><span class="sxs-lookup"><span data-stu-id="36881-164">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="36881-165">Testare l'installazione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="36881-165">Test package installation</span></span>

<span data-ttu-id="36881-166">Prima di pubblicare un pacchetto, in genere si preferisce testarne il processo di installazione in un progetto.</span><span class="sxs-lookup"><span data-stu-id="36881-166">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="36881-167">I test assicurano che i file necessari vengano inseriti nei percorsi corretti all'interno del progetto.</span><span class="sxs-lookup"><span data-stu-id="36881-167">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="36881-168">È possibile testare manualmente le installazioni in Visual Studio o dalla riga di comando seguendo i normali [passaggi di installazione del pacchetto](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="36881-168">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36881-169">I pacchetti non sono modificabili.</span><span class="sxs-lookup"><span data-stu-id="36881-169">Packages are immutable.</span></span> <span data-ttu-id="36881-170">Se si corregge un problema, modificare il contenuto del pacchetto e crearlo di nuovo. Quando si ripetono i test verrà comunque usata la versione precedente del pacchetto fino a quando non si [cancella la cartella dei pacchetti globali](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders).</span><span class="sxs-lookup"><span data-stu-id="36881-170">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="36881-171">Questo aspetto è particolarmente importante quando si testano pacchetti che non usano un'etichetta di versione preliminare univoca per ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="36881-171">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36881-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="36881-172">Next Steps</span></span>

<span data-ttu-id="36881-173">Dopo aver creato un pacchetto, ovvero un file `.nupkg`, è possibile pubblicarlo nella raccolta di propria scelta, come descritto in [Pubblicazione di un pacchetto](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="36881-173">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="36881-174">Potrebbe anche essere necessario estendere le funzionalità del pacchetto o supportare altri scenari, come descritto negli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="36881-174">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="36881-175">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="36881-175">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="36881-176">Supportare più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="36881-176">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="36881-177">Trasformazioni di file di origine e di configurazione</span><span class="sxs-lookup"><span data-stu-id="36881-177">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="36881-178">Localizzazione</span><span class="sxs-lookup"><span data-stu-id="36881-178">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="36881-179">Versioni non definitive</span><span class="sxs-lookup"><span data-stu-id="36881-179">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="36881-180">Impostare il tipo di pacchetto</span><span class="sxs-lookup"><span data-stu-id="36881-180">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="36881-181">Creare pacchetti con assembly di interoperabilità COM</span><span class="sxs-lookup"><span data-stu-id="36881-181">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="36881-182">Sono infine disponibili altri tipi di pacchetti da tenere presenti:</span><span class="sxs-lookup"><span data-stu-id="36881-182">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="36881-183">Pacchetti nativi</span><span class="sxs-lookup"><span data-stu-id="36881-183">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="36881-184">Pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="36881-184">Symbol Packages</span></span>](../create-packages/symbol-packages.md)