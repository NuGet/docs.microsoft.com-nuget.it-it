---
title: Pack e restore di NuGet come destinazioni MSBuild | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: I comandi pack e restore di NuGet possono essere usati direttamente come destinazioni MSBuild con NuGet 4.0 +.
keywords: NuGet e MSBuild, destinazione pack NuGet, destinazione restore NuGet
ms.reviewer:
- karann-msft
ms.openlocfilehash: 6c488f49e12b014e7bd197d57041745387a4d7b4
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="5266f-104">Pack e restore di NuGet come destinazioni MSBuild</span><span class="sxs-lookup"><span data-stu-id="5266f-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="5266f-105">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="5266f-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="5266f-106">Con il formato di PackageReference NuGet 4.0 + possono archiviare i metadati di tutti i manifesti direttamente all'interno di un file di progetto, anziché tramite un apposito `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="5266f-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="5266f-107">Con MSBuild 15.1 +, anche NuGet è un membro di MSBuild di prima classe con le destinazioni `pack` e `restore` come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="5266f-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="5266f-108">Queste destinazioni consentono di usare NuGet come qualsiasi altra attività o destinazione MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5266f-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="5266f-109">Per NuGet 3.x e versioni precedenti, usare invece i comandi [pack](../tools/cli-ref-pack.md) e [restore](../tools/cli-ref-restore.md) tramite l'interfaccia della riga di comando di NuGet.</span><span class="sxs-lookup"><span data-stu-id="5266f-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="5266f-110">Ordine di compilazione delle destinazioni</span><span class="sxs-lookup"><span data-stu-id="5266f-110">Target build order</span></span>

<span data-ttu-id="5266f-111">Dato che `pack` e `restore` sono destinazioni MSBuild, è possibile accedervi per ottimizzare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="5266f-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="5266f-112">Si supponga, ad esempio, di voler copiare il pacchetto in una condivisione di rete dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="5266f-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="5266f-113">È possibile farlo aggiungendo quanto segue nel file di progetto:</span><span class="sxs-lookup"><span data-stu-id="5266f-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="5266f-114">Analogamente, è possibile scrivere un'attività MSBuild, scrivere la propria destinazione e utilizzare proprietà NuGet nell'attività MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5266f-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="5266f-115">Destinazione pack</span><span class="sxs-lookup"><span data-stu-id="5266f-115">pack target</span></span>

