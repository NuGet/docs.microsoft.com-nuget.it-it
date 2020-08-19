---
title: Pack e restore di NuGet come destinazioni MSBuild
description: I comandi pack e restore di NuGet possono essere usati direttamente come destinazioni MSBuild con NuGet 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 16fd7b9103ef5ac335f0b2e5493dd2983b182f50
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623175"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="ff584-103">Pack e restore di NuGet come destinazioni MSBuild</span><span class="sxs-lookup"><span data-stu-id="ff584-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="ff584-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="ff584-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="ff584-105">Con il formato [PackageReference](../consume-packages/package-references-in-project-files.md) , NuGet 4.0 + può archiviare tutti i metadati del manifesto direttamente all'interno di un file di progetto anziché usare un `.nuspec` file separato.</span><span class="sxs-lookup"><span data-stu-id="ff584-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="ff584-106">Con MSBuild 15.1 +, anche NuGet è un membro di MSBuild di prima classe con le destinazioni `pack` e `restore` come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="ff584-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="ff584-107">Queste destinazioni consentono di usare NuGet come qualsiasi altra attività o destinazione MSBuild.</span><span class="sxs-lookup"><span data-stu-id="ff584-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="ff584-108">Per istruzioni sulla creazione di un pacchetto NuGet con MSBuild, vedere [creare un pacchetto NuGet con MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="ff584-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="ff584-109">Per NuGet 3.x e versioni precedenti, usare invece i comandi [pack](../reference/cli-reference/cli-ref-pack.md) e [restore](../reference/cli-reference/cli-ref-restore.md) tramite l'interfaccia della riga di comando di NuGet.</span><span class="sxs-lookup"><span data-stu-id="ff584-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="ff584-110">Ordine di compilazione delle destinazioni</span><span class="sxs-lookup"><span data-stu-id="ff584-110">Target build order</span></span>

<span data-ttu-id="ff584-111">Dato che `pack` e `restore` sono destinazioni MSBuild, è possibile accedervi per ottimizzare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ff584-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="ff584-112">Si supponga, ad esempio, di voler copiare il pacchetto in una condivisione di rete dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="ff584-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="ff584-113">È possibile farlo aggiungendo quanto segue nel file di progetto:</span><span class="sxs-lookup"><span data-stu-id="ff584-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="ff584-114">Analogamente, è possibile scrivere un'attività MSBuild, scrivere la propria destinazione e utilizzare proprietà NuGet nell'attività MSBuild.</span><span class="sxs-lookup"><span data-stu-id="ff584-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="ff584-115">`$(OutputPath)` è relativo e prevede che si esegua il comando dalla radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="ff584-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="ff584-116">Destinazione pack</span><span class="sxs-lookup"><span data-stu-id="ff584-116">pack target</span></span>

