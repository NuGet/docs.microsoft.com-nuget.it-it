---
title: Informazioni di riferimento sulle versioni dei pacchetti NuGet
description: Informazioni dettagliate su come specificare i numeri di versione e gli intervalli per altri pacchetti da cui dipende un pacchetto NuGet e sulla modalità di installazione delle dipendenze.
author: JonDouglas
ms.author: jodou
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 77b96e83f8fc7afd391537d16120d037585dd379
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859200"
---
# <a name="package-versioning"></a><span data-ttu-id="e6de4-103">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="e6de4-103">Package versioning</span></span>

<span data-ttu-id="e6de4-104">A un pacchetto specifico viene sempre fatto riferimento usando l'identificatore del pacchetto e un numero di versione esatto.</span><span class="sxs-lookup"><span data-stu-id="e6de4-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="e6de4-105">Per [Entity Framework](https://www.nuget.org/packages/EntityFramework/) su nuget.org, ad esempio, sono disponibili alcune decine di pacchetti specifici, compresi tra la versione *4.1.10311* e la versione *6.1.3* (la versione stabile più recente) e svariate versioni non definitive come *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="e6de4-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="e6de4-106">Quando si crea un pacchetto, si assegna un numero di versione specifico con un suffisso di testo per la versione non definitiva facoltativo.</span><span class="sxs-lookup"><span data-stu-id="e6de4-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="e6de4-107">Quando si utilizzano i pacchetti, invece, è possibile specificare un numero di versione esatto o un intervallo di versioni accettabili.</span><span class="sxs-lookup"><span data-stu-id="e6de4-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="e6de4-108">In questo argomento</span><span class="sxs-lookup"><span data-stu-id="e6de4-108">In this topic:</span></span>

