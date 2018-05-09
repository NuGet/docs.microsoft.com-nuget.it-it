---
title: Pack e restore di NuGet come destinazioni MSBuild
description: I comandi pack e restore di NuGet possono essere usati direttamente come destinazioni MSBuild con NuGet 4.0 +.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: e922da94a02450d4ea476c828209fa0cd4305725
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="623fa-103">Pack e restore di NuGet come destinazioni MSBuild</span><span class="sxs-lookup"><span data-stu-id="623fa-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="623fa-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="623fa-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="623fa-105">Con il formato PackageReference, NuGet 4.0 + può archiviare tutti i metadati del manifesto direttamente all'interno di un file di progetto, invece di usare un file `.nuspec` separato.</span><span class="sxs-lookup"><span data-stu-id="623fa-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="623fa-106">Con MSBuild 15.1 +, anche NuGet è un membro di MSBuild di prima classe con le destinazioni `pack` e `restore` come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="623fa-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="623fa-107">Queste destinazioni consentono di usare NuGet come qualsiasi altra attività o destinazione MSBuild.</span><span class="sxs-lookup"><span data-stu-id="623fa-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="623fa-108">Per NuGet 3.x e versioni precedenti, usare invece i comandi [pack](../tools/cli-ref-pack.md) e [restore](../tools/cli-ref-restore.md) tramite l'interfaccia della riga di comando di NuGet.</span><span class="sxs-lookup"><span data-stu-id="623fa-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="623fa-109">Ordine di compilazione delle destinazioni</span><span class="sxs-lookup"><span data-stu-id="623fa-109">Target build order</span></span>

<span data-ttu-id="623fa-110">Dato che `pack` e `restore` sono destinazioni MSBuild, è possibile accedervi per ottimizzare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="623fa-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="623fa-111">Si supponga, ad esempio, di voler copiare il pacchetto in una condivisione di rete dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="623fa-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="623fa-112">È possibile farlo aggiungendo quanto segue nel file di progetto:</span><span class="sxs-lookup"><span data-stu-id="623fa-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="623fa-113">Analogamente, è possibile scrivere un'attività MSBuild, scrivere la propria destinazione e utilizzare proprietà NuGet nell'attività MSBuild.</span><span class="sxs-lookup"><span data-stu-id="623fa-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="623fa-114">Destinazione pack</span><span class="sxs-lookup"><span data-stu-id="623fa-114">pack target</span></span>

