---
title: Informazioni di riferimento sulle versioni dei pacchetti NuGet
description: Informazioni dettagliate su come specificare i numeri di versione e gli intervalli per altri pacchetti da cui dipende un pacchetto NuGet e sulla modalità di installazione delle dipendenze.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520351"
---
# <a name="package-versioning"></a><span data-ttu-id="1885f-103">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="1885f-103">Package versioning</span></span>

<span data-ttu-id="1885f-104">A un pacchetto specifico viene sempre fatto riferimento usando l'identificatore del pacchetto e un numero di versione esatto.</span><span class="sxs-lookup"><span data-stu-id="1885f-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="1885f-105">Per [Entity Framework](https://www.nuget.org/packages/EntityFramework/) su nuget.org, ad esempio, sono disponibili alcune decine di pacchetti specifici, compresi tra la versione *4.1.10311* e la versione *6.1.3* (la versione stabile più recente) e svariate versioni non definitive come *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="1885f-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="1885f-106">Quando si crea un pacchetto, si assegna un numero di versione specifico con un suffisso di testo per la versione non definitiva facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1885f-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="1885f-107">Quando si utilizzano i pacchetti, invece, è possibile specificare un numero di versione esatto o un intervallo di versioni accettabili.</span><span class="sxs-lookup"><span data-stu-id="1885f-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="1885f-108">In questo argomento</span><span class="sxs-lookup"><span data-stu-id="1885f-108">In this topic:</span></span>

