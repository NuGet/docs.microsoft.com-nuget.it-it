---
title: Versioni non definitive nei pacchetti NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: df6a366a-22c1-47bb-8017-18231311ce88
description: Linee guida per la compilazione di versioni non definitive dei pacchetti
keywords: controllo delle versioni, controllo delle versioni del pacchetto NuGet, versioni non definitive NuGet, pacchetti in versione non definitiva NuGet, versioni di anteprima dei pacchetti, versioni dei pacchetti RC, versioni dei pacchetti beta, controllo delle versioni semantico NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 07cb9b9bdeeea6f283e95a11a06d7f2043c9b17c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="42be5-104">Compilazione di versioni non definitive dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="42be5-104">Building pre-release packages</span></span>

<span data-ttu-id="42be5-105">Ogni volta che si rilascia un pacchetto aggiornato con un nuovo numero di versione, NuGet considera tale versione l'ultima versione stabile, come illustrato, ad esempio, nell'interfaccia utente di Gestione pacchetti all'interno di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="42be5-105">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Interfaccia utente di Gestione pacchetti che mostra l'ultima versione stabile](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="42be5-107">Una versione stabile è una versione considerata sufficientemente affidabile da poter essere usata in ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="42be5-107">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="42be5-108">L'ultima versione stabile è anche quella che verrà installata come aggiornamento del pacchetto oppure durante il ripristino del pacchetto (soggetto a vincoli, come descritto in [Reinstallazione e aggiornamento di pacchetti](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="42be5-108">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="42be5-109">Per supportare il ciclo di vita di rilascio del software, NuGet 1.6 e versioni successive consentono la distribuzione di pacchetti in versione non definitiva, in cui il numero di versione include un suffisso per il controllo delle versioni semantico, ad esempio `-alpha`, `-beta` o `-rc`.</span><span class="sxs-lookup"><span data-stu-id="42be5-109">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="42be5-110">Per altre informazioni, vedere [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="42be5-110">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="42be5-111">È possibile specificare tali versioni in due modi:</span><span class="sxs-lookup"><span data-stu-id="42be5-111">You can specify such versions in two ways:</span></span>

- <span data-ttu-id="42be5-112">File `.nuspec`: includere il suffisso di versione semantico nell'elemento `version`:</span><span class="sxs-lookup"><span data-stu-id="42be5-112">`.nuspec` file: include the semantic version suffix in the `version` element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

- <span data-ttu-id="42be5-113">Attributi dell'assembly: quando si compila un pacchetto da un progetto di Visual Studio (`.csproj` o `.vbproj`), usare `AssemblyInformationalVersionAttribute` per specificare la versione:</span><span class="sxs-lookup"><span data-stu-id="42be5-113">Assembly attributes: when building a package from a Visual Studio project (`.csproj` or `.vbproj`), use the `AssemblyInformationalVersionAttribute` to specify the version:</span></span>

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    <span data-ttu-id="42be5-114">NuGet preleva questo valore anziché quello specificato nell'attributo `AssemblyVersion`, che non supporta il versionamento semantico.</span><span class="sxs-lookup"><span data-stu-id="42be5-114">NuGet picks up this value instead of the one specified in the `AssemblyVersion` attribute, which does not support semantic versioning.</span></span>

<span data-ttu-id="42be5-115">Quando si è pronti per rilasciare una versione stabile, è sufficiente rimuovere il suffisso e il pacchetto ottiene la precedenza rispetto a qualsiasi altra versione non definitiva.</span><span class="sxs-lookup"><span data-stu-id="42be5-115">When you’re ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="42be5-116">Vedere di nuovo [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="42be5-116">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>


## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="42be5-117">Installazione e aggiornamento di pacchetti in versione non definitiva</span><span class="sxs-lookup"><span data-stu-id="42be5-117">Installing and updating pre-release packages</span></span>

<span data-ttu-id="42be5-118">Per impostazione predefinita, NuGet non include le versioni non definitive quando si lavora con i pacchetti, ma è possibile modificare questo comportamento come segue:</span><span class="sxs-lookup"><span data-stu-id="42be5-118">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="42be5-119">**Interfaccia utente di Gestione pacchetti in Visual Studio**: nell'interfaccia utente di **Gestisci pacchetti NuGet** selezionare la casella di controllo **Includi versione preliminare**:</span><span class="sxs-lookup"><span data-stu-id="42be5-119">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Casella di controllo Includi versione preliminare in Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="42be5-121">La selezione o la deselezione di questa casella di controllo aggiorna l'interfaccia utente di Gestione pacchetti e l'elenco delle versioni disponibili che è possibile installare.</span><span class="sxs-lookup"><span data-stu-id="42be5-121">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="42be5-122">**Console di Gestione pacchetti**: usare l'opzione `-IncludePrerelease` con i comandi `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` e `Update-Package`.</span><span class="sxs-lookup"><span data-stu-id="42be5-122">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="42be5-123">Vedere [Informazioni di riferimento su PowerShell](../tools/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="42be5-123">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="42be5-124">**Interfaccia della riga di comando di NuGet**: usare l'opzione `-prerelease` con i comandi `install`, `update`, `delete` e `mirror`.</span><span class="sxs-lookup"><span data-stu-id="42be5-124">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="42be5-125">Vedere [NuGet CLI reference](../tools/nuget-exe-cli-reference.md) (Informazioni di riferimento sull'interfaccia della riga di comando di NuGet).</span><span class="sxs-lookup"><span data-stu-id="42be5-125">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>


## <a name="semantic-versioning"></a><span data-ttu-id="42be5-126">Versionamento semantico</span><span class="sxs-lookup"><span data-stu-id="42be5-126">Semantic versioning</span></span>

<span data-ttu-id="42be5-127">La [convenzione di versionamento semantico o SemVer](http://semver.org/spec/v1.0.0.html) descrive come usare le stringhe nei numeri di versione per indicare il significato del codice sottostante.</span><span class="sxs-lookup"><span data-stu-id="42be5-127">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey they meaning of the underlying code.</span></span>

<span data-ttu-id="42be5-128">In questa convenzione, ogni versione è composta di tre parti, `Major.Minor.Patch`, con il significato seguente:</span><span class="sxs-lookup"><span data-stu-id="42be5-128">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="42be5-129">`Major`: modifiche importanti</span><span class="sxs-lookup"><span data-stu-id="42be5-129">`Major`: Breaking changes</span></span>
- <span data-ttu-id="42be5-130">`Minor`: nuove funzionalità, ma compatibili con le versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="42be5-130">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="42be5-131">`Patch`: solo correzioni di bug compatibili con le versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="42be5-131">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="42be5-132">Le versioni non definitive vengono quindi contrassegnate aggiungendo un trattino e una stringa dopo il numero di patch.</span><span class="sxs-lookup"><span data-stu-id="42be5-132">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="42be5-133">Tecnicamente, è possibile usare *qualsiasi* stringa dopo il trattino e NuGet considererà il pacchetto come in versione non definitiva.</span><span class="sxs-lookup"><span data-stu-id="42be5-133">Technically speaking, you can use *any *string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="42be5-134">NuGet visualizza quindi il numero di versione completo nell'interfaccia utente applicabile, lasciando ai consumer l'interpretazione del significato.</span><span class="sxs-lookup"><span data-stu-id="42be5-134">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="42be5-135">Tenendo conto di questo aspetto, è in genere consigliabile seguire convenzioni di denominazione riconosciute, come le seguenti:</span><span class="sxs-lookup"><span data-stu-id="42be5-135">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="42be5-136">`-alpha`: versione alfa, usata in genere per lavori in corso e sperimentazione</span><span class="sxs-lookup"><span data-stu-id="42be5-136">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="42be5-137">`-beta`: versione beta, in genere completa dal punto di vista funzionale per il successivo rilascio pianificato, ma può contenere bug noti.</span><span class="sxs-lookup"><span data-stu-id="42be5-137">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="42be5-138">`-rc`: versione finale candidata, in genere potenzialmente finale (stabile) se non emergono bug significativi.</span><span class="sxs-lookup"><span data-stu-id="42be5-138">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="42be5-139">NuGet non supporta i numeri di versione non definitiva [compatibili con SemVer (v 2.0.0)](http://semver.org/spec/v2.0.0.html) con la notazione del punto, come in `1.0.1-build.23`.</span><span class="sxs-lookup"><span data-stu-id="42be5-139">NuGet does not support [SemVer-compatible (v2.0.0)](http://semver.org/spec/v2.0.0.html) prerelease numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="42be5-140">È possibile usare un formato come `1.0.1-build23`, ma verrà sempre considerata una versione non definitiva.</span><span class="sxs-lookup"><span data-stu-id="42be5-140">You can use a form like `1.0.1-build23` but this is always considered a pre-release version.</span></span>

<span data-ttu-id="42be5-141">Indipendentemente dai suffissi usati, tuttavia, NuGet stabilirà sempre la precedenza in ordine alfabetico inverso:</span><span class="sxs-lookup"><span data-stu-id="42be5-141">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta12
1.0.1-beta05
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
```

<span data-ttu-id="42be5-142">Come illustrato, la versione senza suffisso avrà sempre la precedenza rispetto alle versioni non definitive.</span><span class="sxs-lookup"><span data-stu-id="42be5-142">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="42be5-143">Si noti inoltre che se si usano suffissi numerici con i tag di versione non definitiva che potrebbero usare numeri a due cifre (o più), è buona norma usare zeri iniziali come in beta01 e beta05 per assicurare un ordinamento corretto con l'aumentare dei numeri.</span><span class="sxs-lookup"><span data-stu-id="42be5-143">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>
