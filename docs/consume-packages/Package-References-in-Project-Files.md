---
title: Formato PackageReference NuGet (riferimenti a pacchetti nei file di progetto)
description: Informazioni dettagliate su PackageReference NuGet nei file di progetto, come supportato da NuGet 4.0 +, Visual Studio 2017 e .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 71ab5bb464d1513df89ab53e119d9768e880e4e5
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981028"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="db7c5-103">Riferimenti a pacchetti (PackageReference) nei file di progetto</span><span class="sxs-lookup"><span data-stu-id="db7c5-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="db7c5-104">I riferimenti ai pacchetti, tramite il nodo `PackageReference`, consentono di gestire le dipendenze di NuGet direttamente all'interno di file di progetto, invece di dover ricorrere a un file `packages.config` separato.</span><span class="sxs-lookup"><span data-stu-id="db7c5-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="db7c5-105">L'uso di PackageReference non influenza altri aspetti di NuGet. Ad esempio le impostazioni nei file \`NuGet.</span><span class="sxs-lookup"><span data-stu-id="db7c5-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in \`NuGet.</span></span>





<span data-ttu-id="db7c5-106">fig\` (incluse le origini dei pacchetti) vengono comunque applicate come illustrato in [Configurazione del comportamento di NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="db7c5-106">fig\` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="db7c5-107">Con PackageReference è anche possibile usare condizioni MSBuild per scegliere i riferimenti ai pacchetti in base a framework di destinazione, configurazione, piattaforma o altri raggruppamenti.</span><span class="sxs-lookup"><span data-stu-id="db7c5-107">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="db7c5-108">Consente anche un controllo più capillare delle dipendenze e del flusso del contenuto.</span><span class="sxs-lookup"><span data-stu-id="db7c5-108">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="db7c5-109">(Per altri dettagli, vedere [Pack e restore di NuGet come destinazioni MSBuild ](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="db7c5-109">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="db7c5-110">Per impostazione predefinita, PackageReference viene usato per i progetti .NET Core, i progetti .NET Standard e i progetti UWP destinati a Windows 10 Build 15063 (Creators Update) e versioni successive, con l'eccezione dei progetti UWP C++.</span><span class="sxs-lookup"><span data-stu-id="db7c5-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="db7c5-111">I progetti .NET Framework supportano PackageReference, ma usano attualmente `packages.config` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="db7c5-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="db7c5-112">Per usare PackageReference, eseguire la migrazione delle dipendenze da `packages.config` nel file di progetto e quindi rimuovere packages.config.</span><span class="sxs-lookup"><span data-stu-id="db7c5-112">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="db7c5-113">Aggiunta di PackageReference</span><span class="sxs-lookup"><span data-stu-id="db7c5-113">Adding a PackageReference</span></span>

<span data-ttu-id="db7c5-114">Aggiungere una dipendenza nel file di progetto usando la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="db7c5-114">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="db7c5-115">Controllo della versione della dipendenza</span><span class="sxs-lookup"><span data-stu-id="db7c5-115">Controlling dependency version</span></span>

<span data-ttu-id="db7c5-116">La convenzione per specificare la versione di un pacchetto è uguale quando si usa `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="db7c5-116">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="db7c5-117">Nell'esempio precedente, 3.6.0 significa qualsiasi versione > = 3.6.0 con preferenza per la versione più bassa, come descritto in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="db7c5-117">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="db7c5-118">Uso di PackageReference per un progetto senza PackageReference</span><span class="sxs-lookup"><span data-stu-id="db7c5-118">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="db7c5-119">Avanzato: se non si hanno pacchetti installati in un progetto (nessun PackageReference nel file di progetto e nessun file packages.config), ma si vuole ripristinare il progetto con stile PackageReference, è possibile impostare una proprietà del progetto RestoreProjectStyle su PackageReference nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="db7c5-119">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="db7c5-120">Questa opzione può essere utile se si fa riferimento a progetti con stile PackageReference (progetti con stile SDK o csproj esistenti).</span><span class="sxs-lookup"><span data-stu-id="db7c5-120">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="db7c5-121">In questo modo, sarà possibile fare riferimento "in modo transitivo" dal progetto ai pacchetti a cui fanno riferimento tali progetti.</span><span class="sxs-lookup"><span data-stu-id="db7c5-121">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="db7c5-122">Versioni mobili</span><span class="sxs-lookup"><span data-stu-id="db7c5-122">Floating Versions</span></span>

