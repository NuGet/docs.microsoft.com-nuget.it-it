---
title: Pack e restore di NuGet come destinazioni MSBuild
description: I comandi pack e restore di NuGet possono essere usati direttamente come destinazioni MSBuild con NuGet 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 6a49e410617c14e22f0d4a67d8bfe280f64f5505
ms.sourcegitcommit: 8a424829b1f70cf7590e95db61997af6ae2d7a41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72510801"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="5017e-103">Pack e restore di NuGet come destinazioni MSBuild</span><span class="sxs-lookup"><span data-stu-id="5017e-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="5017e-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="5017e-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="5017e-105">Con il formato [PackageReference](../consume-packages/package-references-in-project-files.md) , NuGet 4.0 + può archiviare tutti i metadati del manifesto direttamente all'interno di un file di progetto anziché usare un file separato `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="5017e-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="5017e-106">Con MSBuild 15.1 +, anche NuGet è un membro di MSBuild di prima classe con le destinazioni `pack` e `restore` come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="5017e-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="5017e-107">Queste destinazioni consentono di usare NuGet come qualsiasi altra attività o destinazione MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5017e-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="5017e-108">Per istruzioni sulla creazione di un pacchetto NuGet con MSBuild, vedere [creare un pacchetto NuGet con MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="5017e-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="5017e-109">Per NuGet 3.x e versioni precedenti, usare invece i comandi [pack](../reference/cli-reference/cli-ref-pack.md) e [restore](../reference/cli-reference/cli-ref-restore.md) tramite l'interfaccia della riga di comando di NuGet.</span><span class="sxs-lookup"><span data-stu-id="5017e-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="5017e-110">Ordine di compilazione delle destinazioni</span><span class="sxs-lookup"><span data-stu-id="5017e-110">Target build order</span></span>

<span data-ttu-id="5017e-111">Dato che `pack` e `restore` sono destinazioni MSBuild, è possibile accedervi per ottimizzare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="5017e-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="5017e-112">Si supponga, ad esempio, di voler copiare il pacchetto in una condivisione di rete dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="5017e-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="5017e-113">È possibile farlo aggiungendo quanto segue nel file di progetto:</span><span class="sxs-lookup"><span data-stu-id="5017e-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="5017e-114">Analogamente, è possibile scrivere un'attività MSBuild, scrivere la propria destinazione e utilizzare proprietà NuGet nell'attività MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5017e-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="5017e-115">`$(OutputPath)` è relativo e prevede che venga eseguito il comando dalla radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="5017e-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="5017e-116">Destinazione pack</span><span class="sxs-lookup"><span data-stu-id="5017e-116">pack target</span></span>

