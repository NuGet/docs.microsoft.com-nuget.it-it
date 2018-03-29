---
title: Pack e restore di NuGet come destinazioni MSBuild | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: I comandi pack e restore di NuGet possono essere usati direttamente come destinazioni MSBuild con NuGet 4.0 +.
keywords: NuGet e MSBuild, destinazione pack NuGet, destinazione restore NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: a9c2c2229d717dff8472dce0ba568e4a21900b19
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="fa1b6-104">Pack e restore di NuGet come destinazioni MSBuild</span><span class="sxs-lookup"><span data-stu-id="fa1b6-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="fa1b6-105">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="fa1b6-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="fa1b6-106">Con il formato PackageReference, NuGet 4.0 + può archiviare tutti i metadati del manifesto direttamente all'interno di un file di progetto, invece di usare un file `.nuspec` separato.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="fa1b6-107">Con MSBuild 15.1 +, anche NuGet è un membro di MSBuild di prima classe con le destinazioni `pack` e `restore` come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="fa1b6-108">Queste destinazioni consentono di usare NuGet come qualsiasi altra attività o destinazione MSBuild.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="fa1b6-109">Per NuGet 3.x e versioni precedenti, usare invece i comandi [pack](../tools/cli-ref-pack.md) e [restore](../tools/cli-ref-restore.md) tramite l'interfaccia della riga di comando di NuGet.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="fa1b6-110">Ordine di compilazione delle destinazioni</span><span class="sxs-lookup"><span data-stu-id="fa1b6-110">Target build order</span></span>

<span data-ttu-id="fa1b6-111">Dato che `pack` e `restore` sono destinazioni MSBuild, è possibile accedervi per ottimizzare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="fa1b6-112">Si supponga, ad esempio, di voler copiare il pacchetto in una condivisione di rete dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="fa1b6-113">È possibile farlo aggiungendo quanto segue nel file di progetto:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="fa1b6-114">Analogamente, è possibile scrivere un'attività MSBuild, scrivere la propria destinazione e utilizzare proprietà NuGet nell'attività MSBuild.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="fa1b6-115">Destinazione pack</span><span class="sxs-lookup"><span data-stu-id="fa1b6-115">pack target</span></span>