<span data-ttu-id="5266f-116">Quando si utilizza la destinazione di Service pack, vale a dire `msbuild /t:pack`, MSBuild crea il relativo input dal file di progetto.</span><span class="sxs-lookup"><span data-stu-id="5266f-116">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the project file.</span></span> <span data-ttu-id="5266f-117">Nella tabella seguente vengono descritte le proprietà di MSBuild che possono essere aggiunto in un file di progetto all'interno della prima `<PropertyGroup>` nodo.</span><span class="sxs-lookup"><span data-stu-id="5266f-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="5266f-118">È possibile apportare facilmente queste modifiche in Visual Studio 2017 e versioni successive facendo clic con il pulsante destro del mouse sul progetto e scegliendo **Modifica {nome_progetto}** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="5266f-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="5266f-119">Per praticità, la tabella è organizzata in base alla proprietà equivalente in un [file `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="5266f-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="5266f-120">Si noti che le proprietà `Owners` e `Summary` da `.nuspec` non sono supportate con MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5266f-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="5266f-121">Valore di attributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="5266f-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="5266f-122">Proprietà MSBuild</span><span class="sxs-lookup"><span data-stu-id="5266f-122">MSBuild Property</span></span> | <span data-ttu-id="5266f-123">Impostazione predefinita</span><span class="sxs-lookup"><span data-stu-id="5266f-123">Default</span></span> | <span data-ttu-id="5266f-124">Note</span><span class="sxs-lookup"><span data-stu-id="5266f-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="5266f-125">Id</span><span class="sxs-lookup"><span data-stu-id="5266f-125">Id</span></span> | <span data-ttu-id="5266f-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="5266f-126">PackageId</span></span> | <span data-ttu-id="5266f-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="5266f-127">AssemblyName</span></span> | <span data-ttu-id="5266f-128">$(AssemblyName) da MSBuild</span><span class="sxs-lookup"><span data-stu-id="5266f-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="5266f-129">Versione</span><span class="sxs-lookup"><span data-stu-id="5266f-129">Version</span></span> | <span data-ttu-id="5266f-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="5266f-130">PackageVersion</span></span> | <span data-ttu-id="5266f-131">Versione</span><span class="sxs-lookup"><span data-stu-id="5266f-131">Version</span></span> | <span data-ttu-id="5266f-132">Compatibile con SemVer, ad esempio "1.0.0", "1.0.0-beta" o "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="5266f-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="5266f-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5266f-133">VersionPrefix</span></span> | <span data-ttu-id="5266f-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5266f-134">PackageVersionPrefix</span></span> | <span data-ttu-id="5266f-135">vuoto</span><span class="sxs-lookup"><span data-stu-id="5266f-135">empty</span></span> | <span data-ttu-id="5266f-136">Impostazione PackageVersion sovrascrive PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5266f-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="5266f-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5266f-137">VersionSuffix</span></span> | <span data-ttu-id="5266f-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5266f-138">PackageVersionSuffix</span></span> | <span data-ttu-id="5266f-139">vuoto</span><span class="sxs-lookup"><span data-stu-id="5266f-139">empty</span></span> | <span data-ttu-id="5266f-140">$(VersionSuffix) da MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5266f-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="5266f-141">Impostazione PackageVersion sovrascrive PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5266f-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="5266f-142">Autori</span><span class="sxs-lookup"><span data-stu-id="5266f-142">Authors</span></span> | <span data-ttu-id="5266f-143">Autori</span><span class="sxs-lookup"><span data-stu-id="5266f-143">Authors</span></span> | <span data-ttu-id="5266f-144">Nome utente dell'utente corrente</span><span class="sxs-lookup"><span data-stu-id="5266f-144">Username of the current user</span></span> | |
| <span data-ttu-id="5266f-145">Proprietari</span><span class="sxs-lookup"><span data-stu-id="5266f-145">Owners</span></span> | <span data-ttu-id="5266f-146">N/D</span><span class="sxs-lookup"><span data-stu-id="5266f-146">N/A</span></span> | <span data-ttu-id="5266f-147">Non presente in NuSpec</span><span class="sxs-lookup"><span data-stu-id="5266f-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="5266f-148">Titolo</span><span class="sxs-lookup"><span data-stu-id="5266f-148">Title</span></span> | <span data-ttu-id="5266f-149">Titolo</span><span class="sxs-lookup"><span data-stu-id="5266f-149">Title</span></span> | <span data-ttu-id="5266f-150">PackageId</span><span class="sxs-lookup"><span data-stu-id="5266f-150">The PackageId</span></span>| |
| <span data-ttu-id="5266f-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5266f-151">Description</span></span> | <span data-ttu-id="5266f-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5266f-152">Description</span></span> | <span data-ttu-id="5266f-153">"Descrizione del pacchetto"</span><span class="sxs-lookup"><span data-stu-id="5266f-153">"Package Description"</span></span> | |
| <span data-ttu-id="5266f-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="5266f-154">Copyright</span></span> | <span data-ttu-id="5266f-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="5266f-155">Copyright</span></span> | <span data-ttu-id="5266f-156">vuoto</span><span class="sxs-lookup"><span data-stu-id="5266f-156">empty</span></span> | |
| <span data-ttu-id="5266f-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5266f-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="5266f-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5266f-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="5266f-159">False</span><span class="sxs-lookup"><span data-stu-id="5266f-159">false</span></span> | |
| <span data-ttu-id="5266f-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5266f-160">LicenseUrl</span></span> | <span data-ttu-id="5266f-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5266f-161">PackageLicenseUrl</span></span> | <span data-ttu-id="5266f-162">vuoto</span><span class="sxs-lookup"><span data-stu-id="5266f-162">empty</span></span> | |
| <span data-ttu-id="5266f-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5266f-163">ProjectUrl</span></span> | <span data-ttu-id="5266f-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5266f-164">PackageProjectUrl</span></span> | <span data-ttu-id="5266f-165">vuoto</span><span class="sxs-lookup"><span data-stu-id="5266f-165">empty</span></span> | |
| <span data-ttu-id="5266f-166">IconUrl</span><span class="sxs-lookup"><span data-stu-id="5266f-166">IconUrl</span></span> | <span data-ttu-id="5266f-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5266f-167">PackageIconUrl</span></span> | <span data-ttu-id="5266f-168">vuoto</span><span class="sxs-lookup"><span data-stu-id="5266f-168">empty</span></span> | |
| <span data-ttu-id="5266f-169">Tag</span><span class="sxs-lookup"><span data-stu-id="5266f-169">Tags</span></span> | <span data-ttu-id="5266f-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="5266f-170">PackageTags</span></span> | <span data-ttu-id="5266f-171">vuoto</span><span class="sxs-lookup"><span data-stu-id="5266f-171">empty</span></span> | <span data-ttu-id="5266f-172">I tag sono delimitati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="5266f-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="5266f-173">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5266f-173">ReleaseNotes</span></span> | <span data-ttu-id="5266f-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5266f-174">PackageReleaseNotes</span></span> | <span data-ttu-id="5266f-175">vuoto</span><span class="sxs-lookup"><span data-stu-id="5266f-175">empty</span></span> | |
| <span data-ttu-id="5266f-176">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="5266f-176">RepositoryUrl</span></span> | <span data-ttu-id="5266f-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="5266f-177">RepositoryUrl</span></span> | <span data-ttu-id="5266f-178">vuoto</span><span class="sxs-lookup"><span data-stu-id="5266f-178">empty</span></span> | |
| <span data-ttu-id="5266f-179">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="5266f-179">RepositoryType</span></span> | <span data-ttu-id="5266f-180">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="5266f-180">RepositoryType</span></span> | <span data-ttu-id="5266f-181">vuoto</span><span class="sxs-lookup"><span data-stu-id="5266f-181">empty</span></span> | |
| <span data-ttu-id="5266f-182">PackageType</span><span class="sxs-lookup"><span data-stu-id="5266f-182">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="5266f-183">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="5266f-183">Summary</span></span> | <span data-ttu-id="5266f-184">Non supportato</span><span class="sxs-lookup"><span data-stu-id="5266f-184">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="5266f-185">Input destinazione pack</span><span class="sxs-lookup"><span data-stu-id="5266f-185">pack target inputs</span></span>