<span data-ttu-id="5017e-117">Per .NET Standard progetti che usano il formato PackageReference, l'uso di `msbuild -t:pack` disegna gli input dal file di progetto da usare per la creazione di un pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="5017e-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="5017e-118">La tabella seguente descrive le proprietà di MSBuild che possono essere aggiunte a un file di progetto all'interno del primo nodo `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="5017e-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="5017e-119">È possibile apportare facilmente queste modifiche in Visual Studio 2017 e versioni successive facendo clic con il pulsante destro del mouse sul progetto e scegliendo **Modifica {nome_progetto}** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="5017e-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="5017e-120">Per praticità, la tabella è organizzata in base alla proprietà equivalente in un [file `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="5017e-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="5017e-121">Si noti che le proprietà `Owners` e `Summary` da `.nuspec` non sono supportate con MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5017e-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="5017e-122">Valore di attributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="5017e-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="5017e-123">Proprietà MSBuild</span><span class="sxs-lookup"><span data-stu-id="5017e-123">MSBuild Property</span></span> | <span data-ttu-id="5017e-124">Impostazione predefinita</span><span class="sxs-lookup"><span data-stu-id="5017e-124">Default</span></span> | <span data-ttu-id="5017e-125">Note</span><span class="sxs-lookup"><span data-stu-id="5017e-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="5017e-126">Id</span><span class="sxs-lookup"><span data-stu-id="5017e-126">Id</span></span> | <span data-ttu-id="5017e-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="5017e-127">PackageId</span></span> | <span data-ttu-id="5017e-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="5017e-128">AssemblyName</span></span> | <span data-ttu-id="5017e-129">$(AssemblyName) da MSBuild</span><span class="sxs-lookup"><span data-stu-id="5017e-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="5017e-130">Versione</span><span class="sxs-lookup"><span data-stu-id="5017e-130">Version</span></span> | <span data-ttu-id="5017e-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="5017e-131">PackageVersion</span></span> | <span data-ttu-id="5017e-132">Versione</span><span class="sxs-lookup"><span data-stu-id="5017e-132">Version</span></span> | <span data-ttu-id="5017e-133">Compatibile con SemVer, ad esempio "1.0.0", "1.0.0-beta" o "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="5017e-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="5017e-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5017e-134">VersionPrefix</span></span> | <span data-ttu-id="5017e-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5017e-135">PackageVersionPrefix</span></span> | <span data-ttu-id="5017e-136">vuoto</span><span class="sxs-lookup"><span data-stu-id="5017e-136">empty</span></span> | <span data-ttu-id="5017e-137">L'impostazione di PackageVersion sovrascrive PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5017e-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="5017e-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5017e-138">VersionSuffix</span></span> | <span data-ttu-id="5017e-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5017e-139">PackageVersionSuffix</span></span> | <span data-ttu-id="5017e-140">vuoto</span><span class="sxs-lookup"><span data-stu-id="5017e-140">empty</span></span> | <span data-ttu-id="5017e-141">$(VersionSuffix) da MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5017e-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="5017e-142">L'impostazione di PackageVersion sovrascrive PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5017e-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="5017e-143">Autori</span><span class="sxs-lookup"><span data-stu-id="5017e-143">Authors</span></span> | <span data-ttu-id="5017e-144">Autori</span><span class="sxs-lookup"><span data-stu-id="5017e-144">Authors</span></span> | <span data-ttu-id="5017e-145">Nome utente dell'utente corrente</span><span class="sxs-lookup"><span data-stu-id="5017e-145">Username of the current user</span></span> | |
| <span data-ttu-id="5017e-146">Proprietari</span><span class="sxs-lookup"><span data-stu-id="5017e-146">Owners</span></span> | <span data-ttu-id="5017e-147">N/D</span><span class="sxs-lookup"><span data-stu-id="5017e-147">N/A</span></span> | <span data-ttu-id="5017e-148">Non presente in NuSpec</span><span class="sxs-lookup"><span data-stu-id="5017e-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="5017e-149">Titolo</span><span class="sxs-lookup"><span data-stu-id="5017e-149">Title</span></span> | <span data-ttu-id="5017e-150">Titolo</span><span class="sxs-lookup"><span data-stu-id="5017e-150">Title</span></span> | <span data-ttu-id="5017e-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="5017e-151">The PackageId</span></span>| |
| <span data-ttu-id="5017e-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5017e-152">Description</span></span> | <span data-ttu-id="5017e-153">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5017e-153">Description</span></span> | <span data-ttu-id="5017e-154">"Descrizione del pacchetto"</span><span class="sxs-lookup"><span data-stu-id="5017e-154">"Package Description"</span></span> | |
| <span data-ttu-id="5017e-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="5017e-155">Copyright</span></span> | <span data-ttu-id="5017e-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="5017e-156">Copyright</span></span> | <span data-ttu-id="5017e-157">vuoto</span><span class="sxs-lookup"><span data-stu-id="5017e-157">empty</span></span> | |
| <span data-ttu-id="5017e-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5017e-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="5017e-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5017e-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="5017e-160">False</span><span class="sxs-lookup"><span data-stu-id="5017e-160">false</span></span> | |
| <span data-ttu-id="5017e-161">licenza</span><span class="sxs-lookup"><span data-stu-id="5017e-161">license</span></span> | <span data-ttu-id="5017e-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="5017e-162">PackageLicenseExpression</span></span> | <span data-ttu-id="5017e-163">vuoto</span><span class="sxs-lookup"><span data-stu-id="5017e-163">empty</span></span> | <span data-ttu-id="5017e-164">Corrisponde a `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="5017e-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="5017e-165">licenza</span><span class="sxs-lookup"><span data-stu-id="5017e-165">license</span></span> | <span data-ttu-id="5017e-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="5017e-166">PackageLicenseFile</span></span> | <span data-ttu-id="5017e-167">vuoto</span><span class="sxs-lookup"><span data-stu-id="5017e-167">empty</span></span> | <span data-ttu-id="5017e-168">Corrisponde a `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="5017e-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="5017e-169">Potrebbe essere necessario comprimere in modo esplicito il file di licenza a cui si fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="5017e-169">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="5017e-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5017e-170">LicenseUrl</span></span> | <span data-ttu-id="5017e-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5017e-171">PackageLicenseUrl</span></span> | <span data-ttu-id="5017e-172">vuoto</span><span class="sxs-lookup"><span data-stu-id="5017e-172">empty</span></span> | <span data-ttu-id="5017e-173">`PackageLicenseUrl` è deprecato, utilizzare la proprietà PackageLicenseExpression o PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="5017e-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="5017e-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5017e-174">ProjectUrl</span></span> | <span data-ttu-id="5017e-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5017e-175">PackageProjectUrl</span></span> | <span data-ttu-id="5017e-176">vuoto</span><span class="sxs-lookup"><span data-stu-id="5017e-176">empty</span></span> | |
| <span data-ttu-id="5017e-177">Icona</span><span class="sxs-lookup"><span data-stu-id="5017e-177">Icon</span></span> | <span data-ttu-id="5017e-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="5017e-178">PackageIcon</span></span> | <span data-ttu-id="5017e-179">vuoto</span><span class="sxs-lookup"><span data-stu-id="5017e-179">empty</span></span> | <span data-ttu-id="5017e-180">Potrebbe essere necessario comprimere in modo esplicito il file di immagine icona a cui si fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="5017e-180">You may need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="5017e-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="5017e-181">IconUrl</span></span> | <span data-ttu-id="5017e-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5017e-182">PackageIconUrl</span></span> | <span data-ttu-id="5017e-183">vuoto</span><span class="sxs-lookup"><span data-stu-id="5017e-183">empty</span></span> | <span data-ttu-id="5017e-184">`PackageIconUrl` è deprecato, utilizzare la proprietà PackageIcon</span><span class="sxs-lookup"><span data-stu-id="5017e-184">`PackageIconUrl` is deprecated, use the PackageIcon property</span></span> |
| <span data-ttu-id="5017e-185">Tag</span><span class="sxs-lookup"><span data-stu-id="5017e-185">Tags</span></span> | <span data-ttu-id="5017e-186">PackageTags</span><span class="sxs-lookup"><span data-stu-id="5017e-186">PackageTags</span></span> | <span data-ttu-id="5017e-187">vuoto</span><span class="sxs-lookup"><span data-stu-id="5017e-187">empty</span></span> | <span data-ttu-id="5017e-188">I tag sono delimitati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="5017e-188">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="5017e-189">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5017e-189">ReleaseNotes</span></span> | <span data-ttu-id="5017e-190">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5017e-190">PackageReleaseNotes</span></span> | <span data-ttu-id="5017e-191">vuoto</span><span class="sxs-lookup"><span data-stu-id="5017e-191">empty</span></span> | |
| <span data-ttu-id="5017e-192">Repository/URL</span><span class="sxs-lookup"><span data-stu-id="5017e-192">Repository/Url</span></span> | <span data-ttu-id="5017e-193">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="5017e-193">RepositoryUrl</span></span> | <span data-ttu-id="5017e-194">vuoto</span><span class="sxs-lookup"><span data-stu-id="5017e-194">empty</span></span> | <span data-ttu-id="5017e-195">URL del repository usato per clonare o recuperare il codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="5017e-195">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="5017e-196">Esempio: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="5017e-196">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="5017e-197">Repository/tipo</span><span class="sxs-lookup"><span data-stu-id="5017e-197">Repository/Type</span></span> | <span data-ttu-id="5017e-198">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="5017e-198">RepositoryType</span></span> | <span data-ttu-id="5017e-199">vuoto</span><span class="sxs-lookup"><span data-stu-id="5017e-199">empty</span></span> | <span data-ttu-id="5017e-200">Tipo di repository.</span><span class="sxs-lookup"><span data-stu-id="5017e-200">Repository type.</span></span> <span data-ttu-id="5017e-201">Esempi: *git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="5017e-201">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="5017e-202">Repository/ramo</span><span class="sxs-lookup"><span data-stu-id="5017e-202">Repository/Branch</span></span> | <span data-ttu-id="5017e-203">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="5017e-203">RepositoryBranch</span></span> | <span data-ttu-id="5017e-204">vuoto</span><span class="sxs-lookup"><span data-stu-id="5017e-204">empty</span></span> | <span data-ttu-id="5017e-205">Informazioni facoltative sul ramo del repository.</span><span class="sxs-lookup"><span data-stu-id="5017e-205">Optional repository branch information.</span></span> <span data-ttu-id="5017e-206">Per includere questa proprietà, è necessario specificare anche *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="5017e-206">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="5017e-207">Esempio: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="5017e-207">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="5017e-208">Repository/commit</span><span class="sxs-lookup"><span data-stu-id="5017e-208">Repository/Commit</span></span> | <span data-ttu-id="5017e-209">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="5017e-209">RepositoryCommit</span></span> | <span data-ttu-id="5017e-210">vuoto</span><span class="sxs-lookup"><span data-stu-id="5017e-210">empty</span></span> | <span data-ttu-id="5017e-211">Commit o insieme di modifiche facoltativo del repository per indicare l'origine su cui è stato compilato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5017e-211">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="5017e-212">Per includere questa proprietà, è necessario specificare anche *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="5017e-212">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="5017e-213">Esempio: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="5017e-213">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="5017e-214">PackageType</span><span class="sxs-lookup"><span data-stu-id="5017e-214">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="5017e-215">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="5017e-215">Summary</span></span> | <span data-ttu-id="5017e-216">Non supportato</span><span class="sxs-lookup"><span data-stu-id="5017e-216">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="5017e-217">Input destinazione pack</span><span class="sxs-lookup"><span data-stu-id="5017e-217">pack target inputs</span></span>