<span data-ttu-id="fa1b6-116">Per i progetti .NET Standard utilizzando il formato PackageReference, utilizzando `msbuild /t:pack` disegna input dal file di progetto da utilizzare nella creazione di un pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-116">For .NET Standard projects using the PackageReference format, using `msbuild /t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="fa1b6-117">La tabella seguente descrive le proprietà di MSBuild che possono essere aggiunte a un file di progetto all'interno del primo nodo `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="fa1b6-118">È possibile apportare facilmente queste modifiche in Visual Studio 2017 e versioni successive facendo clic con il pulsante destro del mouse sul progetto e scegliendo **Modifica {nome_progetto}** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="fa1b6-119">Per praticità, la tabella è organizzata in base alla proprietà equivalente in un [file `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="fa1b6-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="fa1b6-120">Si noti che le proprietà `Owners` e `Summary` da `.nuspec` non sono supportate con MSBuild.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="fa1b6-121">Valore di attributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="fa1b6-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="fa1b6-122">Proprietà MSBuild</span><span class="sxs-lookup"><span data-stu-id="fa1b6-122">MSBuild Property</span></span> | <span data-ttu-id="fa1b6-123">Impostazione predefinita</span><span class="sxs-lookup"><span data-stu-id="fa1b6-123">Default</span></span> | <span data-ttu-id="fa1b6-124">Note</span><span class="sxs-lookup"><span data-stu-id="fa1b6-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="fa1b6-125">Id</span><span class="sxs-lookup"><span data-stu-id="fa1b6-125">Id</span></span> | <span data-ttu-id="fa1b6-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="fa1b6-126">PackageId</span></span> | <span data-ttu-id="fa1b6-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="fa1b6-127">AssemblyName</span></span> | <span data-ttu-id="fa1b6-128">$(AssemblyName) da MSBuild</span><span class="sxs-lookup"><span data-stu-id="fa1b6-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="fa1b6-129">Versione</span><span class="sxs-lookup"><span data-stu-id="fa1b6-129">Version</span></span> | <span data-ttu-id="fa1b6-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="fa1b6-130">PackageVersion</span></span> | <span data-ttu-id="fa1b6-131">Versione</span><span class="sxs-lookup"><span data-stu-id="fa1b6-131">Version</span></span> | <span data-ttu-id="fa1b6-132">Compatibile con SemVer, ad esempio "1.0.0", "1.0.0-beta" o "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="fa1b6-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="fa1b6-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="fa1b6-133">VersionPrefix</span></span> | <span data-ttu-id="fa1b6-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="fa1b6-134">PackageVersionPrefix</span></span> | <span data-ttu-id="fa1b6-135">vuoto</span><span class="sxs-lookup"><span data-stu-id="fa1b6-135">empty</span></span> | <span data-ttu-id="fa1b6-136">L'impostazione di PackageVersion sovrascrive PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="fa1b6-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="fa1b6-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="fa1b6-137">VersionSuffix</span></span> | <span data-ttu-id="fa1b6-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="fa1b6-138">PackageVersionSuffix</span></span> | <span data-ttu-id="fa1b6-139">vuoto</span><span class="sxs-lookup"><span data-stu-id="fa1b6-139">empty</span></span> | <span data-ttu-id="fa1b6-140">$(VersionSuffix) da MSBuild.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="fa1b6-141">L'impostazione di PackageVersion sovrascrive PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="fa1b6-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="fa1b6-142">Autori</span><span class="sxs-lookup"><span data-stu-id="fa1b6-142">Authors</span></span> | <span data-ttu-id="fa1b6-143">Autori</span><span class="sxs-lookup"><span data-stu-id="fa1b6-143">Authors</span></span> | <span data-ttu-id="fa1b6-144">Nome utente dell'utente corrente</span><span class="sxs-lookup"><span data-stu-id="fa1b6-144">Username of the current user</span></span> | |
| <span data-ttu-id="fa1b6-145">Proprietari</span><span class="sxs-lookup"><span data-stu-id="fa1b6-145">Owners</span></span> | <span data-ttu-id="fa1b6-146">N/D</span><span class="sxs-lookup"><span data-stu-id="fa1b6-146">N/A</span></span> | <span data-ttu-id="fa1b6-147">Non presente in NuSpec</span><span class="sxs-lookup"><span data-stu-id="fa1b6-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="fa1b6-148">Titolo</span><span class="sxs-lookup"><span data-stu-id="fa1b6-148">Title</span></span> | <span data-ttu-id="fa1b6-149">Titolo</span><span class="sxs-lookup"><span data-stu-id="fa1b6-149">Title</span></span> | <span data-ttu-id="fa1b6-150">PackageId</span><span class="sxs-lookup"><span data-stu-id="fa1b6-150">The PackageId</span></span>| |
| <span data-ttu-id="fa1b6-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fa1b6-151">Description</span></span> | <span data-ttu-id="fa1b6-152">PackageDescription</span><span class="sxs-lookup"><span data-stu-id="fa1b6-152">PackageDescription</span></span> | <span data-ttu-id="fa1b6-153">"Descrizione del pacchetto"</span><span class="sxs-lookup"><span data-stu-id="fa1b6-153">"Package Description"</span></span> | |
| <span data-ttu-id="fa1b6-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="fa1b6-154">Copyright</span></span> | <span data-ttu-id="fa1b6-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="fa1b6-155">Copyright</span></span> | <span data-ttu-id="fa1b6-156">vuoto</span><span class="sxs-lookup"><span data-stu-id="fa1b6-156">empty</span></span> | |
| <span data-ttu-id="fa1b6-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="fa1b6-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="fa1b6-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="fa1b6-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="fa1b6-159">False</span><span class="sxs-lookup"><span data-stu-id="fa1b6-159">false</span></span> | |
| <span data-ttu-id="fa1b6-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="fa1b6-160">LicenseUrl</span></span> | <span data-ttu-id="fa1b6-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="fa1b6-161">PackageLicenseUrl</span></span> | <span data-ttu-id="fa1b6-162">vuoto</span><span class="sxs-lookup"><span data-stu-id="fa1b6-162">empty</span></span> | |
| <span data-ttu-id="fa1b6-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="fa1b6-163">ProjectUrl</span></span> | <span data-ttu-id="fa1b6-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="fa1b6-164">PackageProjectUrl</span></span> | <span data-ttu-id="fa1b6-165">vuoto</span><span class="sxs-lookup"><span data-stu-id="fa1b6-165">empty</span></span> | |
| <span data-ttu-id="fa1b6-166">IconUrl</span><span class="sxs-lookup"><span data-stu-id="fa1b6-166">IconUrl</span></span> | <span data-ttu-id="fa1b6-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="fa1b6-167">PackageIconUrl</span></span> | <span data-ttu-id="fa1b6-168">vuoto</span><span class="sxs-lookup"><span data-stu-id="fa1b6-168">empty</span></span> | |
| <span data-ttu-id="fa1b6-169">Tag</span><span class="sxs-lookup"><span data-stu-id="fa1b6-169">Tags</span></span> | <span data-ttu-id="fa1b6-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="fa1b6-170">PackageTags</span></span> | <span data-ttu-id="fa1b6-171">vuoto</span><span class="sxs-lookup"><span data-stu-id="fa1b6-171">empty</span></span> | <span data-ttu-id="fa1b6-172">I tag sono delimitati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="fa1b6-173">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="fa1b6-173">ReleaseNotes</span></span> | <span data-ttu-id="fa1b6-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="fa1b6-174">PackageReleaseNotes</span></span> | <span data-ttu-id="fa1b6-175">vuoto</span><span class="sxs-lookup"><span data-stu-id="fa1b6-175">empty</span></span> | |
| <span data-ttu-id="fa1b6-176">Url del repository /</span><span class="sxs-lookup"><span data-stu-id="fa1b6-176">Repository/Url</span></span> | <span data-ttu-id="fa1b6-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="fa1b6-177">RepositoryUrl</span></span> | <span data-ttu-id="fa1b6-178">vuoto</span><span class="sxs-lookup"><span data-stu-id="fa1b6-178">empty</span></span> | <span data-ttu-id="fa1b6-179">URL del repository utilizzata per clonare o recuperare il codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-179">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="fa1b6-180">Esempio: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="fa1b6-180">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="fa1b6-181">Tipo di repository /</span><span class="sxs-lookup"><span data-stu-id="fa1b6-181">Repository/Type</span></span> | <span data-ttu-id="fa1b6-182">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="fa1b6-182">RepositoryType</span></span> | <span data-ttu-id="fa1b6-183">vuoto</span><span class="sxs-lookup"><span data-stu-id="fa1b6-183">empty</span></span> | <span data-ttu-id="fa1b6-184">Tipo di repository.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-184">Repository type.</span></span> <span data-ttu-id="fa1b6-185">Esempi: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-185">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="fa1b6-186">Ramo del repository /</span><span class="sxs-lookup"><span data-stu-id="fa1b6-186">Repository/Branch</span></span> | <span data-ttu-id="fa1b6-187">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="fa1b6-187">RepositoryBranch</span></span> | <span data-ttu-id="fa1b6-188">vuoto</span><span class="sxs-lookup"><span data-stu-id="fa1b6-188">empty</span></span> | <span data-ttu-id="fa1b6-189">Informazioni di ramo del repository facoltativo.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-189">Optional repository branch information.</span></span> <span data-ttu-id="fa1b6-190">*RepositoryUrl* deve anche essere specificato per questa proprietà deve essere incluso.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-190">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="fa1b6-191">Esempio: *master* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="fa1b6-191">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="fa1b6-192">Repository/Commit</span><span class="sxs-lookup"><span data-stu-id="fa1b6-192">Repository/Commit</span></span> | <span data-ttu-id="fa1b6-193">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="fa1b6-193">RepositoryCommit</span></span> | <span data-ttu-id="fa1b6-194">vuoto</span><span class="sxs-lookup"><span data-stu-id="fa1b6-194">empty</span></span> | <span data-ttu-id="fa1b6-195">Commit repository facoltativo o insieme di modifiche per indicare che il pacchetto di origine è stato compilato con.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-195">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="fa1b6-196">*RepositoryUrl* deve anche essere specificato per questa proprietà deve essere incluso.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-196">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="fa1b6-197">Esempio: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="fa1b6-197">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="fa1b6-198">PackageType</span><span class="sxs-lookup"><span data-stu-id="fa1b6-198">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="fa1b6-199">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="fa1b6-199">Summary</span></span> | <span data-ttu-id="fa1b6-200">Non supportato</span><span class="sxs-lookup"><span data-stu-id="fa1b6-200">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="fa1b6-201">Input destinazione pack</span><span class="sxs-lookup"><span data-stu-id="fa1b6-201">pack target inputs</span></span>