- <span data-ttu-id="5266f-186">IsPackable</span><span class="sxs-lookup"><span data-stu-id="5266f-186">IsPackable</span></span>
- <span data-ttu-id="5266f-187">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="5266f-187">PackageVersion</span></span>
- <span data-ttu-id="5266f-188">PackageId</span><span class="sxs-lookup"><span data-stu-id="5266f-188">PackageId</span></span>
- <span data-ttu-id="5266f-189">Autori</span><span class="sxs-lookup"><span data-stu-id="5266f-189">Authors</span></span>
- <span data-ttu-id="5266f-190">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5266f-190">Description</span></span>
- <span data-ttu-id="5266f-191">Copyright</span><span class="sxs-lookup"><span data-stu-id="5266f-191">Copyright</span></span>
- <span data-ttu-id="5266f-192">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5266f-192">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="5266f-193">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="5266f-193">DevelopmentDependency</span></span>
- <span data-ttu-id="5266f-194">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5266f-194">PackageLicenseUrl</span></span>
- <span data-ttu-id="5266f-195">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5266f-195">PackageProjectUrl</span></span>
- <span data-ttu-id="5266f-196">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5266f-196">PackageIconUrl</span></span>
- <span data-ttu-id="5266f-197">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5266f-197">PackageReleaseNotes</span></span>
- <span data-ttu-id="5266f-198">PackageTags</span><span class="sxs-lookup"><span data-stu-id="5266f-198">PackageTags</span></span>
- <span data-ttu-id="5266f-199">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="5266f-199">PackageOutputPath</span></span>
- <span data-ttu-id="5266f-200">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="5266f-200">IncludeSymbols</span></span>
- <span data-ttu-id="5266f-201">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="5266f-201">IncludeSource</span></span>
- <span data-ttu-id="5266f-202">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="5266f-202">PackageTypes</span></span>
- <span data-ttu-id="5266f-203">IsTool</span><span class="sxs-lookup"><span data-stu-id="5266f-203">IsTool</span></span>
- <span data-ttu-id="5266f-204">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="5266f-204">RepositoryUrl</span></span>
- <span data-ttu-id="5266f-205">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="5266f-205">RepositoryType</span></span>
- <span data-ttu-id="5266f-206">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="5266f-206">NoPackageAnalysis</span></span>
- <span data-ttu-id="5266f-207">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="5266f-207">MinClientVersion</span></span>
- <span data-ttu-id="5266f-208">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="5266f-208">IncludeBuildOutput</span></span>
- <span data-ttu-id="5266f-209">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="5266f-209">IncludeContentInPack</span></span>
- <span data-ttu-id="5266f-210">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="5266f-210">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="5266f-211">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="5266f-211">ContentTargetFolders</span></span>
- <span data-ttu-id="5266f-212">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="5266f-212">NuspecFile</span></span>
- <span data-ttu-id="5266f-213">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="5266f-213">NuspecBasePath</span></span>
- <span data-ttu-id="5266f-214">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="5266f-214">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="5266f-215">Scenari pack</span><span class="sxs-lookup"><span data-stu-id="5266f-215">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="5266f-216">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5266f-216">PackageIconUrl</span></span>

