---
title: PackageReference NuGet nei file di progetto di Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: Informazioni dettagliate su PackageReference NuGet nei file di progetto, come supportato da NuGet 4.0 + e VS2017
keywords: Dipendenze dei pacchetti NuGet, riferimenti a pacchetti, file di progetto, PackageReference, packages.config, project.json, VS2017, Visual Studio 2017, NuGet 4
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 275957c94e4a4bb45f359cd48816acf4f286ebad
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="b8c87-104">Riferimenti a pacchetti (PackageReference) nei file di progetto</span><span class="sxs-lookup"><span data-stu-id="b8c87-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="b8c87-105">I riferimenti ai pacchetti, tramite il nodo `PackageReference`, consentono di gestire le dipendenze di NuGet direttamente all'interno di file di progetto, invece di dover ricorrere a un file `packages.config` o `project.json` separato.</span><span class="sxs-lookup"><span data-stu-id="b8c87-105">Package references, using the `PackageReference` node, allow you to manage NuGet dependencies directly within project files, rather than needing a separate `packages.config` or `project.json` file.</span></span> <span data-ttu-id="b8c87-106">Questo metodo non influenza altri aspetti di NuGet. Ad esempio le impostazioni nei file `NuGet.Config` (incluse le origini dei pacchetti) vengono comunque applicate come illustrato in [Configurazione del comportamento di NuGet](Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="b8c87-106">This method doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](Configuring-NuGet-Behavior.md).</span></span>

> [!Important]
> <span data-ttu-id="b8c87-107">Al momento, i riferimenti ai pacchetti sono supportati solo in Visual Studio 2017, per i progetti .NET Core, i progetti .NET Standard e i progetti UWP destinati a Windows 10 Build 15063 (Creators Update).</span><span class="sxs-lookup"><span data-stu-id="b8c87-107">At present, package references are supported in Visual Studio 2017 only, for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update).</span></span>

<span data-ttu-id="b8c87-108">L'approccio `PackageReference` consente di usare condizioni MSBuild per scegliere i riferimenti ai pacchetti in base a framework di destinazione, configurazione, piattaforma o altri raggruppamenti.</span><span class="sxs-lookup"><span data-stu-id="b8c87-108">The `PackageReference` approach allows you to use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="b8c87-109">Consente anche un controllo più capillare delle dipendenze e del flusso del contenuto.</span><span class="sxs-lookup"><span data-stu-id="b8c87-109">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="b8c87-110">In termini di comportamento e [risoluzione delle dipendenze](Dependency-Resolution.md) equivale a usare `project.json`.</span><span class="sxs-lookup"><span data-stu-id="b8c87-110">In terms of behavior and [dependency resolution](Dependency-Resolution.md), it's the same as using `project.json`.</span></span>

<span data-ttu-id="b8c87-111">Per altre informazioni sull'integrazione di MSBuild con i riferimenti ai pacchetti nei file di progetto, vedere [Pack e restore di NuGet come destinazioni MSBuild](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="b8c87-111">For more details on the integration of MSBuild with package references in project files, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="b8c87-112">Aggiunta di PackageReference</span><span class="sxs-lookup"><span data-stu-id="b8c87-112">Adding a PackageReference</span></span>

<span data-ttu-id="b8c87-113">Aggiungere una dipendenza nel file di progetto usando la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="b8c87-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />    
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="b8c87-114">Controllo della versione della dipendenza</span><span class="sxs-lookup"><span data-stu-id="b8c87-114">Controlling dependency version</span></span>

<span data-ttu-id="b8c87-115">La convenzione per specificare la versione di un pacchetto è uguale quando si usa `packages.config` o `project.json`:</span><span class="sxs-lookup"><span data-stu-id="b8c87-115">The convention for specifying the version of a package is the same as when using `packages.config` or `project.json`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="b8c87-116">Nell'esempio precedente, 3.6.0 significa qualsiasi versione > = 3.6.0 con preferenza per la versione più bassa, come descritto in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="b8c87-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="b8c87-117">Versioni mobili</span><span class="sxs-lookup"><span data-stu-id="b8c87-117">Floating Versions</span></span>