- <span data-ttu-id="5017e-218">IsPackable</span><span class="sxs-lookup"><span data-stu-id="5017e-218">IsPackable</span></span>
- <span data-ttu-id="5017e-219">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="5017e-219">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="5017e-220">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="5017e-220">PackageVersion</span></span>
- <span data-ttu-id="5017e-221">PackageId</span><span class="sxs-lookup"><span data-stu-id="5017e-221">PackageId</span></span>
- <span data-ttu-id="5017e-222">Autori</span><span class="sxs-lookup"><span data-stu-id="5017e-222">Authors</span></span>
- <span data-ttu-id="5017e-223">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5017e-223">Description</span></span>
- <span data-ttu-id="5017e-224">Copyright</span><span class="sxs-lookup"><span data-stu-id="5017e-224">Copyright</span></span>
- <span data-ttu-id="5017e-225">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5017e-225">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="5017e-226">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="5017e-226">DevelopmentDependency</span></span>
- <span data-ttu-id="5017e-227">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="5017e-227">PackageLicenseExpression</span></span>
- <span data-ttu-id="5017e-228">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="5017e-228">PackageLicenseFile</span></span>
- <span data-ttu-id="5017e-229">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5017e-229">PackageLicenseUrl</span></span>
- <span data-ttu-id="5017e-230">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5017e-230">PackageProjectUrl</span></span>
- <span data-ttu-id="5017e-231">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5017e-231">PackageIconUrl</span></span>
- <span data-ttu-id="5017e-232">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5017e-232">PackageReleaseNotes</span></span>
- <span data-ttu-id="5017e-233">PackageTags</span><span class="sxs-lookup"><span data-stu-id="5017e-233">PackageTags</span></span>
- <span data-ttu-id="5017e-234">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="5017e-234">PackageOutputPath</span></span>
- <span data-ttu-id="5017e-235">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="5017e-235">IncludeSymbols</span></span>
- <span data-ttu-id="5017e-236">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="5017e-236">IncludeSource</span></span>
- <span data-ttu-id="5017e-237">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="5017e-237">PackageTypes</span></span>
- <span data-ttu-id="5017e-238">IsTool</span><span class="sxs-lookup"><span data-stu-id="5017e-238">IsTool</span></span>
- <span data-ttu-id="5017e-239">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="5017e-239">RepositoryUrl</span></span>
- <span data-ttu-id="5017e-240">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="5017e-240">RepositoryType</span></span>
- <span data-ttu-id="5017e-241">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="5017e-241">RepositoryBranch</span></span>
- <span data-ttu-id="5017e-242">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="5017e-242">RepositoryCommit</span></span>
- <span data-ttu-id="5017e-243">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="5017e-243">NoPackageAnalysis</span></span>
- <span data-ttu-id="5017e-244">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="5017e-244">MinClientVersion</span></span>
- <span data-ttu-id="5017e-245">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="5017e-245">IncludeBuildOutput</span></span>
- <span data-ttu-id="5017e-246">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="5017e-246">IncludeContentInPack</span></span>
- <span data-ttu-id="5017e-247">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="5017e-247">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="5017e-248">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="5017e-248">ContentTargetFolders</span></span>
- <span data-ttu-id="5017e-249">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="5017e-249">NuspecFile</span></span>
- <span data-ttu-id="5017e-250">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="5017e-250">NuspecBasePath</span></span>
- <span data-ttu-id="5017e-251">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="5017e-251">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="5017e-252">Scenari pack</span><span class="sxs-lookup"><span data-stu-id="5017e-252">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="5017e-253">Non visualizzare le dipendenze</span><span class="sxs-lookup"><span data-stu-id="5017e-253">Suppress dependencies</span></span>

