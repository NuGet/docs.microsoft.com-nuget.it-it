---
title: Riferimenti della versione del pacchetto NuGet
description: Tutti i dettagli su come specificare i numeri di versione e gli intervalli per gli altri pacchetti su cui dipende un pacchetto NuGet e modalità di installazione delle dipendenze.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: b980c1084fe8e31573053a4dcf38bbfa6146e6de
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549773"
---
# <a name="package-versioning"></a><span data-ttu-id="da963-103">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="da963-103">Package versioning</span></span>

<span data-ttu-id="da963-104">Un pacchetto specifico fa sempre riferimento utilizzando il relativo identificatore di pacchetto e un numero di versione esatto.</span><span class="sxs-lookup"><span data-stu-id="da963-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="da963-105">Ad esempio, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) ha diverse decine specifici dei pacchetti disponibili, che vanno dalla versione in nuget.org *4.1.10311* alla versione *6.1.3* (l'ultima versione stabile da Release) e, ad esempio un'ampia gamma di versioni non definitive *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="da963-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="da963-106">Quando si crea un pacchetto, si assegna un numero di versione specifico con un suffisso di versione non definitiva facoltativa in formato testo.</span><span class="sxs-lookup"><span data-stu-id="da963-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="da963-107">Quando si utilizzano i pacchetti, d'altra parte, è possibile specificare un numero di versione esatto o un intervallo di versioni accettabili.</span><span class="sxs-lookup"><span data-stu-id="da963-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="da963-108">In questo argomento</span><span class="sxs-lookup"><span data-stu-id="da963-108">In this topic:</span></span>

