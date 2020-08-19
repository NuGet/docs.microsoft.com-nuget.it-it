---
title: informazioni di riferimento sul file. nuspec per NuGet
description: Il file. nuspec contiene i metadati del pacchetto usati per la compilazione e per fornire informazioni ai consumer del pacchetto.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: f91d47bdf9b957b512d3d83434693ee93de07afb
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623136"
---
# <a name="nuspec-reference"></a><span data-ttu-id="fd1d8-103">Informazioni di riferimento sul file .nuspec</span><span class="sxs-lookup"><span data-stu-id="fd1d8-103">.nuspec reference</span></span>

<span data-ttu-id="fd1d8-104">Un file `.nuspec` è un manifesto XML che contiene i metadati del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="fd1d8-105">Questo manifesto viene usato per compilare il pacchetto e per fornire informazioni ai consumer.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="fd1d8-106">Il manifesto viene sempre incluso in un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="fd1d8-107">In questo argomento</span><span class="sxs-lookup"><span data-stu-id="fd1d8-107">In this topic:</span></span>

- [<span data-ttu-id="fd1d8-108">Formato generale e schema</span><span class="sxs-lookup"><span data-stu-id="fd1d8-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="fd1d8-109">[Token di sostituzione](#replacement-tokens) (usati con un progetto di Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="fd1d8-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="fd1d8-110">Dipendenze</span><span class="sxs-lookup"><span data-stu-id="fd1d8-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="fd1d8-111">Riferimenti espliciti agli assembly</span><span class="sxs-lookup"><span data-stu-id="fd1d8-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="fd1d8-112">Riferimenti agli assembly del framework</span><span class="sxs-lookup"><span data-stu-id="fd1d8-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="fd1d8-113">Inclusione di file di assembly</span><span class="sxs-lookup"><span data-stu-id="fd1d8-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="fd1d8-114">Inclusione di file di contenuto</span><span class="sxs-lookup"><span data-stu-id="fd1d8-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="fd1d8-115">File nuspec di esempio</span><span class="sxs-lookup"><span data-stu-id="fd1d8-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="fd1d8-116">Compatibilità del tipo di progetto</span><span class="sxs-lookup"><span data-stu-id="fd1d8-116">Project type compatibility</span></span>

- <span data-ttu-id="fd1d8-117">Usare `.nuspec` con `nuget.exe pack` per i progetti non in stile SDK che usano `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="fd1d8-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="fd1d8-118">`.nuspec`Non è necessario un file per creare pacchetti per i [progetti di tipo SDK](../resources/check-project-format.md) (in genere .net core e .NET standard progetti che usano l' [attributo SDK](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="fd1d8-119">Si noti che `.nuspec` quando si crea il pacchetto viene generato un oggetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="fd1d8-120">Se si sta creando un pacchetto usando `dotnet.exe pack` o `msbuild pack target` , si consiglia di [includere tutte le proprietà](../reference/msbuild-targets.md#pack-target) che in genere si trovano nel file del `.nuspec` progetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="fd1d8-121">Tuttavia, è invece possibile scegliere di [usare un `.nuspec` file per eseguire il Pack usando `dotnet.exe` o `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="fd1d8-122">Per i progetti migrati da `packages.config` a [PackageReference](../consume-packages/package-references-in-project-files.md), `.nuspec` non è necessario un file per creare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="fd1d8-123">Usare invece [msbuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="fd1d8-124">Formato generale e schema</span><span class="sxs-lookup"><span data-stu-id="fd1d8-124">General form and schema</span></span>

<span data-ttu-id="fd1d8-125">Il file dello schema di `nuspec.xsd` corrente è disponibile nel [repository GitHub di NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="fd1d8-126">All'interno di questo schema, un file `.nuspec` ha il formato generale seguente:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

<span data-ttu-id="fd1d8-127">Per una rappresentazione visiva chiara dello schema, aprire il file di schema in Visual Studio in modalità progettazione e fare clic sul collegamento **XML Schema Explorer**.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="fd1d8-128">In alternativa, aprire il file come codice, fare clic con il pulsante destro del mouse nell'editor e scegliere **Mostra in XML Schema Explorer**.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="fd1d8-129">In entrambi i casi si ottiene una visualizzazione simile alla seguente (quando è per la maggior parte espansa):</span><span class="sxs-lookup"><span data-stu-id="fd1d8-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio Schema Explorer con nuspec.xsd aperto](media/SchemaExplorer.png)

<span data-ttu-id="fd1d8-131">Tutti i nomi degli elementi XML nel file con estensione NuSpec fanno distinzione tra maiuscole e minuscole, come nel caso di XML in generale.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-131">All XML element names in the .nuspec file are case-sensitive, as is the case for XML in general.</span></span> <span data-ttu-id="fd1d8-132">Ad esempio, l'utilizzo dell'elemento Metadata `<description>` è corretto e `<Description>` non è corretto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-132">For example, using the metadata element `<description>` is correct and `<Description>` is not correct.</span></span> <span data-ttu-id="fd1d8-133">La combinazione di maiuscole e minuscole appropriata per ogni nome di elemento è riportata di seguito</span><span class="sxs-lookup"><span data-stu-id="fd1d8-133">The proper casing for each element name is documented below.</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="fd1d8-134">Elementi dei metadati obbligatori</span><span class="sxs-lookup"><span data-stu-id="fd1d8-134">Required metadata elements</span></span>

<span data-ttu-id="fd1d8-135">Anche se gli elementi seguenti sono i requisiti minimi per un pacchetto, è consigliabile aggiungere gli [elementi dei metadati facoltativi](#optional-metadata-elements) per migliorare l'esperienza complessiva degli sviluppatori con il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-135">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="fd1d8-136">Questi elementi devono essere visualizzati all'interno di un elemento `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-136">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="fd1d8-137">id</span><span class="sxs-lookup"><span data-stu-id="fd1d8-137">id</span></span> 
<span data-ttu-id="fd1d8-138">Identificatore del pacchetto senza distinzione tra maiuscole e minuscole che deve essere univoco in nuget.org o in qualsiasi raccolta in cui risiede il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-138">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="fd1d8-139">L'ID non può contenere spazi o caratteri non validi per un URL e in genere segue le regole dello spazio dei nomi .NET.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-139">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="fd1d8-140">Vedere [Choosing a unique package identifier and setting the version number](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) (Scelta di un identificatore univoco del pacchetto e impostazione del numero di versione) per altre indicazioni.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-140">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>

<span data-ttu-id="fd1d8-141">Quando si carica un pacchetto in nuget.org, il `id` campo è limitato a 128 caratteri.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-141">When uploading a package to nuget.org, the `id` field is limited to 128 characters.</span></span>

#### <a name="version"></a><span data-ttu-id="fd1d8-142">version</span><span class="sxs-lookup"><span data-stu-id="fd1d8-142">version</span></span>
<span data-ttu-id="fd1d8-143">La versione del pacchetto secondo il criterio *principale.secondaria.patch*.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-143">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="fd1d8-144">I numeri di versione possono includere un suffisso di versione non definitiva, come descritto in [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-144">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 

<span data-ttu-id="fd1d8-145">Quando si carica un pacchetto in nuget.org, il `version` campo è limitato a 64 caratteri.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-145">When uploading a package to nuget.org, the `version` field is limited to 64 characters.</span></span>

#### <a name="description"></a><span data-ttu-id="fd1d8-146">description</span><span class="sxs-lookup"><span data-stu-id="fd1d8-146">description</span></span>
<span data-ttu-id="fd1d8-147">Descrizione del pacchetto per la visualizzazione dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-147">A description of the package for UI display.</span></span>

<span data-ttu-id="fd1d8-148">Quando si carica un pacchetto in nuget.org, il `description` campo è limitato a 4000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-148">When uploading a package to nuget.org, the `description` field is limited to 4000 characters.</span></span>

#### <a name="authors"></a><span data-ttu-id="fd1d8-149">authors</span><span class="sxs-lookup"><span data-stu-id="fd1d8-149">authors</span></span>
<span data-ttu-id="fd1d8-150">Elenco delimitato da virgole di autori di pacchetti, corrispondenti ai nomi di profilo in nuget.org. Questi vengono visualizzati nella raccolta NuGet in nuget.org e vengono usati per fare riferimento a pacchetti con gli stessi autori.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

<span data-ttu-id="fd1d8-151">Quando si carica un pacchetto in nuget.org, il `authors` campo è limitato a 4000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-151">When uploading a package to nuget.org, the `authors` field is limited to 4000 characters.</span></span>

### <a name="optional-metadata-elements"></a><span data-ttu-id="fd1d8-152">Elementi dei metadati facoltativi</span><span class="sxs-lookup"><span data-stu-id="fd1d8-152">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="fd1d8-153">owners</span><span class="sxs-lookup"><span data-stu-id="fd1d8-153">owners</span></span>
<span data-ttu-id="fd1d8-154">Elenco delimitato da virgole degli autori di pacchetti che utilizzano nomi di profilo in nuget.org. Si tratta spesso dello stesso elenco di `authors` e viene ignorato quando si carica il pacchetto in NuGet.org. Vedere [gestione dei proprietari dei pacchetti in NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-154">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="fd1d8-155">projectUrl</span><span class="sxs-lookup"><span data-stu-id="fd1d8-155">projectUrl</span></span>
<span data-ttu-id="fd1d8-156">URL della pagina iniziale del pacchetto, spesso visualizzato nell'interfaccia utente e in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-156">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

<span data-ttu-id="fd1d8-157">Quando si carica un pacchetto in nuget.org, il `projectUrl` campo è limitato a 4000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-157">When uploading a package to nuget.org, the `projectUrl` field is limited to 4000 characters.</span></span>

#### <a name="licenseurl"></a><span data-ttu-id="fd1d8-158">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="fd1d8-158">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="fd1d8-159">licenseUrl è deprecato.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-159">licenseUrl is deprecated.</span></span> <span data-ttu-id="fd1d8-160">Usare invece la licenza.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-160">Use license instead.</span></span>

<span data-ttu-id="fd1d8-161">URL per la licenza del pacchetto, spesso visualizzato in interfacce utente come nuget.org.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-161">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

<span data-ttu-id="fd1d8-162">Quando si carica un pacchetto in nuget.org, il `licenseUrl` campo è limitato a 4000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-162">When uploading a package to nuget.org, the `licenseUrl` field is limited to 4000 characters.</span></span>

#### <a name="license"></a><span data-ttu-id="fd1d8-163">license</span><span class="sxs-lookup"><span data-stu-id="fd1d8-163">license</span></span>

<span data-ttu-id="fd1d8-164">*Supportato con **NuGet 4.9.0** e versioni successive*</span><span class="sxs-lookup"><span data-stu-id="fd1d8-164">*Supported with **NuGet 4.9.0** and above*</span></span>

<span data-ttu-id="fd1d8-165">Espressione di licenza SPDX o percorso di un file di licenza all'interno del pacchetto, spesso visualizzato in interfacce utente come nuget.org. Se si sta eseguendo la licenza del pacchetto con una licenza comune, ad esempio MIT o BSD-2-clause, usare l' [identificatore di licenza SPDX](https://spdx.org/licenses/)associato.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-165">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="fd1d8-166">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-166">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="fd1d8-167">NuGet.org accetta solo le espressioni di licenza approvate dall'iniziativa Open Source o dalla versione gratuita di Software Foundation.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-167">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="fd1d8-168">Se il pacchetto è concesso in licenza in base a più licenze comuni, è possibile specificare una licenza composita usando la [sintassi dell'espressione SPDX versione 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-168">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="fd1d8-169">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-169">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="fd1d8-170">Se si usa una licenza personalizzata che non è supportata dalle espressioni di licenza, è possibile creare un pacchetto di un `.txt` `.md` file o con il testo della licenza.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-170">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="fd1d8-171">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-171">For example:</span></span>

```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

<span data-ttu-id="fd1d8-172">Per l'equivalente MSBuild, vedere la pagina relativa all' [imballaggio di un'espressione di licenza o di un file di licenza](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-172">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="fd1d8-173">La sintassi esatta delle espressioni di licenza di NuGet è descritta di seguito in [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-173">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a><span data-ttu-id="fd1d8-174">iconUrl</span><span class="sxs-lookup"><span data-stu-id="fd1d8-174">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="fd1d8-175">iconUrl è deprecato.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-175">iconUrl is deprecated.</span></span> <span data-ttu-id="fd1d8-176">Usare invece l'icona.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-176">Use icon instead.</span></span>

<span data-ttu-id="fd1d8-177">URL per un'immagine 128x128 con sfondo trasparente da usare come icona per il pacchetto nella visualizzazione dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-177">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="fd1d8-178">Assicurarsi che questo elemento contenga l'*URL diretto dell'immagine* e non l'URL di una pagina Web contenente l'immagine.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-178">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="fd1d8-179">Ad esempio, per usare un'immagine da GitHub, usare l'URL del file non elaborato come <em> https://github.com/ \<username\> / \<repository\> /RAW/ \<branch\> / \<logo.png\> </em>.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-179">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 
   
<span data-ttu-id="fd1d8-180">Quando si carica un pacchetto in nuget.org, il `iconUrl` campo è limitato a 4000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-180">When uploading a package to nuget.org, the `iconUrl` field is limited to 4000 characters.</span></span>

#### <a name="icon"></a><span data-ttu-id="fd1d8-181">icon</span><span class="sxs-lookup"><span data-stu-id="fd1d8-181">icon</span></span>

<span data-ttu-id="fd1d8-182">*Supportato con **NuGet 5.3.0** e versioni successive*</span><span class="sxs-lookup"><span data-stu-id="fd1d8-182">*Supported with **NuGet 5.3.0** and above*</span></span>

<span data-ttu-id="fd1d8-183">Si tratta di un percorso di un file di immagine all'interno del pacchetto, spesso visualizzato in interfacce utente come nuget.org come icona del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-183">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="fd1d8-184">Le dimensioni del file di immagine sono limitate a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-184">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="fd1d8-185">I formati di file supportati sono JPEG e PNG.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-185">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="fd1d8-186">Si consiglia la risoluzione di un'immagine di 128x128.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-186">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="fd1d8-187">Ad esempio, quando si crea un pacchetto utilizzando nuget.exe è necessario aggiungere il codice seguente al NuSpec:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-187">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

```xml
<package>
  <metadata>
    ...
    <icon>images\icon.png</icon>
    ...
  </metadata>
  <files>
    ...
    <file src="..\icon.png" target="images\" />
    ...
  </files>
</package>
```

[<span data-ttu-id="fd1d8-188">Esempio di icona del pacchetto NuSpec.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-188">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/master/PackageIconNuspecExample)

<span data-ttu-id="fd1d8-189">Per l'equivalente MSBuild, vedere la pagina [relativa all'imballaggio di un file di immagine icona](msbuild-targets.md#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-189">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="fd1d8-190">È possibile specificare sia `icon` che `iconUrl` per mantenere la compatibilità con le origini che non supportano `icon` .</span><span class="sxs-lookup"><span data-stu-id="fd1d8-190">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="fd1d8-191">Visual Studio supporterà `icon` i pacchetti provenienti da un'origine basata su cartelle in una versione futura.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-191">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="fd1d8-192">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="fd1d8-192">requireLicenseAcceptance</span></span>
<span data-ttu-id="fd1d8-193">Valore booleano che specifica se il client deve richiedere al consumer di accettare la licenza del pacchetto prima di installarlo.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-193">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="fd1d8-194">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="fd1d8-194">developmentDependency</span></span>
<span data-ttu-id="fd1d8-195">\*(2.8 +) \* Valore booleano che specifica se il pacchetto deve essere contrassegnato come dipendenza solo per lo sviluppo, in modo che il pacchetto non possa essere incluso come dipendenza in altri pacchetti.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-195">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="fd1d8-196">Con PackageReference (NuGet 4.8 +), questo flag indica anche che gli asset in fase di compilazione verranno esclusi dalla compilazione.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-196">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="fd1d8-197">Vedere [supporto di DevelopmentDependency per PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="fd1d8-197">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="fd1d8-198">riepilogo</span><span class="sxs-lookup"><span data-stu-id="fd1d8-198">summary</span></span>
> [!Important]
> <span data-ttu-id="fd1d8-199">`summary` verrà deprecato.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-199">`summary` is being deprecated.</span></span> <span data-ttu-id="fd1d8-200">Usare invece `description`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-200">Use `description` instead.</span></span>

<span data-ttu-id="fd1d8-201">Descrizione breve del pacchetto per la visualizzazione dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-201">A short description of the package for UI display.</span></span> <span data-ttu-id="fd1d8-202">Se omesso, viene usata una versione troncata di `description`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-202">If omitted, a truncated version of `description` is used.</span></span>

<span data-ttu-id="fd1d8-203">Quando si carica un pacchetto in nuget.org, il `summary` campo è limitato a 4000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-203">When uploading a package to nuget.org, the `summary` field is limited to 4000 characters.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="fd1d8-204">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="fd1d8-204">releaseNotes</span></span>
<span data-ttu-id="fd1d8-205">*(1.5+)* Descrizione delle modifiche apportate in questa versione del pacchetto, spesso usata nell'interfaccia utente, come la scheda **Aggiornamenti** di Gestione pacchetti di Visual Studio, in sostituzione della descrizione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-205">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

<span data-ttu-id="fd1d8-206">Quando si carica un pacchetto in nuget.org, il `releaseNotes` campo è limitato a 35.000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-206">When uploading a package to nuget.org, the `releaseNotes` field is limited to 35,000 characters.</span></span>

#### <a name="copyright"></a><span data-ttu-id="fd1d8-207">copyright</span><span class="sxs-lookup"><span data-stu-id="fd1d8-207">copyright</span></span>
<span data-ttu-id="fd1d8-208">*(1.5+)* Informazioni sul copyright per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-208">*(1.5+)* Copyright details for the package.</span></span>

<span data-ttu-id="fd1d8-209">Quando si carica un pacchetto in nuget.org, il `copyright` campo è limitato a 4000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-209">When uploading a package to nuget.org, the `copyright` field is limited to 4000 characters.</span></span>

#### <a name="language"></a><span data-ttu-id="fd1d8-210">Linguaggio</span><span class="sxs-lookup"><span data-stu-id="fd1d8-210">language</span></span>
<span data-ttu-id="fd1d8-211">ID delle impostazioni locali per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-211">The locale ID for the package.</span></span> <span data-ttu-id="fd1d8-212">Vedere [Creazione di pacchetti localizzati](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-212">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="fd1d8-213">tags</span><span class="sxs-lookup"><span data-stu-id="fd1d8-213">tags</span></span>
<span data-ttu-id="fd1d8-214">Elenco di tag e parole chiave delimitati da spazi che descrivono il pacchetto e facilitano l'individuabilità dei pacchetti tramite meccanismi di ricerca e filtro.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-214">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

<span data-ttu-id="fd1d8-215">Quando si carica un pacchetto in nuget.org, il `tags` campo è limitato a 4000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-215">When uploading a package to nuget.org, the `tags` field is limited to 4000 characters.</span></span>

#### <a name="serviceable"></a><span data-ttu-id="fd1d8-216">serviceable</span><span class="sxs-lookup"><span data-stu-id="fd1d8-216">serviceable</span></span> 
<span data-ttu-id="fd1d8-217">*(3.3+)* Solo per uso interno in NuGet.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-217">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="fd1d8-218">repository</span><span class="sxs-lookup"><span data-stu-id="fd1d8-218">repository</span></span>
<span data-ttu-id="fd1d8-219">Metadati del repository, composti da quattro attributi facoltativi: `type` and `url` *(4.0 +)*, and `branch` e `commit` *(4.6 +)*.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-219">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="fd1d8-220">Questi attributi consentono di eseguire il mapping `.nupkg` di al repository che lo ha compilato, con la possibilità di ottenere informazioni dettagliate come il nome del singolo ramo e/o l'hash SHA-1 di commit che ha compilato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-220">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="fd1d8-221">Deve trattarsi di un URL disponibile pubblicamente che può essere richiamato direttamente da un software di controllo della versione.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-221">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="fd1d8-222">Non deve trattarsi di una pagina HTML, perché è destinata al computer.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-222">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="fd1d8-223">Per il collegamento alla pagina del progetto, usare `projectUrl` invece il campo.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-223">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="fd1d8-224">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-224">For example:</span></span>
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

<span data-ttu-id="fd1d8-225">Quando si carica un pacchetto in nuget.org, l' `type` attributo è limitato a 100 caratteri e l' `url` attributo è limitato a 4000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-225">When uploading a package to nuget.org, the `type` attribute is limited to 100 characters and the `url` attribute is limited to 4000 characters.</span></span>

#### <a name="title"></a><span data-ttu-id="fd1d8-226">title</span><span class="sxs-lookup"><span data-stu-id="fd1d8-226">title</span></span>
<span data-ttu-id="fd1d8-227">Titolo descrittivo del pacchetto che può essere usato in alcune visualizzazioni dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-227">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="fd1d8-228">(nuget.org e gestione pacchetti in Visual Studio non mostrano titolo)</span><span class="sxs-lookup"><span data-stu-id="fd1d8-228">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

<span data-ttu-id="fd1d8-229">Quando si carica un pacchetto in nuget.org, il `title` campo è limitato a 256 caratteri, ma non viene usato per scopi di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-229">When uploading a package to nuget.org, the `title` field is limited to 256 characters but is not used for any display purposes.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="fd1d8-230">Elementi di raccolta</span><span class="sxs-lookup"><span data-stu-id="fd1d8-230">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="fd1d8-231">packageTypes</span><span class="sxs-lookup"><span data-stu-id="fd1d8-231">packageTypes</span></span>
<span data-ttu-id="fd1d8-232">*(3.5 +)* Raccolta di zero o più elementi `<packageType>` che specificano il tipo del pacchetto se diverso da un pacchetto di dipendenza tradizionale.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-232">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="fd1d8-233">Ogni packageType include gli attributi di *name* e *version*.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-233">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="fd1d8-234">Vedere [Setting a package type](../create-packages/set-package-type.md) (Impostazione di un tipo di pacchetto).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-234">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="fd1d8-235">dipendenze</span><span class="sxs-lookup"><span data-stu-id="fd1d8-235">dependencies</span></span>
<span data-ttu-id="fd1d8-236">Raccolta di zero o più elementi `<dependency>` che specificano le dipendenze per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-236">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="fd1d8-237">Ogni dipendenza include gli attributi *id*, *version*, *include* (3.x+) ed *exclude* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-237">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="fd1d8-238">Vedere [Dipendenze](#dependencies-element) di seguito.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-238">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="fd1d8-239">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="fd1d8-239">frameworkAssemblies</span></span>
<span data-ttu-id="fd1d8-240">*(1.2 +)* Raccolta di zero o più elementi `<frameworkAssembly>` che identificano i riferimenti ad assembly .NET Framework richiesti dal pacchetto. Ciò assicura che i riferimenti vengano aggiunti ai progetti che utilizzano il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-240">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="fd1d8-241">Ogni frameworkAssembly include gli attributi *assemblyName* e *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-241">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="fd1d8-242">Vedere [Riferimenti agli assembly del framework](#specifying-framework-assembly-references-gac) più avanti.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-242">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>
#### <a name="references"></a><span data-ttu-id="fd1d8-243">references</span><span class="sxs-lookup"><span data-stu-id="fd1d8-243">references</span></span>
<span data-ttu-id="fd1d8-244">*(1.5 +)* Raccolta di zero o più elementi `<reference>` per la denominazione degli assembly nella cartella `lib` del pacchetto, aggiunti come riferimenti al progetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-244">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="fd1d8-245">Ogni riferimento include un attributo *file*.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-245">Each reference has a *file* attribute.</span></span> <span data-ttu-id="fd1d8-246">`<references>` può anche contenere un elemento `<group>` con un attributo *targetFramework*, che contiene a sua volta elementi `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-246">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="fd1d8-247">Se omesso, vengono inclusi tutti i riferimenti in `lib`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-247">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="fd1d8-248">Vedere [Riferimenti espliciti agli assembly](#specifying-explicit-assembly-references) più avanti.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-248">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="fd1d8-249">contentFiles</span><span class="sxs-lookup"><span data-stu-id="fd1d8-249">contentFiles</span></span>
<span data-ttu-id="fd1d8-250">*(3.3 +)* Raccolta di elementi `<files>` che identificano i file di contenuto da includere nel progetto che utilizza il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-250">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="fd1d8-251">Questi file sono specificati con un set di attributi che descrivono come devono essere usati all'interno del sistema del progetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-251">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="fd1d8-252">Vedere [Inclusione di file di assembly](#specifying-files-to-include-in-the-package) più avanti.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-252">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="fd1d8-253">files</span><span class="sxs-lookup"><span data-stu-id="fd1d8-253">files</span></span> 
<span data-ttu-id="fd1d8-254">Il `<package>` nodo può contenere un `<files>` nodo di pari livello `<metadata>` e un `<contentFiles>` elemento figlio in `<metadata>` per specificare l'assembly e i file di contenuto da includere nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-254">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="fd1d8-255">Vedere [Inclusione di file di assembly](#including-assembly-files) e [Inclusione di file di contenuto](#including-content-files) più avanti in questo argomento per ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-255">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="fd1d8-256">attributi di metadati</span><span class="sxs-lookup"><span data-stu-id="fd1d8-256">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="fd1d8-257">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="fd1d8-257">minClientVersion</span></span>
<span data-ttu-id="fd1d8-258">Specifica la versione minima del client NuGet, imposta da nuget.exe e da Gestione pacchetti di Visual Studio, che può installare questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-258">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="fd1d8-259">Questo attributo viene usato ogni volta che il pacchetto dipende da funzionalità specifiche del file `.nuspec` aggiunte in una particolare versione del client NuGet.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-259">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="fd1d8-260">Ad esempio, un pacchetto che usa l'attributo `developmentDependency` deve specificare "2.8" per `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-260">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="fd1d8-261">Analogamente, un pacchetto che usa l'elemento `contentFiles` (vedere la sezione successiva) deve impostare `minClientVersion` su "3.3".</span><span class="sxs-lookup"><span data-stu-id="fd1d8-261">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="fd1d8-262">Si noti che poiché i client NuGet prima della versione 2.5 non riconoscono questo flag, essi rifiutano *sempre* di installare il pacchetto indipendentemente dal contenuto di `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-262">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata minClientVersion="100.0.0.1">
        <id>dasdas</id>
        <version>2.0.0</version>
        <title />
        <authors>dsadas</authors>
        <owners />
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>My package description.</description>
    </metadata>
    <files>
        <file src="content\one.txt" target="content\one.txt" />
    </files>
</package>
```

## <a name="replacement-tokens"></a><span data-ttu-id="fd1d8-263">Token di sostituzione</span><span class="sxs-lookup"><span data-stu-id="fd1d8-263">Replacement tokens</span></span>

<span data-ttu-id="fd1d8-264">Quando si crea un pacchetto, il [ `nuget pack` comando](../reference/cli-reference/cli-ref-pack.md) sostituisce i token delimitati da $ nel `.nuspec` nodo del file `<metadata>` con i valori derivati da un file di progetto o dall' `pack` opzione del comando `-properties` .</span><span class="sxs-lookup"><span data-stu-id="fd1d8-264">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="fd1d8-265">Nella riga di comando, i valori dei token vengono specificati con `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-265">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="fd1d8-266">Ad esempio, è possibile usare un token come `$owners$` e `$desc$` nel file `.nuspec` e specificare i valori al momento della creazione del pacchetto come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-266">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="fd1d8-267">Per usare valori da un progetto, specificare il token descritto nella tabella riportata di seguito (AssemblyInfo fa riferimento al file in `Properties`, ad esempio `AssemblyInfo.cs` o `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-267">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="fd1d8-268">Per usare questi token, eseguire `nuget pack` con il file di progetto anziché semplicemente il file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-268">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="fd1d8-269">Ad esempio, quando si usa il comando seguente, i token `$id$` e `$version$` in un file `.nuspec` vengono sostituiti con i valori `AssemblyName` e `AssemblyVersion` del progetto:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-269">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="fd1d8-270">In genere, quando si dispone di un progetto, si crea inizialmente il file `.nuspec` con `nuget spec MyProject.csproj`, che include automaticamente alcuni di questi token standard.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-270">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="fd1d8-271">Tuttavia, se un progetto non include i valori per elementi `.nuspec` obbligatori, `nuget pack` ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-271">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="fd1d8-272">Inoltre, se si modificano i valori del progetto, assicurarsi di ricompilare prima di creare il pacchetto. Questa operazione può essere eseguita facilmente con l'opzione `build` del comando pack.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-272">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="fd1d8-273">Ad eccezione di `$configuration$`, i valori nel progetto vengono usati preferenzialmente rispetto a qualsiasi altro valore assegnato allo stesso token nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-273">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="fd1d8-274">token</span><span class="sxs-lookup"><span data-stu-id="fd1d8-274">Token</span></span> | <span data-ttu-id="fd1d8-275">Origine del valore</span><span class="sxs-lookup"><span data-stu-id="fd1d8-275">Value source</span></span> | <span data-ttu-id="fd1d8-276">Valore</span><span class="sxs-lookup"><span data-stu-id="fd1d8-276">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="fd1d8-277">**$id $**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-277">**$id$**</span></span> | <span data-ttu-id="fd1d8-278">File di progetto</span><span class="sxs-lookup"><span data-stu-id="fd1d8-278">Project file</span></span> | <span data-ttu-id="fd1d8-279">AssemblyName (title) dal file di progetto</span><span class="sxs-lookup"><span data-stu-id="fd1d8-279">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="fd1d8-280">**$version $**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-280">**$version$**</span></span> | <span data-ttu-id="fd1d8-281">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="fd1d8-281">AssemblyInfo</span></span> | <span data-ttu-id="fd1d8-282">AssemblyInformationalVersion se presente, in caso contrario AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="fd1d8-282">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="fd1d8-283">**$author $**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-283">**$author$**</span></span> | <span data-ttu-id="fd1d8-284">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="fd1d8-284">AssemblyInfo</span></span> | <span data-ttu-id="fd1d8-285">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="fd1d8-285">AssemblyCompany</span></span> |
| <span data-ttu-id="fd1d8-286">**$title $**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-286">**$title$**</span></span> | <span data-ttu-id="fd1d8-287">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="fd1d8-287">AssemblyInfo</span></span> | <span data-ttu-id="fd1d8-288">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="fd1d8-288">AssemblyTitle</span></span> |
| <span data-ttu-id="fd1d8-289">**$description $**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-289">**$description$**</span></span> | <span data-ttu-id="fd1d8-290">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="fd1d8-290">AssemblyInfo</span></span> | <span data-ttu-id="fd1d8-291">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="fd1d8-291">AssemblyDescription</span></span> |
| <span data-ttu-id="fd1d8-292">**$copyright $**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-292">**$copyright$**</span></span> | <span data-ttu-id="fd1d8-293">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="fd1d8-293">AssemblyInfo</span></span> | <span data-ttu-id="fd1d8-294">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="fd1d8-294">AssemblyCopyright</span></span> |
| <span data-ttu-id="fd1d8-295">**$configuration $**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-295">**$configuration$**</span></span> | <span data-ttu-id="fd1d8-296">DLL dell'assembly</span><span class="sxs-lookup"><span data-stu-id="fd1d8-296">Assembly DLL</span></span> | <span data-ttu-id="fd1d8-297">Configurazione usata per compilare l'assembly, con impostazione predefinita Debug.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-297">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="fd1d8-298">Si noti che per creare un pacchetto con la configurazione Rilascio, è sempre necessario usare `-properties Configuration=Release` nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-298">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="fd1d8-299">I token possono essere usati anche per risolvere i percorsi quando si includono [file di assembly](#including-assembly-files) e [file di contenuto](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-299">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="fd1d8-300">I token hanno gli stessi nomi delle proprietà di MSBuild e ciò consente di selezionare i file da includere a seconda della configurazione di compilazione corrente.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-300">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="fd1d8-301">Ad esempio, se si usano i token seguenti nel file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-301">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="fd1d8-302">E si compila un assembly il cui `AssemblyName` è `LoggingLibrary` con la configurazione `Release` in MSBuild, le righe risultanti nel file `.nuspec` nel pacchetto sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-302">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="fd1d8-303">Elemento dipendenze</span><span class="sxs-lookup"><span data-stu-id="fd1d8-303">Dependencies element</span></span>

<span data-ttu-id="fd1d8-304">L'elemento `<dependencies>` all'interno di `<metadata>` contiene qualsiasi numero di elementi `<dependency>` che identificano altri pacchetti da cui dipende il pacchetto di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-304">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="fd1d8-305">Gli attributi per ogni `<dependency>` sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-305">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="fd1d8-306">Attributo</span><span class="sxs-lookup"><span data-stu-id="fd1d8-306">Attribute</span></span> | <span data-ttu-id="fd1d8-307">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd1d8-307">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="fd1d8-308">(Obbligatorio) ID pacchetto della dipendenza, ad esempio "EntityFramework" e "NUnit", ovvero il nome di pacchetto che nuget.org mostra nella pagina di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-308">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="fd1d8-309">(Obbligatorio) Intervallo di versioni accettabili come dipendenza.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-309">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="fd1d8-310">Per la sintassi esatta, vedere [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-310">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="fd1d8-311">Le versioni a virgola mobile non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-311">Floating versions are not supported.</span></span> |
| <span data-ttu-id="fd1d8-312">include</span><span class="sxs-lookup"><span data-stu-id="fd1d8-312">include</span></span> | <span data-ttu-id="fd1d8-313">Elenco delimitato da virgole di tag di inclusione/esclusione (vedere di seguito) che indicano la dipendenza da includere nel pacchetto finale.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-313">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="fd1d8-314">Il valore predefinito è `all`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-314">The default value is `all`.</span></span> |
| <span data-ttu-id="fd1d8-315">escludere</span><span class="sxs-lookup"><span data-stu-id="fd1d8-315">exclude</span></span> | <span data-ttu-id="fd1d8-316">Elenco delimitato da virgole di tag di inclusione/esclusione (vedere di seguito) che indicano la dipendenza da escludere nel pacchetto finale.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-316">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="fd1d8-317">Il valore predefinito è, `build,analyzers` che può essere sovrascritto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-317">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="fd1d8-318">Ma `content/ ContentFiles` sono esclusi anche in modo implicito nel pacchetto finale che non può essere sovrascritto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-318">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="fd1d8-319">I tag specificati con `exclude` hanno la precedenza rispetto a quelli specificati con `include`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-319">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="fd1d8-320">Ad esempio, `include="runtime, compile" exclude="compile"` è identico a `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-320">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

<span data-ttu-id="fd1d8-321">Quando si carica un pacchetto in nuget.org, ogni attributo di dipendenza `id` è limitato a 128 caratteri e l' `version` attributo è limitato a 256 caratteri.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-321">When uploading a package to nuget.org, each dependency's `id` attribute is limited to 128 characters and the `version` attribute is limited to 256 characters.</span></span>

| <span data-ttu-id="fd1d8-322">Tag di inclusione/esclusione</span><span class="sxs-lookup"><span data-stu-id="fd1d8-322">Include/Exclude tag</span></span> | <span data-ttu-id="fd1d8-323">Cartelle di destinazione interessate</span><span class="sxs-lookup"><span data-stu-id="fd1d8-323">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="fd1d8-324">contentFiles</span><span class="sxs-lookup"><span data-stu-id="fd1d8-324">contentFiles</span></span> | <span data-ttu-id="fd1d8-325">Contenuto</span><span class="sxs-lookup"><span data-stu-id="fd1d8-325">Content</span></span> |
| <span data-ttu-id="fd1d8-326">runtime</span><span class="sxs-lookup"><span data-stu-id="fd1d8-326">runtime</span></span> | <span data-ttu-id="fd1d8-327">Runtime, Resources e FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="fd1d8-327">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="fd1d8-328">compile</span><span class="sxs-lookup"><span data-stu-id="fd1d8-328">compile</span></span> | <span data-ttu-id="fd1d8-329">lib</span><span class="sxs-lookup"><span data-stu-id="fd1d8-329">lib</span></span> |
| <span data-ttu-id="fd1d8-330">build</span><span class="sxs-lookup"><span data-stu-id="fd1d8-330">build</span></span> | <span data-ttu-id="fd1d8-331">build (proprietà e destinazioni MSBuild)</span><span class="sxs-lookup"><span data-stu-id="fd1d8-331">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="fd1d8-332">nativi</span><span class="sxs-lookup"><span data-stu-id="fd1d8-332">native</span></span> | <span data-ttu-id="fd1d8-333">nativi</span><span class="sxs-lookup"><span data-stu-id="fd1d8-333">native</span></span> |
| <span data-ttu-id="fd1d8-334">Nessuno</span><span class="sxs-lookup"><span data-stu-id="fd1d8-334">none</span></span> | <span data-ttu-id="fd1d8-335">Nessuna cartella</span><span class="sxs-lookup"><span data-stu-id="fd1d8-335">No folders</span></span> |
| <span data-ttu-id="fd1d8-336">all</span><span class="sxs-lookup"><span data-stu-id="fd1d8-336">all</span></span> | <span data-ttu-id="fd1d8-337">Tutte le cartelle</span><span class="sxs-lookup"><span data-stu-id="fd1d8-337">All folders</span></span> |

<span data-ttu-id="fd1d8-338">Ad esempio, le righe seguenti indicano dipendenze da `PackageA` versione 1.1.0 o successive e da `PackageB` versione 1.x.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-338">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="fd1d8-339">Le righe seguenti indicano dipendenze dagli stessi pacchetti, ma specificano di includere le cartelle `contentFiles` e `build` di `PackageA` e tutte le cartelle tranne `native` e `compile` di `PackageB`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-339">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="fd1d8-340">Quando si crea un oggetto `.nuspec` da un progetto usando `nuget spec` , le dipendenze esistenti nel progetto non vengono incluse automaticamente nel `.nuspec` file risultante.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-340">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="fd1d8-341">Usare invece `nuget pack myproject.csproj` e ottenere il file con estensione *NuSpec* dall'interno del file *nupkg* generato.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-341">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="fd1d8-342">Questo *. NuSpec* contiene le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-342">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="fd1d8-343">Gruppi di dipendenze</span><span class="sxs-lookup"><span data-stu-id="fd1d8-343">Dependency groups</span></span>

<span data-ttu-id="fd1d8-344">*Versione 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="fd1d8-344">*Version 2.0+*</span></span>

<span data-ttu-id="fd1d8-345">In alternativa a un unico elenco semplice, è possibile specificare le dipendenze in base al profilo del framework del progetto di destinazione usando elementi `<group>` all'interno di `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-345">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="fd1d8-346">Ogni gruppo ha un attributo denominato `targetFramework` e contiene zero o più elementi `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-346">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="fd1d8-347">Tali dipendenze vengono installate insieme quando il framework di destinazione è compatibile con il profilo di framework del progetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-347">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="fd1d8-348">L'elemento `<group>` senza un attributo `targetFramework` viene usato come elenco predefinito o di fallback delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-348">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="fd1d8-349">Vedere [Framework di destinazione](../reference/target-frameworks.md) per gli identificatori di framework esatti.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-349">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="fd1d8-350">Il formato di gruppo non può essere usato in combinazione con un elenco semplice.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-350">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="fd1d8-351">Il formato del [moniker del Framework di destinazione (TFM)](../reference/target-frameworks.md) usato nella `lib/ref` cartella è diverso rispetto al TFM usato in `dependency groups` .</span><span class="sxs-lookup"><span data-stu-id="fd1d8-351">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="fd1d8-352">Se i Framework di destinazione dichiarati in `dependencies group` e la `lib/ref` cartella del `.nuspec` file non hanno corrispondenze esatte, il comando genererà l' `pack` [avviso NuGet NU5128](../reference/errors-and-warnings/nu5128.md).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-352">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="fd1d8-353">L'esempio seguente mostra variazioni diverse dell'elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-353">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework=".NETFramework4.7.2">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="netcoreapp3.1">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="fd1d8-354">Riferimenti espliciti agli assembly</span><span class="sxs-lookup"><span data-stu-id="fd1d8-354">Explicit assembly references</span></span>

<span data-ttu-id="fd1d8-355">L' `<references>` elemento viene usato dai progetti `packages.config` che usano per specificare in modo esplicito gli assembly a cui deve fare riferimento il progetto di destinazione quando si usa il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-355">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="fd1d8-356">I riferimenti espliciti vengono generalmente usati per gli assembly solo della fase di progettazione.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-356">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="fd1d8-357">Per ulteriori informazioni, vedere la pagina relativa alla [selezione degli assembly a cui fanno riferimento i progetti](../create-packages/select-assemblies-referenced-by-projects.md) .</span><span class="sxs-lookup"><span data-stu-id="fd1d8-357">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="fd1d8-358">Ad esempio, l'elemento `<references>` seguente indica a NuGet di aggiungere riferimenti solo a `xunit.dll` e a `xunit.extensions.dll` anche se sono presenti altri assembly nel pacchetto:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-358">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="fd1d8-359">Gruppi di riferimenti</span><span class="sxs-lookup"><span data-stu-id="fd1d8-359">Reference groups</span></span>

<span data-ttu-id="fd1d8-360">In alternativa a un unico elenco semplice, è possibile specificare i riferimenti in base al profilo del framework del progetto di destinazione usando elementi `<group>` all'interno di `<references>`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-360">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="fd1d8-361">Ogni gruppo ha un attributo denominato `targetFramework` e contiene zero o più elementi `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-361">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="fd1d8-362">Tali riferimenti vengono aggiunti a un progetto quando il framework di destinazione è compatibile con il profilo di framework del progetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-362">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="fd1d8-363">L'elemento `<group>` senza un attributo `targetFramework` viene usato come elenco predefinito o di fallback dei riferimenti.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-363">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="fd1d8-364">Vedere [Framework di destinazione](../reference/target-frameworks.md) per gli identificatori di framework esatti.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-364">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="fd1d8-365">Il formato di gruppo non può essere usato in combinazione con un elenco semplice.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-365">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="fd1d8-366">L'esempio seguente mostra variazioni diverse dell'elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-366">The following example shows different variations of the `<group>` element:</span></span>

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a><span data-ttu-id="fd1d8-367">Riferimenti agli assembly del framework</span><span class="sxs-lookup"><span data-stu-id="fd1d8-367">Framework assembly references</span></span>

<span data-ttu-id="fd1d8-368">Gli assembly del framework sono quelli che fanno parte di .NET Framework e devono essere già presenti nella Global Assembly Cache (GAC) per qualsiasi computer.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-368">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="fd1d8-369">Grazie all'identificazione di tali assembly all'interno dell'elemento `<frameworkAssemblies>`, un pacchetto può garantire che i riferimenti necessari vengano aggiunti a un progetto nel caso in cui il progetto non includa già tali riferimenti.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-369">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="fd1d8-370">Tali assembly, ovviamente, non vengono inclusi in un pacchetto direttamente.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-370">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="fd1d8-371">L'elemento `<frameworkAssemblies>` contiene zero o più elementi `<frameworkAssembly>`, ognuno dei quali specifica gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-371">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="fd1d8-372">Attributo</span><span class="sxs-lookup"><span data-stu-id="fd1d8-372">Attribute</span></span> | <span data-ttu-id="fd1d8-373">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd1d8-373">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fd1d8-374">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-374">**assemblyName**</span></span> | <span data-ttu-id="fd1d8-375">(Obbligatorio) Nome completo dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-375">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="fd1d8-376">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-376">**targetFramework**</span></span> | <span data-ttu-id="fd1d8-377">(Facoltativo) Specifica il framework di destinazione a cui si applica questo riferimento.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-377">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="fd1d8-378">Se omesso, indica che il riferimento si applica a tutti i framework.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-378">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="fd1d8-379">Vedere [Framework di destinazione](../reference/target-frameworks.md) per gli identificatori di framework esatti.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-379">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="fd1d8-380">L'esempio seguente mostra un riferimento a `System.Net` per tutti i framework di destinazione e un riferimento a `System.ServiceModel` solo per .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-380">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="fd1d8-381">Inclusione di file di assembly</span><span class="sxs-lookup"><span data-stu-id="fd1d8-381">Including assembly files</span></span>

<span data-ttu-id="fd1d8-382">Se si seguono le convenzioni descritte in [Creazione di un pacchetto](../create-packages/creating-a-package.md), non è necessario specificare in modo esplicito un elenco di file nel file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-382">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="fd1d8-383">Il comando `nuget pack` rileva automaticamente i file necessari.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-383">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="fd1d8-384">Quando un pacchetto viene installato in un progetto, NuGet aggiunge automaticamente i riferimenti agli assembly alle DLL del pacchetto, *escludendo* quelli denominati `.resources.dll` perché si presuppone che siano assembly satellite localizzati.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-384">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="fd1d8-385">Per questo motivo, evitare di usare `.resources.dll` per i file che contengono invece codice essenziale per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-385">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="fd1d8-386">Per evitare questo comportamento automatico e controllare in modo esplicito quali file vengono inclusi in un pacchetto, posizionare un elemento `<files>` come elemento figlio di `<package>` (ed elemento di pari livello di `<metadata>`), identificando ogni file con un elemento `<file>` separato.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-386">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="fd1d8-387">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-387">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="fd1d8-388">Con NuGet 2.x e versioni precedenti e i progetti che usano `packages.config`, l'elemento `<files>` viene usato anche per includere file di contenuto non modificabili quando viene installato un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-388">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="fd1d8-389">Con NuGet 3.3 + e PackageReference per i progetti, viene invece usato l'elemento `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-389">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="fd1d8-390">Vedere [Inclusione di file di contenuto](#including-content-files) di seguito per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-390">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="fd1d8-391">Attributi dell'elemento file</span><span class="sxs-lookup"><span data-stu-id="fd1d8-391">File element attributes</span></span>

<span data-ttu-id="fd1d8-392">Ogni elemento `<file>` specifica gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-392">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="fd1d8-393">Attributo</span><span class="sxs-lookup"><span data-stu-id="fd1d8-393">Attribute</span></span> | <span data-ttu-id="fd1d8-394">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd1d8-394">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fd1d8-395">**src**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-395">**src**</span></span> | <span data-ttu-id="fd1d8-396">Percorso del file o dei file da includere, soggetto alle esclusioni specificate dall'attributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-396">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="fd1d8-397">Il percorso è relativo al file `.nuspec`, a meno che non venga specificato un percorso assoluto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-397">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="fd1d8-398">Il carattere jolly `*` è consentito e il carattere jolly doppio `**` implica una ricerca ricorsiva nelle cartelle.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-398">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="fd1d8-399">**target**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-399">**target**</span></span> | <span data-ttu-id="fd1d8-400">Percorso relativo della cartella all'interno del pacchetto in cui vengono collocati i file di origine, che deve iniziare con `lib`, `content`, `build` o `tools`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-400">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="fd1d8-401">Vedere [Creazione di un file .nuspec da una directory di lavoro basata su convenzioni](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-401">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="fd1d8-402">**escludere**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-402">**exclude**</span></span> | <span data-ttu-id="fd1d8-403">Elenco delimitato da punti e virgola dei file o dei modelli di file da escludere dal percorso `src`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-403">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="fd1d8-404">Il carattere jolly `*` è consentito e il carattere jolly doppio `**` implica una ricerca ricorsiva nelle cartelle.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-404">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="fd1d8-405">Esempi</span><span class="sxs-lookup"><span data-stu-id="fd1d8-405">Examples</span></span>

<span data-ttu-id="fd1d8-406">**Singolo assembly**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-406">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="fd1d8-407">**Singolo assembly specifico di un framework di destinazione**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-407">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="fd1d8-408">**Set di DLL con un carattere jolly**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-408">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="fd1d8-409">**DLL per framework diversi**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-409">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="fd1d8-410">**Esclusione di file**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-410">**Excluding files**</span></span>

    Source files:
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a><span data-ttu-id="fd1d8-411">Inclusione di file di contenuto</span><span class="sxs-lookup"><span data-stu-id="fd1d8-411">Including content files</span></span>

<span data-ttu-id="fd1d8-412">I file di contenuto sono file non modificabili che un pacchetto deve includere in un progetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-412">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="fd1d8-413">Essendo non modificabili, non sono progettati per essere modificati dal progetto che li utilizza.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-413">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="fd1d8-414">Alcuni esempi di file di contenuto includono:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-414">Example content files include:</span></span>

- <span data-ttu-id="fd1d8-415">Immagini incorporate come risorse</span><span class="sxs-lookup"><span data-stu-id="fd1d8-415">Images that are embedded as resources</span></span>
- <span data-ttu-id="fd1d8-416">File di origine già compilati</span><span class="sxs-lookup"><span data-stu-id="fd1d8-416">Source files that are already compiled</span></span>
- <span data-ttu-id="fd1d8-417">Script che devono essere inclusi con l'output di compilazione del progetto</span><span class="sxs-lookup"><span data-stu-id="fd1d8-417">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="fd1d8-418">File di configurazione per il pacchetto che devono essere inclusi nel progetto ma non richiedono modifiche specifiche del progetto</span><span class="sxs-lookup"><span data-stu-id="fd1d8-418">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="fd1d8-419">I file di contenuto vengono inclusi in un pacchetto con l'elemento `<files>`, specificando la cartella `content` nell'attributo `target`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-419">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="fd1d8-420">Questi file vengono tuttavia ignorati quando il pacchetto viene installato in un progetto usando PackageReference, che usa invece l'elemento `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-420">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="fd1d8-421">Per ottenere la massima compatibilità con i progetti in cui viene utilizzato, un pacchetto specifica idealmente i file di contenuto in entrambi gli elementi.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-421">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="fd1d8-422">Uso dell'elemento files per i file di contenuto</span><span class="sxs-lookup"><span data-stu-id="fd1d8-422">Using the files element for content files</span></span>

<span data-ttu-id="fd1d8-423">Per i file di contenuto, usare semplicemente lo stesso formato usato per i file di assembly, ma specificare `content` come cartella di base nell'attributo `target`, come illustrato negli esempi seguenti.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-423">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="fd1d8-424">**File di contenuto semplici**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-424">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="fd1d8-425">**File di contenuto con struttura di directory**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-425">**Content files with directory structure**</span></span>

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

<span data-ttu-id="fd1d8-426">**File di contenuto specifico di un framework di destinazione**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-426">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="fd1d8-427">**File di contenuto copiato in una cartella con un punto nel nome**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-427">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="fd1d8-428">In questo caso, NuGet rileva che l'estensione in `target` non corrisponde all'estensione in `src`, quindi interpreta la parte del nome in `target` come cartella:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-428">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="fd1d8-429">**File di contenuto senza estensione**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-429">**Content files without extensions**</span></span>

<span data-ttu-id="fd1d8-430">Per includere i file senza estensione, usare i caratteri jolly `*` o `**`:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-430">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="fd1d8-431">**File di contenuto con percorso completo e destinazione completa**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-431">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="fd1d8-432">In questo caso, dato che le estensioni dei file di origine e di destinazione corrispondono, NuGet presuppone che la destinazione sia un nome di file e non una cartella:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-432">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="fd1d8-433">**Ridenominazione di un file di contenuto nel pacchetto**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-433">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="fd1d8-434">**Esclusione di file**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-434">**Excluding files**</span></span>

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="fd1d8-435">Uso dell'elemento contentFiles per i file di contenuto</span><span class="sxs-lookup"><span data-stu-id="fd1d8-435">Using the contentFiles element for content files</span></span>

<span data-ttu-id="fd1d8-436">*NuGet 4.0 + con PackageReference*</span><span class="sxs-lookup"><span data-stu-id="fd1d8-436">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="fd1d8-437">Per impostazione predefinita, un pacchetto inserisce il contenuto in una cartella `contentFiles` (vedere di seguito) e `nuget pack` include tutti i file nella cartella usando gli attributi predefiniti.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-437">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="fd1d8-438">In questo caso non è affatto necessario includere un nodo `contentFiles` nel file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-438">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="fd1d8-439">Per controllare quali file sono inclusi, l'elemento `<contentFiles>` specifica una raccolta di elementi `<files>` che identificano i file esatti inclusi.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-439">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="fd1d8-440">Questi file sono specificati con un set di attributi che descrivono come devono essere usati all'interno del sistema del progetto:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-440">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="fd1d8-441">Attributo</span><span class="sxs-lookup"><span data-stu-id="fd1d8-441">Attribute</span></span> | <span data-ttu-id="fd1d8-442">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd1d8-442">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fd1d8-443">**includere**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-443">**include**</span></span> | <span data-ttu-id="fd1d8-444">(Obbligatorio) Percorso del file o dei file da includere, soggetto alle esclusioni specificate dall'attributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-444">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="fd1d8-445">Il percorso è relativo alla `contentFiles` cartella, a meno che non sia specificato un percorso assoluto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-445">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="fd1d8-446">Il carattere jolly `*` è consentito e il carattere jolly doppio `**` implica una ricerca ricorsiva nelle cartelle.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-446">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="fd1d8-447">**escludere**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-447">**exclude**</span></span> | <span data-ttu-id="fd1d8-448">Elenco delimitato da punti e virgola dei file o dei modelli di file da escludere dal percorso `src`.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-448">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="fd1d8-449">Il carattere jolly `*` è consentito e il carattere jolly doppio `**` implica una ricerca ricorsiva nelle cartelle.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-449">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="fd1d8-450">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-450">**buildAction**</span></span> | <span data-ttu-id="fd1d8-451">Azione di compilazione da assegnare all'elemento di contenuto per MSBuild, ad esempio `Content` , `None` , `Embedded Resource` , `Compile` e così via. Il valore predefinito è `Compile` .</span><span class="sxs-lookup"><span data-stu-id="fd1d8-451">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="fd1d8-452">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-452">**copyToOutput**</span></span> | <span data-ttu-id="fd1d8-453">Valore booleano che indica se copiare gli elementi di contenuto nella cartella di output di compilazione o pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-453">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="fd1d8-454">Il valore predefinito è false.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-454">The default is false.</span></span> |
| <span data-ttu-id="fd1d8-455">**flatten**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-455">**flatten**</span></span> | <span data-ttu-id="fd1d8-456">Valore booleano che indica se copiare gli elementi di contenuto di una singola cartella nell'output di compilazione (true) o se mantenere la struttura di cartelle nel pacchetto (false).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-456">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="fd1d8-457">Questo flag funziona solo quando il flag copyToOutput è impostato su true.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-457">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="fd1d8-458">Il valore predefinito è false.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-458">The default is false.</span></span> |

<span data-ttu-id="fd1d8-459">Quando si installa un pacchetto, NuGet applica gli elementi figlio di `<contentFiles>` dall'alto verso il basso.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-459">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="fd1d8-460">Se più voci corrispondono allo stesso file, vengono applicate tutte le voci.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-460">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="fd1d8-461">La voce di livello superiore sostituisce le voci inferiori in presenza di un conflitto per lo stesso attributo.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-461">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="fd1d8-462">Struttura delle cartelle del pacchetto</span><span class="sxs-lookup"><span data-stu-id="fd1d8-462">Package folder structure</span></span>

<span data-ttu-id="fd1d8-463">Il progetto del pacchetto deve strutturare il contenuto in base al modello seguente:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-463">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="fd1d8-464">`codeLanguages` può essere `cs`, `vb`, `fs`, `any` o l'equivalente in caratteri minuscoli di uno specifico `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="fd1d8-464">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="fd1d8-465">`TxM` è qualsiasi moniker di framework di destinazione valido supportato da NuGet (vedere [Framework di destinazione](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="fd1d8-465">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="fd1d8-466">Qualsiasi struttura di cartelle può essere aggiunta alla fine di questa sintassi.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-466">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="fd1d8-467">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-467">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="fd1d8-468">Le cartelle vuote possono usare `.` per rifiutare esplicitamente di fornire contenuti per determinate combinazioni di linguaggio e TxM, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-468">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="fd1d8-469">Sezione di esempio contentFiles</span><span class="sxs-lookup"><span data-stu-id="fd1d8-469">Example contentFiles section</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <contentFiles>
            <!-- Embed image resources -->
            <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
            <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

            <!-- Embed all image resources under contentFiles/cs/ -->
            <files include="cs/**/*.png" buildAction="EmbeddedResource" />

            <!-- Copy config.xml to the root of the output folder -->
            <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

            <!-- Copy run.cmd to the output folder and keep the directory structure -->
            <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

            <!-- Include everything in the scripts folder except exe files -->
            <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
        </contentFiles>
        </metadata>
</package>
```

## <a name="framework-reference-groups"></a><span data-ttu-id="fd1d8-470">Gruppi di riferimento del Framework</span><span class="sxs-lookup"><span data-stu-id="fd1d8-470">Framework reference groups</span></span>

<span data-ttu-id="fd1d8-471">*Versione 5.1 + wih solo PackageReference*</span><span class="sxs-lookup"><span data-stu-id="fd1d8-471">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="fd1d8-472">I riferimenti al Framework sono un concetto .NET Core che rappresenta Framework condivisi, ad esempio WPF o Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-472">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="fd1d8-473">Specificando un Framework condiviso, il pacchetto garantisce che tutte le relative dipendenze del Framework siano incluse nel progetto di riferimento.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-473">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="fd1d8-474">Ogni `<group>` elemento richiede un `targetFramework` attributo e zero o più `<frameworkReference>` elementi.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-474">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="fd1d8-475">Nell'esempio seguente viene illustrato un NuSpec generato per un progetto WPF .NET Core.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-475">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="fd1d8-476">Si noti che la creazione manuale di nuspecs che contengono riferimenti al Framework non è consigliata.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-476">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="fd1d8-477">Prendere in considerazione l'uso del pacchetto [targets](msbuild-targets.md) , che li dedurrà automaticamente dal progetto.</span><span class="sxs-lookup"><span data-stu-id="fd1d8-477">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

```xml
<package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
  <metadata>
    <dependencies>
      <group targetFramework=".NETCoreApp3.1" />
    </dependencies>
    <frameworkReferences>
      <group targetFramework=".NETCoreApp3.1">
        <frameworkReference name="Microsoft.WindowsDesktop.App.WPF" />
      </group>
    </frameworkReferences>
  </metadata>
</package>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="fd1d8-478">File nuspec di esempio</span><span class="sxs-lookup"><span data-stu-id="fd1d8-478">Example nuspec files</span></span>

<span data-ttu-id="fd1d8-479">**File `.nuspec` semplice che non specifica dipendenze o file**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-479">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

<span data-ttu-id="fd1d8-480">**File `.nuspec` con dipendenze**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-480">**A `.nuspec` with dependencies**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

<span data-ttu-id="fd1d8-481">**File `.nuspec` con file**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-481">**A `.nuspec` with files**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

<span data-ttu-id="fd1d8-482">**File `.nuspec` con assembly di framework**</span><span class="sxs-lookup"><span data-stu-id="fd1d8-482">**A `.nuspec` with framework assemblies**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

<span data-ttu-id="fd1d8-483">In questo esempio vengono installati i componenti seguenti per destinazioni di progetto specifiche:</span><span class="sxs-lookup"><span data-stu-id="fd1d8-483">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="fd1d8-484">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="fd1d8-484">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="fd1d8-485">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="fd1d8-485">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="fd1d8-486">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="fd1d8-486">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="fd1d8-487">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="fd1d8-487">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
