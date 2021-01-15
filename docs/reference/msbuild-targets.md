---
title: Pack e restore di NuGet come destinazioni MSBuild
description: I comandi pack e restore di NuGet possono essere usati direttamente come destinazioni MSBuild con NuGet 4.0 +.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 7de3f0f1133a89848e9268d489751293fb3cbf25
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235698"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="6e118-103">Pack e restore di NuGet come destinazioni MSBuild</span><span class="sxs-lookup"><span data-stu-id="6e118-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="6e118-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="6e118-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="6e118-105">Con il formato [PackageReference](../consume-packages/package-references-in-project-files.md) , NuGet 4.0 + può archiviare tutti i metadati del manifesto direttamente all'interno di un file di progetto anziché usare un `.nuspec` file separato.</span><span class="sxs-lookup"><span data-stu-id="6e118-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="6e118-106">Con MSBuild 15.1 +, anche NuGet è un membro di MSBuild di prima classe con le destinazioni `pack` e `restore` come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="6e118-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="6e118-107">Queste destinazioni consentono di usare NuGet come qualsiasi altra attività o destinazione MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6e118-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="6e118-108">Per istruzioni sulla creazione di un pacchetto NuGet con MSBuild, vedere [creare un pacchetto NuGet con MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="6e118-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="6e118-109">Per NuGet 3.x e versioni precedenti, usare invece i comandi [pack](../reference/cli-reference/cli-ref-pack.md) e [restore](../reference/cli-reference/cli-ref-restore.md) tramite l'interfaccia della riga di comando di NuGet.</span><span class="sxs-lookup"><span data-stu-id="6e118-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="6e118-110">Ordine di compilazione delle destinazioni</span><span class="sxs-lookup"><span data-stu-id="6e118-110">Target build order</span></span>

<span data-ttu-id="6e118-111">Dato che `pack` e `restore` sono destinazioni MSBuild, è possibile accedervi per ottimizzare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6e118-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="6e118-112">Si supponga, ad esempio, di voler copiare il pacchetto in una condivisione di rete dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="6e118-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="6e118-113">È possibile farlo aggiungendo quanto segue nel file di progetto:</span><span class="sxs-lookup"><span data-stu-id="6e118-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="6e118-114">Analogamente, è possibile scrivere un'attività MSBuild, scrivere la propria destinazione e utilizzare proprietà NuGet nell'attività MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6e118-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="6e118-115">`$(OutputPath)` è relativo e prevede che si esegua il comando dalla radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="6e118-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="6e118-116">Destinazione pack</span><span class="sxs-lookup"><span data-stu-id="6e118-116">pack target</span></span>

