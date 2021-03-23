---
title: NuGet Pack e Restore come MSBuild destinazioni
description: NuGet Pack e Restore possono funzionare direttamente come MSBuild destinazioni con NuGet 4.0 +.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 9d40d43d972537ee1cb11d54194ed6450ccd0b6e
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2021
ms.locfileid: "104858966"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="1ee0a-103">NuGet Pack e Restore come MSBuild destinazioni</span><span class="sxs-lookup"><span data-stu-id="1ee0a-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="1ee0a-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="1ee0a-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="1ee0a-105">Con il formato [PackageReference](../consume-packages/package-references-in-project-files.md) , NuGet 4.0 + può archiviare tutti i metadati del manifesto direttamente all'interno di un file di progetto anziché usare un `.nuspec` file separato.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="1ee0a-106">Con MSBuild 15.1 +, NuGet è anche un MSBuild cittadino di prima classe con le `pack` `restore` destinazioni e come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="1ee0a-107">Queste destinazioni consentono di utilizzare NuGet come si farebbe con qualsiasi altra MSBuild attività o destinazione.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="1ee0a-108">Per istruzioni sulla creazione di un NuGet pacchetto con MSBuild , vedere [creare un NuGet pacchetto usando MSBuild ](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="1ee0a-109">(Per NuGet 3. x e versioni precedenti, è invece possibile usare i comandi [Pack](../reference/cli-reference/cli-ref-pack.md) e [Restore](../reference/cli-reference/cli-ref-restore.md) tramite l'interfaccia della riga di comando NuGet .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="1ee0a-110">Ordine di compilazione delle destinazioni</span><span class="sxs-lookup"><span data-stu-id="1ee0a-110">Target build order</span></span>

<span data-ttu-id="1ee0a-111">Poiché `pack` e `restore` sono  MSBuild destinazioni, è possibile accedervi per migliorare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="1ee0a-112">Si immagini, ad esempio, di voler copiare il pacchetto in una condivisione di rete dopo averla comprimendo.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-112">For example, let's say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="1ee0a-113">È possibile farlo aggiungendo quanto segue nel file di progetto:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="1ee0a-114">Analogamente, è possibile scrivere un' MSBuild attività, scrivere la propria destinazione e utilizzare NuGet le proprietà nell' MSBuild attività.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="1ee0a-115">`$(OutputPath)` è relativo e prevede che si esegua il comando dalla radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="1ee0a-116">Destinazione pack</span><span class="sxs-lookup"><span data-stu-id="1ee0a-116">pack target</span></span>

