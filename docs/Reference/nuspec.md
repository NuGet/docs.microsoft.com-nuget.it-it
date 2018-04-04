---
title: Informazioni di riferimento sul file .nuspec per NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/29/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Il file. nuspec contiene i metadati del pacchetto usati per la compilazione e per fornire informazioni ai consumer del pacchetto.
keywords: informazioni di riferimento su nuspec, metadati dei pacchetti NuGet, manifesto dei pacchetti NuGet, schema di nuspec
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 086826b47402bb5e7066c7a10b1e2ff246fd58ea
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/03/2018
---
# <a name="nuspec-reference"></a><span data-ttu-id="cd85e-104">Informazioni di riferimento sul file .nuspec</span><span class="sxs-lookup"><span data-stu-id="cd85e-104">.nuspec reference</span></span>

<span data-ttu-id="cd85e-105">Un file `.nuspec` è un manifesto XML che contiene i metadati del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-105">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="cd85e-106">Questo manifesto viene usato per compilare il pacchetto e per fornire informazioni ai consumer.</span><span class="sxs-lookup"><span data-stu-id="cd85e-106">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="cd85e-107">Il manifesto viene sempre incluso in un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-107">The manifest is always included in a package.</span></span>

<span data-ttu-id="cd85e-108">In questo argomento</span><span class="sxs-lookup"><span data-stu-id="cd85e-108">In this topic:</span></span>