- <span data-ttu-id="da963-109">[Nozioni fondamentali sulla versione](#version-basics) incluse versioni non definitive suffissi.</span><span class="sxs-lookup"><span data-stu-id="da963-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="da963-110">I caratteri jolly e intervalli di versione</span><span class="sxs-lookup"><span data-stu-id="da963-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="da963-111">Numeri di versione normalizzata</span><span class="sxs-lookup"><span data-stu-id="da963-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="da963-112">Nozioni fondamentali sulla versione</span><span class="sxs-lookup"><span data-stu-id="da963-112">Version basics</span></span>

<span data-ttu-id="da963-113">Numero di versione specifico è nel formato *Major [-suffisso]*, in cui i componenti hanno i significati seguenti:</span><span class="sxs-lookup"><span data-stu-id="da963-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="da963-114">*Principali*: modifiche di rilievo</span><span class="sxs-lookup"><span data-stu-id="da963-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="da963-115">*Minori*: nuove funzionalità, ma compatibili con le versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="da963-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="da963-116">*Patch*: solo correzioni di bug compatibili con le versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="da963-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="da963-117">*-Suffisso* (facoltativo): un trattino seguita da una stringa che indica una versione non definitiva (segue il [convenzione di Versionamento semantico o SemVer 1.0](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="da963-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="da963-118">**Esempi:**</span><span class="sxs-lookup"><span data-stu-id="da963-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="da963-119">NuGet.org Rifiuta qualsiasi il caricamento del pacchetto che non dispone di un numero di versione esatto.</span><span class="sxs-lookup"><span data-stu-id="da963-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="da963-120">La versione deve essere specificata nel `.nuspec` o file di progetto usato per creare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="da963-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="da963-121">Versioni non definitive</span><span class="sxs-lookup"><span data-stu-id="da963-121">Pre-release versions</span></span>

<span data-ttu-id="da963-122">Tecnicamente, gli autori dei pacchetti possono utilizzare qualsiasi stringa come un suffisso per indicare una versione non definitiva, perché NuGet considera tale versione di qualsiasi versione non definitiva e non rende interpretazione di altri.</span><span class="sxs-lookup"><span data-stu-id="da963-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="da963-123">Vale a dire, NuGet consente di visualizzare la versione completa di stringhe nell'interfaccia utente di qualsiasi è coinvolta, lasciando l'interpretazione del significato del suffisso per il consumer.</span><span class="sxs-lookup"><span data-stu-id="da963-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="da963-124">Ciò premesso, gli sviluppatori di pacchetti in genere seguono le convenzioni di denominazione riconosciute:</span><span class="sxs-lookup"><span data-stu-id="da963-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="da963-125">`-alpha`: Versione alfa, in genere usato per lavoro in corso e sperimentazione.</span><span class="sxs-lookup"><span data-stu-id="da963-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="da963-126">`-beta`: versione beta, in genere completa dal punto di vista funzionale per il successivo rilascio pianificato, ma può contenere bug noti.</span><span class="sxs-lookup"><span data-stu-id="da963-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="da963-127">`-rc`: versione finale candidata, in genere potenzialmente finale (stabile) se non emergono bug significativi.</span><span class="sxs-lookup"><span data-stu-id="da963-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="da963-128">NuGet 4.3.0 + supporta [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), che supporta i numeri di versione non definitiva con la notazione del punto, come mostrato nella *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="da963-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="da963-129">La notazione con punto non è supportata con le versioni di NuGet precedenti alla versione 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="da963-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="da963-130">È possibile usare un modulo, ad esempio *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="da963-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="da963-131">Durante la risoluzione di riferimenti ai pacchetti e più versioni del pacchetto sono diversi solo per il suffisso, NuGet sceglie una versione senza suffisso, prima di tutto, quindi si applica la priorità per versioni non definitive in ordine alfabetico inverso.</span><span class="sxs-lookup"><span data-stu-id="da963-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="da963-132">Ad esempio, le versioni seguenti viene scelta in base all'ordine esatto illustrato:</span><span class="sxs-lookup"><span data-stu-id="da963-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="da963-133">Versionamento semantico 2.0.0</span><span class="sxs-lookup"><span data-stu-id="da963-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="da963-134">Con NuGet 4.3.0 + e Visual Studio 2017 versione 15.3 +, NuGet supporta [Versionamento semantico 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="da963-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="da963-135">Determinati semantica di SemVer v2.0.0 non è supportata nel client meno recenti.</span><span class="sxs-lookup"><span data-stu-id="da963-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="da963-136">NuGet considera una versione del pacchetto sia v2.0.0 SemVer specifici se una delle seguenti affermazioni è vera:</span><span class="sxs-lookup"><span data-stu-id="da963-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="da963-137">L'etichetta di versioni non definitive è delimitato da punti, ad esempio, *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="da963-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="da963-138">La versione contiene metadati di compilazione, ad esempio, *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="da963-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="da963-139">Per nuget.org, un pacchetto è definito come un pacchetto v2.0.0 SemVer se una delle seguenti affermazioni è vera:</span><span class="sxs-lookup"><span data-stu-id="da963-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="da963-140">La versione del pacchetto è compatibile con SemVer v2.0.0 ma non SemVer v1.0.0 conforme, come definito in precedenza.</span><span class="sxs-lookup"><span data-stu-id="da963-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="da963-141">Uno degli intervalli di versione delle dipendenze del pacchetto ha una versione minima o massima che è compatibile con SemVer v2.0.0 ma non SemVer v1.0.0 conforme, definiti in precedenza; ad esempio, *[1.0.0-alpha.1,)*.</span><span class="sxs-lookup"><span data-stu-id="da963-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="da963-142">Se si carica un pacchetto specifico v2.0.0 SemVer su nuget.org, il pacchetto sia visibile ai client meno recenti e disponibile per i seguenti client di NuGet:</span><span class="sxs-lookup"><span data-stu-id="da963-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="da963-143">NuGet 4.3.0 +</span><span class="sxs-lookup"><span data-stu-id="da963-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="da963-144">Visual Studio 2017 versione 15.3 +</span><span class="sxs-lookup"><span data-stu-id="da963-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="da963-145">Visual Studio 2015 con [v3.6.0 VSIX di NuGet](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="da963-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="da963-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="da963-146">dotnet</span></span>
  - <span data-ttu-id="da963-147">dotnetcore.exe (2.0.0+ .NET SDK)</span><span class="sxs-lookup"><span data-stu-id="da963-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="da963-148">Client di terze parti:</span><span class="sxs-lookup"><span data-stu-id="da963-148">Third-party clients:</span></span>

- <span data-ttu-id="da963-149">Rider JetBrains</span><span class="sxs-lookup"><span data-stu-id="da963-149">JetBrains Rider</span></span>
- <span data-ttu-id="da963-150">Paket versione 5.0 +</span><span class="sxs-lookup"><span data-stu-id="da963-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="da963-151">I caratteri jolly e intervalli di versione</span><span class="sxs-lookup"><span data-stu-id="da963-151">Version ranges and wildcards</span></span>

<span data-ttu-id="da963-152">Quando si fa riferimento alle dipendenze di pacchetto, NuGet supporta utilizzando la notazione di intervallo per la specifica di intervalli di versione, riepilogati come segue:</span><span class="sxs-lookup"><span data-stu-id="da963-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="da963-153">Notation</span><span class="sxs-lookup"><span data-stu-id="da963-153">Notation</span></span> | <span data-ttu-id="da963-154">Regola applicata</span><span class="sxs-lookup"><span data-stu-id="da963-154">Applied rule</span></span> | <span data-ttu-id="da963-155">Descrizione</span><span class="sxs-lookup"><span data-stu-id="da963-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="da963-156">1.0</span><span class="sxs-lookup"><span data-stu-id="da963-156">1.0</span></span> | <span data-ttu-id="da963-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="da963-157">x ≥ 1.0</span></span> | <span data-ttu-id="da963-158">Versione minima, inclusivo</span><span class="sxs-lookup"><span data-stu-id="da963-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="da963-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="da963-159">(1.0,)</span></span> | <span data-ttu-id="da963-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="da963-160">x > 1.0</span></span> | <span data-ttu-id="da963-161">Versione minima, esclusivo</span><span class="sxs-lookup"><span data-stu-id="da963-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="da963-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="da963-162">[1.0]</span></span> | <span data-ttu-id="da963-163">x = = 1.0</span><span class="sxs-lookup"><span data-stu-id="da963-163">x == 1.0</span></span> | <span data-ttu-id="da963-164">Corrispondenza esatta della versione</span><span class="sxs-lookup"><span data-stu-id="da963-164">Exact version match</span></span> |
| <span data-ttu-id="da963-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="da963-165">(,1.0]</span></span> | <span data-ttu-id="da963-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="da963-166">x ≤ 1.0</span></span> | <span data-ttu-id="da963-167">Versione massima, inclusivo</span><span class="sxs-lookup"><span data-stu-id="da963-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="da963-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="da963-168">(,1.0)</span></span> | <span data-ttu-id="da963-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="da963-169">x < 1.0</span></span> | <span data-ttu-id="da963-170">Versione massima, esclusivo</span><span class="sxs-lookup"><span data-stu-id="da963-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="da963-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="da963-171">[1.0,2.0]</span></span> | <span data-ttu-id="da963-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="da963-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="da963-173">Intervallo esatto, inclusivo</span><span class="sxs-lookup"><span data-stu-id="da963-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="da963-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="da963-174">(1.0,2.0)</span></span> | <span data-ttu-id="da963-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="da963-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="da963-176">Intervallo esatto, esclusivo</span><span class="sxs-lookup"><span data-stu-id="da963-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="da963-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="da963-177">[1.0,2.0)</span></span> | <span data-ttu-id="da963-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="da963-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="da963-179">Inclusivo minimo ed esclusivo massimo mista</span><span class="sxs-lookup"><span data-stu-id="da963-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="da963-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="da963-180">(1.0)</span></span>    | <span data-ttu-id="da963-181">non valido</span><span class="sxs-lookup"><span data-stu-id="da963-181">invalid</span></span> | <span data-ttu-id="da963-182">non valido</span><span class="sxs-lookup"><span data-stu-id="da963-182">invalid</span></span> |

<span data-ttu-id="da963-183">Quando si usa il formato PackageReference, NuGet supporta anche l'utilizzo di una notazione con caratteri jolly, \*per principale, secondaria, Patch e parti del suffisso di versione non definitiva del numero.</span><span class="sxs-lookup"><span data-stu-id="da963-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="da963-184">I caratteri jolly non sono supportate con il `packages.config` formato.</span><span class="sxs-lookup"><span data-stu-id="da963-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="da963-185">Le versioni non definitive non sono incluse durante la risoluzione di intervalli di versione.</span><span class="sxs-lookup"><span data-stu-id="da963-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="da963-186">Versioni non definitive *vengono* incluso quando si usa un carattere jolly (\*).</span><span class="sxs-lookup"><span data-stu-id="da963-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="da963-187">L'intervallo di versioni *[1.0,2.0]*, ad esempio, non includere 2.0-beta, ma la notazione con caratteri jolly _2.0-\*_ viene.</span><span class="sxs-lookup"><span data-stu-id="da963-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-\*_ does.</span></span> <span data-ttu-id="da963-188">Visualizzare [emettere 912](https://github.com/NuGet/Home/issues/912) per ulteriori informazioni sui caratteri jolly di versioni non definitive.</span><span class="sxs-lookup"><span data-stu-id="da963-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="da963-189">Esempi</span><span class="sxs-lookup"><span data-stu-id="da963-189">Examples</span></span>

<span data-ttu-id="da963-190">Specificare sempre una versione o intervallo di versioni per le dipendenze dei pacchetti nei file di progetto `packages.config` file, e `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="da963-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="da963-191">Senza una versione o intervallo di versioni, NuGet 2.8.x e in precedenza sceglie la versione più recente del pacchetto disponibile quando si risolve una dipendenza, mentre NuGet 3.x e versioni successive sceglie la versione del pacchetto più bassa.</span><span class="sxs-lookup"><span data-stu-id="da963-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="da963-192">Specificare una versione o intervallo consente di evitare questa incertezza.</span><span class="sxs-lookup"><span data-stu-id="da963-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="da963-193">Riferimenti nel file di progetto (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="da963-193">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="da963-194">**Fa riferimento `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="da963-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="da963-195">Nelle `packages.config`, tutte le dipendenze sia elencata con un valore esatto `version` attributo che viene usato quando il ripristino dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="da963-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="da963-196">Il `allowedVersions` attributo viene utilizzato solo durante le operazioni di aggiornamento per vincolare le versioni a cui il pacchetto potrebbe essere aggiornato.</span><span class="sxs-lookup"><span data-stu-id="da963-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

<span data-ttu-id="da963-197">**Fa riferimento `.nuspec` file**</span><span class="sxs-lookup"><span data-stu-id="da963-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="da963-198">Il `version` dell'attributo un `<dependency>` elemento descrive le versioni di intervallo sono accettabili per una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="da963-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a><span data-ttu-id="da963-199">Numeri di versione normalizzata</span><span class="sxs-lookup"><span data-stu-id="da963-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="da963-200">Si tratta di una modifica di rilievo per NuGet 3.4 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="da963-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="da963-201">Durante l'acquisizione di pacchetti da un repository durante l'installazione, reinstallare o ripristinare le operazioni, NuGet 3.4 + considera i numeri di versione come segue:</span><span class="sxs-lookup"><span data-stu-id="da963-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="da963-202">Gli zeri iniziali vengono rimossi dai numeri di versione:</span><span class="sxs-lookup"><span data-stu-id="da963-202">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="da963-203">Verrà omesso uno zero nella quarta parte del numero di versione</span><span class="sxs-lookup"><span data-stu-id="da963-203">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="da963-204">Questa normalizzazione non influisce sui numeri di versione nei pacchetti stessi; ha effetto sul modo in cui NuGet corrisponde solo versioni quando la risoluzione delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="da963-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="da963-205">Tuttavia, i repository dei pacchetti NuGet devono considerare questi valori nello stesso modo come NuGet per evitare la duplicazione di versione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="da963-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="da963-206">In questo modo un repository che contiene la versione *1.0* di un pacchetto non deve inoltre ospitare versione *1.0.0* come pacchetto separato e diverso.</span><span class="sxs-lookup"><span data-stu-id="da963-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