- <span data-ttu-id="e6de4-109">[Nozioni di base sulle versioni](#version-basics), inclusi i suffissi di versione non definitiva.</span><span class="sxs-lookup"><span data-stu-id="e6de4-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="e6de4-110">Intervalli di versione</span><span class="sxs-lookup"><span data-stu-id="e6de4-110">Version ranges</span></span>](#version-ranges)
- [<span data-ttu-id="e6de4-111">Numeri di versione normalizzati</span><span class="sxs-lookup"><span data-stu-id="e6de4-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="e6de4-112">Nozioni di base sulle versioni</span><span class="sxs-lookup"><span data-stu-id="e6de4-112">Version basics</span></span>

<span data-ttu-id="e6de4-113">Un numero di versione specifico è nel formato *Principale.Secondaria.Patch[-Suffisso]*, dove i singoli componenti hanno i significati seguenti:</span><span class="sxs-lookup"><span data-stu-id="e6de4-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="e6de4-114">*Principale*: modifiche di rilievo</span><span class="sxs-lookup"><span data-stu-id="e6de4-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="e6de4-115">*Minor*: nuove funzionalità, ma compatibili con le versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="e6de4-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="e6de4-116">*Patch*: solo correzioni di bug compatibili con le versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="e6de4-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="e6de4-117">*-Suffisso* (facoltativo): un trattino seguito da una stringa che indica una versione non definitiva (in base alla [convenzione Semantic Versioning o SemVer 1.0](https://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="e6de4-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="e6de4-118">**Esempi:**</span><span class="sxs-lookup"><span data-stu-id="e6de4-118">**Examples:**</span></span>

```
1.0.1
6.11.1231
4.3.1-rc
2.2.44-beta1
```

> [!Important]
> <span data-ttu-id="e6de4-119">nuget.org rifiuta il caricamento di un pacchetto senza un numero di versione esatto.</span><span class="sxs-lookup"><span data-stu-id="e6de4-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="e6de4-120">La versione deve essere specificata nel file `.nuspec` o nel file di progetto usato per creare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e6de4-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="e6de4-121">Versioni non definitive</span><span class="sxs-lookup"><span data-stu-id="e6de4-121">Pre-release versions</span></span>

<span data-ttu-id="e6de4-122">Dal punto di vista tecnico, i creatori di pacchetti possono usare qualsiasi stringa come suffisso per indicare una versione non definitiva, perché NuGet considera una versione con questa caratteristica non definitiva senza altre interpretazioni.</span><span class="sxs-lookup"><span data-stu-id="e6de4-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="e6de4-123">In altre parole, NuGet visualizza la stringa di versione completa in qualsiasi interfaccia utente, lasciando l'interpretazione del significato del suffisso all'utente.</span><span class="sxs-lookup"><span data-stu-id="e6de4-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="e6de4-124">Ciò premesso, gli sviluppatori di pacchetti seguono generalmente convenzioni di denominazione riconosciute:</span><span class="sxs-lookup"><span data-stu-id="e6de4-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="e6de4-125">`-alpha`: Versione Alpha, in genere usata per il lavoro in corso e la sperimentazione.</span><span class="sxs-lookup"><span data-stu-id="e6de4-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="e6de4-126">`-beta`: versione beta, in genere completa dal punto di vista funzionale per il successivo rilascio pianificato, ma può contenere bug noti.</span><span class="sxs-lookup"><span data-stu-id="e6de4-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="e6de4-127">`-rc`: versione finale candidata, in genere potenzialmente finale (stabile) se non emergono bug significativi.</span><span class="sxs-lookup"><span data-stu-id="e6de4-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="e6de4-128">NuGet 4.3.0+ supporta [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), ovvero numeri di versione non definitiva con la notazione con punto, come in *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="e6de4-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="e6de4-129">La notazione con punto non è supportata con le versioni di NuGet precedenti alla versione 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="e6de4-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="e6de4-130">È possibile usare un formato come *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="e6de4-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="e6de4-131">Se durante la risoluzione dei riferimenti al pacchetto risultano più versioni del pacchetto che differiscono solo per il suffisso, NuGet sceglie prima una versione senza suffisso, quindi applica la precedenza alle versioni non definitive in ordine alfabetico inverso.</span><span class="sxs-lookup"><span data-stu-id="e6de4-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="e6de4-132">Le versioni seguenti, ad esempio, verrebbero scelte nell'esatto ordine indicato:</span><span class="sxs-lookup"><span data-stu-id="e6de4-132">For example, the following versions would be chosen in the exact order shown:</span></span>

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
1.0.1-aaa
```

## <a name="semantic-versioning-200"></a><span data-ttu-id="e6de4-133">Semantic Versioning 2.0.0</span><span class="sxs-lookup"><span data-stu-id="e6de4-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="e6de4-134">Con NuGet 4.3.0+ e Visual Studio 2017 versione 15.3+, NuGet supporta la convenzione [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="e6de4-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="e6de4-135">Certe regole semantiche di SemVer 2.0.0 non sono supportate nei client meno recenti.</span><span class="sxs-lookup"><span data-stu-id="e6de4-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="e6de4-136">NuGet considera la versione di un pacchetto come specifica di SemVer 2.0.0 se una delle affermazioni seguenti è vera:</span><span class="sxs-lookup"><span data-stu-id="e6de4-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="e6de4-137">L'etichetta della versione non definitiva è separata da punti, ad esempio *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="e6de4-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="e6de4-138">La versione include metadati di compilazione, ad esempio *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="e6de4-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="e6de4-139">Per nuget.org, un pacchetto viene definito come pacchetto SemVer 2.0.0 se una delle affermazioni seguenti è vera:</span><span class="sxs-lookup"><span data-stu-id="e6de4-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="e6de4-140">La versione del pacchetto è conforme a SemVer 2.0.0 ma non è conforme a SemVer 1.0.0, come definito sopra.</span><span class="sxs-lookup"><span data-stu-id="e6de4-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="e6de4-141">Uno degli intervalli di versioni delle dipendenze del pacchetto ha una versione minima o massima conforme a SemVer 2.0.0 ma non conforme a SemVer 1.0.0, definita in precedenza. Ad esempio, *[1.0.0-alpha.1, )*.</span><span class="sxs-lookup"><span data-stu-id="e6de4-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="e6de4-142">Se si carica un pacchetto specifico di SemVer 2.0.0 in nuget.org, il pacchetto è invisibile ai client meno recenti e disponibile solo per i client NuGet seguenti:</span><span class="sxs-lookup"><span data-stu-id="e6de4-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="e6de4-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="e6de4-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="e6de4-144">Visual Studio 2017 versione 15.3+</span><span class="sxs-lookup"><span data-stu-id="e6de4-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="e6de4-145">Visual Studio 2015 con [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="e6de4-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="e6de4-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="e6de4-146">dotnet</span></span>
  - <span data-ttu-id="e6de4-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="e6de4-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="e6de4-148">Client di terze parti:</span><span class="sxs-lookup"><span data-stu-id="e6de4-148">Third-party clients:</span></span>

- <span data-ttu-id="e6de4-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="e6de4-149">JetBrains Rider</span></span>
- <span data-ttu-id="e6de4-150">Paket versione 5.0 +</span><span class="sxs-lookup"><span data-stu-id="e6de4-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a><span data-ttu-id="e6de4-151">Intervalli di versione</span><span class="sxs-lookup"><span data-stu-id="e6de4-151">Version ranges</span></span>

<span data-ttu-id="e6de4-152">Quando si fa riferimento alle dipendenze dei pacchetti, NuGet supporta l'uso della notazione con intervallo per specificare gli intervalli di versione, riepilogati come segue:</span><span class="sxs-lookup"><span data-stu-id="e6de4-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="e6de4-153">Notation</span><span class="sxs-lookup"><span data-stu-id="e6de4-153">Notation</span></span> | <span data-ttu-id="e6de4-154">Regola applicata</span><span class="sxs-lookup"><span data-stu-id="e6de4-154">Applied rule</span></span> | <span data-ttu-id="e6de4-155">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e6de4-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="e6de4-156">1.0</span><span class="sxs-lookup"><span data-stu-id="e6de4-156">1.0</span></span> | <span data-ttu-id="e6de4-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="e6de4-157">x ≥ 1.0</span></span> | <span data-ttu-id="e6de4-158">Versione minima, inclusiva</span><span class="sxs-lookup"><span data-stu-id="e6de4-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="e6de4-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="e6de4-159">(1.0,)</span></span> | <span data-ttu-id="e6de4-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="e6de4-160">x > 1.0</span></span> | <span data-ttu-id="e6de4-161">Versione minima, esclusiva</span><span class="sxs-lookup"><span data-stu-id="e6de4-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="e6de4-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="e6de4-162">[1.0]</span></span> | <span data-ttu-id="e6de4-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="e6de4-163">x == 1.0</span></span> | <span data-ttu-id="e6de4-164">Corrispondenza esatta della versione</span><span class="sxs-lookup"><span data-stu-id="e6de4-164">Exact version match</span></span> |
| <span data-ttu-id="e6de4-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="e6de4-165">(,1.0]</span></span> | <span data-ttu-id="e6de4-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="e6de4-166">x ≤ 1.0</span></span> | <span data-ttu-id="e6de4-167">Versione massima, inclusiva</span><span class="sxs-lookup"><span data-stu-id="e6de4-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="e6de4-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="e6de4-168">(,1.0)</span></span> | <span data-ttu-id="e6de4-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="e6de4-169">x < 1.0</span></span> | <span data-ttu-id="e6de4-170">Versione massima, esclusiva</span><span class="sxs-lookup"><span data-stu-id="e6de4-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="e6de4-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="e6de4-171">[1.0,2.0]</span></span> | <span data-ttu-id="e6de4-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="e6de4-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="e6de4-173">Intervallo esatto, inclusivo</span><span class="sxs-lookup"><span data-stu-id="e6de4-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="e6de4-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="e6de4-174">(1.0,2.0)</span></span> | <span data-ttu-id="e6de4-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="e6de4-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="e6de4-176">Intervallo esatto, esclusivo</span><span class="sxs-lookup"><span data-stu-id="e6de4-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="e6de4-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="e6de4-177">[1.0,2.0)</span></span> | <span data-ttu-id="e6de4-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="e6de4-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="e6de4-179">Versione minima inclusiva e massima esclusiva mista</span><span class="sxs-lookup"><span data-stu-id="e6de4-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="e6de4-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="e6de4-180">(1.0)</span></span>    | <span data-ttu-id="e6de4-181">non valido</span><span class="sxs-lookup"><span data-stu-id="e6de4-181">invalid</span></span> | <span data-ttu-id="e6de4-182">non valido</span><span class="sxs-lookup"><span data-stu-id="e6de4-182">invalid</span></span> |

<span data-ttu-id="e6de4-183">Quando si usa il formato PackageReference, NuGet supporta anche l'uso di una notazione mobile, \* , per le parti principali, secondarie, patch e del suffisso di versione non definitiva del numero.</span><span class="sxs-lookup"><span data-stu-id="e6de4-183">When using the PackageReference format, NuGet also supports using a floating notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="e6de4-184">Le versioni a virgola mobile non sono supportate con il `packages.config` formato.</span><span class="sxs-lookup"><span data-stu-id="e6de4-184">Floating versions are not supported with the `packages.config` format.</span></span> <span data-ttu-id="e6de4-185">Quando si specifica una versione a virgola mobile, la regola deve essere risolta con la versione più recente esistente corrispondente alla descrizione della versione.</span><span class="sxs-lookup"><span data-stu-id="e6de4-185">When a floating version is specified, the rule is to resolve to the highest existent version that matches the version description.</span></span> <span data-ttu-id="e6de4-186">Di seguito sono riportati alcuni esempi di versioni a virgola mobile e le risoluzioni.</span><span class="sxs-lookup"><span data-stu-id="e6de4-186">Examples of floating versions and the resolutions are below.</span></span>

> [!Note]
> <span data-ttu-id="e6de4-187">Gli intervalli di versione in PackageReference includono le versioni non definitive.</span><span class="sxs-lookup"><span data-stu-id="e6de4-187">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="e6de4-188">Per impostazione predefinita, le versioni mobili non risolvono le versioni non definitive se non con consenso esplicito.</span><span class="sxs-lookup"><span data-stu-id="e6de4-188">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="e6de4-189">Per lo stato della richiesta di funzionalità correlata, vedere il [problema 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="e6de4-189">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="e6de4-190">Esempio</span><span class="sxs-lookup"><span data-stu-id="e6de4-190">Examples</span></span>

<span data-ttu-id="e6de4-191">Specificare sempre una versione o un intervallo di versioni per le dipendenze dei pacchetti nei file di progetto, nei file `packages.config` e nei file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="e6de4-191">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="e6de4-192">Senza una versione o un intervallo di versioni, NuGet 2.8.x e versioni precedenti scelgono la versione più recente del pacchetto disponibile durante la risoluzione di una dipendenza, mentre NuGet 3.x e versioni successive scelgono la versione del pacchetto più bassa.</span><span class="sxs-lookup"><span data-stu-id="e6de4-192">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="e6de4-193">La specifica di una versione o di un intervallo di versioni evita questa incertezza.</span><span class="sxs-lookup"><span data-stu-id="e6de4-193">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="e6de4-194">Riferimenti nei file di progetto (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="e6de4-194">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version.
     Will resolve to the highest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. 
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. 
     Will resolve to the smallest acceptable stable version.
     -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher.
     Will resolve to the smallest acceptable stable version. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

#### <a name="floating-version-resolutions"></a><span data-ttu-id="e6de4-195">Risoluzioni a versione mobile</span><span class="sxs-lookup"><span data-stu-id="e6de4-195">Floating version resolutions</span></span> 

| <span data-ttu-id="e6de4-196">Versione</span><span class="sxs-lookup"><span data-stu-id="e6de4-196">Version</span></span> | <span data-ttu-id="e6de4-197">Versioni presenti sul server</span><span class="sxs-lookup"><span data-stu-id="e6de4-197">Versions present on server</span></span> | <span data-ttu-id="e6de4-198">Soluzione</span><span class="sxs-lookup"><span data-stu-id="e6de4-198">Resolution</span></span> | <span data-ttu-id="e6de4-199">Motivo</span><span class="sxs-lookup"><span data-stu-id="e6de4-199">Reason</span></span> | <span data-ttu-id="e6de4-200">Note</span><span class="sxs-lookup"><span data-stu-id="e6de4-200">Notes</span></span> |
|----------|--------------|-------------|-------------|-------------|
| * | <span data-ttu-id="e6de4-201">1.1.0</span><span class="sxs-lookup"><span data-stu-id="e6de4-201">1.1.0</span></span> <br> <span data-ttu-id="e6de4-202">1.1.1</span><span class="sxs-lookup"><span data-stu-id="e6de4-202">1.1.1</span></span> <br> <span data-ttu-id="e6de4-203">1.2.0</span><span class="sxs-lookup"><span data-stu-id="e6de4-203">1.2.0</span></span> <br> <span data-ttu-id="e6de4-204">1.3.0-alfa</span><span class="sxs-lookup"><span data-stu-id="e6de4-204">1.3.0-alpha</span></span>  | <span data-ttu-id="e6de4-205">1.2.0</span><span class="sxs-lookup"><span data-stu-id="e6de4-205">1.2.0</span></span> | <span data-ttu-id="e6de4-206">Versione stabile più recente.</span><span class="sxs-lookup"><span data-stu-id="e6de4-206">The highest stable version.</span></span> |
| <span data-ttu-id="e6de4-207">1.1.\*</span><span class="sxs-lookup"><span data-stu-id="e6de4-207">1.1.\*</span></span> | <span data-ttu-id="e6de4-208">1.1.0</span><span class="sxs-lookup"><span data-stu-id="e6de4-208">1.1.0</span></span> <br> <span data-ttu-id="e6de4-209">1.1.1</span><span class="sxs-lookup"><span data-stu-id="e6de4-209">1.1.1</span></span> <br> <span data-ttu-id="e6de4-210">1.1.2-alfa</span><span class="sxs-lookup"><span data-stu-id="e6de4-210">1.1.2-alpha</span></span> <br> <span data-ttu-id="e6de4-211">1.2.0-alfa</span><span class="sxs-lookup"><span data-stu-id="e6de4-211">1.2.0-alpha</span></span> | <span data-ttu-id="e6de4-212">1.1.1</span><span class="sxs-lookup"><span data-stu-id="e6de4-212">1.1.1</span></span> | <span data-ttu-id="e6de4-213">Versione stabile più elevata che rispetta il modello specificato.</span><span class="sxs-lookup"><span data-stu-id="e6de4-213">The highest stable version that respects the specified pattern.</span></span>|
| <span data-ttu-id="e6de4-214">\* - \*</span><span class="sxs-lookup"><span data-stu-id="e6de4-214">\* - \*</span></span> | <span data-ttu-id="e6de4-215">1.1.0</span><span class="sxs-lookup"><span data-stu-id="e6de4-215">1.1.0</span></span> <br> <span data-ttu-id="e6de4-216">1.1.1</span><span class="sxs-lookup"><span data-stu-id="e6de4-216">1.1.1</span></span> <br> <span data-ttu-id="e6de4-217">1.1.2-alfa</span><span class="sxs-lookup"><span data-stu-id="e6de4-217">1.1.2-alpha</span></span> <br> <span data-ttu-id="e6de4-218">1.3.0-beta</span><span class="sxs-lookup"><span data-stu-id="e6de4-218">1.3.0-beta</span></span>  | <span data-ttu-id="e6de4-219">1.3.0-beta</span><span class="sxs-lookup"><span data-stu-id="e6de4-219">1.3.0-beta</span></span> | <span data-ttu-id="e6de4-220">Versione più recente, incluse le versioni non stabili.</span><span class="sxs-lookup"><span data-stu-id="e6de4-220">The highest version including the not stable versions.</span></span> | <span data-ttu-id="e6de4-221">Disponibile in Visual Studio versione 16,6, NuGet versione 5,6, .NET Core SDK versione 3.1.300</span><span class="sxs-lookup"><span data-stu-id="e6de4-221">Available in Visual Studio version 16.6, NuGet version 5.6, .NET Core SDK version 3.1.300</span></span> |
| <span data-ttu-id="e6de4-222">1,1. *-*</span><span class="sxs-lookup"><span data-stu-id="e6de4-222">1.1.\* - \*</span></span> | <span data-ttu-id="e6de4-223">1.1.0</span><span class="sxs-lookup"><span data-stu-id="e6de4-223">1.1.0</span></span> <br> <span data-ttu-id="e6de4-224">1.1.1</span><span class="sxs-lookup"><span data-stu-id="e6de4-224">1.1.1</span></span> <br> <span data-ttu-id="e6de4-225">1.1.2-alfa</span><span class="sxs-lookup"><span data-stu-id="e6de4-225">1.1.2-alpha</span></span> <br> <span data-ttu-id="e6de4-226">1.1.2-beta</span><span class="sxs-lookup"><span data-stu-id="e6de4-226">1.1.2-beta</span></span> <br> <span data-ttu-id="e6de4-227">1.3.0-beta</span><span class="sxs-lookup"><span data-stu-id="e6de4-227">1.3.0-beta</span></span>  | <span data-ttu-id="e6de4-228">1.1.2-beta</span><span class="sxs-lookup"><span data-stu-id="e6de4-228">1.1.2-beta</span></span> | <span data-ttu-id="e6de4-229">La versione più recente che rispetta il modello e include le versioni non stabili.</span><span class="sxs-lookup"><span data-stu-id="e6de4-229">The highest version respecting the pattern and including the not stable versions.</span></span> | <span data-ttu-id="e6de4-230">Disponibile in Visual Studio versione 16,6, NuGet versione 5,6, .NET Core SDK versione 3.1.300</span><span class="sxs-lookup"><span data-stu-id="e6de4-230">Available in Visual Studio version 16.6, NuGet version 5.6, .NET Core SDK version 3.1.300</span></span> |

<span data-ttu-id="e6de4-231">**Riferimenti in `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="e6de4-231">**References in `packages.config`:**</span></span>

<span data-ttu-id="e6de4-232">In `packages.config` ogni dipendenza viene elencata con un attributo `version` esatto usato durante il ripristino dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="e6de4-232">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="e6de4-233">L'attributo `allowedVersions` viene usato solo durante le operazioni di aggiornamento per vincolare le versioni per l'aggiornamento del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e6de4-233">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="e6de4-234">**Riferimenti nei file `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="e6de4-234">**References in `.nuspec` files**</span></span>

<span data-ttu-id="e6de4-235">L'attributo `version` in un elemento `<dependency>` descrive le versioni di intervallo accettabili per una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="e6de4-235">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="e6de4-236">Numeri di versione normalizzati</span><span class="sxs-lookup"><span data-stu-id="e6de4-236">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="e6de4-237">Si tratta di una modifica di rilievo per NuGet 3.4 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="e6de4-237">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="e6de4-238">Quando si ottengono pacchetti da un repository durante le operazioni di installazione, reinstallazione o ripristino, NuGet 3.4+ gestisce i numeri di versione come segue:</span><span class="sxs-lookup"><span data-stu-id="e6de4-238">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="e6de4-239">Gli zeri iniziali vengono rimossi dai numeri di versione:</span><span class="sxs-lookup"><span data-stu-id="e6de4-239">Leading zeroes are removed from version numbers:</span></span>

  <span data-ttu-id="e6de4-240">1,00 viene considerato come 1,0 1.01.1 viene considerato come 1.1.1 1.00.0.1 viene considerato 1.0.0.1</span><span class="sxs-lookup"><span data-stu-id="e6de4-240">1.00 is treated as 1.0 1.01.1 is treated as 1.1.1 1.00.0.1 is treated as 1.0.0.1</span></span>

- <span data-ttu-id="e6de4-241">uno zero nella quarta parte del numero di versione verrà omesso</span><span class="sxs-lookup"><span data-stu-id="e6de4-241">A zero in the fourth part of the version number will be omitted</span></span>

  <span data-ttu-id="e6de4-242">1.0.0.0 viene considerato come 1.0.0 1.0.01.0 viene considerato come 1.0.1</span><span class="sxs-lookup"><span data-stu-id="e6de4-242">1.0.0.0 is treated as 1.0.0 1.0.01.0 is treated as 1.0.1</span></span>

- <span data-ttu-id="e6de4-243">SemVer i metadati di compilazione 2.0.0 sono stati rimossi</span><span class="sxs-lookup"><span data-stu-id="e6de4-243">SemVer 2.0.0 build metadata is removed</span></span>

  <span data-ttu-id="e6de4-244">1.0.7 + r3456 viene considerato 1.0.7</span><span class="sxs-lookup"><span data-stu-id="e6de4-244">1.0.7+r3456 is treated as 1.0.7</span></span>

<span data-ttu-id="e6de4-245">Le operazioni `pack` e `restore` normalizzano le versioni quando possibile.</span><span class="sxs-lookup"><span data-stu-id="e6de4-245">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="e6de4-246">Per i pacchetti già compilati, la normalizzazione non influisce sui numeri di versione dei pacchetti stessi, ma influisce solo sul modo in cui NuGet abbina le versioni durante la risoluzione delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="e6de4-246">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="e6de4-247">Tuttavia, i repository di pacchetti NuGet devono gestire questi valori nello stesso modo di NuGet per evitare la duplicazione della versione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e6de4-247">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="e6de4-248">Un repository che contiene la versione *1.0* di un pacchetto non deve inoltre ospitare la versione *1.0.0* come pacchetto separato e diverso.</span><span class="sxs-lookup"><span data-stu-id="e6de4-248">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>

## <a name="where-nugetversion-diverges-from-semantic-versioning"></a><span data-ttu-id="e6de4-249">Dove NuGetVersion diverge dal controllo delle versioni semantico</span><span class="sxs-lookup"><span data-stu-id="e6de4-249">Where NuGetVersion diverges from Semantic Versioning</span></span>

<span data-ttu-id="e6de4-250">Se si vuole a livello usare le versioni dei pacchetti NuGet, è consigliabile usare [il pacchetto NuGet. Versioning](https://www.nuget.org/packages/NuGet.Versioning).</span><span class="sxs-lookup"><span data-stu-id="e6de4-250">If you want to programatically use NuGet package versions, it is strongly recommended to use [the package NuGet.Versioning](https://www.nuget.org/packages/NuGet.Versioning).</span></span> <span data-ttu-id="e6de4-251">Il metodo statico `NuGetVersion.Parse(string)` può essere utilizzato per analizzare le stringhe di versione e `VersionComparer` può essere utilizzato per ordinare le `NuGetVersion` istanze.</span><span class="sxs-lookup"><span data-stu-id="e6de4-251">The static method `NuGetVersion.Parse(string)` can be used to parse the version strings, and `VersionComparer` can be used to sort `NuGetVersion` instances.</span></span>

<span data-ttu-id="e6de4-252">Se si implementa la funzionalità NuGet in un linguaggio che non viene eseguito in .NET, di seguito è riportato un elenco noto di differenze tra `NuGetVersion` e il controllo delle versioni semantico e i motivi per cui una libreria di controllo delle versioni semantica esistente potrebbe non funzionare per i pacchetti già pubblicati in NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="e6de4-252">If you are implementing NuGet functionality in a language that does not run on .NET, here are the known list of differences between `NuGetVersion` and Semantic Versioning, and the reasons why an existing Semantic Versioning library might not work for packages already published on nuget.org.</span></span>

1. <span data-ttu-id="e6de4-253">`NuGetVersion` supporta un segmento di versione 4, `Revision` , per essere compatibile con o un superset di, [`System.Version`](/dotnet/api/system.version) .</span><span class="sxs-lookup"><span data-stu-id="e6de4-253">`NuGetVersion` supports a 4th version segment, `Revision`, to be compatible with, or a superset of, [`System.Version`](/dotnet/api/system.version).</span></span> <span data-ttu-id="e6de4-254">Pertanto, escludendo le etichette di versione provvisoria e dei metadati, una stringa di versione è `Major.Minor.Patch.Revision` .</span><span class="sxs-lookup"><span data-stu-id="e6de4-254">Therefore, excluding prerelease and metadata labels, a version string is `Major.Minor.Patch.Revision`.</span></span> <span data-ttu-id="e6de4-255">Come per la normalizzazione delle versioni descritta in precedenza, se `Revision` è zero, viene omesso dalla stringa di versione normalizzata.</span><span class="sxs-lookup"><span data-stu-id="e6de4-255">As per version normalization described above, if `Revision` is zero, it is omit from the normalized version string.</span></span>
2. <span data-ttu-id="e6de4-256">`NuGetVersion` richiede solo il segmento principale da definire.</span><span class="sxs-lookup"><span data-stu-id="e6de4-256">`NuGetVersion` only requires the major segment to be defined.</span></span> <span data-ttu-id="e6de4-257">Tutti gli altri sono facoltativi e sono equivalenti a zero.</span><span class="sxs-lookup"><span data-stu-id="e6de4-257">All others are optional, and are equivalent to zero.</span></span> <span data-ttu-id="e6de4-258">Ciò significa che `1` , `1.0` , `1.0.0` e `1.0.0.0` sono tutti accettati e uguali.</span><span class="sxs-lookup"><span data-stu-id="e6de4-258">This means that `1`, `1.0`, `1.0.0`, and `1.0.0.0` are all accepted and equal.</span></span>
3. <span data-ttu-id="e6de4-259">`NuGetVersion` Usa il case non attiva confronti di stringhe per i componenti di versioni non definitive.</span><span class="sxs-lookup"><span data-stu-id="e6de4-259">`NuGetVersion` uses case insenstive string comparisons for pre-release components.</span></span> <span data-ttu-id="e6de4-260">Ciò significa che `1.0.0-alpha` e `1.0.0-Alpha` sono uguali.</span><span class="sxs-lookup"><span data-stu-id="e6de4-260">This means that `1.0.0-alpha` and `1.0.0-Alpha` are equal.</span></span>