<span data-ttu-id="ff584-117">Per .NET Standard progetti che usano il formato PackageReference, l'uso di `msbuild -t:pack` disegna gli input dal file di progetto da usare per la creazione di un pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="ff584-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="ff584-118">La tabella seguente descrive le proprietà di MSBuild che possono essere aggiunte a un file di progetto all'interno del primo nodo `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="ff584-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="ff584-119">È possibile apportare facilmente queste modifiche in Visual Studio 2017 e versioni successive facendo clic con il pulsante destro del mouse sul progetto e scegliendo **Modifica {nome_progetto}** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="ff584-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="ff584-120">Per praticità, la tabella è organizzata in base alla proprietà equivalente in un [ `.nuspec` file](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="ff584-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="ff584-121">Si noti che le proprietà `Owners` e `Summary` da `.nuspec` non sono supportate con MSBuild.</span><span class="sxs-lookup"><span data-stu-id="ff584-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="ff584-122">Valore di attributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="ff584-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="ff584-123">Proprietà MSBuild</span><span class="sxs-lookup"><span data-stu-id="ff584-123">MSBuild Property</span></span> | <span data-ttu-id="ff584-124">Predefinito</span><span class="sxs-lookup"><span data-stu-id="ff584-124">Default</span></span> | <span data-ttu-id="ff584-125">Note</span><span class="sxs-lookup"><span data-stu-id="ff584-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="ff584-126">ID</span><span class="sxs-lookup"><span data-stu-id="ff584-126">Id</span></span> | <span data-ttu-id="ff584-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="ff584-127">PackageId</span></span> | <span data-ttu-id="ff584-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="ff584-128">AssemblyName</span></span> | <span data-ttu-id="ff584-129">$(AssemblyName) da MSBuild</span><span class="sxs-lookup"><span data-stu-id="ff584-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="ff584-130">Versione</span><span class="sxs-lookup"><span data-stu-id="ff584-130">Version</span></span> | <span data-ttu-id="ff584-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="ff584-131">PackageVersion</span></span> | <span data-ttu-id="ff584-132">Versione</span><span class="sxs-lookup"><span data-stu-id="ff584-132">Version</span></span> | <span data-ttu-id="ff584-133">Compatibile con SemVer, ad esempio "1.0.0", "1.0.0-beta" o "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="ff584-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="ff584-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="ff584-134">VersionPrefix</span></span> | <span data-ttu-id="ff584-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="ff584-135">PackageVersionPrefix</span></span> | <span data-ttu-id="ff584-136">empty</span><span class="sxs-lookup"><span data-stu-id="ff584-136">empty</span></span> | <span data-ttu-id="ff584-137">L'impostazione di PackageVersion sovrascrive PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="ff584-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="ff584-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="ff584-138">VersionSuffix</span></span> | <span data-ttu-id="ff584-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="ff584-139">PackageVersionSuffix</span></span> | <span data-ttu-id="ff584-140">empty</span><span class="sxs-lookup"><span data-stu-id="ff584-140">empty</span></span> | <span data-ttu-id="ff584-141">$(VersionSuffix) da MSBuild.</span><span class="sxs-lookup"><span data-stu-id="ff584-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="ff584-142">L'impostazione di PackageVersion sovrascrive PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="ff584-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="ff584-143">Autori</span><span class="sxs-lookup"><span data-stu-id="ff584-143">Authors</span></span> | <span data-ttu-id="ff584-144">Autori</span><span class="sxs-lookup"><span data-stu-id="ff584-144">Authors</span></span> | <span data-ttu-id="ff584-145">Nome utente dell'utente corrente</span><span class="sxs-lookup"><span data-stu-id="ff584-145">Username of the current user</span></span> | |
| <span data-ttu-id="ff584-146">Proprietari</span><span class="sxs-lookup"><span data-stu-id="ff584-146">Owners</span></span> | <span data-ttu-id="ff584-147">N/D</span><span class="sxs-lookup"><span data-stu-id="ff584-147">N/A</span></span> | <span data-ttu-id="ff584-148">Non presente in NuSpec</span><span class="sxs-lookup"><span data-stu-id="ff584-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="ff584-149">Titolo</span><span class="sxs-lookup"><span data-stu-id="ff584-149">Title</span></span> | <span data-ttu-id="ff584-150">Titolo</span><span class="sxs-lookup"><span data-stu-id="ff584-150">Title</span></span> | <span data-ttu-id="ff584-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="ff584-151">The PackageId</span></span>| |
| <span data-ttu-id="ff584-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff584-152">Description</span></span> | <span data-ttu-id="ff584-153">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff584-153">Description</span></span> | <span data-ttu-id="ff584-154">"Descrizione del pacchetto"</span><span class="sxs-lookup"><span data-stu-id="ff584-154">"Package Description"</span></span> | |
| <span data-ttu-id="ff584-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="ff584-155">Copyright</span></span> | <span data-ttu-id="ff584-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="ff584-156">Copyright</span></span> | <span data-ttu-id="ff584-157">empty</span><span class="sxs-lookup"><span data-stu-id="ff584-157">empty</span></span> | |
| <span data-ttu-id="ff584-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="ff584-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="ff584-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="ff584-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="ff584-160">false</span><span class="sxs-lookup"><span data-stu-id="ff584-160">false</span></span> | |
| <span data-ttu-id="ff584-161">license</span><span class="sxs-lookup"><span data-stu-id="ff584-161">license</span></span> | <span data-ttu-id="ff584-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="ff584-162">PackageLicenseExpression</span></span> | <span data-ttu-id="ff584-163">empty</span><span class="sxs-lookup"><span data-stu-id="ff584-163">empty</span></span> | <span data-ttu-id="ff584-164">Corrisponde a `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="ff584-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="ff584-165">license</span><span class="sxs-lookup"><span data-stu-id="ff584-165">license</span></span> | <span data-ttu-id="ff584-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="ff584-166">PackageLicenseFile</span></span> | <span data-ttu-id="ff584-167">empty</span><span class="sxs-lookup"><span data-stu-id="ff584-167">empty</span></span> | <span data-ttu-id="ff584-168">Corrisponde a `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="ff584-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="ff584-169">È necessario comprimere in modo esplicito il file di licenza a cui si fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="ff584-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="ff584-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="ff584-170">LicenseUrl</span></span> | <span data-ttu-id="ff584-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="ff584-171">PackageLicenseUrl</span></span> | <span data-ttu-id="ff584-172">empty</span><span class="sxs-lookup"><span data-stu-id="ff584-172">empty</span></span> | <span data-ttu-id="ff584-173">`PackageLicenseUrl` è deprecato, usare la proprietà PackageLicenseExpression o PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="ff584-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="ff584-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="ff584-174">ProjectUrl</span></span> | <span data-ttu-id="ff584-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="ff584-175">PackageProjectUrl</span></span> | <span data-ttu-id="ff584-176">empty</span><span class="sxs-lookup"><span data-stu-id="ff584-176">empty</span></span> | |
| <span data-ttu-id="ff584-177">Icona</span><span class="sxs-lookup"><span data-stu-id="ff584-177">Icon</span></span> | <span data-ttu-id="ff584-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="ff584-178">PackageIcon</span></span> | <span data-ttu-id="ff584-179">empty</span><span class="sxs-lookup"><span data-stu-id="ff584-179">empty</span></span> | <span data-ttu-id="ff584-180">È necessario comprimere in modo esplicito il file di immagine icona a cui si fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="ff584-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="ff584-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="ff584-181">IconUrl</span></span> | <span data-ttu-id="ff584-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="ff584-182">PackageIconUrl</span></span> | <span data-ttu-id="ff584-183">empty</span><span class="sxs-lookup"><span data-stu-id="ff584-183">empty</span></span> | <span data-ttu-id="ff584-184">Per la migliore esperienza di livello inferiore, `PackageIconUrl` è necessario specificare oltre a `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="ff584-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="ff584-185">A lungo termine, `PackageIconUrl` verrà deprecato.</span><span class="sxs-lookup"><span data-stu-id="ff584-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="ff584-186">Tag</span><span class="sxs-lookup"><span data-stu-id="ff584-186">Tags</span></span> | <span data-ttu-id="ff584-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="ff584-187">PackageTags</span></span> | <span data-ttu-id="ff584-188">empty</span><span class="sxs-lookup"><span data-stu-id="ff584-188">empty</span></span> | <span data-ttu-id="ff584-189">I tag sono delimitati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="ff584-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="ff584-190">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="ff584-190">ReleaseNotes</span></span> | <span data-ttu-id="ff584-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="ff584-191">PackageReleaseNotes</span></span> | <span data-ttu-id="ff584-192">empty</span><span class="sxs-lookup"><span data-stu-id="ff584-192">empty</span></span> | |
| <span data-ttu-id="ff584-193">Repository/URL</span><span class="sxs-lookup"><span data-stu-id="ff584-193">Repository/Url</span></span> | <span data-ttu-id="ff584-194">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="ff584-194">RepositoryUrl</span></span> | <span data-ttu-id="ff584-195">empty</span><span class="sxs-lookup"><span data-stu-id="ff584-195">empty</span></span> | <span data-ttu-id="ff584-196">URL del repository usato per clonare o recuperare il codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="ff584-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="ff584-197">Esempio *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="ff584-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="ff584-198">Repository/tipo</span><span class="sxs-lookup"><span data-stu-id="ff584-198">Repository/Type</span></span> | <span data-ttu-id="ff584-199">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="ff584-199">RepositoryType</span></span> | <span data-ttu-id="ff584-200">empty</span><span class="sxs-lookup"><span data-stu-id="ff584-200">empty</span></span> | <span data-ttu-id="ff584-201">Tipo di repository.</span><span class="sxs-lookup"><span data-stu-id="ff584-201">Repository type.</span></span> <span data-ttu-id="ff584-202">Esempi: *git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="ff584-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="ff584-203">Repository/ramo</span><span class="sxs-lookup"><span data-stu-id="ff584-203">Repository/Branch</span></span> | <span data-ttu-id="ff584-204">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="ff584-204">RepositoryBranch</span></span> | <span data-ttu-id="ff584-205">empty</span><span class="sxs-lookup"><span data-stu-id="ff584-205">empty</span></span> | <span data-ttu-id="ff584-206">Informazioni facoltative sul ramo del repository.</span><span class="sxs-lookup"><span data-stu-id="ff584-206">Optional repository branch information.</span></span> <span data-ttu-id="ff584-207">Per includere questa proprietà, è necessario specificare anche *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="ff584-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="ff584-208">Esempio: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="ff584-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="ff584-209">Repository/commit</span><span class="sxs-lookup"><span data-stu-id="ff584-209">Repository/Commit</span></span> | <span data-ttu-id="ff584-210">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="ff584-210">RepositoryCommit</span></span> | <span data-ttu-id="ff584-211">empty</span><span class="sxs-lookup"><span data-stu-id="ff584-211">empty</span></span> | <span data-ttu-id="ff584-212">Commit o insieme di modifiche facoltativo del repository per indicare l'origine su cui è stato compilato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ff584-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="ff584-213">Per includere questa proprietà, è necessario specificare anche *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="ff584-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="ff584-214">Esempio: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="ff584-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="ff584-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="ff584-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="ff584-216">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="ff584-216">Summary</span></span> | <span data-ttu-id="ff584-217">Non supportate</span><span class="sxs-lookup"><span data-stu-id="ff584-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="ff584-218">Input destinazione pack</span><span class="sxs-lookup"><span data-stu-id="ff584-218">pack target inputs</span></span>

