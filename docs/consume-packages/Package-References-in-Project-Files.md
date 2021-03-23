---
title: Formato PackageReference NuGet (riferimenti a pacchetti nei file di progetto)
description: Informazioni dettagliate su PackageReference NuGet nei file di progetto, come supportato da NuGet 4.0 +, Visual Studio 2017 e .NET Core 2.0
author: nkolev92
ms.author: nikolev
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: df7c793d115622f04a148cbbc3ebf396a3e4ab69
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859187"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="6d272-103">Riferimenti ai pacchetti ( `PackageReference` ) nei file di progetto</span><span class="sxs-lookup"><span data-stu-id="6d272-103">Package references (`PackageReference`) in project files</span></span>

<span data-ttu-id="6d272-104">I riferimenti ai pacchetti, tramite il nodo `PackageReference`, consentono di gestire le dipendenze di NuGet direttamente all'interno di file di progetto, invece di dover ricorrere a un file `packages.config` separato.</span><span class="sxs-lookup"><span data-stu-id="6d272-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="6d272-105">L'uso di PackageReference non influenza altri aspetti di NuGet. Ad esempio le impostazioni nei file `NuGet.config` (incluse le origini dei pacchetti) vengono comunque applicate come illustrato in [Configurazione comuni di NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="6d272-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="6d272-106">Con PackageReference è inoltre possibile utilizzare le condizioni di MSBuild per scegliere i riferimenti ai pacchetti per ogni Framework di destinazione o altri raggruppamenti.</span><span class="sxs-lookup"><span data-stu-id="6d272-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="6d272-107">Consente anche un controllo più capillare delle dipendenze e del flusso del contenuto.</span><span class="sxs-lookup"><span data-stu-id="6d272-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="6d272-108">(Per altri dettagli, vedere [Pack e restore di NuGet come destinazioni MSBuild ](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="6d272-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="6d272-109">Supporto dei tipi di progetto</span><span class="sxs-lookup"><span data-stu-id="6d272-109">Project type support</span></span>

<span data-ttu-id="6d272-110">Per impostazione predefinita, PackageReference viene usato per i progetti .NET Core, i progetti .NET Standard e i progetti UWP destinati a Windows 10 Build 15063 (Creators Update) e versioni successive, con l'eccezione dei progetti UWP C++.</span><span class="sxs-lookup"><span data-stu-id="6d272-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="6d272-111">I progetti .NET Framework supportano PackageReference, ma usano attualmente `packages.config` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="6d272-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="6d272-112">Per usare PackageReference, [eseguire la migrazione](../consume-packages/migrate-packages-config-to-package-reference.md) delle dipendenze da `packages.config` nel file di progetto, quindi rimuovere packages.config.</span><span class="sxs-lookup"><span data-stu-id="6d272-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="6d272-113">Le app ASP.NET destinate a .NET Framework includono solo un [supporto limitato](https://github.com/NuGet/Home/issues/5877) per PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6d272-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="6d272-114">I tipi di progetto C++ e JavaScript non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="6d272-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="6d272-115">Aggiunta di PackageReference</span><span class="sxs-lookup"><span data-stu-id="6d272-115">Adding a PackageReference</span></span>

<span data-ttu-id="6d272-116">Aggiungere una dipendenza nel file di progetto usando la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="6d272-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="6d272-117">Controllo della versione della dipendenza</span><span class="sxs-lookup"><span data-stu-id="6d272-117">Controlling dependency version</span></span>

<span data-ttu-id="6d272-118">La convenzione per specificare la versione di un pacchetto è uguale quando si usa `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="6d272-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="6d272-119">Nell'esempio precedente, 3.6.0 significa qualsiasi versione > = 3.6.0 con preferenza per la versione più bassa, come descritto in [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="6d272-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="6d272-120">Uso di PackageReference per un progetto senza PackageReference</span><span class="sxs-lookup"><span data-stu-id="6d272-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="6d272-121">Avanzato: se non si hanno pacchetti installati in un progetto (nessun PackageReference nel file di progetto e nessun file packages.config), ma si vuole ripristinare il progetto con stile PackageReference, è possibile impostare una proprietà del progetto RestoreProjectStyle su PackageReference nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="6d272-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="6d272-122">Questa opzione può essere utile se si fa riferimento a progetti con stile PackageReference (progetti con stile SDK o csproj esistenti).</span><span class="sxs-lookup"><span data-stu-id="6d272-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="6d272-123">In questo modo, sarà possibile fare riferimento "in modo transitivo" dal progetto ai pacchetti a cui fanno riferimento tali progetti.</span><span class="sxs-lookup"><span data-stu-id="6d272-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="6d272-124">PackageReference e origini</span><span class="sxs-lookup"><span data-stu-id="6d272-124">PackageReference and sources</span></span>

<span data-ttu-id="6d272-125">Nei progetti PackageReference le versioni delle dipendenze transitive vengono risolte in fase di ripristino.</span><span class="sxs-lookup"><span data-stu-id="6d272-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="6d272-126">Di conseguenza, nei progetti PackageReference è necessario che tutte le origini siano disponibili per tutti i ripristini.</span><span class="sxs-lookup"><span data-stu-id="6d272-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="6d272-127">Versioni mobili</span><span class="sxs-lookup"><span data-stu-id="6d272-127">Floating Versions</span></span>

<span data-ttu-id="6d272-128">Le [versioni mobili](../concepts/dependency-resolution.md#floating-versions) sono supportate con `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="6d272-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="6d272-129">Controllo degli asset delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="6d272-129">Controlling dependency assets</span></span>

<span data-ttu-id="6d272-130">È possibile che si usi una dipendenza esclusivamente come strumento di sviluppo e che non si voglia esporla nei progetti che utilizzano il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6d272-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="6d272-131">In questo scenario, è possibile usare i metadati `PrivateAssets` per controllare questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="6d272-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="6d272-132">I tag di metadati seguenti controllano gli asset delle dipendenze:</span><span class="sxs-lookup"><span data-stu-id="6d272-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="6d272-133">Tag</span><span class="sxs-lookup"><span data-stu-id="6d272-133">Tag</span></span> | <span data-ttu-id="6d272-134">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6d272-134">Description</span></span> | <span data-ttu-id="6d272-135">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="6d272-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d272-136">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="6d272-136">IncludeAssets</span></span> | <span data-ttu-id="6d272-137">Questi asset verranno utilizzati</span><span class="sxs-lookup"><span data-stu-id="6d272-137">These assets will be consumed</span></span> | <span data-ttu-id="6d272-138">all</span><span class="sxs-lookup"><span data-stu-id="6d272-138">all</span></span> |
| <span data-ttu-id="6d272-139">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="6d272-139">ExcludeAssets</span></span> | <span data-ttu-id="6d272-140">Questi asset non verranno utilizzati</span><span class="sxs-lookup"><span data-stu-id="6d272-140">These assets will not be consumed</span></span> | <span data-ttu-id="6d272-141">Nessuno</span><span class="sxs-lookup"><span data-stu-id="6d272-141">none</span></span> |
| <span data-ttu-id="6d272-142">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="6d272-142">PrivateAssets</span></span> | <span data-ttu-id="6d272-143">Questi asset verranno utilizzati, ma non verranno trasferiti al progetto padre</span><span class="sxs-lookup"><span data-stu-id="6d272-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="6d272-144">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="6d272-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="6d272-145">I valori consentiti per questi tag sono i seguenti, con più valori separati da un punto e virgola, ad eccezione di `all` e `none` che devono essere usati da soli:</span><span class="sxs-lookup"><span data-stu-id="6d272-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="6d272-146">Valore</span><span class="sxs-lookup"><span data-stu-id="6d272-146">Value</span></span> | <span data-ttu-id="6d272-147">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6d272-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="6d272-148">compile</span><span class="sxs-lookup"><span data-stu-id="6d272-148">compile</span></span> | <span data-ttu-id="6d272-149">Contenuti della cartella `lib`. Controlla se il progetto può essere compilato in base agli assembly nella cartella</span><span class="sxs-lookup"><span data-stu-id="6d272-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="6d272-150">runtime</span><span class="sxs-lookup"><span data-stu-id="6d272-150">runtime</span></span> | <span data-ttu-id="6d272-151">Contenuti delle cartelle `lib` e `runtimes`. Controlla se questi assembly verranno copiati nella directory di output build</span><span class="sxs-lookup"><span data-stu-id="6d272-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="6d272-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="6d272-152">contentFiles</span></span> | <span data-ttu-id="6d272-153">Contenuto della cartella `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="6d272-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="6d272-154">build</span><span class="sxs-lookup"><span data-stu-id="6d272-154">build</span></span> | <span data-ttu-id="6d272-155">`.props` e `.targets` nella cartella `build`</span><span class="sxs-lookup"><span data-stu-id="6d272-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="6d272-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="6d272-156">buildMultitargeting</span></span> | <span data-ttu-id="6d272-157">*(4.0)* `.props` e `.targets` nella cartella `buildMultitargeting` per più framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="6d272-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="6d272-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="6d272-158">buildTransitive</span></span> | <span data-ttu-id="6d272-159">*(5.0 +)* `.props` e `.targets` nella cartella `buildTransitive` per gli asset che si propagano in modo transitivo a qualsiasi progetto che gli utilizza.</span><span class="sxs-lookup"><span data-stu-id="6d272-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="6d272-160">Vedere la pagina delle [funzionalità](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior).</span><span class="sxs-lookup"><span data-stu-id="6d272-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="6d272-161">analyzers</span><span class="sxs-lookup"><span data-stu-id="6d272-161">analyzers</span></span> | <span data-ttu-id="6d272-162">Analizzatori .NET</span><span class="sxs-lookup"><span data-stu-id="6d272-162">.NET analyzers</span></span> |
| <span data-ttu-id="6d272-163">nativi</span><span class="sxs-lookup"><span data-stu-id="6d272-163">native</span></span> | <span data-ttu-id="6d272-164">Contenuto della cartella `native`</span><span class="sxs-lookup"><span data-stu-id="6d272-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="6d272-165">Nessuno</span><span class="sxs-lookup"><span data-stu-id="6d272-165">none</span></span> | <span data-ttu-id="6d272-166">Non viene usato alcuno dei valori precedenti.</span><span class="sxs-lookup"><span data-stu-id="6d272-166">None of the above are used.</span></span> |
| <span data-ttu-id="6d272-167">all</span><span class="sxs-lookup"><span data-stu-id="6d272-167">all</span></span> | <span data-ttu-id="6d272-168">Tutti i valori precedenti (ad eccezione di `none`)</span><span class="sxs-lookup"><span data-stu-id="6d272-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="6d272-169">Nell'esempio seguente, il progetto utilizzerà tutti gli elementi tranne i file di contenuto dal pacchetto e tutti gli elementi, tranne gli analizzatori e i file di contenuto, verranno trasferiti al progetto padre.</span><span class="sxs-lookup"><span data-stu-id="6d272-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="6d272-170">Si noti che dato che `build` non è incluso in `PrivateAssets`, le destinazioni e le proprietà *verranno trasferite* al progetto padre.</span><span class="sxs-lookup"><span data-stu-id="6d272-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="6d272-171">Si consideri, ad esempio, che il riferimento precedente viene usato in un progetto che compila un pacchetto NuGet chiamato AppLogger.</span><span class="sxs-lookup"><span data-stu-id="6d272-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="6d272-172">AppLogger può utilizzare le destinazioni e le proprietà da `Contoso.Utility.UsefulStuff`, analogamente ai progetti che utilizzano AppLogger.</span><span class="sxs-lookup"><span data-stu-id="6d272-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="6d272-173">Quando `developmentDependency` è impostato su `true` in un file `.nuspec`, un pacchetto viene contrassegnato come dipendenza solo per lo sviluppo, impedendo in tal modo che il pacchetto venga incluso come dipendenza in altri pacchetti.</span><span class="sxs-lookup"><span data-stu-id="6d272-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="6d272-174">Con PackageReference *(NuGet 4.8 +)*, questo flag indica anche che gli asset in fase di compilazione verranno esclusi dalla compilazione.</span><span class="sxs-lookup"><span data-stu-id="6d272-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="6d272-175">Per altre informazioni, vedere [Supporto di DevelopmentDependency per PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="6d272-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="6d272-176">Aggiunta di una condizione PackageReference</span><span class="sxs-lookup"><span data-stu-id="6d272-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="6d272-177">È possibile usare una condizione per controllare se un pacchetto è incluso e le condizioni possono usare qualsiasi variabile di MSBuild o una variabile definita nel file delle destinazioni o delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="6d272-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="6d272-178">Tuttavia, attualmente è supportata solo la variabile `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="6d272-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="6d272-179">Ad esempio, si supponga di usare `netstandard1.4` e `net452` come destinazione, ma di avere una dipendenza applicabile solo per `net452`.</span><span class="sxs-lookup"><span data-stu-id="6d272-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="6d272-180">In questo caso non si vuole che un progetto `netstandard1.4` che utilizza il pacchetto aggiunta tale dipendenza non necessaria.</span><span class="sxs-lookup"><span data-stu-id="6d272-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="6d272-181">Per evitarlo, è possibile specificare una condizione in `PackageReference` come segue:</span><span class="sxs-lookup"><span data-stu-id="6d272-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="6d272-182">Un pacchetto compilato con questo progetto indica che Newtonsoft.Json è incluso come dipendenza solo per una destinazione `net452`:</span><span class="sxs-lookup"><span data-stu-id="6d272-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Risultato dell'applicazione di una condizione per PackageReference con VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="6d272-184">Le condizioni possono essere applicate anche al livello `ItemGroup` e verranno applicate a tutti gli elementi `PackageReference` figlio:</span><span class="sxs-lookup"><span data-stu-id="6d272-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="6d272-185">GeneratePathProperty</span><span class="sxs-lookup"><span data-stu-id="6d272-185">GeneratePathProperty</span></span>

<span data-ttu-id="6d272-186">Questa funzionalità è disponibile con NuGet **5,0** o versione successiva e con Visual Studio 2019 **16,0** o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="6d272-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="6d272-187">A volte è consigliabile fare riferimento a file in un pacchetto da una destinazione MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6d272-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="6d272-188">Nei `packages.config` progetti basati, i pacchetti vengono installati in una cartella relativa al file di progetto.</span><span class="sxs-lookup"><span data-stu-id="6d272-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="6d272-189">In PackageReference, tuttavia, i pacchetti vengono [utilizzati](../concepts/package-installation-process.md) dalla cartella *Global-Packages* , che può variare da computer a computer.</span><span class="sxs-lookup"><span data-stu-id="6d272-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="6d272-190">Per colmare tale lacuna, NuGet ha introdotto una proprietà che punta al percorso da cui verrà utilizzato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6d272-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="6d272-191">Esempio:</span><span class="sxs-lookup"><span data-stu-id="6d272-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="6d272-192">NuGet genera inoltre automaticamente le proprietà per i pacchetti contenenti una cartella degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="6d272-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
```

<span data-ttu-id="6d272-193">Le proprietà di MSBuild e le identità dei pacchetti non hanno le stesse restrizioni, pertanto l'identità del pacchetto deve essere modificata in un nome descrittivo di MSBuild, preceduto dalla parola `Pkg` .</span><span class="sxs-lookup"><span data-stu-id="6d272-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="6d272-194">Per verificare il nome esatto della proprietà generata, esaminare il file [NuGet. g. props](../reference/msbuild-targets.md#restore-outputs) generato.</span><span class="sxs-lookup"><span data-stu-id="6d272-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="packagereference-aliases"></a><span data-ttu-id="6d272-195">Alias PackageReference</span><span class="sxs-lookup"><span data-stu-id="6d272-195">PackageReference Aliases</span></span>

<span data-ttu-id="6d272-196">In alcuni casi rari, i pacchetti diversi conterranno le classi nello stesso spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="6d272-196">In some rare instances different packages will contain classes in the same namespace.</span></span> <span data-ttu-id="6d272-197">A partire da NuGet 5,7 & Visual Studio 2019 Update 7, equivalente a ProjectReference, PackageReference supporta [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases) .</span><span class="sxs-lookup"><span data-stu-id="6d272-197">Starting with NuGet 5.7 & Visual Studio 2019 Update 7, equivalent to ProjectReference, PackageReference supports [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases).</span></span>
<span data-ttu-id="6d272-198">Per impostazione predefinita, non viene specificato alcun alias.</span><span class="sxs-lookup"><span data-stu-id="6d272-198">By default no aliases are provided.</span></span> <span data-ttu-id="6d272-199">Quando viene specificato un alias, è necessario fare riferimento a *tutti* gli assembly provenienti dal pacchetto con annotazioni con un alias.</span><span class="sxs-lookup"><span data-stu-id="6d272-199">When an alias is specified, *all* assemblies coming from the annotated package with need to be referenced with an alias.</span></span>

<span data-ttu-id="6d272-200">È possibile esaminare l'utilizzo di esempio in [NuGet\Samples](https://github.com/NuGet/Samples/tree/main/PackageReferenceAliasesExample)</span><span class="sxs-lookup"><span data-stu-id="6d272-200">You can look at sample usage at [NuGet\Samples](https://github.com/NuGet/Samples/tree/main/PackageReferenceAliasesExample)</span></span>

<span data-ttu-id="6d272-201">Nel file di progetto specificare gli alias come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6d272-201">In the project file, specify the aliases as follows:</span></span>

```xml
  <ItemGroup>
    <PackageReference Include="NuGet.Versioning" Version="5.8.0" Aliases="ExampleAlias" />
  </ItemGroup>
```

<span data-ttu-id="6d272-202">e nel codice lo usano come segue:</span><span class="sxs-lookup"><span data-stu-id="6d272-202">and in the code use it as follows:</span></span>

```cs
extern alias ExampleAlias;

namespace PackageReferenceAliasesExample
{
...
        {
            var version = ExampleAlias.NuGet.Versioning.NuGetVersion.Parse("5.0.0");
            Console.WriteLine($"Version : {version}");
        }
...
}

```

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="6d272-203">Avvisi ed errori di NuGet</span><span class="sxs-lookup"><span data-stu-id="6d272-203">NuGet warnings and errors</span></span>

<span data-ttu-id="6d272-204">*Questa funzionalità è disponibile con NuGet **4,3** o versione successiva e con Visual Studio 2017 **15,3** o versione successiva.*</span><span class="sxs-lookup"><span data-stu-id="6d272-204">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="6d272-205">Per molti scenari di Pack e ripristino, tutti gli avvisi e gli errori di NuGet vengono codificati e iniziano con `NU****` .</span><span class="sxs-lookup"><span data-stu-id="6d272-205">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="6d272-206">Tutti gli avvisi e gli errori di NuGet sono elencati nella documentazione di [riferimento](../reference/errors-and-warnings.md) .</span><span class="sxs-lookup"><span data-stu-id="6d272-206">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="6d272-207">NuGet osserva le seguenti proprietà di avviso:</span><span class="sxs-lookup"><span data-stu-id="6d272-207">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="6d272-208">`TreatWarningsAsErrors`, considera tutti gli avvisi come errori</span><span class="sxs-lookup"><span data-stu-id="6d272-208">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="6d272-209">`WarningsAsErrors`, considera gli avvisi specifici come errori</span><span class="sxs-lookup"><span data-stu-id="6d272-209">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="6d272-210">`NoWarn`, nascondere avvisi specifici, sia a livello di progetto che a livello di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6d272-210">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="6d272-211">Esempi:</span><span class="sxs-lookup"><span data-stu-id="6d272-211">Examples:</span></span>

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="6d272-212">Eliminazione degli avvisi di NuGet</span><span class="sxs-lookup"><span data-stu-id="6d272-212">Suppressing NuGet warnings</span></span>

<span data-ttu-id="6d272-213">Sebbene sia consigliabile risolvere tutti gli avvisi di NuGet durante le operazioni di Pack e ripristino, in determinate situazioni la relativa eliminazione è garantita.</span><span class="sxs-lookup"><span data-stu-id="6d272-213">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="6d272-214">Per evitare l'avviso di un intero progetto, provare a eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6d272-214">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="6d272-215">A volte gli avvisi si applicano solo a un determinato pacchetto nel grafico.</span><span class="sxs-lookup"><span data-stu-id="6d272-215">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="6d272-216">È possibile scegliere di sopprimere l'avviso in modo più selettivo aggiungendo un oggetto nell' `NoWarn` elemento PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6d272-216">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="6d272-217">Eliminazione degli avvisi del pacchetto NuGet in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6d272-217">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="6d272-218">In Visual Studio è anche possibile disattivare gli [avvisi](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) tramite l'IDE.</span><span class="sxs-lookup"><span data-stu-id="6d272-218">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="6d272-219">Blocco delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="6d272-219">Locking dependencies</span></span>

<span data-ttu-id="6d272-220">*Questa funzionalità è disponibile con NuGet **4.9** o versione successiva e con Visual Studio 2017 **15.9** o versione successiva.*</span><span class="sxs-lookup"><span data-stu-id="6d272-220">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="6d272-221">L'input per il ripristino NuGet è un set di riferimenti al pacchetto dal file di progetto (dipendenze dirette o di primo livello) e l'output è una chiusura completa di tutte le dipendenze del pacchetto, incluse le dipendenze transitive.</span><span class="sxs-lookup"><span data-stu-id="6d272-221">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="6d272-222">NuGet prova a produrre sempre la stessa chiusura completa di dipendenze del pacchetto se l'elenco PackageReference di input non è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="6d272-222">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="6d272-223">Esistono tuttavia alcuni scenari in cui non è possibile farlo.</span><span class="sxs-lookup"><span data-stu-id="6d272-223">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="6d272-224">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6d272-224">For example:</span></span>

* <span data-ttu-id="6d272-225">Quando si usano versioni mobili, ad esempio `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="6d272-225">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="6d272-226">Anche se in questo caso la finalità è il passaggio alla versione più recente a ogni ripristino dei pacchetti, esistono scenari in cui gli utenti richiedono che il grafo venga bloccato su una determinata versione più recente e passi a una versione successiva, se disponibile, in caso di movimento esplicito.</span><span class="sxs-lookup"><span data-stu-id="6d272-226">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="6d272-227">Viene pubblicata una versione più recente del pacchetto che risponde ai requisiti di versione di PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6d272-227">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="6d272-228">ad esempio</span><span class="sxs-lookup"><span data-stu-id="6d272-228">E.g.</span></span> 

  * <span data-ttu-id="6d272-229">Giorno 1: si è specificato `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, ma le versioni disponibili nei repository NuGet erano 4.1.0, 4.2.0 e 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="6d272-229">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="6d272-230">In questo caso, NuGet restituirebbe 4.1.0 (la versione minima più vicina)</span><span class="sxs-lookup"><span data-stu-id="6d272-230">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="6d272-231">Giorno 2: viene pubblicata la versione 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="6d272-231">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="6d272-232">NuGet troverà ora la corrispondenza esatta e inizierà a restituire 4.0.0</span><span class="sxs-lookup"><span data-stu-id="6d272-232">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="6d272-233">Una versione del pacchetto specifica viene rimossa dal repository.</span><span class="sxs-lookup"><span data-stu-id="6d272-233">A given package version is removed from the repository.</span></span> <span data-ttu-id="6d272-234">Anche se nuget.org non consente l'eliminazione dei pacchetti, non tutti i repository di pacchetti presentano questo vincolo.</span><span class="sxs-lookup"><span data-stu-id="6d272-234">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="6d272-235">NuGet trova di conseguenza la corrispondenza migliore quando non può restituire la versione eliminata.</span><span class="sxs-lookup"><span data-stu-id="6d272-235">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="6d272-236">Abilitazione del file di blocco</span><span class="sxs-lookup"><span data-stu-id="6d272-236">Enabling lock file</span></span>

<span data-ttu-id="6d272-237">Per rendere persistente la chiusura completa delle dipendenze del pacchetto, è possibile acconsentire esplicitamente alla funzionalità di file di blocco impostando la proprietà MSBuild `RestorePackagesWithLockFile` per il progetto:</span><span class="sxs-lookup"><span data-stu-id="6d272-237">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="6d272-238">Se questa proprietà viene impostata, il ripristino NuGet genererà un file di blocco, il file `packages.lock.json`, nella directory radice del progetto, che elenca tutte le dipendenze del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6d272-238">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="6d272-239">Quando nella directory radice di un progetto è presente il file `packages.lock.json`, il file di blocco viene sempre usato con il ripristino anche se la proprietà `RestorePackagesWithLockFile` non è impostata.</span><span class="sxs-lookup"><span data-stu-id="6d272-239">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="6d272-240">Un altro modo per acconsentire esplicitamente a questa funzionalità è quindi quello di creare un file `packages.lock.json` fittizio vuoto nella directory radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="6d272-240">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="6d272-241">Comportamento di `restore` con il file di blocco</span><span class="sxs-lookup"><span data-stu-id="6d272-241">`restore` behavior with lock file</span></span>
<span data-ttu-id="6d272-242">Se un file di blocco è presente per il progetto, NuGet lo usa per eseguire `restore`.</span><span class="sxs-lookup"><span data-stu-id="6d272-242">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="6d272-243">NuGet esegue un rapido controllo per verificare se sono state apportate modifiche alle dipendenze del pacchetto indicate nel file di progetto (o nei file dei progetti dipendenti) e, se non sono presenti modifiche, si limita a ripristinare i pacchetti indicati nel file di blocco.</span><span class="sxs-lookup"><span data-stu-id="6d272-243">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="6d272-244">Non viene eseguita alcuna rivalutazione delle dipendenze del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6d272-244">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="6d272-245">Se NuGet rileva una modifica nelle dipendenze definite indicate nei file di progetto, rivaluta il grafo del pacchetto e aggiorna il file di blocco in modo da riflettere la nuova chiusura del pacchetto per il progetto.</span><span class="sxs-lookup"><span data-stu-id="6d272-245">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="6d272-246">Per CI/CD e altri scenari in cui non si vogliono modificare le dipendenze del pacchetto immediatamente, è possibile farlo impostando `lockedmode` su `true`:</span><span class="sxs-lookup"><span data-stu-id="6d272-246">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="6d272-247">Per dotnet.exe, eseguire:</span><span class="sxs-lookup"><span data-stu-id="6d272-247">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="6d272-248">Per msbuild.exe, eseguire:</span><span class="sxs-lookup"><span data-stu-id="6d272-248">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="6d272-249">È anche possibile impostare questa proprietà MSBuild condizionale nel file di progetto:</span><span class="sxs-lookup"><span data-stu-id="6d272-249">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="6d272-250">Se la modalità di blocco è `true`, verranno ripristinati i pacchetti esatti elencati nel file di blocco. Il ripristino avrà invece esito negativo se le dipendenze del pacchetto definite per il progetto sono state aggiornate dopo la creazione del file di blocco.</span><span class="sxs-lookup"><span data-stu-id="6d272-250">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="6d272-251">Rendere il file di blocco parte del repository di origine</span><span class="sxs-lookup"><span data-stu-id="6d272-251">Make lock file part of your source repository</span></span>
<span data-ttu-id="6d272-252">Se si compila un'applicazione, un file eseguibile e il progetto in questione sono alla inizio della catena di dipendenze, quindi archiviare il file di blocco nel repository di codice sorgente in modo che NuGet possa usarlo durante il ripristino.</span><span class="sxs-lookup"><span data-stu-id="6d272-252">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="6d272-253">Se tuttavia il progetto è un progetto libreria che non viene distribuito o un progetto di codice comune da cui dipendono altri progetti, **non è consigliabile** archiviare il file di blocco come parte del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="6d272-253">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="6d272-254">È possibile mantenere il file di blocco, ma le dipendenze del pacchetto bloccato per il progetto di codice comune, elencate nel file di blocco, non possono essere usate durante il ripristino o la compilazione di un progetto che dipende da questo progetto di codice comune.</span><span class="sxs-lookup"><span data-stu-id="6d272-254">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="6d272-255">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6d272-255">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="6d272-256">Se `ProjectA` ha una dipendenza da `PackageX` versione `2.0.0` e fa anche riferimento a `ProjectB` che dipende da `PackageX` versione `1.0.0`, il file di blocco per `ProjectB` elencherà una dipendenza da `PackageX` versione `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="6d272-256">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="6d272-257">Tuttavia, quando `ProjectA` viene compilato, il file di blocco conterrà una dipendenza dalla `PackageX` versione **`2.0.0`** e **non** `1.0.0` come elencato nel file di blocco per `ProjectB` .</span><span class="sxs-lookup"><span data-stu-id="6d272-257">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="6d272-258">Di conseguenza, il file di blocco di un progetto di codice comune ha poca influenza sui pacchetti risolti per i progetti che dipendono da esso.</span><span class="sxs-lookup"><span data-stu-id="6d272-258">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="6d272-259">Estendibilità di file di blocco</span><span class="sxs-lookup"><span data-stu-id="6d272-259">Lock file extensibility</span></span>

<span data-ttu-id="6d272-260">È possibile controllare diversi comportamenti di ripristino con file di blocco, come descritto di seguito:</span><span class="sxs-lookup"><span data-stu-id="6d272-260">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="6d272-261">Opzione NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="6d272-261">NuGet.exe option</span></span> | <span data-ttu-id="6d272-262">opzione DotNet</span><span class="sxs-lookup"><span data-stu-id="6d272-262">dotnet option</span></span> | <span data-ttu-id="6d272-263">Opzione MSBuild equivalente</span><span class="sxs-lookup"><span data-stu-id="6d272-263">MSBuild equivalent option</span></span> | <span data-ttu-id="6d272-264">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6d272-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="6d272-265">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="6d272-265">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="6d272-266">Optare per l'utilizzo di un file di blocco.</span><span class="sxs-lookup"><span data-stu-id="6d272-266">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="6d272-267">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="6d272-267">RestoreLockedMode</span></span> | <span data-ttu-id="6d272-268">Abilita la modalità di blocco per il ripristino.</span><span class="sxs-lookup"><span data-stu-id="6d272-268">Enables locked mode for restore.</span></span> <span data-ttu-id="6d272-269">Questa operazione è utile negli scenari CI/CD in cui si desiderano compilazioni ripetibili.</span><span class="sxs-lookup"><span data-stu-id="6d272-269">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="6d272-270">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="6d272-270">RestoreForceEvaluate</span></span> | <span data-ttu-id="6d272-271">Questa opzione è utile con i pacchetti con la versione mobile definita nel progetto.</span><span class="sxs-lookup"><span data-stu-id="6d272-271">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="6d272-272">Per impostazione predefinita, NuGet Restore non aggiornerà automaticamente la versione del pacchetto a ogni ripristino, a meno che non si esegua Restore con questa opzione.</span><span class="sxs-lookup"><span data-stu-id="6d272-272">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="6d272-273">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="6d272-273">NuGetLockFilePath</span></span> | <span data-ttu-id="6d272-274">Definisce un percorso di file di blocco personalizzato per un progetto.</span><span class="sxs-lookup"><span data-stu-id="6d272-274">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="6d272-275">Per impostazione predefinita, NuGet supporta `packages.lock.json` nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="6d272-275">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="6d272-276">Se nella stessa directory sono presenti più progetti, NuGet supporta il file di blocco `packages.<project_name>.lock.json` specifico del progetto</span><span class="sxs-lookup"><span data-stu-id="6d272-276">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |

## <a name="assettargetfallback"></a><span data-ttu-id="6d272-277">AssetTargetFallback</span><span class="sxs-lookup"><span data-stu-id="6d272-277">AssetTargetFallback</span></span>

<span data-ttu-id="6d272-278">La `AssetTargetFallback` proprietà consente di specificare versioni aggiuntive del Framework compatibili per i progetti a cui fa riferimento il progetto e i pacchetti NuGet utilizzati dal progetto.</span><span class="sxs-lookup"><span data-stu-id="6d272-278">The `AssetTargetFallback` property lets you specify additional compatible framework versions for projects that your project references and NuGet packages that your project consumes.</span></span>

<span data-ttu-id="6d272-279">Se si specifica una dipendenza del pacchetto usando `PackageReference` ma il pacchetto non contiene asset compatibili con il Framework di destinazione del progetto, la `AssetTargetFallback` Proprietà entra in gioco.</span><span class="sxs-lookup"><span data-stu-id="6d272-279">If you specify a package dependency using `PackageReference` but that package doesn't contain assets that are compatible with your projects's target framework, the `AssetTargetFallback` property comes into play.</span></span> <span data-ttu-id="6d272-280">La compatibilità del pacchetto a cui si fa riferimento viene riverificata utilizzando ogni Framework di destinazione specificato in `AssetTargetFallback` .</span><span class="sxs-lookup"><span data-stu-id="6d272-280">The compatibility of the referenced package is rechecked using each target framework that's specified in `AssetTargetFallback`.</span></span>
<span data-ttu-id="6d272-281">Quando `project` si fa riferimento a un oggetto o a `package` `AssetTargetFallback` , viene generato l'avviso [NU1701](../reference/errors-and-warnings/NU1701.md) .</span><span class="sxs-lookup"><span data-stu-id="6d272-281">When a `project` or a `package` is referenced through `AssetTargetFallback`, the [NU1701](../reference/errors-and-warnings/NU1701.md) warning will be raised.</span></span>

<span data-ttu-id="6d272-282">Per esempi relativi alla compatibilità, vedere la tabella seguente `AssetTargetFallback` .</span><span class="sxs-lookup"><span data-stu-id="6d272-282">Refer to the table below for examples of how `AssetTargetFallback` affects compatibility.</span></span>

| <span data-ttu-id="6d272-283">Framework del progetto</span><span class="sxs-lookup"><span data-stu-id="6d272-283">Project framework</span></span> | <span data-ttu-id="6d272-284">AssetTargetFallback</span><span class="sxs-lookup"><span data-stu-id="6d272-284">AssetTargetFallback</span></span> | <span data-ttu-id="6d272-285">Framework di pacchetto</span><span class="sxs-lookup"><span data-stu-id="6d272-285">Package frameworks</span></span> | <span data-ttu-id="6d272-286">Risultato</span><span class="sxs-lookup"><span data-stu-id="6d272-286">Result</span></span> |
|-------------------|---------------------|--------------------|--------|
| <span data-ttu-id="6d272-287">.NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="6d272-287">.NET Framework 4.7.2</span></span> | | <span data-ttu-id="6d272-288">.NET Standard 2.0</span><span class="sxs-lookup"><span data-stu-id="6d272-288">.NET Standard 2.0</span></span> | <span data-ttu-id="6d272-289">.NET Standard 2.0</span><span class="sxs-lookup"><span data-stu-id="6d272-289">.NET Standard 2.0</span></span> |
| <span data-ttu-id="6d272-290">App .NET Core 3,1</span><span class="sxs-lookup"><span data-stu-id="6d272-290">.NET Core App 3.1</span></span> | | <span data-ttu-id="6d272-291">.NET Standard 2,0, .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="6d272-291">.NET Standard 2.0, .NET Framework 4.7.2</span></span> | <span data-ttu-id="6d272-292">.NET Standard 2.0</span><span class="sxs-lookup"><span data-stu-id="6d272-292">.NET Standard 2.0</span></span> |
| <span data-ttu-id="6d272-293">App .NET Core 3,1</span><span class="sxs-lookup"><span data-stu-id="6d272-293">.NET Core App 3.1</span></span> | | <span data-ttu-id="6d272-294">.NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="6d272-294">.NET Framework 4.7.2</span></span> | <span data-ttu-id="6d272-295">Incompatibile, con esito negativo [`NU1202`](../reference/errors-and-warnings/NU1202.md)</span><span class="sxs-lookup"><span data-stu-id="6d272-295">Incompatible, fail with [`NU1202`](../reference/errors-and-warnings/NU1202.md)</span></span> |
| <span data-ttu-id="6d272-296">App .NET Core 3,1</span><span class="sxs-lookup"><span data-stu-id="6d272-296">.NET Core App 3.1</span></span> | <span data-ttu-id="6d272-297">net472;net471</span><span class="sxs-lookup"><span data-stu-id="6d272-297">net472;net471</span></span> | <span data-ttu-id="6d272-298">.NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="6d272-298">.NET Framework 4.7.2</span></span> | <span data-ttu-id="6d272-299">.NET Framework 4.7.2 con [`NU1701`](../reference/errors-and-warnings/NU1701.md)</span><span class="sxs-lookup"><span data-stu-id="6d272-299">.NET Framework 4.7.2 with [`NU1701`](../reference/errors-and-warnings/NU1701.md)</span></span> |

<span data-ttu-id="6d272-300">È possibile specificare più Framework utilizzando `;` come delimitatore.</span><span class="sxs-lookup"><span data-stu-id="6d272-300">Multiple frameworks can be specified using `;` as a delimiter.</span></span> <span data-ttu-id="6d272-301">Per aggiungere un Framework di fallback, è possibile eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6d272-301">To add a fallback framework you can do the following:</span></span>

```xml
<AssetTargetFallback Condition=" '$(TargetFramework)'=='netcoreapp3.1' ">
    $(AssetTargetFallback);net472;net471
</AssetTargetFallback>
```

<span data-ttu-id="6d272-302">È possibile lasciare disattivato `$(AssetTargetFallback)` se si desidera sovrascrivere, anziché aggiungere i `AssetTargetFallback` valori esistenti.</span><span class="sxs-lookup"><span data-stu-id="6d272-302">You can leave off `$(AssetTargetFallback)` if you wish to overwrite, instead of add to the existing `AssetTargetFallback` values.</span></span>

> [!NOTE]
> <span data-ttu-id="6d272-303">Se si usa un [progetto basato su .NET SDK](/dotnet/core/sdk), `$(AssetTargetFallback)` vengono configurati i valori appropriati e non è necessario impostarli manualmente.</span><span class="sxs-lookup"><span data-stu-id="6d272-303">If you are using a [.NET SDK based project](/dotnet/core/sdk), appropriate `$(AssetTargetFallback)` values are configured and you do not need to set them manually.</span></span>
>
> <span data-ttu-id="6d272-304">`$(PackageTargetFallback)` era una funzionalità precedente che ha tentato di risolvere questo problema, ma è fondamentalmente interrotta e non *deve* essere usata.</span><span class="sxs-lookup"><span data-stu-id="6d272-304">`$(PackageTargetFallback)` was an earlier feature that attempted to address this challenge, but it is fundamentally broken and *should* not be used.</span></span> <span data-ttu-id="6d272-305">Per eseguire la migrazione da `$(PackageTargetFallback)` a `$(AssetTargetFallback)` , è sufficiente modificare il nome della proprietà.</span><span class="sxs-lookup"><span data-stu-id="6d272-305">To migrate from `$(PackageTargetFallback)` to `$(AssetTargetFallback)`, simply change the property name.</span></span>
