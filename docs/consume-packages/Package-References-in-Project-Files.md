---
title: Formato PackageReference NuGet (riferimenti a pacchetti nei file di progetto)
description: Informazioni dettagliate su PackageReference NuGet nei file di progetto, come supportato da NuGet 4.0 +, Visual Studio 2017 e .NET Core 2.0
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 8f277a8af7f988d6fdcfa75c43a10b3792c2ae22
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="682c5-103">Riferimenti a pacchetti (PackageReference) nei file di progetto</span><span class="sxs-lookup"><span data-stu-id="682c5-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="682c5-104">I riferimenti ai pacchetti, tramite il nodo `PackageReference`, consentono di gestire le dipendenze di NuGet direttamente all'interno di file di progetto, invece di dover ricorrere a un file `packages.config` separato.</span><span class="sxs-lookup"><span data-stu-id="682c5-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="682c5-105">L'uso di PackageReference non influenza altri aspetti di NuGet. Ad esempio le impostazioni nei file `NuGet.Config` (incluse le origini dei pacchetti) vengono comunque applicate come illustrato in [Configurazione del comportamento di NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="682c5-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="682c5-106">Con PackageReference è anche possibile usare condizioni MSBuild per scegliere i riferimenti ai pacchetti in base a framework di destinazione, configurazione, piattaforma o altri raggruppamenti.</span><span class="sxs-lookup"><span data-stu-id="682c5-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="682c5-107">Consente anche un controllo più capillare delle dipendenze e del flusso del contenuto.</span><span class="sxs-lookup"><span data-stu-id="682c5-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="682c5-108">(Per altri dettagli, vedere [Pack e restore di NuGet come destinazioni MSBuild ](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="682c5-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="682c5-109">Per impostazione predefinita, PackageReference viene usato per i progetti .NET Core, i progetti .NET Standard e i progetti UWP destinati a Windows 10 Build 15063 (Creators Update) e versioni successive, con l'eccezione dei progetti UWP C++.</span><span class="sxs-lookup"><span data-stu-id="682c5-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="682c5-110">I progetti .NET Framework completi supportano PackageReference, ma usano attualmente `packages.config` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="682c5-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="682c5-111">Per usare PackageReference, eseguire la migrazione delle dipendenze da `packages.config` nel file di progetto e quindi rimuovere packages.config.</span><span class="sxs-lookup"><span data-stu-id="682c5-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="682c5-112">Aggiunta di PackageReference</span><span class="sxs-lookup"><span data-stu-id="682c5-112">Adding a PackageReference</span></span>

<span data-ttu-id="682c5-113">Aggiungere una dipendenza nel file di progetto usando la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="682c5-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="682c5-114">Controllo della versione della dipendenza</span><span class="sxs-lookup"><span data-stu-id="682c5-114">Controlling dependency version</span></span>

<span data-ttu-id="682c5-115">La convenzione per specificare la versione di un pacchetto è uguale quando si usa `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="682c5-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="682c5-116">Nell'esempio precedente, 3.6.0 significa qualsiasi versione > = 3.6.0 con preferenza per la versione più bassa, come descritto in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="682c5-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="682c5-117">Versioni mobili</span><span class="sxs-lookup"><span data-stu-id="682c5-117">Floating Versions</span></span>

<span data-ttu-id="682c5-118">Le [versioni mobili](../consume-packages/dependency-resolution.md#floating-versions) sono supportate con `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="682c5-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="682c5-119">Controllo degli asset delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="682c5-119">Controlling dependency assets</span></span>