<span data-ttu-id="db7c5-123">Le [versioni mobili](../consume-packages/dependency-resolution.md#floating-versions) sono supportate con `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="db7c5-123">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="db7c5-124">Controllo degli asset delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="db7c5-124">Controlling dependency assets</span></span>

<span data-ttu-id="db7c5-125">È possibile che si usi una dipendenza esclusivamente come strumento di sviluppo e che non si voglia esporla nei progetti che utilizzano il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="db7c5-125">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="db7c5-126">In questo scenario, è possibile usare i metadati `PrivateAssets` per controllare questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="db7c5-126">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="db7c5-127">I tag di metadati seguenti controllano gli asset delle dipendenze:</span><span class="sxs-lookup"><span data-stu-id="db7c5-127">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="db7c5-128">Tag</span><span class="sxs-lookup"><span data-stu-id="db7c5-128">Tag</span></span> | <span data-ttu-id="db7c5-129">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db7c5-129">Description</span></span> | <span data-ttu-id="db7c5-130">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="db7c5-130">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="db7c5-131">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="db7c5-131">IncludeAssets</span></span> | <span data-ttu-id="db7c5-132">Questi asset verranno utilizzati</span><span class="sxs-lookup"><span data-stu-id="db7c5-132">These assets will be consumed</span></span> | <span data-ttu-id="db7c5-133">tutti</span><span class="sxs-lookup"><span data-stu-id="db7c5-133">all</span></span> |
| <span data-ttu-id="db7c5-134">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="db7c5-134">ExcludeAssets</span></span> | <span data-ttu-id="db7c5-135">Questi asset non verranno utilizzati</span><span class="sxs-lookup"><span data-stu-id="db7c5-135">These assets will not be consumed</span></span> | <span data-ttu-id="db7c5-136">none</span><span class="sxs-lookup"><span data-stu-id="db7c5-136">none</span></span> |
| <span data-ttu-id="db7c5-137">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="db7c5-137">PrivateAssets</span></span> | <span data-ttu-id="db7c5-138">Questi asset verranno utilizzati, ma non verranno trasferiti al progetto padre</span><span class="sxs-lookup"><span data-stu-id="db7c5-138">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="db7c5-139">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="db7c5-139">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="db7c5-140">I valori consentiti per questi tag sono i seguenti, con più valori separati da un punto e virgola, ad eccezione di `all` e `none` che devono essere usati da soli:</span><span class="sxs-lookup"><span data-stu-id="db7c5-140">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="db7c5-141">Valore</span><span class="sxs-lookup"><span data-stu-id="db7c5-141">Value</span></span> | <span data-ttu-id="db7c5-142">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db7c5-142">Description</span></span> |
| --- | ---
| <span data-ttu-id="db7c5-143">compile</span><span class="sxs-lookup"><span data-stu-id="db7c5-143">compile</span></span> | <span data-ttu-id="db7c5-144">Contenuti della cartella `lib`. Controlla se il progetto può essere compilato in base agli assembly nella cartella</span><span class="sxs-lookup"><span data-stu-id="db7c5-144">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="db7c5-145">runtime</span><span class="sxs-lookup"><span data-stu-id="db7c5-145">runtime</span></span> | <span data-ttu-id="db7c5-146">Contenuti delle cartelle `lib` e `runtimes`. Controlla se questi assembly verranno copiati nella directory di output build</span><span class="sxs-lookup"><span data-stu-id="db7c5-146">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="db7c5-147">contentFiles</span><span class="sxs-lookup"><span data-stu-id="db7c5-147">contentFiles</span></span> | <span data-ttu-id="db7c5-148">Contenuto della cartella `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="db7c5-148">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="db7c5-149">build</span><span class="sxs-lookup"><span data-stu-id="db7c5-149">build</span></span> | <span data-ttu-id="db7c5-150">Proprietà e destinazioni nella cartella `build`</span><span class="sxs-lookup"><span data-stu-id="db7c5-150">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="db7c5-151">analyzers</span><span class="sxs-lookup"><span data-stu-id="db7c5-151">analyzers</span></span> | <span data-ttu-id="db7c5-152">Analizzatori .NET</span><span class="sxs-lookup"><span data-stu-id="db7c5-152">.NET analyzers</span></span> |
| <span data-ttu-id="db7c5-153">native</span><span class="sxs-lookup"><span data-stu-id="db7c5-153">native</span></span> | <span data-ttu-id="db7c5-154">Contenuto della cartella `native`</span><span class="sxs-lookup"><span data-stu-id="db7c5-154">Contents of the `native` folder</span></span> |
| <span data-ttu-id="db7c5-155">none</span><span class="sxs-lookup"><span data-stu-id="db7c5-155">none</span></span> | <span data-ttu-id="db7c5-156">Non viene usato alcuno dei valori precedenti.</span><span class="sxs-lookup"><span data-stu-id="db7c5-156">None of the above are used.</span></span> |
| <span data-ttu-id="db7c5-157">tutti</span><span class="sxs-lookup"><span data-stu-id="db7c5-157">all</span></span> | <span data-ttu-id="db7c5-158">Tutti i valori precedenti (ad eccezione di `none`)</span><span class="sxs-lookup"><span data-stu-id="db7c5-158">All of the above (except `none`)</span></span> |

<span data-ttu-id="db7c5-159">Nell'esempio seguente, il progetto utilizzerà tutti gli elementi tranne i file di contenuto dal pacchetto e tutti gli elementi, tranne gli analizzatori e i file di contenuto, verranno trasferiti al progetto padre.</span><span class="sxs-lookup"><span data-stu-id="db7c5-159">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="db7c5-160">Si noti che dato che `build` non è incluso in `PrivateAssets`, le destinazioni e le proprietà *verranno trasferite* al progetto padre.</span><span class="sxs-lookup"><span data-stu-id="db7c5-160">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="db7c5-161">Si consideri, ad esempio, che il riferimento precedente viene usato in un progetto che compila un pacchetto NuGet chiamato AppLogger.</span><span class="sxs-lookup"><span data-stu-id="db7c5-161">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="db7c5-162">AppLogger può utilizzare le destinazioni e le proprietà da `Contoso.Utility.UsefulStuff`, analogamente ai progetti che utilizzano AppLogger.</span><span class="sxs-lookup"><span data-stu-id="db7c5-162">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="db7c5-163">Aggiunta di una condizione PackageReference</span><span class="sxs-lookup"><span data-stu-id="db7c5-163">Adding a PackageReference condition</span></span>

<span data-ttu-id="db7c5-164">È possibile usare una condizione per controllare se un pacchetto è incluso e le condizioni possono usare qualsiasi variabile di MSBuild o una variabile definita nel file delle destinazioni o delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="db7c5-164">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="db7c5-165">Tuttavia, attualmente è supportata solo la variabile `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="db7c5-165">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="db7c5-166">Ad esempio, si supponga di usare `netstandard1.4` e `net452` come destinazione, ma di avere una dipendenza applicabile solo per `net452`.</span><span class="sxs-lookup"><span data-stu-id="db7c5-166">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="db7c5-167">In questo caso non si vuole che un progetto `netstandard1.4` che utilizza il pacchetto aggiunta tale dipendenza non necessaria.</span><span class="sxs-lookup"><span data-stu-id="db7c5-167">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="db7c5-168">Per evitarlo, è possibile specificare una condizione in `PackageReference` come segue:</span><span class="sxs-lookup"><span data-stu-id="db7c5-168">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="db7c5-169">Un pacchetto compilato con questo progetto indica che Newtonsoft.Json è incluso come dipendenza solo per una destinazione `net452`:</span><span class="sxs-lookup"><span data-stu-id="db7c5-169">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Risultato dell'applicazione di una condizione per PackageReference con VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="db7c5-171">Le condizioni possono essere applicate anche al livello `ItemGroup` e verranno applicate a tutti gli elementi `PackageReference` figlio:</span><span class="sxs-lookup"><span data-stu-id="db7c5-171">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="db7c5-172">Blocco delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="db7c5-172">Locking dependencies</span></span>
<span data-ttu-id="db7c5-173">*Questa funzionalità è disponibile con NuGet **4.9** o versione successiva e con Visual Studio 2017 **15.9 Preview 5** o versione successiva.*</span><span class="sxs-lookup"><span data-stu-id="db7c5-173">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9 Preview 5** or above.*</span></span>

<span data-ttu-id="db7c5-174">L'input per il ripristino NuGet è un set di riferimenti al pacchetto dal file di progetto (dipendenze dirette o di primo livello) e l'output è una chiusura completa di tutte le dipendenze del pacchetto, incluse le dipendenze transitive.</span><span class="sxs-lookup"><span data-stu-id="db7c5-174">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependenices) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="db7c5-175">NuGet prova a produrre sempre la stessa chiusura completa di dipendenze del pacchetto se l'elenco PackageReference di input non è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="db7c5-175">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="db7c5-176">Esistono tuttavia alcuni scenari in cui non è possibile farlo.</span><span class="sxs-lookup"><span data-stu-id="db7c5-176">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="db7c5-177">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="db7c5-177">For example:</span></span>