<span data-ttu-id="5017e-254">Per non visualizzare le dipendenze del pacchetto dal pacchetto NuGet generato, impostare `SuppressDependenciesWhenPacking` su `true` che consentirà di ignorare tutte le dipendenze dal file nupkg generato.</span><span class="sxs-lookup"><span data-stu-id="5017e-254">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="5017e-255">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5017e-255">PackageIconUrl</span></span>

> [!Important]
> <span data-ttu-id="5017e-256">PackageIconUrl è deprecato con NuGet 5.3 + & Visual Studio 2019 versione 16,3 +.</span><span class="sxs-lookup"><span data-stu-id="5017e-256">PackageIconUrl is deprecated with NuGet 5.3+ & Visual Studio 2019 version 16.3+.</span></span> <span data-ttu-id="5017e-257">In alternativa, usare [PackageIcon](#packing-an-icon-image-file) .</span><span class="sxs-lookup"><span data-stu-id="5017e-257">Use [PackageIcon](#packing-an-icon-image-file) instead.</span></span>

### <a name="packing-an-icon-image-file"></a><span data-ttu-id="5017e-258">Compressione di un file di immagine icona</span><span class="sxs-lookup"><span data-stu-id="5017e-258">Packing an icon image file</span></span>

<span data-ttu-id="5017e-259">Quando si imballa un file di immagine icona, è necessario utilizzare la proprietà PackageIcon per specificare il percorso del pacchetto, relativo alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5017e-259">When packing an icon image file, you need to use PackageIcon property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="5017e-260">Inoltre, è necessario assicurarsi che il file sia incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5017e-260">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="5017e-261">Le dimensioni del file di immagine sono limitate a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="5017e-261">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="5017e-262">I formati di file supportati sono JPEG e PNG.</span><span class="sxs-lookup"><span data-stu-id="5017e-262">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="5017e-263">Si consiglia la risoluzione di un'immagine di 64x64.</span><span class="sxs-lookup"><span data-stu-id="5017e-263">We recommend an image resolution of 64x64.</span></span>

<span data-ttu-id="5017e-264">Esempio:</span><span class="sxs-lookup"><span data-stu-id="5017e-264">For example:</span></span>

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

<span data-ttu-id="5017e-265">[Esempio di icona del pacchetto](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="5017e-265">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="5017e-266">Per l'equivalente NuSpec, vedere la pagina [di riferimento di nuspec per l'icona](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="5017e-266">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="5017e-267">Assembly di output</span><span class="sxs-lookup"><span data-stu-id="5017e-267">Output assemblies</span></span>

<span data-ttu-id="5017e-268">`nuget pack` copia i file di output con le estensioni `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="5017e-268">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="5017e-269">I file di output copiati dipendono da quanto fornito da MSBuild dalla destinazione `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="5017e-269">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="5017e-270">Sono disponibili due proprietà di MSBuild che è possibile usare nel file di progetto o nella riga di comando per controllare la destinazione degli assembly di output:</span><span class="sxs-lookup"><span data-stu-id="5017e-270">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="5017e-271">`IncludeBuildOutput`: valore booleano che determina se gli assembly di output della compilazione devono essere inclusi nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5017e-271">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="5017e-272">`BuildOutputTargetFolder`: specifica la cartella in cui devono essere posizionati gli assembly di output.</span><span class="sxs-lookup"><span data-stu-id="5017e-272">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="5017e-273">Gli assembly di output (e altri file di output) vengono copiati nelle rispettive cartelle per framework.</span><span class="sxs-lookup"><span data-stu-id="5017e-273">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="5017e-274">Riferimenti ai pacchetti</span><span class="sxs-lookup"><span data-stu-id="5017e-274">Package references</span></span>

<span data-ttu-id="5017e-275">Vedere [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="5017e-275">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="5017e-276">Riferimenti da progetto a progetto</span><span class="sxs-lookup"><span data-stu-id="5017e-276">Project to project references</span></span>

<span data-ttu-id="5017e-277">I riferimenti da progetto a progetto sono considerati per impostazione predefinita come riferimenti a pacchetti NuGet, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="5017e-277">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="5017e-278">È anche possibile aggiungere i metadati seguenti ai riferimenti del progetto:</span><span class="sxs-lookup"><span data-stu-id="5017e-278">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="5017e-279">Inclusione di contenuto in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="5017e-279">Including content in a package</span></span>

<span data-ttu-id="5017e-280">Per includere il contenuto, aggiungere altri metadati all'elemento `<Content>` esistente.</span><span class="sxs-lookup"><span data-stu-id="5017e-280">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="5017e-281">Per impostazione predefinita tutti gli elementi di tipo"Content" vengono inclusi nel pacchetto, a meno che non si esegua l'override con voci simili al codice seguente:</span><span class="sxs-lookup"><span data-stu-id="5017e-281">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="5017e-282">Per impostazione predefinita, tutti gli elementi vengono aggiunti alla radice di `content` e della cartella `contentFiles\any\<target_framework>` all'interno di un pacchetto e viene mantenuta la struttura di cartelle relative, a meno che non si specifichi un percorso di pacchetto:</span><span class="sxs-lookup"><span data-stu-id="5017e-282">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="5017e-283">Se si vuole copiare tutto il contenuto sono in cartelle radice specifiche (invece di copiarlo sia in `content` che in `contentFiles`), è possibile usare la proprietà di MSBuild `ContentTargetFolders`, che ha il valore predefinito "content;contentFiles" ma può essere impostata su qualsiasi altro nome di cartella.</span><span class="sxs-lookup"><span data-stu-id="5017e-283">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="5017e-284">Si noti che se si specifica solo "contentFiles" in `ContentTargetFolders`, i file vengono posizionati in `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` in base a `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="5017e-284">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="5017e-285">`PackagePath` può essere un set di percorsi di destinazione delimitati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="5017e-285">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="5017e-286">Se si specifica un percorso di pacchetto vuoto, il file viene aggiunto alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5017e-286">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="5017e-287">Ad esempio, il codice seguente aggiunge `libuv.txt` a `content\myfiles`, `content\samples` e nella radice del pacchetto:</span><span class="sxs-lookup"><span data-stu-id="5017e-287">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="5017e-288">È disponibile anche una proprietà di MSBuild `$(IncludeContentInPack)`, con valore predefinito `true`.</span><span class="sxs-lookup"><span data-stu-id="5017e-288">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="5017e-289">Se questa proprietà viene impostata su `false` in qualsiasi progetto, il contenuto da tale progetto non viene incluso nel pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="5017e-289">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="5017e-290">Altri metadati specifici di pack che è possibile impostare per qualsiasi elemento precedente includono ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, che impostano i valori ```CopyToOutput``` e ```Flatten``` sulla voce ```contentFiles``` nel file nuspec di output.</span><span class="sxs-lookup"><span data-stu-id="5017e-290">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="5017e-291">Oltre agli elementi Content, i metadati `<Pack>` e `<PackagePath>` possono anche essere impostati nei file con l'azione di compilazione Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o None.</span><span class="sxs-lookup"><span data-stu-id="5017e-291">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="5017e-292">Per fare in modo che il comando pack aggiunga il nome del file al percorso del pacchetto quando si usano modelli con caratteri jolly (glob), il percorso del pacchetto deve terminare con il carattere separatore di cartella. In caso contrario, il percorso del pacchetto viene interpretato come percorso completo, incluso il nome del file.</span><span class="sxs-lookup"><span data-stu-id="5017e-292">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="5017e-293">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="5017e-293">IncludeSymbols</span></span>

<span data-ttu-id="5017e-294">Quando si usa `MSBuild -t:pack -p:IncludeSymbols=true`, i file `.pdb` corrispondenti vengono copiati insieme agli altri file di output (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="5017e-294">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="5017e-295">Si noti che l'impostazione `IncludeSymbols=true` crea un pacchetto regolare *e* un pacchetto di simboli.</span><span class="sxs-lookup"><span data-stu-id="5017e-295">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="5017e-296">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="5017e-296">IncludeSource</span></span>

<span data-ttu-id="5017e-297">Equivale a `IncludeSymbols`, ma insieme ai file `.pdb` vengono copiati anche i file di origine.</span><span class="sxs-lookup"><span data-stu-id="5017e-297">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="5017e-298">Tutti i file di tipo `Compile` vengono copiati in `src\<ProjectName>\` conservando la struttura di cartelle del percorso relativo nel pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="5017e-298">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="5017e-299">Lo stesso accade anche per i file di origine di qualsiasi `ProjectReference` con `TreatAsPackageReference` impostato su `false`.</span><span class="sxs-lookup"><span data-stu-id="5017e-299">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="5017e-300">Se un file di tipo Compile è all'esterno della cartella di progetto, viene semplicemente aggiunto a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="5017e-300">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="5017e-301">Compressione di un'espressione di licenza o di un file di licenza</span><span class="sxs-lookup"><span data-stu-id="5017e-301">Packing a license expression or a license file</span></span>

<span data-ttu-id="5017e-302">Quando si usa un'espressione di licenza, è necessario usare la proprietà PackageLicenseExpression.</span><span class="sxs-lookup"><span data-stu-id="5017e-302">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="5017e-303">[Esempio di espressione di licenza](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="5017e-303">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="5017e-304">[Altre informazioni sulle espressioni di licenza e le licenze accettate da NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="5017e-304">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="5017e-305">Quando si imballa un file di licenza, è necessario utilizzare la proprietà PackageLicenseFile per specificare il percorso del pacchetto, relativo alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5017e-305">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="5017e-306">Inoltre, è necessario assicurarsi che il file sia incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5017e-306">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="5017e-307">Esempio:</span><span class="sxs-lookup"><span data-stu-id="5017e-307">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="5017e-308">[Esempio di file di licenza](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="5017e-308">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="5017e-309">IsTool</span><span class="sxs-lookup"><span data-stu-id="5017e-309">IsTool</span></span>

<span data-ttu-id="5017e-310">Quando si usa `MSBuild -t:pack -p:IsTool=true`, tutti i file, come specificato nello scenario [Assembly di output](#output-assemblies), vengono copiati nella cartella `tools` invece che nella cartella `lib`.</span><span class="sxs-lookup"><span data-stu-id="5017e-310">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="5017e-311">Si noti che questo comportamento è diverso da `DotNetCliTool`, che viene specificato impostando `PackageType` nel file `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="5017e-311">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="5017e-312">Creazione di un pacchetto con un file .nuspec</span><span class="sxs-lookup"><span data-stu-id="5017e-312">Packing using a .nuspec</span></span>

<span data-ttu-id="5017e-313">Sebbene sia consigliabile [includere tutte le proprietà](../reference/msbuild-targets.md#pack-target) che in genere si trovano nel file `.nuspec` del file di progetto, è possibile scegliere di utilizzare un file `.nuspec` per comprimere il progetto.</span><span class="sxs-lookup"><span data-stu-id="5017e-313">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="5017e-314">Per un progetto non di tipo SDK che usa `PackageReference`, è necessario importare `NuGet.Build.Tasks.Pack.targets` in modo che l'attività Pack possa essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="5017e-314">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="5017e-315">Prima di poter comprimere un file nuspec, è ancora necessario ripristinare il progetto.</span><span class="sxs-lookup"><span data-stu-id="5017e-315">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="5017e-316">Un progetto di tipo SDK include le destinazioni di tipo pack per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5017e-316">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="5017e-317">Il Framework di destinazione del file di progetto non è rilevante e non viene usato per la compressione di un NuSpec.</span><span class="sxs-lookup"><span data-stu-id="5017e-317">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="5017e-318">Le tre proprietà di MSBuild seguenti sono rilevanti per la creazione di pacchetti con un file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="5017e-318">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="5017e-319">`NuspecFile`: percorso relativo o assoluto per il file `.nuspec` usato per la creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5017e-319">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="5017e-320">`NuspecProperties`: elenco con valori delimitati da punto e virgola di coppie chiave=valore.</span><span class="sxs-lookup"><span data-stu-id="5017e-320">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="5017e-321">A causa della modalità di funzionamento dell'analisi della riga di comando di MSBuild, è necessario specificare più proprietà come indicato di seguito: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="5017e-321">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="5017e-322">`NuspecBasePath`: percorso di base per il file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="5017e-322">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="5017e-323">Se si usa `dotnet.exe` per creare il pacchetto del progetto, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="5017e-323">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="5017e-324">Se si usa MSBuild per creare il pacchetto del progetto, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="5017e-324">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="5017e-325">Si noti che la compressione di un NuSpec con dotnet. exe o MSBuild comporta anche la compilazione del progetto per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5017e-325">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="5017e-326">Questa operazione può essere evitata passando @no__t proprietà-0 a dotnet. exe, che equivale a impostare ```<NoBuild>true</NoBuild> ``` nel file di progetto, oltre a impostare ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="5017e-326">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="5017e-327">Un esempio di file con estensione *csproj* per la compressione di un file nuspec è:</span><span class="sxs-lookup"><span data-stu-id="5017e-327">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="5017e-328">Punti di estensione avanzati per la creazione di pacchetti personalizzati</span><span class="sxs-lookup"><span data-stu-id="5017e-328">Advanced extension points to create customized package</span></span>

<span data-ttu-id="5017e-329">La destinazione `pack` fornisce due punti di estensione che vengono eseguiti nella compilazione specifica del Framework di destinazione interno.</span><span class="sxs-lookup"><span data-stu-id="5017e-329">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="5017e-330">I punti di estensione supportano l'inclusione di contenuto e assembly specifici del Framework di destinazione in un pacchetto:</span><span class="sxs-lookup"><span data-stu-id="5017e-330">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="5017e-331">destinazione `TargetsForTfmSpecificBuildOutput`: usare per i file all'interno della cartella `lib` o una cartella specificata con `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="5017e-331">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="5017e-332">destinazione `TargetsForTfmSpecificContentInPackage`: usare per i file all'esterno del `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="5017e-332">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="5017e-333">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="5017e-333">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="5017e-334">Scrivere una destinazione personalizzata e specificarla come valore della proprietà `$(TargetsForTfmSpecificBuildOutput)`.</span><span class="sxs-lookup"><span data-stu-id="5017e-334">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="5017e-335">Per tutti i file che devono entrare in `BuildOutputTargetFolder` (lib per impostazione predefinita), la destinazione deve scrivere i file in ItemGroup `BuildOutputInPackage` e impostare i due valori di metadati seguenti:</span><span class="sxs-lookup"><span data-stu-id="5017e-335">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="5017e-336">`FinalOutputPath`: il percorso assoluto del file; Se non viene specificato, l'identità viene utilizzata per valutare il percorso di origine.</span><span class="sxs-lookup"><span data-stu-id="5017e-336">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="5017e-337">`TargetPath`: (facoltativo) impostare quando il file deve essere inserito in una sottocartella all'interno di `lib\<TargetFramework>`, ad esempio gli assembly satellite che passano nelle rispettive cartelle delle impostazioni cultura.</span><span class="sxs-lookup"><span data-stu-id="5017e-337">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="5017e-338">Il valore predefinito è il nome del file.</span><span class="sxs-lookup"><span data-stu-id="5017e-338">Defaults to the name of the file.</span></span>

<span data-ttu-id="5017e-339">Esempio:</span><span class="sxs-lookup"><span data-stu-id="5017e-339">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="5017e-340">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="5017e-340">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="5017e-341">Scrivere una destinazione personalizzata e specificarla come valore della proprietà `$(TargetsForTfmSpecificContentInPackage)`.</span><span class="sxs-lookup"><span data-stu-id="5017e-341">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="5017e-342">Per tutti i file da includere nel pacchetto, la destinazione deve scrivere i file in ItemGroup `TfmSpecificPackageFile` e impostare i metadati facoltativi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5017e-342">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="5017e-343">`PackagePath`: percorso in cui il file deve essere restituito nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5017e-343">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="5017e-344">NuGet genera un avviso se viene aggiunto più di un file allo stesso percorso del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5017e-344">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="5017e-345">`BuildAction`: l'azione di compilazione da assegnare al file, necessaria solo se il percorso del pacchetto si trova nella cartella `contentFiles`.</span><span class="sxs-lookup"><span data-stu-id="5017e-345">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="5017e-346">Il valore predefinito è "None".</span><span class="sxs-lookup"><span data-stu-id="5017e-346">Defaults to "None".</span></span>

<span data-ttu-id="5017e-347">Esempio:</span><span class="sxs-lookup"><span data-stu-id="5017e-347">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="5017e-348">Destinazione restore</span><span class="sxs-lookup"><span data-stu-id="5017e-348">restore target</span></span>

<span data-ttu-id="5017e-349">`MSBuild -t:restore` (usato da `nuget restore` e `dotnet restore` con progetti .NET Core) consente di ripristinare i pacchetti a cui si fa riferimento nel file di progetto, come segue:</span><span class="sxs-lookup"><span data-stu-id="5017e-349">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="5017e-350">Lettura di tutti i riferimenti da progetto a progetto</span><span class="sxs-lookup"><span data-stu-id="5017e-350">Read all project to project references</span></span>
1. <span data-ttu-id="5017e-351">Lettura delle proprietà del progetto per trovare la cartella intermedia e i framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="5017e-351">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="5017e-352">Passare i dati di MSBuild a NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="5017e-352">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="5017e-353">Esecuzione di restore</span><span class="sxs-lookup"><span data-stu-id="5017e-353">Run restore</span></span>
1. <span data-ttu-id="5017e-354">Download dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="5017e-354">Download packages</span></span>
1. <span data-ttu-id="5017e-355">Scrittura dei file di asset, delle destinazioni e delle proprietà</span><span class="sxs-lookup"><span data-stu-id="5017e-355">Write assets file, targets, and props</span></span>

<span data-ttu-id="5017e-356">La destinazione `restore` funziona **solo** per i progetti che usano il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="5017e-356">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="5017e-357">**Non funziona per** i progetti che usano il formato `packages.config`; in alternativa, usare [NuGet Restore](../reference/cli-reference/cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="5017e-357">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="5017e-358">Ripristino delle proprietà</span><span class="sxs-lookup"><span data-stu-id="5017e-358">Restore properties</span></span>

<span data-ttu-id="5017e-359">Possono esistere ulteriori impostazioni di ripristino derivate da proprietà di MSBuild nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="5017e-359">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="5017e-360">I valori possono essere impostati anche dalla riga di comando tramite l'opzione `-p:` (vedere gli esempi riportati di seguito).</span><span class="sxs-lookup"><span data-stu-id="5017e-360">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="5017e-361">proprietà</span><span class="sxs-lookup"><span data-stu-id="5017e-361">Property</span></span> | <span data-ttu-id="5017e-362">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5017e-362">Description</span></span> |
|--------|--------|
| <span data-ttu-id="5017e-363">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="5017e-363">RestoreSources</span></span> | <span data-ttu-id="5017e-364">Elenco delimitato da punto e virgola delle origini di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5017e-364">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="5017e-365">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="5017e-365">RestorePackagesPath</span></span> | <span data-ttu-id="5017e-366">Percorso della cartella dei pacchetti dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5017e-366">User packages folder path.</span></span> |
| <span data-ttu-id="5017e-367">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="5017e-367">RestoreDisableParallel</span></span> | <span data-ttu-id="5017e-368">Consente di limitare i download a uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="5017e-368">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="5017e-369">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="5017e-369">RestoreConfigFile</span></span> | <span data-ttu-id="5017e-370">Percorso per un file `Nuget.Config` da applicare.</span><span class="sxs-lookup"><span data-stu-id="5017e-370">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="5017e-371">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="5017e-371">RestoreNoCache</span></span> | <span data-ttu-id="5017e-372">Se true, evita l'utilizzo di pacchetti memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="5017e-372">If true, avoids using cached packages.</span></span> <span data-ttu-id="5017e-373">Vedere [gestione dei pacchetti globali e delle cartelle della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="5017e-373">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="5017e-374">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="5017e-374">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="5017e-375">Se true, ignora le origini di pacchetti in errore o mancanti.</span><span class="sxs-lookup"><span data-stu-id="5017e-375">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="5017e-376">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="5017e-376">RestoreFallbackFolders</span></span> | <span data-ttu-id="5017e-377">Cartelle di fallback, utilizzate nello stesso modo in cui viene utilizzata la cartella Pacchetti utente.</span><span class="sxs-lookup"><span data-stu-id="5017e-377">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="5017e-378">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="5017e-378">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="5017e-379">Origini aggiuntive da utilizzare durante il ripristino.</span><span class="sxs-lookup"><span data-stu-id="5017e-379">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="5017e-380">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="5017e-380">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="5017e-381">Cartelle di fallback aggiuntive da usare durante il ripristino.</span><span class="sxs-lookup"><span data-stu-id="5017e-381">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="5017e-382">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="5017e-382">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="5017e-383">Esclude le cartelle di fallback specificate in `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="5017e-383">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="5017e-384">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="5017e-384">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="5017e-385">Percorso di `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="5017e-385">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="5017e-386">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="5017e-386">RestoreGraphProjectInput</span></span> | <span data-ttu-id="5017e-387">Elenco delimitato da punto e virgola dei progetti da ripristinare, che deve contenere percorsi assoluti.</span><span class="sxs-lookup"><span data-stu-id="5017e-387">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="5017e-388">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="5017e-388">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="5017e-389">Quando i progetti vengono raccolti tramite MSBuild, determina se vengono raccolti usando l'ottimizzazione `SkipNonexistentTargets`.</span><span class="sxs-lookup"><span data-stu-id="5017e-389">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="5017e-390">Se non è impostato, il valore predefinito è `true`.</span><span class="sxs-lookup"><span data-stu-id="5017e-390">When not set, defaults to `true`.</span></span> <span data-ttu-id="5017e-391">La conseguenza è un comportamento non rapido quando le destinazioni di un progetto non possono essere importate.</span><span class="sxs-lookup"><span data-stu-id="5017e-391">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="5017e-392">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="5017e-392">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="5017e-393">Cartella di output, per impostazione predefinita `BaseIntermediateOutputPath` e la cartella `obj`.</span><span class="sxs-lookup"><span data-stu-id="5017e-393">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="5017e-394">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="5017e-394">RestoreForce</span></span> | <span data-ttu-id="5017e-395">Nei progetti basati su PackageReference, impone la risoluzione di tutte le dipendenze anche se l'ultimo ripristino ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="5017e-395">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="5017e-396">La specifica di questo flag è simile all'eliminazione del file `project.assets.json`.</span><span class="sxs-lookup"><span data-stu-id="5017e-396">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="5017e-397">Questa operazione non consente di ignorare la cache HTTP.</span><span class="sxs-lookup"><span data-stu-id="5017e-397">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="5017e-398">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="5017e-398">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="5017e-399">Optare per l'utilizzo di un file di blocco.</span><span class="sxs-lookup"><span data-stu-id="5017e-399">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="5017e-400">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="5017e-400">RestoreLockedMode</span></span> | <span data-ttu-id="5017e-401">Eseguire Restore in modalità bloccata.</span><span class="sxs-lookup"><span data-stu-id="5017e-401">Run restore in locked mode.</span></span> <span data-ttu-id="5017e-402">Questo significa che il ripristino non valuterà nuovamente le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="5017e-402">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="5017e-403">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="5017e-403">NuGetLockFilePath</span></span> | <span data-ttu-id="5017e-404">Percorso personalizzato per il file di blocco.</span><span class="sxs-lookup"><span data-stu-id="5017e-404">A custom location for the lock file.</span></span> <span data-ttu-id="5017e-405">Il percorso predefinito è accanto al progetto ed è denominato `packages.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="5017e-405">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="5017e-406">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="5017e-406">RestoreForceEvaluate</span></span> | <span data-ttu-id="5017e-407">Forza il ripristino per ricalcolare le dipendenze e aggiornare il file di blocco senza alcun avviso.</span><span class="sxs-lookup"><span data-stu-id="5017e-407">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> | 

#### <a name="examples"></a><span data-ttu-id="5017e-408">Esempi</span><span class="sxs-lookup"><span data-stu-id="5017e-408">Examples</span></span>

<span data-ttu-id="5017e-409">Riga di comando:</span><span class="sxs-lookup"><span data-stu-id="5017e-409">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="5017e-410">File di progetto:</span><span class="sxs-lookup"><span data-stu-id="5017e-410">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="5017e-411">Output del ripristino</span><span class="sxs-lookup"><span data-stu-id="5017e-411">Restore outputs</span></span>

<span data-ttu-id="5017e-412">Il ripristino crea i file seguenti nella cartella `obj` di compilazione:</span><span class="sxs-lookup"><span data-stu-id="5017e-412">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="5017e-413">File</span><span class="sxs-lookup"><span data-stu-id="5017e-413">File</span></span> | <span data-ttu-id="5017e-414">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5017e-414">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="5017e-415">Contiene il grafico delle dipendenze di tutti i riferimenti ai pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5017e-415">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="5017e-416">Riferimenti alle proprietà di MSBuild contenute nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="5017e-416">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="5017e-417">Riferimenti alle destinazioni di MSBuild contenute nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="5017e-417">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="5017e-418">Ripristino e compilazione con un comando MSBuild</span><span class="sxs-lookup"><span data-stu-id="5017e-418">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="5017e-419">A causa del fatto che NuGet può ripristinare i pacchetti che arrestano le destinazioni e le proprietà di MSBuild, le valutazioni di ripristino e compilazione vengono eseguite con proprietà globali diverse.</span><span class="sxs-lookup"><span data-stu-id="5017e-419">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="5017e-420">Ciò significa che le operazioni seguenti avranno un comportamento imprevedibile e spesso errato.</span><span class="sxs-lookup"><span data-stu-id="5017e-420">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="5017e-421">L'approccio consigliato è invece:</span><span class="sxs-lookup"><span data-stu-id="5017e-421">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="5017e-422">La stessa logica si applica ad altre destinazioni simili a `build`.</span><span class="sxs-lookup"><span data-stu-id="5017e-422">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="5017e-423">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="5017e-423">PackageTargetFallback</span></span>

<span data-ttu-id="5017e-424">L'elemento `PackageTargetFallback` consente di specificare un set di destinazioni compatibili da usare durante il ripristino di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5017e-424">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="5017e-425">È progettato per consentire ai pacchetti che usano un [TxM](../reference/target-frameworks.md) dotnet di interagire con pacchetti compatibili che non dichiarano un TxM dotnet.</span><span class="sxs-lookup"><span data-stu-id="5017e-425">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="5017e-426">Se il progetto usa il TxM dotnet, devono averlo anche tutti i pacchetti da cui il progetto dipende, a meno che non si aggiunga `<PackageTargetFallback>` al progetto, in modo da rendere compatibili con dotnet le piattaforme che non lo sono.</span><span class="sxs-lookup"><span data-stu-id="5017e-426">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="5017e-427">Ad esempio, se il progetto usa il TxM `netstandard1.6` e un pacchetto dipendente contiene solo `lib/net45/a.dll` e `lib/portable-net45+win81/a.dll`, la compilazione del progetto avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="5017e-427">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="5017e-428">Se si vuole includere solo quest'ultima DLL, è possibile aggiungere un `PackageTargetFallback` come segue per segnalare che la DLL `portable-net45+win81` è compatibile:</span><span class="sxs-lookup"><span data-stu-id="5017e-428">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="5017e-429">Per dichiarare un fallback per tutte le destinazioni nel progetto, non specificare l'attributo `Condition`.</span><span class="sxs-lookup"><span data-stu-id="5017e-429">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="5017e-430">È anche possibile estendere qualsiasi `PackageTargetFallback` esistente includendo `$(PackageTargetFallback)` come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5017e-430">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="5017e-431">Sostituzione di una libreria da un grafico di ripristino</span><span class="sxs-lookup"><span data-stu-id="5017e-431">Replacing one library from a restore graph</span></span>

<span data-ttu-id="5017e-432">Se un ripristino restituisce l'assembly errato, è possibile escludere la scelta predefinita di tali pacchetti e sostituirla con la propria scelta.</span><span class="sxs-lookup"><span data-stu-id="5017e-432">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="5017e-433">Prima di tutto, con un `PackageReference` di livello superiore, escludere tutti gli asset:</span><span class="sxs-lookup"><span data-stu-id="5017e-433">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="5017e-434">Aggiungere quindi il riferimento personalizzato alla copia locale appropriata della DLL:</span><span class="sxs-lookup"><span data-stu-id="5017e-434">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