- <span data-ttu-id="ff584-219">IsPackable</span><span class="sxs-lookup"><span data-stu-id="ff584-219">IsPackable</span></span>
- <span data-ttu-id="ff584-220">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="ff584-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="ff584-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="ff584-221">PackageVersion</span></span>
- <span data-ttu-id="ff584-222">PackageId</span><span class="sxs-lookup"><span data-stu-id="ff584-222">PackageId</span></span>
- <span data-ttu-id="ff584-223">Autori</span><span class="sxs-lookup"><span data-stu-id="ff584-223">Authors</span></span>
- <span data-ttu-id="ff584-224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff584-224">Description</span></span>
- <span data-ttu-id="ff584-225">Copyright</span><span class="sxs-lookup"><span data-stu-id="ff584-225">Copyright</span></span>
- <span data-ttu-id="ff584-226">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="ff584-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="ff584-227">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="ff584-227">DevelopmentDependency</span></span>
- <span data-ttu-id="ff584-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="ff584-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="ff584-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="ff584-229">PackageLicenseFile</span></span>
- <span data-ttu-id="ff584-230">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="ff584-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="ff584-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="ff584-231">PackageProjectUrl</span></span>
- <span data-ttu-id="ff584-232">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="ff584-232">PackageIconUrl</span></span>
- <span data-ttu-id="ff584-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="ff584-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="ff584-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="ff584-234">PackageTags</span></span>
- <span data-ttu-id="ff584-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="ff584-235">PackageOutputPath</span></span>
- <span data-ttu-id="ff584-236">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="ff584-236">IncludeSymbols</span></span>
- <span data-ttu-id="ff584-237">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="ff584-237">IncludeSource</span></span>
- <span data-ttu-id="ff584-238">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="ff584-238">PackageTypes</span></span>
- <span data-ttu-id="ff584-239">IsTool</span><span class="sxs-lookup"><span data-stu-id="ff584-239">IsTool</span></span>
- <span data-ttu-id="ff584-240">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="ff584-240">RepositoryUrl</span></span>
- <span data-ttu-id="ff584-241">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="ff584-241">RepositoryType</span></span>
- <span data-ttu-id="ff584-242">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="ff584-242">RepositoryBranch</span></span>
- <span data-ttu-id="ff584-243">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="ff584-243">RepositoryCommit</span></span>
- <span data-ttu-id="ff584-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="ff584-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="ff584-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="ff584-245">MinClientVersion</span></span>
- <span data-ttu-id="ff584-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="ff584-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="ff584-247">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="ff584-247">IncludeContentInPack</span></span>
- <span data-ttu-id="ff584-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="ff584-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="ff584-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="ff584-249">ContentTargetFolders</span></span>
- <span data-ttu-id="ff584-250">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="ff584-250">NuspecFile</span></span>
- <span data-ttu-id="ff584-251">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="ff584-251">NuspecBasePath</span></span>
- <span data-ttu-id="ff584-252">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="ff584-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="ff584-253">Scenari pack</span><span class="sxs-lookup"><span data-stu-id="ff584-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="ff584-254">Non visualizzare le dipendenze</span><span class="sxs-lookup"><span data-stu-id="ff584-254">Suppress dependencies</span></span>