* <span data-ttu-id="db7c5-178">Quando si usano versioni mobili, ad esempio `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="db7c5-178">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="db7c5-179">Anche se in questo caso la finalità è il passaggio alla versione più recente a ogni ripristino dei pacchetti, esistono scenari in cui gli utenti richiedono che il grafo venga bloccato su una determinata versione più recente e passi a una versione successiva, se disponibile, in caso di movimento esplicito.</span><span class="sxs-lookup"><span data-stu-id="db7c5-179">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="db7c5-180">Viene pubblicata una versione più recente del pacchetto che risponde ai requisiti di versione di PackageReference.</span><span class="sxs-lookup"><span data-stu-id="db7c5-180">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="db7c5-181">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="db7c5-181">E.g.</span></span> 

  * <span data-ttu-id="db7c5-182">Giorno 1: si è specificato `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, ma le versioni disponibili nei repository NuGet erano 4.1.0, 4.2.0 e 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="db7c5-182">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="db7c5-183">In questo caso, NuGet restituirebbe 4.1.0 (la versione minima più vicina)</span><span class="sxs-lookup"><span data-stu-id="db7c5-183">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="db7c5-184">Giorno 2: viene pubblicata la versione 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="db7c5-184">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="db7c5-185">NuGet troverà ora la corrispondenza esatta e inizierà a restituire 4.0.0</span><span class="sxs-lookup"><span data-stu-id="db7c5-185">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="db7c5-186">Una versione del pacchetto specifica viene rimossa dal repository.</span><span class="sxs-lookup"><span data-stu-id="db7c5-186">A given package version is removed from the repository.</span></span> <span data-ttu-id="db7c5-187">Anche se nuget.org non consente l'eliminazione dei pacchetti, non tutti i repository di pacchetti presentano questo vincolo.</span><span class="sxs-lookup"><span data-stu-id="db7c5-187">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="db7c5-188">NuGet trova di conseguenza la corrispondenza migliore quando non può restituire la versione eliminata.</span><span class="sxs-lookup"><span data-stu-id="db7c5-188">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="db7c5-189">Abilitazione del file di blocco</span><span class="sxs-lookup"><span data-stu-id="db7c5-189">Enabling lock file</span></span>
