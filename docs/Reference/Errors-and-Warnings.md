---
title: Ripristino NuGet errori e avvisi riferimento | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b76b8a00-7155-4163-b533-894086d2ef78
description: Riferimento complete per avvisi ed errori generati da NuGet durante il ripristino del pacchetto
keywords: NuGet errori, avvisi NuGet, diagnostica
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3423e30eae07ff0c70a010576b8e701be027b847
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="errors-and-warnings"></a><span data-ttu-id="b6d99-104">Errori e avvisi</span><span class="sxs-lookup"><span data-stu-id="b6d99-104">Errors and warnings</span></span>

<span data-ttu-id="b6d99-105">In NuGet 4.3.0, errori e avvisi sono numerati come descritto in questo argomento e forniscono informazioni dettagliate che consentono di risolvere i problemi che interessano.</span><span class="sxs-lookup"><span data-stu-id="b6d99-105">In NuGet 4.3.0, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span> 

<span data-ttu-id="b6d99-106">Gli errori e avvisi elencati di seguito sono disponibili solo con [basato su PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) progetti e NuGet 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="b6d99-106">The errors and warnings listed here are available only with [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) projects and NuGet 4.3.0.</span></span> <span data-ttu-id="b6d99-107">NuGet anche rispetta la proprietà di MSBuild per l'esclusione di avvisi o li elevare a errori.</span><span class="sxs-lookup"><span data-stu-id="b6d99-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="b6d99-108">Per ulteriori informazioni, vedere [procedura: esclusione di avvisi del compilatore](https://docs.microsoft.com/visualstudio/ide/how-to-suppress-compiler-warnings) nella documentazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6d99-108">For more information, see [How to: Suppress Compiler Warnings](https://docs.microsoft.com/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="b6d99-109">**Errori**</span><span class="sxs-lookup"><span data-stu-id="b6d99-109">**Errors**</span></span>

