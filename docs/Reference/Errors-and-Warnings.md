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
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
ms.openlocfilehash: 9e22b63636980ce64017c950148d9005bf9c2fb1
ms.sourcegitcommit: ed01eaeef9bf488c36556b97247ca440384c0242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/23/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="91c2c-104">Errori e avvisi</span><span class="sxs-lookup"><span data-stu-id="91c2c-104">Errors and warnings</span></span>

<span data-ttu-id="91c2c-105">In NuGet 4.3.0, errori e avvisi sono numerati come descritto in questo argomento e forniscono informazioni dettagliate che consentono di risolvere i problemi che interessano.</span><span class="sxs-lookup"><span data-stu-id="91c2c-105">In NuGet 4.3.0, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span> 

<span data-ttu-id="91c2c-106">Gli errori e avvisi elencati di seguito sono disponibili solo con [basato su PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) progetti e NuGet 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="91c2c-106">The errors and warnings listed here are available only with [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) projects and NuGet 4.3.0.</span></span> <span data-ttu-id="91c2c-107">NuGet anche rispetta la proprietà di MSBuild per l'esclusione di avvisi o li elevare a errori.</span><span class="sxs-lookup"><span data-stu-id="91c2c-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="91c2c-108">Per ulteriori informazioni, vedere [procedura: esclusione di avvisi del compilatore](/visualstudio/ide/how-to-suppress-compiler-warnings) nella documentazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="91c2c-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="91c2c-109">**Errori**</span><span class="sxs-lookup"><span data-stu-id="91c2c-109">**Errors**</span></span>

