---
title: Pack e restore di NuGet come destinazioni MSBuild
description: I comandi pack e restore di NuGet possono essere usati direttamente come destinazioni MSBuild con NuGet 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 8403ae38b5d2e907c6f06b162a18cdcd5425565b
ms.sourcegitcommit: 5aa49478dc466c67db5c3edda7c6ce8dcd8ae033
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/06/2019
ms.locfileid: "68817530"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="05a8e-103">Pack e restore di NuGet come destinazioni MSBuild</span><span class="sxs-lookup"><span data-stu-id="05a8e-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="05a8e-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="05a8e-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="05a8e-105">Con il formato [PackageReference](../consume-packages/package-references-in-project-files.md) , NuGet 4.0 + può archiviare tutti i metadati del manifesto direttamente all'interno di un file di progetto `.nuspec` anziché usare un file separato.</span><span class="sxs-lookup"><span data-stu-id="05a8e-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="05a8e-106">Con MSBuild 15.1 +, anche NuGet è un membro di MSBuild di prima classe con le destinazioni `pack` e `restore` come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="05a8e-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="05a8e-107">Queste destinazioni consentono di usare NuGet come qualsiasi altra attività o destinazione MSBuild.</span><span class="sxs-lookup"><span data-stu-id="05a8e-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="05a8e-108">Per istruzioni sulla creazione di un pacchetto NuGet con MSBuild, vedere [creare un pacchetto NuGet con MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="05a8e-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="05a8e-109">Per NuGet 3.x e versioni precedenti, usare invece i comandi [pack](../reference/cli-reference/cli-ref-pack.md) e [restore](../reference/cli-reference/cli-ref-restore.md) tramite l'interfaccia della riga di comando di NuGet.</span><span class="sxs-lookup"><span data-stu-id="05a8e-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="05a8e-110">Ordine di compilazione delle destinazioni</span><span class="sxs-lookup"><span data-stu-id="05a8e-110">Target build order</span></span>

<span data-ttu-id="05a8e-111">Dato che `pack` e `restore` sono destinazioni MSBuild, è possibile accedervi per ottimizzare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="05a8e-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="05a8e-112">Si supponga, ad esempio, di voler copiare il pacchetto in una condivisione di rete dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="05a8e-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="05a8e-113">È possibile farlo aggiungendo quanto segue nel file di progetto:</span><span class="sxs-lookup"><span data-stu-id="05a8e-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="05a8e-114">Analogamente, è possibile scrivere un'attività MSBuild, scrivere la propria destinazione e utilizzare proprietà NuGet nell'attività MSBuild.</span><span class="sxs-lookup"><span data-stu-id="05a8e-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="05a8e-115">Destinazione pack</span><span class="sxs-lookup"><span data-stu-id="05a8e-115">pack target</span></span>

<span data-ttu-id="05a8e-116">Per .NET standard progetti che usano il formato PackageReference, `msbuild -t:pack` l'uso di disegna gli input dal file di progetto da usare per la creazione di un pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="05a8e-116">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="05a8e-117">La tabella seguente descrive le proprietà di MSBuild che possono essere aggiunte a un file di progetto all'interno del primo nodo `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="05a8e-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="05a8e-118">È possibile apportare facilmente queste modifiche in Visual Studio 2017 e versioni successive facendo clic con il pulsante destro del mouse sul progetto e scegliendo **Modifica {nome_progetto}** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="05a8e-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="05a8e-119">Per praticità, la tabella è organizzata in base alla proprietà equivalente in un [file `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="05a8e-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="05a8e-120">Si noti che le proprietà `Owners` e `Summary` da `.nuspec` non sono supportate con MSBuild.</span><span class="sxs-lookup"><span data-stu-id="05a8e-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="05a8e-121">Valore di attributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="05a8e-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="05a8e-122">Proprietà MSBuild</span><span class="sxs-lookup"><span data-stu-id="05a8e-122">MSBuild Property</span></span> | <span data-ttu-id="05a8e-123">Predefinito</span><span class="sxs-lookup"><span data-stu-id="05a8e-123">Default</span></span> | <span data-ttu-id="05a8e-124">Note</span><span class="sxs-lookup"><span data-stu-id="05a8e-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="05a8e-125">ID</span><span class="sxs-lookup"><span data-stu-id="05a8e-125">Id</span></span> | <span data-ttu-id="05a8e-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="05a8e-126">PackageId</span></span> | <span data-ttu-id="05a8e-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="05a8e-127">AssemblyName</span></span> | <span data-ttu-id="05a8e-128">$(AssemblyName) da MSBuild</span><span class="sxs-lookup"><span data-stu-id="05a8e-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="05a8e-129">Version</span><span class="sxs-lookup"><span data-stu-id="05a8e-129">Version</span></span> | <span data-ttu-id="05a8e-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="05a8e-130">PackageVersion</span></span> | <span data-ttu-id="05a8e-131">Version</span><span class="sxs-lookup"><span data-stu-id="05a8e-131">Version</span></span> | <span data-ttu-id="05a8e-132">Compatibile con SemVer, ad esempio "1.0.0", "1.0.0-beta" o "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="05a8e-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="05a8e-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="05a8e-133">VersionPrefix</span></span> | <span data-ttu-id="05a8e-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="05a8e-134">PackageVersionPrefix</span></span> | <span data-ttu-id="05a8e-135">vuoto</span><span class="sxs-lookup"><span data-stu-id="05a8e-135">empty</span></span> | <span data-ttu-id="05a8e-136">L'impostazione di PackageVersion sovrascrive PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="05a8e-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="05a8e-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="05a8e-137">VersionSuffix</span></span> | <span data-ttu-id="05a8e-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="05a8e-138">PackageVersionSuffix</span></span> | <span data-ttu-id="05a8e-139">vuoto</span><span class="sxs-lookup"><span data-stu-id="05a8e-139">empty</span></span> | <span data-ttu-id="05a8e-140">$(VersionSuffix) da MSBuild.</span><span class="sxs-lookup"><span data-stu-id="05a8e-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="05a8e-141">L'impostazione di PackageVersion sovrascrive PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="05a8e-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="05a8e-142">Autori</span><span class="sxs-lookup"><span data-stu-id="05a8e-142">Authors</span></span> | <span data-ttu-id="05a8e-143">Autori</span><span class="sxs-lookup"><span data-stu-id="05a8e-143">Authors</span></span> | <span data-ttu-id="05a8e-144">Nome utente dell'utente corrente</span><span class="sxs-lookup"><span data-stu-id="05a8e-144">Username of the current user</span></span> | |
| <span data-ttu-id="05a8e-145">Proprietari</span><span class="sxs-lookup"><span data-stu-id="05a8e-145">Owners</span></span> | <span data-ttu-id="05a8e-146">N/D</span><span class="sxs-lookup"><span data-stu-id="05a8e-146">N/A</span></span> | <span data-ttu-id="05a8e-147">Non presente in NuSpec</span><span class="sxs-lookup"><span data-stu-id="05a8e-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="05a8e-148">Titolo</span><span class="sxs-lookup"><span data-stu-id="05a8e-148">Title</span></span> | <span data-ttu-id="05a8e-149">Titolo</span><span class="sxs-lookup"><span data-stu-id="05a8e-149">Title</span></span> | <span data-ttu-id="05a8e-150">PackageId</span><span class="sxs-lookup"><span data-stu-id="05a8e-150">The PackageId</span></span>| |
| <span data-ttu-id="05a8e-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="05a8e-151">Description</span></span> | <span data-ttu-id="05a8e-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="05a8e-152">Description</span></span> | <span data-ttu-id="05a8e-153">"Descrizione del pacchetto"</span><span class="sxs-lookup"><span data-stu-id="05a8e-153">"Package Description"</span></span> | |
| <span data-ttu-id="05a8e-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="05a8e-154">Copyright</span></span> | <span data-ttu-id="05a8e-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="05a8e-155">Copyright</span></span> | <span data-ttu-id="05a8e-156">vuoto</span><span class="sxs-lookup"><span data-stu-id="05a8e-156">empty</span></span> | |
| <span data-ttu-id="05a8e-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="05a8e-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="05a8e-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="05a8e-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="05a8e-159">false</span><span class="sxs-lookup"><span data-stu-id="05a8e-159">false</span></span> | |
| <span data-ttu-id="05a8e-160">licenza</span><span class="sxs-lookup"><span data-stu-id="05a8e-160">license</span></span> | <span data-ttu-id="05a8e-161">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="05a8e-161">PackageLicenseExpression</span></span> | <span data-ttu-id="05a8e-162">vuoto</span><span class="sxs-lookup"><span data-stu-id="05a8e-162">empty</span></span> | <span data-ttu-id="05a8e-163">Corrisponde a`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="05a8e-163">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="05a8e-164">licenza</span><span class="sxs-lookup"><span data-stu-id="05a8e-164">license</span></span> | <span data-ttu-id="05a8e-165">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="05a8e-165">PackageLicenseFile</span></span> | <span data-ttu-id="05a8e-166">vuoto</span><span class="sxs-lookup"><span data-stu-id="05a8e-166">empty</span></span> | <span data-ttu-id="05a8e-167">Corrisponde a `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="05a8e-167">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="05a8e-168">Potrebbe essere necessario comprimere in modo esplicito il file di licenza a cui si fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="05a8e-168">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="05a8e-169">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="05a8e-169">LicenseUrl</span></span> | <span data-ttu-id="05a8e-170">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="05a8e-170">PackageLicenseUrl</span></span> | <span data-ttu-id="05a8e-171">vuoto</span><span class="sxs-lookup"><span data-stu-id="05a8e-171">empty</span></span> | <span data-ttu-id="05a8e-172">`licenseUrl`verrà deprecato, utilizzare la proprietà PackageLicenseExpression o PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="05a8e-172">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="05a8e-173">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="05a8e-173">ProjectUrl</span></span> | <span data-ttu-id="05a8e-174">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="05a8e-174">PackageProjectUrl</span></span> | <span data-ttu-id="05a8e-175">vuoto</span><span class="sxs-lookup"><span data-stu-id="05a8e-175">empty</span></span> | |
| <span data-ttu-id="05a8e-176">IconUrl</span><span class="sxs-lookup"><span data-stu-id="05a8e-176">IconUrl</span></span> | <span data-ttu-id="05a8e-177">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="05a8e-177">PackageIconUrl</span></span> | <span data-ttu-id="05a8e-178">vuoto</span><span class="sxs-lookup"><span data-stu-id="05a8e-178">empty</span></span> | |
| <span data-ttu-id="05a8e-179">Tag</span><span class="sxs-lookup"><span data-stu-id="05a8e-179">Tags</span></span> | <span data-ttu-id="05a8e-180">PackageTags</span><span class="sxs-lookup"><span data-stu-id="05a8e-180">PackageTags</span></span> | <span data-ttu-id="05a8e-181">vuoto</span><span class="sxs-lookup"><span data-stu-id="05a8e-181">empty</span></span> | <span data-ttu-id="05a8e-182">I tag sono delimitati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="05a8e-182">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="05a8e-183">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="05a8e-183">ReleaseNotes</span></span> | <span data-ttu-id="05a8e-184">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="05a8e-184">PackageReleaseNotes</span></span> | <span data-ttu-id="05a8e-185">vuoto</span><span class="sxs-lookup"><span data-stu-id="05a8e-185">empty</span></span> | |
| <span data-ttu-id="05a8e-186">Repository/URL</span><span class="sxs-lookup"><span data-stu-id="05a8e-186">Repository/Url</span></span> | <span data-ttu-id="05a8e-187">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="05a8e-187">RepositoryUrl</span></span> | <span data-ttu-id="05a8e-188">vuoto</span><span class="sxs-lookup"><span data-stu-id="05a8e-188">empty</span></span> | <span data-ttu-id="05a8e-189">URL del repository usato per clonare o recuperare il codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="05a8e-189">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="05a8e-190">Esempio *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="05a8e-190">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="05a8e-191">Repository/tipo</span><span class="sxs-lookup"><span data-stu-id="05a8e-191">Repository/Type</span></span> | <span data-ttu-id="05a8e-192">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="05a8e-192">RepositoryType</span></span> | <span data-ttu-id="05a8e-193">vuoto</span><span class="sxs-lookup"><span data-stu-id="05a8e-193">empty</span></span> | <span data-ttu-id="05a8e-194">Tipo di repository.</span><span class="sxs-lookup"><span data-stu-id="05a8e-194">Repository type.</span></span> <span data-ttu-id="05a8e-195">Esempi: *git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="05a8e-195">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="05a8e-196">Repository/ramo</span><span class="sxs-lookup"><span data-stu-id="05a8e-196">Repository/Branch</span></span> | <span data-ttu-id="05a8e-197">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="05a8e-197">RepositoryBranch</span></span> | <span data-ttu-id="05a8e-198">vuoto</span><span class="sxs-lookup"><span data-stu-id="05a8e-198">empty</span></span> | <span data-ttu-id="05a8e-199">Informazioni facoltative sul ramo del repository.</span><span class="sxs-lookup"><span data-stu-id="05a8e-199">Optional repository branch information.</span></span> <span data-ttu-id="05a8e-200">Per includere questa proprietà, è necessario specificare anche *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="05a8e-200">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="05a8e-201">Esempio: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="05a8e-201">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="05a8e-202">Repository/commit</span><span class="sxs-lookup"><span data-stu-id="05a8e-202">Repository/Commit</span></span> | <span data-ttu-id="05a8e-203">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="05a8e-203">RepositoryCommit</span></span> | <span data-ttu-id="05a8e-204">vuoto</span><span class="sxs-lookup"><span data-stu-id="05a8e-204">empty</span></span> | <span data-ttu-id="05a8e-205">Commit o insieme di modifiche facoltativo del repository per indicare l'origine su cui è stato compilato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="05a8e-205">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="05a8e-206">Per includere questa proprietà, è necessario specificare anche *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="05a8e-206">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="05a8e-207">Esempio: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="05a8e-207">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="05a8e-208">PackageType</span><span class="sxs-lookup"><span data-stu-id="05a8e-208">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="05a8e-209">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="05a8e-209">Summary</span></span> | <span data-ttu-id="05a8e-210">Non supportate</span><span class="sxs-lookup"><span data-stu-id="05a8e-210">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="05a8e-211">Input destinazione pack</span><span class="sxs-lookup"><span data-stu-id="05a8e-211">pack target inputs</span></span>

- <span data-ttu-id="05a8e-212">IsPackable</span><span class="sxs-lookup"><span data-stu-id="05a8e-212">IsPackable</span></span>
- <span data-ttu-id="05a8e-213">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="05a8e-213">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="05a8e-214">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="05a8e-214">PackageVersion</span></span>
- <span data-ttu-id="05a8e-215">PackageId</span><span class="sxs-lookup"><span data-stu-id="05a8e-215">PackageId</span></span>
- <span data-ttu-id="05a8e-216">Autori</span><span class="sxs-lookup"><span data-stu-id="05a8e-216">Authors</span></span>
- <span data-ttu-id="05a8e-217">Descrizione</span><span class="sxs-lookup"><span data-stu-id="05a8e-217">Description</span></span>
- <span data-ttu-id="05a8e-218">Copyright</span><span class="sxs-lookup"><span data-stu-id="05a8e-218">Copyright</span></span>
- <span data-ttu-id="05a8e-219">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="05a8e-219">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="05a8e-220">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="05a8e-220">DevelopmentDependency</span></span>
- <span data-ttu-id="05a8e-221">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="05a8e-221">PackageLicenseExpression</span></span>
- <span data-ttu-id="05a8e-222">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="05a8e-222">PackageLicenseFile</span></span>
- <span data-ttu-id="05a8e-223">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="05a8e-223">PackageLicenseUrl</span></span>
- <span data-ttu-id="05a8e-224">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="05a8e-224">PackageProjectUrl</span></span>
- <span data-ttu-id="05a8e-225">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="05a8e-225">PackageIconUrl</span></span>
- <span data-ttu-id="05a8e-226">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="05a8e-226">PackageReleaseNotes</span></span>
- <span data-ttu-id="05a8e-227">PackageTags</span><span class="sxs-lookup"><span data-stu-id="05a8e-227">PackageTags</span></span>
- <span data-ttu-id="05a8e-228">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="05a8e-228">PackageOutputPath</span></span>
- <span data-ttu-id="05a8e-229">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="05a8e-229">IncludeSymbols</span></span>
- <span data-ttu-id="05a8e-230">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="05a8e-230">IncludeSource</span></span>
- <span data-ttu-id="05a8e-231">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="05a8e-231">PackageTypes</span></span>
- <span data-ttu-id="05a8e-232">IsTool</span><span class="sxs-lookup"><span data-stu-id="05a8e-232">IsTool</span></span>
- <span data-ttu-id="05a8e-233">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="05a8e-233">RepositoryUrl</span></span>
- <span data-ttu-id="05a8e-234">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="05a8e-234">RepositoryType</span></span>
- <span data-ttu-id="05a8e-235">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="05a8e-235">RepositoryBranch</span></span>
- <span data-ttu-id="05a8e-236">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="05a8e-236">RepositoryCommit</span></span>
- <span data-ttu-id="05a8e-237">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="05a8e-237">NoPackageAnalysis</span></span>
- <span data-ttu-id="05a8e-238">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="05a8e-238">MinClientVersion</span></span>
- <span data-ttu-id="05a8e-239">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="05a8e-239">IncludeBuildOutput</span></span>
- <span data-ttu-id="05a8e-240">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="05a8e-240">IncludeContentInPack</span></span>
- <span data-ttu-id="05a8e-241">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="05a8e-241">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="05a8e-242">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="05a8e-242">ContentTargetFolders</span></span>
- <span data-ttu-id="05a8e-243">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="05a8e-243">NuspecFile</span></span>
- <span data-ttu-id="05a8e-244">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="05a8e-244">NuspecBasePath</span></span>
- <span data-ttu-id="05a8e-245">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="05a8e-245">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="05a8e-246">Scenari pack</span><span class="sxs-lookup"><span data-stu-id="05a8e-246">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="05a8e-247">Non visualizzare le dipendenze</span><span class="sxs-lookup"><span data-stu-id="05a8e-247">Suppress dependencies</span></span>

<span data-ttu-id="05a8e-248">Per non visualizzare le dipendenze del pacchetto dal pacchetto `SuppressDependenciesWhenPacking` NuGet `true` generato, impostare su che consentirà di ignorare tutte le dipendenze dal file nupkg generato.</span><span class="sxs-lookup"><span data-stu-id="05a8e-248">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="05a8e-249">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="05a8e-249">PackageIconUrl</span></span>

<span data-ttu-id="05a8e-250">Come parte della modifica del [problema NuGet 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` verrà modificato in `PackageIconUri` e può essere il percorso relativo di un file di icona che verrà incluso alla radice del pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="05a8e-250">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="05a8e-251">Assembly di output</span><span class="sxs-lookup"><span data-stu-id="05a8e-251">Output assemblies</span></span>

<span data-ttu-id="05a8e-252">`nuget pack` copia i file di output con le estensioni `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="05a8e-252">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="05a8e-253">I file di output copiati dipendono da quanto fornito da MSBuild dalla destinazione `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="05a8e-253">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="05a8e-254">Sono disponibili due proprietà di MSBuild che è possibile usare nel file di progetto o nella riga di comando per controllare la destinazione degli assembly di output:</span><span class="sxs-lookup"><span data-stu-id="05a8e-254">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="05a8e-255">`IncludeBuildOutput`: Valore booleano che determina se gli assembly di output della compilazione devono essere inclusi nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="05a8e-255">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="05a8e-256">`BuildOutputTargetFolder`: Specifica la cartella in cui devono essere inseriti gli assembly di output.</span><span class="sxs-lookup"><span data-stu-id="05a8e-256">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="05a8e-257">Gli assembly di output (e altri file di output) vengono copiati nelle rispettive cartelle per framework.</span><span class="sxs-lookup"><span data-stu-id="05a8e-257">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="05a8e-258">Riferimenti ai pacchetti</span><span class="sxs-lookup"><span data-stu-id="05a8e-258">Package references</span></span>

<span data-ttu-id="05a8e-259">Vedere [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="05a8e-259">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="05a8e-260">Riferimenti da progetto a progetto</span><span class="sxs-lookup"><span data-stu-id="05a8e-260">Project to project references</span></span>

<span data-ttu-id="05a8e-261">I riferimenti da progetto a progetto sono considerati per impostazione predefinita come riferimenti a pacchetti NuGet, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="05a8e-261">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="05a8e-262">È anche possibile aggiungere i metadati seguenti ai riferimenti del progetto:</span><span class="sxs-lookup"><span data-stu-id="05a8e-262">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="05a8e-263">Inclusione di contenuto in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="05a8e-263">Including content in a package</span></span>

<span data-ttu-id="05a8e-264">Per includere il contenuto, aggiungere altri metadati all'elemento `<Content>` esistente.</span><span class="sxs-lookup"><span data-stu-id="05a8e-264">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="05a8e-265">Per impostazione predefinita tutti gli elementi di tipo"Content" vengono inclusi nel pacchetto, a meno che non si esegua l'override con voci simili al codice seguente:</span><span class="sxs-lookup"><span data-stu-id="05a8e-265">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="05a8e-266">Per impostazione predefinita, tutti gli elementi vengono aggiunti alla radice di `content` e della cartella `contentFiles\any\<target_framework>` all'interno di un pacchetto e viene mantenuta la struttura di cartelle relative, a meno che non si specifichi un percorso di pacchetto:</span><span class="sxs-lookup"><span data-stu-id="05a8e-266">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="05a8e-267">Se si vuole copiare tutto il contenuto sono in cartelle radice specifiche (invece di copiarlo sia in `content` che in `contentFiles`), è possibile usare la proprietà di MSBuild `ContentTargetFolders`, che ha il valore predefinito "content;contentFiles" ma può essere impostata su qualsiasi altro nome di cartella.</span><span class="sxs-lookup"><span data-stu-id="05a8e-267">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="05a8e-268">Si noti che se si specifica solo "contentFiles" in `ContentTargetFolders`, i file vengono posizionati in `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` in base a `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="05a8e-268">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="05a8e-269">`PackagePath` può essere un set di percorsi di destinazione delimitati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="05a8e-269">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="05a8e-270">Se si specifica un percorso di pacchetto vuoto, il file viene aggiunto alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="05a8e-270">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="05a8e-271">Ad esempio, il codice seguente aggiunge `libuv.txt` a `content\myfiles`, `content\samples` e nella radice del pacchetto:</span><span class="sxs-lookup"><span data-stu-id="05a8e-271">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="05a8e-272">È disponibile anche una proprietà di MSBuild `$(IncludeContentInPack)`, con valore predefinito `true`.</span><span class="sxs-lookup"><span data-stu-id="05a8e-272">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="05a8e-273">Se questa proprietà viene impostata su `false` in qualsiasi progetto, il contenuto da tale progetto non viene incluso nel pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="05a8e-273">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="05a8e-274">Altri metadati specifici di pack che è possibile impostare per qualsiasi elemento precedente includono ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, che impostano i valori ```CopyToOutput``` e ```Flatten``` sulla voce ```contentFiles``` nel file nuspec di output.</span><span class="sxs-lookup"><span data-stu-id="05a8e-274">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="05a8e-275">Oltre agli elementi Content, i metadati `<Pack>` e `<PackagePath>` possono anche essere impostati nei file con l'azione di compilazione Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o None.</span><span class="sxs-lookup"><span data-stu-id="05a8e-275">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="05a8e-276">Per fare in modo che il comando pack aggiunga il nome del file al percorso del pacchetto quando si usano modelli con caratteri jolly (glob), il percorso del pacchetto deve terminare con il carattere separatore di cartella. In caso contrario, il percorso del pacchetto viene interpretato come percorso completo, incluso il nome del file.</span><span class="sxs-lookup"><span data-stu-id="05a8e-276">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="05a8e-277">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="05a8e-277">IncludeSymbols</span></span>

<span data-ttu-id="05a8e-278">Quando si usa `MSBuild -t:pack -p:IncludeSymbols=true`, i file `.pdb` corrispondenti vengono copiati insieme agli altri file di output (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="05a8e-278">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="05a8e-279">Si noti che l'impostazione `IncludeSymbols=true` crea un pacchetto regolare *e* un pacchetto di simboli.</span><span class="sxs-lookup"><span data-stu-id="05a8e-279">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="05a8e-280">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="05a8e-280">IncludeSource</span></span>

<span data-ttu-id="05a8e-281">Equivale a `IncludeSymbols`, ma insieme ai file `.pdb` vengono copiati anche i file di origine.</span><span class="sxs-lookup"><span data-stu-id="05a8e-281">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="05a8e-282">Tutti i file di tipo `Compile` vengono copiati in `src\<ProjectName>\` conservando la struttura di cartelle del percorso relativo nel pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="05a8e-282">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="05a8e-283">Lo stesso accade anche per i file di origine di qualsiasi `ProjectReference` con `TreatAsPackageReference` impostato su `false`.</span><span class="sxs-lookup"><span data-stu-id="05a8e-283">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="05a8e-284">Se un file di tipo Compile è all'esterno della cartella di progetto, viene semplicemente aggiunto a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="05a8e-284">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="05a8e-285">Compressione di un'espressione di licenza o di un file di licenza</span><span class="sxs-lookup"><span data-stu-id="05a8e-285">Packing a license expression or a license file</span></span>

<span data-ttu-id="05a8e-286">Quando si usa un'espressione di licenza, è necessario usare la proprietà PackageLicenseExpression.</span><span class="sxs-lookup"><span data-stu-id="05a8e-286">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="05a8e-287">[Esempio di espressione di licenza](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="05a8e-287">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="05a8e-288">[Altre informazioni sulle espressioni di licenza e le licenze accettate da NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="05a8e-288">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="05a8e-289">Quando si imballa un file di licenza, è necessario utilizzare la proprietà PackageLicenseFile per specificare il percorso del pacchetto, relativo alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="05a8e-289">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="05a8e-290">Inoltre, è necessario assicurarsi che il file sia incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="05a8e-290">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="05a8e-291">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="05a8e-291">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="05a8e-292">[Esempio di file di licenza](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="05a8e-292">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="05a8e-293">IsTool</span><span class="sxs-lookup"><span data-stu-id="05a8e-293">IsTool</span></span>

<span data-ttu-id="05a8e-294">Quando si usa `MSBuild -t:pack -p:IsTool=true`, tutti i file, come specificato nello scenario [Assembly di output](#output-assemblies), vengono copiati nella cartella `tools` invece che nella cartella `lib`.</span><span class="sxs-lookup"><span data-stu-id="05a8e-294">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="05a8e-295">Si noti che questo comportamento è diverso da `DotNetCliTool`, che viene specificato impostando `PackageType` nel file `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="05a8e-295">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="05a8e-296">Creazione di un pacchetto con un file .nuspec</span><span class="sxs-lookup"><span data-stu-id="05a8e-296">Packing using a .nuspec</span></span>

<span data-ttu-id="05a8e-297">Sebbene sia consigliabile includere in alternativa [tutte le proprietà](../reference/msbuild-targets.md#pack-target) che in genere si trovano nel `.nuspec` file del progetto, è possibile scegliere di utilizzare un `.nuspec` file per comprimere il progetto.</span><span class="sxs-lookup"><span data-stu-id="05a8e-297">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="05a8e-298">Per un progetto non di tipo SDK che utilizza `PackageReference`, è necessario importare `NuGet.Build.Tasks.Pack.targets` in modo che l'attività Pack possa essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="05a8e-298">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="05a8e-299">Prima di poter comprimere un file nuspec, è ancora necessario ripristinare il progetto.</span><span class="sxs-lookup"><span data-stu-id="05a8e-299">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="05a8e-300">Un progetto di tipo SDK include le destinazioni di tipo pack per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="05a8e-300">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="05a8e-301">Il Framework di destinazione del file di progetto non è rilevante e non viene usato per la compressione di un NuSpec.</span><span class="sxs-lookup"><span data-stu-id="05a8e-301">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="05a8e-302">Le tre proprietà di MSBuild seguenti sono rilevanti per la creazione di pacchetti con un file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="05a8e-302">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="05a8e-303">`NuspecFile`: percorso relativo o assoluto per il file `.nuspec` usato per la creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="05a8e-303">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="05a8e-304">`NuspecProperties`: elenco con valori delimitati da punto e virgola di coppie chiave=valore.</span><span class="sxs-lookup"><span data-stu-id="05a8e-304">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="05a8e-305">A causa della modalità di funzionamento dell'analisi della riga di comando di MSBuild, è necessario specificare più proprietà come indicato di seguito: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="05a8e-305">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="05a8e-306">`NuspecBasePath`: Percorso di base del `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="05a8e-306">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="05a8e-307">Se si usa `dotnet.exe` per creare il pacchetto del progetto, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="05a8e-307">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="05a8e-308">Se si usa MSBuild per creare il pacchetto del progetto, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="05a8e-308">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="05a8e-309">Si noti che la compressione di un NuSpec con dotnet. exe o MSBuild comporta anche la compilazione del progetto per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="05a8e-309">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="05a8e-310">Questa operazione può essere evitata ```--no-build``` passando la proprietà a dotnet. exe, che è l'equivalente ```<NoBuild>true</NoBuild> ``` dell'impostazione nel file di progetto, insieme ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` all'impostazione nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="05a8e-310">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="05a8e-311">Un esempio di file con estensione *csproj* per la compressione di un file nuspec è:</span><span class="sxs-lookup"><span data-stu-id="05a8e-311">An example of a *.csproj* file to pack a nuspec file is:</span></span>

```xml
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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="05a8e-312">Punti di estensione avanzati per la creazione di pacchetti personalizzati</span><span class="sxs-lookup"><span data-stu-id="05a8e-312">Advanced extension points to create customized package</span></span>

<span data-ttu-id="05a8e-313">La `pack` destinazione fornisce due punti di estensione che vengono eseguiti nella compilazione specifica del Framework di destinazione interno.</span><span class="sxs-lookup"><span data-stu-id="05a8e-313">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="05a8e-314">I punti di estensione supportano l'inclusione di contenuto e assembly specifici del Framework di destinazione in un pacchetto:</span><span class="sxs-lookup"><span data-stu-id="05a8e-314">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="05a8e-315">`TargetsForTfmSpecificBuildOutput`destinazione Utilizzare per i file all' `lib` interno della cartella o in una `BuildOutputTargetFolder`cartella specificata utilizzando.</span><span class="sxs-lookup"><span data-stu-id="05a8e-315">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="05a8e-316">`TargetsForTfmSpecificContentInPackage`destinazione Utilizzare per i file all' `BuildOutputTargetFolder`esterno di.</span><span class="sxs-lookup"><span data-stu-id="05a8e-316">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="05a8e-317">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="05a8e-317">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="05a8e-318">Scrivere una destinazione personalizzata e specificarla come valore della `$(TargetsForTfmSpecificBuildOutput)` proprietà.</span><span class="sxs-lookup"><span data-stu-id="05a8e-318">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="05a8e-319">Per tutti i file che devono essere inseriti in `BuildOutputTargetFolder` (per impostazione predefinita, lib), la destinazione deve scrivere i file in `BuildOutputInPackage` ItemGroup e impostare i due valori di metadati seguenti:</span><span class="sxs-lookup"><span data-stu-id="05a8e-319">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="05a8e-320">`FinalOutputPath`: Percorso assoluto del file; Se non viene specificato, l'identità viene utilizzata per valutare il percorso di origine.</span><span class="sxs-lookup"><span data-stu-id="05a8e-320">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="05a8e-321">`TargetPath`:  Opzionale Impostare quando il file deve essere inserito in una sottocartella all' `lib\<TargetFramework>` interno di, ad esempio gli assembly satellite che passano sotto le rispettive cartelle delle impostazioni cultura.</span><span class="sxs-lookup"><span data-stu-id="05a8e-321">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="05a8e-322">Il valore predefinito è il nome del file.</span><span class="sxs-lookup"><span data-stu-id="05a8e-322">Defaults to the name of the file.</span></span>

<span data-ttu-id="05a8e-323">Esempio:</span><span class="sxs-lookup"><span data-stu-id="05a8e-323">Example:</span></span>

```xml
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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="05a8e-324">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="05a8e-324">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="05a8e-325">Scrivere una destinazione personalizzata e specificarla come valore della `$(TargetsForTfmSpecificContentInPackage)` proprietà.</span><span class="sxs-lookup"><span data-stu-id="05a8e-325">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="05a8e-326">Per tutti i file da includere nel pacchetto, la destinazione deve scrivere i file in ItemGroup `TfmSpecificPackageFile` e impostare i metadati facoltativi seguenti:</span><span class="sxs-lookup"><span data-stu-id="05a8e-326">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="05a8e-327">`PackagePath`: Percorso in cui il file deve essere restituito nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="05a8e-327">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="05a8e-328">NuGet genera un avviso se viene aggiunto più di un file allo stesso percorso del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="05a8e-328">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="05a8e-329">`BuildAction`: L'azione di compilazione da assegnare al file, necessaria solo se il percorso del pacchetto si trova `contentFiles` nella cartella.</span><span class="sxs-lookup"><span data-stu-id="05a8e-329">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="05a8e-330">Il valore predefinito è "None".</span><span class="sxs-lookup"><span data-stu-id="05a8e-330">Defaults to "None".</span></span>

<span data-ttu-id="05a8e-331">Esempio:</span><span class="sxs-lookup"><span data-stu-id="05a8e-331">An example:</span></span>
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a><span data-ttu-id="05a8e-332">Destinazione restore</span><span class="sxs-lookup"><span data-stu-id="05a8e-332">restore target</span></span>

<span data-ttu-id="05a8e-333">`MSBuild -t:restore` (usato da `nuget restore` e `dotnet restore` con progetti .NET Core) consente di ripristinare i pacchetti a cui si fa riferimento nel file di progetto, come segue:</span><span class="sxs-lookup"><span data-stu-id="05a8e-333">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="05a8e-334">Lettura di tutti i riferimenti da progetto a progetto</span><span class="sxs-lookup"><span data-stu-id="05a8e-334">Read all project to project references</span></span>
1. <span data-ttu-id="05a8e-335">Lettura delle proprietà del progetto per trovare la cartella intermedia e i framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="05a8e-335">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="05a8e-336">Passare i dati di MSBuild a NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="05a8e-336">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="05a8e-337">Esecuzione di restore</span><span class="sxs-lookup"><span data-stu-id="05a8e-337">Run restore</span></span>
1. <span data-ttu-id="05a8e-338">Download dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="05a8e-338">Download packages</span></span>
1. <span data-ttu-id="05a8e-339">Scrittura dei file di asset, delle destinazioni e delle proprietà</span><span class="sxs-lookup"><span data-stu-id="05a8e-339">Write assets file, targets, and props</span></span>

<span data-ttu-id="05a8e-340">La `restore` destinazione funziona **solo** per i progetti che usano il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="05a8e-340">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="05a8e-341">Non funziona per i progetti che usano il `packages.config` formato; usare invece il [ripristino NuGet](../reference/cli-reference/cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="05a8e-341">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="05a8e-342">Ripristino delle proprietà</span><span class="sxs-lookup"><span data-stu-id="05a8e-342">Restore properties</span></span>

<span data-ttu-id="05a8e-343">Possono esistere ulteriori impostazioni di ripristino derivate da proprietà di MSBuild nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="05a8e-343">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="05a8e-344">I valori possono essere impostati anche dalla riga di comando tramite l'opzione `-p:` (vedere gli esempi riportati di seguito).</span><span class="sxs-lookup"><span data-stu-id="05a8e-344">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="05a8e-345">Proprietà</span><span class="sxs-lookup"><span data-stu-id="05a8e-345">Property</span></span> | <span data-ttu-id="05a8e-346">Descrizione</span><span class="sxs-lookup"><span data-stu-id="05a8e-346">Description</span></span> |
|--------|--------|
| <span data-ttu-id="05a8e-347">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="05a8e-347">RestoreSources</span></span> | <span data-ttu-id="05a8e-348">Elenco delimitato da punto e virgola delle origini di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="05a8e-348">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="05a8e-349">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="05a8e-349">RestorePackagesPath</span></span> | <span data-ttu-id="05a8e-350">Percorso della cartella dei pacchetti dell'utente.</span><span class="sxs-lookup"><span data-stu-id="05a8e-350">User packages folder path.</span></span> |
| <span data-ttu-id="05a8e-351">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="05a8e-351">RestoreDisableParallel</span></span> | <span data-ttu-id="05a8e-352">Consente di limitare i download a uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="05a8e-352">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="05a8e-353">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="05a8e-353">RestoreConfigFile</span></span> | <span data-ttu-id="05a8e-354">Percorso per un file `Nuget.Config` da applicare.</span><span class="sxs-lookup"><span data-stu-id="05a8e-354">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="05a8e-355">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="05a8e-355">RestoreNoCache</span></span> | <span data-ttu-id="05a8e-356">Se true, evita l'utilizzo di pacchetti memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="05a8e-356">If true, avoids using cached packages.</span></span> <span data-ttu-id="05a8e-357">Vedere [gestione dei pacchetti globali e delle cartelle della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="05a8e-357">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="05a8e-358">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="05a8e-358">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="05a8e-359">Se true, ignora le origini di pacchetti in errore o mancanti.</span><span class="sxs-lookup"><span data-stu-id="05a8e-359">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="05a8e-360">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="05a8e-360">RestoreFallbackFolders</span></span> | <span data-ttu-id="05a8e-361">Cartelle di fallback, utilizzate nello stesso modo in cui viene utilizzata la cartella Pacchetti utente.</span><span class="sxs-lookup"><span data-stu-id="05a8e-361">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="05a8e-362">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="05a8e-362">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="05a8e-363">Origini aggiuntive da utilizzare durante il ripristino.</span><span class="sxs-lookup"><span data-stu-id="05a8e-363">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="05a8e-364">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="05a8e-364">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="05a8e-365">Cartelle di fallback aggiuntive da usare durante il ripristino.</span><span class="sxs-lookup"><span data-stu-id="05a8e-365">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="05a8e-366">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="05a8e-366">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="05a8e-367">Esclude le cartelle di fallback specificate in`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="05a8e-367">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="05a8e-368">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="05a8e-368">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="05a8e-369">Percorso di `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="05a8e-369">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="05a8e-370">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="05a8e-370">RestoreGraphProjectInput</span></span> | <span data-ttu-id="05a8e-371">Elenco delimitato da punto e virgola dei progetti da ripristinare, che deve contenere percorsi assoluti.</span><span class="sxs-lookup"><span data-stu-id="05a8e-371">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="05a8e-372">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="05a8e-372">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="05a8e-373">Quando i progetti vengono raccolti tramite MSBuild, determina se vengono raccolti usando l' `SkipNonexistentTargets` ottimizzazione.</span><span class="sxs-lookup"><span data-stu-id="05a8e-373">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="05a8e-374">Quando non è impostato, il valore `true`predefinito è.</span><span class="sxs-lookup"><span data-stu-id="05a8e-374">When not set, defaults to `true`.</span></span> <span data-ttu-id="05a8e-375">La conseguenza è un comportamento non rapido quando le destinazioni di un progetto non possono essere importate.</span><span class="sxs-lookup"><span data-stu-id="05a8e-375">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="05a8e-376">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="05a8e-376">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="05a8e-377">Cartella di output, per `BaseIntermediateOutputPath` impostazione predefinita e la `obj` cartella.</span><span class="sxs-lookup"><span data-stu-id="05a8e-377">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="05a8e-378">Esempi</span><span class="sxs-lookup"><span data-stu-id="05a8e-378">Examples</span></span>

<span data-ttu-id="05a8e-379">Riga di comando:</span><span class="sxs-lookup"><span data-stu-id="05a8e-379">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="05a8e-380">File di progetto:</span><span class="sxs-lookup"><span data-stu-id="05a8e-380">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="05a8e-381">Output del ripristino</span><span class="sxs-lookup"><span data-stu-id="05a8e-381">Restore outputs</span></span>

<span data-ttu-id="05a8e-382">Il ripristino crea i file seguenti nella cartella `obj` di compilazione:</span><span class="sxs-lookup"><span data-stu-id="05a8e-382">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="05a8e-383">File</span><span class="sxs-lookup"><span data-stu-id="05a8e-383">File</span></span> | <span data-ttu-id="05a8e-384">DESCRIZIONE</span><span class="sxs-lookup"><span data-stu-id="05a8e-384">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="05a8e-385">Contiene il grafico delle dipendenze di tutti i riferimenti ai pacchetti.</span><span class="sxs-lookup"><span data-stu-id="05a8e-385">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="05a8e-386">Riferimenti alle proprietà di MSBuild contenute nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="05a8e-386">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="05a8e-387">Riferimenti alle destinazioni di MSBuild contenute nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="05a8e-387">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="05a8e-388">Ripristino e compilazione con un comando MSBuild</span><span class="sxs-lookup"><span data-stu-id="05a8e-388">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="05a8e-389">A causa del fatto che NuGet può ripristinare i pacchetti che arrestano le destinazioni e le proprietà di MSBuild, le valutazioni di ripristino e compilazione vengono eseguite con proprietà globali diverse.</span><span class="sxs-lookup"><span data-stu-id="05a8e-389">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="05a8e-390">Ciò significa che le operazioni seguenti avranno un comportamento imprevedibile e spesso errato.</span><span class="sxs-lookup"><span data-stu-id="05a8e-390">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="05a8e-391">L'approccio consigliato è invece:</span><span class="sxs-lookup"><span data-stu-id="05a8e-391">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="05a8e-392">La stessa logica si applica ad altre destinazioni simili `build`a.</span><span class="sxs-lookup"><span data-stu-id="05a8e-392">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="05a8e-393">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="05a8e-393">PackageTargetFallback</span></span>

<span data-ttu-id="05a8e-394">L'elemento `PackageTargetFallback` consente di specificare un set di destinazioni compatibili da usare durante il ripristino di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="05a8e-394">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="05a8e-395">È progettato per consentire ai pacchetti che usano un [TxM](../reference/target-frameworks.md) dotnet di interagire con pacchetti compatibili che non dichiarano un TxM dotnet.</span><span class="sxs-lookup"><span data-stu-id="05a8e-395">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="05a8e-396">Se il progetto usa il TxM dotnet, devono averlo anche tutti i pacchetti da cui il progetto dipende, a meno che non si aggiunga `<PackageTargetFallback>` al progetto, in modo da rendere compatibili con dotnet le piattaforme che non lo sono.</span><span class="sxs-lookup"><span data-stu-id="05a8e-396">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="05a8e-397">Ad esempio, se il progetto usa il TxM `netstandard1.6` e un pacchetto dipendente contiene solo `lib/net45/a.dll` e `lib/portable-net45+win81/a.dll`, la compilazione del progetto avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="05a8e-397">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="05a8e-398">Se si vuole includere solo quest'ultima DLL, è possibile aggiungere un `PackageTargetFallback` come segue per segnalare che la DLL `portable-net45+win81` è compatibile:</span><span class="sxs-lookup"><span data-stu-id="05a8e-398">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="05a8e-399">Per dichiarare un fallback per tutte le destinazioni nel progetto, non specificare l'attributo `Condition`.</span><span class="sxs-lookup"><span data-stu-id="05a8e-399">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="05a8e-400">È anche possibile estendere qualsiasi `PackageTargetFallback` esistente includendo `$(PackageTargetFallback)` come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="05a8e-400">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="05a8e-401">Sostituzione di una libreria da un grafico di ripristino</span><span class="sxs-lookup"><span data-stu-id="05a8e-401">Replacing one library from a restore graph</span></span>

<span data-ttu-id="05a8e-402">Se un ripristino restituisce l'assembly errato, è possibile escludere la scelta predefinita di tali pacchetti e sostituirla con la propria scelta.</span><span class="sxs-lookup"><span data-stu-id="05a8e-402">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="05a8e-403">Prima di tutto, con un `PackageReference` di livello superiore, escludere tutti gli asset:</span><span class="sxs-lookup"><span data-stu-id="05a8e-403">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="05a8e-404">Aggiungere quindi il riferimento personalizzato alla copia locale appropriata della DLL:</span><span class="sxs-lookup"><span data-stu-id="05a8e-404">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