| <span data-ttu-id="b6d99-110">Gruppo</span><span class="sxs-lookup"><span data-stu-id="b6d99-110">Group</span></span> | <span data-ttu-id="b6d99-111">Numeri di errore</span><span class="sxs-lookup"><span data-stu-id="b6d99-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="b6d99-112">Errori di input non validi</span><span class="sxs-lookup"><span data-stu-id="b6d99-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="b6d99-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="b6d99-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="b6d99-114">Errori di pacchetto e progetto mancanti</span><span class="sxs-lookup"><span data-stu-id="b6d99-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="b6d99-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (in precedenza NU1607), [NU1108](#nu1107) (in precedenza NU1606)</span><span class="sxs-lookup"><span data-stu-id="b6d99-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1107) (previously NU1606)</span></span> |
| [<span data-ttu-id="b6d99-116">Errori di compatibilità</span><span class="sxs-lookup"><span data-stu-id="b6d99-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="b6d99-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="b6d99-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="b6d99-118">**Avvisi**</span><span class="sxs-lookup"><span data-stu-id="b6d99-118">**Warnings**</span></span>

| <span data-ttu-id="b6d99-119">Gruppo</span><span class="sxs-lookup"><span data-stu-id="b6d99-119">Group</span></span> | <span data-ttu-id="b6d99-120">Numeri di avviso</span><span class="sxs-lookup"><span data-stu-id="b6d99-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="b6d99-121">Avvisi di input non validi</span><span class="sxs-lookup"><span data-stu-id="b6d99-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="b6d99-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="b6d99-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="b6d99-123">Avvisi di versione di pacchetto imprevisto</span><span class="sxs-lookup"><span data-stu-id="b6d99-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="b6d99-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="b6d99-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="b6d99-125">Avvisi di sistema di risoluzione dei conflitti</span><span class="sxs-lookup"><span data-stu-id="b6d99-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="b6d99-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="b6d99-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="b6d99-127">Avvisi di fallback di pacchetto</span><span class="sxs-lookup"><span data-stu-id="b6d99-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="b6d99-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="b6d99-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="b6d99-129">Feed di avvisi</span><span class="sxs-lookup"><span data-stu-id="b6d99-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="b6d99-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="b6d99-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="b6d99-131">Avvisi ed errori interni di NuGet</span><span class="sxs-lookup"><span data-stu-id="b6d99-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="b6d99-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="b6d99-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="b6d99-133">Errori di input non validi</span><span class="sxs-lookup"><span data-stu-id="b6d99-133">Invalid input errors</span></span>

<span data-ttu-id="b6d99-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="b6d99-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="b6d99-135">NU1001</span><span class="sxs-lookup"><span data-stu-id="b6d99-135">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-136">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-136">**Issue**</span></span> | <span data-ttu-id="b6d99-137">Il progetto non contiene uno o più Framework.</span><span class="sxs-lookup"><span data-stu-id="b6d99-137">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="b6d99-138">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-138">**Common causes**</span></span> | <span data-ttu-id="b6d99-139">Il progetto non contiene un `TargetFramework` o `TargetFrameworks` proprietà.</span><span class="sxs-lookup"><span data-stu-id="b6d99-139">The project doesn't contain a `TargetFramework` or `TargetFrameworks` property.</span></span> |
| <span data-ttu-id="b6d99-140">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-140">**Example message**</span></span> | <span data-ttu-id="b6d99-141">*ProjA il progetto non specifica alcun framework di destinazione in c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="b6d99-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |

### <a name="nu1002"></a><span data-ttu-id="b6d99-142">NU1002</span><span class="sxs-lookup"><span data-stu-id="b6d99-142">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-143">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-143">**Issue**</span></span> | <span data-ttu-id="b6d99-144">Combinazione non valida di input con una parola chiave non CRITTOGRAFATO.</span><span class="sxs-lookup"><span data-stu-id="b6d99-144">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="b6d99-145">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-145">**Common causes**</span></span> | <span data-ttu-id="b6d99-146">CLEAR non possono essere combinati con altri input.</span><span class="sxs-lookup"><span data-stu-id="b6d99-146">CLEAR may not be combined with other inputs.</span></span> |
| <span data-ttu-id="b6d99-147">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-147">**Example message**</span></span> | <span data-ttu-id="b6d99-148">*'CLEAR' non può essere utilizzato in combinazione con altri valori*</span><span class="sxs-lookup"><span data-stu-id="b6d99-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |

### <a name="nu1003"></a><span data-ttu-id="b6d99-149">NU1003</span><span class="sxs-lookup"><span data-stu-id="b6d99-149">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-150">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-150">**Issue**</span></span> | <span data-ttu-id="b6d99-151">`PackageTargetFallback`e `AssetTargetFallback` comportamenti diversi per la selezione di risorse e non possono essere utilizzati insieme.</span><span class="sxs-lookup"><span data-stu-id="b6d99-151">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="b6d99-152">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-152">**Common causes**</span></span> | <span data-ttu-id="b6d99-153">Entrambi `PackageTargetFallback` e `AssetTargetFallback` esiste nel progetto.</span><span class="sxs-lookup"><span data-stu-id="b6d99-153">Both `PackageTargetFallback` and `AssetTargetFallback` exist in the project.</span></span> |
| <span data-ttu-id="b6d99-154">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-154">**Example message**</span></span> | <span data-ttu-id="b6d99-155">*PackageTargetFallback e AssetTargetFallback non possono essere utilizzati insieme. Rimuovere i riferimenti di PackageTargetFallback(deprecated) dall'ambiente del progetto.*</span><span class="sxs-lookup"><span data-stu-id="b6d99-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="b6d99-156">Errori di pacchetto e progetto mancanti</span><span class="sxs-lookup"><span data-stu-id="b6d99-156">Missing package and project errors</span></span>

<span data-ttu-id="b6d99-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104 ](#nu1104)  |  [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="b6d99-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="b6d99-158">NU1100</span><span class="sxs-lookup"><span data-stu-id="b6d99-158">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-159">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-159">**Issue**</span></span> | <span data-ttu-id="b6d99-160">Un gruppo di dipendenze non essere risolto.</span><span class="sxs-lookup"><span data-stu-id="b6d99-160">A dependency group not be resolved.</span></span> <span data-ttu-id="b6d99-161">Questo è un problema generico per tipi che non sono pacchetti o progetti.</span><span class="sxs-lookup"><span data-stu-id="b6d99-161">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="b6d99-162">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-162">**Common causes**</span></span> | <span data-ttu-id="b6d99-163">Il progetto contiene una dipendenza su un elemento che non esiste.</span><span class="sxs-lookup"><span data-stu-id="b6d99-163">The project contains a dependency on an item that doesn't exist.</span></span> |
| <span data-ttu-id="b6d99-164">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-164">**Example message**</span></span> | <span data-ttu-id="b6d99-165">*Impossibile risolvere System.Missing per net45*</span><span class="sxs-lookup"><span data-stu-id="b6d99-165">*Unable to resolve System.Missing for net45*</span></span> |

### <a name="nu1101"></a><span data-ttu-id="b6d99-166">NU1101</span><span class="sxs-lookup"><span data-stu-id="b6d99-166">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-167">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-167">**Issue**</span></span> | <span data-ttu-id="b6d99-168">Impossibile trovare il pacchetto su tutte le origini.</span><span class="sxs-lookup"><span data-stu-id="b6d99-168">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="b6d99-169">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-169">**Common causes**</span></span> | <span data-ttu-id="b6d99-170">L'origine del pacchetto corretto è manca o l'identificatore del pacchetto non è corretto.</span><span class="sxs-lookup"><span data-stu-id="b6d99-170">The correct package source is missing or the package identifier is incorrect.</span></span> |
| <span data-ttu-id="b6d99-171">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-171">**Example message**</span></span> | <span data-ttu-id="b6d99-172">*Impossibile trovare il pacchetto System.Missing. Nessun pacchetto esistenti con questo id nelle origini: dotnet-core, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="b6d99-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |

### <a name="nu1102"></a><span data-ttu-id="b6d99-173">NU1102</span><span class="sxs-lookup"><span data-stu-id="b6d99-173">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-174">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-174">**Issue**</span></span> | <span data-ttu-id="b6d99-175">L'identificatore del pacchetto è stato trovato ma presente una versione all'interno dell'intervallo di dipendenza specificata non può essere una delle origini.</span><span class="sxs-lookup"><span data-stu-id="b6d99-175">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> |
| <span data-ttu-id="b6d99-176">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-176">**Common causes**</span></span> | <span data-ttu-id="b6d99-177">L'origine del pacchetto corretto è manca o l'intervallo di dipendenza non è corretto.</span><span class="sxs-lookup"><span data-stu-id="b6d99-177">The correct package source is missing or the dependency range is incorrect.</span></span> <span data-ttu-id="b6d99-178">L'intervallo può essere specificato da un pacchetto e non dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b6d99-178">The range might be specified by a package and not the user.</span></span> <span data-ttu-id="b6d99-179">L'utente potrebbe essere necessario passare a una versione disponibile se il pacchetto fa riferimento direttamente il progetto.</span><span class="sxs-lookup"><span data-stu-id="b6d99-179">The user may need to switch to an available version if this package is referenced by the project directly.</span></span> |
| <span data-ttu-id="b6d99-180">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-180">**Example message**</span></span> | <span data-ttu-id="b6d99-181">*Impossibile trovare il pacchetto NuGet.Versioning con la versione (> = 9.0.1)<br/> -30 trovare versioni in nuget.org [più vicino di versione: 4.0.0]<br/> -versioni 10 trovato in dotnet buildtools [più vicino di versione: 4.0.0-rc-2129]<br/> -9 trovato versioni in NuGetVolatile [più vicino di versione: 3.0.0-beta-00032]<br/> -0 versioni, vedere dotnet core<br/> -0 versioni, vedere dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="b6d99-181">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1103"></a><span data-ttu-id="b6d99-182">NU1103</span><span class="sxs-lookup"><span data-stu-id="b6d99-182">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-183">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-183">**Issue**</span></span> | <span data-ttu-id="b6d99-184">Nessuna versione stabile sono stata trovata nell'intervallo di dipendenza.</span><span class="sxs-lookup"><span data-stu-id="b6d99-184">No stable versions were found in the dependency range.</span></span> <span data-ttu-id="b6d99-185">Le versioni non definitive sono state trovate, ma non sono consentite.</span><span class="sxs-lookup"><span data-stu-id="b6d99-185">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="b6d99-186">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-186">**Common causes**</span></span> | <span data-ttu-id="b6d99-187">Il progetto specificato una versione stabile per l'intervallo di dipendenza.</span><span class="sxs-lookup"><span data-stu-id="b6d99-187">The project specified a stable version for the dependency range.</span></span> <span data-ttu-id="b6d99-188">Gli utenti devono modificare l'intervallo di versione per includere le versioni non definitive.</span><span class="sxs-lookup"><span data-stu-id="b6d99-188">Users need to change the version range to include pre-release versions.</span></span> |
| <span data-ttu-id="b6d99-189">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-189">**Example message**</span></span> | <span data-ttu-id="b6d99-190">*Impossibile trovare un pacchetto stabile NuGet.Versioning con la versione (> = 3.0.0)<br/> -versioni 10 trovato in dotnet buildtools [più vicino di versione: 4.0.0-rc-2129]<br/> -versioni 9 trovato in NuGetVolatile [più vicino di versione: 3.0.0-beta-00032] <br/> -0 versioni, vedere dotnet core<br/> -0 versioni, vedere dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="b6d99-190">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1104"></a><span data-ttu-id="b6d99-191">NU1104</span><span class="sxs-lookup"><span data-stu-id="b6d99-191">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-192">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-192">**Issue**</span></span> | <span data-ttu-id="b6d99-193">Un elemento ProjectReference punta a un file che non esiste.</span><span class="sxs-lookup"><span data-stu-id="b6d99-193">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="b6d99-194">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-194">**Common causes**</span></span> | <span data-ttu-id="b6d99-195">Il file di progetto è presente sul disco o il riferimento non è corretto.</span><span class="sxs-lookup"><span data-stu-id="b6d99-195">The project file is missing from disk or the reference is incorrect.</span></span> |
| <span data-ttu-id="b6d99-196">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-196">**Example message**</span></span> | <span data-ttu-id="b6d99-197">*Riferimento al progetto non esiste 'c:\a.csproj'. Verificare che il riferimento al progetto sia valido e che esista il file di progetto.*</span><span class="sxs-lookup"><span data-stu-id="b6d99-197">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |

### <a name="nu1105"></a><span data-ttu-id="b6d99-198">NU1105</span><span class="sxs-lookup"><span data-stu-id="b6d99-198">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-199">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-199">**Issue**</span></span> | <span data-ttu-id="b6d99-200">Il file di progetto esiste ma è stata fornita alcuna informazione di ripristino per tale.</span><span class="sxs-lookup"><span data-stu-id="b6d99-200">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="b6d99-201">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-201">**Common causes**</span></span> | <span data-ttu-id="b6d99-202">In Visual Studio ciò vuol dire che il progetto viene scaricato.</span><span class="sxs-lookup"><span data-stu-id="b6d99-202">In Visual Studio this could mean that the project is unloaded.</span></span> <span data-ttu-id="b6d99-203">Dalla riga di comando ciò vuol dire che il file è danneggiato o che non contenga personalizzata dopo la destinazione di importazioni necessarie per il ripristino leggere il progetto.</span><span class="sxs-lookup"><span data-stu-id="b6d99-203">From the command line this could mean that the file is corrupt or that it doesn't contain the custom after imports target needed for restore to read the project.</span></span> |
| <span data-ttu-id="b6d99-204">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-204">**Example message**</span></span> | <span data-ttu-id="b6d99-205">*Impossibile leggere le informazioni di progetto per 'c:\a.csproj'. Il file di progetto potrebbe essere destinazioni non valide o mancante necessarie per il ripristino.*</span><span class="sxs-lookup"><span data-stu-id="b6d99-205">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

### <a name="nu1106"></a><span data-ttu-id="b6d99-206">NU1106</span><span class="sxs-lookup"><span data-stu-id="b6d99-206">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-207">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-207">**Issue**</span></span> | <span data-ttu-id="b6d99-208">Vincoli di dipendenza non possono essere risolti.</span><span class="sxs-lookup"><span data-stu-id="b6d99-208">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="b6d99-209">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-209">**Common causes**</span></span> | <span data-ttu-id="b6d99-210">I pacchetti contengono dipendenza versioni esatte di un pacchetto anziché intervalli aperti.</span><span class="sxs-lookup"><span data-stu-id="b6d99-210">Packages contain dependency on exact versions of a package instead of open-ended ranges.</span></span> |
| <span data-ttu-id="b6d99-211">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-211">**Example message**</span></span> | <span data-ttu-id="b6d99-212">*Non è possibile soddisfare le richieste con conflitto per {id}: {percorso conflitto} Framework: {grafico di destinazione}*</span><span class="sxs-lookup"><span data-stu-id="b6d99-212">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |

<span data-ttu-id="b6d99-213">< name = "NU1107 ></a></span><span class="sxs-lookup"><span data-stu-id="b6d99-213"><a name="NU1107></a></span></span>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="b6d99-214">NU1107 (in precedenza NU1607)</span><span class="sxs-lookup"><span data-stu-id="b6d99-214">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-215">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-215">**Issue**</span></span> | <span data-ttu-id="b6d99-216">Impossibile risolvere i vincoli di dipendenza tra pacchetti.</span><span class="sxs-lookup"><span data-stu-id="b6d99-216">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="b6d99-217">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-217">**Common causes**</span></span> | <span data-ttu-id="b6d99-218">Pacchetti con vincoli di dipendenza in versioni esatte non consentono altri pacchetti per incrementare la versione, se necessario.</span><span class="sxs-lookup"><span data-stu-id="b6d99-218">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> |
| <span data-ttu-id="b6d99-219">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-219">**Example message**</span></span> | <span data-ttu-id="b6d99-220">*Conflitto di versione per NuGet.Versioning. Fare riferimento il pacchetto direttamente dal progetto per risolvere il problema.<br/>  NuGet. Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (4.0.0 =)*</span><span class="sxs-lookup"><span data-stu-id="b6d99-220">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |

<span data-ttu-id="b6d99-221">< name = "NU1108 ></a></span><span class="sxs-lookup"><span data-stu-id="b6d99-221"><a name="NU1108></a></span></span>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="b6d99-222">NU1108 (in precedenza NU1606)</span><span class="sxs-lookup"><span data-stu-id="b6d99-222">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-223">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-223">**Issue**</span></span> | <span data-ttu-id="b6d99-224">È stata rilevata una dipendenza circolare.</span><span class="sxs-lookup"><span data-stu-id="b6d99-224">A circular dependency was detected.</span></span> |
| <span data-ttu-id="b6d99-225">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-225">**Common causes**</span></span> | <span data-ttu-id="b6d99-226">Un pacchetto viene creato in modo non corretto.</span><span class="sxs-lookup"><span data-stu-id="b6d99-226">A package is authored incorrectly.</span></span> |
| <span data-ttu-id="b6d99-227">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-227">**Example message**</span></span> | <span data-ttu-id="b6d99-228">*Rilevato ciclo: A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="b6d99-228">*Cycle detected: A -> B -> A*</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="b6d99-229">Errori di compatibilità</span><span class="sxs-lookup"><span data-stu-id="b6d99-229">Compatibility errors</span></span>

<span data-ttu-id="b6d99-230">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="b6d99-230">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="b6d99-231">NU1201</span><span class="sxs-lookup"><span data-stu-id="b6d99-231">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-232">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-232">**Issue**</span></span> | <span data-ttu-id="b6d99-233">Una dipendenza di progetto non contiene un framework compatibile con il progetto corrente.</span><span class="sxs-lookup"><span data-stu-id="b6d99-233">A dependency project doesn't contain a framework compatible with the current project.</span></span> |
| <span data-ttu-id="b6d99-234">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-234">**Common causes**</span></span> | <span data-ttu-id="b6d99-235">Il framework di destinazione del progetto è una versione successiva a quella del progetto consumer.</span><span class="sxs-lookup"><span data-stu-id="b6d99-235">The project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="b6d99-236">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-236">**Example message**</span></span> | <span data-ttu-id="b6d99-237">*Progetto ServerWeb non è compatibile con netstandard1.3 (. Moniker NETStandard, Version = v 1.3). Progetto supporta ServerWeb:<br/> -netstandard1.6 (. Moniker NETStandard, Version = v 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = v 1.0)*</span><span class="sxs-lookup"><span data-stu-id="b6d99-237">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |

### <a name="nu1202"></a><span data-ttu-id="b6d99-238">NU1202</span><span class="sxs-lookup"><span data-stu-id="b6d99-238">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-239">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-239">**Issue**</span></span> | <span data-ttu-id="b6d99-240">Un pacchetto di dipendenze non contiene tutte le risorse compatibile con il progetto.</span><span class="sxs-lookup"><span data-stu-id="b6d99-240">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="b6d99-241">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-241">**Common causes**</span></span> | <span data-ttu-id="b6d99-242">Il pacchetto non supporta il framework di destinazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="b6d99-242">The package doesn't support the project's target framework.</span></span> |
| <span data-ttu-id="b6d99-243">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-243">**Example message**</span></span> | <span data-ttu-id="b6d99-244">*Pacchetto System.ComponentModel.EventBasedAsync 4.0.11 non è compatibile con netstandard1.3 (. Moniker NETStandard, Version = v 1.3). Creare il pacchetto supporta System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, Version = v 1.0)<br/> -monotouch10 (MonoTouch, Version = v 1.0)<br/> -net45 (. NETFramework, Version = v 4.5)<br/> -netcore50 (. NETCore, Version = v 5.0)<br/> -netstandard1.0 (. Moniker NETStandard, Version = v 1.0)<br/> -portabile net45 win8 wp8 + wpa81 (. NETPortable, versione = v0.0, profilo = Profile259)<br/> -win8 (Windows, Version = v 8.0)<br/> -wp8 (WindowsPhone, Version = v 8.0)<br/> -wpa81 (WindowsPhoneApp, Version = v 8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="b6d99-244">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|

### <a name="nu1203"></a><span data-ttu-id="b6d99-245">NU1203</span><span class="sxs-lookup"><span data-stu-id="b6d99-245">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-246">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-246">**Issue**</span></span> | <span data-ttu-id="b6d99-247">Il pacchetto non supporta il progetto `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="b6d99-247">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="b6d99-248">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-248">**Common causes**</span></span> | <span data-ttu-id="b6d99-249">Il pacchetto non supporta corrente `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="b6d99-249">The package doesn't support the current `RuntimeIdentifier`.</span></span> <span data-ttu-id="b6d99-250">Modifica il `RuntimeIdentifier` valori usati nel progetto, se necessario.</span><span class="sxs-lookup"><span data-stu-id="b6d99-250">Change the `RuntimeIdentifier` values used in the project if needed.</span></span> |
| <span data-ttu-id="b6d99-251">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-251">**Example message**</span></span> | <span data-ttu-id="b6d99-252">*System.Example 1.0.0 fornisce un assembly di riferimento in fase di compilazione per DLL in net461, ma non sono presenti assembly di runtime compatibili.*</span><span class="sxs-lookup"><span data-stu-id="b6d99-252">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |

### <a name="nu1401"></a><span data-ttu-id="b6d99-253">NU1401</span><span class="sxs-lookup"><span data-stu-id="b6d99-253">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-254">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-254">**Issue**</span></span> | <span data-ttu-id="b6d99-255">Il pacchetto richiede caratteristiche o Framework non sono attualmente supportati dalla versione installata di NuGet.</span><span class="sxs-lookup"><span data-stu-id="b6d99-255">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="b6d99-256">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-256">**Common causes**</span></span> | <span data-ttu-id="b6d99-257">Aggiornare NuGet per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="b6d99-257">Upgrade NuGet to fix the issue.</span></span> |
| <span data-ttu-id="b6d99-258">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-258">**Example message**</span></span> | <span data-ttu-id="b6d99-259">*Il pacchetto 'NuGet.Versioning' richiede '5.0.0' alla versione client NuGet o versione successiva, ma la versione NuGet corrente è '4.3.0'. Per aggiornare NuGet, vedere http://docs.nuget.org/consume/installing-nuget.*</span><span class="sxs-lookup"><span data-stu-id="b6d99-259">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'. To upgrade NuGet, please go to http://docs.nuget.org/consume/installing-nuget.*</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="b6d99-260">Avvisi di input non validi</span><span class="sxs-lookup"><span data-stu-id="b6d99-260">Invalid input warnings</span></span>

<span data-ttu-id="b6d99-261">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="b6d99-261">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="b6d99-262">NU1501</span><span class="sxs-lookup"><span data-stu-id="b6d99-262">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-263">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-263">**Issue**</span></span> | <span data-ttu-id="b6d99-264">Il ripristino del progetto sta tentando di operare in non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="b6d99-264">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="b6d99-265">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-265">**Common causes**</span></span> | <span data-ttu-id="b6d99-266">Il progetto è mancano.</span><span class="sxs-lookup"><span data-stu-id="b6d99-266">The project is missing.</span></span> |
| <span data-ttu-id="b6d99-267">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-267">**Example message**</span></span> | <span data-ttu-id="b6d99-268">*La cartella 'c:\projects\a' non contiene un progetto da ripristinare.*</span><span class="sxs-lookup"><span data-stu-id="b6d99-268">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |

### <a name="nu1502"></a><span data-ttu-id="b6d99-269">NU1502</span><span class="sxs-lookup"><span data-stu-id="b6d99-269">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-270">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-270">**Issue**</span></span> | <span data-ttu-id="b6d99-271">`RuntimeSupports`contiene un profilo non valido.</span><span class="sxs-lookup"><span data-stu-id="b6d99-271">`RuntimeSupports` contains an invalid profile.</span></span> |
| <span data-ttu-id="b6d99-272">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-272">**Common causes**</span></span> | <span data-ttu-id="b6d99-273">Impossibile trovare il profilo supporta un `runtime.json` file dai pacchetti dipendenza corrente.</span><span class="sxs-lookup"><span data-stu-id="b6d99-273">The supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span> |
| <span data-ttu-id="b6d99-274">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-274">**Example message**</span></span> | <span data-ttu-id="b6d99-275">*Profilo di compatibilità sconosciuto: aaa*</span><span class="sxs-lookup"><span data-stu-id="b6d99-275">*Unknown Compatibility Profile: aaa*</span></span> |

### <a name="nu1503"></a><span data-ttu-id="b6d99-276">NU1503</span><span class="sxs-lookup"><span data-stu-id="b6d99-276">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-277">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-277">**Issue**</span></span> | <span data-ttu-id="b6d99-278">Una dipendenza di progetto non importa le destinazioni di ripristino di NuGet.</span><span class="sxs-lookup"><span data-stu-id="b6d99-278">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="b6d99-279">È simile a NU1105 ma qui il progetto viene ignorato e ignorato anziché causare tutte esito negativo del ripristino.</span><span class="sxs-lookup"><span data-stu-id="b6d99-279">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="b6d99-280">Nelle soluzioni complesse sono spesso altri tipi di progetti che non supportano il ripristino.</span><span class="sxs-lookup"><span data-stu-id="b6d99-280">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="b6d99-281">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-281">**Common causes**</span></span> | <span data-ttu-id="b6d99-282">Questa situazione può verificarsi per i progetti che non si importano props/destinazioni comuni quali l'importazione automatica di ripristino.</span><span class="sxs-lookup"><span data-stu-id="b6d99-282">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="b6d99-283">Se il progetto non è necessaria per il ripristino può essere ignorato.</span><span class="sxs-lookup"><span data-stu-id="b6d99-283">If the project doesn't need to be restored this can be ignored.</span></span> |
| <span data-ttu-id="b6d99-284">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-284">**Example message**</span></span> | <span data-ttu-id="b6d99-285">*Mancato ripristino per il progetto 'c:\a.csproj'. Il file di progetto potrebbe essere destinazioni non valide o mancante necessarie per il ripristino.*</span><span class="sxs-lookup"><span data-stu-id="b6d99-285">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="b6d99-286">Avvisi di versione di pacchetto imprevisto</span><span class="sxs-lookup"><span data-stu-id="b6d99-286">Unexpected package version warnings</span></span>

<span data-ttu-id="b6d99-287">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="b6d99-287">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="b6d99-288">NU1601</span><span class="sxs-lookup"><span data-stu-id="b6d99-288">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-289">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-289">**Issue**</span></span> | <span data-ttu-id="b6d99-290">Una dipendenza diretta del progetto è stato ha respinto per una versione successiva a quella del progetto specificato.</span><span class="sxs-lookup"><span data-stu-id="b6d99-290">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="b6d99-291">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-291">**Common causes**</span></span> | <span data-ttu-id="b6d99-292">Un altro pacchetto dipendenza necessaria una versione successiva e aumentata del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b6d99-292">Another dependency package required a higher version and bumped the package up.</span></span> |
| <span data-ttu-id="b6d99-293">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-293">**Example message**</span></span> | <span data-ttu-id="b6d99-294">*Dipendenza specificata è NuGet.Versioning (> = 3.5.0) ma è risultata NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="b6d99-294">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |

### <a name="nu1602"></a><span data-ttu-id="b6d99-295">NU1602</span><span class="sxs-lookup"><span data-stu-id="b6d99-295">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-296">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-296">**Issue**</span></span> | <span data-ttu-id="b6d99-297">Una dipendenza pacchetto manca un limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="b6d99-297">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="b6d99-298">Questo non consente il ripristino trovare il *migliore corrispondenza*.</span><span class="sxs-lookup"><span data-stu-id="b6d99-298">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="b6d99-299">Ogni ripristino verrà spostata verso il basso il tentativo di trovare una versione precedente che può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="b6d99-299">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="b6d99-300">Ciò significa che il ripristino passa nello stato online per controllare tutte le origini di ogni volta che invece di usare i pacchetti già esistenti nella cartella del pacchetto utente.</span><span class="sxs-lookup"><span data-stu-id="b6d99-300">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="b6d99-301">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-301">**Common causes**</span></span> | <span data-ttu-id="b6d99-302">In genere si tratta di un pacchetto con errore di creazione.</span><span class="sxs-lookup"><span data-stu-id="b6d99-302">This is usually a package authoring error.</span></span> |
| <span data-ttu-id="b6d99-303">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-303">**Example message**</span></span> | <span data-ttu-id="b6d99-304">*NuGet. Packaging 4.0.0 non prevede un limite inferiore inclusivo dipendenza NuGet.Versioning (3.5.0 >). Una corrispondenza migliore approssimativa di 3.6.0 è stato risolta.*</span><span class="sxs-lookup"><span data-stu-id="b6d99-304">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |

### <a name="nu1603"></a><span data-ttu-id="b6d99-305">NU1603</span><span class="sxs-lookup"><span data-stu-id="b6d99-305">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-306">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-306">**Issue**</span></span> | <span data-ttu-id="b6d99-307">Una dipendenza pacchetto specificata una versione che non è stata trovata.</span><span class="sxs-lookup"><span data-stu-id="b6d99-307">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="b6d99-308">È stata utilizzata una versione successiva, che differisce da cosa è stato creato il pacchetto base.</span><span class="sxs-lookup"><span data-stu-id="b6d99-308">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="b6d99-309">Ciò significa che il ripristino non è stata trovata la *migliore corrispondenza*.</span><span class="sxs-lookup"><span data-stu-id="b6d99-309">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="b6d99-310">Ogni ripristino verrà spostata verso il basso il tentativo di trovare una versione precedente che può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="b6d99-310">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="b6d99-311">Ciò significa che il ripristino passa nello stato online per controllare tutte le origini di ogni volta che invece di usare i pacchetti già esistenti nella cartella del pacchetto utente.</span><span class="sxs-lookup"><span data-stu-id="b6d99-311">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="b6d99-312">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-312">**Common causes**</span></span> | <span data-ttu-id="b6d99-313">Le origini del pacchetto non contengono la versione prevista limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="b6d99-313">The package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="b6d99-314">Se il pacchetto previsto non è stato rilasciato quindi potrebbe trattarsi di un pacchetto con errore di creazione.</span><span class="sxs-lookup"><span data-stu-id="b6d99-314">If the package expected has not been released then this may be a package authoring error.</span></span> |
| <span data-ttu-id="b6d99-315">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-315">**Example message**</span></span> | <span data-ttu-id="b6d99-316">NuGet. Packaging 4.0.0 dipende NuGet.Versioning (> = 4.0.0) 4.0.0 non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="b6d99-316">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="b6d99-317">Una corrispondenza migliore approssimativa di 5.0.0 è stato risolta.</span><span class="sxs-lookup"><span data-stu-id="b6d99-317">An approximate best match of 5.0.0 was resolved.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="b6d99-318">NU1604</span><span class="sxs-lookup"><span data-stu-id="b6d99-318">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-319">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-319">**Issue**</span></span> | <span data-ttu-id="b6d99-320">Dipendenza di progetto non viene definito un limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="b6d99-320">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="b6d99-321">Ciò significa che il ripristino non è stata trovata la *migliore corrispondenza*.</span><span class="sxs-lookup"><span data-stu-id="b6d99-321">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="b6d99-322">Ogni ripristino verrà spostata verso il basso il tentativo di trovare una versione precedente che può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="b6d99-322">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="b6d99-323">Ciò significa che il ripristino passa nello stato online per controllare tutte le origini di ogni volta che invece di usare i pacchetti già esistenti nella cartella del pacchetto utente.</span><span class="sxs-lookup"><span data-stu-id="b6d99-323">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="b6d99-324">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-324">**Common causes**</span></span> | <span data-ttu-id="b6d99-325">Il progetto *PackageReference* *versione* attributo deve essere aggiornato per includere un limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="b6d99-325">The project's *PackageReference* *Version* attribute should be updated to include a lower bound.</span></span> |
| <span data-ttu-id="b6d99-326">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-326">**Example message**</span></span> | <span data-ttu-id="b6d99-327">*Progetto dipendenza NuGet.Versioning (< = 9.0.0) doe non contengono un limite inferiore inclusivo. Includere un limite inferiore nella versione di dipendenza per garantire risultati coerenti di ripristino.*</span><span class="sxs-lookup"><span data-stu-id="b6d99-327">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |

### <a name="nu1605"></a><span data-ttu-id="b6d99-328">NU1605</span><span class="sxs-lookup"><span data-stu-id="b6d99-328">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-329">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-329">**Issue**</span></span> | <span data-ttu-id="b6d99-330">Un pacchetto di dipendenza è specificato un vincolo di versione in una versione superiore di un pacchetto rispetto al ripristino risolta.</span><span class="sxs-lookup"><span data-stu-id="b6d99-330">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> |
| <span data-ttu-id="b6d99-331">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-331">**Common causes**</span></span> | <span data-ttu-id="b6d99-332">Più vicino wins per la risoluzione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="b6d99-332">Nearest wins when resolving packages.</span></span> <span data-ttu-id="b6d99-333">Un pacchetto più vicini nel grafico può avere sottoposto a override un pacchetto distante.</span><span class="sxs-lookup"><span data-stu-id="b6d99-333">A nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="b6d99-334">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-334">**Example message**</span></span> | <span data-ttu-id="b6d99-335">*Rilevato downgrade del pacchetto: NuGet.Versioning da 4.0.0 a 3.5.0. Fare riferimento il pacchetto direttamente dal progetto per selezionare una versione diversa.<br/>  NuGet. Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="b6d99-335">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="b6d99-336">Avvisi di sistema di risoluzione dei conflitti</span><span class="sxs-lookup"><span data-stu-id="b6d99-336">Resolver conflict warnings</span></span>

[<span data-ttu-id="b6d99-337">NU1608</span><span class="sxs-lookup"><span data-stu-id="b6d99-337">NU1608</span></span>](#nu1608)

### <a name="nu1608"></a><span data-ttu-id="b6d99-338">NU1608</span><span class="sxs-lookup"><span data-stu-id="b6d99-338">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-339">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-339">**Issue**</span></span> | <span data-ttu-id="b6d99-340">Un pacchetto di risoluzione è supera a quello di un vincolo di dipendenza.</span><span class="sxs-lookup"><span data-stu-id="b6d99-340">A resolve package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="b6d99-341">In alcuni casi ciò è intenzionale e l'avviso può essere eliminato.</span><span class="sxs-lookup"><span data-stu-id="b6d99-341">In some cases this is intentional and the warning can be suppressed.</span></span> |
| <span data-ttu-id="b6d99-342">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-342">**Common causes**</span></span> | <span data-ttu-id="b6d99-343">Un pacchetto a cui fa riferimento direttamente un progetto sostituiranno i vincoli di dipendenze da altri pacchetti.</span><span class="sxs-lookup"><span data-stu-id="b6d99-343">A package referenced directly by a project will override dependency constraints from other packages.</span></span>   |
| <span data-ttu-id="b6d99-344">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-344">**Example message**</span></span> | <span data-ttu-id="b6d99-345">*Versione del pacchetto rilevato all'esterno di vincolo dipendenza: x 1.0.0 richiede y (= 1.0.0) ma versione 2.0.0 y è stato risolto.*</span><span class="sxs-lookup"><span data-stu-id="b6d99-345">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="b6d99-346">Avvisi di fallback di pacchetto</span><span class="sxs-lookup"><span data-stu-id="b6d99-346">Package fallback warnings</span></span>

[<span data-ttu-id="b6d99-347">NU1701</span><span class="sxs-lookup"><span data-stu-id="b6d99-347">NU1701</span></span>](#nu1701)

### <a name="nu1701"></a><span data-ttu-id="b6d99-348">NU1701</span><span class="sxs-lookup"><span data-stu-id="b6d99-348">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-349">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-349">**Issue**</span></span> | <span data-ttu-id="b6d99-350">*PackageTargetFallback/AssetTargetFallback* veniva utilizzato per selezionare asset da un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b6d99-350">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span></span> <span data-ttu-id="b6d99-351">Questo è un avviso per informare l'utente che le risorse potrebbero non essere compatibile al 100%.</span><span class="sxs-lookup"><span data-stu-id="b6d99-351">This is a warning to let the user know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="b6d99-352">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-352">**Common causes**</span></span> | <span data-ttu-id="b6d99-353">Il pacchetto non supporta la struttura del progetto.</span><span class="sxs-lookup"><span data-stu-id="b6d99-353">The package doesn't support the project framework.</span></span> |
| <span data-ttu-id="b6d99-354">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-354">**Example message**</span></span> | <span data-ttu-id="b6d99-355">*Pacchetto 'NuGet.Versioning' è stato ripristinato mediante 'portable net45 + win8' invece del framework di destinazione del progetto 'netstandard1.5'. Questo pacchetto potrebbe non essere completamente compatibile con il progetto.*</span><span class="sxs-lookup"><span data-stu-id="b6d99-355">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="b6d99-356">Feed di avvisi</span><span class="sxs-lookup"><span data-stu-id="b6d99-356">Feed warnings</span></span>

[<span data-ttu-id="b6d99-357">NU1801</span><span class="sxs-lookup"><span data-stu-id="b6d99-357">NU1801</span></span>](#nu1801)

### <a name="nu1801"></a><span data-ttu-id="b6d99-358">NU1801</span><span class="sxs-lookup"><span data-stu-id="b6d99-358">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-359">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-359">**Issue**</span></span> | <span data-ttu-id="b6d99-360">Si è verificato un errore durante la lettura dei feed quando `IgnoreFailedSources` è impostata su true, convertendolo in un messaggio di avviso non irreversibile.</span><span class="sxs-lookup"><span data-stu-id="b6d99-360">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="b6d99-361">Ciò può contenere qualsiasi messaggio ed è generico.</span><span class="sxs-lookup"><span data-stu-id="b6d99-361">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="b6d99-362">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-362">**Common causes**</span></span> | <span data-ttu-id="b6d99-363">L'origine non è valido.</span><span class="sxs-lookup"><span data-stu-id="b6d99-363">The source is invalid.</span></span> |
| <span data-ttu-id="b6d99-364">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="b6d99-364">**Example message**</span></span> | <span data-ttu-id="b6d99-365">n/d</span><span class="sxs-lookup"><span data-stu-id="b6d99-365">n/a</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="b6d99-366">Avvisi ed errori interni di NuGet</span><span class="sxs-lookup"><span data-stu-id="b6d99-366">NuGet internal errors and warnings</span></span>

<span data-ttu-id="b6d99-367">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="b6d99-367">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="b6d99-368">NU1000</span><span class="sxs-lookup"><span data-stu-id="b6d99-368">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-369">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-369">**Issue**</span></span> | <span data-ttu-id="b6d99-370">Un errore interno non specifico da NuGet.</span><span class="sxs-lookup"><span data-stu-id="b6d99-370">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="b6d99-371">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-371">**Common causes**</span></span> | <span data-ttu-id="b6d99-372">Controllare i registri per ulteriori informazioni</span><span class="sxs-lookup"><span data-stu-id="b6d99-372">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="b6d99-373">NU1500</span><span class="sxs-lookup"><span data-stu-id="b6d99-373">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6d99-374">**Problema**</span><span class="sxs-lookup"><span data-stu-id="b6d99-374">**Issue**</span></span> | <span data-ttu-id="b6d99-375">Un avviso interno non specifico da NuGet.</span><span class="sxs-lookup"><span data-stu-id="b6d99-375">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="b6d99-376">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="b6d99-376">**Common causes**</span></span> | <span data-ttu-id="b6d99-377">Controllare i registri per ulteriori informazioni</span><span class="sxs-lookup"><span data-stu-id="b6d99-377">Check the logs for more information</span></span> |