| <span data-ttu-id="91c2c-110">Gruppo</span><span class="sxs-lookup"><span data-stu-id="91c2c-110">Group</span></span> | <span data-ttu-id="91c2c-111">Numeri di errore</span><span class="sxs-lookup"><span data-stu-id="91c2c-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="91c2c-112">Errori di input non validi</span><span class="sxs-lookup"><span data-stu-id="91c2c-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="91c2c-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="91c2c-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="91c2c-114">Errori di pacchetto e progetto mancanti</span><span class="sxs-lookup"><span data-stu-id="91c2c-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="91c2c-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (in precedenza NU1607), [NU1108](#nu1108) (in precedenza NU1606)</span><span class="sxs-lookup"><span data-stu-id="91c2c-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="91c2c-116">Errori di compatibilità</span><span class="sxs-lookup"><span data-stu-id="91c2c-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="91c2c-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="91c2c-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="91c2c-118">**Avvisi**</span><span class="sxs-lookup"><span data-stu-id="91c2c-118">**Warnings**</span></span>

| <span data-ttu-id="91c2c-119">Gruppo</span><span class="sxs-lookup"><span data-stu-id="91c2c-119">Group</span></span> | <span data-ttu-id="91c2c-120">Numeri di avviso</span><span class="sxs-lookup"><span data-stu-id="91c2c-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="91c2c-121">Avvisi di input non validi</span><span class="sxs-lookup"><span data-stu-id="91c2c-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="91c2c-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="91c2c-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="91c2c-123">Avvisi di versione di pacchetto imprevisto</span><span class="sxs-lookup"><span data-stu-id="91c2c-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="91c2c-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="91c2c-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="91c2c-125">Avvisi di sistema di risoluzione dei conflitti</span><span class="sxs-lookup"><span data-stu-id="91c2c-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="91c2c-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="91c2c-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="91c2c-127">Avvisi di fallback di pacchetto</span><span class="sxs-lookup"><span data-stu-id="91c2c-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="91c2c-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="91c2c-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="91c2c-129">Feed di avvisi</span><span class="sxs-lookup"><span data-stu-id="91c2c-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="91c2c-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="91c2c-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="91c2c-131">Avvisi ed errori interni di NuGet</span><span class="sxs-lookup"><span data-stu-id="91c2c-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="91c2c-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="91c2c-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="91c2c-133">Errori di input non validi</span><span class="sxs-lookup"><span data-stu-id="91c2c-133">Invalid input errors</span></span>

<span data-ttu-id="91c2c-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="91c2c-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="91c2c-135">NU1001</span><span class="sxs-lookup"><span data-stu-id="91c2c-135">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-136">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-136">**Issue**</span></span> | <span data-ttu-id="91c2c-137">Il progetto non contiene uno o più Framework.</span><span class="sxs-lookup"><span data-stu-id="91c2c-137">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="91c2c-138">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-138">**Common causes**</span></span> | <span data-ttu-id="91c2c-139">Il progetto non contiene un `TargetFramework` o `TargetFrameworks` proprietà.</span><span class="sxs-lookup"><span data-stu-id="91c2c-139">The project doesn't contain a `TargetFramework` or `TargetFrameworks` property.</span></span> |
| <span data-ttu-id="91c2c-140">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-140">**Example message**</span></span> | <span data-ttu-id="91c2c-141">*ProjA il progetto non specifica alcun framework di destinazione in c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="91c2c-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |

### <a name="nu1002"></a><span data-ttu-id="91c2c-142">NU1002</span><span class="sxs-lookup"><span data-stu-id="91c2c-142">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-143">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-143">**Issue**</span></span> | <span data-ttu-id="91c2c-144">Combinazione non valida di input con una parola chiave non CRITTOGRAFATO.</span><span class="sxs-lookup"><span data-stu-id="91c2c-144">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="91c2c-145">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-145">**Common causes**</span></span> | <span data-ttu-id="91c2c-146">CLEAR non possono essere combinati con altri input.</span><span class="sxs-lookup"><span data-stu-id="91c2c-146">CLEAR may not be combined with other inputs.</span></span> |
| <span data-ttu-id="91c2c-147">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-147">**Example message**</span></span> | <span data-ttu-id="91c2c-148">*'CLEAR' non può essere utilizzato in combinazione con altri valori*</span><span class="sxs-lookup"><span data-stu-id="91c2c-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |

### <a name="nu1003"></a><span data-ttu-id="91c2c-149">NU1003</span><span class="sxs-lookup"><span data-stu-id="91c2c-149">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-150">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-150">**Issue**</span></span> | <span data-ttu-id="91c2c-151">`PackageTargetFallback`e `AssetTargetFallback` comportamenti diversi per la selezione di risorse e non possono essere utilizzati insieme.</span><span class="sxs-lookup"><span data-stu-id="91c2c-151">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="91c2c-152">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-152">**Common causes**</span></span> | <span data-ttu-id="91c2c-153">Entrambi `PackageTargetFallback` e `AssetTargetFallback` esiste nel progetto.</span><span class="sxs-lookup"><span data-stu-id="91c2c-153">Both `PackageTargetFallback` and `AssetTargetFallback` exist in the project.</span></span> |
| <span data-ttu-id="91c2c-154">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-154">**Example message**</span></span> | <span data-ttu-id="91c2c-155">*PackageTargetFallback e AssetTargetFallback non possono essere utilizzati insieme. Rimuovere i riferimenti di PackageTargetFallback(deprecated) dall'ambiente del progetto.*</span><span class="sxs-lookup"><span data-stu-id="91c2c-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="91c2c-156">Errori di pacchetto e progetto mancanti</span><span class="sxs-lookup"><span data-stu-id="91c2c-156">Missing package and project errors</span></span>

<span data-ttu-id="91c2c-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="91c2c-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="91c2c-158">NU1100</span><span class="sxs-lookup"><span data-stu-id="91c2c-158">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-159">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-159">**Issue**</span></span> | <span data-ttu-id="91c2c-160">Un gruppo di dipendenze non essere risolto.</span><span class="sxs-lookup"><span data-stu-id="91c2c-160">A dependency group not be resolved.</span></span> <span data-ttu-id="91c2c-161">Questo è un problema generico per tipi che non sono pacchetti o progetti.</span><span class="sxs-lookup"><span data-stu-id="91c2c-161">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="91c2c-162">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-162">**Common causes**</span></span> | <span data-ttu-id="91c2c-163">Il progetto contiene una dipendenza su un elemento che non esiste.</span><span class="sxs-lookup"><span data-stu-id="91c2c-163">The project contains a dependency on an item that doesn't exist.</span></span> |
| <span data-ttu-id="91c2c-164">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-164">**Example message**</span></span> | <span data-ttu-id="91c2c-165">*Impossibile risolvere System.Missing per net45*</span><span class="sxs-lookup"><span data-stu-id="91c2c-165">*Unable to resolve System.Missing for net45*</span></span> |

### <a name="nu1101"></a><span data-ttu-id="91c2c-166">NU1101</span><span class="sxs-lookup"><span data-stu-id="91c2c-166">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-167">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-167">**Issue**</span></span> | <span data-ttu-id="91c2c-168">Impossibile trovare il pacchetto su tutte le origini.</span><span class="sxs-lookup"><span data-stu-id="91c2c-168">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="91c2c-169">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-169">**Common causes**</span></span> | <span data-ttu-id="91c2c-170">L'origine del pacchetto corretto è manca o l'identificatore del pacchetto non è corretto.</span><span class="sxs-lookup"><span data-stu-id="91c2c-170">The correct package source is missing or the package identifier is incorrect.</span></span> |
| <span data-ttu-id="91c2c-171">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-171">**Example message**</span></span> | <span data-ttu-id="91c2c-172">*Impossibile trovare il pacchetto System.Missing. Nessun pacchetto esistenti con questo id nelle origini: dotnet-core, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="91c2c-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |

### <a name="nu1102"></a><span data-ttu-id="91c2c-173">NU1102</span><span class="sxs-lookup"><span data-stu-id="91c2c-173">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-174">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-174">**Issue**</span></span> | <span data-ttu-id="91c2c-175">L'identificatore del pacchetto è stato trovato ma presente una versione all'interno dell'intervallo di dipendenza specificata non può essere una delle origini.</span><span class="sxs-lookup"><span data-stu-id="91c2c-175">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> |
| <span data-ttu-id="91c2c-176">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-176">**Common causes**</span></span> | <span data-ttu-id="91c2c-177">L'origine del pacchetto corretto è manca o l'intervallo di dipendenza non è corretto.</span><span class="sxs-lookup"><span data-stu-id="91c2c-177">The correct package source is missing or the dependency range is incorrect.</span></span> <span data-ttu-id="91c2c-178">L'intervallo può essere specificato da un pacchetto e non dell'utente.</span><span class="sxs-lookup"><span data-stu-id="91c2c-178">The range might be specified by a package and not the user.</span></span> <span data-ttu-id="91c2c-179">L'utente potrebbe essere necessario passare a una versione disponibile se il pacchetto fa riferimento direttamente il progetto.</span><span class="sxs-lookup"><span data-stu-id="91c2c-179">The user may need to switch to an available version if this package is referenced by the project directly.</span></span> |
| <span data-ttu-id="91c2c-180">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-180">**Example message**</span></span> | <span data-ttu-id="91c2c-181">*Impossibile trovare il pacchetto NuGet.Versioning con la versione (> = 9.0.1)<br/> -30 trovare versioni in nuget.org [più vicino di versione: 4.0.0]<br/> -versioni 10 trovato in dotnet buildtools [più vicino di versione: 4.0.0-rc-2129]<br/> -9 trovato versioni in NuGetVolatile [più vicino di versione: 3.0.0-beta-00032]<br/> -0 versioni, vedere dotnet core<br/> -0 versioni, vedere dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="91c2c-181">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1103"></a><span data-ttu-id="91c2c-182">NU1103</span><span class="sxs-lookup"><span data-stu-id="91c2c-182">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-183">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-183">**Issue**</span></span> | <span data-ttu-id="91c2c-184">Nessuna versione stabile sono stata trovata nell'intervallo di dipendenza.</span><span class="sxs-lookup"><span data-stu-id="91c2c-184">No stable versions were found in the dependency range.</span></span> <span data-ttu-id="91c2c-185">Le versioni non definitive sono state trovate, ma non sono consentite.</span><span class="sxs-lookup"><span data-stu-id="91c2c-185">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="91c2c-186">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-186">**Common causes**</span></span> | <span data-ttu-id="91c2c-187">Il progetto specificato una versione stabile per l'intervallo di dipendenza.</span><span class="sxs-lookup"><span data-stu-id="91c2c-187">The project specified a stable version for the dependency range.</span></span> <span data-ttu-id="91c2c-188">Gli utenti devono modificare l'intervallo di versione per includere le versioni non definitive.</span><span class="sxs-lookup"><span data-stu-id="91c2c-188">Users need to change the version range to include pre-release versions.</span></span> |
| <span data-ttu-id="91c2c-189">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-189">**Example message**</span></span> | <span data-ttu-id="91c2c-190">*Impossibile trovare un pacchetto stabile NuGet.Versioning con la versione (> = 3.0.0)<br/> -versioni 10 trovato in dotnet buildtools [più vicino di versione: 4.0.0-rc-2129]<br/> -versioni 9 trovato in NuGetVolatile [più vicino di versione: 3.0.0-beta-00032] <br/> -0 versioni, vedere dotnet core<br/> -0 versioni, vedere dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="91c2c-190">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1104"></a><span data-ttu-id="91c2c-191">NU1104</span><span class="sxs-lookup"><span data-stu-id="91c2c-191">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-192">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-192">**Issue**</span></span> | <span data-ttu-id="91c2c-193">Un elemento ProjectReference punta a un file che non esiste.</span><span class="sxs-lookup"><span data-stu-id="91c2c-193">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="91c2c-194">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-194">**Common causes**</span></span> | <span data-ttu-id="91c2c-195">Il file di progetto è presente sul disco o il riferimento non è corretto.</span><span class="sxs-lookup"><span data-stu-id="91c2c-195">The project file is missing from disk or the reference is incorrect.</span></span> |
| <span data-ttu-id="91c2c-196">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-196">**Example message**</span></span> | <span data-ttu-id="91c2c-197">*Riferimento al progetto non esiste 'c:\a.csproj'. Verificare che il riferimento al progetto sia valido e che esista il file di progetto.*</span><span class="sxs-lookup"><span data-stu-id="91c2c-197">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |

### <a name="nu1105"></a><span data-ttu-id="91c2c-198">NU1105</span><span class="sxs-lookup"><span data-stu-id="91c2c-198">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-199">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-199">**Issue**</span></span> | <span data-ttu-id="91c2c-200">Il file di progetto esiste ma è stata fornita alcuna informazione di ripristino per tale.</span><span class="sxs-lookup"><span data-stu-id="91c2c-200">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="91c2c-201">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-201">**Common causes**</span></span> | <span data-ttu-id="91c2c-202">In Visual Studio ciò vuol dire che il progetto viene scaricato.</span><span class="sxs-lookup"><span data-stu-id="91c2c-202">In Visual Studio this could mean that the project is unloaded.</span></span> <span data-ttu-id="91c2c-203">Dalla riga di comando ciò vuol dire che il file è danneggiato o che non contenga personalizzata dopo la destinazione di importazioni necessarie per il ripristino leggere il progetto.</span><span class="sxs-lookup"><span data-stu-id="91c2c-203">From the command line this could mean that the file is corrupt or that it doesn't contain the custom after imports target needed for restore to read the project.</span></span> |
| <span data-ttu-id="91c2c-204">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-204">**Example message**</span></span> | <span data-ttu-id="91c2c-205">*Impossibile leggere le informazioni di progetto per 'c:\a.csproj'. Il file di progetto potrebbe essere destinazioni non valide o mancante necessarie per il ripristino.*</span><span class="sxs-lookup"><span data-stu-id="91c2c-205">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

### <a name="nu1106"></a><span data-ttu-id="91c2c-206">NU1106</span><span class="sxs-lookup"><span data-stu-id="91c2c-206">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-207">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-207">**Issue**</span></span> | <span data-ttu-id="91c2c-208">Vincoli di dipendenza non possono essere risolti.</span><span class="sxs-lookup"><span data-stu-id="91c2c-208">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="91c2c-209">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-209">**Common causes**</span></span> | <span data-ttu-id="91c2c-210">I pacchetti contengono dipendenza versioni esatte di un pacchetto anziché intervalli aperti.</span><span class="sxs-lookup"><span data-stu-id="91c2c-210">Packages contain dependency on exact versions of a package instead of open-ended ranges.</span></span> |
| <span data-ttu-id="91c2c-211">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-211">**Example message**</span></span> | <span data-ttu-id="91c2c-212">*Non è possibile soddisfare le richieste con conflitto per {id}: {percorso conflitto} Framework: {grafico di destinazione}*</span><span class="sxs-lookup"><span data-stu-id="91c2c-212">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |

<a name="nu1107"></a> 

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="91c2c-213">NU1107 (in precedenza NU1607)</span><span class="sxs-lookup"><span data-stu-id="91c2c-213">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-214">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-214">**Issue**</span></span> | <span data-ttu-id="91c2c-215">Impossibile risolvere i vincoli di dipendenza tra pacchetti.</span><span class="sxs-lookup"><span data-stu-id="91c2c-215">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="91c2c-216">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-216">**Common causes**</span></span> | <span data-ttu-id="91c2c-217">Pacchetti con vincoli di dipendenza in versioni esatte non consentono altri pacchetti per incrementare la versione, se necessario.</span><span class="sxs-lookup"><span data-stu-id="91c2c-217">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> |
| <span data-ttu-id="91c2c-218">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-218">**Example message**</span></span> | <span data-ttu-id="91c2c-219">*Conflitto di versione per NuGet.Versioning. Fare riferimento il pacchetto direttamente dal progetto per risolvere il problema.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="91c2c-219">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="91c2c-220">NU1108 (in precedenza NU1606)</span><span class="sxs-lookup"><span data-stu-id="91c2c-220">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-221">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-221">**Issue**</span></span> | <span data-ttu-id="91c2c-222">È stata rilevata una dipendenza circolare.</span><span class="sxs-lookup"><span data-stu-id="91c2c-222">A circular dependency was detected.</span></span> |
| <span data-ttu-id="91c2c-223">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-223">**Common causes**</span></span> | <span data-ttu-id="91c2c-224">Un pacchetto viene creato in modo non corretto.</span><span class="sxs-lookup"><span data-stu-id="91c2c-224">A package is authored incorrectly.</span></span> |
| <span data-ttu-id="91c2c-225">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-225">**Example message**</span></span> | <span data-ttu-id="91c2c-226">*Rilevato ciclo: A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="91c2c-226">*Cycle detected: A -> B -> A*</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="91c2c-227">Errori di compatibilità</span><span class="sxs-lookup"><span data-stu-id="91c2c-227">Compatibility errors</span></span>

<span data-ttu-id="91c2c-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="91c2c-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="91c2c-229">NU1201</span><span class="sxs-lookup"><span data-stu-id="91c2c-229">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-230">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-230">**Issue**</span></span> | <span data-ttu-id="91c2c-231">Una dipendenza di progetto non contiene un framework compatibile con il progetto corrente.</span><span class="sxs-lookup"><span data-stu-id="91c2c-231">A dependency project doesn't contain a framework compatible with the current project.</span></span> |
| <span data-ttu-id="91c2c-232">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-232">**Common causes**</span></span> | <span data-ttu-id="91c2c-233">Il framework di destinazione del progetto è una versione successiva a quella del progetto consumer.</span><span class="sxs-lookup"><span data-stu-id="91c2c-233">The project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="91c2c-234">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-234">**Example message**</span></span> | <span data-ttu-id="91c2c-235">*Progetto ServerWeb non è compatibile con netstandard1.3 (. Moniker NETStandard, Version = v 1.3). Progetto supporta ServerWeb:<br/> -netstandard1.6 (. Moniker NETStandard, Version = v 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = v 1.0)*</span><span class="sxs-lookup"><span data-stu-id="91c2c-235">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |

### <a name="nu1202"></a><span data-ttu-id="91c2c-236">NU1202</span><span class="sxs-lookup"><span data-stu-id="91c2c-236">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-237">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-237">**Issue**</span></span> | <span data-ttu-id="91c2c-238">Un pacchetto di dipendenze non contiene tutte le risorse compatibile con il progetto.</span><span class="sxs-lookup"><span data-stu-id="91c2c-238">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="91c2c-239">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-239">**Common causes**</span></span> | <span data-ttu-id="91c2c-240">Il pacchetto non supporta il framework di destinazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="91c2c-240">The package doesn't support the project's target framework.</span></span> |
| <span data-ttu-id="91c2c-241">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-241">**Example message**</span></span> | <span data-ttu-id="91c2c-242">*Pacchetto System.ComponentModel.EventBasedAsync 4.0.11 non è compatibile con netstandard1.3 (. Moniker NETStandard, Version = v 1.3). Creare il pacchetto supporta System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, Version = v 1.0)<br/> -monotouch10 (MonoTouch, Version = v 1.0)<br/> -net45 (. NETFramework, Version = v 4.5)<br/> -netcore50 (. NETCore, Version = v 5.0)<br/> -netstandard1.0 (. Moniker NETStandard, Version = v 1.0)<br/> -portabile net45 win8 wp8 + wpa81 (. NETPortable, versione = v0.0, profilo = Profile259)<br/> -win8 (Windows, Version = v 8.0)<br/> -wp8 (WindowsPhone, Version = v 8.0)<br/> -wpa81 (WindowsPhoneApp, Version = v 8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="91c2c-242">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|

### <a name="nu1203"></a><span data-ttu-id="91c2c-243">NU1203</span><span class="sxs-lookup"><span data-stu-id="91c2c-243">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-244">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-244">**Issue**</span></span> | <span data-ttu-id="91c2c-245">Il pacchetto non supporta il progetto `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="91c2c-245">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="91c2c-246">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-246">**Common causes**</span></span> | <span data-ttu-id="91c2c-247">Il pacchetto non supporta corrente `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="91c2c-247">The package doesn't support the current `RuntimeIdentifier`.</span></span> <span data-ttu-id="91c2c-248">Modifica il `RuntimeIdentifier` valori usati nel progetto, se necessario.</span><span class="sxs-lookup"><span data-stu-id="91c2c-248">Change the `RuntimeIdentifier` values used in the project if needed.</span></span> |
| <span data-ttu-id="91c2c-249">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-249">**Example message**</span></span> | <span data-ttu-id="91c2c-250">*System.Example 1.0.0 fornisce un assembly di riferimento in fase di compilazione per DLL in net461, ma non sono presenti assembly di runtime compatibili.*</span><span class="sxs-lookup"><span data-stu-id="91c2c-250">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |

### <a name="nu1401"></a><span data-ttu-id="91c2c-251">NU1401</span><span class="sxs-lookup"><span data-stu-id="91c2c-251">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-252">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-252">**Issue**</span></span> | <span data-ttu-id="91c2c-253">Il pacchetto richiede caratteristiche o Framework non sono attualmente supportati dalla versione installata di NuGet.</span><span class="sxs-lookup"><span data-stu-id="91c2c-253">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="91c2c-254">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-254">**Common causes**</span></span> | <span data-ttu-id="91c2c-255">Aggiornare NuGet per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="91c2c-255">Upgrade NuGet to fix the issue.</span></span> |
| <span data-ttu-id="91c2c-256">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-256">**Example message**</span></span> | <span data-ttu-id="91c2c-257">*Il pacchetto 'NuGet.Versioning' richiede '5.0.0' alla versione client NuGet o versione successiva, ma la versione NuGet corrente è '4.3.0'. Per aggiornare NuGet, vedere http://docs.nuget.org/consume/installing-nuget.*</span><span class="sxs-lookup"><span data-stu-id="91c2c-257">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'. To upgrade NuGet, please go to http://docs.nuget.org/consume/installing-nuget.*</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="91c2c-258">Avvisi di input non validi</span><span class="sxs-lookup"><span data-stu-id="91c2c-258">Invalid input warnings</span></span>

<span data-ttu-id="91c2c-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="91c2c-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="91c2c-260">NU1501</span><span class="sxs-lookup"><span data-stu-id="91c2c-260">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-261">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-261">**Issue**</span></span> | <span data-ttu-id="91c2c-262">Il ripristino del progetto sta tentando di operare in non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="91c2c-262">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="91c2c-263">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-263">**Common causes**</span></span> | <span data-ttu-id="91c2c-264">Il progetto è mancano.</span><span class="sxs-lookup"><span data-stu-id="91c2c-264">The project is missing.</span></span> |
| <span data-ttu-id="91c2c-265">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-265">**Example message**</span></span> | <span data-ttu-id="91c2c-266">*La cartella 'c:\projects\a' non contiene un progetto da ripristinare.*</span><span class="sxs-lookup"><span data-stu-id="91c2c-266">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |

### <a name="nu1502"></a><span data-ttu-id="91c2c-267">NU1502</span><span class="sxs-lookup"><span data-stu-id="91c2c-267">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-268">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-268">**Issue**</span></span> | <span data-ttu-id="91c2c-269">`RuntimeSupports`contiene un profilo non valido.</span><span class="sxs-lookup"><span data-stu-id="91c2c-269">`RuntimeSupports` contains an invalid profile.</span></span> |
| <span data-ttu-id="91c2c-270">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-270">**Common causes**</span></span> | <span data-ttu-id="91c2c-271">Impossibile trovare il profilo supporta un `runtime.json` file dai pacchetti dipendenza corrente.</span><span class="sxs-lookup"><span data-stu-id="91c2c-271">The supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span> |
| <span data-ttu-id="91c2c-272">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-272">**Example message**</span></span> | <span data-ttu-id="91c2c-273">*Profilo di compatibilità sconosciuto: aaa*</span><span class="sxs-lookup"><span data-stu-id="91c2c-273">*Unknown Compatibility Profile: aaa*</span></span> |

### <a name="nu1503"></a><span data-ttu-id="91c2c-274">NU1503</span><span class="sxs-lookup"><span data-stu-id="91c2c-274">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-275">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-275">**Issue**</span></span> | <span data-ttu-id="91c2c-276">Una dipendenza di progetto non importa le destinazioni di ripristino di NuGet.</span><span class="sxs-lookup"><span data-stu-id="91c2c-276">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="91c2c-277">È simile a NU1105 ma qui il progetto viene ignorato e ignorato anziché causare tutte esito negativo del ripristino.</span><span class="sxs-lookup"><span data-stu-id="91c2c-277">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="91c2c-278">Nelle soluzioni complesse sono spesso altri tipi di progetti che non supportano il ripristino.</span><span class="sxs-lookup"><span data-stu-id="91c2c-278">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="91c2c-279">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-279">**Common causes**</span></span> | <span data-ttu-id="91c2c-280">Questa situazione può verificarsi per i progetti che non si importano props/destinazioni comuni quali l'importazione automatica di ripristino.</span><span class="sxs-lookup"><span data-stu-id="91c2c-280">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="91c2c-281">Se il progetto non è necessaria per il ripristino può essere ignorato.</span><span class="sxs-lookup"><span data-stu-id="91c2c-281">If the project doesn't need to be restored this can be ignored.</span></span> |
| <span data-ttu-id="91c2c-282">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-282">**Example message**</span></span> | <span data-ttu-id="91c2c-283">*Mancato ripristino per il progetto 'c:\a.csproj'. Il file di progetto potrebbe essere destinazioni non valide o mancante necessarie per il ripristino.*</span><span class="sxs-lookup"><span data-stu-id="91c2c-283">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="91c2c-284">Avvisi di versione di pacchetto imprevisto</span><span class="sxs-lookup"><span data-stu-id="91c2c-284">Unexpected package version warnings</span></span>

<span data-ttu-id="91c2c-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="91c2c-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="91c2c-286">NU1601</span><span class="sxs-lookup"><span data-stu-id="91c2c-286">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-287">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-287">**Issue**</span></span> | <span data-ttu-id="91c2c-288">Una dipendenza diretta del progetto è stato ha respinto per una versione successiva a quella del progetto specificato.</span><span class="sxs-lookup"><span data-stu-id="91c2c-288">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="91c2c-289">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-289">**Common causes**</span></span> | <span data-ttu-id="91c2c-290">Un altro pacchetto dipendenza necessaria una versione successiva e aumentata del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="91c2c-290">Another dependency package required a higher version and bumped the package up.</span></span> |
| <span data-ttu-id="91c2c-291">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-291">**Example message**</span></span> | <span data-ttu-id="91c2c-292">*Dipendenza specificata è NuGet.Versioning (> = 3.5.0) ma è risultata NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="91c2c-292">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |

### <a name="nu1602"></a><span data-ttu-id="91c2c-293">NU1602</span><span class="sxs-lookup"><span data-stu-id="91c2c-293">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-294">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-294">**Issue**</span></span> | <span data-ttu-id="91c2c-295">Una dipendenza pacchetto manca un limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="91c2c-295">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="91c2c-296">Questo non consente il ripristino trovare il *migliore corrispondenza*.</span><span class="sxs-lookup"><span data-stu-id="91c2c-296">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="91c2c-297">Ogni ripristino verrà spostata verso il basso il tentativo di trovare una versione precedente che può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="91c2c-297">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="91c2c-298">Ciò significa che il ripristino passa nello stato online per controllare tutte le origini di ogni volta che invece di usare i pacchetti già esistenti nella cartella del pacchetto utente.</span><span class="sxs-lookup"><span data-stu-id="91c2c-298">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="91c2c-299">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-299">**Common causes**</span></span> | <span data-ttu-id="91c2c-300">In genere si tratta di un pacchetto con errore di creazione.</span><span class="sxs-lookup"><span data-stu-id="91c2c-300">This is usually a package authoring error.</span></span> |
| <span data-ttu-id="91c2c-301">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-301">**Example message**</span></span> | <span data-ttu-id="91c2c-302">*NuGet. Packaging 4.0.0 non prevede un limite inferiore inclusivo dipendenza NuGet.Versioning (3.5.0 >). Una corrispondenza migliore approssimativa di 3.6.0 è stato risolta.*</span><span class="sxs-lookup"><span data-stu-id="91c2c-302">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |

### <a name="nu1603"></a><span data-ttu-id="91c2c-303">NU1603</span><span class="sxs-lookup"><span data-stu-id="91c2c-303">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-304">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-304">**Issue**</span></span> | <span data-ttu-id="91c2c-305">Una dipendenza pacchetto specificata una versione che non è stata trovata.</span><span class="sxs-lookup"><span data-stu-id="91c2c-305">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="91c2c-306">È stata utilizzata una versione successiva, che differisce da cosa è stato creato il pacchetto base.</span><span class="sxs-lookup"><span data-stu-id="91c2c-306">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="91c2c-307">Ciò significa che il ripristino non è stata trovata la *migliore corrispondenza*.</span><span class="sxs-lookup"><span data-stu-id="91c2c-307">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="91c2c-308">Ogni ripristino verrà spostata verso il basso il tentativo di trovare una versione precedente che può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="91c2c-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="91c2c-309">Ciò significa che il ripristino passa nello stato online per controllare tutte le origini di ogni volta che invece di usare i pacchetti già esistenti nella cartella del pacchetto utente.</span><span class="sxs-lookup"><span data-stu-id="91c2c-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="91c2c-310">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-310">**Common causes**</span></span> | <span data-ttu-id="91c2c-311">Le origini del pacchetto non contengono la versione prevista limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="91c2c-311">The package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="91c2c-312">Se il pacchetto previsto non è stato rilasciato quindi potrebbe trattarsi di un pacchetto con errore di creazione.</span><span class="sxs-lookup"><span data-stu-id="91c2c-312">If the package expected has not been released then this may be a package authoring error.</span></span> |
| <span data-ttu-id="91c2c-313">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-313">**Example message**</span></span> | <span data-ttu-id="91c2c-314">NuGet. Packaging 4.0.0 dipende NuGet.Versioning (> = 4.0.0) 4.0.0 non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="91c2c-314">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="91c2c-315">Una corrispondenza migliore approssimativa di 5.0.0 è stato risolta.</span><span class="sxs-lookup"><span data-stu-id="91c2c-315">An approximate best match of 5.0.0 was resolved.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="91c2c-316">NU1604</span><span class="sxs-lookup"><span data-stu-id="91c2c-316">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-317">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-317">**Issue**</span></span> | <span data-ttu-id="91c2c-318">Dipendenza di progetto non viene definito un limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="91c2c-318">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="91c2c-319">Ciò significa che il ripristino non è stata trovata la *migliore corrispondenza*.</span><span class="sxs-lookup"><span data-stu-id="91c2c-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="91c2c-320">Ogni ripristino verrà spostata verso il basso il tentativo di trovare una versione precedente che può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="91c2c-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="91c2c-321">Ciò significa che il ripristino passa nello stato online per controllare tutte le origini di ogni volta che invece di usare i pacchetti già esistenti nella cartella del pacchetto utente.</span><span class="sxs-lookup"><span data-stu-id="91c2c-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="91c2c-322">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-322">**Common causes**</span></span> | <span data-ttu-id="91c2c-323">Il progetto *PackageReference* *versione* attributo deve essere aggiornato per includere un limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="91c2c-323">The project's *PackageReference* *Version* attribute should be updated to include a lower bound.</span></span> |
| <span data-ttu-id="91c2c-324">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-324">**Example message**</span></span> | <span data-ttu-id="91c2c-325">*Progetto dipendenza NuGet.Versioning (< = 9.0.0) doe non contengono un limite inferiore inclusivo. Includere un limite inferiore nella versione di dipendenza per garantire risultati coerenti di ripristino.*</span><span class="sxs-lookup"><span data-stu-id="91c2c-325">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |

### <a name="nu1605"></a><span data-ttu-id="91c2c-326">NU1605</span><span class="sxs-lookup"><span data-stu-id="91c2c-326">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-327">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-327">**Issue**</span></span> | <span data-ttu-id="91c2c-328">Un pacchetto di dipendenza è specificato un vincolo di versione in una versione superiore di un pacchetto rispetto al ripristino risolta.</span><span class="sxs-lookup"><span data-stu-id="91c2c-328">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> |
| <span data-ttu-id="91c2c-329">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-329">**Common causes**</span></span> | <span data-ttu-id="91c2c-330">Più vicino wins per la risoluzione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="91c2c-330">Nearest wins when resolving packages.</span></span> <span data-ttu-id="91c2c-331">Un pacchetto più vicini nel grafico può avere sottoposto a override un pacchetto distante.</span><span class="sxs-lookup"><span data-stu-id="91c2c-331">A nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="91c2c-332">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-332">**Example message**</span></span> | <span data-ttu-id="91c2c-333">*Rilevato downgrade del pacchetto: NuGet.Versioning da 4.0.0 a 3.5.0. Fare riferimento il pacchetto direttamente dal progetto per selezionare una versione diversa.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="91c2c-333">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="91c2c-334">Avvisi di sistema di risoluzione dei conflitti</span><span class="sxs-lookup"><span data-stu-id="91c2c-334">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="91c2c-335">NU1608</span><span class="sxs-lookup"><span data-stu-id="91c2c-335">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-336">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-336">**Issue**</span></span> | <span data-ttu-id="91c2c-337">Un pacchetto di risoluzione è supera a quello di un vincolo di dipendenza.</span><span class="sxs-lookup"><span data-stu-id="91c2c-337">A resolve package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="91c2c-338">In alcuni casi ciò è intenzionale e l'avviso può essere eliminato.</span><span class="sxs-lookup"><span data-stu-id="91c2c-338">In some cases this is intentional and the warning can be suppressed.</span></span> |
| <span data-ttu-id="91c2c-339">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-339">**Common causes**</span></span> | <span data-ttu-id="91c2c-340">Un pacchetto a cui fa riferimento direttamente un progetto sostituiranno i vincoli di dipendenze da altri pacchetti.</span><span class="sxs-lookup"><span data-stu-id="91c2c-340">A package referenced directly by a project will override dependency constraints from other packages.</span></span>   |
| <span data-ttu-id="91c2c-341">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-341">**Example message**</span></span> | <span data-ttu-id="91c2c-342">*Versione del pacchetto rilevato all'esterno di vincolo dipendenza: x 1.0.0 richiede y (= 1.0.0) ma versione 2.0.0 y è stato risolto.*</span><span class="sxs-lookup"><span data-stu-id="91c2c-342">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="91c2c-343">Avvisi di fallback di pacchetto</span><span class="sxs-lookup"><span data-stu-id="91c2c-343">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="91c2c-344">NU1701</span><span class="sxs-lookup"><span data-stu-id="91c2c-344">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-345">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-345">**Issue**</span></span> | <span data-ttu-id="91c2c-346">*PackageTargetFallback/AssetTargetFallback* veniva utilizzato per selezionare asset da un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="91c2c-346">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span></span> <span data-ttu-id="91c2c-347">Questo è un avviso per informare l'utente che le risorse potrebbero non essere compatibile al 100%.</span><span class="sxs-lookup"><span data-stu-id="91c2c-347">This is a warning to let the user know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="91c2c-348">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-348">**Common causes**</span></span> | <span data-ttu-id="91c2c-349">Il pacchetto non supporta la struttura del progetto.</span><span class="sxs-lookup"><span data-stu-id="91c2c-349">The package doesn't support the project framework.</span></span> |
| <span data-ttu-id="91c2c-350">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-350">**Example message**</span></span> | <span data-ttu-id="91c2c-351">*Pacchetto 'NuGet.Versioning' è stato ripristinato mediante 'portable net45 + win8' invece del framework di destinazione del progetto 'netstandard1.5'. Questo pacchetto potrebbe non essere completamente compatibile con il progetto.*</span><span class="sxs-lookup"><span data-stu-id="91c2c-351">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="91c2c-352">Feed di avvisi</span><span class="sxs-lookup"><span data-stu-id="91c2c-352">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="91c2c-353">NU1801</span><span class="sxs-lookup"><span data-stu-id="91c2c-353">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-354">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-354">**Issue**</span></span> | <span data-ttu-id="91c2c-355">Si è verificato un errore durante la lettura dei feed quando `IgnoreFailedSources` è impostata su true, convertendolo in un messaggio di avviso non irreversibile.</span><span class="sxs-lookup"><span data-stu-id="91c2c-355">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="91c2c-356">Ciò può contenere qualsiasi messaggio ed è generico.</span><span class="sxs-lookup"><span data-stu-id="91c2c-356">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="91c2c-357">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-357">**Common causes**</span></span> | <span data-ttu-id="91c2c-358">L'origine non è valido.</span><span class="sxs-lookup"><span data-stu-id="91c2c-358">The source is invalid.</span></span> |
| <span data-ttu-id="91c2c-359">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="91c2c-359">**Example message**</span></span> | <span data-ttu-id="91c2c-360">N/D</span><span class="sxs-lookup"><span data-stu-id="91c2c-360">n/a</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="91c2c-361">Avvisi ed errori interni di NuGet</span><span class="sxs-lookup"><span data-stu-id="91c2c-361">NuGet internal errors and warnings</span></span>

<span data-ttu-id="91c2c-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="91c2c-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="91c2c-363">NU1000</span><span class="sxs-lookup"><span data-stu-id="91c2c-363">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-364">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-364">**Issue**</span></span> | <span data-ttu-id="91c2c-365">Un errore interno non specifico da NuGet.</span><span class="sxs-lookup"><span data-stu-id="91c2c-365">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="91c2c-366">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-366">**Common causes**</span></span> | <span data-ttu-id="91c2c-367">Controllare i registri per ulteriori informazioni</span><span class="sxs-lookup"><span data-stu-id="91c2c-367">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="91c2c-368">NU1500</span><span class="sxs-lookup"><span data-stu-id="91c2c-368">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="91c2c-369">**Problema**</span><span class="sxs-lookup"><span data-stu-id="91c2c-369">**Issue**</span></span> | <span data-ttu-id="91c2c-370">Un avviso interno non specifico da NuGet.</span><span class="sxs-lookup"><span data-stu-id="91c2c-370">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="91c2c-371">**Cause più comuni**</span><span class="sxs-lookup"><span data-stu-id="91c2c-371">**Common causes**</span></span> | <span data-ttu-id="91c2c-372">Controllare i registri per ulteriori informazioni</span><span class="sxs-lookup"><span data-stu-id="91c2c-372">Check the logs for more information</span></span> |
