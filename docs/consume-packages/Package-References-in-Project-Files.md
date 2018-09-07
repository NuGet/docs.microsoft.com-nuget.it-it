---
title: Formato PackageReference NuGet (riferimenti a pacchetti nei file di progetto)
description: Informazioni dettagliate su PackageReference NuGet nei file di progetto, come supportato da NuGet 4.0 +, Visual Studio 2017 e .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9ae8e8dc4e7e901acacffed8b7dfb4162c5ad2b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551390"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="7795e-103">Riferimenti a pacchetti (PackageReference) nei file di progetto</span><span class="sxs-lookup"><span data-stu-id="7795e-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="7795e-104">I riferimenti ai pacchetti, tramite il nodo `PackageReference`, consentono di gestire le dipendenze di NuGet direttamente all'interno di file di progetto, invece di dover ricorrere a un file `packages.config` separato.</span><span class="sxs-lookup"><span data-stu-id="7795e-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="7795e-105">L'uso di PackageReference non influenza altri aspetti di NuGet. Ad esempio le impostazioni nei file `NuGet.Config` (incluse le origini dei pacchetti) vengono comunque applicate come illustrato in [Configurazione del comportamento di NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="7795e-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="7795e-106">Con PackageReference è anche possibile usare condizioni MSBuild per scegliere i riferimenti ai pacchetti in base a framework di destinazione, configurazione, piattaforma o altri raggruppamenti.</span><span class="sxs-lookup"><span data-stu-id="7795e-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="7795e-107">Consente anche un controllo più capillare delle dipendenze e del flusso del contenuto.</span><span class="sxs-lookup"><span data-stu-id="7795e-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="7795e-108">(Per altri dettagli, vedere [Pack e restore di NuGet come destinazioni MSBuild ](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="7795e-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="7795e-109">Per impostazione predefinita, PackageReference viene usato per i progetti .NET Core, i progetti .NET Standard e i progetti UWP destinati a Windows 10 Build 15063 (Creators Update) e versioni successive, con l'eccezione dei progetti UWP C++.</span><span class="sxs-lookup"><span data-stu-id="7795e-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="7795e-110">I progetti .NET Framework completi supportano PackageReference, ma usano attualmente `packages.config` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="7795e-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="7795e-111">Per usare PackageReference, eseguire la migrazione delle dipendenze da `packages.config` nel file di progetto e quindi rimuovere packages.config.</span><span class="sxs-lookup"><span data-stu-id="7795e-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="7795e-112">Aggiunta di PackageReference</span><span class="sxs-lookup"><span data-stu-id="7795e-112">Adding a PackageReference</span></span>

<span data-ttu-id="7795e-113">Aggiungere una dipendenza nel file di progetto usando la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="7795e-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="7795e-114">Controllo della versione della dipendenza</span><span class="sxs-lookup"><span data-stu-id="7795e-114">Controlling dependency version</span></span>

<span data-ttu-id="7795e-115">La convenzione per specificare la versione di un pacchetto è uguale quando si usa `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="7795e-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="7795e-116">Nell'esempio precedente, 3.6.0 significa qualsiasi versione > = 3.6.0 con preferenza per la versione più bassa, come descritto in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="7795e-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="7795e-117">Uso di PackageReference per un progetto senza PackageReference</span><span class="sxs-lookup"><span data-stu-id="7795e-117">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="7795e-118">Avanzato: se non si hanno pacchetti installati in un progetto (nessun PackageReference nel file di progetto e nessun file packages.config), ma si vuole ripristinare il progetto con stile PackageReference, è possibile impostare una proprietà del progetto RestoreProjectStyle su PackageReference nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="7795e-118">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="7795e-119">Questa opzione può essere utile se si fa riferimento a progetti con stile PackageReference (progetti con stile SDK o csproj esistenti).</span><span class="sxs-lookup"><span data-stu-id="7795e-119">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="7795e-120">In questo modo, sarà possibile fare riferimento "in modo transitivo" dal progetto ai pacchetti a cui fanno riferimento tali progetti.</span><span class="sxs-lookup"><span data-stu-id="7795e-120">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="7795e-121">Versioni mobili</span><span class="sxs-lookup"><span data-stu-id="7795e-121">Floating Versions</span></span>

<span data-ttu-id="7795e-122">Le [versioni mobili](../consume-packages/dependency-resolution.md#floating-versions) sono supportate con `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="7795e-122">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="7795e-123">Controllo degli asset delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="7795e-123">Controlling dependency assets</span></span>

<span data-ttu-id="7795e-124">È possibile che si usi una dipendenza esclusivamente come strumento di sviluppo e che non si voglia esporla nei progetti che utilizzano il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="7795e-124">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="7795e-125">In questo scenario, è possibile usare i metadati `PrivateAssets` per controllare questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="7795e-125">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="7795e-126">I tag di metadati seguenti controllano gli asset delle dipendenze:</span><span class="sxs-lookup"><span data-stu-id="7795e-126">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="7795e-127">Tag</span><span class="sxs-lookup"><span data-stu-id="7795e-127">Tag</span></span> | <span data-ttu-id="7795e-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7795e-128">Description</span></span> | <span data-ttu-id="7795e-129">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="7795e-129">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7795e-130">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="7795e-130">IncludeAssets</span></span> | <span data-ttu-id="7795e-131">Questi asset verranno utilizzati</span><span class="sxs-lookup"><span data-stu-id="7795e-131">These assets will be consumed</span></span> | <span data-ttu-id="7795e-132">tutti</span><span class="sxs-lookup"><span data-stu-id="7795e-132">all</span></span> |
| <span data-ttu-id="7795e-133">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="7795e-133">ExcludeAssets</span></span> | <span data-ttu-id="7795e-134">Questi asset non verranno utilizzati</span><span class="sxs-lookup"><span data-stu-id="7795e-134">These assets will not be consumed</span></span> | <span data-ttu-id="7795e-135">none</span><span class="sxs-lookup"><span data-stu-id="7795e-135">none</span></span> |
| <span data-ttu-id="7795e-136">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="7795e-136">PrivateAssets</span></span> | <span data-ttu-id="7795e-137">Questi asset verranno utilizzati, ma non verranno trasferiti al progetto padre</span><span class="sxs-lookup"><span data-stu-id="7795e-137">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="7795e-138">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="7795e-138">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="7795e-139">I valori consentiti per questi tag sono i seguenti, con più valori separati da un punto e virgola, ad eccezione di `all` e `none` che devono essere usati da soli:</span><span class="sxs-lookup"><span data-stu-id="7795e-139">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="7795e-140">Valore</span><span class="sxs-lookup"><span data-stu-id="7795e-140">Value</span></span> | <span data-ttu-id="7795e-141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7795e-141">Description</span></span> |
| --- | ---
| <span data-ttu-id="7795e-142">compile</span><span class="sxs-lookup"><span data-stu-id="7795e-142">compile</span></span> | <span data-ttu-id="7795e-143">Contenuti della cartella `lib`. Controlla se il progetto può essere compilato in base agli assembly nella cartella</span><span class="sxs-lookup"><span data-stu-id="7795e-143">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="7795e-144">runtime</span><span class="sxs-lookup"><span data-stu-id="7795e-144">runtime</span></span> | <span data-ttu-id="7795e-145">Contenuti delle cartelle `lib` e `runtimes`. Controlla se questi assembly verranno copiati nella directory di output build</span><span class="sxs-lookup"><span data-stu-id="7795e-145">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="7795e-146">contentFiles</span><span class="sxs-lookup"><span data-stu-id="7795e-146">contentFiles</span></span> | <span data-ttu-id="7795e-147">Contenuto della cartella `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="7795e-147">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="7795e-148">build</span><span class="sxs-lookup"><span data-stu-id="7795e-148">build</span></span> | <span data-ttu-id="7795e-149">Proprietà e destinazioni nella cartella `build`</span><span class="sxs-lookup"><span data-stu-id="7795e-149">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="7795e-150">analyzers</span><span class="sxs-lookup"><span data-stu-id="7795e-150">analyzers</span></span> | <span data-ttu-id="7795e-151">Analizzatori .NET</span><span class="sxs-lookup"><span data-stu-id="7795e-151">.NET analyzers</span></span> |
| <span data-ttu-id="7795e-152">native</span><span class="sxs-lookup"><span data-stu-id="7795e-152">native</span></span> | <span data-ttu-id="7795e-153">Contenuto della cartella `native`</span><span class="sxs-lookup"><span data-stu-id="7795e-153">Contents of the `native` folder</span></span> |
| <span data-ttu-id="7795e-154">none</span><span class="sxs-lookup"><span data-stu-id="7795e-154">none</span></span> | <span data-ttu-id="7795e-155">Non viene usato alcuno dei valori precedenti.</span><span class="sxs-lookup"><span data-stu-id="7795e-155">None of the above are used.</span></span> |
| <span data-ttu-id="7795e-156">tutti</span><span class="sxs-lookup"><span data-stu-id="7795e-156">all</span></span> | <span data-ttu-id="7795e-157">Tutti i valori precedenti (ad eccezione di `none`)</span><span class="sxs-lookup"><span data-stu-id="7795e-157">All of the above (except `none`)</span></span> |

<span data-ttu-id="7795e-158">Nell'esempio seguente, il progetto utilizzerà tutti gli elementi tranne i file di contenuto dal pacchetto e tutti gli elementi, tranne gli analizzatori e i file di contenuto, verranno trasferiti al progetto padre.</span><span class="sxs-lookup"><span data-stu-id="7795e-158">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="7795e-159">Si noti che dato che `build` non è incluso in `PrivateAssets`, le destinazioni e le proprietà *verranno trasferite* al progetto padre.</span><span class="sxs-lookup"><span data-stu-id="7795e-159">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="7795e-160">Si consideri, ad esempio, che il riferimento precedente viene usato in un progetto che compila un pacchetto NuGet chiamato AppLogger.</span><span class="sxs-lookup"><span data-stu-id="7795e-160">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="7795e-161">AppLogger può utilizzare le destinazioni e le proprietà da `Contoso.Utility.UsefulStuff`, analogamente ai progetti che utilizzano AppLogger.</span><span class="sxs-lookup"><span data-stu-id="7795e-161">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="7795e-162">Aggiunta di una condizione PackageReference</span><span class="sxs-lookup"><span data-stu-id="7795e-162">Adding a PackageReference condition</span></span>

<span data-ttu-id="7795e-163">È possibile usare una condizione per controllare se un pacchetto è incluso e le condizioni possono usare qualsiasi variabile di MSBuild o una variabile definita nel file delle destinazioni o delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="7795e-163">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="7795e-164">Tuttavia, attualmente è supportata solo la variabile `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="7795e-164">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="7795e-165">Ad esempio, si supponga di usare `netstandard1.4` e `net452` come destinazione, ma di avere una dipendenza applicabile solo per `net452`.</span><span class="sxs-lookup"><span data-stu-id="7795e-165">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="7795e-166">In questo caso non si vuole che un progetto `netstandard1.4` che utilizza il pacchetto aggiunta tale dipendenza non necessaria.</span><span class="sxs-lookup"><span data-stu-id="7795e-166">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="7795e-167">Per evitarlo, è possibile specificare una condizione in `PackageReference` come segue:</span><span class="sxs-lookup"><span data-stu-id="7795e-167">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="7795e-168">Un pacchetto compilato con questo progetto indica che Newtonsoft.Json è incluso come dipendenza solo per una destinazione `net452`:</span><span class="sxs-lookup"><span data-stu-id="7795e-168">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Risultato dell'applicazione di una condizione per PackageReference con VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="7795e-170">Le condizioni possono essere applicate anche al livello `ItemGroup` e verranno applicate a tutti gli elementi `PackageReference` figlio:</span><span class="sxs-lookup"><span data-stu-id="7795e-170">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