<span data-ttu-id="623fa-115">Per i progetti .NET Standard utilizzando il formato PackageReference, utilizzando `msbuild /t:pack` disegna input dal file di progetto da utilizzare nella creazione di un pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="623fa-115">For .NET Standard projects using the PackageReference format, using `msbuild /t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="623fa-116">La tabella seguente descrive le proprietà di MSBuild che possono essere aggiunte a un file di progetto all'interno del primo nodo `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="623fa-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="623fa-117">È possibile apportare facilmente queste modifiche in Visual Studio 2017 e versioni successive facendo clic con il pulsante destro del mouse sul progetto e scegliendo **Modifica {nome_progetto}** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="623fa-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="623fa-118">Per praticità, la tabella è organizzata in base alla proprietà equivalente in un [file `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="623fa-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="623fa-119">Si noti che le proprietà `Owners` e `Summary` da `.nuspec` non sono supportate con MSBuild.</span><span class="sxs-lookup"><span data-stu-id="623fa-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="623fa-120">Valore di attributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="623fa-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="623fa-121">Proprietà MSBuild</span><span class="sxs-lookup"><span data-stu-id="623fa-121">MSBuild Property</span></span> | <span data-ttu-id="623fa-122">Impostazione predefinita</span><span class="sxs-lookup"><span data-stu-id="623fa-122">Default</span></span> | <span data-ttu-id="623fa-123">Note</span><span class="sxs-lookup"><span data-stu-id="623fa-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="623fa-124">Id</span><span class="sxs-lookup"><span data-stu-id="623fa-124">Id</span></span> | <span data-ttu-id="623fa-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="623fa-125">PackageId</span></span> | <span data-ttu-id="623fa-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="623fa-126">AssemblyName</span></span> | <span data-ttu-id="623fa-127">$(AssemblyName) da MSBuild</span><span class="sxs-lookup"><span data-stu-id="623fa-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="623fa-128">Versione</span><span class="sxs-lookup"><span data-stu-id="623fa-128">Version</span></span> | <span data-ttu-id="623fa-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="623fa-129">PackageVersion</span></span> | <span data-ttu-id="623fa-130">Versione</span><span class="sxs-lookup"><span data-stu-id="623fa-130">Version</span></span> | <span data-ttu-id="623fa-131">Compatibile con SemVer, ad esempio "1.0.0", "1.0.0-beta" o "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="623fa-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="623fa-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="623fa-132">VersionPrefix</span></span> | <span data-ttu-id="623fa-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="623fa-133">PackageVersionPrefix</span></span> | <span data-ttu-id="623fa-134">vuoto</span><span class="sxs-lookup"><span data-stu-id="623fa-134">empty</span></span> | <span data-ttu-id="623fa-135">L'impostazione di PackageVersion sovrascrive PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="623fa-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="623fa-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="623fa-136">VersionSuffix</span></span> | <span data-ttu-id="623fa-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="623fa-137">PackageVersionSuffix</span></span> | <span data-ttu-id="623fa-138">vuoto</span><span class="sxs-lookup"><span data-stu-id="623fa-138">empty</span></span> | <span data-ttu-id="623fa-139">$(VersionSuffix) da MSBuild.</span><span class="sxs-lookup"><span data-stu-id="623fa-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="623fa-140">L'impostazione di PackageVersion sovrascrive PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="623fa-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="623fa-141">Autori</span><span class="sxs-lookup"><span data-stu-id="623fa-141">Authors</span></span> | <span data-ttu-id="623fa-142">Autori</span><span class="sxs-lookup"><span data-stu-id="623fa-142">Authors</span></span> | <span data-ttu-id="623fa-143">Nome utente dell'utente corrente</span><span class="sxs-lookup"><span data-stu-id="623fa-143">Username of the current user</span></span> | |
| <span data-ttu-id="623fa-144">Proprietari</span><span class="sxs-lookup"><span data-stu-id="623fa-144">Owners</span></span> | <span data-ttu-id="623fa-145">N/D</span><span class="sxs-lookup"><span data-stu-id="623fa-145">N/A</span></span> | <span data-ttu-id="623fa-146">Non presente in NuSpec</span><span class="sxs-lookup"><span data-stu-id="623fa-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="623fa-147">Titolo</span><span class="sxs-lookup"><span data-stu-id="623fa-147">Title</span></span> | <span data-ttu-id="623fa-148">Titolo</span><span class="sxs-lookup"><span data-stu-id="623fa-148">Title</span></span> | <span data-ttu-id="623fa-149">PackageId</span><span class="sxs-lookup"><span data-stu-id="623fa-149">The PackageId</span></span>| |
| <span data-ttu-id="623fa-150">Descrizione</span><span class="sxs-lookup"><span data-stu-id="623fa-150">Description</span></span> | <span data-ttu-id="623fa-151">PackageDescription</span><span class="sxs-lookup"><span data-stu-id="623fa-151">PackageDescription</span></span> | <span data-ttu-id="623fa-152">"Descrizione del pacchetto"</span><span class="sxs-lookup"><span data-stu-id="623fa-152">"Package Description"</span></span> | |
| <span data-ttu-id="623fa-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="623fa-153">Copyright</span></span> | <span data-ttu-id="623fa-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="623fa-154">Copyright</span></span> | <span data-ttu-id="623fa-155">vuoto</span><span class="sxs-lookup"><span data-stu-id="623fa-155">empty</span></span> | |
| <span data-ttu-id="623fa-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="623fa-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="623fa-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="623fa-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="623fa-158">False</span><span class="sxs-lookup"><span data-stu-id="623fa-158">false</span></span> | |
| <span data-ttu-id="623fa-159">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="623fa-159">LicenseUrl</span></span> | <span data-ttu-id="623fa-160">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="623fa-160">PackageLicenseUrl</span></span> | <span data-ttu-id="623fa-161">vuoto</span><span class="sxs-lookup"><span data-stu-id="623fa-161">empty</span></span> | |
| <span data-ttu-id="623fa-162">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="623fa-162">ProjectUrl</span></span> | <span data-ttu-id="623fa-163">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="623fa-163">PackageProjectUrl</span></span> | <span data-ttu-id="623fa-164">vuoto</span><span class="sxs-lookup"><span data-stu-id="623fa-164">empty</span></span> | |
| <span data-ttu-id="623fa-165">IconUrl</span><span class="sxs-lookup"><span data-stu-id="623fa-165">IconUrl</span></span> | <span data-ttu-id="623fa-166">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="623fa-166">PackageIconUrl</span></span> | <span data-ttu-id="623fa-167">vuoto</span><span class="sxs-lookup"><span data-stu-id="623fa-167">empty</span></span> | |
| <span data-ttu-id="623fa-168">Tag</span><span class="sxs-lookup"><span data-stu-id="623fa-168">Tags</span></span> | <span data-ttu-id="623fa-169">PackageTags</span><span class="sxs-lookup"><span data-stu-id="623fa-169">PackageTags</span></span> | <span data-ttu-id="623fa-170">vuoto</span><span class="sxs-lookup"><span data-stu-id="623fa-170">empty</span></span> | <span data-ttu-id="623fa-171">I tag sono delimitati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="623fa-171">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="623fa-172">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="623fa-172">ReleaseNotes</span></span> | <span data-ttu-id="623fa-173">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="623fa-173">PackageReleaseNotes</span></span> | <span data-ttu-id="623fa-174">vuoto</span><span class="sxs-lookup"><span data-stu-id="623fa-174">empty</span></span> | |
| <span data-ttu-id="623fa-175">Url del repository /</span><span class="sxs-lookup"><span data-stu-id="623fa-175">Repository/Url</span></span> | <span data-ttu-id="623fa-176">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="623fa-176">RepositoryUrl</span></span> | <span data-ttu-id="623fa-177">vuoto</span><span class="sxs-lookup"><span data-stu-id="623fa-177">empty</span></span> | <span data-ttu-id="623fa-178">URL del repository utilizzata per clonare o recuperare il codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="623fa-178">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="623fa-179">Esempio: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="623fa-179">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="623fa-180">Tipo di repository /</span><span class="sxs-lookup"><span data-stu-id="623fa-180">Repository/Type</span></span> | <span data-ttu-id="623fa-181">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="623fa-181">RepositoryType</span></span> | <span data-ttu-id="623fa-182">vuoto</span><span class="sxs-lookup"><span data-stu-id="623fa-182">empty</span></span> | <span data-ttu-id="623fa-183">Tipo di repository.</span><span class="sxs-lookup"><span data-stu-id="623fa-183">Repository type.</span></span> <span data-ttu-id="623fa-184">Esempi: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="623fa-184">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="623fa-185">Ramo del repository /</span><span class="sxs-lookup"><span data-stu-id="623fa-185">Repository/Branch</span></span> | <span data-ttu-id="623fa-186">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="623fa-186">RepositoryBranch</span></span> | <span data-ttu-id="623fa-187">vuoto</span><span class="sxs-lookup"><span data-stu-id="623fa-187">empty</span></span> | <span data-ttu-id="623fa-188">Informazioni di ramo del repository facoltativo.</span><span class="sxs-lookup"><span data-stu-id="623fa-188">Optional repository branch information.</span></span> <span data-ttu-id="623fa-189">*RepositoryUrl* deve anche essere specificato per questa proprietà deve essere incluso.</span><span class="sxs-lookup"><span data-stu-id="623fa-189">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="623fa-190">Esempio: *master* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="623fa-190">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="623fa-191">Repository/Commit</span><span class="sxs-lookup"><span data-stu-id="623fa-191">Repository/Commit</span></span> | <span data-ttu-id="623fa-192">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="623fa-192">RepositoryCommit</span></span> | <span data-ttu-id="623fa-193">vuoto</span><span class="sxs-lookup"><span data-stu-id="623fa-193">empty</span></span> | <span data-ttu-id="623fa-194">Commit repository facoltativo o insieme di modifiche per indicare che il pacchetto di origine è stato compilato con.</span><span class="sxs-lookup"><span data-stu-id="623fa-194">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="623fa-195">*RepositoryUrl* deve anche essere specificato per questa proprietà deve essere incluso.</span><span class="sxs-lookup"><span data-stu-id="623fa-195">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="623fa-196">Esempio: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="623fa-196">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="623fa-197">PackageType</span><span class="sxs-lookup"><span data-stu-id="623fa-197">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="623fa-198">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="623fa-198">Summary</span></span> | <span data-ttu-id="623fa-199">Non supportato</span><span class="sxs-lookup"><span data-stu-id="623fa-199">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="623fa-200">Input destinazione pack</span><span class="sxs-lookup"><span data-stu-id="623fa-200">pack target inputs</span></span>

- <span data-ttu-id="623fa-201">IsPackable</span><span class="sxs-lookup"><span data-stu-id="623fa-201">IsPackable</span></span>
- <span data-ttu-id="623fa-202">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="623fa-202">PackageVersion</span></span>
- <span data-ttu-id="623fa-203">PackageId</span><span class="sxs-lookup"><span data-stu-id="623fa-203">PackageId</span></span>
- <span data-ttu-id="623fa-204">Autori</span><span class="sxs-lookup"><span data-stu-id="623fa-204">Authors</span></span>
- <span data-ttu-id="623fa-205">Descrizione</span><span class="sxs-lookup"><span data-stu-id="623fa-205">Description</span></span>
- <span data-ttu-id="623fa-206">Copyright</span><span class="sxs-lookup"><span data-stu-id="623fa-206">Copyright</span></span>
- <span data-ttu-id="623fa-207">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="623fa-207">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="623fa-208">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="623fa-208">DevelopmentDependency</span></span>
- <span data-ttu-id="623fa-209">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="623fa-209">PackageLicenseUrl</span></span>
- <span data-ttu-id="623fa-210">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="623fa-210">PackageProjectUrl</span></span>
- <span data-ttu-id="623fa-211">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="623fa-211">PackageIconUrl</span></span>
- <span data-ttu-id="623fa-212">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="623fa-212">PackageReleaseNotes</span></span>
- <span data-ttu-id="623fa-213">PackageTags</span><span class="sxs-lookup"><span data-stu-id="623fa-213">PackageTags</span></span>
- <span data-ttu-id="623fa-214">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="623fa-214">PackageOutputPath</span></span>
- <span data-ttu-id="623fa-215">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="623fa-215">IncludeSymbols</span></span>
- <span data-ttu-id="623fa-216">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="623fa-216">IncludeSource</span></span>
- <span data-ttu-id="623fa-217">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="623fa-217">PackageTypes</span></span>
- <span data-ttu-id="623fa-218">IsTool</span><span class="sxs-lookup"><span data-stu-id="623fa-218">IsTool</span></span>
- <span data-ttu-id="623fa-219">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="623fa-219">RepositoryUrl</span></span>
- <span data-ttu-id="623fa-220">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="623fa-220">RepositoryType</span></span>
- <span data-ttu-id="623fa-221">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="623fa-221">RepositoryBranch</span></span>
- <span data-ttu-id="623fa-222">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="623fa-222">RepositoryCommit</span></span>
- <span data-ttu-id="623fa-223">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="623fa-223">NoPackageAnalysis</span></span>
- <span data-ttu-id="623fa-224">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="623fa-224">MinClientVersion</span></span>
- <span data-ttu-id="623fa-225">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="623fa-225">IncludeBuildOutput</span></span>
- <span data-ttu-id="623fa-226">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="623fa-226">IncludeContentInPack</span></span>
- <span data-ttu-id="623fa-227">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="623fa-227">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="623fa-228">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="623fa-228">ContentTargetFolders</span></span>
- <span data-ttu-id="623fa-229">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="623fa-229">NuspecFile</span></span>
- <span data-ttu-id="623fa-230">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="623fa-230">NuspecBasePath</span></span>
- <span data-ttu-id="623fa-231">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="623fa-231">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="623fa-232">Scenari pack</span><span class="sxs-lookup"><span data-stu-id="623fa-232">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="623fa-233">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="623fa-233">PackageIconUrl</span></span>

<span data-ttu-id="623fa-234">Come parte della modifica del [NuGet problema 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` alla fine verrà modificato in `PackageIconUri` e può essere un percorso relativo a un file di icona che verrà incluso nella directory principale del pacchetto risulta.</span><span class="sxs-lookup"><span data-stu-id="623fa-234">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="623fa-235">Assembly di output</span><span class="sxs-lookup"><span data-stu-id="623fa-235">Output assemblies</span></span>

<span data-ttu-id="623fa-236">`nuget pack` copia i file di output con le estensioni `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="623fa-236">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="623fa-237">I file di output copiati dipendono da quanto fornito da MSBuild dalla destinazione `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="623fa-237">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="623fa-238">Sono disponibili due proprietà di MSBuild che è possibile usare nel file di progetto o nella riga di comando per controllare la destinazione degli assembly di output:</span><span class="sxs-lookup"><span data-stu-id="623fa-238">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="623fa-239">`IncludeBuildOutput`: valore booleano che determina se gli assembly di output della compilazione devono essere inclusi nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="623fa-239">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="623fa-240">`BuildOutputTargetFolder`: specifica la cartella in cui devono essere posizionati gli assembly di output.</span><span class="sxs-lookup"><span data-stu-id="623fa-240">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="623fa-241">Gli assembly di output (e altri file di output) vengono copiati nelle rispettive cartelle per framework.</span><span class="sxs-lookup"><span data-stu-id="623fa-241">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="623fa-242">Riferimenti ai pacchetti</span><span class="sxs-lookup"><span data-stu-id="623fa-242">Package references</span></span>

<span data-ttu-id="623fa-243">Vedere [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="623fa-243">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="623fa-244">Riferimenti da progetto a progetto</span><span class="sxs-lookup"><span data-stu-id="623fa-244">Project to project references</span></span>

<span data-ttu-id="623fa-245">I riferimenti da progetto a progetto sono considerati per impostazione predefinita come riferimenti a pacchetti NuGet, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="623fa-245">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="623fa-246">È anche possibile aggiungere i metadati seguenti ai riferimenti del progetto:</span><span class="sxs-lookup"><span data-stu-id="623fa-246">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="623fa-247">Inclusione di contenuto in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="623fa-247">Including content in a package</span></span>

<span data-ttu-id="623fa-248">Per includere il contenuto, aggiungere altri metadati all'elemento `<Content>` esistente.</span><span class="sxs-lookup"><span data-stu-id="623fa-248">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="623fa-249">Per impostazione predefinita tutti gli elementi di tipo"Content" vengono inclusi nel pacchetto, a meno che non si esegua l'override con voci simili al codice seguente:</span><span class="sxs-lookup"><span data-stu-id="623fa-249">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="623fa-250">Per impostazione predefinita, tutti gli elementi vengono aggiunti alla radice di `content` e della cartella `contentFiles\any\<target_framework>` all'interno di un pacchetto e viene mantenuta la struttura di cartelle relative, a meno che non si specifichi un percorso di pacchetto:</span><span class="sxs-lookup"><span data-stu-id="623fa-250">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="623fa-251">Se si vuole copiare tutto il contenuto sono in cartelle radice specifiche (invece di copiarlo sia in `content` che in `contentFiles`), è possibile usare la proprietà di MSBuild `ContentTargetFolders`, che ha il valore predefinito "content;contentFiles" ma può essere impostata su qualsiasi altro nome di cartella.</span><span class="sxs-lookup"><span data-stu-id="623fa-251">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="623fa-252">Si noti che se si specifica solo "contentFiles" in `ContentTargetFolders`, i file vengono posizionati in `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` in base a `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="623fa-252">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="623fa-253">`PackagePath` può essere un set di percorsi di destinazione delimitati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="623fa-253">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="623fa-254">Se si specifica un percorso di pacchetto vuoto, il file viene aggiunto alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="623fa-254">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="623fa-255">Ad esempio, il codice seguente aggiunge `libuv.txt` a `content\myfiles`, `content\samples` e nella radice del pacchetto:</span><span class="sxs-lookup"><span data-stu-id="623fa-255">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="623fa-256">È disponibile anche una proprietà di MSBuild `$(IncludeContentInPack)`, con valore predefinito `true`.</span><span class="sxs-lookup"><span data-stu-id="623fa-256">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="623fa-257">Se questa proprietà viene impostata su `false` in qualsiasi progetto, il contenuto da tale progetto non viene incluso nel pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="623fa-257">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="623fa-258">Altri metadati specifici di pack che è possibile impostare per qualsiasi elemento precedente includono ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, che impostano i valori ```CopyToOutput``` e ```Flatten``` sulla voce ```contentFiles``` nel file nuspec di output.</span><span class="sxs-lookup"><span data-stu-id="623fa-258">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="623fa-259">Oltre agli elementi Content, i metadati `<Pack>` e `<PackagePath>` possono anche essere impostati nei file con l'azione di compilazione Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o None.</span><span class="sxs-lookup"><span data-stu-id="623fa-259">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="623fa-260">Per fare in modo che il comando pack aggiunga il nome del file al percorso del pacchetto quando si usano modelli con caratteri jolly (glob), il percorso del pacchetto deve terminare con il carattere separatore di cartella. In caso contrario, il percorso del pacchetto viene interpretato come percorso completo, incluso il nome del file.</span><span class="sxs-lookup"><span data-stu-id="623fa-260">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="623fa-261">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="623fa-261">IncludeSymbols</span></span>

<span data-ttu-id="623fa-262">Quando si usa `MSBuild /t:pack /p:IncludeSymbols=true`, i file `.pdb` corrispondenti vengono copiati insieme agli altri file di output (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="623fa-262">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="623fa-263">Si noti che l'impostazione `IncludeSymbols=true` crea un pacchetto regolare *e* un pacchetto di simboli.</span><span class="sxs-lookup"><span data-stu-id="623fa-263">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="623fa-264">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="623fa-264">IncludeSource</span></span>

<span data-ttu-id="623fa-265">Equivale a `IncludeSymbols`, ma insieme ai file `.pdb` vengono copiati anche i file di origine.</span><span class="sxs-lookup"><span data-stu-id="623fa-265">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="623fa-266">Tutti i file di tipo `Compile` vengono copiati in `src\<ProjectName>\` conservando la struttura di cartelle del percorso relativo nel pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="623fa-266">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="623fa-267">Lo stesso accade anche per i file di origine di qualsiasi `ProjectReference` con `TreatAsPackageReference` impostato su `false`.</span><span class="sxs-lookup"><span data-stu-id="623fa-267">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="623fa-268">Se un file di tipo Compile è all'esterno della cartella di progetto, viene semplicemente aggiunto a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="623fa-268">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="623fa-269">IsTool</span><span class="sxs-lookup"><span data-stu-id="623fa-269">IsTool</span></span>

<span data-ttu-id="623fa-270">Quando si usa `MSBuild /t:pack /p:IsTool=true`, tutti i file, come specificato nello scenario [Assembly di output](#output-assemblies), vengono copiati nella cartella `tools` invece che nella cartella `lib`.</span><span class="sxs-lookup"><span data-stu-id="623fa-270">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="623fa-271">Si noti che questo comportamento è diverso da `DotNetCliTool`, che viene specificato impostando `PackageType` nel file `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="623fa-271">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="623fa-272">Creazione di un pacchetto con un file .nuspec</span><span class="sxs-lookup"><span data-stu-id="623fa-272">Packing using a .nuspec</span></span>

<span data-ttu-id="623fa-273">È possibile utilizzare un `.nuspec` file per comprimere il progetto, purché si disponga di un file di progetto SDK da importare `NuGet.Build.Tasks.Pack.targets` in modo che l'attività di Service pack può essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="623fa-273">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="623fa-274">È comunque necessario ripristinare il progetto prima di possibile comprimere un file nuspec.</span><span class="sxs-lookup"><span data-stu-id="623fa-274">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="623fa-275">Il framework di destinazione del file di progetto è irrilevante e non utilizzata per la compressione di un nuspec.</span><span class="sxs-lookup"><span data-stu-id="623fa-275">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="623fa-276">Le tre proprietà di MSBuild seguenti sono rilevanti per la creazione di pacchetti con un file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="623fa-276">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="623fa-277">`NuspecFile`: percorso relativo o assoluto per il file `.nuspec` usato per la creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="623fa-277">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="623fa-278">`NuspecProperties`: elenco con valori delimitati da punto e virgola di coppie chiave=valore.</span><span class="sxs-lookup"><span data-stu-id="623fa-278">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="623fa-279">A causa della modalità di funzionamento dell'analisi della riga di comando di MSBuild, è necessario specificare più proprietà come indicato di seguito: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="623fa-279">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="623fa-280">`NuspecBasePath`: percorso di base per il file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="623fa-280">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="623fa-281">Se si usa `dotnet.exe` per creare il pacchetto del progetto, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="623fa-281">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="623fa-282">Se si usa MSBuild per creare il pacchetto del progetto, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="623fa-282">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="623fa-283">Si noti che un nuspec di compressione utilizzando dotnet.exe o msbuild comporta anche per la compilazione del progetto per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="623fa-283">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="623fa-284">Questo può essere evitato passando ```--no-build``` dotnet.exe, che equivale all'impostazione della proprietà ```<NoBuild>true</NoBuild> ``` nel file di progetto, insieme a impostazione ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` nel file di progetto</span><span class="sxs-lookup"><span data-stu-id="623fa-284">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="623fa-285">È un esempio di un file csproj per comprimere un file nuspec.</span><span class="sxs-lookup"><span data-stu-id="623fa-285">An example of a csproj file to pack a nuspec file is:</span></span>

```
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="623fa-286">Advanced punti di estensione per creare pacchetto personalizzato</span><span class="sxs-lookup"><span data-stu-id="623fa-286">Advanced extension points to create customized package</span></span>

<span data-ttu-id="623fa-287">Il `pack` destinazione fornisce due punti di estensione che eseguono l'interna, compilazione specifica framework di destinazione.</span><span class="sxs-lookup"><span data-stu-id="623fa-287">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="623fa-288">I punti di estensione supportano inclusi contenuto specifico framework di destinazione e assembly in un pacchetto:</span><span class="sxs-lookup"><span data-stu-id="623fa-288">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="623fa-289">`TargetsForTfmSpecificBuildOutput` destinazione: usare per i file all'interno di `lib` cartella o una cartella specificata utilizzando `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="623fa-289">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="623fa-290">`TargetsForTfmSpecificContentInPackage` destinazione: usare per i file all'esterno di `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="623fa-290">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="623fa-291">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="623fa-291">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="623fa-292">Scrivere una destinazione personalizzata e specificarlo come valore della `$(TargetsForTfmSpecificBuildOutput)` proprietà.</span><span class="sxs-lookup"><span data-stu-id="623fa-292">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="623fa-293">Per tutti i file che devono passare nel `BuildOutputTargetFolder` (lib per impostazione predefinita), la destinazione deve scrivere tali file in ItemGroup `BuildOutputInPackage` e impostare i due valori di metadati seguenti:</span><span class="sxs-lookup"><span data-stu-id="623fa-293">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="623fa-294">`FinalOutputPath`: Il percorso assoluto del file. Se omesso, l'identità viene utilizzata per valutare il percorso di origine.</span><span class="sxs-lookup"><span data-stu-id="623fa-294">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="623fa-295">`TargetPath`: (Facoltativo) impostare quando il file deve essere inviato in una sottocartella all'interno di `lib\<TargetFramework>` , come assembly satellite che vanno sotto le cartelle delle rispettive impostazioni cultura.</span><span class="sxs-lookup"><span data-stu-id="623fa-295">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="623fa-296">Valore predefinito è il nome del file.</span><span class="sxs-lookup"><span data-stu-id="623fa-296">Defaults to the name of the file.</span></span>

<span data-ttu-id="623fa-297">Esempio:</span><span class="sxs-lookup"><span data-stu-id="623fa-297">Example:</span></span>

```
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="623fa-298">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="623fa-298">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="623fa-299">Scrivere una destinazione personalizzata e specificarlo come valore della `$(TargetsForTfmSpecificContentInPackage)` proprietà.</span><span class="sxs-lookup"><span data-stu-id="623fa-299">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="623fa-300">Per tutti i file da includere nel pacchetto, la destinazione deve scrivere tali file in ItemGroup `TfmSpecificPackageFile` e impostare i metadati facoltativi seguenti:</span><span class="sxs-lookup"><span data-stu-id="623fa-300">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="623fa-301">`PackagePath`: Percorso in cui il file deve essere l'output del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="623fa-301">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="623fa-302">NuGet genera un avviso se più di un file viene aggiunto al percorso del pacchetto stesso.</span><span class="sxs-lookup"><span data-stu-id="623fa-302">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="623fa-303">`BuildAction`: L'azione di compilazione da assegnare al file, è obbligatorio solo se il percorso del pacchetto è nel `contentFiles` cartella.</span><span class="sxs-lookup"><span data-stu-id="623fa-303">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="623fa-304">Valore predefinito è "None".</span><span class="sxs-lookup"><span data-stu-id="623fa-304">Defaults to "None".</span></span>

<span data-ttu-id="623fa-305">Un esempio:</span><span class="sxs-lookup"><span data-stu-id="623fa-305">An example:</span></span>
```
<PropertyGroup>
    <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name=""CustomContentTarget"">
    <ItemGroup>
      <TfmSpecificPackageFile Include=""abc.txt"">
        <PackagePath>mycontent/$(TargetFramework)</PackagePath>
      </TfmSpecificPackageFile>
      <TfmSpecificPackageFile Include=""Extensions/ext.txt"" Condition=""'$(TargetFramework)' == 'net46'"">
        <PackagePath>net46content</PackagePath>
      </TfmSpecificPackageFile>  
    </ItemGroup>
  </Target>  
```

## <a name="restore-target"></a><span data-ttu-id="623fa-306">Destinazione restore</span><span class="sxs-lookup"><span data-stu-id="623fa-306">restore target</span></span>

<span data-ttu-id="623fa-307">`MSBuild /t:restore` (usato da `nuget restore` e `dotnet restore` con progetti .NET Core) consente di ripristinare i pacchetti a cui si fa riferimento nel file di progetto, come segue:</span><span class="sxs-lookup"><span data-stu-id="623fa-307">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="623fa-308">Lettura di tutti i riferimenti da progetto a progetto</span><span class="sxs-lookup"><span data-stu-id="623fa-308">Read all project to project references</span></span>
1. <span data-ttu-id="623fa-309">Lettura delle proprietà del progetto per trovare la cartella intermedia e i framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="623fa-309">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="623fa-310">Passaggio dei dati msbuild a NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="623fa-310">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="623fa-311">Esecuzione di restore</span><span class="sxs-lookup"><span data-stu-id="623fa-311">Run restore</span></span>
1. <span data-ttu-id="623fa-312">Download dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="623fa-312">Download packages</span></span>
1. <span data-ttu-id="623fa-313">Scrittura dei file di asset, delle destinazioni e delle proprietà</span><span class="sxs-lookup"><span data-stu-id="623fa-313">Write assets file, targets, and props</span></span>

<span data-ttu-id="623fa-314">Il `restore` destinazione works **solo** per i progetti utilizzando il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="623fa-314">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="623fa-315">Caso **non** funzionano per i progetti utilizzando il `packages.config` formato; utilizzare [ripristino nuget](../tools/cli-ref-restore.md) invece.</span><span class="sxs-lookup"><span data-stu-id="623fa-315">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="623fa-316">Ripristino delle proprietà</span><span class="sxs-lookup"><span data-stu-id="623fa-316">Restore properties</span></span>

<span data-ttu-id="623fa-317">Possono esistere ulteriori impostazioni di ripristino derivate da proprietà di MSBuild nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="623fa-317">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="623fa-318">I valori possono essere impostati anche dalla riga di comando tramite l'opzione `/p:` (vedere gli esempi riportati di seguito).</span><span class="sxs-lookup"><span data-stu-id="623fa-318">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="623fa-319">Proprietà</span><span class="sxs-lookup"><span data-stu-id="623fa-319">Property</span></span> | <span data-ttu-id="623fa-320">Descrizione</span><span class="sxs-lookup"><span data-stu-id="623fa-320">Description</span></span> |
|--------|--------|
| <span data-ttu-id="623fa-321">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="623fa-321">RestoreSources</span></span> | <span data-ttu-id="623fa-322">Elenco delimitato da punto e virgola delle origini di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="623fa-322">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="623fa-323">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="623fa-323">RestorePackagesPath</span></span> | <span data-ttu-id="623fa-324">Percorso della cartella dei pacchetti dell'utente.</span><span class="sxs-lookup"><span data-stu-id="623fa-324">User packages folder path.</span></span> |
| <span data-ttu-id="623fa-325">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="623fa-325">RestoreDisableParallel</span></span> | <span data-ttu-id="623fa-326">Consente di limitare i download a uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="623fa-326">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="623fa-327">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="623fa-327">RestoreConfigFile</span></span> | <span data-ttu-id="623fa-328">Percorso per un file `Nuget.Config` da applicare.</span><span class="sxs-lookup"><span data-stu-id="623fa-328">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="623fa-329">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="623fa-329">RestoreNoCache</span></span> | <span data-ttu-id="623fa-330">Se true, si evita l'uso di pacchetti memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="623fa-330">If true, avoids using cached packages.</span></span> <span data-ttu-id="623fa-331">Vedere [gestione dei pacchetti globali e alla cartella della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="623fa-331">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="623fa-332">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="623fa-332">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="623fa-333">Se true, ignora le origini di pacchetti in errore o mancanti.</span><span class="sxs-lookup"><span data-stu-id="623fa-333">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="623fa-334">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="623fa-334">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="623fa-335">Percorso di `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="623fa-335">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="623fa-336">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="623fa-336">RestoreGraphProjectInput</span></span> | <span data-ttu-id="623fa-337">Elenco delimitato da punto e virgola dei progetti da ripristinare, che deve contenere percorsi assoluti.</span><span class="sxs-lookup"><span data-stu-id="623fa-337">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="623fa-338">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="623fa-338">RestoreOutputPath</span></span> | <span data-ttu-id="623fa-339">Cartella di output. Per impostazione predefinita, la cartella `obj`.</span><span class="sxs-lookup"><span data-stu-id="623fa-339">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="623fa-340">Esempi</span><span class="sxs-lookup"><span data-stu-id="623fa-340">Examples</span></span>

<span data-ttu-id="623fa-341">Riga di comando:</span><span class="sxs-lookup"><span data-stu-id="623fa-341">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="623fa-342">File di progetto:</span><span class="sxs-lookup"><span data-stu-id="623fa-342">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="623fa-343">Output del ripristino</span><span class="sxs-lookup"><span data-stu-id="623fa-343">Restore outputs</span></span>

<span data-ttu-id="623fa-344">Il ripristino crea i file seguenti nella cartella `obj` di compilazione:</span><span class="sxs-lookup"><span data-stu-id="623fa-344">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="623fa-345">File</span><span class="sxs-lookup"><span data-stu-id="623fa-345">File</span></span> | <span data-ttu-id="623fa-346">Descrizione</span><span class="sxs-lookup"><span data-stu-id="623fa-346">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="623fa-347">Contiene il grafico delle dipendenze di tutti i riferimenti di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="623fa-347">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="623fa-348">Riferimenti alle proprietà di MSBuild contenute nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="623fa-348">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="623fa-349">Riferimenti alle destinazioni di MSBuild contenute nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="623fa-349">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="623fa-350">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="623fa-350">PackageTargetFallback</span></span>

<span data-ttu-id="623fa-351">L'elemento `PackageTargetFallback` consente di specificare un set di destinazioni compatibili da usare durante il ripristino di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="623fa-351">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="623fa-352">È progettato per consentire ai pacchetti che usano un [TxM](../reference/target-frameworks.md) dotnet di interagire con pacchetti compatibili che non dichiarano un TxM dotnet.</span><span class="sxs-lookup"><span data-stu-id="623fa-352">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="623fa-353">Se il progetto usa il TxM dotnet, devono averlo anche tutti i pacchetti da cui il progetto dipende, a meno che non si aggiunga `<PackageTargetFallback>` al progetto, in modo da rendere compatibili con dotnet le piattaforme che non lo sono.</span><span class="sxs-lookup"><span data-stu-id="623fa-353">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="623fa-354">Ad esempio, se il progetto usa il TxM `netstandard1.6` e un pacchetto dipendente contiene solo `lib/net45/a.dll` e `lib/portable-net45+win81/a.dll`, la compilazione del progetto avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="623fa-354">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="623fa-355">Se si vuole includere solo quest'ultima DLL, è possibile aggiungere un `PackageTargetFallback` come segue per segnalare che la DLL `portable-net45+win81` è compatibile:</span><span class="sxs-lookup"><span data-stu-id="623fa-355">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="623fa-356">Per dichiarare un fallback per tutte le destinazioni nel progetto, non specificare l'attributo `Condition`.</span><span class="sxs-lookup"><span data-stu-id="623fa-356">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="623fa-357">È anche possibile estendere qualsiasi `PackageTargetFallback` esistente includendo `$(PackageTargetFallback)` come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="623fa-357">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="623fa-358">Sostituzione di una libreria da un grafico di ripristino</span><span class="sxs-lookup"><span data-stu-id="623fa-358">Replacing one library from a restore graph</span></span>

<span data-ttu-id="623fa-359">Se un ripristino restituisce l'assembly errato, è possibile escludere la scelta predefinita di tali pacchetti e sostituirla con la propria scelta.</span><span class="sxs-lookup"><span data-stu-id="623fa-359">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="623fa-360">Prima di tutto, con un `PackageReference` di livello superiore, escludere tutti gli asset:</span><span class="sxs-lookup"><span data-stu-id="623fa-360">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="623fa-361">Aggiungere quindi il riferimento personalizzato alla copia locale appropriata della DLL:</span><span class="sxs-lookup"><span data-stu-id="623fa-361">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