<span data-ttu-id="1ee0a-117">Per i progetti .NET che usano il `PackageReference` formato, usando `msbuild -t:pack` disegna gli input dal file di progetto da usare per la creazione di un NuGet pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="1ee0a-118">Nella tabella seguente vengono descritte le MSBuild proprietà che è possibile aggiungere a un file di progetto all'interno del primo `<PropertyGroup>` nodo.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="1ee0a-119">È possibile apportare facilmente queste modifiche in Visual Studio 2017 e versioni successive facendo clic con il pulsante destro del mouse sul progetto e scegliendo **Modifica {nome_progetto}** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="1ee0a-120">Per praticità, la tabella è organizzata in base alla proprietà equivalente in un [ `.nuspec` file](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1ee0a-121">`Owners` le `Summary` proprietà e da `.nuspec` non sono supportate con MSBuild .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-121">`Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="1ee0a-122">Attributo/ nuspec valore</span><span class="sxs-lookup"><span data-stu-id="1ee0a-122">Attribute/nuspec Value</span></span> | <span data-ttu-id="1ee0a-123">Proprietà diMSBuild</span><span class="sxs-lookup"><span data-stu-id="1ee0a-123">MSBuild Property</span></span> | <span data-ttu-id="1ee0a-124">Predefinito</span><span class="sxs-lookup"><span data-stu-id="1ee0a-124">Default</span></span> | <span data-ttu-id="1ee0a-125">Note</span><span class="sxs-lookup"><span data-stu-id="1ee0a-125">Notes</span></span> |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | <span data-ttu-id="1ee0a-126">`$(AssemblyName)` da MSBuild</span><span class="sxs-lookup"><span data-stu-id="1ee0a-126">`$(AssemblyName)` from MSBuild</span></span> |
| `Version` | `PackageVersion` | <span data-ttu-id="1ee0a-127">Versione</span><span class="sxs-lookup"><span data-stu-id="1ee0a-127">Version</span></span> | <span data-ttu-id="1ee0a-128">Si tratta di un semver compatibile, ad esempio, `1.0.0` `1.0.0-beta` o `1.0.0-beta-00345`</span><span class="sxs-lookup"><span data-stu-id="1ee0a-128">This is semver compatible, for example `1.0.0`, `1.0.0-beta`, or `1.0.0-beta-00345`</span></span> |
| `VersionPrefix` | `PackageVersionPrefix` | <span data-ttu-id="1ee0a-129">empty</span><span class="sxs-lookup"><span data-stu-id="1ee0a-129">empty</span></span> | <span data-ttu-id="1ee0a-130">Impostazione delle `PackageVersion` sovrascritture `PackageVersionPrefix`</span><span class="sxs-lookup"><span data-stu-id="1ee0a-130">Setting `PackageVersion` overwrites `PackageVersionPrefix`</span></span> |
| `VersionSuffix` | `PackageVersionSuffix` | <span data-ttu-id="1ee0a-131">empty</span><span class="sxs-lookup"><span data-stu-id="1ee0a-131">empty</span></span> | <span data-ttu-id="1ee0a-132">`$(VersionSuffix)` da MSBuild .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-132">`$(VersionSuffix)` from MSBuild.</span></span> <span data-ttu-id="1ee0a-133">Impostazione delle `PackageVersion` sovrascritture `PackageVersionSuffix`</span><span class="sxs-lookup"><span data-stu-id="1ee0a-133">Setting `PackageVersion` overwrites `PackageVersionSuffix`</span></span> |
| `Authors` | `Authors` | <span data-ttu-id="1ee0a-134">Nome utente dell'utente corrente</span><span class="sxs-lookup"><span data-stu-id="1ee0a-134">Username of the current user</span></span> | <span data-ttu-id="1ee0a-135">Elenco delimitato da punti e virgola di autori di pacchetti, corrispondenti ai nomi di profilo in nuget.org. Questi vengono visualizzati nella NuGet raccolta in NuGet.org e vengono usati per fare riferimento a pacchetti con gli stessi autori.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-135">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Owners` | <span data-ttu-id="1ee0a-136">N/D</span><span class="sxs-lookup"><span data-stu-id="1ee0a-136">N/A</span></span> | <span data-ttu-id="1ee0a-137">Non presente in nuspec</span><span class="sxs-lookup"><span data-stu-id="1ee0a-137">Not present in nuspec</span></span> | |
| `Title` | `Title` | <span data-ttu-id="1ee0a-138">Il tipo `PackageId`</span><span class="sxs-lookup"><span data-stu-id="1ee0a-138">The `PackageId`</span></span> | <span data-ttu-id="1ee0a-139">Titolo del pacchetto facilmente comprensibile per l'utente, usato di solito per la visualizzazione dell'interfaccia utente, ad esempio in nuget.org e in Gestione pacchetti in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| `Description` | `Description` | <span data-ttu-id="1ee0a-140">"Descrizione del pacchetto"</span><span class="sxs-lookup"><span data-stu-id="1ee0a-140">"Package Description"</span></span> | <span data-ttu-id="1ee0a-141">Descrizione lunga per l'assembly.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-141">A long description for the assembly.</span></span> <span data-ttu-id="1ee0a-142">Se `PackageDescription` viene omesso, questa proprietà viene utilizzata anche come descrizione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-142">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | `Copyright` | <span data-ttu-id="1ee0a-143">empty</span><span class="sxs-lookup"><span data-stu-id="1ee0a-143">empty</span></span> | <span data-ttu-id="1ee0a-144">Informazioni sul copyright per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-144">Copyright details for the package.</span></span> |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | <span data-ttu-id="1ee0a-145">Valore booleano che specifica se il client deve richiedere al consumer di accettare la licenza del pacchetto prima di installarlo.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-145">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| `license` | `PackageLicenseExpression` | <span data-ttu-id="1ee0a-146">empty</span><span class="sxs-lookup"><span data-stu-id="1ee0a-146">empty</span></span> | <span data-ttu-id="1ee0a-147">Corrisponde a `<license type="expression">`.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-147">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="1ee0a-148">Vedere [compressione di un'espressione di licenza o di un file di licenza](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-148">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `license` | `PackageLicenseFile` | <span data-ttu-id="1ee0a-149">empty</span><span class="sxs-lookup"><span data-stu-id="1ee0a-149">empty</span></span> | <span data-ttu-id="1ee0a-150">Percorso di un file di licenza all'interno del pacchetto se si usa una licenza personalizzata o una licenza a cui non è stato assegnato un identificatore SPDX.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-150">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="1ee0a-151">È necessario comprimere in modo esplicito il file di licenza a cui si fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-151">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="1ee0a-152">Corrisponde a `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-152">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="1ee0a-153">Vedere [compressione di un'espressione di licenza o di un file di licenza](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-153">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `LicenseUrl` | `PackageLicenseUrl` | <span data-ttu-id="1ee0a-154">empty</span><span class="sxs-lookup"><span data-stu-id="1ee0a-154">empty</span></span> | <span data-ttu-id="1ee0a-155">L'oggetto `PackageLicenseUrl` è deprecato.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-155">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="1ee0a-156">In sostituzione usare `PackageLicenseExpression` o `PackageLicenseFile`.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-156">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `ProjectUrl` | `PackageProjectUrl` | <span data-ttu-id="1ee0a-157">empty</span><span class="sxs-lookup"><span data-stu-id="1ee0a-157">empty</span></span> | |
| `Icon` | `PackageIcon` | <span data-ttu-id="1ee0a-158">empty</span><span class="sxs-lookup"><span data-stu-id="1ee0a-158">empty</span></span> | <span data-ttu-id="1ee0a-159">Percorso di un'immagine nel pacchetto da utilizzare come icona del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-159">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="1ee0a-160">È necessario comprimere in modo esplicito il file di immagine icona a cui si fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-160">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="1ee0a-161">Per altre informazioni, vedere [compressione di un file di immagine icona](#packing-an-icon-image-file) e [ `icon` metadati](/nuget/reference/nuspec#icon).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-161">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](/nuget/reference/nuspec#icon).</span></span> |
| `IconUrl` | `PackageIconUrl` | <span data-ttu-id="1ee0a-162">empty</span><span class="sxs-lookup"><span data-stu-id="1ee0a-162">empty</span></span> | <span data-ttu-id="1ee0a-163">`PackageIconUrl` è deprecato a favore di `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-163">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="1ee0a-164">Tuttavia, per la migliore esperienza di livello inferiore, è necessario specificare oltre `PackageIconUrl` a `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-164">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| `Tags` | `PackageTags` | <span data-ttu-id="1ee0a-165">empty</span><span class="sxs-lookup"><span data-stu-id="1ee0a-165">empty</span></span> | <span data-ttu-id="1ee0a-166">Elenco di tag con valori delimitati da punto e virgola che designa il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-166">A semicolon-delimited list of tags that designates the package.</span></span> |
| `ReleaseNotes` | `PackageReleaseNotes` | <span data-ttu-id="1ee0a-167">empty</span><span class="sxs-lookup"><span data-stu-id="1ee0a-167">empty</span></span> | <span data-ttu-id="1ee0a-168">Note sulla versione per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-168">Release notes for the package.</span></span> |
| `Repository/Url` | `RepositoryUrl` | <span data-ttu-id="1ee0a-169">empty</span><span class="sxs-lookup"><span data-stu-id="1ee0a-169">empty</span></span> | <span data-ttu-id="1ee0a-170">URL del repository usato per clonare o recuperare il codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-170">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="1ee0a-171">Esempio: *https://github.com/ NuGet / NuGet . Client. git*.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-171">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `Repository/Type` | `RepositoryType` | <span data-ttu-id="1ee0a-172">empty</span><span class="sxs-lookup"><span data-stu-id="1ee0a-172">empty</span></span> | <span data-ttu-id="1ee0a-173">Tipo di repository.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-173">Repository type.</span></span> <span data-ttu-id="1ee0a-174">Esempi: `git` (impostazione predefinita), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-174">Examples: `git` (default), `tfs`.</span></span> |
| `Repository/Branch` | `RepositoryBranch` | <span data-ttu-id="1ee0a-175">empty</span><span class="sxs-lookup"><span data-stu-id="1ee0a-175">empty</span></span> | <span data-ttu-id="1ee0a-176">Informazioni facoltative sul ramo del repository.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-176">Optional repository branch information.</span></span> <span data-ttu-id="1ee0a-177">`RepositoryUrl` per includere questa proprietà, è necessario specificare anche.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-177">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="1ee0a-178">Esempio: *Master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-178">Example: *master* (NuGet 4.7.0+).</span></span> |
| `Repository/Commit` | `RepositoryCommit` | <span data-ttu-id="1ee0a-179">empty</span><span class="sxs-lookup"><span data-stu-id="1ee0a-179">empty</span></span> | <span data-ttu-id="1ee0a-180">Commit o insieme di modifiche facoltativo del repository per indicare l'origine su cui è stato compilato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-180">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="1ee0a-181">`RepositoryUrl` per includere questa proprietà, è necessario specificare anche.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-181">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="1ee0a-182">Esempio: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-182">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | <span data-ttu-id="1ee0a-183">Non supportato</span><span class="sxs-lookup"><span data-stu-id="1ee0a-183">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="1ee0a-184">Input destinazione pack</span><span class="sxs-lookup"><span data-stu-id="1ee0a-184">pack target inputs</span></span>

| <span data-ttu-id="1ee0a-185">Proprietà</span><span class="sxs-lookup"><span data-stu-id="1ee0a-185">Property</span></span> | <span data-ttu-id="1ee0a-186">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1ee0a-186">Description</span></span> |
| - | - |
| `IsPackable` | <span data-ttu-id="1ee0a-187">Valore booleano che specifica se dal progetto può essere creato un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-187">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="1ee0a-188">Il valore predefinito è `true`.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-188">The default value is `true`.</span></span> |
| `SuppressDependenciesWhenPacking` | <span data-ttu-id="1ee0a-189">Impostare su `true` per non visualizzare le dipendenze del pacchetto dal NuGet pacchetto generato.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-189">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| `PackageVersion` | <span data-ttu-id="1ee0a-190">Specifica la versione che avrà il pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-190">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="1ee0a-191">Accetta tutte le forme della NuGet stringa di versione.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-191">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="1ee0a-192">Il valore predefinito corrisponde al valore di `$(Version)`, vale a dire della proprietà `Version` nel progetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-192">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| `PackageId` | <span data-ttu-id="1ee0a-193">Specifica il nome del pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-193">Specifies the name for the resulting package.</span></span> <span data-ttu-id="1ee0a-194">Se non specificato, l'impostazione predefinita per l'operazione `pack` corrisponde all'uso di `AssemblyName` o del nome della directory come nome del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-194">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| `PackageDescription` | <span data-ttu-id="1ee0a-195">Descrizione lunga del pacchetto per la visualizzazione dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-195">A long description of the package for UI display.</span></span> |
| `Authors` | <span data-ttu-id="1ee0a-196">Elenco delimitato da punti e virgola di autori di pacchetti, corrispondenti ai nomi di profilo in nuget.org. Questi vengono visualizzati nella NuGet raccolta in NuGet.org e vengono usati per fare riferimento a pacchetti con gli stessi autori.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-196">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Description` | <span data-ttu-id="1ee0a-197">Descrizione lunga per l'assembly.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-197">A long description for the assembly.</span></span> <span data-ttu-id="1ee0a-198">Se `PackageDescription` viene omesso, questa proprietà viene utilizzata anche come descrizione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-198">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | <span data-ttu-id="1ee0a-199">Informazioni sul copyright per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-199">Copyright details for the package.</span></span> |
| `PackageRequireLicenseAcceptance` | <span data-ttu-id="1ee0a-200">Valore booleano che specifica se il client deve richiedere al consumer di accettare la licenza del pacchetto prima di installarlo.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-200">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="1ee0a-201">Il valore predefinito è `false`.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-201">The default is `false`.</span></span> |
| `DevelopmentDependency` | <span data-ttu-id="1ee0a-202">Valore booleano che specifica se il pacchetto è contrassegnato come dipendenza solo per lo sviluppo, impedendo che il pacchetto venga incluso come dipendenza in altri pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-202">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="1ee0a-203">Con `PackageReference` ( NuGet 4.8 +), questo flag indica anche che gli asset in fase di compilazione vengono esclusi dalla compilazione.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-203">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="1ee0a-204">Per altre informazioni, vedere [Supporto di DevelopmentDependency per PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-204">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| `PackageLicenseExpression` | <span data-ttu-id="1ee0a-205">[Identificatore di licenza SPDX](https://spdx.org/licenses/) o espressione, ad esempio `Apache-2.0` .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-205">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="1ee0a-206">Per ulteriori informazioni, vedere [compressione di un'espressione di licenza o di un file di licenza](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-206">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `PackageLicenseFile` | <span data-ttu-id="1ee0a-207">Percorso di un file di licenza all'interno del pacchetto se si usa una licenza personalizzata o una licenza a cui non è stato assegnato un identificatore SPDX.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-207">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| `PackageLicenseUrl` | <span data-ttu-id="1ee0a-208">L'oggetto `PackageLicenseUrl` è deprecato.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-208">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="1ee0a-209">In sostituzione usare `PackageLicenseExpression` o `PackageLicenseFile`.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-209">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `PackageProjectUrl` | |
| `PackageIcon` | <span data-ttu-id="1ee0a-210">Specifica il percorso dell'icona del pacchetto, relativo alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-210">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="1ee0a-211">Per altre informazioni, vedere [compressione di un file di immagine icona](#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-211">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| `PackageReleaseNotes` | <span data-ttu-id="1ee0a-212">Note sulla versione per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-212">Release notes for the package.</span></span> |
| `PackageTags` | <span data-ttu-id="1ee0a-213">Elenco di tag con valori delimitati da punto e virgola che designa il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-213">A semicolon-delimited list of tags that designates the package.</span></span> |
| `PackageOutputPath` | <span data-ttu-id="1ee0a-214">Determina il percorso di output in cui verrà rilasciato il pacchetto creato.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-214">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="1ee0a-215">Il valore predefinito è `$(OutputPath)`.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-215">Default is `$(OutputPath)`.</span></span> |
| `IncludeSymbols` | <span data-ttu-id="1ee0a-216">Valore booleano che indica se al momento della creazione del pacchetto deve essere creato un pacchetto aggiuntivo di simboli.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-216">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="1ee0a-217">Il formato del pacchetto di simboli è controllato dalla proprietà `SymbolPackageFormat`.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-217">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="1ee0a-218">Per ulteriori informazioni, vedere [IncludeSymbols](#includesymbols).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-218">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| `IncludeSource` | <span data-ttu-id="1ee0a-219">Valore booleano che indica se il processo di creazione del pacchetto deve creare un pacchetto di origine.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-219">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="1ee0a-220">Il pacchetto di origine contiene il codice sorgente della libreria, nonché i file PDB.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-220">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="1ee0a-221">I file di origine vengono posizionati nella directory `src/ProjectName` del file del pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-221">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="1ee0a-222">Per ulteriori informazioni, vedere [IncludeSource](#includesource).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-222">For more information, see [IncludeSource](#includesource).</span></span> |
| `PackageType` | |
| `IsTool` | <span data-ttu-id="1ee0a-223">Specifica se tutti i file di output devono essere copiati nella cartella *tools* anziché nella cartella *lib*.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-223">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="1ee0a-224">Per ulteriori informazioni, vedere la pagina relativa allo [strumento](#istool).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-224">For more information, see [IsTool](#istool).</span></span> |
| `RepositoryUrl` | <span data-ttu-id="1ee0a-225">URL del repository usato per clonare o recuperare il codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-225">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="1ee0a-226">Esempio: *https://github.com/ NuGet / NuGet . Client. git*.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-226">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `RepositoryType` | <span data-ttu-id="1ee0a-227">Tipo di repository.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-227">Repository type.</span></span> <span data-ttu-id="1ee0a-228">Esempi: `git` (impostazione predefinita), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-228">Examples: `git` (default), `tfs`.</span></span> |
| `RepositoryBranch` | <span data-ttu-id="1ee0a-229">Informazioni facoltative sul ramo del repository.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-229">Optional repository branch information.</span></span> <span data-ttu-id="1ee0a-230">`RepositoryUrl` per includere questa proprietà, è necessario specificare anche.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-230">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="1ee0a-231">Esempio: *Master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-231">Example: *master* (NuGet 4.7.0+).</span></span> |
| `RepositoryCommit` | <span data-ttu-id="1ee0a-232">Commit o insieme di modifiche facoltativo del repository per indicare l'origine su cui è stato compilato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-232">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="1ee0a-233">`RepositoryUrl` per includere questa proprietà, è necessario specificare anche.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-233">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="1ee0a-234">Esempio: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-234">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `SymbolPackageFormat` | <span data-ttu-id="1ee0a-235">Specifica il formato del pacchetto di simboli.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-235">Specifies the format of the symbols package.</span></span> <span data-ttu-id="1ee0a-236">Se "symbols. nupkg", un pacchetto di simboli legacy viene creato con un'estensione *. symbols. nupkg* che contiene PDB, dll e altri file di output.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-236">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="1ee0a-237">Se "snupkg", viene creato un pacchetto di simboli snupkg contenente il PDB portatile.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-237">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="1ee0a-238">Il valore predefinito è "symbols. nupkg".</span><span class="sxs-lookup"><span data-stu-id="1ee0a-238">The default is "symbols.nupkg".</span></span> |
| `NoPackageAnalysis` | <span data-ttu-id="1ee0a-239">Specifica che `pack` non deve eseguire l'analisi del pacchetto dopo la compilazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-239">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| `MinClientVersion` | <span data-ttu-id="1ee0a-240">Specifica la versione minima del NuGet client che può installare questo pacchetto, applicato da nuget.exe e da Gestione pacchetti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-240">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| `IncludeBuildOutput` | <span data-ttu-id="1ee0a-241">Questo valore booleano specifica se gli assembly di output di compilazione devono essere compressi nel file con *estensione nupkg* o meno.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-241">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| `IncludeContentInPack` | <span data-ttu-id="1ee0a-242">Questo valore booleano specifica se gli elementi che hanno un tipo di `Content` sono inclusi automaticamente nel pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-242">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="1ee0a-243">Il valore predefinito è `true`.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-243">The default is `true`.</span></span> |
| `BuildOutputTargetFolder` | <span data-ttu-id="1ee0a-244">Specifica la cartella in cui inserire gli assembly di output.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-244">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="1ee0a-245">Gli assembly di output (e altri file di output) vengono copiati nelle rispettive cartelle per framework.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-245">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="1ee0a-246">Per altre informazioni, vedere [assembly di output](#output-assemblies).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-246">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| `ContentTargetFolders` | <span data-ttu-id="1ee0a-247">Specifica il percorso predefinito in cui devono essere inseriti tutti i file di contenuto se `PackagePath` non viene specificato.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-247">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="1ee0a-248">Il valore predefinito è "content;contentFiles".</span><span class="sxs-lookup"><span data-stu-id="1ee0a-248">The default value is "content;contentFiles".</span></span> <span data-ttu-id="1ee0a-249">Per altre informazioni, vedere [Including content in a package](#including-content-in-a-package) (Includere contenuto in un pacchetto).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-249">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| `NuspecFile` | <span data-ttu-id="1ee0a-250">Percorso relativo o assoluto del *.nuspec* file usato per la compressione.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-250">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="1ee0a-251">Se specificato, viene usato **esclusivamente** per le informazioni di creazione del pacchetto e tutte le informazioni nei progetti non vengono usate.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-251">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="1ee0a-252">Per altre informazioni, vedere [compressione con un .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-252">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecBasePath` | <span data-ttu-id="1ee0a-253">Percorso di base del *.nuspec* file.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-253">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="1ee0a-254">Per altre informazioni, vedere [compressione con un .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-254">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecProperties` | <span data-ttu-id="1ee0a-255">Elenco con valori delimitati da punto e virgola di coppie chiave=valore.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-255">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="1ee0a-256">Per altre informazioni, vedere [compressione con un .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-256">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="1ee0a-257">Scenari pack</span><span class="sxs-lookup"><span data-stu-id="1ee0a-257">pack scenarios</span></span>

### <a name="suppressing-dependencies"></a><span data-ttu-id="1ee0a-258">Eliminazione delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="1ee0a-258">Suppressing dependencies</span></span>

<span data-ttu-id="1ee0a-259">Per non visualizzare le dipendenze del pacchetto dal NuGet pacchetto generato, impostare `SuppressDependenciesWhenPacking` su, in modo da consentire l'omissione di `true` tutte le dipendenze dal file nupkg generato.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-259">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### `PackageIconUrl`

<span data-ttu-id="1ee0a-260">`PackageIconUrl` è deprecato a favore della [`PackageIcon`](#packageicon) Proprietà.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-260">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="1ee0a-261">A partire da NuGet 5,3 e Visual Studio 2019 versione 16,3, `pack` genera l'avviso [NU5048](./errors-and-warnings/nu5048.md) se i metadati del pacchetto specificano solo `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-261">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### `PackageIcon`

> [!Tip]
> <span data-ttu-id="1ee0a-262">Per mantenere la compatibilità con le versioni precedenti di client e origini che non supportano ancora `PackageIcon` , specificare sia `PackageIcon` che `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-262">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="1ee0a-263">Visual Studio supporta `PackageIcon` i pacchetti provenienti da un'origine basata su cartelle.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-263">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="1ee0a-264">Compressione di un file di immagine icona</span><span class="sxs-lookup"><span data-stu-id="1ee0a-264">Packing an icon image file</span></span>

<span data-ttu-id="1ee0a-265">Quando si imballa un file di immagine icona, utilizzare `PackageIcon` la proprietà per specificare il percorso del file icona rispetto alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-265">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="1ee0a-266">Assicurarsi inoltre che il file sia incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-266">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="1ee0a-267">Le dimensioni del file di immagine sono limitate a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-267">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="1ee0a-268">I formati di file supportati sono JPEG e PNG.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-268">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="1ee0a-269">Si consiglia la risoluzione di un'immagine di 128x128.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-269">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="1ee0a-270">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-270">For example:</span></span>

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

<span data-ttu-id="1ee0a-271">[Esempio di icona del pacchetto](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-271">[Package Icon sample](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span></span>

<span data-ttu-id="1ee0a-272">Per l' nuspec equivalente, vedere il [ nuspec riferimento per l'icona](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-272">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="1ee0a-273">Assembly di output</span><span class="sxs-lookup"><span data-stu-id="1ee0a-273">Output assemblies</span></span>

<span data-ttu-id="1ee0a-274">`nuget pack` copia i file di output con le estensioni `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-274">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="1ee0a-275">I file di output che vengono copiati dipendono da ciò che MSBuild fornisce dalla `BuiltOutputProjectGroup` destinazione.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-275">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="1ee0a-276">Esistono due MSBuild  proprietà che è possibile usare nel file di progetto o nella riga di comando per controllare la posizione degli assembly di output:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-276">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="1ee0a-277">`IncludeBuildOutput`: valore booleano che determina se gli assembly di output della compilazione devono essere inclusi nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-277">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="1ee0a-278">`BuildOutputTargetFolder`: specifica la cartella in cui devono essere posizionati gli assembly di output.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-278">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="1ee0a-279">Gli assembly di output (e altri file di output) vengono copiati nelle rispettive cartelle per framework.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-279">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="1ee0a-280">Riferimenti ai pacchetti</span><span class="sxs-lookup"><span data-stu-id="1ee0a-280">Package references</span></span>

<span data-ttu-id="1ee0a-281">Vedere [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-281">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="1ee0a-282">Riferimenti da progetto a progetto</span><span class="sxs-lookup"><span data-stu-id="1ee0a-282">Project to project references</span></span>

<span data-ttu-id="1ee0a-283">I riferimenti da progetto a progetto sono considerati per impostazione predefinita come NuGet riferimenti ai pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-283">Project to project references are considered by default as NuGet package references.</span></span> <span data-ttu-id="1ee0a-284">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-284">For example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="1ee0a-285">È anche possibile aggiungere i metadati seguenti ai riferimenti del progetto:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-285">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="1ee0a-286">Inclusione di contenuto in un pacchetto</span><span class="sxs-lookup"><span data-stu-id="1ee0a-286">Including content in a package</span></span>

<span data-ttu-id="1ee0a-287">Per includere il contenuto, aggiungere altri metadati all'elemento `<Content>` esistente.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-287">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="1ee0a-288">Per impostazione predefinita tutti gli elementi di tipo"Content" vengono inclusi nel pacchetto, a meno che non si esegua l'override con voci simili al codice seguente:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-288">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="1ee0a-289">Per impostazione predefinita, tutti gli elementi vengono aggiunti alla radice di `content` e della cartella `contentFiles\any\<target_framework>` all'interno di un pacchetto e viene mantenuta la struttura di cartelle relative, a meno che non si specifichi un percorso di pacchetto:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-289">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="1ee0a-290">Se si vuole copiare tutto il contenuto solo in una o più cartelle radice specifiche `content` , anziché ed `contentFiles` entrambi, è possibile usare la MSBuild proprietà `ContentTargetFolders` , che per impostazione predefinita è "Content; contentFiles", ma può essere impostata su qualsiasi altro nome di cartella.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-290">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="1ee0a-291">Si noti che se si specifica solo "contentFiles" in `ContentTargetFolders`, i file vengono posizionati in `contentFiles\any\<target_framework>` o `contentFiles\<language>\<target_framework>` in base a `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-291">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="1ee0a-292">`PackagePath` può essere un set di percorsi di destinazione delimitati da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-292">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="1ee0a-293">Se si specifica un percorso di pacchetto vuoto, il file viene aggiunto alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-293">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="1ee0a-294">Ad esempio, il codice seguente aggiunge `libuv.txt` a `content\myfiles`, `content\samples` e nella radice del pacchetto:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-294">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="1ee0a-295">È disponibile anche una MSBuild proprietà `$(IncludeContentInPack)` , il cui valore predefinito è `true` .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-295">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="1ee0a-296">Se questa proprietà viene impostata su `false` in qualsiasi progetto, il contenuto da tale progetto non viene incluso nel pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-296">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="1ee0a-297">Altri metadati specifici del pacchetto che è possibile impostare in uno degli elementi precedenti includono ```<PackageCopyToOutput>``` e ```<PackageFlatten>``` quali set ```CopyToOutput``` e ```Flatten``` valori nella ```contentFiles``` voce nell'output nuspec .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-297">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="1ee0a-298">Oltre agli elementi Content, i metadati `<Pack>` e `<PackagePath>` possono anche essere impostati nei file con l'azione di compilazione Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource o None.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-298">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="1ee0a-299">Per fare in modo che il comando pack aggiunga il nome del file al percorso del pacchetto quando si usano modelli con caratteri jolly (glob), il percorso del pacchetto deve terminare con il carattere separatore di cartella. In caso contrario, il percorso del pacchetto viene interpretato come percorso completo, incluso il nome del file.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-299">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="1ee0a-300">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="1ee0a-300">IncludeSymbols</span></span>

<span data-ttu-id="1ee0a-301">Quando si usa `MSBuild -t:pack -p:IncludeSymbols=true`, i file `.pdb` corrispondenti vengono copiati insieme agli altri file di output (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-301">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="1ee0a-302">Si noti che l'impostazione `IncludeSymbols=true` crea un pacchetto regolare *e* un pacchetto di simboli.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-302">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="1ee0a-303">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="1ee0a-303">IncludeSource</span></span>

<span data-ttu-id="1ee0a-304">Equivale a `IncludeSymbols`, ma insieme ai file `.pdb` vengono copiati anche i file di origine.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-304">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="1ee0a-305">Tutti i file di tipo `Compile` vengono copiati in `src\<ProjectName>\` conservando la struttura di cartelle del percorso relativo nel pacchetto risultante.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-305">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="1ee0a-306">Lo stesso accade anche per i file di origine di qualsiasi `ProjectReference` con `TreatAsPackageReference` impostato su `false`.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-306">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="1ee0a-307">Se un file di tipo Compile è all'esterno della cartella di progetto, viene semplicemente aggiunto a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-307">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="1ee0a-308">Compressione di un'espressione di licenza o di un file di licenza</span><span class="sxs-lookup"><span data-stu-id="1ee0a-308">Packing a license expression or a license file</span></span>

<span data-ttu-id="1ee0a-309">Quando si utilizza un'espressione di licenza, utilizzare la `PackageLicenseExpression` Proprietà.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-309">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="1ee0a-310">Per un esempio, vedere [esempio di espressione di licenza](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-310">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="1ee0a-311">Per ulteriori informazioni sulle espressioni di licenza e le licenze accettate da NuGet . org, vedere la pagina relativa ai [metadati](nuspec.md#license)delle licenze.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-311">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="1ee0a-312">Quando si imballa un file di licenza, utilizzare la `PackageLicenseFile` proprietà per specificare il percorso del pacchetto, relativo alla radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-312">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="1ee0a-313">Assicurarsi inoltre che il file sia incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-313">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="1ee0a-314">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-314">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="1ee0a-315">Per un esempio, vedere [esempio di file di licenza](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-315">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="1ee0a-316">`PackageLicenseExpression`È possibile specificare solo uno degli, `PackageLicenseFile` e `PackageLicenseUrl` alla volta.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-316">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="1ee0a-317">Compressione di un file senza estensione</span><span class="sxs-lookup"><span data-stu-id="1ee0a-317">Packing a file without an extension</span></span>

<span data-ttu-id="1ee0a-318">In alcuni scenari, ad esempio quando si imballa un file di licenza, potrebbe essere necessario includere un file senza estensione.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-318">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="1ee0a-319">Per motivi cronologici, NuGet  &  MSBuild trattare i percorsi senza un'estensione come directory.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-319">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="1ee0a-320">[File senza un esempio di estensione](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-320">[File without an extension sample](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span></span>

### <a name="istool"></a><span data-ttu-id="1ee0a-321">IsTool</span><span class="sxs-lookup"><span data-stu-id="1ee0a-321">IsTool</span></span>

<span data-ttu-id="1ee0a-322">Quando si usa `MSBuild -t:pack -p:IsTool=true`, tutti i file, come specificato nello scenario [Assembly di output](#output-assemblies), vengono copiati nella cartella `tools` invece che nella cartella `lib`.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-322">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="1ee0a-323">Si noti che questo comportamento è diverso da `DotNetCliTool`, che viene specificato impostando `PackageType` nel file `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-323">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec-file"></a><span data-ttu-id="1ee0a-324">Compressione usando un `.nuspec` file</span><span class="sxs-lookup"><span data-stu-id="1ee0a-324">Packing using a `.nuspec` file</span></span>

<span data-ttu-id="1ee0a-325">Sebbene sia consigliabile includere in alternativa [tutte le proprietà](../reference/msbuild-targets.md#pack-target) che in genere si trovano nel file del `.nuspec` progetto, è possibile scegliere di utilizzare un `.nuspec` file per comprimere il progetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-325">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="1ee0a-326">Per un progetto non di tipo SDK che utilizza `PackageReference` , è necessario importare in `NuGet.Build.Tasks.Pack.targets` modo che l'attività Pack possa essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-326">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="1ee0a-327">Prima di poter comprimere un file, è ancora necessario ripristinare il progetto nuspec .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-327">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="1ee0a-328">Un progetto di tipo SDK include le destinazioni di tipo pack per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-328">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="1ee0a-329">Il Framework di destinazione del file di progetto non è rilevante e non viene usato per la compressione di un oggetto nuspec .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-329">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="1ee0a-330">Le tre MSBuild proprietà seguenti sono rilevanti per la creazione di pacchetti utilizzando `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="1ee0a-330">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="1ee0a-331">`NuspecFile`: percorso relativo o assoluto per il file `.nuspec` usato per la creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-331">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="1ee0a-332">`NuspecProperties`: elenco con valori delimitati da punto e virgola di coppie chiave=valore.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-332">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="1ee0a-333">A causa del MSBuild funzionamento dell'analisi della riga di comando, è necessario specificare più proprietà nel modo seguente: `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-333">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="1ee0a-334">`NuspecBasePath`: percorso di base per il file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-334">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="1ee0a-335">Se si usa `dotnet.exe` per creare il pacchetto del progetto, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-335">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="1ee0a-336">Se si usa MSBuild per creare il pacchetto del progetto, usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-336">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="1ee0a-337">Si noti che la nuspec creazione di un pacchetto usando dotnet.exe o MSBuild comporta anche la compilazione del progetto per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-337">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="1ee0a-338">Questa operazione può essere evitata passando ```--no-build``` la proprietà a dotnet.exe, che è l'equivalente dell'impostazione ```<NoBuild>true</NoBuild> ``` nel file di progetto, insieme all'impostazione ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-338">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="1ee0a-339">Un esempio di file con estensione *csproj* per la compressione di un nuspec file è:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-339">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="1ee0a-340">Punti di estensione avanzati per la creazione di pacchetti personalizzati</span><span class="sxs-lookup"><span data-stu-id="1ee0a-340">Advanced extension points to create customized package</span></span>

<span data-ttu-id="1ee0a-341">La `pack` destinazione fornisce due punti di estensione che vengono eseguiti nella compilazione specifica del Framework di destinazione interno.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-341">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="1ee0a-342">I punti di estensione supportano l'inclusione di contenuto e assembly specifici del Framework di destinazione in un pacchetto:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-342">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="1ee0a-343">`TargetsForTfmSpecificBuildOutput` destinazione: utilizzare per i file all'interno della `lib` cartella o in una cartella specificata utilizzando `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-343">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="1ee0a-344">`TargetsForTfmSpecificContentInPackage` destinazione: usare per i file all'esterno di `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-344">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### `TargetsForTfmSpecificBuildOutput`

<span data-ttu-id="1ee0a-345">Scrivere una destinazione personalizzata e specificarla come valore della `$(TargetsForTfmSpecificBuildOutput)` Proprietà.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-345">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="1ee0a-346">Per tutti i file che devono essere inseriti in `BuildOutputTargetFolder` (per impostazione predefinita, lib), la destinazione deve scrivere i file in ItemGroup `BuildOutputInPackage` e impostare i due valori di metadati seguenti:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-346">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="1ee0a-347">`FinalOutputPath`: Percorso assoluto del file; Se non viene specificato, l'identità viene utilizzata per valutare il percorso di origine.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-347">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="1ee0a-348">`TargetPath`: (Facoltativo) impostare quando il file deve essere inserito in una sottocartella all'interno di `lib\<TargetFramework>` , ad esempio gli assembly satellite che passano sotto le rispettive cartelle delle impostazioni cultura.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-348">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="1ee0a-349">Il valore predefinito è il nome del file.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-349">Defaults to the name of the file.</span></span>

<span data-ttu-id="1ee0a-350">Esempio:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-350">Example:</span></span>

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

<span data-ttu-id="1ee0a-351">Scrivere una destinazione personalizzata e specificarla come valore della `$(TargetsForTfmSpecificContentInPackage)` Proprietà.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-351">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="1ee0a-352">Per tutti i file da includere nel pacchetto, la destinazione deve scrivere i file in ItemGroup `TfmSpecificPackageFile` e impostare i metadati facoltativi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-352">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="1ee0a-353">`PackagePath`: Percorso in cui il file deve essere restituito nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-353">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="1ee0a-354">NuGet genera un avviso se viene aggiunto più di un file allo stesso percorso del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-354">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="1ee0a-355">`BuildAction`: L'azione di compilazione da assegnare al file, necessaria solo se il percorso del pacchetto si trova nella `contentFiles` cartella.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-355">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="1ee0a-356">Il valore predefinito è "None".</span><span class="sxs-lookup"><span data-stu-id="1ee0a-356">Defaults to "None".</span></span>

<span data-ttu-id="1ee0a-357">Esempio:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-357">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="1ee0a-358">Destinazione restore</span><span class="sxs-lookup"><span data-stu-id="1ee0a-358">restore target</span></span>

<span data-ttu-id="1ee0a-359">`MSBuild -t:restore` (usato da `nuget restore` e `dotnet restore` con progetti .NET Core) consente di ripristinare i pacchetti a cui si fa riferimento nel file di progetto, come segue:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-359">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="1ee0a-360">Lettura di tutti i riferimenti da progetto a progetto</span><span class="sxs-lookup"><span data-stu-id="1ee0a-360">Read all project to project references</span></span>
1. <span data-ttu-id="1ee0a-361">Lettura delle proprietà del progetto per trovare la cartella intermedia e i framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="1ee0a-361">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="1ee0a-362">Passare MSBuild i dati a NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="1ee0a-362">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="1ee0a-363">Esecuzione di restore</span><span class="sxs-lookup"><span data-stu-id="1ee0a-363">Run restore</span></span>
1. <span data-ttu-id="1ee0a-364">Download dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="1ee0a-364">Download packages</span></span>
1. <span data-ttu-id="1ee0a-365">Scrittura dei file di asset, delle destinazioni e delle proprietà</span><span class="sxs-lookup"><span data-stu-id="1ee0a-365">Write assets file, targets, and props</span></span>

<span data-ttu-id="1ee0a-366">La `restore` destinazione funziona per i progetti che usano il formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-366">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="1ee0a-367">`MSBuild 16.5+` dispone anche del supporto per il [consenso esplicito](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) per il `packages.config` formato.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-367">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="1ee0a-368">La `restore` destinazione [non deve essere eseguita](#restoring-and-building-with-one-msbuild-command) in combinazione con la `build` destinazione.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-368">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="1ee0a-369">Ripristino delle proprietà</span><span class="sxs-lookup"><span data-stu-id="1ee0a-369">Restore properties</span></span>

<span data-ttu-id="1ee0a-370">Le MSBuild proprietà del file di progetto possono derivare da altre impostazioni di ripristino.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-370">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="1ee0a-371">I valori possono essere impostati anche dalla riga di comando tramite l'opzione `-p:` (vedere gli esempi riportati di seguito).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-371">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="1ee0a-372">Proprietà</span><span class="sxs-lookup"><span data-stu-id="1ee0a-372">Property</span></span> | <span data-ttu-id="1ee0a-373">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1ee0a-373">Description</span></span> |
|--------|--------|
| `RestoreSources` | <span data-ttu-id="1ee0a-374">Elenco delimitato da punto e virgola delle origini di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-374">Semicolon-delimited list of package sources.</span></span> |
| `RestorePackagesPath` | <span data-ttu-id="1ee0a-375">Percorso della cartella dei pacchetti dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-375">User packages folder path.</span></span> |
| `RestoreDisableParallel` | <span data-ttu-id="1ee0a-376">Consente di limitare i download a uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-376">Limit downloads to one at a time.</span></span> |
| `RestoreConfigFile` | <span data-ttu-id="1ee0a-377">Percorso per un file `Nuget.Config` da applicare.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-377">Path to a `Nuget.Config` file to apply.</span></span> |
| `RestoreNoCache` | <span data-ttu-id="1ee0a-378">Se true, evita l'utilizzo di pacchetti memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-378">If true, avoids using cached packages.</span></span> <span data-ttu-id="1ee0a-379">Vedere [gestione dei pacchetti globali e delle cartelle della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-379">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| `RestoreIgnoreFailedSources` | <span data-ttu-id="1ee0a-380">Se true, ignora le origini di pacchetti in errore o mancanti.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-380">If true, ignores failing or missing package sources.</span></span> |
| `RestoreFallbackFolders` | <span data-ttu-id="1ee0a-381">Cartelle di fallback, utilizzate nello stesso modo in cui viene utilizzata la cartella Pacchetti utente.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-381">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| `RestoreAdditionalProjectSources` | <span data-ttu-id="1ee0a-382">Origini aggiuntive da utilizzare durante il ripristino.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-382">Additional sources to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFolders` | <span data-ttu-id="1ee0a-383">Cartelle di fallback aggiuntive da usare durante il ripristino.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-383">Additional fallback folders to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | <span data-ttu-id="1ee0a-384">Esclude le cartelle di fallback specificate in `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="1ee0a-384">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| `RestoreTaskAssemblyFile` | <span data-ttu-id="1ee0a-385">Percorso di `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-385">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| `RestoreGraphProjectInput` | <span data-ttu-id="1ee0a-386">Elenco delimitato da punto e virgola dei progetti da ripristinare, che deve contenere percorsi assoluti.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-386">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| `RestoreUseSkipNonexistentTargets`  | <span data-ttu-id="1ee0a-387">Quando i progetti vengono raccolti tramite MSBuild , determina se vengono raccolti usando l' `SkipNonexistentTargets` ottimizzazione.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-387">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="1ee0a-388">Quando non è impostato, il valore predefinito è `true` .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-388">When not set, defaults to `true`.</span></span> <span data-ttu-id="1ee0a-389">La conseguenza è un comportamento non rapido quando le destinazioni di un progetto non possono essere importate.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-389">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| `MSBuildProjectExtensionsPath` | <span data-ttu-id="1ee0a-390">Cartella di output, per impostazione predefinita `BaseIntermediateOutputPath` e la `obj` cartella.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-390">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| `RestoreForce` | <span data-ttu-id="1ee0a-391">Nei progetti basati su PackageReference, impone la risoluzione di tutte le dipendenze anche se l'ultimo ripristino ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-391">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="1ee0a-392">La specifica di questo flag è simile all'eliminazione del `project.assets.json` file.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-392">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="1ee0a-393">Questa operazione non consente di ignorare la cache HTTP.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-393">This does not bypass the http-cache.</span></span> |
| `RestorePackagesWithLockFile` | <span data-ttu-id="1ee0a-394">Optare per l'utilizzo di un file di blocco.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-394">Opts into the usage of a lock file.</span></span> |
| `RestoreLockedMode` | <span data-ttu-id="1ee0a-395">Eseguire Restore in modalità bloccata.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-395">Run restore in locked mode.</span></span> <span data-ttu-id="1ee0a-396">Questo significa che il ripristino non valuterà nuovamente le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-396">This means that restore will not reevaluate the dependencies.</span></span> |
| `NuGetLockFilePath` | <span data-ttu-id="1ee0a-397">Percorso personalizzato per il file di blocco.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-397">A custom location for the lock file.</span></span> <span data-ttu-id="1ee0a-398">Il percorso predefinito è accanto al progetto ed è denominato `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-398">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| `RestoreForceEvaluate` | <span data-ttu-id="1ee0a-399">Forza il ripristino per ricalcolare le dipendenze e aggiornare il file di blocco senza alcun avviso.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-399">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| `RestorePackagesConfig` | <span data-ttu-id="1ee0a-400">Opzione di consenso esplicito che ripristina i progetti con packages.config. Supporto `MSBuild -t:restore` solo con.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-400">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| `RestoreUseStaticGraphEvaluation` | <span data-ttu-id="1ee0a-401">Opzione di consenso esplicito per MSBuild l'uso della valutazione statica dei grafi anziché della valutazione standard.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-401">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="1ee0a-402">La valutazione statica dei grafi è una funzionalità sperimentale molto più rapida per i repository e le soluzioni di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-402">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="1ee0a-403">Esempio</span><span class="sxs-lookup"><span data-stu-id="1ee0a-403">Examples</span></span>

<span data-ttu-id="1ee0a-404">Riga di comando:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-404">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="1ee0a-405">File di progetto:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-405">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="1ee0a-406">Output del ripristino</span><span class="sxs-lookup"><span data-stu-id="1ee0a-406">Restore outputs</span></span>

<span data-ttu-id="1ee0a-407">Il ripristino crea i file seguenti nella cartella `obj` di compilazione:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-407">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="1ee0a-408">File</span><span class="sxs-lookup"><span data-stu-id="1ee0a-408">File</span></span> | <span data-ttu-id="1ee0a-409">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1ee0a-409">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="1ee0a-410">Contiene il grafico delle dipendenze di tutti i riferimenti ai pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-410">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="1ee0a-411">Riferimenti a MSBuild Props contenuti nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="1ee0a-411">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="1ee0a-412">Riferimenti alle MSBuild destinazioni contenute nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="1ee0a-412">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="1ee0a-413">Ripristino e compilazione con un solo MSBuild comando</span><span class="sxs-lookup"><span data-stu-id="1ee0a-413">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="1ee0a-414">A causa del fatto che è in NuGet grado di ripristinare i pacchetti che arrestano MSBuild destinazioni e prop, le valutazioni di ripristino e compilazione vengono eseguite con proprietà globali diverse.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-414">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="1ee0a-415">Ciò significa che le operazioni seguenti avranno un comportamento imprevedibile e spesso errato.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-415">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="1ee0a-416">L'approccio consigliato è invece:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-416">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="1ee0a-417">La stessa logica si applica ad altre destinazioni simili a `build` .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-417">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a><span data-ttu-id="1ee0a-418">Ripristino di progetti PackageReference e packages.config con MSBuild</span><span class="sxs-lookup"><span data-stu-id="1ee0a-418">Restoring PackageReference and packages.config projects with MSBuild</span></span>

<span data-ttu-id="1ee0a-419">Con MSBuild 16.5 +, packages.config sono supportati anche per `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-419">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="1ee0a-420">`packages.config` il ripristino è disponibile solo con `MSBuild 16.5+` e non con `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="1ee0a-420">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="1ee0a-421">Ripristino con MSBuild valutazione statica dei grafi</span><span class="sxs-lookup"><span data-stu-id="1ee0a-421">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="1ee0a-422">Con MSBuild 16,6 +, NuGet ha aggiunto una funzionalità sperimentale per usare la valutazione statica dei grafi dalla riga di comando che migliora significativamente il tempo di ripristino per i repository di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-422">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="1ee0a-423">In alternativa, è possibile abilitarla impostando la proprietà in un oggetto directory. Build. props.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-423">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="1ee0a-424">A partire da Visual Studio 2019. x e NuGet 5. x, questa funzionalità è considerata sperimentale e acconsentito esplicitamente.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-424">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="1ee0a-425">Per informazioni dettagliate su quando questa funzionalità sarà abilitata per impostazione predefinita, seguire la pagina [ NuGet /Home # 9803](https://github.com/NuGet/Home/issues/9803) .</span><span class="sxs-lookup"><span data-stu-id="1ee0a-425">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="1ee0a-426">Il ripristino statico del grafo modifica la parte MSBuild del ripristino, la lettura e la valutazione del progetto, ma non l'algoritmo di ripristino.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-426">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="1ee0a-427">L'algoritmo di ripristino è lo stesso in tutti gli NuGet strumenti ( NuGet con estensione exe, MSBuild exe, dotnet.exe e Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-427">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="1ee0a-428">In pochissimi scenari, il ripristino statico del grafico può comportarsi in modo diverso rispetto al ripristino corrente e alcuni PackageReferences o ProjectReference dichiarati potrebbero essere mancanti.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-428">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="1ee0a-429">Per facilitare il controllo, in caso di verifica di una sola volta, quando si esegue la migrazione a un ripristino statico del grafo, provare a eseguire:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-429">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="1ee0a-430">NuGet*non* deve segnalare alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-430">NuGet should *not* report any changes.</span></span> <span data-ttu-id="1ee0a-431">Se viene visualizzata una discrepanza, inviare un problema in [ NuGet /Home](https://github.com/nuget/home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="1ee0a-431">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="1ee0a-432">Sostituzione di una libreria da un grafico di ripristino</span><span class="sxs-lookup"><span data-stu-id="1ee0a-432">Replacing one library from a restore graph</span></span>

<span data-ttu-id="1ee0a-433">Se un ripristino restituisce l'assembly errato, è possibile escludere la scelta predefinita di tali pacchetti e sostituirla con la propria scelta.</span><span class="sxs-lookup"><span data-stu-id="1ee0a-433">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="1ee0a-434">Prima di tutto, con un `PackageReference` di livello superiore, escludere tutti gli asset:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-434">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="1ee0a-435">Aggiungere quindi il riferimento personalizzato alla copia locale appropriata della DLL:</span><span class="sxs-lookup"><span data-stu-id="1ee0a-435">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