- <span data-ttu-id="fa1b6-202">IsPackable</span><span class="sxs-lookup"><span data-stu-id="fa1b6-202">IsPackable</span></span>
- <span data-ttu-id="fa1b6-203">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="fa1b6-203">PackageVersion</span></span>
- <span data-ttu-id="fa1b6-204">PackageId</span><span class="sxs-lookup"><span data-stu-id="fa1b6-204">PackageId</span></span>
- <span data-ttu-id="fa1b6-205">Autori</span><span class="sxs-lookup"><span data-stu-id="fa1b6-205">Authors</span></span>
- <span data-ttu-id="fa1b6-206">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fa1b6-206">Description</span></span>
- <span data-ttu-id="fa1b6-207">Copyright</span><span class="sxs-lookup"><span data-stu-id="fa1b6-207">Copyright</span></span>
- <span data-ttu-id="fa1b6-208">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="fa1b6-208">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="fa1b6-209">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="fa1b6-209">DevelopmentDependency</span></span>
- <span data-ttu-id="fa1b6-210">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="fa1b6-210">PackageLicenseUrl</span></span>
- <span data-ttu-id="fa1b6-211">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="fa1b6-211">PackageProjectUrl</span></span>
- <span data-ttu-id="fa1b6-212">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="fa1b6-212">PackageIconUrl</span></span>
- <span data-ttu-id="fa1b6-213">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="fa1b6-213">PackageReleaseNotes</span></span>
- <span data-ttu-id="fa1b6-214">PackageTags</span><span class="sxs-lookup"><span data-stu-id="fa1b6-214">PackageTags</span></span>
- <span data-ttu-id="fa1b6-215">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="fa1b6-215">PackageOutputPath</span></span>
- <span data-ttu-id="fa1b6-216">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="fa1b6-216">IncludeSymbols</span></span>
- <span data-ttu-id="fa1b6-217">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="fa1b6-217">IncludeSource</span></span>
- <span data-ttu-id="fa1b6-218">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="fa1b6-218">PackageTypes</span></span>
- <span data-ttu-id="fa1b6-219">IsTool</span><span class="sxs-lookup"><span data-stu-id="fa1b6-219">IsTool</span></span>
- <span data-ttu-id="fa1b6-220">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="fa1b6-220">RepositoryUrl</span></span>
- <span data-ttu-id="fa1b6-221">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="fa1b6-221">RepositoryType</span></span>
- <span data-ttu-id="fa1b6-222">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="fa1b6-222">RepositoryBranch</span></span>
- <span data-ttu-id="fa1b6-223">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="fa1b6-223">RepositoryCommit</span></span>
- <span data-ttu-id="fa1b6-224">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="fa1b6-224">NoPackageAnalysis</span></span>
- <span data-ttu-id="fa1b6-225">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="fa1b6-225">MinClientVersion</span></span>
- <span data-ttu-id="fa1b6-226">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="fa1b6-226">IncludeBuildOutput</span></span>
- <span data-ttu-id="fa1b6-227">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="fa1b6-227">IncludeContentInPack</span></span>
- <span data-ttu-id="fa1b6-228">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="fa1b6-228">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="fa1b6-229">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="fa1b6-229">ContentTargetFolders</span></span>
- <span data-ttu-id="fa1b6-230">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="fa1b6-230">NuspecFile</span></span>
- <span data-ttu-id="fa1b6-231">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="fa1b6-231">NuspecBasePath</span></span>
- <span data-ttu-id="fa1b6-232">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="fa1b6-232">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="fa1b6-233">Scenari pack</span><span class="sxs-lookup"><span data-stu-id="fa1b6-233">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="fa1b6-234">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="fa1b6-234">PackageIconUrl</span></span>