<span data-ttu-id="5266f-217">Come parte della modifica per il [problema NuGet 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` verrà infine modificato in `PackageIconUri` e può essere un percorso relativo a un file di icona che verrà incluso alla radice del pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="5266f-217">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="5266f-218">Assembly di output</span><span class="sxs-lookup"><span data-stu-id="5266f-218">Output assemblies</span></span>

<span data-ttu-id="5266f-219">`nuget pack` copia i file di output con le estensioni `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="5266f-219">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="5266f-220">I file di output copiati dipendono da quanto fornito da MSBuild dalla destinazione `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="5266f-220">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="5266f-221">Sono disponibili due proprietà di MSBuild che è possibile usare nel file di progetto o nella riga di comando per controllare la destinazione degli assembly di output:</span><span class="sxs-lookup"><span data-stu-id="5266f-221">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="5266f-222">`IncludeBuildOutput`: valore booleano che determina se gli assembly di output della compilazione devono essere inclusi nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5266f-222">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="5266f-223">`BuildOutputTargetFolder`: specifica la cartella in cui devono essere posizionati gli assembly di output.</span><span class="sxs-lookup"><span data-stu-id="5266f-223">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="5266f-224">Gli assembly di output (e altri file di output) vengono copiati nelle rispettive cartelle per framework.</span><span class="sxs-lookup"><span data-stu-id="5266f-224">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="5266f-225">Riferimenti ai pacchetti</span><span class="sxs-lookup"><span data-stu-id="5266f-225">Package references</span></span>

<span data-ttu-id="5266f-226">Vedere [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="5266f-226">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="5266f-227">Riferimenti da progetto a progetto</span><span class="sxs-lookup"><span data-stu-id="5266f-227">Project to project references</span></span>

<span data-ttu-id="5266f-228">I riferimenti da progetto a progetto sono considerati per impostazione predefinita come riferimenti a pacchetti NuGet, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="5266f-228">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="5266f-229">È anche possibile aggiungere i metadati seguenti ai riferimenti del progetto:</span><span class="sxs-lookup"><span data-stu-id="5266f-229">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="5266f-230">Inclusione di contenuto in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="5266f-230">Including content in a package</span></span>

<span data-ttu-id="5266f-231">Per includere il contenuto, aggiungere altri metadati all'elemento `<Content>` esistente.</span><span class="sxs-lookup"><span data-stu-id="5266f-231">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="5266f-232">Per impostazione predefinita tutti gli elementi di tipo"Content" vengono inclusi nel pacchetto, a meno che non si esegua l'override con voci simili al codice seguente:</span><span class="sxs-lookup"><span data-stu-id="5266f-232">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="5266f-233">Per impostazione predefinita, tutti gli elementi vengono aggiunti alla radice di `content` e della cartella `contentFiles\any\<target_framework>` all'interno di un pacchetto e viene mantenuta la struttura di cartelle relative, a meno che non si specifichi un percorso di pacchetto:</span><span class="sxs-lookup"><span data-stu-id="5266f-233">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="5266f-234">Se si vuole copiare tutto il contenuto sono in cartelle radice specifiche (invece di copiarlo sia in `content` che in `contentFiles`), è possibile usare la proprietà di MSBuild `ContentTargetFolders`, che ha il valore predefinito "content;contentFiles" ma può essere impostata su qualsiasi altro nome di cartella.</span><span class="sxs-lookup"><span data-stu-id="5266f-234">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="5266f-235">Si noti che se si specifica solo "contentFiles" in `ContentTargetFolders`, i file vengono posizionati in `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` in base a `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="5266f-235">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="5266f-236">`PackagePath` può essere un set di percorsi di destinazione delimitati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="5266f-236">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="5266f-237">Se si specifica un percorso di pacchetto vuoto, il file viene aggiunto alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5266f-237">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="5266f-238">Ad esempio, il codice seguente aggiunge `libuv.txt` a `content\myfiles`, `content\samples` e nella radice del pacchetto:</span><span class="sxs-lookup"><span data-stu-id="5266f-238">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="5266f-239">È disponibile anche una proprietà di MSBuild `$(IncludeContentInPack)`, con valore predefinito `true`.</span><span class="sxs-lookup"><span data-stu-id="5266f-239">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="5266f-240">Se questa proprietà viene impostata su `false` in qualsiasi progetto, il contenuto da tale progetto non viene incluso nel pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="5266f-240">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="5266f-241">Altri metadati specifici di pack che è possibile impostare per qualsiasi elemento precedente includono ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, che impostano i valori ```CopyToOutput``` e ```Flatten``` sulla voce ```contentFiles``` nel file nuspec di output.</span><span class="sxs-lookup"><span data-stu-id="5266f-241">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="5266f-242">Oltre a elementi di contenuto, il `<Pack>` e `<PackagePath>` metadati possono essere impostati anche nel file con un'azione di compilazione di compilazione, EmbeddedResource, ApplicationDefinition, pagina, risorse, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o nessuno.</span><span class="sxs-lookup"><span data-stu-id="5266f-242">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="5266f-243">Per fare in modo che il comando pack aggiunga il nome del file al percorso del pacchetto quando si usano modelli con caratteri jolly (glob), il percorso del pacchetto deve terminare con il carattere separatore di cartella. In caso contrario, il percorso del pacchetto viene interpretato come percorso completo, incluso il nome del file.</span><span class="sxs-lookup"><span data-stu-id="5266f-243">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="5266f-244">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="5266f-244">IncludeSymbols</span></span>

<span data-ttu-id="5266f-245">Quando si usa `MSBuild /t:pack /p:IncludeSymbols=true`, i file `.pdb` corrispondenti vengono copiati insieme agli altri file di output (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="5266f-245">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="5266f-246">Si noti che l'impostazione `IncludeSymbols=true` crea un pacchetto regolare *e* un pacchetto di simboli.</span><span class="sxs-lookup"><span data-stu-id="5266f-246">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="5266f-247">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="5266f-247">IncludeSource</span></span>

<span data-ttu-id="5266f-248">Equivale a `IncludeSymbols`, ma insieme ai file `.pdb` vengono copiati anche i file di origine.</span><span class="sxs-lookup"><span data-stu-id="5266f-248">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="5266f-249">Tutti i file di tipo `Compile` vengono copiati in `src\<ProjectName>\` conservando la struttura di cartelle del percorso relativo nel pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="5266f-249">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="5266f-250">Lo stesso accade anche per i file di origine di qualsiasi `ProjectReference` con `TreatAsPackageReference` impostato su `false`.</span><span class="sxs-lookup"><span data-stu-id="5266f-250">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="5266f-251">Se un file di tipo Compile è all'esterno della cartella di progetto, viene semplicemente aggiunto a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="5266f-251">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="5266f-252">IsTool</span><span class="sxs-lookup"><span data-stu-id="5266f-252">IsTool</span></span>

<span data-ttu-id="5266f-253">Quando si usa `MSBuild /t:pack /p:IsTool=true`, tutti i file, come specificato nello scenario [Assembly di output](#output-assemblies), vengono copiati nella cartella `tools` invece che nella cartella `lib`.</span><span class="sxs-lookup"><span data-stu-id="5266f-253">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="5266f-254">Si noti che questo comportamento è diverso da `DotNetCliTool`, che viene specificato impostando `PackageType` nel file `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="5266f-254">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="5266f-255">Creazione di un pacchetto con un file .nuspec</span><span class="sxs-lookup"><span data-stu-id="5266f-255">Packing using a .nuspec</span></span>

<span data-ttu-id="5266f-256">È possibile usare un file `.nuspec` per creare un pacchetto del progetto, a condizione di disporre di un file di progetto per importare `NuGet.Build.Tasks.Pack.targets`, in modo da poter eseguire l'attività pack.</span><span class="sxs-lookup"><span data-stu-id="5266f-256">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="5266f-257">Le tre proprietà di MSBuild seguenti sono rilevanti per la creazione di pacchetti con un file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="5266f-257">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="5266f-258">`NuspecFile`: percorso relativo o assoluto per il file `.nuspec` usato per la creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5266f-258">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="5266f-259">`NuspecProperties`: elenco con valori delimitati da punto e virgola di coppie chiave=valore.</span><span class="sxs-lookup"><span data-stu-id="5266f-259">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="5266f-260">A causa della modalità di funzionamento dell'analisi della riga di comando di MSBuild, è necessario specificare più proprietà come indicato di seguito: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="5266f-260">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="5266f-261">`NuspecBasePath`: percorso di base per il file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="5266f-261">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="5266f-262">Se si usa `dotnet.exe` per creare il pacchetto del progetto, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="5266f-262">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="5266f-263">Se si usa MSBuild per creare il pacchetto del progetto, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="5266f-263">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="5266f-264">Destinazione restore</span><span class="sxs-lookup"><span data-stu-id="5266f-264">restore target</span></span>

<span data-ttu-id="5266f-265">`MSBuild /t:restore` (usato da `nuget restore` e `dotnet restore` con progetti .NET Core) consente di ripristinare i pacchetti a cui si fa riferimento nel file di progetto, come segue:</span><span class="sxs-lookup"><span data-stu-id="5266f-265">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="5266f-266">Lettura di tutti i riferimenti da progetto a progetto</span><span class="sxs-lookup"><span data-stu-id="5266f-266">Read all project to project references</span></span>
1. <span data-ttu-id="5266f-267">Lettura delle proprietà del progetto per trovare la cartella intermedia e i framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="5266f-267">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="5266f-268">Passaggio dei dati msbuild a NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="5266f-268">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="5266f-269">Esecuzione di restore</span><span class="sxs-lookup"><span data-stu-id="5266f-269">Run restore</span></span>
1. <span data-ttu-id="5266f-270">Download dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="5266f-270">Download packages</span></span>
1. <span data-ttu-id="5266f-271">Scrittura dei file di asset, delle destinazioni e delle proprietà</span><span class="sxs-lookup"><span data-stu-id="5266f-271">Write assets file, targets, and props</span></span>

### <a name="restore-properties"></a><span data-ttu-id="5266f-272">Ripristino delle proprietà</span><span class="sxs-lookup"><span data-stu-id="5266f-272">Restore properties</span></span>

<span data-ttu-id="5266f-273">Possono esistere ulteriori impostazioni di ripristino derivate da proprietà di MSBuild nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="5266f-273">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="5266f-274">I valori possono essere impostati anche dalla riga di comando tramite l'opzione `/p:` (vedere gli esempi riportati di seguito).</span><span class="sxs-lookup"><span data-stu-id="5266f-274">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="5266f-275">Proprietà</span><span class="sxs-lookup"><span data-stu-id="5266f-275">Property</span></span> | <span data-ttu-id="5266f-276">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5266f-276">Description</span></span> |
|--------|--------|
| <span data-ttu-id="5266f-277">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="5266f-277">RestoreSources</span></span> | <span data-ttu-id="5266f-278">Elenco delimitato da punto e virgola delle origini di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5266f-278">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="5266f-279">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="5266f-279">RestorePackagesPath</span></span> | <span data-ttu-id="5266f-280">Percorso della cartella dei pacchetti dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5266f-280">User packages folder path.</span></span> |
| <span data-ttu-id="5266f-281">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="5266f-281">RestoreDisableParallel</span></span> | <span data-ttu-id="5266f-282">Consente di limitare i download a uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="5266f-282">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="5266f-283">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="5266f-283">RestoreConfigFile</span></span> | <span data-ttu-id="5266f-284">Percorso per un file `Nuget.Config` da applicare.</span><span class="sxs-lookup"><span data-stu-id="5266f-284">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="5266f-285">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="5266f-285">RestoreNoCache</span></span> | <span data-ttu-id="5266f-286">Se true, consente di evitare l'uso della cache Web.</span><span class="sxs-lookup"><span data-stu-id="5266f-286">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="5266f-287">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="5266f-287">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="5266f-288">Se true, ignora le origini di pacchetti in errore o mancanti.</span><span class="sxs-lookup"><span data-stu-id="5266f-288">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="5266f-289">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="5266f-289">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="5266f-290">Percorso di `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="5266f-290">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="5266f-291">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="5266f-291">RestoreGraphProjectInput</span></span> | <span data-ttu-id="5266f-292">Elenco delimitato da punto e virgola dei progetti da ripristinare, che deve contenere percorsi assoluti.</span><span class="sxs-lookup"><span data-stu-id="5266f-292">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="5266f-293">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="5266f-293">RestoreOutputPath</span></span> | <span data-ttu-id="5266f-294">Cartella di output. Per impostazione predefinita, la cartella `obj`.</span><span class="sxs-lookup"><span data-stu-id="5266f-294">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="5266f-295">Esempi</span><span class="sxs-lookup"><span data-stu-id="5266f-295">Examples</span></span>

<span data-ttu-id="5266f-296">Riga di comando:</span><span class="sxs-lookup"><span data-stu-id="5266f-296">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="5266f-297">File di progetto:</span><span class="sxs-lookup"><span data-stu-id="5266f-297">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="5266f-298">Output del ripristino</span><span class="sxs-lookup"><span data-stu-id="5266f-298">Restore outputs</span></span>

<span data-ttu-id="5266f-299">Il ripristino crea i file seguenti nella cartella `obj` di compilazione:</span><span class="sxs-lookup"><span data-stu-id="5266f-299">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="5266f-300">File</span><span class="sxs-lookup"><span data-stu-id="5266f-300">File</span></span> | <span data-ttu-id="5266f-301">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5266f-301">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="5266f-302">In precedenza `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="5266f-302">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="5266f-303">Riferimenti alle proprietà di MSBuild contenute nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="5266f-303">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="5266f-304">Riferimenti alle destinazioni di MSBuild contenute nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="5266f-304">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="5266f-305">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="5266f-305">PackageTargetFallback</span></span>

<span data-ttu-id="5266f-306">L'elemento `PackageTargetFallback` consente di specificare un set di destinazioni compatibili da usare durante il ripristino di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5266f-306">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="5266f-307">È progettato per consentire ai pacchetti che usano un [TxM](../reference/target-frameworks.md) dotnet di interagire con pacchetti compatibili che non dichiarano un TxM dotnet.</span><span class="sxs-lookup"><span data-stu-id="5266f-307">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="5266f-308">Se il progetto usa il TxM dotnet, devono averlo anche tutti i pacchetti da cui il progetto dipende, a meno che non si aggiunga `<PackageTargetFallback>` al progetto, in modo da rendere compatibili con dotnet le piattaforme che non lo sono.</span><span class="sxs-lookup"><span data-stu-id="5266f-308">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="5266f-309">Ad esempio, se il progetto usa il TxM `netstandard1.6` e un pacchetto dipendente contiene solo `lib/net45/a.dll` e `lib/portable-net45+win81/a.dll`, la compilazione del progetto avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="5266f-309">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="5266f-310">Se si vuole includere solo quest'ultima DLL, è possibile aggiungere un `PackageTargetFallback` come segue per segnalare che la DLL `portable-net45+win81` è compatibile:</span><span class="sxs-lookup"><span data-stu-id="5266f-310">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="5266f-311">Per dichiarare un fallback per tutte le destinazioni nel progetto, non specificare l'attributo `Condition`.</span><span class="sxs-lookup"><span data-stu-id="5266f-311">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="5266f-312">È anche possibile estendere qualsiasi `PackageTargetFallback` esistente includendo `$(PackageTargetFallback)` come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5266f-312">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="5266f-313">Sostituzione di una libreria da un grafico di ripristino</span><span class="sxs-lookup"><span data-stu-id="5266f-313">Replacing one library from a restore graph</span></span>

<span data-ttu-id="5266f-314">Se un ripristino restituisce l'assembly errato, è possibile escludere la scelta predefinita di tali pacchetti e sostituirla con la propria scelta.</span><span class="sxs-lookup"><span data-stu-id="5266f-314">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="5266f-315">Prima di tutto, con un `PackageReference` di livello superiore, escludere tutti gli asset:</span><span class="sxs-lookup"><span data-stu-id="5266f-315">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="5266f-316">Aggiungere quindi il riferimento personalizzato alla copia locale appropriata della DLL:</span><span class="sxs-lookup"><span data-stu-id="5266f-316">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