<span data-ttu-id="6e118-117">Per .NET Standard progetti che usano il formato PackageReference, l'uso di `msbuild -t:pack` disegna gli input dal file di progetto da usare per la creazione di un pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="6e118-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="6e118-118">La tabella seguente descrive le proprietà di MSBuild che possono essere aggiunte a un file di progetto all'interno del primo nodo `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="6e118-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="6e118-119">È possibile apportare facilmente queste modifiche in Visual Studio 2017 e versioni successive facendo clic con il pulsante destro del mouse sul progetto e scegliendo **Modifica {nome_progetto}** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="6e118-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="6e118-120">Per praticità, la tabella è organizzata in base alla proprietà equivalente in un [ `.nuspec` file](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="6e118-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="6e118-121">Si noti che le proprietà `Owners` e `Summary` da `.nuspec` non sono supportate con MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6e118-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="6e118-122">Valore di attributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="6e118-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="6e118-123">Proprietà MSBuild</span><span class="sxs-lookup"><span data-stu-id="6e118-123">MSBuild Property</span></span> | <span data-ttu-id="6e118-124">Predefinito</span><span class="sxs-lookup"><span data-stu-id="6e118-124">Default</span></span> | <span data-ttu-id="6e118-125">Note</span><span class="sxs-lookup"><span data-stu-id="6e118-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="6e118-126">Id</span><span class="sxs-lookup"><span data-stu-id="6e118-126">Id</span></span> | <span data-ttu-id="6e118-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="6e118-127">PackageId</span></span> | <span data-ttu-id="6e118-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="6e118-128">AssemblyName</span></span> | <span data-ttu-id="6e118-129">$(AssemblyName) da MSBuild</span><span class="sxs-lookup"><span data-stu-id="6e118-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="6e118-130">Versione</span><span class="sxs-lookup"><span data-stu-id="6e118-130">Version</span></span> | <span data-ttu-id="6e118-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="6e118-131">PackageVersion</span></span> | <span data-ttu-id="6e118-132">Versione</span><span class="sxs-lookup"><span data-stu-id="6e118-132">Version</span></span> | <span data-ttu-id="6e118-133">Compatibile con SemVer, ad esempio "1.0.0", "1.0.0-beta" o "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="6e118-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="6e118-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="6e118-134">VersionPrefix</span></span> | <span data-ttu-id="6e118-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="6e118-135">PackageVersionPrefix</span></span> | <span data-ttu-id="6e118-136">empty</span><span class="sxs-lookup"><span data-stu-id="6e118-136">empty</span></span> | <span data-ttu-id="6e118-137">L'impostazione di PackageVersion sovrascrive PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="6e118-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="6e118-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="6e118-138">VersionSuffix</span></span> | <span data-ttu-id="6e118-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="6e118-139">PackageVersionSuffix</span></span> | <span data-ttu-id="6e118-140">empty</span><span class="sxs-lookup"><span data-stu-id="6e118-140">empty</span></span> | <span data-ttu-id="6e118-141">$(VersionSuffix) da MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6e118-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="6e118-142">L'impostazione di PackageVersion sovrascrive PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="6e118-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="6e118-143">Autori</span><span class="sxs-lookup"><span data-stu-id="6e118-143">Authors</span></span> | <span data-ttu-id="6e118-144">Autori</span><span class="sxs-lookup"><span data-stu-id="6e118-144">Authors</span></span> | <span data-ttu-id="6e118-145">Nome utente dell'utente corrente</span><span class="sxs-lookup"><span data-stu-id="6e118-145">Username of the current user</span></span> | |
| <span data-ttu-id="6e118-146">Proprietari</span><span class="sxs-lookup"><span data-stu-id="6e118-146">Owners</span></span> | <span data-ttu-id="6e118-147">N/D</span><span class="sxs-lookup"><span data-stu-id="6e118-147">N/A</span></span> | <span data-ttu-id="6e118-148">Non presente in NuSpec</span><span class="sxs-lookup"><span data-stu-id="6e118-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="6e118-149">Titolo</span><span class="sxs-lookup"><span data-stu-id="6e118-149">Title</span></span> | <span data-ttu-id="6e118-150">Titolo</span><span class="sxs-lookup"><span data-stu-id="6e118-150">Title</span></span> | <span data-ttu-id="6e118-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="6e118-151">The PackageId</span></span>| |
| <span data-ttu-id="6e118-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e118-152">Description</span></span> | <span data-ttu-id="6e118-153">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e118-153">Description</span></span> | <span data-ttu-id="6e118-154">"Descrizione del pacchetto"</span><span class="sxs-lookup"><span data-stu-id="6e118-154">"Package Description"</span></span> | |
| <span data-ttu-id="6e118-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="6e118-155">Copyright</span></span> | <span data-ttu-id="6e118-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="6e118-156">Copyright</span></span> | <span data-ttu-id="6e118-157">empty</span><span class="sxs-lookup"><span data-stu-id="6e118-157">empty</span></span> | |
| <span data-ttu-id="6e118-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="6e118-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="6e118-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="6e118-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="6e118-160">false</span><span class="sxs-lookup"><span data-stu-id="6e118-160">false</span></span> | |
| <span data-ttu-id="6e118-161">license</span><span class="sxs-lookup"><span data-stu-id="6e118-161">license</span></span> | <span data-ttu-id="6e118-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="6e118-162">PackageLicenseExpression</span></span> | <span data-ttu-id="6e118-163">empty</span><span class="sxs-lookup"><span data-stu-id="6e118-163">empty</span></span> | <span data-ttu-id="6e118-164">Corrisponde a `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="6e118-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="6e118-165">license</span><span class="sxs-lookup"><span data-stu-id="6e118-165">license</span></span> | <span data-ttu-id="6e118-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="6e118-166">PackageLicenseFile</span></span> | <span data-ttu-id="6e118-167">empty</span><span class="sxs-lookup"><span data-stu-id="6e118-167">empty</span></span> | <span data-ttu-id="6e118-168">Corrisponde a `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="6e118-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="6e118-169">È necessario comprimere in modo esplicito il file di licenza a cui si fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="6e118-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="6e118-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="6e118-170">LicenseUrl</span></span> | <span data-ttu-id="6e118-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="6e118-171">PackageLicenseUrl</span></span> | <span data-ttu-id="6e118-172">empty</span><span class="sxs-lookup"><span data-stu-id="6e118-172">empty</span></span> | <span data-ttu-id="6e118-173">`PackageLicenseUrl` è deprecato, usare la proprietà PackageLicenseExpression o PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="6e118-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="6e118-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="6e118-174">ProjectUrl</span></span> | <span data-ttu-id="6e118-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="6e118-175">PackageProjectUrl</span></span> | <span data-ttu-id="6e118-176">empty</span><span class="sxs-lookup"><span data-stu-id="6e118-176">empty</span></span> | |
| <span data-ttu-id="6e118-177">Icona</span><span class="sxs-lookup"><span data-stu-id="6e118-177">Icon</span></span> | <span data-ttu-id="6e118-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="6e118-178">PackageIcon</span></span> | <span data-ttu-id="6e118-179">empty</span><span class="sxs-lookup"><span data-stu-id="6e118-179">empty</span></span> | <span data-ttu-id="6e118-180">È necessario comprimere in modo esplicito il file di immagine icona a cui si fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="6e118-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="6e118-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="6e118-181">IconUrl</span></span> | <span data-ttu-id="6e118-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="6e118-182">PackageIconUrl</span></span> | <span data-ttu-id="6e118-183">empty</span><span class="sxs-lookup"><span data-stu-id="6e118-183">empty</span></span> | <span data-ttu-id="6e118-184">Per la migliore esperienza di livello inferiore, `PackageIconUrl` è necessario specificare oltre a `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="6e118-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="6e118-185">A lungo termine, `PackageIconUrl` verrà deprecato.</span><span class="sxs-lookup"><span data-stu-id="6e118-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="6e118-186">Tag</span><span class="sxs-lookup"><span data-stu-id="6e118-186">Tags</span></span> | <span data-ttu-id="6e118-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="6e118-187">PackageTags</span></span> | <span data-ttu-id="6e118-188">empty</span><span class="sxs-lookup"><span data-stu-id="6e118-188">empty</span></span> | <span data-ttu-id="6e118-189">I tag sono delimitati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="6e118-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="6e118-190">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="6e118-190">ReleaseNotes</span></span> | <span data-ttu-id="6e118-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="6e118-191">PackageReleaseNotes</span></span> | <span data-ttu-id="6e118-192">empty</span><span class="sxs-lookup"><span data-stu-id="6e118-192">empty</span></span> | |
| <span data-ttu-id="6e118-193">Repository/URL</span><span class="sxs-lookup"><span data-stu-id="6e118-193">Repository/Url</span></span> | <span data-ttu-id="6e118-194">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="6e118-194">RepositoryUrl</span></span> | <span data-ttu-id="6e118-195">empty</span><span class="sxs-lookup"><span data-stu-id="6e118-195">empty</span></span> | <span data-ttu-id="6e118-196">URL del repository usato per clonare o recuperare il codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="6e118-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="6e118-197">Esempio *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="6e118-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="6e118-198">Repository/tipo</span><span class="sxs-lookup"><span data-stu-id="6e118-198">Repository/Type</span></span> | <span data-ttu-id="6e118-199">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="6e118-199">RepositoryType</span></span> | <span data-ttu-id="6e118-200">empty</span><span class="sxs-lookup"><span data-stu-id="6e118-200">empty</span></span> | <span data-ttu-id="6e118-201">Tipo di repository.</span><span class="sxs-lookup"><span data-stu-id="6e118-201">Repository type.</span></span> <span data-ttu-id="6e118-202">Esempi: *git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="6e118-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="6e118-203">Repository/ramo</span><span class="sxs-lookup"><span data-stu-id="6e118-203">Repository/Branch</span></span> | <span data-ttu-id="6e118-204">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="6e118-204">RepositoryBranch</span></span> | <span data-ttu-id="6e118-205">empty</span><span class="sxs-lookup"><span data-stu-id="6e118-205">empty</span></span> | <span data-ttu-id="6e118-206">Informazioni facoltative sul ramo del repository.</span><span class="sxs-lookup"><span data-stu-id="6e118-206">Optional repository branch information.</span></span> <span data-ttu-id="6e118-207">Per includere questa proprietà, è necessario specificare anche *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="6e118-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="6e118-208">Esempio: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="6e118-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="6e118-209">Repository/commit</span><span class="sxs-lookup"><span data-stu-id="6e118-209">Repository/Commit</span></span> | <span data-ttu-id="6e118-210">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="6e118-210">RepositoryCommit</span></span> | <span data-ttu-id="6e118-211">empty</span><span class="sxs-lookup"><span data-stu-id="6e118-211">empty</span></span> | <span data-ttu-id="6e118-212">Commit o insieme di modifiche facoltativo del repository per indicare l'origine su cui è stato compilato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6e118-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="6e118-213">Per includere questa proprietà, è necessario specificare anche *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="6e118-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="6e118-214">Esempio: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="6e118-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="6e118-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="6e118-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="6e118-216">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="6e118-216">Summary</span></span> | <span data-ttu-id="6e118-217">Non supportato</span><span class="sxs-lookup"><span data-stu-id="6e118-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="6e118-218">Input destinazione pack</span><span class="sxs-lookup"><span data-stu-id="6e118-218">pack target inputs</span></span>