<span data-ttu-id="fa1b6-235">Come parte della modifica del [NuGet problema 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` alla fine verrà modificato in `PackageIconUri` e può essere un percorso relativo a un file di icona che verrà incluso nella directory principale del pacchetto risulta.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-235">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="fa1b6-236">Assembly di output</span><span class="sxs-lookup"><span data-stu-id="fa1b6-236">Output assemblies</span></span>

<span data-ttu-id="fa1b6-237">`nuget pack` copia i file di output con le estensioni `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-237">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="fa1b6-238">I file di output copiati dipendono da quanto fornito da MSBuild dalla destinazione `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-238">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="fa1b6-239">Sono disponibili due proprietà di MSBuild che è possibile usare nel file di progetto o nella riga di comando per controllare la destinazione degli assembly di output:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-239">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="fa1b6-240">`IncludeBuildOutput`: valore booleano che determina se gli assembly di output della compilazione devono essere inclusi nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-240">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="fa1b6-241">`BuildOutputTargetFolder`: specifica la cartella in cui devono essere posizionati gli assembly di output.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-241">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="fa1b6-242">Gli assembly di output (e altri file di output) vengono copiati nelle rispettive cartelle per framework.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-242">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="fa1b6-243">Riferimenti ai pacchetti</span><span class="sxs-lookup"><span data-stu-id="fa1b6-243">Package references</span></span>

<span data-ttu-id="fa1b6-244">Vedere [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="fa1b6-244">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="fa1b6-245">Riferimenti da progetto a progetto</span><span class="sxs-lookup"><span data-stu-id="fa1b6-245">Project to project references</span></span>

<span data-ttu-id="fa1b6-246">I riferimenti da progetto a progetto sono considerati per impostazione predefinita come riferimenti a pacchetti NuGet, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-246">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="fa1b6-247">È anche possibile aggiungere i metadati seguenti ai riferimenti del progetto:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-247">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="fa1b6-248">Inclusione di contenuto in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="fa1b6-248">Including content in a package</span></span>

<span data-ttu-id="fa1b6-249">Per includere il contenuto, aggiungere altri metadati all'elemento `<Content>` esistente.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-249">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="fa1b6-250">Per impostazione predefinita tutti gli elementi di tipo"Content" vengono inclusi nel pacchetto, a meno che non si esegua l'override con voci simili al codice seguente:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-250">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="fa1b6-251">Per impostazione predefinita, tutti gli elementi vengono aggiunti alla radice di `content` e della cartella `contentFiles\any\<target_framework>` all'interno di un pacchetto e viene mantenuta la struttura di cartelle relative, a meno che non si specifichi un percorso di pacchetto:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-251">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="fa1b6-252">Se si vuole copiare tutto il contenuto sono in cartelle radice specifiche (invece di copiarlo sia in `content` che in `contentFiles`), è possibile usare la proprietà di MSBuild `ContentTargetFolders`, che ha il valore predefinito "content;contentFiles" ma può essere impostata su qualsiasi altro nome di cartella.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-252">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="fa1b6-253">Si noti che se si specifica solo "contentFiles" in `ContentTargetFolders`, i file vengono posizionati in `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` in base a `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-253">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="fa1b6-254">`PackagePath` può essere un set di percorsi di destinazione delimitati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-254">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="fa1b6-255">Se si specifica un percorso di pacchetto vuoto, il file viene aggiunto alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-255">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="fa1b6-256">Ad esempio, il codice seguente aggiunge `libuv.txt` a `content\myfiles`, `content\samples` e nella radice del pacchetto:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-256">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="fa1b6-257">È disponibile anche una proprietà di MSBuild `$(IncludeContentInPack)`, con valore predefinito `true`.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-257">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="fa1b6-258">Se questa proprietà viene impostata su `false` in qualsiasi progetto, il contenuto da tale progetto non viene incluso nel pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-258">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="fa1b6-259">Altri metadati specifici di pack che è possibile impostare per qualsiasi elemento precedente includono ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, che impostano i valori ```CopyToOutput``` e ```Flatten``` sulla voce ```contentFiles``` nel file nuspec di output.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-259">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="fa1b6-260">Oltre agli elementi Content, i metadati `<Pack>` e `<PackagePath>` possono anche essere impostati nei file con l'azione di compilazione Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o None.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-260">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="fa1b6-261">Per fare in modo che il comando pack aggiunga il nome del file al percorso del pacchetto quando si usano modelli con caratteri jolly (glob), il percorso del pacchetto deve terminare con il carattere separatore di cartella. In caso contrario, il percorso del pacchetto viene interpretato come percorso completo, incluso il nome del file.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-261">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="fa1b6-262">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="fa1b6-262">IncludeSymbols</span></span>

<span data-ttu-id="fa1b6-263">Quando si usa `MSBuild /t:pack /p:IncludeSymbols=true`, i file `.pdb` corrispondenti vengono copiati insieme agli altri file di output (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="fa1b6-263">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="fa1b6-264">Si noti che l'impostazione `IncludeSymbols=true` crea un pacchetto regolare *e* un pacchetto di simboli.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-264">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="fa1b6-265">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="fa1b6-265">IncludeSource</span></span>

<span data-ttu-id="fa1b6-266">Equivale a `IncludeSymbols`, ma insieme ai file `.pdb` vengono copiati anche i file di origine.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-266">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="fa1b6-267">Tutti i file di tipo `Compile` vengono copiati in `src\<ProjectName>\` conservando la struttura di cartelle del percorso relativo nel pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-267">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="fa1b6-268">Lo stesso accade anche per i file di origine di qualsiasi `ProjectReference` con `TreatAsPackageReference` impostato su `false`.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-268">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="fa1b6-269">Se un file di tipo Compile è all'esterno della cartella di progetto, viene semplicemente aggiunto a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-269">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="fa1b6-270">IsTool</span><span class="sxs-lookup"><span data-stu-id="fa1b6-270">IsTool</span></span>

<span data-ttu-id="fa1b6-271">Quando si usa `MSBuild /t:pack /p:IsTool=true`, tutti i file, come specificato nello scenario [Assembly di output](#output-assemblies), vengono copiati nella cartella `tools` invece che nella cartella `lib`.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-271">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="fa1b6-272">Si noti che questo comportamento è diverso da `DotNetCliTool`, che viene specificato impostando `PackageType` nel file `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-272">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="fa1b6-273">Creazione di un pacchetto con un file .nuspec</span><span class="sxs-lookup"><span data-stu-id="fa1b6-273">Packing using a .nuspec</span></span>

<span data-ttu-id="fa1b6-274">È possibile utilizzare un `.nuspec` file per comprimere il progetto, purché si disponga di un file di progetto SDK da importare `NuGet.Build.Tasks.Pack.targets` in modo che l'attività di Service pack può essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-274">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="fa1b6-275">È comunque necessario ripristinare il progetto prima di possibile comprimere un file nuspec.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-275">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="fa1b6-276">Il framework di destinazione del file di progetto è irrilevante e non utilizzata per la compressione di un nuspec.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-276">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="fa1b6-277">Le tre proprietà di MSBuild seguenti sono rilevanti per la creazione di pacchetti con un file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-277">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="fa1b6-278">`NuspecFile`: percorso relativo o assoluto per il file `.nuspec` usato per la creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-278">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="fa1b6-279">`NuspecProperties`: elenco con valori delimitati da punto e virgola di coppie chiave=valore.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-279">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="fa1b6-280">A causa della modalità di funzionamento dell'analisi della riga di comando di MSBuild, è necessario specificare più proprietà come indicato di seguito: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-280">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="fa1b6-281">`NuspecBasePath`: percorso di base per il file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-281">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="fa1b6-282">Se si usa `dotnet.exe` per creare il pacchetto del progetto, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-282">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="fa1b6-283">Se si usa MSBuild per creare il pacchetto del progetto, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-283">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="fa1b6-284">Si noti che un nuspec di compressione utilizzando dotnet.exe o msbuild comporta anche per la compilazione del progetto per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-284">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="fa1b6-285">Questo può essere evitato passando ```--no-build``` dotnet.exe, che equivale all'impostazione della proprietà ```<NoBuild>true</NoBuild> ``` nel file di progetto, insieme a impostazione ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` nel file di progetto</span><span class="sxs-lookup"><span data-stu-id="fa1b6-285">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="fa1b6-286">È un esempio di un file csproj per comprimere un file nuspec.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-286">An example of a csproj file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="fa1b6-287">Advanced punti di estensione per creare pacchetto personalizzato</span><span class="sxs-lookup"><span data-stu-id="fa1b6-287">Advanced extension points to create customized package</span></span>

<span data-ttu-id="fa1b6-288">Il `pack` destinazione fornisce due punti di estensione che eseguono l'interna, compilazione specifica framework di destinazione.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-288">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="fa1b6-289">I punti di estensione supportano inclusi contenuto specifico framework di destinazione e assembly in un pacchetto:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-289">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="fa1b6-290">`TargetsForTfmSpecificBuildOutput` destinazione: usare per i file all'interno di `lib` cartella o una cartella specificata utilizzando `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-290">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="fa1b6-291">`TargetsForTfmSpecificContentInPackage` destinazione: usare per i file all'esterno di `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-291">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="fa1b6-292">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="fa1b6-292">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="fa1b6-293">Scrivere una destinazione personalizzata e specificarlo come valore della `$(TargetsForTfmSpecificBuildOutput)` proprietà.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-293">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="fa1b6-294">Per tutti i file che devono passare nel `BuildOutputTargetFolder` (lib per impostazione predefinita), la destinazione deve scrivere tali file in ItemGroup `BuildOutputInPackage` e impostare i due valori di metadati seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-294">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="fa1b6-295">`FinalOutputPath`: Il percorso assoluto del file. Se omesso, l'identità viene utilizzata per valutare il percorso di origine.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-295">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="fa1b6-296">`TargetPath`: (Facoltativo) impostare quando il file deve essere inviato in una sottocartella all'interno di `lib\<TargetFramework>` , come assembly satellite che vanno sotto le cartelle delle rispettive impostazioni cultura.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-296">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="fa1b6-297">Valore predefinito è il nome del file.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-297">Defaults to the name of the file.</span></span>

<span data-ttu-id="fa1b6-298">Esempio:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-298">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="fa1b6-299">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="fa1b6-299">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="fa1b6-300">Scrivere una destinazione personalizzata e specificarlo come valore della `$(TargetsForTfmSpecificContentInPackage)` proprietà.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-300">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="fa1b6-301">Per tutti i file da includere nel pacchetto, la destinazione deve scrivere tali file in ItemGroup `TfmSpecificPackageFile` e impostare i metadati facoltativi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-301">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="fa1b6-302">`PackagePath`: Percorso in cui il file deve essere l'output del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-302">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="fa1b6-303">NuGet genera un avviso se più di un file viene aggiunto al percorso del pacchetto stesso.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-303">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="fa1b6-304">`BuildAction`: L'azione di compilazione da assegnare al file, è obbligatorio solo se il percorso del pacchetto è nel `contentFiles` cartella.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-304">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="fa1b6-305">Valore predefinito è "None".</span><span class="sxs-lookup"><span data-stu-id="fa1b6-305">Defaults to "None".</span></span>

<span data-ttu-id="fa1b6-306">Un esempio:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-306">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="fa1b6-307">Destinazione restore</span><span class="sxs-lookup"><span data-stu-id="fa1b6-307">restore target</span></span>

<span data-ttu-id="fa1b6-308">`MSBuild /t:restore` (usato da `nuget restore` e `dotnet restore` con progetti .NET Core) consente di ripristinare i pacchetti a cui si fa riferimento nel file di progetto, come segue:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-308">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="fa1b6-309">Lettura di tutti i riferimenti da progetto a progetto</span><span class="sxs-lookup"><span data-stu-id="fa1b6-309">Read all project to project references</span></span>
1. <span data-ttu-id="fa1b6-310">Lettura delle proprietà del progetto per trovare la cartella intermedia e i framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="fa1b6-310">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="fa1b6-311">Passaggio dei dati msbuild a NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="fa1b6-311">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="fa1b6-312">Esecuzione di restore</span><span class="sxs-lookup"><span data-stu-id="fa1b6-312">Run restore</span></span>
1. <span data-ttu-id="fa1b6-313">Download dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="fa1b6-313">Download packages</span></span>
1. <span data-ttu-id="fa1b6-314">Scrittura dei file di asset, delle destinazioni e delle proprietà</span><span class="sxs-lookup"><span data-stu-id="fa1b6-314">Write assets file, targets, and props</span></span>

<span data-ttu-id="fa1b6-315">Il `restore` destinazione works **solo** per i progetti utilizzando il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-315">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="fa1b6-316">Caso **non** funzionano per i progetti utilizzando il `packages.config` formato; utilizzare [ripristino nuget](../tools/cli-ref-restore.md) invece.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-316">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="fa1b6-317">Ripristino delle proprietà</span><span class="sxs-lookup"><span data-stu-id="fa1b6-317">Restore properties</span></span>

<span data-ttu-id="fa1b6-318">Possono esistere ulteriori impostazioni di ripristino derivate da proprietà di MSBuild nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-318">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="fa1b6-319">I valori possono essere impostati anche dalla riga di comando tramite l'opzione `/p:` (vedere gli esempi riportati di seguito).</span><span class="sxs-lookup"><span data-stu-id="fa1b6-319">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="fa1b6-320">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fa1b6-320">Property</span></span> | <span data-ttu-id="fa1b6-321">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fa1b6-321">Description</span></span> |
|--------|--------|
| <span data-ttu-id="fa1b6-322">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="fa1b6-322">RestoreSources</span></span> | <span data-ttu-id="fa1b6-323">Elenco delimitato da punto e virgola delle origini di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-323">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="fa1b6-324">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="fa1b6-324">RestorePackagesPath</span></span> | <span data-ttu-id="fa1b6-325">Percorso della cartella dei pacchetti dell'utente.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-325">User packages folder path.</span></span> |
| <span data-ttu-id="fa1b6-326">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="fa1b6-326">RestoreDisableParallel</span></span> | <span data-ttu-id="fa1b6-327">Consente di limitare i download a uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-327">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="fa1b6-328">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="fa1b6-328">RestoreConfigFile</span></span> | <span data-ttu-id="fa1b6-329">Percorso per un file `Nuget.Config` da applicare.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-329">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="fa1b6-330">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="fa1b6-330">RestoreNoCache</span></span> | <span data-ttu-id="fa1b6-331">Se true, si evita l'uso di pacchetti memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-331">If true, avoids using cached packages.</span></span> <span data-ttu-id="fa1b6-332">Vedere [gestione dei pacchetti globali e alla cartella della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="fa1b6-332">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="fa1b6-333">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="fa1b6-333">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="fa1b6-334">Se true, ignora le origini di pacchetti in errore o mancanti.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-334">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="fa1b6-335">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="fa1b6-335">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="fa1b6-336">Percorso di `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-336">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="fa1b6-337">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="fa1b6-337">RestoreGraphProjectInput</span></span> | <span data-ttu-id="fa1b6-338">Elenco delimitato da punto e virgola dei progetti da ripristinare, che deve contenere percorsi assoluti.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-338">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="fa1b6-339">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="fa1b6-339">RestoreOutputPath</span></span> | <span data-ttu-id="fa1b6-340">Cartella di output. Per impostazione predefinita, la cartella `obj`.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-340">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="fa1b6-341">Esempi</span><span class="sxs-lookup"><span data-stu-id="fa1b6-341">Examples</span></span>

<span data-ttu-id="fa1b6-342">Riga di comando:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-342">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="fa1b6-343">File di progetto:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-343">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="fa1b6-344">Output del ripristino</span><span class="sxs-lookup"><span data-stu-id="fa1b6-344">Restore outputs</span></span>

<span data-ttu-id="fa1b6-345">Il ripristino crea i file seguenti nella cartella `obj` di compilazione:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-345">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="fa1b6-346">File</span><span class="sxs-lookup"><span data-stu-id="fa1b6-346">File</span></span> | <span data-ttu-id="fa1b6-347">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fa1b6-347">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="fa1b6-348">Contiene il grafico delle dipendenze di tutti i riferimenti di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-348">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="fa1b6-349">Riferimenti alle proprietà di MSBuild contenute nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="fa1b6-349">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="fa1b6-350">Riferimenti alle destinazioni di MSBuild contenute nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="fa1b6-350">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="fa1b6-351">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="fa1b6-351">PackageTargetFallback</span></span>

<span data-ttu-id="fa1b6-352">L'elemento `PackageTargetFallback` consente di specificare un set di destinazioni compatibili da usare durante il ripristino di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-352">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="fa1b6-353">È progettato per consentire ai pacchetti che usano un [TxM](../reference/target-frameworks.md) dotnet di interagire con pacchetti compatibili che non dichiarano un TxM dotnet.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-353">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="fa1b6-354">Se il progetto usa il TxM dotnet, devono averlo anche tutti i pacchetti da cui il progetto dipende, a meno che non si aggiunga `<PackageTargetFallback>` al progetto, in modo da rendere compatibili con dotnet le piattaforme che non lo sono.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-354">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="fa1b6-355">Ad esempio, se il progetto usa il TxM `netstandard1.6` e un pacchetto dipendente contiene solo `lib/net45/a.dll` e `lib/portable-net45+win81/a.dll`, la compilazione del progetto avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-355">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="fa1b6-356">Se si vuole includere solo quest'ultima DLL, è possibile aggiungere un `PackageTargetFallback` come segue per segnalare che la DLL `portable-net45+win81` è compatibile:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-356">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="fa1b6-357">Per dichiarare un fallback per tutte le destinazioni nel progetto, non specificare l'attributo `Condition`.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-357">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="fa1b6-358">È anche possibile estendere qualsiasi `PackageTargetFallback` esistente includendo `$(PackageTargetFallback)` come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-358">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="fa1b6-359">Sostituzione di una libreria da un grafico di ripristino</span><span class="sxs-lookup"><span data-stu-id="fa1b6-359">Replacing one library from a restore graph</span></span>

<span data-ttu-id="fa1b6-360">Se un ripristino restituisce l'assembly errato, è possibile escludere la scelta predefinita di tali pacchetti e sostituirla con la propria scelta.</span><span class="sxs-lookup"><span data-stu-id="fa1b6-360">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="fa1b6-361">Prima di tutto, con un `PackageReference` di livello superiore, escludere tutti gli asset:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-361">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="fa1b6-362">Aggiungere quindi il riferimento personalizzato alla copia locale appropriata della DLL:</span><span class="sxs-lookup"><span data-stu-id="fa1b6-362">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
