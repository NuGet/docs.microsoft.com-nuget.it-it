---
title: NuGet eseguire il pack e il ripristino come MSBuild destinazioni
description: NuGet pack e restore possono funzionare direttamente come MSBuild destinazioni con NuGet 4.0+.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 47411641db47884f79f2bc9a4aa00035fc79993b
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387374"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="e5b0e-103">NuGet eseguire il pack e il ripristino come MSBuild destinazioni</span><span class="sxs-lookup"><span data-stu-id="e5b0e-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="e5b0e-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="e5b0e-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="e5b0e-105">Con il [formato PackageReference,](../consume-packages/package-references-in-project-files.md) 4.0+ può archiviare tutti i metadati del manifesto direttamente all'interno di un file di progetto NuGet anziché usare un file `.nuspec` separato.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="e5b0e-106">Con MSBuild 15.1+, è anche un primo livello con le destinazioni NuGet e come descritto di MSBuild `pack` `restore` seguito.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="e5b0e-107">Queste destinazioni consentono di usare come si farebbe NuGet con qualsiasi altra attività o MSBuild destinazione.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="e5b0e-108">Per istruzioni sulla creazione di NuGet un pacchetto tramite , vedere Creare un pacchetto MSBuild [ NuGet usando MSBuild ](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="e5b0e-109">(Per NuGet 3.x e versioni precedenti usano invece i [comandi pack](../reference/cli-reference/cli-ref-pack.md) [e restore](../reference/cli-reference/cli-ref-restore.md) tramite l'interfaccia della riga NuGet di comando.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="e5b0e-110">Ordine di compilazione delle destinazioni</span><span class="sxs-lookup"><span data-stu-id="e5b0e-110">Target build order</span></span>

<span data-ttu-id="e5b0e-111">Poiché `pack` e `restore` sono  MSBuild destinazioni, è possibile accedervi per migliorare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="e5b0e-112">Si supponga, ad esempio, di voler copiare il pacchetto in una condivisione di rete dopo la creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-112">For example, let's say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="e5b0e-113">È possibile farlo aggiungendo quanto segue nel file di progetto:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="e5b0e-114">Analogamente, è possibile scrivere MSBuild un'attività, scrivere la propria destinazione e utilizzare NuGet le proprietà MSBuild nell'attività.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="e5b0e-115">`$(OutputPath)` è relativo e prevede che il comando sia in esecuzione dalla radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="e5b0e-116">Destinazione pack</span><span class="sxs-lookup"><span data-stu-id="e5b0e-116">pack target</span></span>