<span data-ttu-id="682c5-120">È possibile che si usi una dipendenza esclusivamente come strumento di sviluppo e che non si voglia esporla nei progetti che utilizzano il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="682c5-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="682c5-121">In questo scenario, è possibile usare i metadati `PrivateAssets` per controllare questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="682c5-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="682c5-122">I tag di metadati seguenti controllano gli asset delle dipendenze:</span><span class="sxs-lookup"><span data-stu-id="682c5-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="682c5-123">Tag</span><span class="sxs-lookup"><span data-stu-id="682c5-123">Tag</span></span> | <span data-ttu-id="682c5-124">Descrizione</span><span class="sxs-lookup"><span data-stu-id="682c5-124">Description</span></span> | <span data-ttu-id="682c5-125">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="682c5-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="682c5-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="682c5-126">IncludeAssets</span></span> | <span data-ttu-id="682c5-127">Questi asset verranno utilizzati</span><span class="sxs-lookup"><span data-stu-id="682c5-127">These assets will be consumed</span></span> | <span data-ttu-id="682c5-128">tutti</span><span class="sxs-lookup"><span data-stu-id="682c5-128">all</span></span> |
| <span data-ttu-id="682c5-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="682c5-129">ExcludeAssets</span></span> | <span data-ttu-id="682c5-130">Questi asset non verranno utilizzati</span><span class="sxs-lookup"><span data-stu-id="682c5-130">These assets will not be consumed</span></span> | <span data-ttu-id="682c5-131">none</span><span class="sxs-lookup"><span data-stu-id="682c5-131">none</span></span> |
| <span data-ttu-id="682c5-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="682c5-132">PrivateAssets</span></span> | <span data-ttu-id="682c5-133">Questi asset verranno utilizzati, ma non verranno trasferiti al progetto padre</span><span class="sxs-lookup"><span data-stu-id="682c5-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="682c5-134">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="682c5-134">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="682c5-135">I valori consentiti per questi tag sono i seguenti, con più valori separati da un punto e virgola, ad eccezione di `all` e `none` che devono essere usati da soli:</span><span class="sxs-lookup"><span data-stu-id="682c5-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="682c5-136">Valore</span><span class="sxs-lookup"><span data-stu-id="682c5-136">Value</span></span> | <span data-ttu-id="682c5-137">Descrizione</span><span class="sxs-lookup"><span data-stu-id="682c5-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="682c5-138">compile</span><span class="sxs-lookup"><span data-stu-id="682c5-138">compile</span></span> | <span data-ttu-id="682c5-139">Contenuti della cartella `lib`. Controlla se il progetto può essere compilato in base agli assembly nella cartella</span><span class="sxs-lookup"><span data-stu-id="682c5-139">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="682c5-140">runtime</span><span class="sxs-lookup"><span data-stu-id="682c5-140">runtime</span></span> | <span data-ttu-id="682c5-141">Contenuti delle cartelle `lib` e `runtimes`. Controlla se questi assembly verranno copiati nella directory di output build</span><span class="sxs-lookup"><span data-stu-id="682c5-141">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="682c5-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="682c5-142">contentFiles</span></span> | <span data-ttu-id="682c5-143">Contenuto della cartella `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="682c5-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="682c5-144">build</span><span class="sxs-lookup"><span data-stu-id="682c5-144">build</span></span> | <span data-ttu-id="682c5-145">Proprietà e destinazioni nella cartella `build`</span><span class="sxs-lookup"><span data-stu-id="682c5-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="682c5-146">analyzers</span><span class="sxs-lookup"><span data-stu-id="682c5-146">analyzers</span></span> | <span data-ttu-id="682c5-147">Analizzatori .NET</span><span class="sxs-lookup"><span data-stu-id="682c5-147">.NET analyzers</span></span> |
| <span data-ttu-id="682c5-148">native</span><span class="sxs-lookup"><span data-stu-id="682c5-148">native</span></span> | <span data-ttu-id="682c5-149">Contenuto della cartella `native`</span><span class="sxs-lookup"><span data-stu-id="682c5-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="682c5-150">none</span><span class="sxs-lookup"><span data-stu-id="682c5-150">none</span></span> | <span data-ttu-id="682c5-151">Non viene usato alcuno dei valori precedenti.</span><span class="sxs-lookup"><span data-stu-id="682c5-151">None of the above are used.</span></span> |
| <span data-ttu-id="682c5-152">tutti</span><span class="sxs-lookup"><span data-stu-id="682c5-152">all</span></span> | <span data-ttu-id="682c5-153">Tutti i valori precedenti (ad eccezione di `none`)</span><span class="sxs-lookup"><span data-stu-id="682c5-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="682c5-154">Nell'esempio seguente, il progetto utilizzerà tutti gli elementi tranne i file di contenuto dal pacchetto e tutti gli elementi, tranne gli analizzatori e i file di contenuto, verranno trasferiti al progetto padre.</span><span class="sxs-lookup"><span data-stu-id="682c5-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="682c5-155">Si noti che dato che `build` non è incluso in `PrivateAssets`, le destinazioni e le proprietà *verranno trasferite* al progetto padre.</span><span class="sxs-lookup"><span data-stu-id="682c5-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="682c5-156">Si consideri, ad esempio, che il riferimento precedente viene usato in un progetto che compila un pacchetto NuGet chiamato AppLogger.</span><span class="sxs-lookup"><span data-stu-id="682c5-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="682c5-157">AppLogger può utilizzare le destinazioni e le proprietà da `Contoso.Utility.UsefulStuff`, analogamente ai progetti che utilizzano AppLogger.</span><span class="sxs-lookup"><span data-stu-id="682c5-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="682c5-158">Aggiunta di una condizione PackageReference</span><span class="sxs-lookup"><span data-stu-id="682c5-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="682c5-159">È possibile usare una condizione per controllare se un pacchetto è incluso e le condizioni possono usare qualsiasi variabile di MSBuild o una variabile definita nel file delle destinazioni o delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="682c5-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="682c5-160">Tuttavia, attualmente è supportata solo la variabile `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="682c5-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="682c5-161">Ad esempio, si supponga di usare `netstandard1.4` e `net452` come destinazione, ma di avere una dipendenza applicabile solo per `net452`.</span><span class="sxs-lookup"><span data-stu-id="682c5-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="682c5-162">In questo caso non si vuole che un progetto `netstandard1.4` che utilizza il pacchetto aggiunta tale dipendenza non necessaria.</span><span class="sxs-lookup"><span data-stu-id="682c5-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="682c5-163">Per evitarlo, è possibile specificare una condizione in `PackageReference` come segue:</span><span class="sxs-lookup"><span data-stu-id="682c5-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="682c5-164">Un pacchetto compilato con questo progetto indicherà che Newtonsoft.json è incluso come dipendenza solo per una destinazione `net452`:</span><span class="sxs-lookup"><span data-stu-id="682c5-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Risultato dell'applicazione di una condizione per PackageReference con VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="682c5-166">Le condizioni possono essere applicate anche al livello `ItemGroup` e verranno applicate a tutti gli elementi `PackageReference` figlio:</span><span class="sxs-lookup"><span data-stu-id="682c5-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