- [<span data-ttu-id="cd85e-109">Formato generale e schema</span><span class="sxs-lookup"><span data-stu-id="cd85e-109">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="cd85e-110">[Token di sostituzione](#replacement-tokens) (usati con un progetto di Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="cd85e-110">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="cd85e-111">Dipendenze</span><span class="sxs-lookup"><span data-stu-id="cd85e-111">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="cd85e-112">Riferimenti espliciti agli assembly</span><span class="sxs-lookup"><span data-stu-id="cd85e-112">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="cd85e-113">Riferimenti agli assembly del framework</span><span class="sxs-lookup"><span data-stu-id="cd85e-113">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="cd85e-114">Inclusione di file di assembly</span><span class="sxs-lookup"><span data-stu-id="cd85e-114">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="cd85e-115">Inclusione di file di contenuto</span><span class="sxs-lookup"><span data-stu-id="cd85e-115">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="cd85e-116">Esempi</span><span class="sxs-lookup"><span data-stu-id="cd85e-116">Examples</span></span>](#examples)

## <a name="general-form-and-schema"></a><span data-ttu-id="cd85e-117">Formato generale e schema</span><span class="sxs-lookup"><span data-stu-id="cd85e-117">General form and schema</span></span>

<span data-ttu-id="cd85e-118">Il file dello schema di `nuspec.xsd` corrente è disponibile nel [repository GitHub di NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="cd85e-118">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="cd85e-119">All'interno di questo schema, un file `.nuspec` ha il formato generale seguente:</span><span class="sxs-lookup"><span data-stu-id="cd85e-119">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="cd85e-120">Per una rappresentazione visiva chiara dello schema, aprire il file di schema in Visual Studio in modalità progettazione e fare clic sul collegamento **XML Schema Explorer**.</span><span class="sxs-lookup"><span data-stu-id="cd85e-120">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="cd85e-121">In alternativa, aprire il file come codice, fare clic con il pulsante destro del mouse nell'editor e scegliere **Mostra in XML Schema Explorer**.</span><span class="sxs-lookup"><span data-stu-id="cd85e-121">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="cd85e-122">In entrambi i casi si ottiene una visualizzazione simile alla seguente (quando è per la maggior parte espansa):</span><span class="sxs-lookup"><span data-stu-id="cd85e-122">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio Schema Explorer con nuspec.xsd aperto](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a><span data-ttu-id="cd85e-124">Attributi dei metadati</span><span class="sxs-lookup"><span data-stu-id="cd85e-124">Metadata attributes</span></span>

<span data-ttu-id="cd85e-125">L'elemento `<metadata>` supporta gli attributi descritti nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="cd85e-125">The `<metadata>` element supports the attributes described in the following table.</span></span>

| <span data-ttu-id="cd85e-126">Attributo</span><span class="sxs-lookup"><span data-stu-id="cd85e-126">Attribute</span></span> | <span data-ttu-id="cd85e-127">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="cd85e-127">Required</span></span> | <span data-ttu-id="cd85e-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cd85e-128">Description</span></span> |
| --- | --- | --- | 
| <span data-ttu-id="cd85e-129">**minClientVersion**</span><span class="sxs-lookup"><span data-stu-id="cd85e-129">**minClientVersion**</span></span> | <span data-ttu-id="cd85e-130">No</span><span class="sxs-lookup"><span data-stu-id="cd85e-130">No</span></span> | <span data-ttu-id="cd85e-131">Specifica la versione minima del client NuGet, imposta da nuget.exe e da Gestione pacchetti di Visual Studio, che può installare questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-131">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="cd85e-132">Questo attributo viene usato ogni volta che il pacchetto dipende da funzionalità specifiche del file `.nuspec` aggiunte in una particolare versione del client NuGet.</span><span class="sxs-lookup"><span data-stu-id="cd85e-132">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="cd85e-133">Ad esempio, un pacchetto che usa l'attributo `developmentDependency` deve specificare "2.8" per `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-133">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="cd85e-134">Analogamente, un pacchetto che usa l'elemento `contentFiles` (vedere la sezione successiva) deve impostare `minClientVersion` su "3.3".</span><span class="sxs-lookup"><span data-stu-id="cd85e-134">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="cd85e-135">Si noti che poiché i client NuGet prima della versione 2.5 non riconoscono questo flag, essi rifiutano *sempre* di installare il pacchetto indipendentemente dal contenuto di `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-135">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span> |

### <a name="required-metadata-elements"></a><span data-ttu-id="cd85e-136">Elementi dei metadati obbligatori</span><span class="sxs-lookup"><span data-stu-id="cd85e-136">Required metadata elements</span></span>

<span data-ttu-id="cd85e-137">Anche se gli elementi seguenti sono i requisiti minimi per un pacchetto, è consigliabile aggiungere gli [elementi dei metadati facoltativi](#optional-metadata-elements) per migliorare l'esperienza complessiva degli sviluppatori con il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-137">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span>

<span data-ttu-id="cd85e-138">Questi elementi devono essere visualizzati all'interno di un elemento `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-138">These elements must appear within a `<metadata>` element.</span></span>

| <span data-ttu-id="cd85e-139">Elemento</span><span class="sxs-lookup"><span data-stu-id="cd85e-139">Element</span></span> | <span data-ttu-id="cd85e-140">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cd85e-140">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cd85e-141">**ID**</span><span class="sxs-lookup"><span data-stu-id="cd85e-141">**id**</span></span> | <span data-ttu-id="cd85e-142">Identificatore del pacchetto senza distinzione tra maiuscole e minuscole che deve essere univoco in nuget.org o in qualsiasi raccolta in cui risiede il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-142">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="cd85e-143">L'ID non può contenere spazi o caratteri non validi per un URL e in genere segue le regole dello spazio dei nomi .NET.</span><span class="sxs-lookup"><span data-stu-id="cd85e-143">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="cd85e-144">Vedere [Choosing a unique package identifier and setting the version number](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) (Scelta di un identificatore univoco del pacchetto e impostazione del numero di versione) per altre indicazioni.</span><span class="sxs-lookup"><span data-stu-id="cd85e-144">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
| <span data-ttu-id="cd85e-145">**version**</span><span class="sxs-lookup"><span data-stu-id="cd85e-145">**version**</span></span> | <span data-ttu-id="cd85e-146">La versione del pacchetto secondo il criterio *principale.secondaria.patch*.</span><span class="sxs-lookup"><span data-stu-id="cd85e-146">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="cd85e-147">I numeri di versione possono includere un suffisso di versione non definitiva, come descritto in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="cd85e-147">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> |
| <span data-ttu-id="cd85e-148">**description**</span><span class="sxs-lookup"><span data-stu-id="cd85e-148">**description**</span></span> | <span data-ttu-id="cd85e-149">Descrizione lunga del pacchetto per la visualizzazione dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="cd85e-149">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="cd85e-150">**authors**</span><span class="sxs-lookup"><span data-stu-id="cd85e-150">**authors**</span></span> | <span data-ttu-id="cd85e-151">Elenco con valori delimitati da virgola di autori di pacchetti, corrispondenti ai nomi di profili in nuget.org. Questi, visualizzati nella raccolta NuGet in nuget.org, vengono usati per creare riferimenti incrociati ai pacchetti dello stesso autore.</span><span class="sxs-lookup"><span data-stu-id="cd85e-151">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |

### <a name="optional-metadata-elements"></a><span data-ttu-id="cd85e-152">Elementi dei metadati facoltativi</span><span class="sxs-lookup"><span data-stu-id="cd85e-152">Optional metadata elements</span></span>

<span data-ttu-id="cd85e-153">Questi elementi possono essere visualizzati all'interno di un elemento `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-153">These elements may appear within a `<metadata>` element.</span></span>

#### <a name="single-elements"></a><span data-ttu-id="cd85e-154">Singoli elementi</span><span class="sxs-lookup"><span data-stu-id="cd85e-154">Single elements</span></span>

| <span data-ttu-id="cd85e-155">Elemento</span><span class="sxs-lookup"><span data-stu-id="cd85e-155">Element</span></span> | <span data-ttu-id="cd85e-156">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cd85e-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cd85e-157">**title**</span><span class="sxs-lookup"><span data-stu-id="cd85e-157">**title**</span></span> | <span data-ttu-id="cd85e-158">Titolo del pacchetto facilmente comprensibile per l'utente, usato di solito per la visualizzazione dell'interfaccia utente, ad esempio in nuget.org e in Gestione pacchetti in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cd85e-158">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="cd85e-159">Se non specificato, viene usato l'ID del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-159">If not specified, the package ID is used.</span></span> |
| <span data-ttu-id="cd85e-160">**owners**</span><span class="sxs-lookup"><span data-stu-id="cd85e-160">**owners**</span></span> | <span data-ttu-id="cd85e-161">Elenco con valori delimitati da virgola di autori di pacchetti, corrispondenti ai nomi di profili in nuget.org. Si tratta spesso dello stesso elenco in `authors` e viene ignorato durante il caricamento del pacchetto in nuget.org. Vedere [Gestione dei proprietari dei pacchetti in nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="cd85e-161">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> |
| <span data-ttu-id="cd85e-162">**projectUrl**</span><span class="sxs-lookup"><span data-stu-id="cd85e-162">**projectUrl**</span></span> | <span data-ttu-id="cd85e-163">URL della pagina iniziale del pacchetto, spesso visualizzato nell'interfaccia utente e in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="cd85e-163">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="cd85e-164">**licenseUrl**</span><span class="sxs-lookup"><span data-stu-id="cd85e-164">**licenseUrl**</span></span> | <span data-ttu-id="cd85e-165">URL della licenza del pacchetto, spesso visualizzato nell'interfaccia utente e in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="cd85e-165">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="cd85e-166">**iconUrl**</span><span class="sxs-lookup"><span data-stu-id="cd85e-166">**iconUrl**</span></span> | <span data-ttu-id="cd85e-167">URL di un'immagine 64x64 con sfondo trasparente da usare come icona per il pacchetto nella visualizzazione dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="cd85e-167">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="cd85e-168">Assicurarsi che questo elemento contenga l'*URL diretto dell'immagine* e non l'URL di una pagina Web contenente l'immagine.</span><span class="sxs-lookup"><span data-stu-id="cd85e-168">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="cd85e-169">Ad esempio, per utilizzare un'immagine da GitHub, utilizzare il file non elaborato URL  *https://github.com/ \<username\>/\<repository\>/raw/\<ramo\> / \<logo.png\>*.</span><span class="sxs-lookup"><span data-stu-id="cd85e-169">For example, to use an image from GitHub, use the raw file URL like *https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\>*.</span></span> |
| <span data-ttu-id="cd85e-170">**requireLicenseAcceptance**</span><span class="sxs-lookup"><span data-stu-id="cd85e-170">**requireLicenseAcceptance**</span></span> | <span data-ttu-id="cd85e-171">Valore booleano che specifica se il client deve richiedere al consumer di accettare la licenza del pacchetto prima di installarlo.</span><span class="sxs-lookup"><span data-stu-id="cd85e-171">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| <span data-ttu-id="cd85e-172">**developmentDependency**</span><span class="sxs-lookup"><span data-stu-id="cd85e-172">**developmentDependency**</span></span> | <span data-ttu-id="cd85e-173">*(2.8 +)*  Valore booleano che specifica se il pacchetto deve essere contrassegnato come dipendenza solo per lo sviluppo, in modo che il pacchetto non possa essere incluso come dipendenza in altri pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cd85e-173">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> |
| <span data-ttu-id="cd85e-174">**summary**</span><span class="sxs-lookup"><span data-stu-id="cd85e-174">**summary**</span></span> | <span data-ttu-id="cd85e-175">Descrizione breve del pacchetto per la visualizzazione dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="cd85e-175">A short description of the package for UI display.</span></span> <span data-ttu-id="cd85e-176">Se omesso, viene usata una versione troncata di `description`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-176">If omitted, a truncated version of `description` is used.</span></span> |
| <span data-ttu-id="cd85e-177">**releaseNotes**</span><span class="sxs-lookup"><span data-stu-id="cd85e-177">**releaseNotes**</span></span> | <span data-ttu-id="cd85e-178">*(1.5+)* Descrizione delle modifiche apportate in questa versione del pacchetto, spesso usata nell'interfaccia utente, come la scheda **Aggiornamenti** di Gestione pacchetti di Visual Studio, in sostituzione della descrizione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-178">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span> |
| <span data-ttu-id="cd85e-179">**copyright**</span><span class="sxs-lookup"><span data-stu-id="cd85e-179">**copyright**</span></span> | <span data-ttu-id="cd85e-180">*(1.5+)* Informazioni sul copyright per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-180">*(1.5+)* Copyright details for the package.</span></span> |
| <span data-ttu-id="cd85e-181">**linguaggio**</span><span class="sxs-lookup"><span data-stu-id="cd85e-181">**language**</span></span> | <span data-ttu-id="cd85e-182">ID delle impostazioni locali per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-182">The locale ID for the package.</span></span> <span data-ttu-id="cd85e-183">Vedere [Creazione di pacchetti localizzati](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="cd85e-183">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span> |
| <span data-ttu-id="cd85e-184">**tags**</span><span class="sxs-lookup"><span data-stu-id="cd85e-184">**tags**</span></span> | <span data-ttu-id="cd85e-185">Elenco di tag e parole chiave delimitati da spazi che descrivono il pacchetto e facilitano l'individuabilità dei pacchetti tramite meccanismi di ricerca e filtro.</span><span class="sxs-lookup"><span data-stu-id="cd85e-185">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> |
| <span data-ttu-id="cd85e-186">**serviceable**</span><span class="sxs-lookup"><span data-stu-id="cd85e-186">**serviceable**</span></span> | <span data-ttu-id="cd85e-187">*(3.3+)* Solo per uso interno in NuGet.</span><span class="sxs-lookup"><span data-stu-id="cd85e-187">*(3.3+)* For internal NuGet use only.</span></span> |

#### <a name="collection-elements"></a><span data-ttu-id="cd85e-188">Elementi di raccolta</span><span class="sxs-lookup"><span data-stu-id="cd85e-188">Collection elements</span></span>

| <span data-ttu-id="cd85e-189">Elemento</span><span class="sxs-lookup"><span data-stu-id="cd85e-189">Element</span></span> | <span data-ttu-id="cd85e-190">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cd85e-190">Description</span></span> |
| --- | --- |
<span data-ttu-id="cd85e-191">**packageTypes**</span><span class="sxs-lookup"><span data-stu-id="cd85e-191">**packageTypes**</span></span> | <span data-ttu-id="cd85e-192">*(3.5 +)* Raccolta di zero o più elementi `<packageType>` che specificano il tipo del pacchetto se diverso da un pacchetto di dipendenza tradizionale.</span><span class="sxs-lookup"><span data-stu-id="cd85e-192">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="cd85e-193">Ogni packageType include gli attributi di *name* e *version*.</span><span class="sxs-lookup"><span data-stu-id="cd85e-193">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="cd85e-194">Vedere [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type) (Impostazione di un tipo di pacchetto).</span><span class="sxs-lookup"><span data-stu-id="cd85e-194">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span> |
| <span data-ttu-id="cd85e-195">**dependencies**</span><span class="sxs-lookup"><span data-stu-id="cd85e-195">**dependencies**</span></span> | <span data-ttu-id="cd85e-196">Raccolta di zero o più elementi `<dependency>` che specificano le dipendenze per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-196">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="cd85e-197">Ogni dipendenza include gli attributi *id*, *version*, *include* (3.x+) ed *exclude* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="cd85e-197">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="cd85e-198">Vedere [Dipendenze](#dependencies) di seguito.</span><span class="sxs-lookup"><span data-stu-id="cd85e-198">See [Dependencies](#dependencies) below.</span></span> |
| <span data-ttu-id="cd85e-199">**frameworkAssemblies**</span><span class="sxs-lookup"><span data-stu-id="cd85e-199">**frameworkAssemblies**</span></span> | <span data-ttu-id="cd85e-200">*(1.2 +)* Raccolta di zero o più elementi `<frameworkAssembly>` che identificano i riferimenti ad assembly .NET Framework richiesti dal pacchetto. Ciò assicura che i riferimenti vengano aggiunti ai progetti che utilizzano il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-200">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="cd85e-201">Ogni frameworkAssembly include gli attributi *assemblyName* e *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="cd85e-201">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="cd85e-202">Vedere [Riferimenti agli assembly del framework](#specifying-framework-assembly-references-gac) più avanti.</span><span class="sxs-lookup"><span data-stu-id="cd85e-202">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
| <span data-ttu-id="cd85e-203">**references**</span><span class="sxs-lookup"><span data-stu-id="cd85e-203">**references**</span></span> | <span data-ttu-id="cd85e-204">*(1.5 +)* Raccolta di zero o più elementi `<reference>` per la denominazione degli assembly nella cartella `lib` del pacchetto, aggiunti come riferimenti al progetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-204">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="cd85e-205">Ogni riferimento include un attributo *file*.</span><span class="sxs-lookup"><span data-stu-id="cd85e-205">Each reference has a *file* attribute.</span></span> <span data-ttu-id="cd85e-206">`<references>` può anche contenere un elemento `<group>` con un attributo *targetFramework*, che contiene a sua volta elementi `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-206">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="cd85e-207">Se omesso, vengono inclusi tutti i riferimenti in `lib`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-207">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="cd85e-208">Vedere [Riferimenti espliciti agli assembly](#specifying-explicit-assembly-references) più avanti.</span><span class="sxs-lookup"><span data-stu-id="cd85e-208">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span> |
| <span data-ttu-id="cd85e-209">**contentFiles**</span><span class="sxs-lookup"><span data-stu-id="cd85e-209">**contentFiles**</span></span> | <span data-ttu-id="cd85e-210">*(3.3 +)* Raccolta di elementi `<files>` che identificano i file di contenuto da includere nel progetto che utilizza il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-210">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="cd85e-211">Questi file sono specificati con un set di attributi che descrivono come devono essere usati all'interno del sistema del progetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-211">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="cd85e-212">Vedere [Inclusione di file di assembly](#specifying-files-to-include-in-the-package) più avanti.</span><span class="sxs-lookup"><span data-stu-id="cd85e-212">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span> |

### <a name="files-element"></a><span data-ttu-id="cd85e-213">Files (elemento)</span><span class="sxs-lookup"><span data-stu-id="cd85e-213">Files element</span></span>

<span data-ttu-id="cd85e-214">Il nodo `<package>` può contenere un nodo `<files>` come elemento di pari livello di `<metadata>` e/o un elemento `<contentFiles>` in `<metadata>` per specificare quali file di assembly e di contenuto includere nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-214">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="cd85e-215">Vedere [Inclusione di file di assembly](#including-assembly-files) e [Inclusione di file di contenuto](#including-content-files) più avanti in questo argomento per ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="cd85e-215">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="cd85e-216">Token di sostituzione</span><span class="sxs-lookup"><span data-stu-id="cd85e-216">Replacement tokens</span></span>

<span data-ttu-id="cd85e-217">Quando si crea un pacchetto, il [comando `nuget pack`](../tools/cli-ref-pack.md) sostituisce i token delimitati da $ nel nodo `<metadata>` del file `.nuspec` con valori provenienti da un file di progetto o dall'opzione `-properties` del comando `pack`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-217">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="cd85e-218">Nella riga di comando, i valori dei token vengono specificati con `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-218">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="cd85e-219">Ad esempio, è possibile usare un token come `$owners$` e `$desc$` nel file `.nuspec` e specificare i valori al momento della creazione del pacchetto come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="cd85e-219">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="cd85e-220">Per usare valori da un progetto, specificare il token descritto nella tabella riportata di seguito (AssemblyInfo fa riferimento al file in `Properties`, ad esempio `AssemblyInfo.cs` o `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="cd85e-220">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="cd85e-221">Per usare questi token, eseguire `nuget pack` con il file di progetto anziché semplicemente il file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-221">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="cd85e-222">Ad esempio, quando si usa il comando seguente, i token `$id$` e `$version$` in un file `.nuspec` vengono sostituiti con i valori `AssemblyName` e `AssemblyVersion` del progetto:</span><span class="sxs-lookup"><span data-stu-id="cd85e-222">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="cd85e-223">In genere, quando si dispone di un progetto, si crea inizialmente il file `.nuspec` con `nuget spec MyProject.csproj`, che include automaticamente alcuni di questi token standard.</span><span class="sxs-lookup"><span data-stu-id="cd85e-223">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="cd85e-224">Tuttavia, se un progetto non include i valori per elementi `.nuspec` obbligatori, `nuget pack` ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="cd85e-224">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="cd85e-225">Inoltre, se si modificano i valori del progetto, assicurarsi di ricompilare prima di creare il pacchetto. Questa operazione può essere eseguita facilmente con l'opzione `build` del comando pack.</span><span class="sxs-lookup"><span data-stu-id="cd85e-225">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="cd85e-226">Ad eccezione di `$configuration$`, i valori nel progetto vengono usati preferenzialmente rispetto a qualsiasi altro valore assegnato allo stesso token nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="cd85e-226">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="cd85e-227">Token</span><span class="sxs-lookup"><span data-stu-id="cd85e-227">Token</span></span> | <span data-ttu-id="cd85e-228">Origine del valore</span><span class="sxs-lookup"><span data-stu-id="cd85e-228">Value source</span></span> | <span data-ttu-id="cd85e-229">Valore</span><span class="sxs-lookup"><span data-stu-id="cd85e-229">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="cd85e-230">**$id$**</span><span class="sxs-lookup"><span data-stu-id="cd85e-230">**$id$**</span></span> | <span data-ttu-id="cd85e-231">File di progetto</span><span class="sxs-lookup"><span data-stu-id="cd85e-231">Project file</span></span> | <span data-ttu-id="cd85e-232">AssemblyName (titolo) dal file di progetto</span><span class="sxs-lookup"><span data-stu-id="cd85e-232">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="cd85e-233">**$version$**</span><span class="sxs-lookup"><span data-stu-id="cd85e-233">**$version$**</span></span> | <span data-ttu-id="cd85e-234">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="cd85e-234">AssemblyInfo</span></span> | <span data-ttu-id="cd85e-235">AssemblyInformationalVersion se presente, in caso contrario AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="cd85e-235">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="cd85e-236">**$author$**</span><span class="sxs-lookup"><span data-stu-id="cd85e-236">**$author$**</span></span> | <span data-ttu-id="cd85e-237">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="cd85e-237">AssemblyInfo</span></span> | <span data-ttu-id="cd85e-238">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="cd85e-238">AssemblyCompany</span></span> |
| <span data-ttu-id="cd85e-239">**$ $title**</span><span class="sxs-lookup"><span data-stu-id="cd85e-239">**$title$**</span></span> | <span data-ttu-id="cd85e-240">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="cd85e-240">AssemblyInfo</span></span> | <span data-ttu-id="cd85e-241">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="cd85e-241">AssemblyTitle</span></span> |
| <span data-ttu-id="cd85e-242">**$description$**</span><span class="sxs-lookup"><span data-stu-id="cd85e-242">**$description$**</span></span> | <span data-ttu-id="cd85e-243">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="cd85e-243">AssemblyInfo</span></span> | <span data-ttu-id="cd85e-244">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="cd85e-244">AssemblyDescription</span></span> |
| <span data-ttu-id="cd85e-245">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="cd85e-245">**$copyright$**</span></span> | <span data-ttu-id="cd85e-246">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="cd85e-246">AssemblyInfo</span></span> | <span data-ttu-id="cd85e-247">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="cd85e-247">AssemblyCopyright</span></span> |
| <span data-ttu-id="cd85e-248">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="cd85e-248">**$configuration$**</span></span> | <span data-ttu-id="cd85e-249">DLL dell'assembly</span><span class="sxs-lookup"><span data-stu-id="cd85e-249">Assembly DLL</span></span> | <span data-ttu-id="cd85e-250">Configurazione usata per compilare l'assembly, con impostazione predefinita Debug.</span><span class="sxs-lookup"><span data-stu-id="cd85e-250">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="cd85e-251">Si noti che per creare un pacchetto con la configurazione Rilascio, è sempre necessario usare `-properties Configuration=Release` nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="cd85e-251">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="cd85e-252">I token possono essere usati anche per risolvere i percorsi quando si includono [file di assembly](#including-assembly-files) e [file di contenuto](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="cd85e-252">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="cd85e-253">I token hanno gli stessi nomi delle proprietà di MSBuild e ciò consente di selezionare i file da includere a seconda della configurazione di compilazione corrente.</span><span class="sxs-lookup"><span data-stu-id="cd85e-253">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="cd85e-254">Ad esempio, se si usano i token seguenti nel file `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="cd85e-254">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="cd85e-255">E si compila un assembly il cui `AssemblyName` è `LoggingLibrary` con la configurazione `Release` in MSBuild, le righe risultanti nel file `.nuspec` nel pacchetto sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="cd85e-255">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a><span data-ttu-id="cd85e-256">Dipendenze</span><span class="sxs-lookup"><span data-stu-id="cd85e-256">Dependencies</span></span>

<span data-ttu-id="cd85e-257">L'elemento `<dependencies>` all'interno di `<metadata>` contiene qualsiasi numero di elementi `<dependency>` che identificano altri pacchetti da cui dipende il pacchetto di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="cd85e-257">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="cd85e-258">Gli attributi per ogni `<dependency>` sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="cd85e-258">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="cd85e-259">Attributo</span><span class="sxs-lookup"><span data-stu-id="cd85e-259">Attribute</span></span> | <span data-ttu-id="cd85e-260">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cd85e-260">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="cd85e-261">(Obbligatorio) ID pacchetto della dipendenza, ad esempio "EntityFramework" e "NUnit", ovvero il nome di pacchetto che nuget.org mostra nella pagina di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-261">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="cd85e-262">(Obbligatorio) Intervallo di versioni accettabili come dipendenza.</span><span class="sxs-lookup"><span data-stu-id="cd85e-262">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="cd85e-263">Per la sintassi esatta, vedere [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="cd85e-263">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="cd85e-264">include</span><span class="sxs-lookup"><span data-stu-id="cd85e-264">include</span></span> | <span data-ttu-id="cd85e-265">Elenco delimitato da virgole di tag di inclusione/esclusione (vedere di seguito) che indicano la dipendenza da includere nel pacchetto finale.</span><span class="sxs-lookup"><span data-stu-id="cd85e-265">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="cd85e-266">Il valore predefinito è `none`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-266">The default value is `none`.</span></span> |
| <span data-ttu-id="cd85e-267">exclude</span><span class="sxs-lookup"><span data-stu-id="cd85e-267">exclude</span></span> | <span data-ttu-id="cd85e-268">Elenco delimitato da virgole di tag di inclusione/esclusione (vedere di seguito) che indicano la dipendenza da escludere nel pacchetto finale.</span><span class="sxs-lookup"><span data-stu-id="cd85e-268">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="cd85e-269">Il valore predefinito è `all`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-269">The  default value is `all`.</span></span> <span data-ttu-id="cd85e-270">I tag specificati con `exclude` hanno la precedenza rispetto a quelli specificati con `include`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-270">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="cd85e-271">Ad esempio, `include="runtime, compile" exclude="compile"` equivale a `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-271">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="cd85e-272">Tag di inclusione/esclusione</span><span class="sxs-lookup"><span data-stu-id="cd85e-272">Include/Exclude tag</span></span> | <span data-ttu-id="cd85e-273">Cartelle di destinazione interessate</span><span class="sxs-lookup"><span data-stu-id="cd85e-273">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="cd85e-274">contentFiles</span><span class="sxs-lookup"><span data-stu-id="cd85e-274">contentFiles</span></span> | <span data-ttu-id="cd85e-275">Content</span><span class="sxs-lookup"><span data-stu-id="cd85e-275">Content</span></span>  |
| <span data-ttu-id="cd85e-276">runtime</span><span class="sxs-lookup"><span data-stu-id="cd85e-276">runtime</span></span> | <span data-ttu-id="cd85e-277">Runtime, Resources e FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="cd85e-277">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="cd85e-278">compile</span><span class="sxs-lookup"><span data-stu-id="cd85e-278">compile</span></span> | <span data-ttu-id="cd85e-279">lib</span><span class="sxs-lookup"><span data-stu-id="cd85e-279">lib</span></span> |
| <span data-ttu-id="cd85e-280">build</span><span class="sxs-lookup"><span data-stu-id="cd85e-280">build</span></span> | <span data-ttu-id="cd85e-281">build (proprietà e destinazioni MSBuild)</span><span class="sxs-lookup"><span data-stu-id="cd85e-281">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="cd85e-282">native</span><span class="sxs-lookup"><span data-stu-id="cd85e-282">native</span></span> | <span data-ttu-id="cd85e-283">native</span><span class="sxs-lookup"><span data-stu-id="cd85e-283">native</span></span> |
| <span data-ttu-id="cd85e-284">none</span><span class="sxs-lookup"><span data-stu-id="cd85e-284">none</span></span> | <span data-ttu-id="cd85e-285">Nessuna cartella</span><span class="sxs-lookup"><span data-stu-id="cd85e-285">No folders</span></span> |
| <span data-ttu-id="cd85e-286">tutti</span><span class="sxs-lookup"><span data-stu-id="cd85e-286">all</span></span> | <span data-ttu-id="cd85e-287">Tutte le cartelle</span><span class="sxs-lookup"><span data-stu-id="cd85e-287">All folders</span></span> |

<span data-ttu-id="cd85e-288">Ad esempio, le righe seguenti indicano dipendenze da `PackageA` versione 1.1.0 o successive e da `PackageB` versione 1.x.</span><span class="sxs-lookup"><span data-stu-id="cd85e-288">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="cd85e-289">Le righe seguenti indicano dipendenze dagli stessi pacchetti, ma specificano di includere le cartelle `contentFiles` e `build` di `PackageA` e tutte le cartelle tranne `native` e `compile` di `PackageB`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-289">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="cd85e-290">Nota: quando si crea un file `.nuspec` da un progetto tramite `nuget spec`, le dipendenze esistenti in tale progetto vengono incluse automaticamente nel file `.nuspec` risultante.</span><span class="sxs-lookup"><span data-stu-id="cd85e-290">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="cd85e-291">Gruppi di dipendenze</span><span class="sxs-lookup"><span data-stu-id="cd85e-291">Dependency groups</span></span>

<span data-ttu-id="cd85e-292">*Versione 2.0+*</span><span class="sxs-lookup"><span data-stu-id="cd85e-292">*Version 2.0+*</span></span>

<span data-ttu-id="cd85e-293">In alternativa a un unico elenco semplice, è possibile specificare le dipendenze in base al profilo del framework del progetto di destinazione usando elementi `<group>` all'interno di `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-293">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="cd85e-294">Ogni gruppo ha un attributo denominato `targetFramework` e contiene zero o più elementi `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-294">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="cd85e-295">Tali dipendenze vengono installate insieme quando il framework di destinazione è compatibile con il profilo di framework del progetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-295">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="cd85e-296">L'elemento `<group>` senza un attributo `targetFramework` viene usato come elenco predefinito o di fallback delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="cd85e-296">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="cd85e-297">Vedere [Framework di destinazione](../reference/target-frameworks.md) per gli identificatori di framework esatti.</span><span class="sxs-lookup"><span data-stu-id="cd85e-297">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="cd85e-298">Il formato di gruppo non può essere usato in combinazione con un elenco semplice.</span><span class="sxs-lookup"><span data-stu-id="cd85e-298">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="cd85e-299">L'esempio seguente mostra variazioni diverse dell'elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="cd85e-299">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="cd85e-300">Riferimenti espliciti agli assembly</span><span class="sxs-lookup"><span data-stu-id="cd85e-300">Explicit assembly references</span></span>

<span data-ttu-id="cd85e-301">L'elemento `<references>` specifica in modo esplicito gli assembly a cui deve fare riferimento il progetto di destinazione quando usa il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-301">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="cd85e-302">Quando questo elemento è presente, NuGet aggiunge riferimenti solo agli assembly solo elencati e non aggiunge alcun riferimento per eventuali altri assembly nella cartella `lib` del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-302">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="cd85e-303">Ad esempio, l'elemento `<references>` seguente indica a NuGet di aggiungere riferimenti solo a `xunit.dll` e a `xunit.extensions.dll` anche se sono presenti altri assembly nel pacchetto:</span><span class="sxs-lookup"><span data-stu-id="cd85e-303">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="cd85e-304">I riferimenti espliciti vengono generalmente usati per gli assembly solo della fase di progettazione.</span><span class="sxs-lookup"><span data-stu-id="cd85e-304">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="cd85e-305">Quando si usano [contratti di codice](/dotnet/framework/debug-trace-profile/code-contracts), ad esempio, gli assembly del contratto devono essere in prossimità degli assembly di runtime che estendono, in modo che Visual Studio possa trovarli, ma non è necessario che il progetto faccia riferimento agli assembly di contratto oppure che vengano copiati nella cartella `bin` del progetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-305">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="cd85e-306">In modo analogo, si possono usare riferimenti espliciti per i framework di unit test, ad esempio XUnit, che richiedono che gli assembly degli strumenti siano collocati in prossimità degli assembly di runtime, ma non che siano inclusi riferimenti del progetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-306">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="cd85e-307">Gruppi di riferimenti</span><span class="sxs-lookup"><span data-stu-id="cd85e-307">Reference groups</span></span>

<span data-ttu-id="cd85e-308">In alternativa a un unico elenco semplice, è possibile specificare i riferimenti in base al profilo del framework del progetto di destinazione usando elementi `<group>` all'interno di `<references>`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-308">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="cd85e-309">Ogni gruppo ha un attributo denominato `targetFramework` e contiene zero o più elementi `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-309">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="cd85e-310">Tali riferimenti vengono aggiunti a un progetto quando il framework di destinazione è compatibile con il profilo di framework del progetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-310">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="cd85e-311">L'elemento `<group>` senza un attributo `targetFramework` viene usato come elenco predefinito o di fallback dei riferimenti.</span><span class="sxs-lookup"><span data-stu-id="cd85e-311">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="cd85e-312">Vedere [Framework di destinazione](../reference/target-frameworks.md) per gli identificatori di framework esatti.</span><span class="sxs-lookup"><span data-stu-id="cd85e-312">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="cd85e-313">Il formato di gruppo non può essere usato in combinazione con un elenco semplice.</span><span class="sxs-lookup"><span data-stu-id="cd85e-313">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="cd85e-314">L'esempio seguente mostra variazioni diverse dell'elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="cd85e-314">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="cd85e-315">Riferimenti agli assembly del framework</span><span class="sxs-lookup"><span data-stu-id="cd85e-315">Framework assembly references</span></span>

<span data-ttu-id="cd85e-316">Gli assembly del framework sono quelli che fanno parte di .NET Framework e devono essere già presenti nella Global Assembly Cache (GAC) per qualsiasi computer.</span><span class="sxs-lookup"><span data-stu-id="cd85e-316">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="cd85e-317">Grazie all'identificazione di tali assembly all'interno dell'elemento `<frameworkAssemblies>`, un pacchetto può garantire che i riferimenti necessari vengano aggiunti a un progetto nel caso in cui il progetto non includa già tali riferimenti.</span><span class="sxs-lookup"><span data-stu-id="cd85e-317">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="cd85e-318">Tali assembly, ovviamente, non vengono inclusi in un pacchetto direttamente.</span><span class="sxs-lookup"><span data-stu-id="cd85e-318">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="cd85e-319">L'elemento `<frameworkAssemblies>` contiene zero o più elementi `<frameworkAssembly>`, ognuno dei quali specifica gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cd85e-319">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="cd85e-320">Attributo</span><span class="sxs-lookup"><span data-stu-id="cd85e-320">Attribute</span></span> | <span data-ttu-id="cd85e-321">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cd85e-321">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cd85e-322">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="cd85e-322">**assemblyName**</span></span> | <span data-ttu-id="cd85e-323">(Obbligatorio) Nome completo dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="cd85e-323">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="cd85e-324">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="cd85e-324">**targetFramework**</span></span> | <span data-ttu-id="cd85e-325">(Facoltativo) Specifica il framework di destinazione a cui si applica questo riferimento.</span><span class="sxs-lookup"><span data-stu-id="cd85e-325">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="cd85e-326">Se omesso, indica che il riferimento si applica a tutti i framework.</span><span class="sxs-lookup"><span data-stu-id="cd85e-326">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="cd85e-327">Vedere [Framework di destinazione](../reference/target-frameworks.md) per gli identificatori di framework esatti.</span><span class="sxs-lookup"><span data-stu-id="cd85e-327">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="cd85e-328">L'esempio seguente mostra un riferimento a `System.Net` per tutti i framework di destinazione e un riferimento a `System.ServiceModel` solo per .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="cd85e-328">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="cd85e-329">Inclusione di file di assembly</span><span class="sxs-lookup"><span data-stu-id="cd85e-329">Including assembly files</span></span>

<span data-ttu-id="cd85e-330">Se si seguono le convenzioni descritte in [Creazione di un pacchetto](../create-packages/creating-a-package.md), non è necessario specificare in modo esplicito un elenco di file nel file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-330">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="cd85e-331">Il comando `nuget pack` rileva automaticamente i file necessari.</span><span class="sxs-lookup"><span data-stu-id="cd85e-331">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="cd85e-332">Quando un pacchetto viene installato in un progetto, NuGet aggiunge automaticamente i riferimenti agli assembly alle DLL del pacchetto, *escludendo* quelli denominati `.resources.dll` perché si presuppone che siano assembly satellite localizzati.</span><span class="sxs-lookup"><span data-stu-id="cd85e-332">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="cd85e-333">Per questo motivo, evitare di usare `.resources.dll` per i file che contengono invece codice essenziale per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-333">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="cd85e-334">Per evitare questo comportamento automatico e controllare in modo esplicito quali file vengono inclusi in un pacchetto, posizionare un elemento `<files>` come elemento figlio di `<package>` (ed elemento di pari livello di `<metadata>`), identificando ogni file con un elemento `<file>` separato.</span><span class="sxs-lookup"><span data-stu-id="cd85e-334">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="cd85e-335">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="cd85e-335">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="cd85e-336">Con NuGet 2.x e versioni precedenti e i progetti che usano `packages.config`, l'elemento `<files>` viene usato anche per includere file di contenuto non modificabili quando viene installato un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-336">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="cd85e-337">Con NuGet 3.3 + e PackageReference per i progetti, viene invece usato l'elemento `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-337">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="cd85e-338">Vedere [Inclusione di file di contenuto](#including-content-files) di seguito per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="cd85e-338">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="cd85e-339">Attributi dell'elemento file</span><span class="sxs-lookup"><span data-stu-id="cd85e-339">File element attributes</span></span>

<span data-ttu-id="cd85e-340">Ogni elemento `<file>` specifica gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cd85e-340">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="cd85e-341">Attributo</span><span class="sxs-lookup"><span data-stu-id="cd85e-341">Attribute</span></span> | <span data-ttu-id="cd85e-342">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cd85e-342">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cd85e-343">**src**</span><span class="sxs-lookup"><span data-stu-id="cd85e-343">**src**</span></span> | <span data-ttu-id="cd85e-344">Percorso del file o dei file da includere, soggetto alle esclusioni specificate dall'attributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-344">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="cd85e-345">Il percorso è relativo al file `.nuspec`, a meno che non venga specificato un percorso assoluto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-345">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="cd85e-346">Il carattere jolly `*` è consentito e il carattere jolly doppio `**` implica una ricerca ricorsiva nelle cartelle.</span><span class="sxs-lookup"><span data-stu-id="cd85e-346">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="cd85e-347">**target**</span><span class="sxs-lookup"><span data-stu-id="cd85e-347">**target**</span></span> | <span data-ttu-id="cd85e-348">Percorso relativo della cartella all'interno del pacchetto in cui vengono collocati i file di origine, che deve iniziare con `lib`, `content`, `build` o `tools`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-348">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="cd85e-349">Vedere [Creazione di un file .nuspec da una directory di lavoro basata su convenzioni](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="cd85e-349">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="cd85e-350">**exclude**</span><span class="sxs-lookup"><span data-stu-id="cd85e-350">**exclude**</span></span> | <span data-ttu-id="cd85e-351">Elenco delimitato da punti e virgola dei file o dei modelli di file da escludere dal percorso `src`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-351">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="cd85e-352">Il carattere jolly `*` è consentito e il carattere jolly doppio `**` implica una ricerca ricorsiva nelle cartelle.</span><span class="sxs-lookup"><span data-stu-id="cd85e-352">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="cd85e-353">Esempi</span><span class="sxs-lookup"><span data-stu-id="cd85e-353">Examples</span></span>

<span data-ttu-id="cd85e-354">**Singolo assembly**</span><span class="sxs-lookup"><span data-stu-id="cd85e-354">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="cd85e-355">**Singolo assembly specifico di un framework di destinazione**</span><span class="sxs-lookup"><span data-stu-id="cd85e-355">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="cd85e-356">**Set di DLL con un carattere jolly**</span><span class="sxs-lookup"><span data-stu-id="cd85e-356">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="cd85e-357">**DLL per framework diversi**</span><span class="sxs-lookup"><span data-stu-id="cd85e-357">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="cd85e-358">**Esclusione di file**</span><span class="sxs-lookup"><span data-stu-id="cd85e-358">**Excluding files**</span></span>

    Source files:
        \tools\*.bak
        \tools\*.log
        \tools\build\*.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a><span data-ttu-id="cd85e-359">Inclusione di file di contenuto</span><span class="sxs-lookup"><span data-stu-id="cd85e-359">Including content files</span></span>

<span data-ttu-id="cd85e-360">I file di contenuto sono file non modificabili che un pacchetto deve includere in un progetto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-360">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="cd85e-361">Essendo non modificabili, non sono progettati per essere modificati dal progetto che li utilizza.</span><span class="sxs-lookup"><span data-stu-id="cd85e-361">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="cd85e-362">Alcuni esempi di file di contenuto includono:</span><span class="sxs-lookup"><span data-stu-id="cd85e-362">Example content files include:</span></span>

- <span data-ttu-id="cd85e-363">Immagini incorporate come risorse</span><span class="sxs-lookup"><span data-stu-id="cd85e-363">Images that are embedded as resources</span></span>
- <span data-ttu-id="cd85e-364">File di origine già compilati</span><span class="sxs-lookup"><span data-stu-id="cd85e-364">Source files that are already compiled</span></span>
- <span data-ttu-id="cd85e-365">Script che devono essere inclusi con l'output di compilazione del progetto</span><span class="sxs-lookup"><span data-stu-id="cd85e-365">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="cd85e-366">File di configurazione per il pacchetto che devono essere inclusi nel progetto ma non richiedono modifiche specifiche del progetto</span><span class="sxs-lookup"><span data-stu-id="cd85e-366">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="cd85e-367">I file di contenuto vengono inclusi in un pacchetto con l'elemento `<files>`, specificando la cartella `content` nell'attributo `target`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-367">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="cd85e-368">Questi file vengono tuttavia ignorati quando il pacchetto viene installato in un progetto usando PackageReference, che usa invece l'elemento `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-368">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="cd85e-369">Per ottenere la massima compatibilità con i progetti in cui viene utilizzato, un pacchetto specifica idealmente i file di contenuto in entrambi gli elementi.</span><span class="sxs-lookup"><span data-stu-id="cd85e-369">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="cd85e-370">Uso dell'elemento files per i file di contenuto</span><span class="sxs-lookup"><span data-stu-id="cd85e-370">Using the files element for content files</span></span>

<span data-ttu-id="cd85e-371">Per i file di contenuto, usare semplicemente lo stesso formato usato per i file di assembly, ma specificare `content` come cartella di base nell'attributo `target`, come illustrato negli esempi seguenti.</span><span class="sxs-lookup"><span data-stu-id="cd85e-371">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="cd85e-372">**File di contenuto semplici**</span><span class="sxs-lookup"><span data-stu-id="cd85e-372">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="cd85e-373">**File di contenuto con struttura di directory**</span><span class="sxs-lookup"><span data-stu-id="cd85e-373">**Content files with directory structure**</span></span>

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

<span data-ttu-id="cd85e-374">**File di contenuto specifico di un framework di destinazione**</span><span class="sxs-lookup"><span data-stu-id="cd85e-374">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="cd85e-375">**File di contenuto copiato in una cartella con un punto nel nome**</span><span class="sxs-lookup"><span data-stu-id="cd85e-375">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="cd85e-376">In questo caso, NuGet rileva che l'estensione in `target` non corrisponde all'estensione in `src`, quindi interpreta la parte del nome in `target` come cartella:</span><span class="sxs-lookup"><span data-stu-id="cd85e-376">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="cd85e-377">**File di contenuto senza estensione**</span><span class="sxs-lookup"><span data-stu-id="cd85e-377">**Content files without extensions**</span></span>

<span data-ttu-id="cd85e-378">Per includere i file senza estensione, usare i caratteri jolly `*` o `**`:</span><span class="sxs-lookup"><span data-stu-id="cd85e-378">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="cd85e-379">**File di contenuto con percorso completo e destinazione completa**</span><span class="sxs-lookup"><span data-stu-id="cd85e-379">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="cd85e-380">In questo caso, dato che le estensioni dei file di origine e di destinazione corrispondono, NuGet presuppone che la destinazione sia un nome di file e non una cartella:</span><span class="sxs-lookup"><span data-stu-id="cd85e-380">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="cd85e-381">**Ridenominazione di un file di contenuto nel pacchetto**</span><span class="sxs-lookup"><span data-stu-id="cd85e-381">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="cd85e-382">**Esclusione di file**</span><span class="sxs-lookup"><span data-stu-id="cd85e-382">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="cd85e-383">Uso dell'elemento contentFiles per i file di contenuto</span><span class="sxs-lookup"><span data-stu-id="cd85e-383">Using the contentFiles element for content files</span></span>

<span data-ttu-id="cd85e-384">*NuGet 4.0 + con PackageReference*</span><span class="sxs-lookup"><span data-stu-id="cd85e-384">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="cd85e-385">Per impostazione predefinita, un pacchetto inserisce il contenuto in una cartella `contentFiles` (vedere di seguito) e `nuget pack` include tutti i file nella cartella usando gli attributi predefiniti.</span><span class="sxs-lookup"><span data-stu-id="cd85e-385">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="cd85e-386">In questo caso non è affatto necessario includere un nodo `contentFiles` nel file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-386">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="cd85e-387">Per controllare quali file sono inclusi, l'elemento `<contentFiles>` specifica una raccolta di elementi `<files>` che identificano i file esatti inclusi.</span><span class="sxs-lookup"><span data-stu-id="cd85e-387">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="cd85e-388">Questi file sono specificati con un set di attributi che descrivono come devono essere usati all'interno del sistema del progetto:</span><span class="sxs-lookup"><span data-stu-id="cd85e-388">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="cd85e-389">Attributo</span><span class="sxs-lookup"><span data-stu-id="cd85e-389">Attribute</span></span> | <span data-ttu-id="cd85e-390">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cd85e-390">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cd85e-391">**include**</span><span class="sxs-lookup"><span data-stu-id="cd85e-391">**include**</span></span> | <span data-ttu-id="cd85e-392">(Obbligatorio) Percorso del file o dei file da includere, soggetto alle esclusioni specificate dall'attributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-392">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="cd85e-393">Il percorso è relativo al file `.nuspec`, a meno che non venga specificato un percorso assoluto.</span><span class="sxs-lookup"><span data-stu-id="cd85e-393">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="cd85e-394">Il carattere jolly `*` è consentito e il carattere jolly doppio `**` implica una ricerca ricorsiva nelle cartelle.</span><span class="sxs-lookup"><span data-stu-id="cd85e-394">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="cd85e-395">**exclude**</span><span class="sxs-lookup"><span data-stu-id="cd85e-395">**exclude**</span></span> | <span data-ttu-id="cd85e-396">Elenco delimitato da punti e virgola dei file o dei modelli di file da escludere dal percorso `src`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-396">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="cd85e-397">Il carattere jolly `*` è consentito e il carattere jolly doppio `**` implica una ricerca ricorsiva nelle cartelle.</span><span class="sxs-lookup"><span data-stu-id="cd85e-397">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="cd85e-398">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="cd85e-398">**buildAction**</span></span> | <span data-ttu-id="cd85e-399">Azione di compilazione da assegnare all'elemento di contenuto per MSBuild, ad esempio `Content`, `None`, `Embedded Resource`, `Compile` e così via. Il valore predefinito è `Compile`.</span><span class="sxs-lookup"><span data-stu-id="cd85e-399">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="cd85e-400">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="cd85e-400">**copyToOutput**</span></span> | <span data-ttu-id="cd85e-401">Valore booleano che indica se copiare gli elementi di contenuto per la compilazione (o pubblicare) cartella di output.</span><span class="sxs-lookup"><span data-stu-id="cd85e-401">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="cd85e-402">Il valore predefinito è false.</span><span class="sxs-lookup"><span data-stu-id="cd85e-402">The default is false.</span></span> |
| <span data-ttu-id="cd85e-403">**flatten**</span><span class="sxs-lookup"><span data-stu-id="cd85e-403">**flatten**</span></span> | <span data-ttu-id="cd85e-404">Valore booleano che indica se copiare gli elementi di contenuto di una singola cartella nell'output di compilazione (true) o se mantenere la struttura di cartelle nel pacchetto (false).</span><span class="sxs-lookup"><span data-stu-id="cd85e-404">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="cd85e-405">Questo flag funziona solo quando il flag copyToOutput è impostato su true.</span><span class="sxs-lookup"><span data-stu-id="cd85e-405">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="cd85e-406">Il valore predefinito è false.</span><span class="sxs-lookup"><span data-stu-id="cd85e-406">The default is false.</span></span> |

<span data-ttu-id="cd85e-407">Quando si installa un pacchetto, NuGet applica gli elementi figlio di `<contentFiles>` dall'alto verso il basso.</span><span class="sxs-lookup"><span data-stu-id="cd85e-407">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="cd85e-408">Se più voci corrispondono allo stesso file, vengono applicate tutte le voci.</span><span class="sxs-lookup"><span data-stu-id="cd85e-408">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="cd85e-409">La voce di livello superiore sostituisce le voci inferiori in presenza di un conflitto per lo stesso attributo.</span><span class="sxs-lookup"><span data-stu-id="cd85e-409">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="cd85e-410">Struttura delle cartelle del pacchetto</span><span class="sxs-lookup"><span data-stu-id="cd85e-410">Package folder structure</span></span>

<span data-ttu-id="cd85e-411">Il progetto del pacchetto deve strutturare il contenuto in base al modello seguente:</span><span class="sxs-lookup"><span data-stu-id="cd85e-411">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="cd85e-412">`codeLanguages` può essere `cs`, `vb`, `fs`, `any` o l'equivalente in caratteri minuscoli di uno specifico `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="cd85e-412">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="cd85e-413">`TxM` è qualsiasi moniker di framework di destinazione valido supportato da NuGet (vedere [Framework di destinazione](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="cd85e-413">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="cd85e-414">Qualsiasi struttura di cartelle può essere aggiunta alla fine di questa sintassi.</span><span class="sxs-lookup"><span data-stu-id="cd85e-414">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="cd85e-415">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="cd85e-415">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="cd85e-416">Le cartelle vuote possono usare `.` per rifiutare esplicitamente di fornire contenuti per determinate combinazioni di linguaggio e TxM, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="cd85e-416">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="cd85e-417">Sezione di esempio contentFiles</span><span class="sxs-lookup"><span data-stu-id="cd85e-417">Example contentFiles section</span></span>

```xml
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
```

## <a name="example-nuspec-files"></a><span data-ttu-id="cd85e-418">File. nuspec di esempio</span><span class="sxs-lookup"><span data-stu-id="cd85e-418">Example .nuspec files</span></span>

<span data-ttu-id="cd85e-419">**File `.nuspec` semplice che non specifica dipendenze o file**</span><span class="sxs-lookup"><span data-stu-id="cd85e-419">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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
        <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
    </metadata>
</package>
```

<span data-ttu-id="cd85e-420">**File `.nuspec` con dipendenze**</span><span class="sxs-lookup"><span data-stu-id="cd85e-420">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="cd85e-421">**File `.nuspec` con file**</span><span class="sxs-lookup"><span data-stu-id="cd85e-421">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="cd85e-422">**File `.nuspec` con assembly di framework**</span><span class="sxs-lookup"><span data-stu-id="cd85e-422">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="cd85e-423">In questo esempio vengono installati i componenti seguenti per destinazioni di progetto specifiche:</span><span class="sxs-lookup"><span data-stu-id="cd85e-423">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="cd85e-424">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="cd85e-424">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="cd85e-425">.NET4 Client Profile -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="cd85e-425">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="cd85e-426">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="cd85e-426">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="cd85e-427">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="cd85e-427">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="cd85e-428">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="cd85e-428">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