<span data-ttu-id="b8c87-118">Le [versioni mobili](../consume-packages/dependency-resolution.md#floating-versions) sono supportate con `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="b8c87-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="b8c87-119">Controllo degli asset delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="b8c87-119">Controlling dependency assets</span></span>

<span data-ttu-id="b8c87-120">È possibile che si usi una dipendenza esclusivamente come strumento di sviluppo e che non si voglia esporla nei progetti che utilizzano il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b8c87-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="b8c87-121">In questo scenario, è possibile usare i metadati `PrivateAssets` per controllare questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="b8c87-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="b8c87-122">I tag di metadati seguenti controllano gli asset delle dipendenze:</span><span class="sxs-lookup"><span data-stu-id="b8c87-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="b8c87-123">Tag</span><span class="sxs-lookup"><span data-stu-id="b8c87-123">Tag</span></span> | <span data-ttu-id="b8c87-124">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b8c87-124">Description</span></span> | <span data-ttu-id="b8c87-125">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="b8c87-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b8c87-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="b8c87-126">IncludeAssets</span></span> | <span data-ttu-id="b8c87-127">Questi asset verranno utilizzati</span><span class="sxs-lookup"><span data-stu-id="b8c87-127">These assets will be consumed</span></span> | <span data-ttu-id="b8c87-128">tutti</span><span class="sxs-lookup"><span data-stu-id="b8c87-128">all</span></span> |
| <span data-ttu-id="b8c87-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="b8c87-129">ExcludeAssets</span></span> | <span data-ttu-id="b8c87-130">Questi asset non verranno utilizzati</span><span class="sxs-lookup"><span data-stu-id="b8c87-130">These assets will not be consumed</span></span> | <span data-ttu-id="b8c87-131">none</span><span class="sxs-lookup"><span data-stu-id="b8c87-131">none</span></span> | 
| <span data-ttu-id="b8c87-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="b8c87-132">PrivateAssets</span></span> | <span data-ttu-id="b8c87-133">Questi asset verranno utilizzati, ma non verranno trasferiti al progetto padre</span><span class="sxs-lookup"><span data-stu-id="b8c87-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="b8c87-134">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="b8c87-134">contentfiles;analyzers;build</span></span> |


<span data-ttu-id="b8c87-135">I valori consentiti per questi tag sono i seguenti, con più valori separati da un punto e virgola, ad eccezione di `all` e `none` che devono essere usati da soli:</span><span class="sxs-lookup"><span data-stu-id="b8c87-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="b8c87-136">Valore</span><span class="sxs-lookup"><span data-stu-id="b8c87-136">Value</span></span> | <span data-ttu-id="b8c87-137">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b8c87-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="b8c87-138">compile</span><span class="sxs-lookup"><span data-stu-id="b8c87-138">compile</span></span> | <span data-ttu-id="b8c87-139">Contenuto della cartella `lib`</span><span class="sxs-lookup"><span data-stu-id="b8c87-139">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="b8c87-140">runtime</span><span class="sxs-lookup"><span data-stu-id="b8c87-140">runtime</span></span> | <span data-ttu-id="b8c87-141">Contenuto della cartella `runtime`</span><span class="sxs-lookup"><span data-stu-id="b8c87-141">Contents of the `runtime` folder</span></span> |
| <span data-ttu-id="b8c87-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="b8c87-142">contentFiles</span></span> | <span data-ttu-id="b8c87-143">Contenuto della cartella `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="b8c87-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="b8c87-144">build</span><span class="sxs-lookup"><span data-stu-id="b8c87-144">build</span></span> | <span data-ttu-id="b8c87-145">Proprietà e destinazioni nella cartella `build`</span><span class="sxs-lookup"><span data-stu-id="b8c87-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="b8c87-146">analyzers</span><span class="sxs-lookup"><span data-stu-id="b8c87-146">analyzers</span></span> | <span data-ttu-id="b8c87-147">Analizzatori .NET</span><span class="sxs-lookup"><span data-stu-id="b8c87-147">.NET analyzers</span></span> |
| <span data-ttu-id="b8c87-148">native</span><span class="sxs-lookup"><span data-stu-id="b8c87-148">native</span></span> | <span data-ttu-id="b8c87-149">Contenuto della cartella `native`</span><span class="sxs-lookup"><span data-stu-id="b8c87-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="b8c87-150">none</span><span class="sxs-lookup"><span data-stu-id="b8c87-150">none</span></span> | <span data-ttu-id="b8c87-151">Non viene usato alcuno dei valori precedenti.</span><span class="sxs-lookup"><span data-stu-id="b8c87-151">None of the above are used.</span></span> |
| <span data-ttu-id="b8c87-152">tutti</span><span class="sxs-lookup"><span data-stu-id="b8c87-152">all</span></span> | <span data-ttu-id="b8c87-153">Tutti i valori precedenti (ad eccezione di `none`)</span><span class="sxs-lookup"><span data-stu-id="b8c87-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="b8c87-154">Nell'esempio seguente, il progetto utilizzerà tutti gli elementi tranne i file di contenuto dal pacchetto e tutti gli elementi, tranne gli analizzatori e i file di contenuto, verranno trasferiti al progetto padre.</span><span class="sxs-lookup"><span data-stu-id="b8c87-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="b8c87-155">Si noti che dato che `build` non è incluso in `PrivateAssets`, le destinazioni e le proprietà *verranno trasferite* al progetto padre.</span><span class="sxs-lookup"><span data-stu-id="b8c87-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="b8c87-156">Si consideri, ad esempio, che il riferimento precedente viene usato in un progetto che compila un pacchetto NuGet chiamato AppLogger.</span><span class="sxs-lookup"><span data-stu-id="b8c87-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="b8c87-157">AppLogger può utilizzare le destinazioni e le proprietà da `Contoso.Utility.UsefulStuff`, analogamente ai progetti che utilizzano AppLogger.</span><span class="sxs-lookup"><span data-stu-id="b8c87-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="b8c87-158">Aggiunta di una condizione PackageReference</span><span class="sxs-lookup"><span data-stu-id="b8c87-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="b8c87-159">È possibile usare una condizione per controllare se un pacchetto è incluso e le condizioni possono usare qualsiasi variabile di MSBuild o una variabile definita nel file delle destinazioni o delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="b8c87-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="b8c87-160">Tuttavia, attualmente è supportata solo la variabile `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="b8c87-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="b8c87-161">Ad esempio, si supponga di usare `netstandard1.4` e `net452` come destinazione, ma di avere una dipendenza applicabile solo per `net452`.</span><span class="sxs-lookup"><span data-stu-id="b8c87-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="b8c87-162">In questo caso non si vuole che un progetto `netstandard1.4` che utilizza il pacchetto aggiunta tale dipendenza non necessaria.</span><span class="sxs-lookup"><span data-stu-id="b8c87-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="b8c87-163">Per evitarlo, è possibile specificare una condizione in `PackageReference` come segue:</span><span class="sxs-lookup"><span data-stu-id="b8c87-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="b8c87-164">Un pacchetto compilato con questo progetto indicherà che Newtonsoft.json è incluso come dipendenza solo per una destinazione `net452`:</span><span class="sxs-lookup"><span data-stu-id="b8c87-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Risultato dell'applicazione di una condizione per PackageReference con VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="b8c87-166">Le condizioni possono essere applicate anche al livello `ItemGroup` e verranno applicate a tutti gli elementi `PackageReference` figlio:</span><span class="sxs-lookup"><span data-stu-id="b8c87-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
