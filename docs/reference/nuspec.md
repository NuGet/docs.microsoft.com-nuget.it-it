---
title: Informazioni di riferimento sul file con estensione nuspec per NuGet
description: Il file. nuspec contiene i metadati del pacchetto usati per la compilazione e per fornire informazioni ai consumer del pacchetto.
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: ed865aad6f72752adcf3e3921287a20b961c4a8a
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901811"
---
# <a name="nuspec-reference"></a><span data-ttu-id="13469-103">Informazioni di riferimento sul file .nuspec</span><span class="sxs-lookup"><span data-stu-id="13469-103">.nuspec reference</span></span>

<span data-ttu-id="13469-104">Un file `.nuspec` è un manifesto XML che contiene i metadati del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="13469-105">Questo manifesto viene usato per compilare il pacchetto e per fornire informazioni ai consumer.</span><span class="sxs-lookup"><span data-stu-id="13469-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="13469-106">Il manifesto viene sempre incluso in un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="13469-107">In questo argomento</span><span class="sxs-lookup"><span data-stu-id="13469-107">In this topic:</span></span>

- [<span data-ttu-id="13469-108">Formato generale e schema</span><span class="sxs-lookup"><span data-stu-id="13469-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="13469-109">[Token di sostituzione](#replacement-tokens) (usati con un progetto di Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="13469-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="13469-110">Dipendenze</span><span class="sxs-lookup"><span data-stu-id="13469-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="13469-111">Riferimenti espliciti agli assembly</span><span class="sxs-lookup"><span data-stu-id="13469-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="13469-112">Riferimenti agli assembly del framework</span><span class="sxs-lookup"><span data-stu-id="13469-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="13469-113">Inclusione di file di assembly</span><span class="sxs-lookup"><span data-stu-id="13469-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="13469-114">Inclusione di file di contenuto</span><span class="sxs-lookup"><span data-stu-id="13469-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="13469-115">File nuspec di esempio</span><span class="sxs-lookup"><span data-stu-id="13469-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="13469-116">Compatibilità dei tipi di progetto</span><span class="sxs-lookup"><span data-stu-id="13469-116">Project type compatibility</span></span>

- <span data-ttu-id="13469-117">Usare `.nuspec` con per i progetti non di tipo SDK che usano `nuget.exe pack` `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="13469-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="13469-118">Non è necessario un file per creare pacchetti per progetti di tipo SDK (in genere progetti .NET Core e .NET Standard che `.nuspec` usano l'attributo [SDK](/dotnet/core/tools/csproj#additions)). [](../resources/check-project-format.md)</span><span class="sxs-lookup"><span data-stu-id="13469-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="13469-119">Si noti che `.nuspec` quando si crea il pacchetto viene generato un oggetto .</span><span class="sxs-lookup"><span data-stu-id="13469-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="13469-120">Se si crea un pacchetto usando o , è consigliabile includere nel file di progetto tutte le proprietà che in genere si trovano `dotnet.exe pack` `msbuild pack target` nel file di [](../reference/msbuild-targets.md#pack-target) `.nuspec` progetto.</span><span class="sxs-lookup"><span data-stu-id="13469-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="13469-121">È tuttavia possibile scegliere di usare un [file per la creazione di un pacchetto usando `.nuspec` `dotnet.exe` o `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="13469-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec-file).</span></span>

- <span data-ttu-id="13469-122">Per i progetti migrati da a PackageReference , non è necessario `packages.config` un file per creare il [](../consume-packages/package-references-in-project-files.md) `.nuspec` pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="13469-123">Usare invece [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="13469-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="13469-124">Formato generale e schema</span><span class="sxs-lookup"><span data-stu-id="13469-124">General form and schema</span></span>

<span data-ttu-id="13469-125">Il file dello schema di `nuspec.xsd` corrente è disponibile nel [repository GitHub di NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="13469-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="13469-126">All'interno di questo schema, un file `.nuspec` ha il formato generale seguente:</span><span class="sxs-lookup"><span data-stu-id="13469-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="13469-127">Per una rappresentazione visiva chiara dello schema, aprire il file di schema in Visual Studio in modalità progettazione e fare clic sul collegamento **XML Schema Explorer**.</span><span class="sxs-lookup"><span data-stu-id="13469-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="13469-128">In alternativa, aprire il file come codice, fare clic con il pulsante destro del mouse nell'editor e scegliere **Mostra in XML Schema Explorer**.</span><span class="sxs-lookup"><span data-stu-id="13469-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="13469-129">In entrambi i casi si ottiene una visualizzazione simile alla seguente (quando è per la maggior parte espansa):</span><span class="sxs-lookup"><span data-stu-id="13469-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio Schema Explorer con nuspec.xsd aperto](media/SchemaExplorer.png)

<span data-ttu-id="13469-131">Tutti i nomi degli elementi XML nel file con estensione nuspec fa distinzione tra maiuscole e minuscole, come nel caso di XML in generale.</span><span class="sxs-lookup"><span data-stu-id="13469-131">All XML element names in the .nuspec file are case-sensitive, as is the case for XML in general.</span></span> <span data-ttu-id="13469-132">Ad esempio, l'uso dell'elemento `<description>` di metadati è corretto e non è `<Description>` corretto.</span><span class="sxs-lookup"><span data-stu-id="13469-132">For example, using the metadata element `<description>` is correct and `<Description>` is not correct.</span></span> <span data-ttu-id="13469-133">La corretta distinzione tra maiuscole e minuscole per ogni nome di elemento è documentata di seguito.</span><span class="sxs-lookup"><span data-stu-id="13469-133">The proper casing for each element name is documented below.</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="13469-134">Elementi dei metadati obbligatori</span><span class="sxs-lookup"><span data-stu-id="13469-134">Required metadata elements</span></span>

<span data-ttu-id="13469-135">Anche se gli elementi seguenti sono i requisiti minimi per un pacchetto, è consigliabile aggiungere gli [elementi dei metadati facoltativi](#optional-metadata-elements) per migliorare l'esperienza complessiva degli sviluppatori con il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-135">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="13469-136">Questi elementi devono essere visualizzati all'interno di un elemento `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="13469-136">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="13469-137">id</span><span class="sxs-lookup"><span data-stu-id="13469-137">id</span></span> 
<span data-ttu-id="13469-138">Identificatore del pacchetto senza distinzione tra maiuscole e minuscole che deve essere univoco in nuget.org o in qualsiasi raccolta in cui risiede il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-138">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="13469-139">L'ID non può contenere spazi o caratteri non validi per un URL e in genere segue le regole dello spazio dei nomi .NET.</span><span class="sxs-lookup"><span data-stu-id="13469-139">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="13469-140">Vedere [Choosing a unique package identifier and setting the version number](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) (Scelta di un identificatore univoco del pacchetto e impostazione del numero di versione) per altre indicazioni.</span><span class="sxs-lookup"><span data-stu-id="13469-140">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>

<span data-ttu-id="13469-141">Quando si carica un pacchetto in nuget.org, il `id` campo è limitato a 128 caratteri.</span><span class="sxs-lookup"><span data-stu-id="13469-141">When uploading a package to nuget.org, the `id` field is limited to 128 characters.</span></span>

#### <a name="version"></a><span data-ttu-id="13469-142">version</span><span class="sxs-lookup"><span data-stu-id="13469-142">version</span></span>
<span data-ttu-id="13469-143">La versione del pacchetto secondo il criterio *principale.secondaria.patch*.</span><span class="sxs-lookup"><span data-stu-id="13469-143">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="13469-144">I numeri di versione possono includere un suffisso di versione non definitiva, come descritto in [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="13469-144">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 

<span data-ttu-id="13469-145">Quando si carica un pacchetto in nuget.org, il `version` campo è limitato a 64 caratteri.</span><span class="sxs-lookup"><span data-stu-id="13469-145">When uploading a package to nuget.org, the `version` field is limited to 64 characters.</span></span>

#### <a name="description"></a><span data-ttu-id="13469-146">Descrizione</span><span class="sxs-lookup"><span data-stu-id="13469-146">description</span></span>
<span data-ttu-id="13469-147">Descrizione del pacchetto per la visualizzazione dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="13469-147">A description of the package for UI display.</span></span>

<span data-ttu-id="13469-148">Quando si carica un pacchetto in nuget.org, `description` il campo è limitato a 4000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="13469-148">When uploading a package to nuget.org, the `description` field is limited to 4000 characters.</span></span>

#### <a name="authors"></a><span data-ttu-id="13469-149">authors</span><span class="sxs-lookup"><span data-stu-id="13469-149">authors</span></span>
<span data-ttu-id="13469-150">Elenco delimitato da virgole di autori di pacchetti, corrispondenti ai nomi dei profili nuget.org. Questi vengono visualizzati nella raccolta NuGet in nuget.org e vengono usati per creare riferimenti incrociati ai pacchetti da parte degli stessi autori.</span><span class="sxs-lookup"><span data-stu-id="13469-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

<span data-ttu-id="13469-151">Quando si carica un pacchetto in nuget.org, `authors` il campo è limitato a 4000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="13469-151">When uploading a package to nuget.org, the `authors` field is limited to 4000 characters.</span></span>

### <a name="optional-metadata-elements"></a><span data-ttu-id="13469-152">Elementi dei metadati facoltativi</span><span class="sxs-lookup"><span data-stu-id="13469-152">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="13469-153">owners</span><span class="sxs-lookup"><span data-stu-id="13469-153">owners</span></span>
> [!Important]
> <span data-ttu-id="13469-154">owners è deprecato.</span><span class="sxs-lookup"><span data-stu-id="13469-154">owners is deprecated.</span></span> <span data-ttu-id="13469-155">Usare invece gli autori.</span><span class="sxs-lookup"><span data-stu-id="13469-155">Use authors instead.</span></span>

<span data-ttu-id="13469-156">Elenco delimitato da virgole degli autori di pacchetti che usano nomi di profilo nuget.org. Questo è spesso lo stesso elenco di e viene ignorato quando si `authors` carica il pacchetto in nuget.org. Vedere [Gestione dei proprietari dei pacchetti in nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="13469-156">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="13469-157">projectUrl</span><span class="sxs-lookup"><span data-stu-id="13469-157">projectUrl</span></span>
<span data-ttu-id="13469-158">URL della pagina iniziale del pacchetto, spesso visualizzato nell'interfaccia utente e in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="13469-158">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

<span data-ttu-id="13469-159">Quando si carica un pacchetto in nuget.org, il campo è limitato a `projectUrl` 4000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="13469-159">When uploading a package to nuget.org, the `projectUrl` field is limited to 4000 characters.</span></span>

#### <a name="licenseurl"></a><span data-ttu-id="13469-160">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="13469-160">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="13469-161">licenseUrl è deprecato.</span><span class="sxs-lookup"><span data-stu-id="13469-161">licenseUrl is deprecated.</span></span> <span data-ttu-id="13469-162">Usare invece la licenza.</span><span class="sxs-lookup"><span data-stu-id="13469-162">Use license instead.</span></span>

<span data-ttu-id="13469-163">URL per la licenza del pacchetto, spesso visualizzato nelle informazioni utente come nuget.org.</span><span class="sxs-lookup"><span data-stu-id="13469-163">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

<span data-ttu-id="13469-164">Quando si carica un pacchetto in nuget.org, il campo è limitato a `licenseUrl` 4000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="13469-164">When uploading a package to nuget.org, the `licenseUrl` field is limited to 4000 characters.</span></span>

#### <a name="license"></a><span data-ttu-id="13469-165">license</span><span class="sxs-lookup"><span data-stu-id="13469-165">license</span></span>

<span data-ttu-id="13469-166">*Supportato con **NuGet 4.9.0** e versioni successive*</span><span class="sxs-lookup"><span data-stu-id="13469-166">*Supported with **NuGet 4.9.0** and above*</span></span>

<span data-ttu-id="13469-167">Espressione di licenza SPDX o percorso di un file di licenza all'interno del pacchetto, spesso visualizzato in un'api come nuget.org. Se si ha la licenza del pacchetto con una licenza comune, ad esempio MIT o BSD-2-Clause, usare l'identificatore di [licenza SPDX associato.](https://spdx.org/licenses/)</span><span class="sxs-lookup"><span data-stu-id="13469-167">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="13469-168">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="13469-168">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="13469-169">NuGet.org accetta solo espressioni di licenza approvate dall'iniziativa Open Source o da Free Software Foundation.</span><span class="sxs-lookup"><span data-stu-id="13469-169">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="13469-170">Se il pacchetto è concesso in licenza con più licenze comuni, è possibile specificare una licenza composita usando la sintassi [dell'espressione SPDX versione 2.0.](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)</span><span class="sxs-lookup"><span data-stu-id="13469-170">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="13469-171">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="13469-171">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="13469-172">Se si usa una licenza personalizzata non supportata dalle espressioni di licenza, è possibile creare un pacchetto di un `.txt` file o con il testo della `.md` licenza.</span><span class="sxs-lookup"><span data-stu-id="13469-172">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="13469-173">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="13469-173">For example:</span></span>

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

<span data-ttu-id="13469-174">Per l'equivalente di MSBuild, vedere Creazione di un'espressione di licenza o [di un file di licenza](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="13469-174">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="13469-175">La sintassi esatta delle espressioni di licenza di NuGet è descritta di seguito in [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="13469-175">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>

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

#### <a name="iconurl"></a><span data-ttu-id="13469-176">iconUrl</span><span class="sxs-lookup"><span data-stu-id="13469-176">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="13469-177">iconUrl è deprecato.</span><span class="sxs-lookup"><span data-stu-id="13469-177">iconUrl is deprecated.</span></span> <span data-ttu-id="13469-178">Usare invece l'icona .</span><span class="sxs-lookup"><span data-stu-id="13469-178">Use icon instead.</span></span>

<span data-ttu-id="13469-179">URL per un'immagine 128x128 con sfondo trasparente da usare come icona per il pacchetto nella visualizzazione dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="13469-179">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="13469-180">Assicurarsi che questo elemento contenga l'*URL diretto dell'immagine* e non l'URL di una pagina Web contenente l'immagine.</span><span class="sxs-lookup"><span data-stu-id="13469-180">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="13469-181">Ad esempio, per usare un'immagine da GitHub, usare l'URL del file non elaborato come <em> https://github.com/ \<username\> / \<repository\> /raw/ \<branch\> / \<logo.png\> </em>.</span><span class="sxs-lookup"><span data-stu-id="13469-181">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

<span data-ttu-id="13469-182">Quando si carica un pacchetto in nuget.org, il campo è limitato a `iconUrl` 4000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="13469-182">When uploading a package to nuget.org, the `iconUrl` field is limited to 4000 characters.</span></span>

#### <a name="icon"></a><span data-ttu-id="13469-183">icon</span><span class="sxs-lookup"><span data-stu-id="13469-183">icon</span></span>

<span data-ttu-id="13469-184">*Supportato con **NuGet 5.3.0** e versioni successive*</span><span class="sxs-lookup"><span data-stu-id="13469-184">*Supported with **NuGet 5.3.0** and above*</span></span>

<span data-ttu-id="13469-185">Si tratta di un percorso di un file di immagine all'interno del pacchetto, spesso visualizzato in ui come nuget.org come icona del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-185">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="13469-186">Le dimensioni del file di immagine sono limitate a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="13469-186">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="13469-187">I formati di file supportati includono JPEG e PNG.</span><span class="sxs-lookup"><span data-stu-id="13469-187">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="13469-188">È consigliabile una risoluzione dell'immagine di 128x128.</span><span class="sxs-lookup"><span data-stu-id="13469-188">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="13469-189">Ad esempio, è necessario aggiungere quanto segue a nuspec quando si crea un pacchetto usando nuget.exe:</span><span class="sxs-lookup"><span data-stu-id="13469-189">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

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

[<span data-ttu-id="13469-190">Esempio nuspec dell'icona del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-190">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/main/PackageIconNuspecExample)

<span data-ttu-id="13469-191">Per l'equivalente di MSBuild, vedere Creazione di un [pacchetto di un file di immagine icona](msbuild-targets.md#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="13469-191">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="13469-192">È possibile specificare sia `icon` che per mantenere la `iconUrl` compatibilità con le versioni precedenti con origini che non supportano `icon` .</span><span class="sxs-lookup"><span data-stu-id="13469-192">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="13469-193">Visual Studio supporterà `icon` i pacchetti provenienti da un'origine basata su cartelle in una versione futura.</span><span class="sxs-lookup"><span data-stu-id="13469-193">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="readme"></a><span data-ttu-id="13469-194">leggimi</span><span class="sxs-lookup"><span data-stu-id="13469-194">readme</span></span>

<span data-ttu-id="13469-195">*Supportato con **NuGet 5.10.0 Preview 2** e versioni successive*</span><span class="sxs-lookup"><span data-stu-id="13469-195">*Supported with **NuGet 5.10.0 preview 2** and above*</span></span>

<span data-ttu-id="13469-196">Quando si esegue il pacchetto di un file Leggimi, è necessario usare l'elemento per specificare il percorso del pacchetto, relativo alla `readme` radice del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-196">When packing a readme file, you need to use the `readme` element to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="13469-197">Inoltre, è necessario assicurarsi che il file sia incluso nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-197">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="13469-198">I formati di file supportati includono solo Markdown (*md*).</span><span class="sxs-lookup"><span data-stu-id="13469-198">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="13469-199">Ad esempio, è necessario aggiungere quanto segue a nuspec per creare un pacchetto di un file Leggimi con il progetto:</span><span class="sxs-lookup"><span data-stu-id="13469-199">For example, you would add the following to your nuspec in order to pack a readme file with your project:</span></span>

```xml
<package>
  <metadata>
    ...
    <readme>docs\readme.md</readme>
    ...
  </metadata>
  <files>
    ...
    <file src="..\readme.md" target="docs\" />
    ...
  </files>
</package>
```

<span data-ttu-id="13469-200">Per l'equivalente di MSBuild, vedere Creazione [di un file Leggimi](msbuild-targets.md#packagereadmefile).</span><span class="sxs-lookup"><span data-stu-id="13469-200">For the MSBuild equivalent, take a look at [Packing a readme file](msbuild-targets.md#packagereadmefile).</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="13469-201">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="13469-201">requireLicenseAcceptance</span></span>
<span data-ttu-id="13469-202">Valore booleano che specifica se il client deve richiedere al consumer di accettare la licenza del pacchetto prima di installarlo.</span><span class="sxs-lookup"><span data-stu-id="13469-202">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="13469-203">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="13469-203">developmentDependency</span></span>
<span data-ttu-id="13469-204">*(2.8 +)* Valore booleano che specifica se il pacchetto deve essere contrassegnato come dipendenza solo per lo sviluppo, in modo che il pacchetto non possa essere incluso come dipendenza in altri pacchetti.</span><span class="sxs-lookup"><span data-stu-id="13469-204">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="13469-205">Con PackageReference (NuGet 4.8 +), questo flag indica anche che gli asset in fase di compilazione verranno esclusi dalla compilazione.</span><span class="sxs-lookup"><span data-stu-id="13469-205">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="13469-206">Vedere [Supporto developmentDependency per PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="13469-206">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="13469-207">riepilogo</span><span class="sxs-lookup"><span data-stu-id="13469-207">summary</span></span>
> [!Important]
> <span data-ttu-id="13469-208">`summary` è in fase di deprecazione.</span><span class="sxs-lookup"><span data-stu-id="13469-208">`summary` is being deprecated.</span></span> <span data-ttu-id="13469-209">In alternativa, utilizzare `description`.</span><span class="sxs-lookup"><span data-stu-id="13469-209">Use `description` instead.</span></span>

<span data-ttu-id="13469-210">Descrizione breve del pacchetto per la visualizzazione dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="13469-210">A short description of the package for UI display.</span></span> <span data-ttu-id="13469-211">Se omesso, viene usata una versione troncata di `description`.</span><span class="sxs-lookup"><span data-stu-id="13469-211">If omitted, a truncated version of `description` is used.</span></span>

<span data-ttu-id="13469-212">Quando si carica un pacchetto in nuget.org, `summary` il campo è limitato a 4000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="13469-212">When uploading a package to nuget.org, the `summary` field is limited to 4000 characters.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="13469-213">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="13469-213">releaseNotes</span></span>
<span data-ttu-id="13469-214">*(1.5+)* Descrizione delle modifiche apportate in questa versione del pacchetto, spesso usata nell'interfaccia utente, come la scheda **Aggiornamenti** di Gestione pacchetti di Visual Studio, in sostituzione della descrizione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-214">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

<span data-ttu-id="13469-215">Quando si carica un pacchetto nuget.org, il `releaseNotes` campo è limitato a 35.000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="13469-215">When uploading a package to nuget.org, the `releaseNotes` field is limited to 35,000 characters.</span></span>

#### <a name="copyright"></a><span data-ttu-id="13469-216">copyright</span><span class="sxs-lookup"><span data-stu-id="13469-216">copyright</span></span>
<span data-ttu-id="13469-217">*(1.5+)* Informazioni sul copyright per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-217">*(1.5+)* Copyright details for the package.</span></span>

<span data-ttu-id="13469-218">Quando si carica un pacchetto in nuget.org, `copyright` il campo è limitato a 4000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="13469-218">When uploading a package to nuget.org, the `copyright` field is limited to 4000 characters.</span></span>

#### <a name="language"></a><span data-ttu-id="13469-219">Linguaggio</span><span class="sxs-lookup"><span data-stu-id="13469-219">language</span></span>
<span data-ttu-id="13469-220">ID delle impostazioni locali per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-220">The locale ID for the package.</span></span> <span data-ttu-id="13469-221">Vedere [Creazione di pacchetti localizzati](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="13469-221">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="13469-222">tags</span><span class="sxs-lookup"><span data-stu-id="13469-222">tags</span></span>
<span data-ttu-id="13469-223">Elenco di tag e parole chiave delimitati da spazi che descrivono il pacchetto e facilitano l'individuabilità dei pacchetti tramite meccanismi di ricerca e filtro.</span><span class="sxs-lookup"><span data-stu-id="13469-223">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

<span data-ttu-id="13469-224">Quando si carica un pacchetto in nuget.org, il campo è limitato a `tags` 4000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="13469-224">When uploading a package to nuget.org, the `tags` field is limited to 4000 characters.</span></span>

#### <a name="serviceable"></a><span data-ttu-id="13469-225">serviceable</span><span class="sxs-lookup"><span data-stu-id="13469-225">serviceable</span></span> 
<span data-ttu-id="13469-226">*(3.3+)* Solo per uso interno in NuGet.</span><span class="sxs-lookup"><span data-stu-id="13469-226">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="13469-227">repository</span><span class="sxs-lookup"><span data-stu-id="13469-227">repository</span></span>
<span data-ttu-id="13469-228">Metadati del repository, costituiti da quattro attributi facoltativi: `type` e `url` *(4.0+)* e `branch` `commit` *(4.6+)*.</span><span class="sxs-lookup"><span data-stu-id="13469-228">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="13469-229">Questi attributi consentono di eseguire il mapping di al repository che lo ha compilato, con la possibilità di ottenere informazioni dettagliate come il nome del singolo ramo e/o eseguire il commit dell'hash SHA-1 che ha compilato `.nupkg` il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-229">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="13469-230">Deve trattarsi di un URL disponibile pubblicamente che può essere richiamato direttamente da un software di controllo della versione.</span><span class="sxs-lookup"><span data-stu-id="13469-230">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="13469-231">Non deve essere una pagina HTML perché è destinata al computer.</span><span class="sxs-lookup"><span data-stu-id="13469-231">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="13469-232">Per il collegamento alla pagina del progetto, usare `projectUrl` invece il campo .</span><span class="sxs-lookup"><span data-stu-id="13469-232">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="13469-233">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="13469-233">For example:</span></span>
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

<span data-ttu-id="13469-234">Quando si carica un pacchetto nuget.org, l'attributo è limitato a 100 caratteri e l'attributo è limitato a `type` `url` 4000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="13469-234">When uploading a package to nuget.org, the `type` attribute is limited to 100 characters and the `url` attribute is limited to 4000 characters.</span></span>

#### <a name="title"></a><span data-ttu-id="13469-235">title</span><span class="sxs-lookup"><span data-stu-id="13469-235">title</span></span>
<span data-ttu-id="13469-236">Titolo descrittivo del pacchetto che può essere usato in alcuni schermi dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="13469-236">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="13469-237">(nuget.org e il Gestione pacchetti in Visual Studio non mostrano il titolo)</span><span class="sxs-lookup"><span data-stu-id="13469-237">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

<span data-ttu-id="13469-238">Quando si carica un pacchetto nuget.org, il campo è limitato a 256 caratteri, ma non viene usato per `title` scopi di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="13469-238">When uploading a package to nuget.org, the `title` field is limited to 256 characters but is not used for any display purposes.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="13469-239">Elementi di raccolta</span><span class="sxs-lookup"><span data-stu-id="13469-239">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="13469-240">packageTypes</span><span class="sxs-lookup"><span data-stu-id="13469-240">packageTypes</span></span>
<span data-ttu-id="13469-241">*(3.5 +)* Raccolta di zero o più elementi `<packageType>` che specificano il tipo del pacchetto se diverso da un pacchetto di dipendenza tradizionale.</span><span class="sxs-lookup"><span data-stu-id="13469-241">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="13469-242">Ogni packageType include gli attributi di *name* e *version*.</span><span class="sxs-lookup"><span data-stu-id="13469-242">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="13469-243">Vedere [Setting a package type](../create-packages/set-package-type.md) (Impostazione di un tipo di pacchetto).</span><span class="sxs-lookup"><span data-stu-id="13469-243">See [Setting a package type](../create-packages/set-package-type.md).</span></span>

#### <a name="dependencies"></a><span data-ttu-id="13469-244">dipendenze</span><span class="sxs-lookup"><span data-stu-id="13469-244">dependencies</span></span>
<span data-ttu-id="13469-245">Raccolta di zero o più elementi `<dependency>` che specificano le dipendenze per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-245">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="13469-246">Ogni dipendenza include gli attributi *id*, *version*, *include* (3.x+) ed *exclude* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="13469-246">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="13469-247">Vedere [Dipendenze](#dependencies-element) di seguito.</span><span class="sxs-lookup"><span data-stu-id="13469-247">See [Dependencies](#dependencies-element) below.</span></span>

#### <a name="frameworkassemblies"></a><span data-ttu-id="13469-248">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="13469-248">frameworkAssemblies</span></span>
<span data-ttu-id="13469-249">*(1.2 +)* Raccolta di zero o più elementi `<frameworkAssembly>` che identificano i riferimenti ad assembly .NET Framework richiesti dal pacchetto. Ciò assicura che i riferimenti vengano aggiunti ai progetti che utilizzano il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-249">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="13469-250">Ogni frameworkAssembly include gli attributi *assemblyName* e *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="13469-250">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="13469-251">Vedere [Riferimenti agli assembly del framework](#specifying-framework-assembly-references-gac) più avanti.</span><span class="sxs-lookup"><span data-stu-id="13469-251">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>

#### <a name="references"></a><span data-ttu-id="13469-252">references</span><span class="sxs-lookup"><span data-stu-id="13469-252">references</span></span>
<span data-ttu-id="13469-253">*(1.5 +)* Raccolta di zero o più elementi `<reference>` per la denominazione degli assembly nella cartella `lib` del pacchetto, aggiunti come riferimenti al progetto.</span><span class="sxs-lookup"><span data-stu-id="13469-253">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="13469-254">Ogni riferimento include un attributo *file*.</span><span class="sxs-lookup"><span data-stu-id="13469-254">Each reference has a *file* attribute.</span></span> <span data-ttu-id="13469-255">`<references>` può anche contenere un elemento `<group>` con un attributo *targetFramework*, che contiene a sua volta elementi `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="13469-255">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="13469-256">Se omesso, vengono inclusi tutti i riferimenti in `lib`.</span><span class="sxs-lookup"><span data-stu-id="13469-256">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="13469-257">Vedere [Riferimenti espliciti agli assembly](#specifying-explicit-assembly-references) più avanti.</span><span class="sxs-lookup"><span data-stu-id="13469-257">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>

#### <a name="contentfiles"></a><span data-ttu-id="13469-258">contentFiles</span><span class="sxs-lookup"><span data-stu-id="13469-258">contentFiles</span></span>
<span data-ttu-id="13469-259">*(3.3 +)* Raccolta di elementi `<files>` che identificano i file di contenuto da includere nel progetto che utilizza il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-259">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="13469-260">Questi file sono specificati con un set di attributi che descrivono come devono essere usati all'interno del sistema del progetto.</span><span class="sxs-lookup"><span data-stu-id="13469-260">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="13469-261">Vedere [Inclusione di file di assembly](#specifying-files-to-include-in-the-package) più avanti.</span><span class="sxs-lookup"><span data-stu-id="13469-261">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>

#### <a name="files"></a><span data-ttu-id="13469-262">files</span><span class="sxs-lookup"><span data-stu-id="13469-262">files</span></span> 
<span data-ttu-id="13469-263">Il nodo può contenere un nodo come elemento di pari livello in e un elemento figlio in per specificare i file di assembly e di contenuto da `<package>` `<files>` includere nel `<metadata>` `<contentFiles>` `<metadata>` pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-263">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="13469-264">Vedere [Inclusione di file di assembly](#including-assembly-files) e [Inclusione di file di contenuto](#including-content-files) più avanti in questo argomento per ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="13469-264">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="13469-265">attributi dei metadati</span><span class="sxs-lookup"><span data-stu-id="13469-265">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="13469-266">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="13469-266">minClientVersion</span></span>
<span data-ttu-id="13469-267">Specifica la versione minima del client NuGet, imposta da nuget.exe e da Gestione pacchetti di Visual Studio, che può installare questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-267">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="13469-268">Questo attributo viene usato ogni volta che il pacchetto dipende da funzionalità specifiche del file `.nuspec` aggiunte in una particolare versione del client NuGet.</span><span class="sxs-lookup"><span data-stu-id="13469-268">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="13469-269">Ad esempio, un pacchetto che usa l'attributo `developmentDependency` deve specificare "2.8" per `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="13469-269">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="13469-270">Analogamente, un pacchetto che usa l'elemento `contentFiles` (vedere la sezione successiva) deve impostare `minClientVersion` su "3.3".</span><span class="sxs-lookup"><span data-stu-id="13469-270">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="13469-271">Si noti che poiché i client NuGet prima della versione 2.5 non riconoscono questo flag, essi rifiutano *sempre* di installare il pacchetto indipendentemente dal contenuto di `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="13469-271">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

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

## <a name="replacement-tokens"></a><span data-ttu-id="13469-272">Token di sostituzione</span><span class="sxs-lookup"><span data-stu-id="13469-272">Replacement tokens</span></span>

<span data-ttu-id="13469-273">Quando si crea [ `nuget pack` ](../reference/cli-reference/cli-ref-pack.md) un pacchetto, il comando sostituisce i token delimitati da $nel nodo del file con valori provenienti da un file di progetto o `.nuspec` `<metadata>` `pack` dall'opzione del `-properties` comando.</span><span class="sxs-lookup"><span data-stu-id="13469-273">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="13469-274">Nella riga di comando, i valori dei token vengono specificati con `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="13469-274">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="13469-275">Ad esempio, è possibile usare un token come `$owners$` e `$desc$` nel file `.nuspec` e specificare i valori al momento della creazione del pacchetto come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="13469-275">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="13469-276">Per usare valori da un progetto, specificare il token descritto nella tabella riportata di seguito (AssemblyInfo fa riferimento al file in `Properties`, ad esempio `AssemblyInfo.cs` o `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="13469-276">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="13469-277">Per usare questi token, eseguire `nuget pack` con il file di progetto anziché semplicemente il file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="13469-277">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="13469-278">Ad esempio, quando si usa il comando seguente, i token `$id$` e `$version$` in un file `.nuspec` vengono sostituiti con i valori `AssemblyName` e `AssemblyVersion` del progetto:</span><span class="sxs-lookup"><span data-stu-id="13469-278">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="13469-279">In genere, quando si dispone di un progetto, si crea inizialmente il file `.nuspec` con `nuget spec MyProject.csproj`, che include automaticamente alcuni di questi token standard.</span><span class="sxs-lookup"><span data-stu-id="13469-279">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="13469-280">Tuttavia, se un progetto non include i valori per elementi `.nuspec` obbligatori, `nuget pack` ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="13469-280">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="13469-281">Inoltre, se si modificano i valori del progetto, assicurarsi di ricompilare prima di creare il pacchetto. Questa operazione può essere eseguita facilmente con l'opzione `build` del comando pack.</span><span class="sxs-lookup"><span data-stu-id="13469-281">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="13469-282">Ad eccezione di `$configuration$`, i valori nel progetto vengono usati preferenzialmente rispetto a qualsiasi altro valore assegnato allo stesso token nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="13469-282">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="13469-283">Token</span><span class="sxs-lookup"><span data-stu-id="13469-283">Token</span></span> | <span data-ttu-id="13469-284">Origine del valore</span><span class="sxs-lookup"><span data-stu-id="13469-284">Value source</span></span> | <span data-ttu-id="13469-285">Valore</span><span class="sxs-lookup"><span data-stu-id="13469-285">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="13469-286">**$id$**</span><span class="sxs-lookup"><span data-stu-id="13469-286">**$id$**</span></span> | <span data-ttu-id="13469-287">File di progetto</span><span class="sxs-lookup"><span data-stu-id="13469-287">Project file</span></span> | <span data-ttu-id="13469-288">AssemblyName (titolo) dal file di progetto</span><span class="sxs-lookup"><span data-stu-id="13469-288">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="13469-289">**$version$**</span><span class="sxs-lookup"><span data-stu-id="13469-289">**$version$**</span></span> | <span data-ttu-id="13469-290">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="13469-290">AssemblyInfo</span></span> | <span data-ttu-id="13469-291">AssemblyInformationalVersion se presente, in caso contrario AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="13469-291">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="13469-292">**$author$**</span><span class="sxs-lookup"><span data-stu-id="13469-292">**$author$**</span></span> | <span data-ttu-id="13469-293">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="13469-293">AssemblyInfo</span></span> | <span data-ttu-id="13469-294">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="13469-294">AssemblyCompany</span></span> |
| <span data-ttu-id="13469-295">**$title$**</span><span class="sxs-lookup"><span data-stu-id="13469-295">**$title$**</span></span> | <span data-ttu-id="13469-296">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="13469-296">AssemblyInfo</span></span> | <span data-ttu-id="13469-297">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="13469-297">AssemblyTitle</span></span> |
| <span data-ttu-id="13469-298">**$description$**</span><span class="sxs-lookup"><span data-stu-id="13469-298">**$description$**</span></span> | <span data-ttu-id="13469-299">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="13469-299">AssemblyInfo</span></span> | <span data-ttu-id="13469-300">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="13469-300">AssemblyDescription</span></span> |
| <span data-ttu-id="13469-301">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="13469-301">**$copyright$**</span></span> | <span data-ttu-id="13469-302">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="13469-302">AssemblyInfo</span></span> | <span data-ttu-id="13469-303">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="13469-303">AssemblyCopyright</span></span> |
| <span data-ttu-id="13469-304">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="13469-304">**$configuration$**</span></span> | <span data-ttu-id="13469-305">DLL dell'assembly</span><span class="sxs-lookup"><span data-stu-id="13469-305">Assembly DLL</span></span> | <span data-ttu-id="13469-306">Configurazione usata per compilare l'assembly, con impostazione predefinita Debug.</span><span class="sxs-lookup"><span data-stu-id="13469-306">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="13469-307">Si noti che per creare un pacchetto con la configurazione Rilascio, è sempre necessario usare `-properties Configuration=Release` nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="13469-307">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="13469-308">I token possono essere usati anche per risolvere i percorsi quando si includono [file di assembly](#including-assembly-files) e [file di contenuto](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="13469-308">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="13469-309">I token hanno gli stessi nomi delle proprietà di MSBuild e ciò consente di selezionare i file da includere a seconda della configurazione di compilazione corrente.</span><span class="sxs-lookup"><span data-stu-id="13469-309">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="13469-310">Ad esempio, se si usano i token seguenti nel file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="13469-310">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="13469-311">E si compila un assembly il cui `AssemblyName` è `LoggingLibrary` con la configurazione `Release` in MSBuild, le righe risultanti nel file `.nuspec` nel pacchetto sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="13469-311">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="13469-312">Dependencies - elemento</span><span class="sxs-lookup"><span data-stu-id="13469-312">Dependencies element</span></span>

<span data-ttu-id="13469-313">L'elemento `<dependencies>` all'interno di `<metadata>` contiene qualsiasi numero di elementi `<dependency>` che identificano altri pacchetti da cui dipende il pacchetto di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="13469-313">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="13469-314">Gli attributi per ogni `<dependency>` sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="13469-314">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="13469-315">Attributo</span><span class="sxs-lookup"><span data-stu-id="13469-315">Attribute</span></span> | <span data-ttu-id="13469-316">Descrizione</span><span class="sxs-lookup"><span data-stu-id="13469-316">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="13469-317">(Obbligatorio) ID pacchetto della dipendenza, ad esempio "EntityFramework" e "NUnit", ovvero il nome di pacchetto che nuget.org mostra nella pagina di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-317">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="13469-318">(Obbligatorio) Intervallo di versioni accettabili come dipendenza.</span><span class="sxs-lookup"><span data-stu-id="13469-318">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="13469-319">Per la sintassi esatta, vedere [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="13469-319">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="13469-320">Le versioni mobili non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="13469-320">Floating versions are not supported.</span></span> |
| <span data-ttu-id="13469-321">include</span><span class="sxs-lookup"><span data-stu-id="13469-321">include</span></span> | <span data-ttu-id="13469-322">Elenco delimitato da virgole di tag di inclusione/esclusione (vedere di seguito) che indicano la dipendenza da includere nel pacchetto finale.</span><span class="sxs-lookup"><span data-stu-id="13469-322">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="13469-323">Il valore predefinito è `all`.</span><span class="sxs-lookup"><span data-stu-id="13469-323">The default value is `all`.</span></span> |
| <span data-ttu-id="13469-324">escludere</span><span class="sxs-lookup"><span data-stu-id="13469-324">exclude</span></span> | <span data-ttu-id="13469-325">Elenco delimitato da virgole di tag di inclusione/esclusione (vedere di seguito) che indicano la dipendenza da escludere nel pacchetto finale.</span><span class="sxs-lookup"><span data-stu-id="13469-325">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="13469-326">Il valore predefinito è `build,analyzers` che può essere sovrascritto.</span><span class="sxs-lookup"><span data-stu-id="13469-326">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="13469-327">Ma `content/ ContentFiles` sono anche implicitamente esclusi nel pacchetto finale che non può essere sovrascritto.</span><span class="sxs-lookup"><span data-stu-id="13469-327">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="13469-328">I tag specificati con `exclude` hanno la precedenza rispetto a quelli specificati con `include`.</span><span class="sxs-lookup"><span data-stu-id="13469-328">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="13469-329">Ad esempio, `include="runtime, compile" exclude="compile"` è identico a `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="13469-329">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

<span data-ttu-id="13469-330">Quando si carica un pacchetto nuget.org, l'attributo di ogni dipendenza è limitato a 128 caratteri e l'attributo è limitato a `id` `version` 256 caratteri.</span><span class="sxs-lookup"><span data-stu-id="13469-330">When uploading a package to nuget.org, each dependency's `id` attribute is limited to 128 characters and the `version` attribute is limited to 256 characters.</span></span>

| <span data-ttu-id="13469-331">Tag di inclusione/esclusione</span><span class="sxs-lookup"><span data-stu-id="13469-331">Include/Exclude tag</span></span> | <span data-ttu-id="13469-332">Cartelle di destinazione interessate</span><span class="sxs-lookup"><span data-stu-id="13469-332">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="13469-333">contentFiles</span><span class="sxs-lookup"><span data-stu-id="13469-333">contentFiles</span></span> | <span data-ttu-id="13469-334">Content</span><span class="sxs-lookup"><span data-stu-id="13469-334">Content</span></span> |
| <span data-ttu-id="13469-335">runtime</span><span class="sxs-lookup"><span data-stu-id="13469-335">runtime</span></span> | <span data-ttu-id="13469-336">Runtime, Resources e FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="13469-336">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="13469-337">compile</span><span class="sxs-lookup"><span data-stu-id="13469-337">compile</span></span> | <span data-ttu-id="13469-338">lib</span><span class="sxs-lookup"><span data-stu-id="13469-338">lib</span></span> |
| <span data-ttu-id="13469-339">build</span><span class="sxs-lookup"><span data-stu-id="13469-339">build</span></span> | <span data-ttu-id="13469-340">build (proprietà e destinazioni MSBuild)</span><span class="sxs-lookup"><span data-stu-id="13469-340">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="13469-341">nativi</span><span class="sxs-lookup"><span data-stu-id="13469-341">native</span></span> | <span data-ttu-id="13469-342">nativi</span><span class="sxs-lookup"><span data-stu-id="13469-342">native</span></span> |
| <span data-ttu-id="13469-343">Nessuno</span><span class="sxs-lookup"><span data-stu-id="13469-343">none</span></span> | <span data-ttu-id="13469-344">Nessuna cartella</span><span class="sxs-lookup"><span data-stu-id="13469-344">No folders</span></span> |
| <span data-ttu-id="13469-345">all</span><span class="sxs-lookup"><span data-stu-id="13469-345">all</span></span> | <span data-ttu-id="13469-346">Tutte le cartelle</span><span class="sxs-lookup"><span data-stu-id="13469-346">All folders</span></span> |

<span data-ttu-id="13469-347">Ad esempio, le righe seguenti indicano dipendenze da `PackageA` versione 1.1.0 o successive e da `PackageB` versione 1.x.</span><span class="sxs-lookup"><span data-stu-id="13469-347">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="13469-348">Le righe seguenti indicano dipendenze dagli stessi pacchetti, ma specificano di includere le cartelle `contentFiles` e `build` di `PackageA` e tutte le cartelle tranne `native` e `compile` di `PackageB`.</span><span class="sxs-lookup"><span data-stu-id="13469-348">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="13469-349">Quando si crea un oggetto da un progetto usando , le dipendenze presenti `.nuspec` in tale progetto non vengono incluse `nuget spec` automaticamente nel file `.nuspec` risultante.</span><span class="sxs-lookup"><span data-stu-id="13469-349">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="13469-350">Usare invece e ottenere il file con estensione `nuget pack myproject.csproj` *nuspec* dall'interno del file *con estensione nupkg* generato.</span><span class="sxs-lookup"><span data-stu-id="13469-350">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="13469-351">Questo *file con estensione nuspec* contiene le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="13469-351">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="13469-352">Gruppi di dipendenze</span><span class="sxs-lookup"><span data-stu-id="13469-352">Dependency groups</span></span>

<span data-ttu-id="13469-353">*Versione 2.0+*</span><span class="sxs-lookup"><span data-stu-id="13469-353">*Version 2.0+*</span></span>

<span data-ttu-id="13469-354">In alternativa a un unico elenco semplice, è possibile specificare le dipendenze in base al profilo del framework del progetto di destinazione usando elementi `<group>` all'interno di `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="13469-354">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="13469-355">Ogni gruppo ha un attributo denominato `targetFramework` e contiene zero o più elementi `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="13469-355">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="13469-356">Tali dipendenze vengono installate insieme quando il framework di destinazione è compatibile con il profilo di framework del progetto.</span><span class="sxs-lookup"><span data-stu-id="13469-356">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="13469-357">L'elemento `<group>` senza un attributo `targetFramework` viene usato come elenco predefinito o di fallback delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="13469-357">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="13469-358">Vedere [Framework di destinazione](../reference/target-frameworks.md) per gli identificatori di framework esatti.</span><span class="sxs-lookup"><span data-stu-id="13469-358">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="13469-359">Il formato di gruppo non può essere usato in combinazione con un elenco semplice.</span><span class="sxs-lookup"><span data-stu-id="13469-359">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="13469-360">Il formato del moniker del framework di destinazione [(TFM)](../reference/target-frameworks.md) usato nella cartella è diverso rispetto al `lib/ref` TFM usato in `dependency groups` .</span><span class="sxs-lookup"><span data-stu-id="13469-360">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="13469-361">Se i framework di destinazione dichiarati in e nella cartella del file non hanno corrispondenze esatte, il comando genererà l'avviso `dependencies group` `lib/ref` `.nuspec` `pack` [NuGet NU5128](../reference/errors-and-warnings/nu5128.md).</span><span class="sxs-lookup"><span data-stu-id="13469-361">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="13469-362">L'esempio seguente mostra variazioni diverse dell'elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="13469-362">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="13469-363">Riferimenti espliciti agli assembly</span><span class="sxs-lookup"><span data-stu-id="13469-363">Explicit assembly references</span></span>

<span data-ttu-id="13469-364">L'elemento viene usato dai progetti che usano per specificare in modo esplicito gli assembly a cui il `<references>` progetto di destinazione deve fare riferimento quando si utilizza il `packages.config` pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-364">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="13469-365">I riferimenti espliciti vengono generalmente usati per gli assembly solo della fase di progettazione.</span><span class="sxs-lookup"><span data-stu-id="13469-365">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="13469-366">Per altre informazioni, vedere la pagina sulla selezione degli assembly a [cui fanno riferimento](../create-packages/select-assemblies-referenced-by-projects.md) i progetti.</span><span class="sxs-lookup"><span data-stu-id="13469-366">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="13469-367">Ad esempio, l'elemento `<references>` seguente indica a NuGet di aggiungere riferimenti solo a `xunit.dll` e a `xunit.extensions.dll` anche se sono presenti altri assembly nel pacchetto:</span><span class="sxs-lookup"><span data-stu-id="13469-367">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="13469-368">Gruppi di riferimenti</span><span class="sxs-lookup"><span data-stu-id="13469-368">Reference groups</span></span>

<span data-ttu-id="13469-369">In alternativa a un unico elenco semplice, è possibile specificare i riferimenti in base al profilo del framework del progetto di destinazione usando elementi `<group>` all'interno di `<references>`.</span><span class="sxs-lookup"><span data-stu-id="13469-369">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="13469-370">Ogni gruppo ha un attributo denominato `targetFramework` e contiene zero o più elementi `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="13469-370">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="13469-371">Tali riferimenti vengono aggiunti a un progetto quando il framework di destinazione è compatibile con il profilo di framework del progetto.</span><span class="sxs-lookup"><span data-stu-id="13469-371">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="13469-372">L'elemento `<group>` senza un attributo `targetFramework` viene usato come elenco predefinito o di fallback dei riferimenti.</span><span class="sxs-lookup"><span data-stu-id="13469-372">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="13469-373">Vedere [Framework di destinazione](../reference/target-frameworks.md) per gli identificatori di framework esatti.</span><span class="sxs-lookup"><span data-stu-id="13469-373">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="13469-374">Il formato di gruppo non può essere usato in combinazione con un elenco semplice.</span><span class="sxs-lookup"><span data-stu-id="13469-374">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="13469-375">L'esempio seguente mostra variazioni diverse dell'elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="13469-375">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="13469-376">Riferimenti agli assembly del framework</span><span class="sxs-lookup"><span data-stu-id="13469-376">Framework assembly references</span></span>

<span data-ttu-id="13469-377">Gli assembly del framework sono quelli che fanno parte di .NET Framework e devono essere già presenti nella Global Assembly Cache (GAC) per qualsiasi computer.</span><span class="sxs-lookup"><span data-stu-id="13469-377">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="13469-378">Grazie all'identificazione di tali assembly all'interno dell'elemento `<frameworkAssemblies>`, un pacchetto può garantire che i riferimenti necessari vengano aggiunti a un progetto nel caso in cui il progetto non includa già tali riferimenti.</span><span class="sxs-lookup"><span data-stu-id="13469-378">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="13469-379">Tali assembly, ovviamente, non vengono inclusi in un pacchetto direttamente.</span><span class="sxs-lookup"><span data-stu-id="13469-379">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="13469-380">L'elemento `<frameworkAssemblies>` contiene zero o più elementi `<frameworkAssembly>`, ognuno dei quali specifica gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="13469-380">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="13469-381">Attributo</span><span class="sxs-lookup"><span data-stu-id="13469-381">Attribute</span></span> | <span data-ttu-id="13469-382">Descrizione</span><span class="sxs-lookup"><span data-stu-id="13469-382">Description</span></span> |
| --- | --- |
| <span data-ttu-id="13469-383">**Assemblyname**</span><span class="sxs-lookup"><span data-stu-id="13469-383">**assemblyName**</span></span> | <span data-ttu-id="13469-384">(Obbligatorio) Nome completo dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="13469-384">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="13469-385">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="13469-385">**targetFramework**</span></span> | <span data-ttu-id="13469-386">(Facoltativo) Specifica il framework di destinazione a cui si applica questo riferimento.</span><span class="sxs-lookup"><span data-stu-id="13469-386">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="13469-387">Se omesso, indica che il riferimento si applica a tutti i framework.</span><span class="sxs-lookup"><span data-stu-id="13469-387">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="13469-388">Vedere [Framework di destinazione](../reference/target-frameworks.md) per gli identificatori di framework esatti.</span><span class="sxs-lookup"><span data-stu-id="13469-388">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="13469-389">L'esempio seguente mostra un riferimento a `System.Net` per tutti i framework di destinazione e un riferimento a `System.ServiceModel` solo per .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="13469-389">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="13469-390">Inclusione di file di assembly</span><span class="sxs-lookup"><span data-stu-id="13469-390">Including assembly files</span></span>

<span data-ttu-id="13469-391">Se si seguono le convenzioni descritte in [Creazione di un pacchetto](../create-packages/creating-a-package.md), non è necessario specificare in modo esplicito un elenco di file nel file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="13469-391">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="13469-392">Il comando `nuget pack` rileva automaticamente i file necessari.</span><span class="sxs-lookup"><span data-stu-id="13469-392">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="13469-393">Quando un pacchetto viene installato in un progetto, NuGet aggiunge automaticamente i riferimenti agli assembly alle DLL del pacchetto, *escludendo* quelli denominati `.resources.dll` perché si presuppone che siano assembly satellite localizzati.</span><span class="sxs-lookup"><span data-stu-id="13469-393">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="13469-394">Per questo motivo, evitare di usare `.resources.dll` per i file che contengono invece codice essenziale per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-394">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="13469-395">Per evitare questo comportamento automatico e controllare in modo esplicito quali file vengono inclusi in un pacchetto, posizionare un elemento `<files>` come elemento figlio di `<package>` (ed elemento di pari livello di `<metadata>`), identificando ogni file con un elemento `<file>` separato.</span><span class="sxs-lookup"><span data-stu-id="13469-395">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="13469-396">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="13469-396">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="13469-397">Con NuGet 2.x e versioni precedenti e i progetti che usano `packages.config`, l'elemento `<files>` viene usato anche per includere file di contenuto non modificabili quando viene installato un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="13469-397">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="13469-398">Con NuGet 3.3 + e PackageReference per i progetti, viene invece usato l'elemento `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="13469-398">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="13469-399">Vedere [Inclusione di file di contenuto](#including-content-files) di seguito per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="13469-399">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="13469-400">Attributi dell'elemento file</span><span class="sxs-lookup"><span data-stu-id="13469-400">File element attributes</span></span>

<span data-ttu-id="13469-401">Ogni elemento `<file>` specifica gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="13469-401">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="13469-402">Attributo</span><span class="sxs-lookup"><span data-stu-id="13469-402">Attribute</span></span> | <span data-ttu-id="13469-403">Descrizione</span><span class="sxs-lookup"><span data-stu-id="13469-403">Description</span></span> |
| --- | --- |
| <span data-ttu-id="13469-404">**src**</span><span class="sxs-lookup"><span data-stu-id="13469-404">**src**</span></span> | <span data-ttu-id="13469-405">Percorso del file o dei file da includere, soggetto alle esclusioni specificate dall'attributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="13469-405">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="13469-406">Il percorso è relativo al file `.nuspec`, a meno che non venga specificato un percorso assoluto.</span><span class="sxs-lookup"><span data-stu-id="13469-406">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="13469-407">Il carattere jolly `*` è consentito e il carattere jolly doppio `**` implica una ricerca ricorsiva nelle cartelle.</span><span class="sxs-lookup"><span data-stu-id="13469-407">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="13469-408">**target**</span><span class="sxs-lookup"><span data-stu-id="13469-408">**target**</span></span> | <span data-ttu-id="13469-409">Percorso relativo della cartella all'interno del pacchetto in cui vengono collocati i file di origine, che deve iniziare con `lib`, `content`, `build` o `tools`.</span><span class="sxs-lookup"><span data-stu-id="13469-409">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="13469-410">Vedere [Creazione di un file .nuspec da una directory di lavoro basata su convenzioni](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="13469-410">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="13469-411">**escludere**</span><span class="sxs-lookup"><span data-stu-id="13469-411">**exclude**</span></span> | <span data-ttu-id="13469-412">Elenco delimitato da punti e virgola dei file o dei modelli di file da escludere dal percorso `src`.</span><span class="sxs-lookup"><span data-stu-id="13469-412">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="13469-413">Il carattere jolly `*` è consentito e il carattere jolly doppio `**` implica una ricerca ricorsiva nelle cartelle.</span><span class="sxs-lookup"><span data-stu-id="13469-413">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="13469-414">Esempio</span><span class="sxs-lookup"><span data-stu-id="13469-414">Examples</span></span>

<span data-ttu-id="13469-415">**Singolo assembly**</span><span class="sxs-lookup"><span data-stu-id="13469-415">**Single assembly**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="library.dll" target="lib" />

Packaged result:
    lib\library.dll
```

<span data-ttu-id="13469-416">**Singolo assembly specifico di un framework di destinazione**</span><span class="sxs-lookup"><span data-stu-id="13469-416">**Single assembly specific to a target framework**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="assemblies\net40\library.dll" target="lib\net40" />

Packaged result:
    lib\net40\library.dll
```

<span data-ttu-id="13469-417">**Set di DLL con un carattere jolly**</span><span class="sxs-lookup"><span data-stu-id="13469-417">**Set of DLLs using a wildcard**</span></span>

```
Source files:
    bin\release\libraryA.dll
    bin\release\libraryB.dll

.nuspec entry:
    <file src="bin\release\*.dll" target="lib" />

Packaged result:
    lib\libraryA.dll
    lib\libraryB.dll
```

<span data-ttu-id="13469-418">**DLL per framework diversi**</span><span class="sxs-lookup"><span data-stu-id="13469-418">**DLLs for different frameworks**</span></span>

```
Source files:
    lib\net40\library.dll
    lib\net20\library.dll

.nuspec entry (using ** recursive search):
    <file src="lib\**" target="lib" />

Packaged result:
    lib\net40\library.dll
    lib\net20\library.dll
```

<span data-ttu-id="13469-419">**Esclusione di file**</span><span class="sxs-lookup"><span data-stu-id="13469-419">**Excluding files**</span></span>

```
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
```

## <a name="including-content-files"></a><span data-ttu-id="13469-420">Inclusione di file di contenuto</span><span class="sxs-lookup"><span data-stu-id="13469-420">Including content files</span></span>

<span data-ttu-id="13469-421">I file di contenuto sono file non modificabili che un pacchetto deve includere in un progetto.</span><span class="sxs-lookup"><span data-stu-id="13469-421">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="13469-422">Essendo non modificabili, non sono progettati per essere modificati dal progetto che li utilizza.</span><span class="sxs-lookup"><span data-stu-id="13469-422">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="13469-423">Alcuni esempi di file di contenuto includono:</span><span class="sxs-lookup"><span data-stu-id="13469-423">Example content files include:</span></span>

- <span data-ttu-id="13469-424">Immagini incorporate come risorse</span><span class="sxs-lookup"><span data-stu-id="13469-424">Images that are embedded as resources</span></span>
- <span data-ttu-id="13469-425">File di origine già compilati</span><span class="sxs-lookup"><span data-stu-id="13469-425">Source files that are already compiled</span></span>
- <span data-ttu-id="13469-426">Script che devono essere inclusi con l'output di compilazione del progetto</span><span class="sxs-lookup"><span data-stu-id="13469-426">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="13469-427">File di configurazione per il pacchetto che devono essere inclusi nel progetto ma non richiedono modifiche specifiche del progetto</span><span class="sxs-lookup"><span data-stu-id="13469-427">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="13469-428">I file di contenuto vengono inclusi in un pacchetto con l'elemento `<files>`, specificando la cartella `content` nell'attributo `target`.</span><span class="sxs-lookup"><span data-stu-id="13469-428">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="13469-429">Questi file vengono tuttavia ignorati quando il pacchetto viene installato in un progetto usando PackageReference, che usa invece l'elemento `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="13469-429">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="13469-430">Per ottenere la massima compatibilità con i progetti in cui viene utilizzato, un pacchetto specifica idealmente i file di contenuto in entrambi gli elementi.</span><span class="sxs-lookup"><span data-stu-id="13469-430">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="13469-431">Uso dell'elemento files per i file di contenuto</span><span class="sxs-lookup"><span data-stu-id="13469-431">Using the files element for content files</span></span>

<span data-ttu-id="13469-432">Per i file di contenuto, usare semplicemente lo stesso formato usato per i file di assembly, ma specificare `content` come cartella di base nell'attributo `target`, come illustrato negli esempi seguenti.</span><span class="sxs-lookup"><span data-stu-id="13469-432">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="13469-433">**File di contenuto semplici**</span><span class="sxs-lookup"><span data-stu-id="13469-433">**Basic content files**</span></span>

```
Source files:
    css\mobile\style1.css
    css\mobile\style2.css

.nuspec entry:
    <file src="css\mobile\*.css" target="content\css\mobile" />

Packaged result:
    content\css\mobile\style1.css
    content\css\mobile\style2.css
```

<span data-ttu-id="13469-434">**File di contenuto con struttura di directory**</span><span class="sxs-lookup"><span data-stu-id="13469-434">**Content files with directory structure**</span></span>

```
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
```

<span data-ttu-id="13469-435">**File di contenuto specifico di un framework di destinazione**</span><span class="sxs-lookup"><span data-stu-id="13469-435">**Content file specific to a target framework**</span></span>

```
Source file:
    css\cool\style.css

.nuspec entry
    <file src="css\cool\style.css" target="Content" />

Packaged result:
    content\style.css
```

<span data-ttu-id="13469-436">**File di contenuto copiato in una cartella con un punto nel nome**</span><span class="sxs-lookup"><span data-stu-id="13469-436">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="13469-437">In questo caso, NuGet rileva che l'estensione in `target` non corrisponde all'estensione in `src`, quindi interpreta la parte del nome in `target` come cartella:</span><span class="sxs-lookup"><span data-stu-id="13469-437">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

```
Source file:
    images\picture.png

.nuspec entry:
    <file src="images\picture.png" target="Content\images\package.icons" />

Packaged result:
    content\images\package.icons\picture.png
```

<span data-ttu-id="13469-438">**File di contenuto senza estensione**</span><span class="sxs-lookup"><span data-stu-id="13469-438">**Content files without extensions**</span></span>

<span data-ttu-id="13469-439">Per includere i file senza estensione, usare i caratteri jolly `*` o `**`:</span><span class="sxs-lookup"><span data-stu-id="13469-439">To include files without an extension, use the `*` or `**` wildcards:</span></span>

```
Source file:
    flags\installed

.nuspec entry:
    <file src="flags\**" target="flags" />

Packaged result:
    flags\installed
```

<span data-ttu-id="13469-440">**File di contenuto con percorso completo e destinazione completa**</span><span class="sxs-lookup"><span data-stu-id="13469-440">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="13469-441">In questo caso, dato che le estensioni dei file di origine e di destinazione corrispondono, NuGet presuppone che la destinazione sia un nome di file e non una cartella:</span><span class="sxs-lookup"><span data-stu-id="13469-441">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

```
Source file:
    css\cool\style.css

.nuspec entry:
    <file src="css\cool\style.css" target="Content\css\cool" />
    or:
    <file src="css\cool\style.css" target="Content\css\cool\style.css" />

Packaged result:
    content\css\cool\style.css
```

<span data-ttu-id="13469-442">**Ridenominazione di un file di contenuto nel pacchetto**</span><span class="sxs-lookup"><span data-stu-id="13469-442">**Renaming a content file in the package**</span></span>

```
Source file:
    ie\css\style.css

.nuspec entry:
    <file src="ie\css\style.css" target="Content\css\ie.css" />

Packaged result:
    content\css\ie.css
```

<span data-ttu-id="13469-443">**Esclusione di file**</span><span class="sxs-lookup"><span data-stu-id="13469-443">**Excluding files**</span></span>

```
Source file:
    docs\*.txt (multiple files)

.nuspec entry:
    <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
    or
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

Packaged result:
    All .txt files from docs except admin.txt (first example)
    All .txt files from docs except admin.txt and log.txt (second example)
```

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="13469-444">Uso dell'elemento contentFiles per i file di contenuto</span><span class="sxs-lookup"><span data-stu-id="13469-444">Using the contentFiles element for content files</span></span>

<span data-ttu-id="13469-445">*NuGet 4.0 + con PackageReference*</span><span class="sxs-lookup"><span data-stu-id="13469-445">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="13469-446">Per impostazione predefinita, un pacchetto inserisce il contenuto in una cartella `contentFiles` (vedere di seguito) e `nuget pack` include tutti i file nella cartella usando gli attributi predefiniti.</span><span class="sxs-lookup"><span data-stu-id="13469-446">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="13469-447">In questo caso non è affatto necessario includere un nodo `contentFiles` nel file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="13469-447">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="13469-448">Per controllare quali file sono inclusi, l'elemento `<contentFiles>` specifica una raccolta di elementi `<files>` che identificano i file esatti inclusi.</span><span class="sxs-lookup"><span data-stu-id="13469-448">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="13469-449">Questi file sono specificati con un set di attributi che descrivono come devono essere usati all'interno del sistema del progetto:</span><span class="sxs-lookup"><span data-stu-id="13469-449">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="13469-450">Attributo</span><span class="sxs-lookup"><span data-stu-id="13469-450">Attribute</span></span> | <span data-ttu-id="13469-451">Descrizione</span><span class="sxs-lookup"><span data-stu-id="13469-451">Description</span></span> |
| --- | --- |
| <span data-ttu-id="13469-452">**Includono**</span><span class="sxs-lookup"><span data-stu-id="13469-452">**include**</span></span> | <span data-ttu-id="13469-453">(Obbligatorio) Percorso del file o dei file da includere, soggetto alle esclusioni specificate dall'attributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="13469-453">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="13469-454">Il percorso è relativo alla cartella, `contentFiles` a meno che non venga specificato un percorso assoluto.</span><span class="sxs-lookup"><span data-stu-id="13469-454">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="13469-455">Il carattere jolly `*` è consentito e il carattere jolly doppio `**` implica una ricerca ricorsiva nelle cartelle.</span><span class="sxs-lookup"><span data-stu-id="13469-455">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="13469-456">**escludere**</span><span class="sxs-lookup"><span data-stu-id="13469-456">**exclude**</span></span> | <span data-ttu-id="13469-457">Elenco delimitato da punti e virgola dei file o dei modelli di file da escludere dal percorso `src`.</span><span class="sxs-lookup"><span data-stu-id="13469-457">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="13469-458">Il carattere jolly `*` è consentito e il carattere jolly doppio `**` implica una ricerca ricorsiva nelle cartelle.</span><span class="sxs-lookup"><span data-stu-id="13469-458">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="13469-459">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="13469-459">**buildAction**</span></span> | <span data-ttu-id="13469-460">Azione di compilazione da assegnare all'elemento di contenuto per MSBuild, ad esempio `Content` , , , e così `None` `Embedded Resource` `Compile` via. Il valore predefinito è `Compile` .</span><span class="sxs-lookup"><span data-stu-id="13469-460">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="13469-461">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="13469-461">**copyToOutput**</span></span> | <span data-ttu-id="13469-462">Valore booleano che indica se copiare gli elementi di contenuto nella cartella di output di compilazione (o pubblicazione).</span><span class="sxs-lookup"><span data-stu-id="13469-462">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="13469-463">Il valore predefinito è false.</span><span class="sxs-lookup"><span data-stu-id="13469-463">The default is false.</span></span> |
| <span data-ttu-id="13469-464">**flatten**</span><span class="sxs-lookup"><span data-stu-id="13469-464">**flatten**</span></span> | <span data-ttu-id="13469-465">Valore booleano che indica se copiare gli elementi di contenuto di una singola cartella nell'output di compilazione (true) o se mantenere la struttura di cartelle nel pacchetto (false).</span><span class="sxs-lookup"><span data-stu-id="13469-465">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="13469-466">Questo flag funziona solo quando il flag copyToOutput è impostato su true.</span><span class="sxs-lookup"><span data-stu-id="13469-466">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="13469-467">Il valore predefinito è false.</span><span class="sxs-lookup"><span data-stu-id="13469-467">The default is false.</span></span> |

<span data-ttu-id="13469-468">Quando si installa un pacchetto, NuGet applica gli elementi figlio di `<contentFiles>` dall'alto verso il basso.</span><span class="sxs-lookup"><span data-stu-id="13469-468">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="13469-469">Se più voci corrispondono allo stesso file, vengono applicate tutte le voci.</span><span class="sxs-lookup"><span data-stu-id="13469-469">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="13469-470">La voce di livello superiore sostituisce le voci inferiori in presenza di un conflitto per lo stesso attributo.</span><span class="sxs-lookup"><span data-stu-id="13469-470">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="13469-471">Struttura delle cartelle del pacchetto</span><span class="sxs-lookup"><span data-stu-id="13469-471">Package folder structure</span></span>

<span data-ttu-id="13469-472">Il progetto del pacchetto deve strutturare il contenuto in base al modello seguente:</span><span class="sxs-lookup"><span data-stu-id="13469-472">The package project should structure content using the following pattern:</span></span>

```
/contentFiles/{codeLanguage}/{TxM}/{any?}
```

- <span data-ttu-id="13469-473">`codeLanguages` può essere `cs`, `vb`, `fs`, `any` o l'equivalente in caratteri minuscoli di uno specifico `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="13469-473">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="13469-474">`TxM` è qualsiasi moniker di framework di destinazione valido supportato da NuGet (vedere [Framework di destinazione](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="13469-474">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="13469-475">Qualsiasi struttura di cartelle può essere aggiunta alla fine di questa sintassi.</span><span class="sxs-lookup"><span data-stu-id="13469-475">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="13469-476">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="13469-476">For example:</span></span>

```
Language- and framework-agnostic:
    /contentFiles/any/any/config.xml

net45 content for all languages
    /contentFiles/any/net45/config.xml

C#-specific content for net45 and up
    /contentFiles/cs/net45/sample.cs
```

<span data-ttu-id="13469-477">Le cartelle vuote possono usare `.` per rifiutare esplicitamente di fornire contenuti per determinate combinazioni di linguaggio e TxM, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="13469-477">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

```
/contentFiles/vb/any/code.vb
/contentFiles/cs/any/.
```

#### <a name="example-contentfiles-section"></a><span data-ttu-id="13469-478">Sezione di esempio contentFiles</span><span class="sxs-lookup"><span data-stu-id="13469-478">Example contentFiles section</span></span>

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

## <a name="framework-reference-groups"></a><span data-ttu-id="13469-479">Gruppi di riferimento del framework</span><span class="sxs-lookup"><span data-stu-id="13469-479">Framework reference groups</span></span>

<span data-ttu-id="13469-480">*Versione 5.1+ wih Solo PackageReference*</span><span class="sxs-lookup"><span data-stu-id="13469-480">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="13469-481">I riferimenti al framework sono un concetto di .NET Core che rappresenta framework condivisi, ad esempio WPF o Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="13469-481">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="13469-482">Specificando un framework condiviso, il pacchetto garantisce che tutte le relative dipendenze del framework siano incluse nel progetto di riferimento.</span><span class="sxs-lookup"><span data-stu-id="13469-482">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="13469-483">Ogni `<group>` elemento richiede un attributo e zero o più `targetFramework` `<frameworkReference>` elementi.</span><span class="sxs-lookup"><span data-stu-id="13469-483">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="13469-484">L'esempio seguente illustra un nuspec generato per un progetto WPF .NET Core.</span><span class="sxs-lookup"><span data-stu-id="13469-484">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="13469-485">Si noti che la creazione manuale di nuspec contenenti riferimenti al framework non è consigliata.</span><span class="sxs-lookup"><span data-stu-id="13469-485">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="13469-486">Prendere in considerazione [l'uso del](msbuild-targets.md) pacchetto di destinazioni, che le dedurrà automaticamente dal progetto.</span><span class="sxs-lookup"><span data-stu-id="13469-486">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="13469-487">File nuspec di esempio</span><span class="sxs-lookup"><span data-stu-id="13469-487">Example nuspec files</span></span>

<span data-ttu-id="13469-488">**File `.nuspec` semplice che non specifica dipendenze o file**</span><span class="sxs-lookup"><span data-stu-id="13469-488">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="13469-489">**File `.nuspec` con dipendenze**</span><span class="sxs-lookup"><span data-stu-id="13469-489">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="13469-490">**File `.nuspec` con file**</span><span class="sxs-lookup"><span data-stu-id="13469-490">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="13469-491">**File `.nuspec` con assembly di framework**</span><span class="sxs-lookup"><span data-stu-id="13469-491">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="13469-492">In questo esempio vengono installati i componenti seguenti per destinazioni di progetto specifiche:</span><span class="sxs-lookup"><span data-stu-id="13469-492">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="13469-493">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="13469-493">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="13469-494">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="13469-494">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="13469-495">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="13469-495">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="13469-496">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="13469-496">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