<span data-ttu-id="db7c5-190">Per rendere persistente la chiusura completa delle dipendenze del pacchetto, è possibile acconsentire esplicitamente alla funzionalità di file di blocco impostando la proprietà MSBuild `RestorePackagesWithLockFile` per il progetto:</span><span class="sxs-lookup"><span data-stu-id="db7c5-190">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="db7c5-191">Se questa proprietà viene impostata, il ripristino NuGet genererà un file di blocco, il file `packages.lock.json`, nella directory radice del progetto, che elenca tutte le dipendenze del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="db7c5-191">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="db7c5-192">Quando nella directory radice di un progetto è presente il file `packages.lock.json`, il file di blocco viene sempre usato con il ripristino anche se la proprietà `RestorePackagesWithLockFile` non è impostata.</span><span class="sxs-lookup"><span data-stu-id="db7c5-192">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="db7c5-193">Un altro modo per acconsentire esplicitamente a questa funzionalità è quindi quello di creare un file `packages.lock.json` fittizio vuoto nella directory radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="db7c5-193">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="db7c5-194">Comportamento di `restore` con il file di blocco</span><span class="sxs-lookup"><span data-stu-id="db7c5-194">`restore` behavior with lock file</span></span>
<span data-ttu-id="db7c5-195">Se un file di blocco è presente per il progetto, NuGet lo usa per eseguire `restore`.</span><span class="sxs-lookup"><span data-stu-id="db7c5-195">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="db7c5-196">NuGet esegue un rapido controllo per verificare se sono state apportate modifiche alle dipendenze del pacchetto indicate nel file di progetto (o nei file dei progetti dipendenti) e, se non sono presenti modifiche, si limita a ripristinare i pacchetti indicati nel file di blocco.</span><span class="sxs-lookup"><span data-stu-id="db7c5-196">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="db7c5-197">Non viene eseguita alcuna rivalutazione delle dipendenze del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="db7c5-197">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="db7c5-198">Se NuGet rileva una modifica nelle dipendenze definite indicate nei file di progetto, rivaluta il grafo del pacchetto e aggiorna il file di blocco in modo da riflettere la nuova chiusura del pacchetto per il progetto.</span><span class="sxs-lookup"><span data-stu-id="db7c5-198">If NuGet detects a change in the defined dependenices as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="db7c5-199">Per CI/CD e altri scenari in cui non si vogliono modificare le dipendenze del pacchetto immediatamente, è possibile farlo impostando `lockedmode` su `true`:</span><span class="sxs-lookup"><span data-stu-id="db7c5-199">For CI/CD and other scenarios, where you would not want to change the package dependenies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="db7c5-200">Per dotnet.exe, eseguire:</span><span class="sxs-lookup"><span data-stu-id="db7c5-200">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="db7c5-201">Per msbuild.exe, eseguire:</span><span class="sxs-lookup"><span data-stu-id="db7c5-201">For msbuild.exe, run:</span></span>
```
> msbuild.exe /t:restore /p:RestoreLockedMode=true
```