<span data-ttu-id="ff584-255">Per non visualizzare le dipendenze del pacchetto dal pacchetto NuGet generato, impostare `SuppressDependenciesWhenPacking` su `true` che consentirà di ignorare tutte le dipendenze dal file nupkg generato.</span><span class="sxs-lookup"><span data-stu-id="ff584-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="ff584-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="ff584-256">PackageIconUrl</span></span>

<span data-ttu-id="ff584-257">`PackageIconUrl` verrà deprecato a favore della nuova [`PackageIcon`](#packageicon) Proprietà.</span><span class="sxs-lookup"><span data-stu-id="ff584-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="ff584-258">A partire da NuGet 5,3 & Visual Studio 2019 versione 16,3, `pack` genererà un avviso [NU5048](./errors-and-warnings/nu5048.md) se i metadati del pacchetto specificano solo `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="ff584-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="ff584-259">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="ff584-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="ff584-260">È necessario specificare sia `PackageIcon` che `PackageIconUrl` per mantenere la compatibilità con le versioni precedenti di client e origini che non supportano ancora `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="ff584-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="ff584-261">Visual Studio supporterà `PackageIcon` i pacchetti provenienti da un'origine basata su cartelle in una versione futura.</span><span class="sxs-lookup"><span data-stu-id="ff584-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="ff584-262">Compressione di un file di immagine icona</span><span class="sxs-lookup"><span data-stu-id="ff584-262">Packing an icon image file</span></span>

<span data-ttu-id="ff584-263">Quando si imballa un file di immagine icona, è necessario utilizzare `PackageIcon` la proprietà per specificare il percorso del pacchetto, relativo alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ff584-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="ff584-264">Inoltre, è necessario assicurarsi che il file sia incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ff584-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="ff584-265">Le dimensioni del file di immagine sono limitate a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="ff584-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="ff584-266">I formati di file supportati sono JPEG e PNG.</span><span class="sxs-lookup"><span data-stu-id="ff584-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="ff584-267">Si consiglia la risoluzione di un'immagine di 128x128.</span><span class="sxs-lookup"><span data-stu-id="ff584-267">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="ff584-268">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ff584-268">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="ff584-269">[Esempio di icona del pacchetto](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="ff584-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="ff584-270">Per l'equivalente NuSpec, vedere la pagina [di riferimento di nuspec per l'icona](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="ff584-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="ff584-271">Assembly di output</span><span class="sxs-lookup"><span data-stu-id="ff584-271">Output assemblies</span></span>

<span data-ttu-id="ff584-272">`nuget pack` copia i file di output con le estensioni `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="ff584-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="ff584-273">I file di output copiati dipendono da quanto fornito da MSBuild dalla destinazione `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="ff584-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="ff584-274">Sono disponibili due proprietà di MSBuild che è possibile usare nel file di progetto o nella riga di comando per controllare la destinazione degli assembly di output:</span><span class="sxs-lookup"><span data-stu-id="ff584-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="ff584-275">`IncludeBuildOutput`: valore booleano che determina se gli assembly di output della compilazione devono essere inclusi nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ff584-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="ff584-276">`BuildOutputTargetFolder`: specifica la cartella in cui devono essere posizionati gli assembly di output.</span><span class="sxs-lookup"><span data-stu-id="ff584-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="ff584-277">Gli assembly di output (e altri file di output) vengono copiati nelle rispettive cartelle per framework.</span><span class="sxs-lookup"><span data-stu-id="ff584-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="ff584-278">Riferimenti ai pacchetti</span><span class="sxs-lookup"><span data-stu-id="ff584-278">Package references</span></span>

<span data-ttu-id="ff584-279">Vedere [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="ff584-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="ff584-280">Riferimenti da progetto a progetto</span><span class="sxs-lookup"><span data-stu-id="ff584-280">Project to project references</span></span>

<span data-ttu-id="ff584-281">I riferimenti da progetto a progetto sono considerati per impostazione predefinita come riferimenti a pacchetti NuGet, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ff584-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="ff584-282">È anche possibile aggiungere i metadati seguenti ai riferimenti del progetto:</span><span class="sxs-lookup"><span data-stu-id="ff584-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="ff584-283">Inclusione di contenuto in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="ff584-283">Including content in a package</span></span>

<span data-ttu-id="ff584-284">Per includere il contenuto, aggiungere altri metadati all'elemento `<Content>` esistente.</span><span class="sxs-lookup"><span data-stu-id="ff584-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="ff584-285">Per impostazione predefinita tutti gli elementi di tipo"Content" vengono inclusi nel pacchetto, a meno che non si esegua l'override con voci simili al codice seguente:</span><span class="sxs-lookup"><span data-stu-id="ff584-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="ff584-286">Per impostazione predefinita, tutti gli elementi vengono aggiunti alla radice di `content` e della cartella `contentFiles\any\<target_framework>` all'interno di un pacchetto e viene mantenuta la struttura di cartelle relative, a meno che non si specifichi un percorso di pacchetto:</span><span class="sxs-lookup"><span data-stu-id="ff584-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="ff584-287">Se si vuole copiare tutto il contenuto sono in cartelle radice specifiche (invece di copiarlo sia in `content` che in `contentFiles`), è possibile usare la proprietà di MSBuild `ContentTargetFolders`, che ha il valore predefinito "content;contentFiles" ma può essere impostata su qualsiasi altro nome di cartella.</span><span class="sxs-lookup"><span data-stu-id="ff584-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="ff584-288">Si noti che se si specifica solo "contentFiles" in `ContentTargetFolders`, i file vengono posizionati in `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` in base a `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="ff584-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="ff584-289">`PackagePath` può essere un set di percorsi di destinazione delimitati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="ff584-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="ff584-290">Se si specifica un percorso di pacchetto vuoto, il file viene aggiunto alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ff584-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="ff584-291">Ad esempio, il codice seguente aggiunge `libuv.txt` a `content\myfiles`, `content\samples` e nella radice del pacchetto:</span><span class="sxs-lookup"><span data-stu-id="ff584-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="ff584-292">È disponibile anche una proprietà di MSBuild `$(IncludeContentInPack)`, con valore predefinito `true`.</span><span class="sxs-lookup"><span data-stu-id="ff584-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="ff584-293">Se questa proprietà viene impostata su `false` in qualsiasi progetto, il contenuto da tale progetto non viene incluso nel pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="ff584-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="ff584-294">Altri metadati specifici di pack che è possibile impostare per qualsiasi elemento precedente includono ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, che impostano i valori ```CopyToOutput``` e ```Flatten``` sulla voce ```contentFiles``` nel file nuspec di output.</span><span class="sxs-lookup"><span data-stu-id="ff584-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="ff584-295">Oltre agli elementi Content, i metadati `<Pack>` e `<PackagePath>` possono anche essere impostati nei file con l'azione di compilazione Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o None.</span><span class="sxs-lookup"><span data-stu-id="ff584-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="ff584-296">Per fare in modo che il comando pack aggiunga il nome del file al percorso del pacchetto quando si usano modelli con caratteri jolly (glob), il percorso del pacchetto deve terminare con il carattere separatore di cartella. In caso contrario, il percorso del pacchetto viene interpretato come percorso completo, incluso il nome del file.</span><span class="sxs-lookup"><span data-stu-id="ff584-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="ff584-297">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="ff584-297">IncludeSymbols</span></span>

<span data-ttu-id="ff584-298">Quando si usa `MSBuild -t:pack -p:IncludeSymbols=true`, i file `.pdb` corrispondenti vengono copiati insieme agli altri file di output (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="ff584-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="ff584-299">Si noti che l'impostazione `IncludeSymbols=true` crea un pacchetto regolare *e* un pacchetto di simboli.</span><span class="sxs-lookup"><span data-stu-id="ff584-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="ff584-300">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="ff584-300">IncludeSource</span></span>

<span data-ttu-id="ff584-301">Equivale a `IncludeSymbols`, ma insieme ai file `.pdb` vengono copiati anche i file di origine.</span><span class="sxs-lookup"><span data-stu-id="ff584-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="ff584-302">Tutti i file di tipo `Compile` vengono copiati in `src\<ProjectName>\` conservando la struttura di cartelle del percorso relativo nel pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="ff584-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="ff584-303">Lo stesso accade anche per i file di origine di qualsiasi `ProjectReference` con `TreatAsPackageReference` impostato su `false`.</span><span class="sxs-lookup"><span data-stu-id="ff584-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="ff584-304">Se un file di tipo Compile è all'esterno della cartella di progetto, viene semplicemente aggiunto a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="ff584-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="ff584-305">Compressione di un'espressione di licenza o di un file di licenza</span><span class="sxs-lookup"><span data-stu-id="ff584-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="ff584-306">Quando si usa un'espressione di licenza, è necessario usare la proprietà PackageLicenseExpression.</span><span class="sxs-lookup"><span data-stu-id="ff584-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="ff584-307">[Esempio di espressione di licenza](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="ff584-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="ff584-308">[Altre informazioni sulle espressioni di licenza e le licenze accettate da NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="ff584-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="ff584-309">Quando si imballa un file di licenza, è necessario utilizzare la proprietà PackageLicenseFile per specificare il percorso del pacchetto, relativo alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ff584-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="ff584-310">Inoltre, è necessario assicurarsi che il file sia incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ff584-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="ff584-311">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ff584-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="ff584-312">[Esempio di file di licenza](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="ff584-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="ff584-313">IsTool</span><span class="sxs-lookup"><span data-stu-id="ff584-313">IsTool</span></span>

<span data-ttu-id="ff584-314">Quando si usa `MSBuild -t:pack -p:IsTool=true`, tutti i file, come specificato nello scenario [Assembly di output](#output-assemblies), vengono copiati nella cartella `tools` invece che nella cartella `lib`.</span><span class="sxs-lookup"><span data-stu-id="ff584-314">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="ff584-315">Si noti che questo comportamento è diverso da `DotNetCliTool`, che viene specificato impostando `PackageType` nel file `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="ff584-315">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="ff584-316">Creazione di un pacchetto con un file .nuspec</span><span class="sxs-lookup"><span data-stu-id="ff584-316">Packing using a .nuspec</span></span>

<span data-ttu-id="ff584-317">Sebbene sia consigliabile includere in alternativa [tutte le proprietà](../reference/msbuild-targets.md#pack-target) che in genere si trovano nel file del `.nuspec` progetto, è possibile scegliere di utilizzare un `.nuspec` file per comprimere il progetto.</span><span class="sxs-lookup"><span data-stu-id="ff584-317">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="ff584-318">Per un progetto non di tipo SDK che utilizza `PackageReference` , è necessario importare in `NuGet.Build.Tasks.Pack.targets` modo che l'attività Pack possa essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="ff584-318">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="ff584-319">Prima di poter comprimere un file nuspec, è ancora necessario ripristinare il progetto.</span><span class="sxs-lookup"><span data-stu-id="ff584-319">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="ff584-320">Un progetto di tipo SDK include le destinazioni di tipo pack per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ff584-320">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="ff584-321">Il Framework di destinazione del file di progetto non è rilevante e non viene usato per la compressione di un NuSpec.</span><span class="sxs-lookup"><span data-stu-id="ff584-321">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="ff584-322">Le tre proprietà di MSBuild seguenti sono rilevanti per la creazione di pacchetti con un file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="ff584-322">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="ff584-323">`NuspecFile`: percorso relativo o assoluto per il file `.nuspec` usato per la creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ff584-323">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="ff584-324">`NuspecProperties`: elenco con valori delimitati da punto e virgola di coppie chiave=valore.</span><span class="sxs-lookup"><span data-stu-id="ff584-324">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="ff584-325">A causa della modalità di funzionamento dell'analisi della riga di comando di MSBuild, è necessario specificare più proprietà come indicato di seguito: `-p:NuspecProperties="key1=value1;key2=value2"`.</span><span class="sxs-lookup"><span data-stu-id="ff584-325">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="ff584-326">`NuspecBasePath`: percorso di base per il file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="ff584-326">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="ff584-327">Se si usa `dotnet.exe` per creare il pacchetto del progetto, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ff584-327">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="ff584-328">Se si usa MSBuild per creare il pacchetto del progetto, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ff584-328">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="ff584-329">Si noti che la compressione di un NuSpec tramite dotnet.exe o MSBuild comporta anche la compilazione del progetto per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ff584-329">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="ff584-330">Questa operazione può essere evitata passando ```--no-build``` la proprietà a dotnet.exe, che è l'equivalente dell'impostazione ```<NoBuild>true</NoBuild> ``` nel file di progetto, insieme all'impostazione ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="ff584-330">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="ff584-331">Un esempio di file con estensione *csproj* per la compressione di un file nuspec è:</span><span class="sxs-lookup"><span data-stu-id="ff584-331">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="ff584-332">Punti di estensione avanzati per la creazione di pacchetti personalizzati</span><span class="sxs-lookup"><span data-stu-id="ff584-332">Advanced extension points to create customized package</span></span>

<span data-ttu-id="ff584-333">La `pack` destinazione fornisce due punti di estensione che vengono eseguiti nella compilazione specifica del Framework di destinazione interno.</span><span class="sxs-lookup"><span data-stu-id="ff584-333">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="ff584-334">I punti di estensione supportano l'inclusione di contenuto e assembly specifici del Framework di destinazione in un pacchetto:</span><span class="sxs-lookup"><span data-stu-id="ff584-334">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="ff584-335">`TargetsForTfmSpecificBuildOutput` destinazione: utilizzare per i file all'interno della `lib` cartella o in una cartella specificata utilizzando `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="ff584-335">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="ff584-336">`TargetsForTfmSpecificContentInPackage` destinazione: usare per i file all'esterno di `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="ff584-336">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="ff584-337">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="ff584-337">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="ff584-338">Scrivere una destinazione personalizzata e specificarla come valore della `$(TargetsForTfmSpecificBuildOutput)` Proprietà.</span><span class="sxs-lookup"><span data-stu-id="ff584-338">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="ff584-339">Per tutti i file che devono essere inseriti in `BuildOutputTargetFolder` (per impostazione predefinita, lib), la destinazione deve scrivere i file in ItemGroup `BuildOutputInPackage` e impostare i due valori di metadati seguenti:</span><span class="sxs-lookup"><span data-stu-id="ff584-339">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="ff584-340">`FinalOutputPath`: Percorso assoluto del file; Se non viene specificato, l'identità viene utilizzata per valutare il percorso di origine.</span><span class="sxs-lookup"><span data-stu-id="ff584-340">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="ff584-341">`TargetPath`: (Facoltativo) impostare quando il file deve essere inserito in una sottocartella all'interno di `lib\<TargetFramework>` , ad esempio gli assembly satellite che passano sotto le rispettive cartelle delle impostazioni cultura.</span><span class="sxs-lookup"><span data-stu-id="ff584-341">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="ff584-342">Il valore predefinito è il nome del file.</span><span class="sxs-lookup"><span data-stu-id="ff584-342">Defaults to the name of the file.</span></span>

<span data-ttu-id="ff584-343">Esempio:</span><span class="sxs-lookup"><span data-stu-id="ff584-343">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="ff584-344">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="ff584-344">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="ff584-345">Scrivere una destinazione personalizzata e specificarla come valore della `$(TargetsForTfmSpecificContentInPackage)` Proprietà.</span><span class="sxs-lookup"><span data-stu-id="ff584-345">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="ff584-346">Per tutti i file da includere nel pacchetto, la destinazione deve scrivere i file in ItemGroup `TfmSpecificPackageFile` e impostare i metadati facoltativi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ff584-346">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="ff584-347">`PackagePath`: Percorso in cui il file deve essere restituito nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ff584-347">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="ff584-348">NuGet genera un avviso se viene aggiunto più di un file allo stesso percorso del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ff584-348">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="ff584-349">`BuildAction`: L'azione di compilazione da assegnare al file, necessaria solo se il percorso del pacchetto si trova nella `contentFiles` cartella.</span><span class="sxs-lookup"><span data-stu-id="ff584-349">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="ff584-350">Il valore predefinito è "None".</span><span class="sxs-lookup"><span data-stu-id="ff584-350">Defaults to "None".</span></span>

<span data-ttu-id="ff584-351">Esempio:</span><span class="sxs-lookup"><span data-stu-id="ff584-351">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="ff584-352">Destinazione restore</span><span class="sxs-lookup"><span data-stu-id="ff584-352">restore target</span></span>

<span data-ttu-id="ff584-353">`MSBuild -t:restore` (usato da `nuget restore` e `dotnet restore` con progetti .NET Core) consente di ripristinare i pacchetti a cui si fa riferimento nel file di progetto, come segue:</span><span class="sxs-lookup"><span data-stu-id="ff584-353">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="ff584-354">Lettura di tutti i riferimenti da progetto a progetto</span><span class="sxs-lookup"><span data-stu-id="ff584-354">Read all project to project references</span></span>
1. <span data-ttu-id="ff584-355">Lettura delle proprietà del progetto per trovare la cartella intermedia e i framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="ff584-355">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="ff584-356">Passare dati MSBuild a NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="ff584-356">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="ff584-357">Esecuzione di restore</span><span class="sxs-lookup"><span data-stu-id="ff584-357">Run restore</span></span>
1. <span data-ttu-id="ff584-358">Download dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="ff584-358">Download packages</span></span>
1. <span data-ttu-id="ff584-359">Scrittura dei file di asset, delle destinazioni e delle proprietà</span><span class="sxs-lookup"><span data-stu-id="ff584-359">Write assets file, targets, and props</span></span>

<span data-ttu-id="ff584-360">La `restore` destinazione funziona **solo** per i progetti che usano il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="ff584-360">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="ff584-361">**Non funziona per** i progetti che usano il `packages.config` formato; usare invece il [ripristino NuGet](../reference/cli-reference/cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="ff584-361">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="ff584-362">Ripristino delle proprietà</span><span class="sxs-lookup"><span data-stu-id="ff584-362">Restore properties</span></span>

<span data-ttu-id="ff584-363">Possono esistere ulteriori impostazioni di ripristino derivate da proprietà di MSBuild nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="ff584-363">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="ff584-364">I valori possono essere impostati anche dalla riga di comando tramite l'opzione `-p:` (vedere gli esempi riportati di seguito).</span><span class="sxs-lookup"><span data-stu-id="ff584-364">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="ff584-365">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ff584-365">Property</span></span> | <span data-ttu-id="ff584-366">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff584-366">Description</span></span> |
|--------|--------|
| <span data-ttu-id="ff584-367">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="ff584-367">RestoreSources</span></span> | <span data-ttu-id="ff584-368">Elenco delimitato da punto e virgola delle origini di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="ff584-368">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="ff584-369">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="ff584-369">RestorePackagesPath</span></span> | <span data-ttu-id="ff584-370">Percorso della cartella dei pacchetti dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ff584-370">User packages folder path.</span></span> |
| <span data-ttu-id="ff584-371">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="ff584-371">RestoreDisableParallel</span></span> | <span data-ttu-id="ff584-372">Consente di limitare i download a uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="ff584-372">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="ff584-373">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="ff584-373">RestoreConfigFile</span></span> | <span data-ttu-id="ff584-374">Percorso per un file `Nuget.Config` da applicare.</span><span class="sxs-lookup"><span data-stu-id="ff584-374">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="ff584-375">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="ff584-375">RestoreNoCache</span></span> | <span data-ttu-id="ff584-376">Se true, evita l'utilizzo di pacchetti memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="ff584-376">If true, avoids using cached packages.</span></span> <span data-ttu-id="ff584-377">Vedere [gestione dei pacchetti globali e delle cartelle della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="ff584-377">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="ff584-378">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="ff584-378">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="ff584-379">Se true, ignora le origini di pacchetti in errore o mancanti.</span><span class="sxs-lookup"><span data-stu-id="ff584-379">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="ff584-380">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="ff584-380">RestoreFallbackFolders</span></span> | <span data-ttu-id="ff584-381">Cartelle di fallback, utilizzate nello stesso modo in cui viene utilizzata la cartella Pacchetti utente.</span><span class="sxs-lookup"><span data-stu-id="ff584-381">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="ff584-382">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="ff584-382">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="ff584-383">Origini aggiuntive da utilizzare durante il ripristino.</span><span class="sxs-lookup"><span data-stu-id="ff584-383">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="ff584-384">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="ff584-384">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="ff584-385">Cartelle di fallback aggiuntive da usare durante il ripristino.</span><span class="sxs-lookup"><span data-stu-id="ff584-385">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="ff584-386">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="ff584-386">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="ff584-387">Esclude le cartelle di fallback specificate in `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="ff584-387">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="ff584-388">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="ff584-388">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="ff584-389">Percorso di `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="ff584-389">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="ff584-390">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="ff584-390">RestoreGraphProjectInput</span></span> | <span data-ttu-id="ff584-391">Elenco delimitato da punto e virgola dei progetti da ripristinare, che deve contenere percorsi assoluti.</span><span class="sxs-lookup"><span data-stu-id="ff584-391">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="ff584-392">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="ff584-392">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="ff584-393">Quando i progetti vengono raccolti tramite MSBuild, determina se vengono raccolti usando l' `SkipNonexistentTargets` ottimizzazione.</span><span class="sxs-lookup"><span data-stu-id="ff584-393">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="ff584-394">Quando non è impostato, il valore predefinito è `true` .</span><span class="sxs-lookup"><span data-stu-id="ff584-394">When not set, defaults to `true`.</span></span> <span data-ttu-id="ff584-395">La conseguenza è un comportamento non rapido quando le destinazioni di un progetto non possono essere importate.</span><span class="sxs-lookup"><span data-stu-id="ff584-395">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="ff584-396">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="ff584-396">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="ff584-397">Cartella di output, per impostazione predefinita `BaseIntermediateOutputPath` e la `obj` cartella.</span><span class="sxs-lookup"><span data-stu-id="ff584-397">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="ff584-398">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="ff584-398">RestoreForce</span></span> | <span data-ttu-id="ff584-399">Nei progetti basati su PackageReference, impone la risoluzione di tutte le dipendenze anche se l'ultimo ripristino ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="ff584-399">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="ff584-400">La specifica di questo flag è simile all'eliminazione del `project.assets.json` file.</span><span class="sxs-lookup"><span data-stu-id="ff584-400">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="ff584-401">Questa operazione non consente di ignorare la cache HTTP.</span><span class="sxs-lookup"><span data-stu-id="ff584-401">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="ff584-402">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="ff584-402">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="ff584-403">Optare per l'utilizzo di un file di blocco.</span><span class="sxs-lookup"><span data-stu-id="ff584-403">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="ff584-404">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="ff584-404">RestoreLockedMode</span></span> | <span data-ttu-id="ff584-405">Eseguire Restore in modalità bloccata.</span><span class="sxs-lookup"><span data-stu-id="ff584-405">Run restore in locked mode.</span></span> <span data-ttu-id="ff584-406">Questo significa che il ripristino non valuterà nuovamente le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="ff584-406">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="ff584-407">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="ff584-407">NuGetLockFilePath</span></span> | <span data-ttu-id="ff584-408">Percorso personalizzato per il file di blocco.</span><span class="sxs-lookup"><span data-stu-id="ff584-408">A custom location for the lock file.</span></span> <span data-ttu-id="ff584-409">Il percorso predefinito è accanto al progetto ed è denominato `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="ff584-409">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="ff584-410">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="ff584-410">RestoreForceEvaluate</span></span> | <span data-ttu-id="ff584-411">Forza il ripristino per ricalcolare le dipendenze e aggiornare il file di blocco senza alcun avviso.</span><span class="sxs-lookup"><span data-stu-id="ff584-411">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> | 

#### <a name="examples"></a><span data-ttu-id="ff584-412">Esempi</span><span class="sxs-lookup"><span data-stu-id="ff584-412">Examples</span></span>

<span data-ttu-id="ff584-413">Riga di comando:</span><span class="sxs-lookup"><span data-stu-id="ff584-413">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="ff584-414">File di progetto:</span><span class="sxs-lookup"><span data-stu-id="ff584-414">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="ff584-415">Output del ripristino</span><span class="sxs-lookup"><span data-stu-id="ff584-415">Restore outputs</span></span>

<span data-ttu-id="ff584-416">Il ripristino crea i file seguenti nella cartella `obj` di compilazione:</span><span class="sxs-lookup"><span data-stu-id="ff584-416">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="ff584-417">File</span><span class="sxs-lookup"><span data-stu-id="ff584-417">File</span></span> | <span data-ttu-id="ff584-418">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ff584-418">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="ff584-419">Contiene il grafico delle dipendenze di tutti i riferimenti ai pacchetti.</span><span class="sxs-lookup"><span data-stu-id="ff584-419">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="ff584-420">Riferimenti alle proprietà di MSBuild contenute nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="ff584-420">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="ff584-421">Riferimenti alle destinazioni di MSBuild contenute nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="ff584-421">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="ff584-422">Ripristino e compilazione con un comando MSBuild</span><span class="sxs-lookup"><span data-stu-id="ff584-422">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="ff584-423">A causa del fatto che NuGet può ripristinare i pacchetti che arrestano le destinazioni e le proprietà di MSBuild, le valutazioni di ripristino e compilazione vengono eseguite con proprietà globali diverse.</span><span class="sxs-lookup"><span data-stu-id="ff584-423">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="ff584-424">Ciò significa che le operazioni seguenti avranno un comportamento imprevedibile e spesso errato.</span><span class="sxs-lookup"><span data-stu-id="ff584-424">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="ff584-425">L'approccio consigliato è invece:</span><span class="sxs-lookup"><span data-stu-id="ff584-425">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="ff584-426">La stessa logica si applica ad altre destinazioni simili a `build` .</span><span class="sxs-lookup"><span data-stu-id="ff584-426">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="ff584-427">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="ff584-427">PackageTargetFallback</span></span>

<span data-ttu-id="ff584-428">L'elemento `PackageTargetFallback` consente di specificare un set di destinazioni compatibili da usare durante il ripristino di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="ff584-428">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="ff584-429">È progettato per consentire ai pacchetti che usano un [TxM](../reference/target-frameworks.md) dotnet di interagire con pacchetti compatibili che non dichiarano un TxM dotnet.</span><span class="sxs-lookup"><span data-stu-id="ff584-429">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="ff584-430">Se il progetto usa il TxM dotnet, devono averlo anche tutti i pacchetti da cui il progetto dipende, a meno che non si aggiunga `<PackageTargetFallback>` al progetto, in modo da rendere compatibili con dotnet le piattaforme che non lo sono.</span><span class="sxs-lookup"><span data-stu-id="ff584-430">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="ff584-431">Ad esempio, se il progetto usa il TxM `netstandard1.6` e un pacchetto dipendente contiene solo `lib/net45/a.dll` e `lib/portable-net45+win81/a.dll`, la compilazione del progetto avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="ff584-431">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="ff584-432">Se si vuole includere solo quest'ultima DLL, è possibile aggiungere un `PackageTargetFallback` come segue per segnalare che la DLL `portable-net45+win81` è compatibile:</span><span class="sxs-lookup"><span data-stu-id="ff584-432">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="ff584-433">Per dichiarare un fallback per tutte le destinazioni nel progetto, non specificare l'attributo `Condition`.</span><span class="sxs-lookup"><span data-stu-id="ff584-433">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="ff584-434">È anche possibile estendere qualsiasi `PackageTargetFallback` esistente includendo `$(PackageTargetFallback)` come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ff584-434">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="ff584-435">Sostituzione di una libreria da un grafico di ripristino</span><span class="sxs-lookup"><span data-stu-id="ff584-435">Replacing one library from a restore graph</span></span>

<span data-ttu-id="ff584-436">Se un ripristino restituisce l'assembly errato, è possibile escludere la scelta predefinita di tali pacchetti e sostituirla con la propria scelta.</span><span class="sxs-lookup"><span data-stu-id="ff584-436">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="ff584-437">Prima di tutto, con un `PackageReference` di livello superiore, escludere tutti gli asset:</span><span class="sxs-lookup"><span data-stu-id="ff584-437">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="ff584-438">Aggiungere quindi il riferimento personalizzato alla copia locale appropriata della DLL:</span><span class="sxs-lookup"><span data-stu-id="ff584-438">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
