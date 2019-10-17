---
title: Formato PackageReference NuGet (riferimenti a pacchetti nei file di progetto)
description: Informazioni dettagliate su PackageReference NuGet nei file di progetto, come supportato da NuGet 4.0 +, Visual Studio 2017 e .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 892483760a9f3568da7101663e93c69ce3d70b96
ms.sourcegitcommit: 8a424829b1f70cf7590e95db61997af6ae2d7a41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72510807"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="04ec8-103">Riferimenti a pacchetti (PackageReference) nei file di progetto</span><span class="sxs-lookup"><span data-stu-id="04ec8-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="04ec8-104">I riferimenti ai pacchetti, tramite il nodo `PackageReference`, consentono di gestire le dipendenze di NuGet direttamente all'interno di file di progetto, invece di dover ricorrere a un file `packages.config` separato.</span><span class="sxs-lookup"><span data-stu-id="04ec8-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="04ec8-105">L'uso di PackageReference non influenza altri aspetti di NuGet. Ad esempio le impostazioni nei file `NuGet.config` (incluse le origini dei pacchetti) vengono comunque applicate come illustrato in [Configurazione comuni di NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="04ec8-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="04ec8-106">Con PackageReference è anche possibile usare condizioni MSBuild per scegliere i riferimenti ai pacchetti in base a framework di destinazione, configurazione, piattaforma o altri raggruppamenti.</span><span class="sxs-lookup"><span data-stu-id="04ec8-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="04ec8-107">Consente anche un controllo più capillare delle dipendenze e del flusso del contenuto.</span><span class="sxs-lookup"><span data-stu-id="04ec8-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="04ec8-108">(Per altri dettagli, vedere [Pack e restore di NuGet come destinazioni MSBuild ](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="04ec8-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="04ec8-109">Supporto dei tipi di progetto</span><span class="sxs-lookup"><span data-stu-id="04ec8-109">Project type support</span></span>

<span data-ttu-id="04ec8-110">Per impostazione predefinita, PackageReference viene usato per i progetti .NET Core, i progetti .NET Standard e i progetti UWP destinati a Windows 10 Build 15063 (Creators Update) e versioni successive, con l'eccezione dei progetti UWP C++.</span><span class="sxs-lookup"><span data-stu-id="04ec8-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="04ec8-111">I progetti .NET Framework supportano PackageReference, ma usano attualmente `packages.config` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="04ec8-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="04ec8-112">Per usare PackageReference, eseguire la [migrazione](../consume-packages/migrate-packages-config-to-package-reference.md) delle dipendenze da `packages.config` nel file di progetto e quindi rimuovere packages.config.</span><span class="sxs-lookup"><span data-stu-id="04ec8-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="04ec8-113">Le app ASP.NET destinate a .NET Framework includono solo un [supporto limitato](https://github.com/NuGet/Home/issues/5877) per PackageReference.</span><span class="sxs-lookup"><span data-stu-id="04ec8-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="04ec8-114">I tipi di progetto C++ e JavaScript non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="04ec8-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="04ec8-115">Aggiunta di PackageReference</span><span class="sxs-lookup"><span data-stu-id="04ec8-115">Adding a PackageReference</span></span>

<span data-ttu-id="04ec8-116">Aggiungere una dipendenza nel file di progetto usando la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="04ec8-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="04ec8-117">Controllo della versione della dipendenza</span><span class="sxs-lookup"><span data-stu-id="04ec8-117">Controlling dependency version</span></span>

<span data-ttu-id="04ec8-118">La convenzione per specificare la versione di un pacchetto è uguale quando si usa `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="04ec8-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="04ec8-119">Nell'esempio precedente, 3.6.0 significa qualsiasi versione > = 3.6.0 con preferenza per la versione più bassa, come descritto in [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="04ec8-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="04ec8-120">Uso di PackageReference per un progetto senza PackageReference</span><span class="sxs-lookup"><span data-stu-id="04ec8-120">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="04ec8-121">Avanzato: se non si hanno pacchetti installati in un progetto (nessun PackageReference nel file di progetto e nessun file packages.config), ma si vuole ripristinare il progetto con stile PackageReference, è possibile impostare una proprietà del progetto RestoreProjectStyle su PackageReference nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="04ec8-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="04ec8-122">Questa opzione può essere utile se si fa riferimento a progetti con stile PackageReference (progetti con stile SDK o csproj esistenti).</span><span class="sxs-lookup"><span data-stu-id="04ec8-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="04ec8-123">In questo modo, sarà possibile fare riferimento "in modo transitivo" dal progetto ai pacchetti a cui fanno riferimento tali progetti.</span><span class="sxs-lookup"><span data-stu-id="04ec8-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="04ec8-124">Versioni mobili</span><span class="sxs-lookup"><span data-stu-id="04ec8-124">Floating Versions</span></span>

<span data-ttu-id="04ec8-125">Le [versioni mobili](../concepts/dependency-resolution.md#floating-versions) sono supportate con `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="04ec8-125">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="04ec8-126">Controllo degli asset delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="04ec8-126">Controlling dependency assets</span></span>

<span data-ttu-id="04ec8-127">È possibile che si usi una dipendenza esclusivamente come strumento di sviluppo e che non si voglia esporla nei progetti che utilizzano il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="04ec8-127">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="04ec8-128">In questo scenario, è possibile usare i metadati `PrivateAssets` per controllare questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="04ec8-128">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="04ec8-129">I tag di metadati seguenti controllano gli asset delle dipendenze:</span><span class="sxs-lookup"><span data-stu-id="04ec8-129">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="04ec8-130">Tag</span><span class="sxs-lookup"><span data-stu-id="04ec8-130">Tag</span></span> | <span data-ttu-id="04ec8-131">Descrizione</span><span class="sxs-lookup"><span data-stu-id="04ec8-131">Description</span></span> | <span data-ttu-id="04ec8-132">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="04ec8-132">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="04ec8-133">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="04ec8-133">IncludeAssets</span></span> | <span data-ttu-id="04ec8-134">Questi asset verranno utilizzati</span><span class="sxs-lookup"><span data-stu-id="04ec8-134">These assets will be consumed</span></span> | <span data-ttu-id="04ec8-135">tutti</span><span class="sxs-lookup"><span data-stu-id="04ec8-135">all</span></span> |
| <span data-ttu-id="04ec8-136">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="04ec8-136">ExcludeAssets</span></span> | <span data-ttu-id="04ec8-137">Questi asset non verranno utilizzati</span><span class="sxs-lookup"><span data-stu-id="04ec8-137">These assets will not be consumed</span></span> | <span data-ttu-id="04ec8-138">none</span><span class="sxs-lookup"><span data-stu-id="04ec8-138">none</span></span> |
| <span data-ttu-id="04ec8-139">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="04ec8-139">PrivateAssets</span></span> | <span data-ttu-id="04ec8-140">Questi asset verranno utilizzati, ma non verranno trasferiti al progetto padre</span><span class="sxs-lookup"><span data-stu-id="04ec8-140">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="04ec8-141">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="04ec8-141">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="04ec8-142">I valori consentiti per questi tag sono i seguenti, con più valori separati da un punto e virgola, ad eccezione di `all` e `none` che devono essere usati da soli:</span><span class="sxs-lookup"><span data-stu-id="04ec8-142">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="04ec8-143">Value</span><span class="sxs-lookup"><span data-stu-id="04ec8-143">Value</span></span> | <span data-ttu-id="04ec8-144">Descrizione</span><span class="sxs-lookup"><span data-stu-id="04ec8-144">Description</span></span> |
| --- | ---
| <span data-ttu-id="04ec8-145">compile</span><span class="sxs-lookup"><span data-stu-id="04ec8-145">compile</span></span> | <span data-ttu-id="04ec8-146">Contenuti della cartella `lib`. Controlla se il progetto può essere compilato in base agli assembly nella cartella</span><span class="sxs-lookup"><span data-stu-id="04ec8-146">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="04ec8-147">runtime</span><span class="sxs-lookup"><span data-stu-id="04ec8-147">runtime</span></span> | <span data-ttu-id="04ec8-148">Contenuti delle cartelle `lib` e `runtimes`. Controlla se questi assembly verranno copiati nella directory di output build</span><span class="sxs-lookup"><span data-stu-id="04ec8-148">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="04ec8-149">contentFiles</span><span class="sxs-lookup"><span data-stu-id="04ec8-149">contentFiles</span></span> | <span data-ttu-id="04ec8-150">Contenuto della cartella `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="04ec8-150">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="04ec8-151">build</span><span class="sxs-lookup"><span data-stu-id="04ec8-151">build</span></span> | <span data-ttu-id="04ec8-152">`.props` e `.targets` nella cartella `build`</span><span class="sxs-lookup"><span data-stu-id="04ec8-152">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="04ec8-153">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="04ec8-153">buildMultitargeting</span></span> | <span data-ttu-id="04ec8-154">*(4.0)* `.props` e `.targets` nella cartella `buildMultitargeting` per più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="04ec8-154">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="04ec8-155">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="04ec8-155">buildTransitive</span></span> | <span data-ttu-id="04ec8-156">*(5.0 +)* `.props` e `.targets` nella cartella `buildTransitive` per gli asset che si propagano in modo transitivo a qualsiasi progetto che gli utilizza.</span><span class="sxs-lookup"><span data-stu-id="04ec8-156">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="04ec8-157">Vedere la pagina delle [funzionalità](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior).</span><span class="sxs-lookup"><span data-stu-id="04ec8-157">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="04ec8-158">analyzers</span><span class="sxs-lookup"><span data-stu-id="04ec8-158">analyzers</span></span> | <span data-ttu-id="04ec8-159">Analizzatori .NET</span><span class="sxs-lookup"><span data-stu-id="04ec8-159">.NET analyzers</span></span> |
| <span data-ttu-id="04ec8-160">nativi</span><span class="sxs-lookup"><span data-stu-id="04ec8-160">native</span></span> | <span data-ttu-id="04ec8-161">Contenuto della cartella `native`</span><span class="sxs-lookup"><span data-stu-id="04ec8-161">Contents of the `native` folder</span></span> |
| <span data-ttu-id="04ec8-162">none</span><span class="sxs-lookup"><span data-stu-id="04ec8-162">none</span></span> | <span data-ttu-id="04ec8-163">Non viene usato alcuno dei valori precedenti.</span><span class="sxs-lookup"><span data-stu-id="04ec8-163">None of the above are used.</span></span> |
| <span data-ttu-id="04ec8-164">tutti</span><span class="sxs-lookup"><span data-stu-id="04ec8-164">all</span></span> | <span data-ttu-id="04ec8-165">Tutti i valori precedenti (ad eccezione di `none`)</span><span class="sxs-lookup"><span data-stu-id="04ec8-165">All of the above (except `none`)</span></span> |

<span data-ttu-id="04ec8-166">Nell'esempio seguente, il progetto utilizzerà tutti gli elementi tranne i file di contenuto dal pacchetto e tutti gli elementi, tranne gli analizzatori e i file di contenuto, verranno trasferiti al progetto padre.</span><span class="sxs-lookup"><span data-stu-id="04ec8-166">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="04ec8-167">Si noti che dato che `build` non è incluso in `PrivateAssets`, le destinazioni e le proprietà *verranno trasferite* al progetto padre.</span><span class="sxs-lookup"><span data-stu-id="04ec8-167">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="04ec8-168">Si consideri, ad esempio, che il riferimento precedente viene usato in un progetto che compila un pacchetto NuGet chiamato AppLogger.</span><span class="sxs-lookup"><span data-stu-id="04ec8-168">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="04ec8-169">AppLogger può utilizzare le destinazioni e le proprietà da `Contoso.Utility.UsefulStuff`, analogamente ai progetti che utilizzano AppLogger.</span><span class="sxs-lookup"><span data-stu-id="04ec8-169">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="04ec8-170">Quando `developmentDependency` è impostato su `true` in un file `.nuspec`, un pacchetto viene contrassegnato come dipendenza solo per lo sviluppo, impedendo in tal modo che il pacchetto venga incluso come dipendenza in altri pacchetti.</span><span class="sxs-lookup"><span data-stu-id="04ec8-170">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="04ec8-171">Con PackageReference *(NuGet 4.8 +)* , questo flag indica anche che gli asset in fase di compilazione verranno esclusi dalla compilazione.</span><span class="sxs-lookup"><span data-stu-id="04ec8-171">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="04ec8-172">Per altre informazioni, vedere [Supporto di DevelopmentDependency per PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="04ec8-172">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="04ec8-173">Aggiunta di una condizione PackageReference</span><span class="sxs-lookup"><span data-stu-id="04ec8-173">Adding a PackageReference condition</span></span>

<span data-ttu-id="04ec8-174">È possibile usare una condizione per controllare se un pacchetto è incluso e le condizioni possono usare qualsiasi variabile di MSBuild o una variabile definita nel file delle destinazioni o delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="04ec8-174">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="04ec8-175">Tuttavia, attualmente è supportata solo la variabile `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="04ec8-175">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="04ec8-176">Ad esempio, si supponga di usare `netstandard1.4` e `net452` come destinazione, ma di avere una dipendenza applicabile solo per `net452`.</span><span class="sxs-lookup"><span data-stu-id="04ec8-176">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="04ec8-177">In questo caso non si vuole che un progetto `netstandard1.4` che utilizza il pacchetto aggiunta tale dipendenza non necessaria.</span><span class="sxs-lookup"><span data-stu-id="04ec8-177">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="04ec8-178">Per evitarlo, è possibile specificare una condizione in `PackageReference` come segue:</span><span class="sxs-lookup"><span data-stu-id="04ec8-178">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="04ec8-179">Un pacchetto compilato con questo progetto indica che Newtonsoft.Json è incluso come dipendenza solo per una destinazione `net452`:</span><span class="sxs-lookup"><span data-stu-id="04ec8-179">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Risultato dell'applicazione di una condizione per PackageReference con VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="04ec8-181">Le condizioni possono essere applicate anche al livello `ItemGroup` e verranno applicate a tutti gli elementi `PackageReference` figlio:</span><span class="sxs-lookup"><span data-stu-id="04ec8-181">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="04ec8-182">Blocco delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="04ec8-182">Locking dependencies</span></span>
<span data-ttu-id="04ec8-183">*Questa funzionalità è disponibile con NuGet **4.9** o versione successiva e con Visual Studio 2017 **15.9** o versione successiva.*</span><span class="sxs-lookup"><span data-stu-id="04ec8-183">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="04ec8-184">L'input per il ripristino NuGet è un set di riferimenti al pacchetto dal file di progetto (dipendenze dirette o di primo livello) e l'output è una chiusura completa di tutte le dipendenze del pacchetto, incluse le dipendenze transitive.</span><span class="sxs-lookup"><span data-stu-id="04ec8-184">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="04ec8-185">NuGet prova a produrre sempre la stessa chiusura completa di dipendenze del pacchetto se l'elenco PackageReference di input non è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="04ec8-185">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="04ec8-186">Esistono tuttavia alcuni scenari in cui non è possibile farlo.</span><span class="sxs-lookup"><span data-stu-id="04ec8-186">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="04ec8-187">Esempio:</span><span class="sxs-lookup"><span data-stu-id="04ec8-187">For example:</span></span>

* <span data-ttu-id="04ec8-188">Quando si usano versioni mobili, ad esempio `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="04ec8-188">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="04ec8-189">Anche se in questo caso la finalità è il passaggio alla versione più recente a ogni ripristino dei pacchetti, esistono scenari in cui gli utenti richiedono che il grafo venga bloccato su una determinata versione più recente e passi a una versione successiva, se disponibile, in caso di movimento esplicito.</span><span class="sxs-lookup"><span data-stu-id="04ec8-189">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="04ec8-190">Viene pubblicata una versione più recente del pacchetto che risponde ai requisiti di versione di PackageReference.</span><span class="sxs-lookup"><span data-stu-id="04ec8-190">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="04ec8-191">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="04ec8-191">E.g.</span></span> 

  * <span data-ttu-id="04ec8-192">Giorno 1: si è specificato `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, ma le versioni disponibili nei repository NuGet erano 4.1.0, 4.2.0 e 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="04ec8-192">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="04ec8-193">In questo caso, NuGet restituirebbe 4.1.0 (la versione minima più vicina)</span><span class="sxs-lookup"><span data-stu-id="04ec8-193">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="04ec8-194">Giorno 2: viene pubblicata la versione 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="04ec8-194">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="04ec8-195">NuGet troverà ora la corrispondenza esatta e inizierà a restituire 4.0.0</span><span class="sxs-lookup"><span data-stu-id="04ec8-195">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="04ec8-196">Una versione del pacchetto specifica viene rimossa dal repository.</span><span class="sxs-lookup"><span data-stu-id="04ec8-196">A given package version is removed from the repository.</span></span> <span data-ttu-id="04ec8-197">Anche se nuget.org non consente l'eliminazione dei pacchetti, non tutti i repository di pacchetti presentano questo vincolo.</span><span class="sxs-lookup"><span data-stu-id="04ec8-197">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="04ec8-198">NuGet trova di conseguenza la corrispondenza migliore quando non può restituire la versione eliminata.</span><span class="sxs-lookup"><span data-stu-id="04ec8-198">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="04ec8-199">Abilitazione del file di blocco</span><span class="sxs-lookup"><span data-stu-id="04ec8-199">Enabling lock file</span></span>
<span data-ttu-id="04ec8-200">Per rendere persistente la chiusura completa delle dipendenze del pacchetto, è possibile acconsentire esplicitamente alla funzionalità di file di blocco impostando la proprietà MSBuild `RestorePackagesWithLockFile` per il progetto:</span><span class="sxs-lookup"><span data-stu-id="04ec8-200">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="04ec8-201">Se questa proprietà viene impostata, il ripristino NuGet genererà un file di blocco, il file `packages.lock.json`, nella directory radice del progetto, che elenca tutte le dipendenze del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="04ec8-201">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="04ec8-202">Quando nella directory radice di un progetto è presente il file `packages.lock.json`, il file di blocco viene sempre usato con il ripristino anche se la proprietà `RestorePackagesWithLockFile` non è impostata.</span><span class="sxs-lookup"><span data-stu-id="04ec8-202">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="04ec8-203">Un altro modo per acconsentire esplicitamente a questa funzionalità è quindi quello di creare un file `packages.lock.json` fittizio vuoto nella directory radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="04ec8-203">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="04ec8-204">Comportamento di `restore` con il file di blocco</span><span class="sxs-lookup"><span data-stu-id="04ec8-204">`restore` behavior with lock file</span></span>
<span data-ttu-id="04ec8-205">Se un file di blocco è presente per il progetto, NuGet lo usa per eseguire `restore`.</span><span class="sxs-lookup"><span data-stu-id="04ec8-205">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="04ec8-206">NuGet esegue un rapido controllo per verificare se sono state apportate modifiche alle dipendenze del pacchetto indicate nel file di progetto (o nei file dei progetti dipendenti) e, se non sono presenti modifiche, si limita a ripristinare i pacchetti indicati nel file di blocco.</span><span class="sxs-lookup"><span data-stu-id="04ec8-206">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="04ec8-207">Non viene eseguita alcuna rivalutazione delle dipendenze del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="04ec8-207">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="04ec8-208">Se NuGet rileva una modifica nelle dipendenze definite indicate nei file di progetto, rivaluta il grafo del pacchetto e aggiorna il file di blocco in modo da riflettere la nuova chiusura del pacchetto per il progetto.</span><span class="sxs-lookup"><span data-stu-id="04ec8-208">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="04ec8-209">Per CI/CD e altri scenari in cui non si vogliono modificare le dipendenze del pacchetto immediatamente, è possibile farlo impostando `lockedmode` su `true`:</span><span class="sxs-lookup"><span data-stu-id="04ec8-209">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="04ec8-210">Per dotnet.exe, eseguire:</span><span class="sxs-lookup"><span data-stu-id="04ec8-210">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="04ec8-211">Per msbuild.exe, eseguire:</span><span class="sxs-lookup"><span data-stu-id="04ec8-211">For msbuild.exe, run:</span></span>
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="04ec8-212">È anche possibile impostare questa proprietà MSBuild condizionale nel file di progetto:</span><span class="sxs-lookup"><span data-stu-id="04ec8-212">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="04ec8-213">Se la modalità di blocco è `true`, verranno ripristinati i pacchetti esatti elencati nel file di blocco. Il ripristino avrà invece esito negativo se le dipendenze del pacchetto definite per il progetto sono state aggiornate dopo la creazione del file di blocco.</span><span class="sxs-lookup"><span data-stu-id="04ec8-213">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="04ec8-214">Rendere il file di blocco parte del repository di origine</span><span class="sxs-lookup"><span data-stu-id="04ec8-214">Make lock file part of your source repository</span></span>
<span data-ttu-id="04ec8-215">Se si compila un'applicazione, un file eseguibile e il progetto in questione sono alla inizio della catena di dipendenze, quindi archiviare il file di blocco nel repository di codice sorgente in modo che NuGet possa usarlo durante il ripristino.</span><span class="sxs-lookup"><span data-stu-id="04ec8-215">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="04ec8-216">Se tuttavia il progetto è un progetto libreria che non viene distribuito o un progetto di codice comune da cui dipendono altri progetti, **non è consigliabile** archiviare il file di blocco come parte del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="04ec8-216">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="04ec8-217">È possibile mantenere il file di blocco, ma le dipendenze del pacchetto bloccato per il progetto di codice comune, elencate nel file di blocco, non possono essere usate durante il ripristino o la compilazione di un progetto che dipende da questo progetto di codice comune.</span><span class="sxs-lookup"><span data-stu-id="04ec8-217">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="04ec8-218">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="04ec8-218">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="04ec8-219">Se `ProjectA` ha una dipendenza da `PackageX` versione `2.0.0` e fa anche riferimento a `ProjectB` che dipende da `PackageX` versione `1.0.0`, il file di blocco per `ProjectB` elencherà una dipendenza da `PackageX` versione `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="04ec8-219">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="04ec8-220">Quando tuttavia `ProjectA` viene compilato, il file di blocco conterrà una dipendenza da `PackageX` versione **`2.0.0`** e **non** `1.0.0` come elencato nel file di blocco per `ProjectB`.</span><span class="sxs-lookup"><span data-stu-id="04ec8-220">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="04ec8-221">Di conseguenza, il file di blocco di un progetto di codice comune ha poca influenza sui pacchetti risolti per i progetti che dipendono da esso.</span><span class="sxs-lookup"><span data-stu-id="04ec8-221">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="04ec8-222">Estendibilità di file di blocco</span><span class="sxs-lookup"><span data-stu-id="04ec8-222">Lock file extensibility</span></span>

<span data-ttu-id="04ec8-223">È possibile controllare diversi comportamenti di ripristino con file di blocco, come descritto di seguito:</span><span class="sxs-lookup"><span data-stu-id="04ec8-223">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="04ec8-224">Opzione</span><span class="sxs-lookup"><span data-stu-id="04ec8-224">Option</span></span> | <span data-ttu-id="04ec8-225">Opzione MSBuild equivalente</span><span class="sxs-lookup"><span data-stu-id="04ec8-225">MSBuild equivalent option</span></span> | <span data-ttu-id="04ec8-226">Descrizione</span><span class="sxs-lookup"><span data-stu-id="04ec8-226">Description</span></span>|
|:---  |:--- |:--- |
| `--use-lock-file` | <span data-ttu-id="04ec8-227">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="04ec8-227">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="04ec8-228">Optare per l'utilizzo di un file di blocco.</span><span class="sxs-lookup"><span data-stu-id="04ec8-228">Opts into the usage of a lock file.</span></span> | 
| `--locked-mode` | <span data-ttu-id="04ec8-229">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="04ec8-229">RestoreLockedMode</span></span> | <span data-ttu-id="04ec8-230">Abilita la modalità di blocco per il ripristino.</span><span class="sxs-lookup"><span data-stu-id="04ec8-230">Enables locked mode for restore.</span></span> <span data-ttu-id="04ec8-231">Questa operazione è utile negli scenari CI/CD in cui si desiderano compilazioni ripetibili.</span><span class="sxs-lookup"><span data-stu-id="04ec8-231">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `--force-evaluate` | <span data-ttu-id="04ec8-232">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="04ec8-232">RestoreForceEvaluate</span></span> | <span data-ttu-id="04ec8-233">Questa opzione è utile con i pacchetti con la versione mobile definita nel progetto.</span><span class="sxs-lookup"><span data-stu-id="04ec8-233">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="04ec8-234">Per impostazione predefinita, NuGet Restore non aggiornerà automaticamente la versione del pacchetto a ogni ripristino, a meno che non si esegua Restore con questa opzione.</span><span class="sxs-lookup"><span data-stu-id="04ec8-234">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="04ec8-235">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="04ec8-235">NuGetLockFilePath</span></span> | <span data-ttu-id="04ec8-236">Definisce un percorso di file di blocco personalizzato per un progetto.</span><span class="sxs-lookup"><span data-stu-id="04ec8-236">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="04ec8-237">Per impostazione predefinita, NuGet supporta `packages.lock.json` nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="04ec8-237">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="04ec8-238">Se nella stessa directory sono presenti più progetti, NuGet supporta il file di blocco `packages.<project_name>.lock.json` specifico del progetto</span><span class="sxs-lookup"><span data-stu-id="04ec8-238">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