- <span data-ttu-id="1885f-109">[Nozioni di base sulle versioni](#version-basics), inclusi i suffissi di versione non definitiva.</span><span class="sxs-lookup"><span data-stu-id="1885f-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="1885f-110">Intervalli di versione e caratteri jolly</span><span class="sxs-lookup"><span data-stu-id="1885f-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="1885f-111">Numeri di versione normalizzati</span><span class="sxs-lookup"><span data-stu-id="1885f-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="1885f-112">Nozioni di base sulle versioni</span><span class="sxs-lookup"><span data-stu-id="1885f-112">Version basics</span></span>

<span data-ttu-id="1885f-113">Un numero di versione specifico è nel formato *Principale.Secondaria.Patch[-Suffisso]* , dove i singoli componenti hanno i significati seguenti:</span><span class="sxs-lookup"><span data-stu-id="1885f-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="1885f-114">*Principale*: Modifiche che causano un'interruzione</span><span class="sxs-lookup"><span data-stu-id="1885f-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="1885f-115">*Secondaria*: nuove funzionalità, ma compatibili con le versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="1885f-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="1885f-116">*Patch*: solo correzioni di bug compatibili con le versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="1885f-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="1885f-117">*-Suffisso* (facoltativo): un trattino seguito da una stringa che indica una versione non definitiva (in base alla [convenzione Semantic Versioning o SemVer 1.0](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="1885f-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="1885f-118">**Esempi:**</span><span class="sxs-lookup"><span data-stu-id="1885f-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="1885f-119">nuget.org rifiuta il caricamento di un pacchetto senza un numero di versione esatto.</span><span class="sxs-lookup"><span data-stu-id="1885f-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="1885f-120">La versione deve essere specificata nel file `.nuspec` o nel file di progetto usato per creare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1885f-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="1885f-121">Versioni non definitive</span><span class="sxs-lookup"><span data-stu-id="1885f-121">Pre-release versions</span></span>

<span data-ttu-id="1885f-122">Dal punto di vista tecnico, i creatori di pacchetti possono usare qualsiasi stringa come suffisso per indicare una versione non definitiva, perché NuGet considera una versione con questa caratteristica non definitiva senza altre interpretazioni.</span><span class="sxs-lookup"><span data-stu-id="1885f-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="1885f-123">In altre parole, NuGet visualizza la stringa di versione completa in qualsiasi interfaccia utente, lasciando l'interpretazione del significato del suffisso all'utente.</span><span class="sxs-lookup"><span data-stu-id="1885f-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="1885f-124">Ciò premesso, gli sviluppatori di pacchetti seguono generalmente convenzioni di denominazione riconosciute:</span><span class="sxs-lookup"><span data-stu-id="1885f-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="1885f-125">`-alpha`: versione alfa, usata in genere per lavori in corso e sperimentazione.</span><span class="sxs-lookup"><span data-stu-id="1885f-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="1885f-126">`-beta`: versione beta, in genere completa dal punto di vista funzionale per il successivo rilascio pianificato, ma può contenere bug noti.</span><span class="sxs-lookup"><span data-stu-id="1885f-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="1885f-127">`-rc`: versione finale candidata, in genere potenzialmente finale (stabile) se non emergono bug significativi.</span><span class="sxs-lookup"><span data-stu-id="1885f-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="1885f-128">NuGet 4.3.0+ supporta [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), ovvero numeri di versione non definitiva con la notazione con punto, come in *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="1885f-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="1885f-129">La notazione con punto non è supportata con le versioni di NuGet precedenti alla versione 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="1885f-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="1885f-130">È possibile usare un formato come *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="1885f-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="1885f-131">Se durante la risoluzione dei riferimenti al pacchetto risultano più versioni del pacchetto che differiscono solo per il suffisso, NuGet sceglie prima una versione senza suffisso, quindi applica la precedenza alle versioni non definitive in ordine alfabetico inverso.</span><span class="sxs-lookup"><span data-stu-id="1885f-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="1885f-132">Le versioni seguenti, ad esempio, verrebbero scelte nell'esatto ordine indicato:</span><span class="sxs-lookup"><span data-stu-id="1885f-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="1885f-133">Semantic Versioning 2.0.0</span><span class="sxs-lookup"><span data-stu-id="1885f-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="1885f-134">Con NuGet 4.3.0+ e Visual Studio 2017 versione 15.3+, NuGet supporta la convenzione [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="1885f-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="1885f-135">Certe regole semantiche di SemVer 2.0.0 non sono supportate nei client meno recenti.</span><span class="sxs-lookup"><span data-stu-id="1885f-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="1885f-136">NuGet considera la versione di un pacchetto come specifica di SemVer 2.0.0 se una delle affermazioni seguenti è vera:</span><span class="sxs-lookup"><span data-stu-id="1885f-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="1885f-137">L'etichetta della versione non definitiva è separata da punti, ad esempio *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="1885f-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="1885f-138">La versione include metadati di compilazione, ad esempio *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="1885f-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="1885f-139">Per nuget.org, un pacchetto viene definito come pacchetto SemVer 2.0.0 se una delle affermazioni seguenti è vera:</span><span class="sxs-lookup"><span data-stu-id="1885f-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="1885f-140">La versione del pacchetto è conforme a SemVer 2.0.0 ma non è conforme a SemVer 1.0.0, come definito sopra.</span><span class="sxs-lookup"><span data-stu-id="1885f-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="1885f-141">Uno degli intervalli di versioni delle dipendenze del pacchetto ha una versione minima o massima conforme a SemVer 2.0.0 ma non conforme a SemVer 1.0.0, definita in precedenza. Ad esempio, *[1.0.0-alpha.1, )* .</span><span class="sxs-lookup"><span data-stu-id="1885f-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="1885f-142">Se si carica un pacchetto specifico di SemVer 2.0.0 in nuget.org, il pacchetto è invisibile ai client meno recenti e disponibile solo per i client NuGet seguenti:</span><span class="sxs-lookup"><span data-stu-id="1885f-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="1885f-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="1885f-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="1885f-144">Visual Studio 2017 versione 15.3+</span><span class="sxs-lookup"><span data-stu-id="1885f-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="1885f-145">Visual Studio 2015 con [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="1885f-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="1885f-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="1885f-146">dotnet</span></span>
  - <span data-ttu-id="1885f-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="1885f-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="1885f-148">Client di terze parti:</span><span class="sxs-lookup"><span data-stu-id="1885f-148">Third-party clients:</span></span>

- <span data-ttu-id="1885f-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="1885f-149">JetBrains Rider</span></span>
- <span data-ttu-id="1885f-150">Paket versione 5.0 +</span><span class="sxs-lookup"><span data-stu-id="1885f-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="1885f-151">Intervalli di versione e caratteri jolly</span><span class="sxs-lookup"><span data-stu-id="1885f-151">Version ranges and wildcards</span></span>

<span data-ttu-id="1885f-152">Quando si fa riferimento alle dipendenze dei pacchetti, NuGet supporta l'uso della notazione con intervallo per specificare gli intervalli di versione, riepilogati come segue:</span><span class="sxs-lookup"><span data-stu-id="1885f-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="1885f-153">Notation</span><span class="sxs-lookup"><span data-stu-id="1885f-153">Notation</span></span> | <span data-ttu-id="1885f-154">Regola applicata</span><span class="sxs-lookup"><span data-stu-id="1885f-154">Applied rule</span></span> | <span data-ttu-id="1885f-155">DESCRIZIONE</span><span class="sxs-lookup"><span data-stu-id="1885f-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="1885f-156">1.0</span><span class="sxs-lookup"><span data-stu-id="1885f-156">1.0</span></span> | <span data-ttu-id="1885f-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="1885f-157">x ≥ 1.0</span></span> | <span data-ttu-id="1885f-158">Versione minima, inclusiva</span><span class="sxs-lookup"><span data-stu-id="1885f-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="1885f-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="1885f-159">(1.0,)</span></span> | <span data-ttu-id="1885f-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="1885f-160">x > 1.0</span></span> | <span data-ttu-id="1885f-161">Versione minima, esclusiva</span><span class="sxs-lookup"><span data-stu-id="1885f-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="1885f-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="1885f-162">[1.0]</span></span> | <span data-ttu-id="1885f-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="1885f-163">x == 1.0</span></span> | <span data-ttu-id="1885f-164">Corrispondenza esatta della versione</span><span class="sxs-lookup"><span data-stu-id="1885f-164">Exact version match</span></span> |
| <span data-ttu-id="1885f-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="1885f-165">(,1.0]</span></span> | <span data-ttu-id="1885f-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="1885f-166">x ≤ 1.0</span></span> | <span data-ttu-id="1885f-167">Versione massima, inclusiva</span><span class="sxs-lookup"><span data-stu-id="1885f-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="1885f-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="1885f-168">(,1.0)</span></span> | <span data-ttu-id="1885f-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="1885f-169">x < 1.0</span></span> | <span data-ttu-id="1885f-170">Versione massima, esclusiva</span><span class="sxs-lookup"><span data-stu-id="1885f-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="1885f-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="1885f-171">[1.0,2.0]</span></span> | <span data-ttu-id="1885f-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="1885f-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="1885f-173">Intervallo esatto, inclusivo</span><span class="sxs-lookup"><span data-stu-id="1885f-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="1885f-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="1885f-174">(1.0,2.0)</span></span> | <span data-ttu-id="1885f-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="1885f-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="1885f-176">Intervallo esatto, esclusivo</span><span class="sxs-lookup"><span data-stu-id="1885f-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="1885f-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="1885f-177">[1.0,2.0)</span></span> | <span data-ttu-id="1885f-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="1885f-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="1885f-179">Versione minima inclusiva e massima esclusiva mista</span><span class="sxs-lookup"><span data-stu-id="1885f-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="1885f-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="1885f-180">(1.0)</span></span>    | <span data-ttu-id="1885f-181">non valido</span><span class="sxs-lookup"><span data-stu-id="1885f-181">invalid</span></span> | <span data-ttu-id="1885f-182">non valido</span><span class="sxs-lookup"><span data-stu-id="1885f-182">invalid</span></span> |

<span data-ttu-id="1885f-183">Quando si usa il formato PackageReference, NuGet supporta anche l'uso di una notazione con caratteri jolly, \*, per le parti del numero per versione principale, secondaria, patch e suffisso di versione non definitiva.</span><span class="sxs-lookup"><span data-stu-id="1885f-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="1885f-184">I caratteri jolly non sono supportati con il formato `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="1885f-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="1885f-185">Gli intervalli di versione in PackageReference includono le versioni non definitive.</span><span class="sxs-lookup"><span data-stu-id="1885f-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="1885f-186">Per impostazione predefinita, le versioni mobili non risolvono le versioni non definitive se non con consenso esplicito.</span><span class="sxs-lookup"><span data-stu-id="1885f-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="1885f-187">Per lo stato della richiesta di funzionalità correlata, vedere il [problema 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="1885f-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="1885f-188">Esempi</span><span class="sxs-lookup"><span data-stu-id="1885f-188">Examples</span></span>

<span data-ttu-id="1885f-189">Specificare sempre una versione o un intervallo di versioni per le dipendenze dei pacchetti nei file di progetto, nei file `packages.config` e nei file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="1885f-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="1885f-190">Senza una versione o un intervallo di versioni, NuGet 2.8.x e versioni precedenti scelgono la versione più recente del pacchetto disponibile durante la risoluzione di una dipendenza, mentre NuGet 3.x e versioni successive scelgono la versione del pacchetto più bassa.</span><span class="sxs-lookup"><span data-stu-id="1885f-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="1885f-191">La specifica di una versione o di un intervallo di versioni evita questa incertezza.</span><span class="sxs-lookup"><span data-stu-id="1885f-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="1885f-192">Riferimenti nei file di progetto (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="1885f-192">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="1885f-193">**Riferimenti in `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="1885f-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="1885f-194">In `packages.config` ogni dipendenza viene elencata con un attributo `version` esatto usato durante il ripristino dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1885f-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="1885f-195">L'attributo `allowedVersions` viene usato solo durante le operazioni di aggiornamento per vincolare le versioni per l'aggiornamento del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1885f-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="1885f-196">**Riferimenti nei file `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="1885f-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="1885f-197">L'attributo `version` in un elemento `<dependency>` descrive le versioni di intervallo accettabili per una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="1885f-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="1885f-198">Numeri di versione normalizzati</span><span class="sxs-lookup"><span data-stu-id="1885f-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="1885f-199">Si tratta di una modifica di rilievo per NuGet 3.4 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="1885f-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="1885f-200">Quando si ottengono pacchetti da un repository durante le operazioni di installazione, reinstallazione o ripristino, NuGet 3.4+ gestisce i numeri di versione come segue:</span><span class="sxs-lookup"><span data-stu-id="1885f-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="1885f-201">Gli zeri iniziali vengono rimossi dai numeri di versione:</span><span class="sxs-lookup"><span data-stu-id="1885f-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="1885f-202">uno zero nella quarta parte del numero di versione verrà omesso</span><span class="sxs-lookup"><span data-stu-id="1885f-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="1885f-203">Le operazioni `pack` e `restore` normalizzano le versioni quando possibile.</span><span class="sxs-lookup"><span data-stu-id="1885f-203">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="1885f-204">Per i pacchetti già compilati, la normalizzazione non influisce sui numeri di versione dei pacchetti stessi, ma influisce solo sul modo in cui NuGet abbina le versioni durante la risoluzione delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="1885f-204">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="1885f-205">Tuttavia, i repository di pacchetti NuGet devono gestire questi valori nello stesso modo di NuGet per evitare la duplicazione della versione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1885f-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="1885f-206">Un repository che contiene la versione *1.0* di un pacchetto non deve inoltre ospitare la versione *1.0.0* come pacchetto separato e diverso.</span><span class="sxs-lookup"><span data-stu-id="1885f-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>