- <span data-ttu-id="6e118-219">IsPackable</span><span class="sxs-lookup"><span data-stu-id="6e118-219">IsPackable</span></span>
- <span data-ttu-id="6e118-220">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="6e118-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="6e118-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="6e118-221">PackageVersion</span></span>
- <span data-ttu-id="6e118-222">PackageId</span><span class="sxs-lookup"><span data-stu-id="6e118-222">PackageId</span></span>
- <span data-ttu-id="6e118-223">Autori</span><span class="sxs-lookup"><span data-stu-id="6e118-223">Authors</span></span>
- <span data-ttu-id="6e118-224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e118-224">Description</span></span>
- <span data-ttu-id="6e118-225">Copyright</span><span class="sxs-lookup"><span data-stu-id="6e118-225">Copyright</span></span>
- <span data-ttu-id="6e118-226">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="6e118-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="6e118-227">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="6e118-227">DevelopmentDependency</span></span>
- <span data-ttu-id="6e118-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="6e118-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="6e118-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="6e118-229">PackageLicenseFile</span></span>
- <span data-ttu-id="6e118-230">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="6e118-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="6e118-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="6e118-231">PackageProjectUrl</span></span>
- <span data-ttu-id="6e118-232">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="6e118-232">PackageIconUrl</span></span>
- <span data-ttu-id="6e118-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="6e118-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="6e118-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="6e118-234">PackageTags</span></span>
- <span data-ttu-id="6e118-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="6e118-235">PackageOutputPath</span></span>
- <span data-ttu-id="6e118-236">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="6e118-236">IncludeSymbols</span></span>
- <span data-ttu-id="6e118-237">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="6e118-237">IncludeSource</span></span>
- <span data-ttu-id="6e118-238">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="6e118-238">PackageTypes</span></span>
- <span data-ttu-id="6e118-239">IsTool</span><span class="sxs-lookup"><span data-stu-id="6e118-239">IsTool</span></span>
- <span data-ttu-id="6e118-240">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="6e118-240">RepositoryUrl</span></span>
- <span data-ttu-id="6e118-241">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="6e118-241">RepositoryType</span></span>
- <span data-ttu-id="6e118-242">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="6e118-242">RepositoryBranch</span></span>
- <span data-ttu-id="6e118-243">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="6e118-243">RepositoryCommit</span></span>
- <span data-ttu-id="6e118-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="6e118-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="6e118-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="6e118-245">MinClientVersion</span></span>
- <span data-ttu-id="6e118-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="6e118-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="6e118-247">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="6e118-247">IncludeContentInPack</span></span>
- <span data-ttu-id="6e118-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="6e118-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="6e118-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="6e118-249">ContentTargetFolders</span></span>
- <span data-ttu-id="6e118-250">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="6e118-250">NuspecFile</span></span>
- <span data-ttu-id="6e118-251">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="6e118-251">NuspecBasePath</span></span>
- <span data-ttu-id="6e118-252">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="6e118-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="6e118-253">Scenari pack</span><span class="sxs-lookup"><span data-stu-id="6e118-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="6e118-254">Non visualizzare le dipendenze</span><span class="sxs-lookup"><span data-stu-id="6e118-254">Suppress dependencies</span></span>

<span data-ttu-id="6e118-255">Per non visualizzare le dipendenze del pacchetto dal pacchetto NuGet generato, impostare `SuppressDependenciesWhenPacking` su `true` che consentirà di ignorare tutte le dipendenze dal file nupkg generato.</span><span class="sxs-lookup"><span data-stu-id="6e118-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="6e118-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="6e118-256">PackageIconUrl</span></span>