<span data-ttu-id="db7c5-202">È anche possibile impostare questa proprietà MSBuild condizionale nel file di progetto:</span><span class="sxs-lookup"><span data-stu-id="db7c5-202">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="db7c5-203">Se la modalità di blocco è `true`, verranno ripristinati i pacchetti esatti elencati nel file di blocco. Il ripristino avrà invece esito negativo se le dipendenze del pacchetto definite per il progetto sono state aggiornate dopo la creazione del file di blocco.</span><span class="sxs-lookup"><span data-stu-id="db7c5-203">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="db7c5-204">Rendere il file di blocco parte del repository di origine</span><span class="sxs-lookup"><span data-stu-id="db7c5-204">Make lock file part of your source repository</span></span>
<span data-ttu-id="db7c5-205">Se si compila un'applicazione, un file eseguibile e il progetto in questione sono alla fine della catena di dipendenze, quindi archiviare il file di blocco nel repository di codice sorgente in modo che NuGet possa usarlo durante il ripristino.</span><span class="sxs-lookup"><span data-stu-id="db7c5-205">If you are building an application, an executable and the project in question is at the end of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="db7c5-206">Se tuttavia il progetto è un progetto libreria che non viene distribuito o un progetto di codice comune da cui dipendono altri progetti, **non è consigliabile** archiviare il file di blocco come parte del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="db7c5-206">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="db7c5-207">È possibile mantenere il file di blocco, ma le dipendenze del pacchetto bloccato per il progetto di codice comune, elencate nel file di blocco, non possono essere usate durante il ripristino o la compilazione di un progetto che dipende da questo progetto di codice comune.</span><span class="sxs-lookup"><span data-stu-id="db7c5-207">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="db7c5-208">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="db7c5-208">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="db7c5-209">Se `ProjectA` ha una dipendenza da `PackageX` versione `2.0.0` e fa anche riferimento a `ProjectB` che dipende da `PackageX` versione `1.0.0`, il file di blocco per `ProjectB` elencherà una dipendenza da `PackageX` versione `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="db7c5-209">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="db7c5-210">Quando tuttavia `ProjectA` viene compilato, il file di blocco conterrà una dipendenza da `PackageX` versione **`2.0.0`** e **non** `1.0.0` come elencato nel file di blocco per `ProjectB`.</span><span class="sxs-lookup"><span data-stu-id="db7c5-210">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="db7c5-211">Di conseguenza, il file di blocco di un progetto di codice comune ha poca influenza sui pacchetti risolti per i progetti che dipendono da esso.</span><span class="sxs-lookup"><span data-stu-id="db7c5-211">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="db7c5-212">Estendibilità di file di blocco</span><span class="sxs-lookup"><span data-stu-id="db7c5-212">Lock file extensibility</span></span>
<span data-ttu-id="db7c5-213">È possibile controllare diversi comportamenti di ripristino con file di blocco, come descritto di seguito:</span><span class="sxs-lookup"><span data-stu-id="db7c5-213">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="db7c5-214">Opzione</span><span class="sxs-lookup"><span data-stu-id="db7c5-214">Option</span></span> | <span data-ttu-id="db7c5-215">Opzione MSBuild equivalente</span><span class="sxs-lookup"><span data-stu-id="db7c5-215">MSBuild equivalent option</span></span> | 
|:---  |:--- |
| `--use-lock-file` | <span data-ttu-id="db7c5-216">Avvia l'uso del file di blocco per un progetto.</span><span class="sxs-lookup"><span data-stu-id="db7c5-216">Bootstraps use of lock file for a project.</span></span> <span data-ttu-id="db7c5-217">In alternativa, è possibile impostare la proprietà `RestorePackagesWithLockFile` nel file di progetto</span><span class="sxs-lookup"><span data-stu-id="db7c5-217">You can alternatively set `RestorePackagesWithLockFile` property in the project file</span></span> | 
| `--locked-mode` | <span data-ttu-id="db7c5-218">Abilita la modalità di blocco per il ripristino.</span><span class="sxs-lookup"><span data-stu-id="db7c5-218">Enables locked mode for restore.</span></span> <span data-ttu-id="db7c5-219">Questa opzione è utile negli scenari di integrazione continua/recapito continuo in cui si vogliono rendere ripetibili le compilazioni.</span><span class="sxs-lookup"><span data-stu-id="db7c5-219">This is useful in CI/CD scenarios where you would like to get the erepeatable builds.</span></span> <span data-ttu-id="db7c5-220">A tal fine, è anche possibile impostare la proprietà MSBuild `RestoreLockedMode` su `true`</span><span class="sxs-lookup"><span data-stu-id="db7c5-220">This can be also by setting the `RestoreLockedMode` MSBuild property to `true`</span></span> |  
| `--force-evaluate` | <span data-ttu-id="db7c5-221">Questa opzione è utile con i pacchetti con la versione mobile definita nel progetto.</span><span class="sxs-lookup"><span data-stu-id="db7c5-221">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="db7c5-222">Per impostazione predefinita, il ripristino NuGet non aggiornerà automaticamente la versione del pacchetto a ogni ripristino, a meno che il ripristino non venga eseguito con l'opzione `--force-evaluate`.</span><span class="sxs-lookup"><span data-stu-id="db7c5-222">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with `--force-evaluate` option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="db7c5-223">Definisce un percorso di file di blocco personalizzato per un progetto.</span><span class="sxs-lookup"><span data-stu-id="db7c5-223">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="db7c5-224">A questo scopo, è anche possibile impostare la proprietà MSBuild `NuGetLockFilePath`.</span><span class="sxs-lookup"><span data-stu-id="db7c5-224">This can be also achieved by setting the MSBuild property `NuGetLockFilePath`.</span></span> <span data-ttu-id="db7c5-225">Per impostazione predefinita, NuGet supporta `packages.lock.json` nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="db7c5-225">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="db7c5-226">Se nella stessa directory sono presenti più progetti, NuGet supporta il file di blocco `packages.<project_name>.lock.json` specifico del progetto</span><span class="sxs-lookup"><span data-stu-id="db7c5-226">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