<span data-ttu-id="e5b0e-117">Per i progetti .NET che usano il formato , l'uso di disegna input dal file di progetto da `PackageReference` usare nella creazione di un `msbuild -t:pack` NuGet pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="e5b0e-118">Nella tabella seguente vengono descritte le MSBuild proprietà che è possibile aggiungere a un file di progetto all'interno del primo `<PropertyGroup>` nodo.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="e5b0e-119">È possibile apportare facilmente queste modifiche in Visual Studio 2017 e versioni successive facendo clic con il pulsante destro del mouse sul progetto e scegliendo **Modifica {nome_progetto}** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="e5b0e-120">Per praticità, la tabella è organizzata in base alla proprietà equivalente in un [ `.nuspec` file](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e5b0e-121">`Owners` Le `Summary` proprietà e da non sono supportate con `.nuspec` MSBuild .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-121">`Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="e5b0e-122">nuspecAttributo/valore</span><span class="sxs-lookup"><span data-stu-id="e5b0e-122">Attribute/nuspec Value</span></span> | <span data-ttu-id="e5b0e-123">Proprietà diMSBuild</span><span class="sxs-lookup"><span data-stu-id="e5b0e-123">MSBuild Property</span></span> | <span data-ttu-id="e5b0e-124">Predefinito</span><span class="sxs-lookup"><span data-stu-id="e5b0e-124">Default</span></span> | <span data-ttu-id="e5b0e-125">Note</span><span class="sxs-lookup"><span data-stu-id="e5b0e-125">Notes</span></span> |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | <span data-ttu-id="e5b0e-126">`$(AssemblyName)` da MSBuild</span><span class="sxs-lookup"><span data-stu-id="e5b0e-126">`$(AssemblyName)` from MSBuild</span></span> |
| `Version` | `PackageVersion` | <span data-ttu-id="e5b0e-127">Versione</span><span class="sxs-lookup"><span data-stu-id="e5b0e-127">Version</span></span> | <span data-ttu-id="e5b0e-128">È compatibile con semver, ad esempio `1.0.0` `1.0.0-beta` , o `1.0.0-beta-00345`</span><span class="sxs-lookup"><span data-stu-id="e5b0e-128">This is semver compatible, for example `1.0.0`, `1.0.0-beta`, or `1.0.0-beta-00345`</span></span> |
| `VersionPrefix` | `PackageVersionPrefix` | <span data-ttu-id="e5b0e-129">empty</span><span class="sxs-lookup"><span data-stu-id="e5b0e-129">empty</span></span> | <span data-ttu-id="e5b0e-130">`PackageVersion`L'impostazione sovrascrive`PackageVersionPrefix`</span><span class="sxs-lookup"><span data-stu-id="e5b0e-130">Setting `PackageVersion` overwrites `PackageVersionPrefix`</span></span> |
| `VersionSuffix` | `PackageVersionSuffix` | <span data-ttu-id="e5b0e-131">empty</span><span class="sxs-lookup"><span data-stu-id="e5b0e-131">empty</span></span> | <span data-ttu-id="e5b0e-132">`$(VersionSuffix)` da MSBuild .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-132">`$(VersionSuffix)` from MSBuild.</span></span> <span data-ttu-id="e5b0e-133">Sovrascrittura `PackageVersion` delle impostazioni `PackageVersionSuffix`</span><span class="sxs-lookup"><span data-stu-id="e5b0e-133">Setting `PackageVersion` overwrites `PackageVersionSuffix`</span></span> |
| `Authors` | `Authors` | <span data-ttu-id="e5b0e-134">Nome utente dell'utente corrente</span><span class="sxs-lookup"><span data-stu-id="e5b0e-134">Username of the current user</span></span> | <span data-ttu-id="e5b0e-135">Elenco di autori di pacchetti separati da punto e virgola, corrispondenti ai nomi dei profili nuget.org. Questi vengono visualizzati in Gallery in nuget.org e vengono usati per creare riferimenti incrociati ai NuGet pacchetti da parte degli stessi autori.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-135">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Owners` | <span data-ttu-id="e5b0e-136">N/D</span><span class="sxs-lookup"><span data-stu-id="e5b0e-136">N/A</span></span> | <span data-ttu-id="e5b0e-137">Non presente in nuspec</span><span class="sxs-lookup"><span data-stu-id="e5b0e-137">Not present in nuspec</span></span> | |
| `Title` | `Title` | <span data-ttu-id="e5b0e-138">Il tipo `PackageId`</span><span class="sxs-lookup"><span data-stu-id="e5b0e-138">The `PackageId`</span></span> | <span data-ttu-id="e5b0e-139">Titolo del pacchetto facilmente comprensibile per l'utente, usato di solito per la visualizzazione dell'interfaccia utente, ad esempio in nuget.org e in Gestione pacchetti in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| `Description` | `Description` | <span data-ttu-id="e5b0e-140">"Descrizione del pacchetto"</span><span class="sxs-lookup"><span data-stu-id="e5b0e-140">"Package Description"</span></span> | <span data-ttu-id="e5b0e-141">Descrizione lunga per l'assembly.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-141">A long description for the assembly.</span></span> <span data-ttu-id="e5b0e-142">Se `PackageDescription` non viene specificato, questa proprietà viene utilizzata anche come descrizione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-142">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | `Copyright` | <span data-ttu-id="e5b0e-143">empty</span><span class="sxs-lookup"><span data-stu-id="e5b0e-143">empty</span></span> | <span data-ttu-id="e5b0e-144">Informazioni sul copyright per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-144">Copyright details for the package.</span></span> |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | <span data-ttu-id="e5b0e-145">Valore booleano che specifica se il client deve richiedere al consumer di accettare la licenza del pacchetto prima di installarlo.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-145">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| `license` | `PackageLicenseExpression` | <span data-ttu-id="e5b0e-146">empty</span><span class="sxs-lookup"><span data-stu-id="e5b0e-146">empty</span></span> | <span data-ttu-id="e5b0e-147">Corrisponde a `<license type="expression">`.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-147">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="e5b0e-148">Vedere [Creazione di un pacchetto di un'espressione di licenza o di un file di licenza.](#packing-a-license-expression-or-a-license-file)</span><span class="sxs-lookup"><span data-stu-id="e5b0e-148">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `license` | `PackageLicenseFile` | <span data-ttu-id="e5b0e-149">empty</span><span class="sxs-lookup"><span data-stu-id="e5b0e-149">empty</span></span> | <span data-ttu-id="e5b0e-150">Percorso di un file di licenza all'interno del pacchetto se si usa una licenza personalizzata o una licenza a cui non è stato assegnato un identificatore SPDX.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-150">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="e5b0e-151">È necessario creare un pacchetto esplicito del file di licenza a cui si fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-151">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="e5b0e-152">Corrisponde a `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-152">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="e5b0e-153">Vedere [Creazione di un pacchetto di un'espressione di licenza o di un file di licenza.](#packing-a-license-expression-or-a-license-file)</span><span class="sxs-lookup"><span data-stu-id="e5b0e-153">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `LicenseUrl` | `PackageLicenseUrl` | <span data-ttu-id="e5b0e-154">empty</span><span class="sxs-lookup"><span data-stu-id="e5b0e-154">empty</span></span> | <span data-ttu-id="e5b0e-155">L'oggetto `PackageLicenseUrl` è deprecato.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-155">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="e5b0e-156">In sostituzione usare `PackageLicenseExpression` o `PackageLicenseFile`.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-156">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `ProjectUrl` | `PackageProjectUrl` | <span data-ttu-id="e5b0e-157">empty</span><span class="sxs-lookup"><span data-stu-id="e5b0e-157">empty</span></span> | |
| `Icon` | `PackageIcon` | <span data-ttu-id="e5b0e-158">empty</span><span class="sxs-lookup"><span data-stu-id="e5b0e-158">empty</span></span> | <span data-ttu-id="e5b0e-159">Percorso di un'immagine nel pacchetto da utilizzare come icona del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-159">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="e5b0e-160">È necessario creare un pacchetto esplicito del file di immagine dell'icona a cui si fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-160">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="e5b0e-161">Per altre informazioni, vedere [Creazione di un pacchetto di un file di immagine icona](#packing-an-icon-image-file) e [ `icon` metadati.](./nuspec.md#icon)</span><span class="sxs-lookup"><span data-stu-id="e5b0e-161">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](./nuspec.md#icon).</span></span> |
| `IconUrl` | `PackageIconUrl` | <span data-ttu-id="e5b0e-162">empty</span><span class="sxs-lookup"><span data-stu-id="e5b0e-162">empty</span></span> | <span data-ttu-id="e5b0e-163">`PackageIconUrl` è deprecato a favore di `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-163">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="e5b0e-164">Tuttavia, per la migliore esperienza di livello inferiore, è necessario `PackageIconUrl` specificare oltre a `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-164">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| `Readme` | `PackageReadmeFile` | <span data-ttu-id="e5b0e-165">empty</span><span class="sxs-lookup"><span data-stu-id="e5b0e-165">empty</span></span> | <span data-ttu-id="e5b0e-166">È necessario creare un pacchetto esplicito del file Leggimi a cui si fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-166">You need to explicitly pack the referenced readme file.</span></span>|
| `Tags` | `PackageTags` | <span data-ttu-id="e5b0e-167">empty</span><span class="sxs-lookup"><span data-stu-id="e5b0e-167">empty</span></span> | <span data-ttu-id="e5b0e-168">Elenco di tag con valori delimitati da punto e virgola che designa il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-168">A semicolon-delimited list of tags that designates the package.</span></span> |
| `ReleaseNotes` | `PackageReleaseNotes` | <span data-ttu-id="e5b0e-169">empty</span><span class="sxs-lookup"><span data-stu-id="e5b0e-169">empty</span></span> | <span data-ttu-id="e5b0e-170">Note sulla versione per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-170">Release notes for the package.</span></span> |
| `Repository/Url` | `RepositoryUrl` | <span data-ttu-id="e5b0e-171">empty</span><span class="sxs-lookup"><span data-stu-id="e5b0e-171">empty</span></span> | <span data-ttu-id="e5b0e-172">URL del repository usato per clonare o recuperare il codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-172">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="e5b0e-173">Esempio: *https://github.com/ NuGet / NuGet . Client.git*.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-173">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `Repository/Type` | `RepositoryType` | <span data-ttu-id="e5b0e-174">empty</span><span class="sxs-lookup"><span data-stu-id="e5b0e-174">empty</span></span> | <span data-ttu-id="e5b0e-175">Tipo di repository.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-175">Repository type.</span></span> <span data-ttu-id="e5b0e-176">Esempi: `git` (impostazione predefinita), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-176">Examples: `git` (default), `tfs`.</span></span> |
| `Repository/Branch` | `RepositoryBranch` | <span data-ttu-id="e5b0e-177">empty</span><span class="sxs-lookup"><span data-stu-id="e5b0e-177">empty</span></span> | <span data-ttu-id="e5b0e-178">Informazioni facoltative sul ramo del repository.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-178">Optional repository branch information.</span></span> <span data-ttu-id="e5b0e-179">`RepositoryUrl` deve essere specificato anche per includere questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-179">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="e5b0e-180">Esempio: *master* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-180">Example: *master* (NuGet 4.7.0+).</span></span> |
| `Repository/Commit` | `RepositoryCommit` | <span data-ttu-id="e5b0e-181">empty</span><span class="sxs-lookup"><span data-stu-id="e5b0e-181">empty</span></span> | <span data-ttu-id="e5b0e-182">Commit del repository o set di modifiche facoltativo per indicare l'origine su cui è stato compilato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-182">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="e5b0e-183">`RepositoryUrl` deve essere specificato anche per includere questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-183">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="e5b0e-184">Esempio: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-184">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | <span data-ttu-id="e5b0e-185">Non supportato</span><span class="sxs-lookup"><span data-stu-id="e5b0e-185">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="e5b0e-186">Input destinazione pack</span><span class="sxs-lookup"><span data-stu-id="e5b0e-186">pack target inputs</span></span>

| <span data-ttu-id="e5b0e-187">Proprietà</span><span class="sxs-lookup"><span data-stu-id="e5b0e-187">Property</span></span> | <span data-ttu-id="e5b0e-188">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e5b0e-188">Description</span></span> |
| - | - |
| `IsPackable` | <span data-ttu-id="e5b0e-189">Valore booleano che specifica se dal progetto può essere creato un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-189">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="e5b0e-190">Il valore predefinito è `true`.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-190">The default value is `true`.</span></span> |
| `SuppressDependenciesWhenPacking` | <span data-ttu-id="e5b0e-191">Impostare su `true` per eliminare le dipendenze del pacchetto dal pacchetto NuGet generato.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-191">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| `PackageVersion` | <span data-ttu-id="e5b0e-192">Specifica la versione che avrà il pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-192">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="e5b0e-193">Accetta tutte le forme di NuGet stringa di versione.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-193">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="e5b0e-194">Il valore predefinito corrisponde al valore di `$(Version)`, vale a dire della proprietà `Version` nel progetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-194">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| `PackageId` | <span data-ttu-id="e5b0e-195">Specifica il nome del pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-195">Specifies the name for the resulting package.</span></span> <span data-ttu-id="e5b0e-196">Se non specificato, l'impostazione predefinita per l'operazione `pack` corrisponde all'uso di `AssemblyName` o del nome della directory come nome del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-196">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| `PackageDescription` | <span data-ttu-id="e5b0e-197">Descrizione lunga del pacchetto per la visualizzazione dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-197">A long description of the package for UI display.</span></span> |
| `Authors` | <span data-ttu-id="e5b0e-198">Elenco di autori di pacchetti separati da punti e virgola, corrispondenti ai nomi dei profili nuget.org. Questi elementi vengono visualizzati nella raccolta in nuget.org e vengono usati per creare riferimenti incrociati ai NuGet pacchetti degli stessi autori.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-198">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Description` | <span data-ttu-id="e5b0e-199">Descrizione lunga per l'assembly.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-199">A long description for the assembly.</span></span> <span data-ttu-id="e5b0e-200">Se non viene specificato, questa proprietà viene usata anche `PackageDescription` come descrizione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-200">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | <span data-ttu-id="e5b0e-201">Informazioni sul copyright per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-201">Copyright details for the package.</span></span> |
| `PackageRequireLicenseAcceptance` | <span data-ttu-id="e5b0e-202">Valore booleano che specifica se il client deve richiedere al consumer di accettare la licenza del pacchetto prima di installarlo.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-202">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="e5b0e-203">Il valore predefinito è `false`.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-203">The default is `false`.</span></span> |
| `DevelopmentDependency` | <span data-ttu-id="e5b0e-204">Valore booleano che specifica se il pacchetto è contrassegnato come dipendenza di solo sviluppo, impedendo che il pacchetto venga incluso come dipendenza in altri pacchetti.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-204">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="e5b0e-205">Con `PackageReference` ( 4.8+), questo flag indica anche che gli asset in fase di compilazione NuGet vengono esclusi dalla compilazione.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-205">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="e5b0e-206">Per altre informazioni, vedere [Supporto di DevelopmentDependency per PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-206">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| `PackageLicenseExpression` | <span data-ttu-id="e5b0e-207">Identificatore [o espressione di licenza SPDX,](https://spdx.org/licenses/) ad esempio `Apache-2.0` .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-207">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="e5b0e-208">Per altre informazioni, vedere [Creazione di un pacchetto di un'espressione di licenza o di un file di licenza.](#packing-a-license-expression-or-a-license-file)</span><span class="sxs-lookup"><span data-stu-id="e5b0e-208">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `PackageLicenseFile` | <span data-ttu-id="e5b0e-209">Percorso di un file di licenza all'interno del pacchetto se si usa una licenza personalizzata o una licenza a cui non è stato assegnato un identificatore SPDX.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-209">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| `PackageLicenseUrl` | <span data-ttu-id="e5b0e-210">L'oggetto `PackageLicenseUrl` è deprecato.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-210">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="e5b0e-211">In sostituzione usare `PackageLicenseExpression` o `PackageLicenseFile`.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-211">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `PackageProjectUrl` | |
| `PackageIcon` | <span data-ttu-id="e5b0e-212">Specifica il percorso dell'icona del pacchetto, relativo alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-212">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="e5b0e-213">Per altre informazioni, vedere [Creazione di un pacchetto di un file di immagine dell'icona.](#packing-an-icon-image-file)</span><span class="sxs-lookup"><span data-stu-id="e5b0e-213">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| `PackageReleaseNotes` | <span data-ttu-id="e5b0e-214">Note sulla versione per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-214">Release notes for the package.</span></span> |
| `PackageReadmeFile` | <span data-ttu-id="e5b0e-215">File Leggimi per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-215">Readme for the package.</span></span> |
| `PackageTags` | <span data-ttu-id="e5b0e-216">Elenco di tag con valori delimitati da punto e virgola che designa il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-216">A semicolon-delimited list of tags that designates the package.</span></span> |
| `PackageOutputPath` | <span data-ttu-id="e5b0e-217">Determina il percorso di output in cui verrà rilasciato il pacchetto creato.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-217">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="e5b0e-218">Il valore predefinito è `$(OutputPath)`.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-218">Default is `$(OutputPath)`.</span></span> |
| `IncludeSymbols` | <span data-ttu-id="e5b0e-219">Valore booleano che indica se al momento della creazione del pacchetto deve essere creato un pacchetto aggiuntivo di simboli.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-219">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="e5b0e-220">Il formato del pacchetto di simboli è controllato dalla proprietà `SymbolPackageFormat`.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-220">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="e5b0e-221">Per altre informazioni, vedere [IncludeSymbols](#includesymbols).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-221">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| `IncludeSource` | <span data-ttu-id="e5b0e-222">Valore booleano che indica se il processo di creazione del pacchetto deve creare un pacchetto di origine.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-222">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="e5b0e-223">Il pacchetto di origine contiene il codice sorgente della libreria, nonché i file PDB.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-223">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="e5b0e-224">I file di origine vengono posizionati nella directory `src/ProjectName` del file del pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-224">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="e5b0e-225">Per altre informazioni, vedere [IncludeSource.](#includesource)</span><span class="sxs-lookup"><span data-stu-id="e5b0e-225">For more information, see [IncludeSource](#includesource).</span></span> |
| `PackageType` | |
| `IsTool` | <span data-ttu-id="e5b0e-226">Specifica se tutti i file di output devono essere copiati nella cartella *tools* anziché nella cartella *lib*.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-226">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="e5b0e-227">Per altre informazioni, vedere [IsTool](#istool).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-227">For more information, see [IsTool](#istool).</span></span> |
| `RepositoryUrl` | <span data-ttu-id="e5b0e-228">URL del repository usato per clonare o recuperare il codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-228">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="e5b0e-229">Esempio: *https://github.com/ NuGet / NuGet . Client.git*.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-229">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `RepositoryType` | <span data-ttu-id="e5b0e-230">Tipo di repository.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-230">Repository type.</span></span> <span data-ttu-id="e5b0e-231">Esempi: `git` (impostazione predefinita), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-231">Examples: `git` (default), `tfs`.</span></span> |
| `RepositoryBranch` | <span data-ttu-id="e5b0e-232">Informazioni facoltative sul ramo del repository.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-232">Optional repository branch information.</span></span> <span data-ttu-id="e5b0e-233">`RepositoryUrl` È inoltre necessario specificare per includere questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-233">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="e5b0e-234">Esempio: *master* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-234">Example: *master* (NuGet 4.7.0+).</span></span> |
| `RepositoryCommit` | <span data-ttu-id="e5b0e-235">Commit del repository o insieme di modifiche facoltativo per indicare l'origine in base alla quale è stato compilato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-235">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="e5b0e-236">`RepositoryUrl` È inoltre necessario specificare per includere questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-236">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="e5b0e-237">Esempio: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-237">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `SymbolPackageFormat` | <span data-ttu-id="e5b0e-238">Specifica il formato del pacchetto di simboli.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-238">Specifies the format of the symbols package.</span></span> <span data-ttu-id="e5b0e-239">Se "symbols.nupkg", viene creato un pacchetto di simboli legacy con estensione *symbols.nupkg* contenente file PDB, DLL e altri file di output.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-239">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="e5b0e-240">Se "snupkg", viene creato un pacchetto di simboli snupkg contenente i PDB portatili.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-240">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="e5b0e-241">Il valore predefinito è "symbols.nupkg".</span><span class="sxs-lookup"><span data-stu-id="e5b0e-241">The default is "symbols.nupkg".</span></span> |
| `NoPackageAnalysis` | <span data-ttu-id="e5b0e-242">Specifica che non deve `pack` eseguire l'analisi del pacchetto dopo la compilazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-242">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| `MinClientVersion` | <span data-ttu-id="e5b0e-243">Specifica la versione minima del client in grado di installare questo pacchetto, applicata da nuget.exe NuGet e dal Visual Studio Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-243">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| `IncludeBuildOutput` | <span data-ttu-id="e5b0e-244">Questo valore booleano specifica se gli assembly di output di compilazione devono essere suddivisi o meno nel file con estensione *nupkg.*</span><span class="sxs-lookup"><span data-stu-id="e5b0e-244">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| `IncludeContentInPack` | <span data-ttu-id="e5b0e-245">Questo valore booleano specifica se eventuali elementi di tipo vengono `Content` inclusi automaticamente nel pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-245">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="e5b0e-246">Il valore predefinito è `true`.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-246">The default is `true`.</span></span> |
| `BuildOutputTargetFolder` | <span data-ttu-id="e5b0e-247">Specifica la cartella in cui inserire gli assembly di output.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-247">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="e5b0e-248">Gli assembly di output (e altri file di output) vengono copiati nelle rispettive cartelle per framework.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-248">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="e5b0e-249">Per altre informazioni, vedere [Assembly di output.](#output-assemblies)</span><span class="sxs-lookup"><span data-stu-id="e5b0e-249">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| `ContentTargetFolders` | <span data-ttu-id="e5b0e-250">Specifica il percorso predefinito di tutti i file di contenuto se `PackagePath` non è specificato.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-250">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="e5b0e-251">Il valore predefinito è "content;contentFiles".</span><span class="sxs-lookup"><span data-stu-id="e5b0e-251">The default value is "content;contentFiles".</span></span> <span data-ttu-id="e5b0e-252">Per altre informazioni, vedere [Including content in a package](#including-content-in-a-package) (Includere contenuto in un pacchetto).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-252">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| `NuspecFile` | <span data-ttu-id="e5b0e-253">Percorso relativo o assoluto del *.nuspec* file utilizzato per la creazione di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-253">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="e5b0e-254">Se specificato, viene usato esclusivamente per **la** creazione di pacchetti di informazioni e le informazioni nei progetti non vengono usate.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-254">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="e5b0e-255">Per altre informazioni, vedere [Packing using a .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-255">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecBasePath` | <span data-ttu-id="e5b0e-256">Percorso di base per il *.nuspec* file.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-256">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="e5b0e-257">Per altre informazioni, vedere [Packing using a .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-257">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecProperties` | <span data-ttu-id="e5b0e-258">Elenco con valori delimitati da punto e virgola di coppie chiave=valore.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-258">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="e5b0e-259">Per altre informazioni, vedere [Creazione di un pacchetto tramite . .nuspec ](#packing-using-a-nuspec-file)</span><span class="sxs-lookup"><span data-stu-id="e5b0e-259">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="e5b0e-260">Scenari pack</span><span class="sxs-lookup"><span data-stu-id="e5b0e-260">pack scenarios</span></span>

### <a name="suppressing-dependencies"></a><span data-ttu-id="e5b0e-261">Eliminazione delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="e5b0e-261">Suppressing dependencies</span></span>

<span data-ttu-id="e5b0e-262">Per eliminare le dipendenze del pacchetto dal pacchetto generato, impostare su che consentirà di ignorare tutte le dipendenze NuGet `SuppressDependenciesWhenPacking` dal file `true` nupkg generato.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-262">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### `PackageIconUrl`

<span data-ttu-id="e5b0e-263">`PackageIconUrl` è deprecato a favore della [`PackageIcon`](#packageicon) proprietà .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-263">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="e5b0e-264">A partire dalla NuGet versione 5.3 e Visual Studio 2019 versione 16.3, genera l'avviso `pack` [NU5048](./errors-and-warnings/nu5048.md) se i metadati del pacchetto specificano solo `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-264">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### `PackageIcon`

> [!Tip]
> <span data-ttu-id="e5b0e-265">Per mantenere la compatibilità con le versioni precedenti con client e origini che non supportano ancora `PackageIcon` , specificare sia che `PackageIcon` `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-265">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="e5b0e-266">Visual Studio per i `PackageIcon` pacchetti provenienti da un'origine basata su cartelle.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-266">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="e5b0e-267">Creazione di un pacchetto di un file di immagine dell'icona</span><span class="sxs-lookup"><span data-stu-id="e5b0e-267">Packing an icon image file</span></span>

<span data-ttu-id="e5b0e-268">Quando si imballa un file di immagine dell'icona, usare la proprietà per specificare il percorso del `PackageIcon` file dell'icona, relativo alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-268">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="e5b0e-269">Assicurarsi inoltre che il file sia incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-269">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="e5b0e-270">Le dimensioni del file di immagine sono limitate a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-270">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="e5b0e-271">I formati di file supportati includono JPEG e PNG.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-271">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="e5b0e-272">È consigliabile una risoluzione dell'immagine di 128x128.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-272">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="e5b0e-273">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-273">For example:</span></span>

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

<span data-ttu-id="e5b0e-274">[Esempio di icona del pacchetto](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-274">[Package Icon sample](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span></span>

<span data-ttu-id="e5b0e-275">Per nuspec l'equivalente, esaminare il riferimento [ nuspec per l'icona](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-275">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="packagereadmefile"></a><span data-ttu-id="e5b0e-276">PackageReadmeFile</span><span class="sxs-lookup"><span data-stu-id="e5b0e-276">PackageReadmeFile</span></span>

<span data-ttu-id="e5b0e-277">Quando si esegue il pacchetto di un file Leggimi, è necessario usare la proprietà per specificare il percorso del pacchetto, relativo alla `PackageReadmeFile` radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-277">When packing a readme file, you need to use the `PackageReadmeFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="e5b0e-278">Inoltre, è necessario assicurarsi che il file sia incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-278">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="e5b0e-279">I formati di file supportati includono solo Markdown (*md*).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-279">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="e5b0e-280">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-280">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageReadmeFile>readme.md</PackageReadmeFile>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="docs\readme.md" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="e5b0e-281">Per nuspec l'equivalente, esaminare il riferimento [ nuspec per il file Leggimi](nuspec.md#readme).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-281">For the nuspec equivalent, take a look at [nuspec reference for readme](nuspec.md#readme).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="e5b0e-282">Assembly di output</span><span class="sxs-lookup"><span data-stu-id="e5b0e-282">Output assemblies</span></span>

<span data-ttu-id="e5b0e-283">`nuget pack` copia i file di output con le estensioni `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-283">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="e5b0e-284">I file di output copiati dipendono dagli elementi MSBuild forniti dalla `BuiltOutputProjectGroup` destinazione.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-284">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="e5b0e-285">Esistono due proprietà che è possibile usare nel file di progetto o nella riga di comando per controllare la MSBuild  posizione degli assembly di output:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-285">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="e5b0e-286">`IncludeBuildOutput`: valore booleano che determina se gli assembly di output della compilazione devono essere inclusi nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-286">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="e5b0e-287">`BuildOutputTargetFolder`: specifica la cartella in cui devono essere posizionati gli assembly di output.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-287">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="e5b0e-288">Gli assembly di output (e altri file di output) vengono copiati nelle rispettive cartelle per framework.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-288">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="e5b0e-289">Riferimenti ai pacchetti</span><span class="sxs-lookup"><span data-stu-id="e5b0e-289">Package references</span></span>

<span data-ttu-id="e5b0e-290">Vedere [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-290">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="e5b0e-291">Riferimenti da progetto a progetto</span><span class="sxs-lookup"><span data-stu-id="e5b0e-291">Project to project references</span></span>

<span data-ttu-id="e5b0e-292">I riferimenti da progetto a progetto vengono considerati per impostazione predefinita come NuGet riferimenti al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-292">Project to project references are considered by default as NuGet package references.</span></span> <span data-ttu-id="e5b0e-293">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-293">For example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="e5b0e-294">È anche possibile aggiungere i metadati seguenti ai riferimenti del progetto:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-294">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="e5b0e-295">Inclusione di contenuto in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="e5b0e-295">Including content in a package</span></span>

<span data-ttu-id="e5b0e-296">Per includere il contenuto, aggiungere altri metadati all'elemento `<Content>` esistente.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-296">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="e5b0e-297">Per impostazione predefinita tutti gli elementi di tipo"Content" vengono inclusi nel pacchetto, a meno che non si esegua l'override con voci simili al codice seguente:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-297">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="e5b0e-298">Per impostazione predefinita, tutti gli elementi vengono aggiunti alla radice di `content` e della cartella `contentFiles\any\<target_framework>` all'interno di un pacchetto e viene mantenuta la struttura di cartelle relative, a meno che non si specifichi un percorso di pacchetto:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-298">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="e5b0e-299">Se si vuole copiare tutto il contenuto solo in una o più cartelle radice specifiche (anziché in entrambe), è possibile usare la proprietà , che per impostazione predefinita è `content` `contentFiles` MSBuild "content;contentFiles", ma può essere impostata su qualsiasi altro nome `ContentTargetFolders` di cartella.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-299">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="e5b0e-300">Si noti che se si specifica solo "contentFiles" in `ContentTargetFolders`, i file vengono posizionati in `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` in base a `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-300">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="e5b0e-301">`PackagePath` può essere un set di percorsi di destinazione delimitati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-301">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="e5b0e-302">Se si specifica un percorso di pacchetto vuoto, il file viene aggiunto alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-302">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="e5b0e-303">Ad esempio, il codice seguente aggiunge `libuv.txt` a `content\myfiles`, `content\samples` e nella radice del pacchetto:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-303">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="e5b0e-304">È anche disponibile una MSBuild proprietà , che per impostazione predefinita è `$(IncludeContentInPack)` `true` .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-304">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="e5b0e-305">Se questa proprietà viene impostata su `false` in qualsiasi progetto, il contenuto da tale progetto non viene incluso nel pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-305">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="e5b0e-306">Altri metadati specifici di tipo pack che è possibile impostare per uno degli elementi precedenti includono e che impostano i valori e ```<PackageCopyToOutput>``` ```<PackageFlatten>``` sulla voce ```CopyToOutput``` ```Flatten``` ```contentFiles``` nell'output nuspec .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-306">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="e5b0e-307">Oltre agli elementi Content, i metadati `<Pack>` e `<PackagePath>` possono anche essere impostati nei file con l'azione di compilazione Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o None.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-307">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="e5b0e-308">Per fare in modo che il comando pack aggiunga il nome del file al percorso del pacchetto quando si usano modelli con caratteri jolly (glob), il percorso del pacchetto deve terminare con il carattere separatore di cartella. In caso contrario, il percorso del pacchetto viene interpretato come percorso completo, incluso il nome del file.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-308">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="e5b0e-309">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="e5b0e-309">IncludeSymbols</span></span>

<span data-ttu-id="e5b0e-310">Quando si usa `MSBuild -t:pack -p:IncludeSymbols=true`, i file `.pdb` corrispondenti vengono copiati insieme agli altri file di output (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-310">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="e5b0e-311">Si noti che l'impostazione `IncludeSymbols=true` crea un pacchetto regolare *e* un pacchetto di simboli.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-311">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="e5b0e-312">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="e5b0e-312">IncludeSource</span></span>

<span data-ttu-id="e5b0e-313">Equivale a `IncludeSymbols`, ma insieme ai file `.pdb` vengono copiati anche i file di origine.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-313">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="e5b0e-314">Tutti i file di tipo `Compile` vengono copiati in `src\<ProjectName>\` conservando la struttura di cartelle del percorso relativo nel pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-314">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="e5b0e-315">Lo stesso accade anche per i file di origine di qualsiasi `ProjectReference` con `TreatAsPackageReference` impostato su `false`.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-315">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="e5b0e-316">Se un file di tipo Compile è all'esterno della cartella di progetto, viene semplicemente aggiunto a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-316">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="e5b0e-317">Creazione di un pacchetto di un'espressione di licenza o di un file di licenza</span><span class="sxs-lookup"><span data-stu-id="e5b0e-317">Packing a license expression or a license file</span></span>

<span data-ttu-id="e5b0e-318">Quando si usa un'espressione di licenza, usare la `PackageLicenseExpression` proprietà .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-318">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="e5b0e-319">Per un esempio, vedere [l'esempio di espressione di licenza](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-319">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="e5b0e-320">Per altre informazioni sulle espressioni di licenza e sulle licenze accettate da NuGet .org, vedere Metadati [delle licenze.](nuspec.md#license)</span><span class="sxs-lookup"><span data-stu-id="e5b0e-320">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="e5b0e-321">Quando si esegue il pacchetto di un file di licenza, usare la proprietà per specificare il percorso del `PackageLicenseFile` pacchetto, relativo alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-321">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="e5b0e-322">Assicurarsi inoltre che il file sia incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-322">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="e5b0e-323">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-323">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="e5b0e-324">Per un esempio, vedere [l'esempio di file di licenza](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-324">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="e5b0e-325">È possibile `PackageLicenseExpression` specificare solo uno di , e alla `PackageLicenseFile` `PackageLicenseUrl` volta.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-325">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="e5b0e-326">Creazione di un pacchetto di un file senza estensione</span><span class="sxs-lookup"><span data-stu-id="e5b0e-326">Packing a file without an extension</span></span>

<span data-ttu-id="e5b0e-327">In alcuni scenari, ad esempio quando si imballa un file di licenza, è possibile includere un file senza estensione.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-327">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="e5b0e-328">Per motivi cronologici, NuGet  &  MSBuild considerare i percorsi senza un'estensione come directory.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-328">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="e5b0e-329">[File senza un esempio di estensione](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-329">[File without an extension sample](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span></span>

### <a name="istool"></a><span data-ttu-id="e5b0e-330">IsTool</span><span class="sxs-lookup"><span data-stu-id="e5b0e-330">IsTool</span></span>

<span data-ttu-id="e5b0e-331">Quando si usa `MSBuild -t:pack -p:IsTool=true`, tutti i file, come specificato nello scenario [Assembly di output](#output-assemblies), vengono copiati nella cartella `tools` invece che nella cartella `lib`.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-331">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="e5b0e-332">Si noti che questo comportamento è diverso da `DotNetCliTool`, che viene specificato impostando `PackageType` nel file `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-332">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec-file"></a><span data-ttu-id="e5b0e-333">Creazione di un pacchetto con un `.nuspec` file</span><span class="sxs-lookup"><span data-stu-id="e5b0e-333">Packing using a `.nuspec` file</span></span>

<span data-ttu-id="e5b0e-334">Anche se è [consigliabile](../reference/msbuild-targets.md#pack-target) includere tutte le proprietà che in genere si trovano nel file nel file di progetto, è possibile scegliere di usare un file per il pacchetto `.nuspec` del `.nuspec` progetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-334">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="e5b0e-335">Per un progetto non di tipo SDK che usa , è necessario importare in modo che sia possibile eseguire l'attività di `PackageReference` `NuGet.Build.Tasks.Pack.targets` tipo pack.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-335">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="e5b0e-336">È comunque necessario ripristinare il progetto prima di poter imballare un nuspec file.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-336">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="e5b0e-337">Un progetto di tipo SDK include le destinazioni di tipo pack per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-337">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="e5b0e-338">Il framework di destinazione del file di progetto non è pertinente e non viene usato quando si imballa un oggetto nuspec .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-338">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="e5b0e-339">Le tre proprietà MSBuild seguenti sono rilevanti per la creazione di un pacchetto tramite `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="e5b0e-339">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="e5b0e-340">`NuspecFile`: percorso relativo o assoluto per il file `.nuspec` usato per la creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-340">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="e5b0e-341">`NuspecProperties`: elenco con valori delimitati da punto e virgola di coppie chiave=valore.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-341">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="e5b0e-342">A causa del funzionamento dell'analisi della riga di comando, è necessario MSBuild specificare più proprietà nel modo seguente: `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-342">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="e5b0e-343">`NuspecBasePath`: percorso di base per il file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-343">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="e5b0e-344">Se si usa `dotnet.exe` per creare il pacchetto del progetto, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-344">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="e5b0e-345">Se si usa MSBuild per creare il pacchetto del progetto, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-345">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="e5b0e-346">Si noti che la creazione di un oggetto using dotnet.exe o msbuild comporta anche nuspec la compilazione del progetto per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-346">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="e5b0e-347">Questa operazione può essere evitata passando la proprietà a dotnet.exe, che equivale all'impostazione nel file di progetto, insieme all'impostazione ```--no-build``` ```<NoBuild>true</NoBuild> ``` nel file di ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` progetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-347">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="e5b0e-348">Un esempio di file *con estensione csproj* per il pacchetto di nuspec un file è:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-348">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="e5b0e-349">Punti di estensione avanzati per creare un pacchetto personalizzato</span><span class="sxs-lookup"><span data-stu-id="e5b0e-349">Advanced extension points to create customized package</span></span>

<span data-ttu-id="e5b0e-350">La `pack` destinazione fornisce due punti di estensione che vengono eseguiti nella compilazione interna specifica del framework di destinazione.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-350">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="e5b0e-351">I punti di estensione supportano inclusi il contenuto e gli assembly specifici del framework di destinazione in un pacchetto:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-351">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="e5b0e-352">`TargetsForTfmSpecificBuildOutput` target: usare per i file all'interno `lib` della cartella o di una cartella specificata tramite `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-352">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="e5b0e-353">`TargetsForTfmSpecificContentInPackage` target: usare per i file all'esterno di `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-353">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### `TargetsForTfmSpecificBuildOutput`

<span data-ttu-id="e5b0e-354">Scrivere una destinazione personalizzata e specificarla come valore della `$(TargetsForTfmSpecificBuildOutput)` proprietà .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-354">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="e5b0e-355">Per tutti i file che devono accedere a (lib per impostazione predefinita), la destinazione deve scrivere tali file in ItemGroup e impostare `BuildOutputTargetFolder` i due valori di metadati `BuildOutputInPackage` seguenti:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-355">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="e5b0e-356">`FinalOutputPath`: percorso assoluto del file. Se non viene specificato, l'identità viene usata per valutare il percorso di origine.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-356">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="e5b0e-357">`TargetPath`: (Facoltativo) Impostare quando il file deve essere inserito in una sottocartella all'interno di , ad esempio gli assembly satellite che si trova `lib\<TargetFramework>` nelle rispettive cartelle delle impostazioni cultura.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-357">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="e5b0e-358">Il valore predefinito è il nome del file.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-358">Defaults to the name of the file.</span></span>

<span data-ttu-id="e5b0e-359">Esempio:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-359">Example:</span></span>

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

#### `TargetsForTfmSpecificContentInPackage`

<span data-ttu-id="e5b0e-360">Scrivere una destinazione personalizzata e specificarla come valore della `$(TargetsForTfmSpecificContentInPackage)` proprietà .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-360">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="e5b0e-361">Per tutti i file da includere nel pacchetto, la destinazione deve scrivere tali file in ItemGroup e `TfmSpecificPackageFile` impostare i metadati facoltativi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-361">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="e5b0e-362">`PackagePath`: percorso in cui deve essere restituito il file nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-362">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="e5b0e-363">NuGet viene generato un avviso se più file vengono aggiunti allo stesso percorso del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-363">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="e5b0e-364">`BuildAction`: azione di compilazione da assegnare al file, necessaria solo se il percorso del pacchetto si trova nella `contentFiles` cartella .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-364">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="e5b0e-365">Il valore predefinito è "None".</span><span class="sxs-lookup"><span data-stu-id="e5b0e-365">Defaults to "None".</span></span>

<span data-ttu-id="e5b0e-366">Esempio:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-366">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="e5b0e-367">Destinazione restore</span><span class="sxs-lookup"><span data-stu-id="e5b0e-367">restore target</span></span>

<span data-ttu-id="e5b0e-368">`MSBuild -t:restore` (usato da `nuget restore` e `dotnet restore` con progetti .NET Core) consente di ripristinare i pacchetti a cui si fa riferimento nel file di progetto, come segue:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-368">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="e5b0e-369">Lettura di tutti i riferimenti da progetto a progetto</span><span class="sxs-lookup"><span data-stu-id="e5b0e-369">Read all project to project references</span></span>
1. <span data-ttu-id="e5b0e-370">Lettura delle proprietà del progetto per trovare la cartella intermedia e i framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="e5b0e-370">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="e5b0e-371">Passare MSBuild dati a NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="e5b0e-371">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="e5b0e-372">Esecuzione di restore</span><span class="sxs-lookup"><span data-stu-id="e5b0e-372">Run restore</span></span>
1. <span data-ttu-id="e5b0e-373">Download dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="e5b0e-373">Download packages</span></span>
1. <span data-ttu-id="e5b0e-374">Scrittura dei file di asset, delle destinazioni e delle proprietà</span><span class="sxs-lookup"><span data-stu-id="e5b0e-374">Write assets file, targets, and props</span></span>

<span data-ttu-id="e5b0e-375">La `restore` destinazione funziona per i progetti che usano il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-375">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="e5b0e-376">`MSBuild 16.5+` include anche [il supporto del consenso](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) esplicito per il `packages.config` formato.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-376">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="e5b0e-377">La `restore` destinazione non deve essere [eseguita](#restoring-and-building-with-one-msbuild-command) in combinazione con la `build` destinazione .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-377">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="e5b0e-378">Ripristino delle proprietà</span><span class="sxs-lookup"><span data-stu-id="e5b0e-378">Restore properties</span></span>

<span data-ttu-id="e5b0e-379">Le impostazioni di ripristino aggiuntive possono MSBuild derivare dalle proprietà nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-379">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="e5b0e-380">I valori possono essere impostati anche dalla riga di comando tramite l'opzione `-p:` (vedere gli esempi riportati di seguito).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-380">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="e5b0e-381">Proprietà</span><span class="sxs-lookup"><span data-stu-id="e5b0e-381">Property</span></span> | <span data-ttu-id="e5b0e-382">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e5b0e-382">Description</span></span> |
|--------|--------|
| `RestoreSources` | <span data-ttu-id="e5b0e-383">Elenco delimitato da punto e virgola delle origini di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-383">Semicolon-delimited list of package sources.</span></span> |
| `RestorePackagesPath` | <span data-ttu-id="e5b0e-384">Percorso della cartella dei pacchetti dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-384">User packages folder path.</span></span> |
| `RestoreDisableParallel` | <span data-ttu-id="e5b0e-385">Consente di limitare i download a uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-385">Limit downloads to one at a time.</span></span> |
| `RestoreConfigFile` | <span data-ttu-id="e5b0e-386">Percorso per un file `Nuget.Config` da applicare.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-386">Path to a `Nuget.Config` file to apply.</span></span> |
| `RestoreNoCache` | <span data-ttu-id="e5b0e-387">Se true, evita l'uso di pacchetti memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-387">If true, avoids using cached packages.</span></span> <span data-ttu-id="e5b0e-388">Vedere [Gestione dei pacchetti globali e delle cartelle della cache.](../consume-packages/managing-the-global-packages-and-cache-folders.md)</span><span class="sxs-lookup"><span data-stu-id="e5b0e-388">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| `RestoreIgnoreFailedSources` | <span data-ttu-id="e5b0e-389">Se true, ignora le origini di pacchetti in errore o mancanti.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-389">If true, ignores failing or missing package sources.</span></span> |
| `RestoreFallbackFolders` | <span data-ttu-id="e5b0e-390">Cartelle di fallback, usate nello stesso modo in cui viene usata la cartella dei pacchetti utente.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-390">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| `RestoreAdditionalProjectSources` | <span data-ttu-id="e5b0e-391">Origini aggiuntive da usare durante il ripristino.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-391">Additional sources to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFolders` | <span data-ttu-id="e5b0e-392">Cartelle di fallback aggiuntive da usare durante il ripristino.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-392">Additional fallback folders to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | <span data-ttu-id="e5b0e-393">Esclude le cartelle di fallback specificate in `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="e5b0e-393">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| `RestoreTaskAssemblyFile` | <span data-ttu-id="e5b0e-394">Percorso di `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-394">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| `RestoreGraphProjectInput` | <span data-ttu-id="e5b0e-395">Elenco delimitato da punto e virgola dei progetti da ripristinare, che deve contenere percorsi assoluti.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-395">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| `RestoreUseSkipNonexistentTargets`  | <span data-ttu-id="e5b0e-396">Quando i progetti vengono raccolti tramite MSBuild , determina se vengono raccolti usando l'ottimizzazione. `SkipNonexistentTargets`</span><span class="sxs-lookup"><span data-stu-id="e5b0e-396">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="e5b0e-397">Se non è impostato, il valore predefinito è `true` .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-397">When not set, defaults to `true`.</span></span> <span data-ttu-id="e5b0e-398">La conseguenza è un comportamento fail-fast quando non è possibile importare le destinazioni di un progetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-398">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| `MSBuildProjectExtensionsPath` | <span data-ttu-id="e5b0e-399">Cartella di output, che per impostazione predefinita `BaseIntermediateOutputPath` è e la cartella `obj` .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-399">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| `RestoreForce` | <span data-ttu-id="e5b0e-400">Nei progetti basati su PackageReference, forza la risoluzione di tutte le dipendenze anche se l'ultimo ripristino ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-400">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="e5b0e-401">La specifica di questo flag è simile all'eliminazione del `project.assets.json` file.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-401">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="e5b0e-402">In questo modo non viene ignorata la http-cache.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-402">This does not bypass the http-cache.</span></span> |
| `RestorePackagesWithLockFile` | <span data-ttu-id="e5b0e-403">Acconsente esplicitamente all'uso di un file di blocco.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-403">Opts into the usage of a lock file.</span></span> |
| `RestoreLockedMode` | <span data-ttu-id="e5b0e-404">Eseguire il ripristino in modalità bloccata.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-404">Run restore in locked mode.</span></span> <span data-ttu-id="e5b0e-405">Ciò significa che il ripristino non rivaluta le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-405">This means that restore will not reevaluate the dependencies.</span></span> |
| `NuGetLockFilePath` | <span data-ttu-id="e5b0e-406">Percorso personalizzato per il file di blocco.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-406">A custom location for the lock file.</span></span> <span data-ttu-id="e5b0e-407">Il percorso predefinito è accanto al progetto ed è denominato `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-407">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| `RestoreForceEvaluate` | <span data-ttu-id="e5b0e-408">Forza il ripristino per ricalcolare le dipendenze e aggiornare il file di blocco senza alcun avviso.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-408">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| `RestorePackagesConfig` | <span data-ttu-id="e5b0e-409">Opzione di consenso esplicito che ripristina i progetti con packages.config. Supporto solo `MSBuild -t:restore` con .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-409">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| `RestoreUseStaticGraphEvaluation` | <span data-ttu-id="e5b0e-410">Opzione di consenso esplicito per l'uso della valutazione a MSBuild grafo statico anziché della valutazione standard.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-410">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="e5b0e-411">La valutazione dei grafi statici è una funzionalità sperimentale notevolmente più veloce per i repository e le soluzioni di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-411">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="e5b0e-412">Esempio</span><span class="sxs-lookup"><span data-stu-id="e5b0e-412">Examples</span></span>

<span data-ttu-id="e5b0e-413">Riga di comando:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-413">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="e5b0e-414">File di progetto:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-414">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="e5b0e-415">Output del ripristino</span><span class="sxs-lookup"><span data-stu-id="e5b0e-415">Restore outputs</span></span>

<span data-ttu-id="e5b0e-416">Il ripristino crea i file seguenti nella cartella `obj` di compilazione:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-416">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="e5b0e-417">File</span><span class="sxs-lookup"><span data-stu-id="e5b0e-417">File</span></span> | <span data-ttu-id="e5b0e-418">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e5b0e-418">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="e5b0e-419">Contiene il grafico delle dipendenze di tutti i riferimenti al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-419">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="e5b0e-420">Riferimenti alle MSBuild proprietà contenute nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="e5b0e-420">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="e5b0e-421">Riferimenti alle MSBuild destinazioni contenute nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="e5b0e-421">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="e5b0e-422">Ripristino e compilazione con MSBuild un comando</span><span class="sxs-lookup"><span data-stu-id="e5b0e-422">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="e5b0e-423">A causa del fatto che può ripristinare pacchetti che portano a destinazione e proprietà, le valutazioni di ripristino e compilazione vengono eseguite NuGet MSBuild con proprietà globali diverse.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-423">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="e5b0e-424">Ciò significa che quanto segue avrà un comportamento imprevedibile e spesso errato.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-424">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="e5b0e-425">L'approccio consigliato è invece:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-425">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="e5b0e-426">La stessa logica si applica ad altre destinazioni simili a `build` .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-426">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a><span data-ttu-id="e5b0e-427">Ripristino di PackageReference e packages.config progetti con MSBuild</span><span class="sxs-lookup"><span data-stu-id="e5b0e-427">Restoring PackageReference and packages.config projects with MSBuild</span></span>

<span data-ttu-id="e5b0e-428">Con MSBuild la versione 16.5+, packages.config sono supportati anche per `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="e5b0e-428">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="e5b0e-429">`packages.config` restore è disponibile solo con `MSBuild 16.5+` e non con `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="e5b0e-429">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="e5b0e-430">Ripristino con valutazione MSBuild di grafi statici</span><span class="sxs-lookup"><span data-stu-id="e5b0e-430">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="e5b0e-431">Con MSBuild la versione 16.6+, è stata aggiunta una funzionalità sperimentale per usare la valutazione del grafo statico dalla riga di comando che migliora significativamente il tempo di ripristino per repository NuGet di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-431">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="e5b0e-432">In alternativa, è possibile abilitarlo impostando la proprietà in un oggetto Directory.Build.Props.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-432">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="e5b0e-433">A Visual Studio 2019.x e 5.x, questa funzionalità è considerata sperimentale e NuGet acconsente esplicitamente.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-433">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="e5b0e-434">Seguire [ NuGet /Home#9803](https://github.com/NuGet/Home/issues/9803) per informazioni dettagliate su quando questa funzionalità verrà abilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-434">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="e5b0e-435">Il ripristino a grafo statico modifica la parte msbuild del ripristino, la lettura e la valutazione del progetto, ma non l'algoritmo di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-435">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="e5b0e-436">L'algoritmo di ripristino è lo stesso in tutti gli NuGet strumenti ( NuGet exe, MSBuild exe, dotnet.exe e Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-436">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="e5b0e-437">In pochissimi scenari, il ripristino di grafi statici può comportarsi in modo diverso dal ripristino corrente e alcuni PackageReference o ProjectReference dichiarati potrebbero risultare mancanti.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-437">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="e5b0e-438">Per semplificare l'esecuzione, come controllo una sola volta, quando si esegue la migrazione al ripristino statico dei grafi, è consigliabile eseguire:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-438">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="e5b0e-439">NuGet non *deve segnalare* alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-439">NuGet should *not* report any changes.</span></span> <span data-ttu-id="e5b0e-440">Se viene visualizzata una discrepanza, determinare un problema in [ NuGet /Home](https://github.com/nuget/home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="e5b0e-440">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="e5b0e-441">Sostituzione di una libreria da un grafico di ripristino</span><span class="sxs-lookup"><span data-stu-id="e5b0e-441">Replacing one library from a restore graph</span></span>

<span data-ttu-id="e5b0e-442">Se un ripristino restituisce l'assembly errato, è possibile escludere la scelta predefinita di tali pacchetti e sostituirla con la propria scelta.</span><span class="sxs-lookup"><span data-stu-id="e5b0e-442">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="e5b0e-443">Prima di tutto, con un `PackageReference` di livello superiore, escludere tutti gli asset:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-443">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="e5b0e-444">Aggiungere quindi il riferimento personalizzato alla copia locale appropriata della DLL:</span><span class="sxs-lookup"><span data-stu-id="e5b0e-444">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```