<span data-ttu-id="6e118-257">`PackageIconUrl` verrà deprecato a favore della nuova [`PackageIcon`](#packageicon) Proprietà.</span><span class="sxs-lookup"><span data-stu-id="6e118-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="6e118-258">A partire da NuGet 5,3 & Visual Studio 2019 versione 16,3, `pack` genererà un avviso [NU5048](./errors-and-warnings/nu5048.md) se i metadati del pacchetto specificano solo `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="6e118-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="6e118-259">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="6e118-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="6e118-260">È necessario specificare sia `PackageIcon` che `PackageIconUrl` per mantenere la compatibilità con le versioni precedenti di client e origini che non supportano ancora `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="6e118-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="6e118-261">Visual Studio supporterà `PackageIcon` i pacchetti provenienti da un'origine basata su cartelle in una versione futura.</span><span class="sxs-lookup"><span data-stu-id="6e118-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="6e118-262">Compressione di un file di immagine icona</span><span class="sxs-lookup"><span data-stu-id="6e118-262">Packing an icon image file</span></span>

<span data-ttu-id="6e118-263">Quando si imballa un file di immagine icona, è necessario utilizzare `PackageIcon` la proprietà per specificare il percorso del pacchetto, relativo alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6e118-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="6e118-264">Inoltre, è necessario assicurarsi che il file sia incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6e118-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="6e118-265">Le dimensioni del file di immagine sono limitate a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="6e118-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="6e118-266">I formati di file supportati sono JPEG e PNG.</span><span class="sxs-lookup"><span data-stu-id="6e118-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="6e118-267">Si consiglia la risoluzione di un'immagine di 128x128.</span><span class="sxs-lookup"><span data-stu-id="6e118-267">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="6e118-268">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6e118-268">For example:</span></span>

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

<span data-ttu-id="6e118-269">[Esempio di icona del pacchetto](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="6e118-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="6e118-270">Per l'equivalente NuSpec, vedere la pagina [di riferimento di nuspec per l'icona](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="6e118-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="6e118-271">Assembly di output</span><span class="sxs-lookup"><span data-stu-id="6e118-271">Output assemblies</span></span>

<span data-ttu-id="6e118-272">`nuget pack` copia i file di output con le estensioni `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="6e118-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="6e118-273">I file di output copiati dipendono da quanto fornito da MSBuild dalla destinazione `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="6e118-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="6e118-274">Sono disponibili due proprietà di MSBuild che è possibile usare nel file di progetto o nella riga di comando per controllare la destinazione degli assembly di output:</span><span class="sxs-lookup"><span data-stu-id="6e118-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="6e118-275">`IncludeBuildOutput`: valore booleano che determina se gli assembly di output della compilazione devono essere inclusi nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6e118-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="6e118-276">`BuildOutputTargetFolder`: specifica la cartella in cui devono essere posizionati gli assembly di output.</span><span class="sxs-lookup"><span data-stu-id="6e118-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="6e118-277">Gli assembly di output (e altri file di output) vengono copiati nelle rispettive cartelle per framework.</span><span class="sxs-lookup"><span data-stu-id="6e118-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="6e118-278">Riferimenti ai pacchetti</span><span class="sxs-lookup"><span data-stu-id="6e118-278">Package references</span></span>

<span data-ttu-id="6e118-279">Vedere [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="6e118-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="6e118-280">Riferimenti da progetto a progetto</span><span class="sxs-lookup"><span data-stu-id="6e118-280">Project to project references</span></span>

<span data-ttu-id="6e118-281">I riferimenti da progetto a progetto sono considerati per impostazione predefinita come riferimenti a pacchetti NuGet, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6e118-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="6e118-282">È anche possibile aggiungere i metadati seguenti ai riferimenti del progetto:</span><span class="sxs-lookup"><span data-stu-id="6e118-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="6e118-283">Inclusione di contenuto in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="6e118-283">Including content in a package</span></span>

<span data-ttu-id="6e118-284">Per includere il contenuto, aggiungere altri metadati all'elemento `<Content>` esistente.</span><span class="sxs-lookup"><span data-stu-id="6e118-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="6e118-285">Per impostazione predefinita tutti gli elementi di tipo"Content" vengono inclusi nel pacchetto, a meno che non si esegua l'override con voci simili al codice seguente:</span><span class="sxs-lookup"><span data-stu-id="6e118-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="6e118-286">Per impostazione predefinita, tutti gli elementi vengono aggiunti alla radice di `content` e della cartella `contentFiles\any\<target_framework>` all'interno di un pacchetto e viene mantenuta la struttura di cartelle relative, a meno che non si specifichi un percorso di pacchetto:</span><span class="sxs-lookup"><span data-stu-id="6e118-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="6e118-287">Se si vuole copiare tutto il contenuto sono in cartelle radice specifiche (invece di copiarlo sia in `content` che in `contentFiles`), è possibile usare la proprietà di MSBuild `ContentTargetFolders`, che ha il valore predefinito "content;contentFiles" ma può essere impostata su qualsiasi altro nome di cartella.</span><span class="sxs-lookup"><span data-stu-id="6e118-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="6e118-288">Si noti che se si specifica solo "contentFiles" in `ContentTargetFolders`, i file vengono posizionati in `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` in base a `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="6e118-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="6e118-289">`PackagePath` può essere un set di percorsi di destinazione delimitati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="6e118-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="6e118-290">Se si specifica un percorso di pacchetto vuoto, il file viene aggiunto alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6e118-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="6e118-291">Ad esempio, il codice seguente aggiunge `libuv.txt` a `content\myfiles`, `content\samples` e nella radice del pacchetto:</span><span class="sxs-lookup"><span data-stu-id="6e118-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="6e118-292">È disponibile anche una proprietà di MSBuild `$(IncludeContentInPack)`, con valore predefinito `true`.</span><span class="sxs-lookup"><span data-stu-id="6e118-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="6e118-293">Se questa proprietà viene impostata su `false` in qualsiasi progetto, il contenuto da tale progetto non viene incluso nel pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="6e118-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="6e118-294">Altri metadati specifici di pack che è possibile impostare per qualsiasi elemento precedente includono ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, che impostano i valori ```CopyToOutput``` e ```Flatten``` sulla voce ```contentFiles``` nel file nuspec di output.</span><span class="sxs-lookup"><span data-stu-id="6e118-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="6e118-295">Oltre agli elementi Content, i metadati `<Pack>` e `<PackagePath>` possono anche essere impostati nei file con l'azione di compilazione Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o None.</span><span class="sxs-lookup"><span data-stu-id="6e118-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="6e118-296">Per fare in modo che il comando pack aggiunga il nome del file al percorso del pacchetto quando si usano modelli con caratteri jolly (glob), il percorso del pacchetto deve terminare con il carattere separatore di cartella. In caso contrario, il percorso del pacchetto viene interpretato come percorso completo, incluso il nome del file.</span><span class="sxs-lookup"><span data-stu-id="6e118-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="6e118-297">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="6e118-297">IncludeSymbols</span></span>

<span data-ttu-id="6e118-298">Quando si usa `MSBuild -t:pack -p:IncludeSymbols=true`, i file `.pdb` corrispondenti vengono copiati insieme agli altri file di output (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="6e118-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="6e118-299">Si noti che l'impostazione `IncludeSymbols=true` crea un pacchetto regolare *e* un pacchetto di simboli.</span><span class="sxs-lookup"><span data-stu-id="6e118-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="6e118-300">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="6e118-300">IncludeSource</span></span>

<span data-ttu-id="6e118-301">Equivale a `IncludeSymbols`, ma insieme ai file `.pdb` vengono copiati anche i file di origine.</span><span class="sxs-lookup"><span data-stu-id="6e118-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="6e118-302">Tutti i file di tipo `Compile` vengono copiati in `src\<ProjectName>\` conservando la struttura di cartelle del percorso relativo nel pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="6e118-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="6e118-303">Lo stesso accade anche per i file di origine di qualsiasi `ProjectReference` con `TreatAsPackageReference` impostato su `false`.</span><span class="sxs-lookup"><span data-stu-id="6e118-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="6e118-304">Se un file di tipo Compile è all'esterno della cartella di progetto, viene semplicemente aggiunto a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="6e118-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="6e118-305">Compressione di un'espressione di licenza o di un file di licenza</span><span class="sxs-lookup"><span data-stu-id="6e118-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="6e118-306">Quando si usa un'espressione di licenza, è necessario usare la proprietà PackageLicenseExpression.</span><span class="sxs-lookup"><span data-stu-id="6e118-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="6e118-307">[Esempio di espressione di licenza](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="6e118-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="6e118-308">[Altre informazioni sulle espressioni di licenza e le licenze accettate da NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="6e118-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="6e118-309">Quando si imballa un file di licenza, è necessario utilizzare la proprietà PackageLicenseFile per specificare il percorso del pacchetto, relativo alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6e118-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="6e118-310">Inoltre, è necessario assicurarsi che il file sia incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6e118-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="6e118-311">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6e118-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="6e118-312">[Esempio di file di licenza](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="6e118-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="6e118-313">Compressione di un file senza estensione</span><span class="sxs-lookup"><span data-stu-id="6e118-313">Packing a file without an extension</span></span>

<span data-ttu-id="6e118-314">In alcuni scenari, ad esempio quando si imballa un file di licenza, potrebbe essere necessario includere un file senza estensione.</span><span class="sxs-lookup"><span data-stu-id="6e118-314">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="6e118-315">Per motivi cronologici, NuGet & MSBuild considera i percorsi senza un'estensione come directory.</span><span class="sxs-lookup"><span data-stu-id="6e118-315">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="6e118-316">[File senza un esempio di estensione](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="6e118-316">[File without an extension sample](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span></span>
### <a name="istool"></a><span data-ttu-id="6e118-317">IsTool</span><span class="sxs-lookup"><span data-stu-id="6e118-317">IsTool</span></span>

<span data-ttu-id="6e118-318">Quando si usa `MSBuild -t:pack -p:IsTool=true`, tutti i file, come specificato nello scenario [Assembly di output](#output-assemblies), vengono copiati nella cartella `tools` invece che nella cartella `lib`.</span><span class="sxs-lookup"><span data-stu-id="6e118-318">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="6e118-319">Si noti che questo comportamento è diverso da `DotNetCliTool`, che viene specificato impostando `PackageType` nel file `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="6e118-319">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="6e118-320">Creazione di un pacchetto con un file .nuspec</span><span class="sxs-lookup"><span data-stu-id="6e118-320">Packing using a .nuspec</span></span>

<span data-ttu-id="6e118-321">Sebbene sia consigliabile includere in alternativa [tutte le proprietà](../reference/msbuild-targets.md#pack-target) che in genere si trovano nel file del `.nuspec` progetto, è possibile scegliere di utilizzare un `.nuspec` file per comprimere il progetto.</span><span class="sxs-lookup"><span data-stu-id="6e118-321">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="6e118-322">Per un progetto non di tipo SDK che utilizza `PackageReference` , è necessario importare in `NuGet.Build.Tasks.Pack.targets` modo che l'attività Pack possa essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="6e118-322">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="6e118-323">Prima di poter comprimere un file nuspec, è ancora necessario ripristinare il progetto.</span><span class="sxs-lookup"><span data-stu-id="6e118-323">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="6e118-324">Un progetto di tipo SDK include le destinazioni di tipo pack per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="6e118-324">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="6e118-325">Il Framework di destinazione del file di progetto non è rilevante e non viene usato per la compressione di un NuSpec.</span><span class="sxs-lookup"><span data-stu-id="6e118-325">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="6e118-326">Le tre proprietà di MSBuild seguenti sono rilevanti per la creazione di pacchetti con un file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="6e118-326">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="6e118-327">`NuspecFile`: percorso relativo o assoluto per il file `.nuspec` usato per la creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6e118-327">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="6e118-328">`NuspecProperties`: elenco con valori delimitati da punto e virgola di coppie chiave=valore.</span><span class="sxs-lookup"><span data-stu-id="6e118-328">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="6e118-329">A causa della modalità di funzionamento dell'analisi della riga di comando di MSBuild, è necessario specificare più proprietà come indicato di seguito: `-p:NuspecProperties="key1=value1;key2=value2"`.</span><span class="sxs-lookup"><span data-stu-id="6e118-329">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="6e118-330">`NuspecBasePath`: percorso di base per il file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="6e118-330">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="6e118-331">Se si usa `dotnet.exe` per creare il pacchetto del progetto, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="6e118-331">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="6e118-332">Se si usa MSBuild per creare il pacchetto del progetto, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="6e118-332">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="6e118-333">Si noti che la compressione di un NuSpec tramite dotnet.exe o MSBuild comporta anche la compilazione del progetto per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="6e118-333">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="6e118-334">Questa operazione può essere evitata passando ```--no-build``` la proprietà a dotnet.exe, che è l'equivalente dell'impostazione ```<NoBuild>true</NoBuild> ``` nel file di progetto, insieme all'impostazione ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="6e118-334">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="6e118-335">Un esempio di file con estensione *csproj* per la compressione di un file nuspec è:</span><span class="sxs-lookup"><span data-stu-id="6e118-335">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="6e118-336">Punti di estensione avanzati per la creazione di pacchetti personalizzati</span><span class="sxs-lookup"><span data-stu-id="6e118-336">Advanced extension points to create customized package</span></span>

<span data-ttu-id="6e118-337">La `pack` destinazione fornisce due punti di estensione che vengono eseguiti nella compilazione specifica del Framework di destinazione interno.</span><span class="sxs-lookup"><span data-stu-id="6e118-337">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="6e118-338">I punti di estensione supportano l'inclusione di contenuto e assembly specifici del Framework di destinazione in un pacchetto:</span><span class="sxs-lookup"><span data-stu-id="6e118-338">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="6e118-339">`TargetsForTfmSpecificBuildOutput` destinazione: utilizzare per i file all'interno della `lib` cartella o in una cartella specificata utilizzando `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="6e118-339">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="6e118-340">`TargetsForTfmSpecificContentInPackage` destinazione: usare per i file all'esterno di `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="6e118-340">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="6e118-341">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="6e118-341">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="6e118-342">Scrivere una destinazione personalizzata e specificarla come valore della `$(TargetsForTfmSpecificBuildOutput)` Proprietà.</span><span class="sxs-lookup"><span data-stu-id="6e118-342">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="6e118-343">Per tutti i file che devono essere inseriti in `BuildOutputTargetFolder` (per impostazione predefinita, lib), la destinazione deve scrivere i file in ItemGroup `BuildOutputInPackage` e impostare i due valori di metadati seguenti:</span><span class="sxs-lookup"><span data-stu-id="6e118-343">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="6e118-344">`FinalOutputPath`: Percorso assoluto del file; Se non viene specificato, l'identità viene utilizzata per valutare il percorso di origine.</span><span class="sxs-lookup"><span data-stu-id="6e118-344">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="6e118-345">`TargetPath`: (Facoltativo) impostare quando il file deve essere inserito in una sottocartella all'interno di `lib\<TargetFramework>` , ad esempio gli assembly satellite che passano sotto le rispettive cartelle delle impostazioni cultura.</span><span class="sxs-lookup"><span data-stu-id="6e118-345">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="6e118-346">Il valore predefinito è il nome del file.</span><span class="sxs-lookup"><span data-stu-id="6e118-346">Defaults to the name of the file.</span></span>

<span data-ttu-id="6e118-347">Esempio:</span><span class="sxs-lookup"><span data-stu-id="6e118-347">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="6e118-348">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="6e118-348">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="6e118-349">Scrivere una destinazione personalizzata e specificarla come valore della `$(TargetsForTfmSpecificContentInPackage)` Proprietà.</span><span class="sxs-lookup"><span data-stu-id="6e118-349">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="6e118-350">Per tutti i file da includere nel pacchetto, la destinazione deve scrivere i file in ItemGroup `TfmSpecificPackageFile` e impostare i metadati facoltativi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6e118-350">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="6e118-351">`PackagePath`: Percorso in cui il file deve essere restituito nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6e118-351">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="6e118-352">NuGet genera un avviso se viene aggiunto più di un file allo stesso percorso del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6e118-352">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="6e118-353">`BuildAction`: L'azione di compilazione da assegnare al file, necessaria solo se il percorso del pacchetto si trova nella `contentFiles` cartella.</span><span class="sxs-lookup"><span data-stu-id="6e118-353">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="6e118-354">Il valore predefinito è "None".</span><span class="sxs-lookup"><span data-stu-id="6e118-354">Defaults to "None".</span></span>

<span data-ttu-id="6e118-355">Esempio:</span><span class="sxs-lookup"><span data-stu-id="6e118-355">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="6e118-356">Destinazione restore</span><span class="sxs-lookup"><span data-stu-id="6e118-356">restore target</span></span>

<span data-ttu-id="6e118-357">`MSBuild -t:restore` (usato da `nuget restore` e `dotnet restore` con progetti .NET Core) consente di ripristinare i pacchetti a cui si fa riferimento nel file di progetto, come segue:</span><span class="sxs-lookup"><span data-stu-id="6e118-357">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="6e118-358">Lettura di tutti i riferimenti da progetto a progetto</span><span class="sxs-lookup"><span data-stu-id="6e118-358">Read all project to project references</span></span>
1. <span data-ttu-id="6e118-359">Lettura delle proprietà del progetto per trovare la cartella intermedia e i framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="6e118-359">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="6e118-360">Passare dati MSBuild a NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="6e118-360">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="6e118-361">Esecuzione di restore</span><span class="sxs-lookup"><span data-stu-id="6e118-361">Run restore</span></span>
1. <span data-ttu-id="6e118-362">Download dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="6e118-362">Download packages</span></span>
1. <span data-ttu-id="6e118-363">Scrittura dei file di asset, delle destinazioni e delle proprietà</span><span class="sxs-lookup"><span data-stu-id="6e118-363">Write assets file, targets, and props</span></span>

<span data-ttu-id="6e118-364">La `restore` destinazione funziona per i progetti che usano il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6e118-364">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="6e118-365">`MSBuild 16.5+` dispone anche del supporto per il [consenso esplicito](#restoring-packagereference-and-packagesconfig-with-msbuild) per il `packages.config` formato.</span><span class="sxs-lookup"><span data-stu-id="6e118-365">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="6e118-366">La `restore` destinazione [non deve essere eseguita](#restoring-and-building-with-one-msbuild-command) in combinazione con la `build` destinazione.</span><span class="sxs-lookup"><span data-stu-id="6e118-366">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="6e118-367">Ripristino delle proprietà</span><span class="sxs-lookup"><span data-stu-id="6e118-367">Restore properties</span></span>

<span data-ttu-id="6e118-368">Possono esistere ulteriori impostazioni di ripristino derivate da proprietà di MSBuild nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="6e118-368">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="6e118-369">I valori possono essere impostati anche dalla riga di comando tramite l'opzione `-p:` (vedere gli esempi riportati di seguito).</span><span class="sxs-lookup"><span data-stu-id="6e118-369">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="6e118-370">Proprietà</span><span class="sxs-lookup"><span data-stu-id="6e118-370">Property</span></span> | <span data-ttu-id="6e118-371">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e118-371">Description</span></span> |
|--------|--------|
| <span data-ttu-id="6e118-372">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="6e118-372">RestoreSources</span></span> | <span data-ttu-id="6e118-373">Elenco delimitato da punto e virgola delle origini di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="6e118-373">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="6e118-374">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="6e118-374">RestorePackagesPath</span></span> | <span data-ttu-id="6e118-375">Percorso della cartella dei pacchetti dell'utente.</span><span class="sxs-lookup"><span data-stu-id="6e118-375">User packages folder path.</span></span> |
| <span data-ttu-id="6e118-376">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="6e118-376">RestoreDisableParallel</span></span> | <span data-ttu-id="6e118-377">Consente di limitare i download a uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="6e118-377">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="6e118-378">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="6e118-378">RestoreConfigFile</span></span> | <span data-ttu-id="6e118-379">Percorso per un file `Nuget.Config` da applicare.</span><span class="sxs-lookup"><span data-stu-id="6e118-379">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="6e118-380">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="6e118-380">RestoreNoCache</span></span> | <span data-ttu-id="6e118-381">Se true, evita l'utilizzo di pacchetti memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="6e118-381">If true, avoids using cached packages.</span></span> <span data-ttu-id="6e118-382">Vedere [gestione dei pacchetti globali e delle cartelle della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="6e118-382">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="6e118-383">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="6e118-383">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="6e118-384">Se true, ignora le origini di pacchetti in errore o mancanti.</span><span class="sxs-lookup"><span data-stu-id="6e118-384">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="6e118-385">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="6e118-385">RestoreFallbackFolders</span></span> | <span data-ttu-id="6e118-386">Cartelle di fallback, utilizzate nello stesso modo in cui viene utilizzata la cartella Pacchetti utente.</span><span class="sxs-lookup"><span data-stu-id="6e118-386">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="6e118-387">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="6e118-387">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="6e118-388">Origini aggiuntive da utilizzare durante il ripristino.</span><span class="sxs-lookup"><span data-stu-id="6e118-388">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="6e118-389">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="6e118-389">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="6e118-390">Cartelle di fallback aggiuntive da usare durante il ripristino.</span><span class="sxs-lookup"><span data-stu-id="6e118-390">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="6e118-391">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="6e118-391">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="6e118-392">Esclude le cartelle di fallback specificate in `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="6e118-392">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="6e118-393">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="6e118-393">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="6e118-394">Percorso di `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="6e118-394">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="6e118-395">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="6e118-395">RestoreGraphProjectInput</span></span> | <span data-ttu-id="6e118-396">Elenco delimitato da punto e virgola dei progetti da ripristinare, che deve contenere percorsi assoluti.</span><span class="sxs-lookup"><span data-stu-id="6e118-396">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="6e118-397">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="6e118-397">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="6e118-398">Quando i progetti vengono raccolti tramite MSBuild, determina se vengono raccolti usando l' `SkipNonexistentTargets` ottimizzazione.</span><span class="sxs-lookup"><span data-stu-id="6e118-398">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="6e118-399">Quando non è impostato, il valore predefinito è `true` .</span><span class="sxs-lookup"><span data-stu-id="6e118-399">When not set, defaults to `true`.</span></span> <span data-ttu-id="6e118-400">La conseguenza è un comportamento non rapido quando le destinazioni di un progetto non possono essere importate.</span><span class="sxs-lookup"><span data-stu-id="6e118-400">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="6e118-401">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="6e118-401">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="6e118-402">Cartella di output, per impostazione predefinita `BaseIntermediateOutputPath` e la `obj` cartella.</span><span class="sxs-lookup"><span data-stu-id="6e118-402">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="6e118-403">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="6e118-403">RestoreForce</span></span> | <span data-ttu-id="6e118-404">Nei progetti basati su PackageReference, impone la risoluzione di tutte le dipendenze anche se l'ultimo ripristino ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="6e118-404">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="6e118-405">La specifica di questo flag è simile all'eliminazione del `project.assets.json` file.</span><span class="sxs-lookup"><span data-stu-id="6e118-405">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="6e118-406">Questa operazione non consente di ignorare la cache HTTP.</span><span class="sxs-lookup"><span data-stu-id="6e118-406">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="6e118-407">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="6e118-407">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="6e118-408">Optare per l'utilizzo di un file di blocco.</span><span class="sxs-lookup"><span data-stu-id="6e118-408">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="6e118-409">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="6e118-409">RestoreLockedMode</span></span> | <span data-ttu-id="6e118-410">Eseguire Restore in modalità bloccata.</span><span class="sxs-lookup"><span data-stu-id="6e118-410">Run restore in locked mode.</span></span> <span data-ttu-id="6e118-411">Questo significa che il ripristino non valuterà nuovamente le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="6e118-411">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="6e118-412">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="6e118-412">NuGetLockFilePath</span></span> | <span data-ttu-id="6e118-413">Percorso personalizzato per il file di blocco.</span><span class="sxs-lookup"><span data-stu-id="6e118-413">A custom location for the lock file.</span></span> <span data-ttu-id="6e118-414">Il percorso predefinito è accanto al progetto ed è denominato `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="6e118-414">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="6e118-415">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="6e118-415">RestoreForceEvaluate</span></span> | <span data-ttu-id="6e118-416">Forza il ripristino per ricalcolare le dipendenze e aggiornare il file di blocco senza alcun avviso.</span><span class="sxs-lookup"><span data-stu-id="6e118-416">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="6e118-417">RestorePackagesConfig</span><span class="sxs-lookup"><span data-stu-id="6e118-417">RestorePackagesConfig</span></span> | <span data-ttu-id="6e118-418">Opzione di consenso esplicito che ripristina i progetti con packages.config. Supporto `MSBuild -t:restore` solo con.</span><span class="sxs-lookup"><span data-stu-id="6e118-418">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| <span data-ttu-id="6e118-419">RestoreUseStaticGraphEvaluation</span><span class="sxs-lookup"><span data-stu-id="6e118-419">RestoreUseStaticGraphEvaluation</span></span> | <span data-ttu-id="6e118-420">Un'opzione di consenso esplicito per l'uso della valutazione MSBuild del grafo statico anziché della valutazione standard.</span><span class="sxs-lookup"><span data-stu-id="6e118-420">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="6e118-421">La valutazione statica dei grafi è una funzionalità sperimentale molto più rapida per i repository e le soluzioni di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="6e118-421">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="6e118-422">Esempi</span><span class="sxs-lookup"><span data-stu-id="6e118-422">Examples</span></span>

<span data-ttu-id="6e118-423">Riga di comando:</span><span class="sxs-lookup"><span data-stu-id="6e118-423">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="6e118-424">File di progetto:</span><span class="sxs-lookup"><span data-stu-id="6e118-424">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="6e118-425">Output del ripristino</span><span class="sxs-lookup"><span data-stu-id="6e118-425">Restore outputs</span></span>

<span data-ttu-id="6e118-426">Il ripristino crea i file seguenti nella cartella `obj` di compilazione:</span><span class="sxs-lookup"><span data-stu-id="6e118-426">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="6e118-427">File</span><span class="sxs-lookup"><span data-stu-id="6e118-427">File</span></span> | <span data-ttu-id="6e118-428">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6e118-428">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="6e118-429">Contiene il grafico delle dipendenze di tutti i riferimenti ai pacchetti.</span><span class="sxs-lookup"><span data-stu-id="6e118-429">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="6e118-430">Riferimenti alle proprietà di MSBuild contenute nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="6e118-430">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="6e118-431">Riferimenti alle destinazioni di MSBuild contenute nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="6e118-431">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="6e118-432">Ripristino e compilazione con un comando MSBuild</span><span class="sxs-lookup"><span data-stu-id="6e118-432">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="6e118-433">A causa del fatto che NuGet può ripristinare i pacchetti che arrestano le destinazioni e le proprietà di MSBuild, le valutazioni di ripristino e compilazione vengono eseguite con proprietà globali diverse.</span><span class="sxs-lookup"><span data-stu-id="6e118-433">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="6e118-434">Ciò significa che le operazioni seguenti avranno un comportamento imprevedibile e spesso errato.</span><span class="sxs-lookup"><span data-stu-id="6e118-434">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="6e118-435">L'approccio consigliato è invece:</span><span class="sxs-lookup"><span data-stu-id="6e118-435">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="6e118-436">La stessa logica si applica ad altre destinazioni simili a `build` .</span><span class="sxs-lookup"><span data-stu-id="6e118-436">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="6e118-437">Ripristino di PackageReference e packages.config con MSBuild</span><span class="sxs-lookup"><span data-stu-id="6e118-437">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="6e118-438">Con MSBuild 16.5 +, packages.config sono supportati anche per `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="6e118-438">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="6e118-439">`packages.config` il ripristino è disponibile solo con `MSBuild 16.5+` e non con `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="6e118-439">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="6e118-440">Ripristino con la valutazione statica Graph di MSBuild</span><span class="sxs-lookup"><span data-stu-id="6e118-440">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="6e118-441">Con MSBuild 16,6 +, NuGet ha aggiunto una funzionalità sperimentale per usare la valutazione statica dei grafi dalla riga di comando che migliora significativamente il tempo di ripristino per i repository di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="6e118-441">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="6e118-442">In alternativa, è possibile abilitarla impostando la proprietà in un oggetto directory. Build. props.</span><span class="sxs-lookup"><span data-stu-id="6e118-442">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="6e118-443">A partire da Visual Studio 2019. x e NuGet 5. x, questa funzionalità è considerata sperimentale e acconsentito esplicitamente.</span><span class="sxs-lookup"><span data-stu-id="6e118-443">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="6e118-444">Per informazioni dettagliate su quando questa funzionalità sarà abilitata per impostazione predefinita, seguire [NuGet/Home # 9803](https://github.com/NuGet/Home/issues/9803) .</span><span class="sxs-lookup"><span data-stu-id="6e118-444">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="6e118-445">Il ripristino statico del grafo modifica la parte MSBuild del ripristino, la lettura e la valutazione del progetto, ma non l'algoritmo di ripristino.</span><span class="sxs-lookup"><span data-stu-id="6e118-445">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="6e118-446">L'algoritmo di ripristino è lo stesso in tutti gli strumenti NuGet (NuGet.exe, MSBuild.exe, dotnet.exe e Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="6e118-446">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="6e118-447">In pochissimi scenari, il ripristino statico del grafico può comportarsi in modo diverso rispetto al ripristino corrente e alcuni PackageReferences o ProjectReference dichiarati potrebbero essere mancanti.</span><span class="sxs-lookup"><span data-stu-id="6e118-447">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="6e118-448">Per facilitare il controllo, in caso di verifica di una sola volta, quando si esegue la migrazione a un ripristino statico del grafo, provare a eseguire:</span><span class="sxs-lookup"><span data-stu-id="6e118-448">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="6e118-449">NuGet *non* deve segnalare alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="6e118-449">NuGet should *not* report any changes.</span></span> <span data-ttu-id="6e118-450">Se viene visualizzata una discrepanza, inviare un problema in [NuGet/Home](https://github.com/nuget/home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="6e118-450">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="6e118-451">Sostituzione di una libreria da un grafico di ripristino</span><span class="sxs-lookup"><span data-stu-id="6e118-451">Replacing one library from a restore graph</span></span>

<span data-ttu-id="6e118-452">Se un ripristino restituisce l'assembly errato, è possibile escludere la scelta predefinita di tali pacchetti e sostituirla con la propria scelta.</span><span class="sxs-lookup"><span data-stu-id="6e118-452">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="6e118-453">Prima di tutto, con un `PackageReference` di livello superiore, escludere tutti gli asset:</span><span class="sxs-lookup"><span data-stu-id="6e118-453">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="6e118-454">Aggiungere quindi il riferimento personalizzato alla copia locale appropriata della DLL:</span><span class="sxs-lookup"><span data-stu-id="6e118-454">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
