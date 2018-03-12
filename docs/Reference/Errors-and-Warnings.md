---
title: NuGet errori e avvisi riferimento | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento complete per avvisi ed errori generati da NuGet durante le varie operazioni di NuGet.
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
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 59bbe37d1a965e5167800148603869645fc5e0b2
ms.sourcegitcommit: df21fe770900644d476d51622a999597a6f20ef8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/12/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="34046-104">Errori e avvisi</span><span class="sxs-lookup"><span data-stu-id="34046-104">Errors and warnings</span></span>

<span data-ttu-id="34046-105">In NuGet 4.3.0+, errori e avvisi sono numerati come descritto in questo argomento e forniscono informazioni dettagliate che consentono di risolvere i problemi che interessano.</span><span class="sxs-lookup"><span data-stu-id="34046-105">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="34046-106">Gli errori e avvisi elencati di seguito sono disponibili solo con [basato su PackageReference](../consume-packages/package-references-in-project-files.md) 4.3.0+ NuGet e progetti.</span><span class="sxs-lookup"><span data-stu-id="34046-106">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="34046-107">NuGet anche rispetta la proprietà di MSBuild per l'esclusione di avvisi o li elevare a errori.</span><span class="sxs-lookup"><span data-stu-id="34046-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="34046-108">Per ulteriori informazioni, vedere [procedura: esclusione di avvisi del compilatore](/visualstudio/ide/how-to-suppress-compiler-warnings) nella documentazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="34046-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="34046-109">**Errori**</span><span class="sxs-lookup"><span data-stu-id="34046-109">**Errors**</span></span>

| <span data-ttu-id="34046-110">Gruppo</span><span class="sxs-lookup"><span data-stu-id="34046-110">Group</span></span> | <span data-ttu-id="34046-111">Numeri di errore</span><span class="sxs-lookup"><span data-stu-id="34046-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="34046-112">Errori di input non validi</span><span class="sxs-lookup"><span data-stu-id="34046-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="34046-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="34046-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="34046-114">Errori di pacchetto e progetto mancanti</span><span class="sxs-lookup"><span data-stu-id="34046-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="34046-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (in precedenza NU1607), [NU1108](#nu1108) (in precedenza NU1606)</span><span class="sxs-lookup"><span data-stu-id="34046-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="34046-116">Errori di compatibilità</span><span class="sxs-lookup"><span data-stu-id="34046-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="34046-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="34046-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="34046-118">**Avvisi**</span><span class="sxs-lookup"><span data-stu-id="34046-118">**Warnings**</span></span>

| <span data-ttu-id="34046-119">Gruppo</span><span class="sxs-lookup"><span data-stu-id="34046-119">Group</span></span> | <span data-ttu-id="34046-120">Numeri di avviso</span><span class="sxs-lookup"><span data-stu-id="34046-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="34046-121">Avvisi di input non validi</span><span class="sxs-lookup"><span data-stu-id="34046-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="34046-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="34046-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="34046-123">Avvisi di versione di pacchetto imprevisto</span><span class="sxs-lookup"><span data-stu-id="34046-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="34046-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="34046-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="34046-125">Avvisi di sistema di risoluzione dei conflitti</span><span class="sxs-lookup"><span data-stu-id="34046-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="34046-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="34046-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="34046-127">Avvisi di fallback di pacchetto</span><span class="sxs-lookup"><span data-stu-id="34046-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="34046-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="34046-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="34046-129">Feed di avvisi</span><span class="sxs-lookup"><span data-stu-id="34046-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="34046-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="34046-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="34046-131">Avvisi ed errori interni di NuGet</span><span class="sxs-lookup"><span data-stu-id="34046-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="34046-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="34046-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="34046-133">Pacchetti firmati (creazione e la verifica)</span><span class="sxs-lookup"><span data-stu-id="34046-133">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="34046-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="34046-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="34046-135">Errori di input non validi</span><span class="sxs-lookup"><span data-stu-id="34046-135">Invalid input errors</span></span>

<span data-ttu-id="34046-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="34046-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="34046-137">NU1001</span><span class="sxs-lookup"><span data-stu-id="34046-137">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-138">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-138">**Issue**</span></span> | <span data-ttu-id="34046-139">Il progetto non contiene uno o più Framework.</span><span class="sxs-lookup"><span data-stu-id="34046-139">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="34046-140">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-140">**Example message**</span></span> | <span data-ttu-id="34046-141">*ProjA il progetto non specifica alcun framework di destinazione in c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="34046-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="34046-142">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-142">**Solution**</span></span> | <span data-ttu-id="34046-143">Aggiungere un `TargetFramework` o `TargetFrameworks` proprietà al file di progetto specificato.</span><span class="sxs-lookup"><span data-stu-id="34046-143">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="34046-144">NU1002</span><span class="sxs-lookup"><span data-stu-id="34046-144">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-145">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-145">**Issue**</span></span> | <span data-ttu-id="34046-146">Combinazione non valida di input con una parola chiave non CRITTOGRAFATO.</span><span class="sxs-lookup"><span data-stu-id="34046-146">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="34046-147">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-147">**Example message**</span></span> | <span data-ttu-id="34046-148">*'CLEAR' non può essere utilizzato in combinazione con altri valori*</span><span class="sxs-lookup"><span data-stu-id="34046-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="34046-149">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-149">**Solution**</span></span> | <span data-ttu-id="34046-150">Usare deselezionare singolarmente e omettere tutti gli altri input.</span><span class="sxs-lookup"><span data-stu-id="34046-150">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="34046-151">NU1003</span><span class="sxs-lookup"><span data-stu-id="34046-151">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-152">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-152">**Issue**</span></span> | <span data-ttu-id="34046-153">`PackageTargetFallback` e `AssetTargetFallback` comportamenti diversi per la selezione di risorse e non possono essere utilizzati insieme.</span><span class="sxs-lookup"><span data-stu-id="34046-153">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="34046-154">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-154">**Example message**</span></span> | <span data-ttu-id="34046-155">*PackageTargetFallback e AssetTargetFallback non possono essere utilizzati insieme. Rimuovere i riferimenti di PackageTargetFallback(deprecated) dall'ambiente del progetto.*</span><span class="sxs-lookup"><span data-stu-id="34046-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="34046-156">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-156">**Solution**</span></span> | <span data-ttu-id="34046-157">Rimuovere deprecate `PackageTargetFallback` elemento dal progetto.</span><span class="sxs-lookup"><span data-stu-id="34046-157">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="34046-158">Errori di pacchetto e progetto mancanti</span><span class="sxs-lookup"><span data-stu-id="34046-158">Missing package and project errors</span></span>

<span data-ttu-id="34046-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="34046-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="34046-160">NU1100</span><span class="sxs-lookup"><span data-stu-id="34046-160">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-161">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-161">**Issue**</span></span> | <span data-ttu-id="34046-162">Un gruppo di dipendenze non essere risolto.</span><span class="sxs-lookup"><span data-stu-id="34046-162">A dependency group not be resolved.</span></span> <span data-ttu-id="34046-163">Questo è un problema generico per tipi che non sono pacchetti o progetti.</span><span class="sxs-lookup"><span data-stu-id="34046-163">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="34046-164">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-164">**Example message**</span></span> | <span data-ttu-id="34046-165">*Impossibile risolvere System.Missing per net45*</span><span class="sxs-lookup"><span data-stu-id="34046-165">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="34046-166">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-166">**Solution**</span></span> | <span data-ttu-id="34046-167">Aprire il file di progetto ed esaminare l'elenco delle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="34046-167">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="34046-168">Verificare che ogni dipendenza presente per le origini del pacchetto in uso e che il pacchetto supporta il framework di destinazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="34046-168">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="34046-169">NU1101</span><span class="sxs-lookup"><span data-stu-id="34046-169">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-170">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-170">**Issue**</span></span> | <span data-ttu-id="34046-171">Impossibile trovare il pacchetto su tutte le origini.</span><span class="sxs-lookup"><span data-stu-id="34046-171">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="34046-172">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-172">**Example message**</span></span> | <span data-ttu-id="34046-173">*Impossibile trovare il pacchetto System.Missing. Nessun pacchetto esistenti con questo id nelle origini: dotnet-core, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="34046-173">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="34046-174">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-174">**Solution**</span></span> | <span data-ttu-id="34046-175">Esaminare le dipendenze del progetto in Visual Studio per verificare che il pacchetto corretto identificatore e numero di versione in uso.</span><span class="sxs-lookup"><span data-stu-id="34046-175">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="34046-176">Controllare inoltre che il [configurazione NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifica l'origine del pacchetto il prevede di utilizzare.</span><span class="sxs-lookup"><span data-stu-id="34046-176">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="34046-177">Se si utilizzano pacchetti contenenti [controllo delle versioni semantico 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), assicurarsi che si sta utilizzando il [V3 feed](https://api.nuget.org/v3/index.json) nel [configurazione NuGet](../consume-packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="34046-177">If you use packages that have [Semantic Versioning 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), please make sure that you are using the [V3 feed](https://api.nuget.org/v3/index.json) in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="34046-178">NU1102</span><span class="sxs-lookup"><span data-stu-id="34046-178">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-179">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-179">**Issue**</span></span> | <span data-ttu-id="34046-180">L'identificatore del pacchetto è stato trovato ma presente una versione all'interno dell'intervallo di dipendenza specificata non può essere una delle origini.</span><span class="sxs-lookup"><span data-stu-id="34046-180">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="34046-181">L'intervallo può essere specificato da un pacchetto e non dell'utente.</span><span class="sxs-lookup"><span data-stu-id="34046-181">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="34046-182">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-182">**Example message**</span></span> | <span data-ttu-id="34046-183">*Impossibile trovare il pacchetto NuGet.Versioning con la versione (> = 9.0.1)<br/> -30 trovare versioni in nuget.org [più vicino di versione: 4.0.0]<br/> -versioni 10 trovato in dotnet buildtools [più vicino di versione: 4.0.0-rc-2129]<br/> -9 trovato versioni in NuGetVolatile [più vicino di versione: 3.0.0-beta-00032]<br/> -0 versioni, vedere dotnet core<br/> -0 versioni, vedere dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="34046-183">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="34046-184">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-184">**Solution**</span></span> | <span data-ttu-id="34046-185">Modificare il file di progetto o `packages.config` per correggere la versione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="34046-185">Edit the project file or `packages.config` to correct the package version.</span></span> <span data-ttu-id="34046-186">Controllare inoltre che il [configurazione NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifica l'origine del pacchetto il prevede di utilizzare.</span><span class="sxs-lookup"><span data-stu-id="34046-186">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="34046-187">Potrebbe essere necessario modificare la versione requeted se il pacchetto fa riferimento direttamente il progetto.</span><span class="sxs-lookup"><span data-stu-id="34046-187">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="34046-188">NU1103</span><span class="sxs-lookup"><span data-stu-id="34046-188">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-189">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-189">**Issue**</span></span> | <span data-ttu-id="34046-190">Il progetto specificato una versione stabile per l'intervallo di dipendenza, ma nessuna versione stabile trovata in tale intervallo.</span><span class="sxs-lookup"><span data-stu-id="34046-190">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="34046-191">Le versioni non definitive sono state trovate, ma non sono consentite.</span><span class="sxs-lookup"><span data-stu-id="34046-191">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="34046-192">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-192">**Example message**</span></span> | <span data-ttu-id="34046-193">*Impossibile trovare un pacchetto stabile NuGet.Versioning con la versione (> = 3.0.0)<br/> -versioni 10 trovato in dotnet buildtools [più vicino di versione: 4.0.0-rc-2129]<br/> -versioni 9 trovato in NuGetVolatile [più vicino di versione: 3.0.0-beta-00032] <br/> -0 versioni, vedere dotnet core<br/> -0 versioni, vedere dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="34046-193">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="34046-194">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-194">**Solution**</span></span> |  <span data-ttu-id="34046-195">Modificare l'intervallo di versione nel file di progetto o `packages.config` per includere le versioni non definitive.</span><span class="sxs-lookup"><span data-stu-id="34046-195">Edit the version range in the project file or `packages.config` to include pre-release versions.</span></span> <span data-ttu-id="34046-196">Vedere [il controllo delle versioni di pacchetto](../reference/Package-Versioning.md).</span><span class="sxs-lookup"><span data-stu-id="34046-196">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="34046-197">NU1104</span><span class="sxs-lookup"><span data-stu-id="34046-197">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-198">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-198">**Issue**</span></span> | <span data-ttu-id="34046-199">Un elemento ProjectReference punta a un file che non esiste.</span><span class="sxs-lookup"><span data-stu-id="34046-199">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="34046-200">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-200">**Example message**</span></span> | <span data-ttu-id="34046-201">*Riferimento al progetto non esiste 'c:\a.csproj'. Verificare che il riferimento al progetto sia valido e che esista il file di progetto.*</span><span class="sxs-lookup"><span data-stu-id="34046-201">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="34046-202">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-202">**Solution**</span></span> | <span data-ttu-id="34046-203">Modificare il file di progetto per correggere il percorso per il progetto di riferimento o per rimuovere il riferimento all'elemento se non è più necessario.</span><span class="sxs-lookup"><span data-stu-id="34046-203">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="34046-204">NU1105</span><span class="sxs-lookup"><span data-stu-id="34046-204">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-205">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-205">**Issue**</span></span> | <span data-ttu-id="34046-206">Il file di progetto esiste ma è stata fornita alcuna informazione di ripristino per tale.</span><span class="sxs-lookup"><span data-stu-id="34046-206">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="34046-207">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-207">**Example message**</span></span> | <span data-ttu-id="34046-208">*Impossibile leggere le informazioni di progetto per 'c:\a.csproj'. Il file di progetto potrebbe essere destinazioni non valide o mancante necessarie per il ripristino.*</span><span class="sxs-lookup"><span data-stu-id="34046-208">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="34046-209">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-209">**Solution**</span></span> | <span data-ttu-id="34046-210">In Visual Studio, l'errore potrebbe indicare che il progetto viene scaricato, nel qual caso ricaricare il progetto.</span><span class="sxs-lookup"><span data-stu-id="34046-210">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="34046-211">Dalla riga di comando ciò vuol dire che il file è danneggiato o che non contenga personalizzata "dopo l'importazione" necessarie per il ripristino leggere il progetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="34046-211">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="34046-212">Verificare che il file di progetto sia valido e contiene una destinazione "dopo l'importazione".</span><span class="sxs-lookup"><span data-stu-id="34046-212">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="34046-213">NU1106</span><span class="sxs-lookup"><span data-stu-id="34046-213">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-214">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-214">**Issue**</span></span> | <span data-ttu-id="34046-215">Vincoli di dipendenza non possono essere risolti.</span><span class="sxs-lookup"><span data-stu-id="34046-215">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="34046-216">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-216">**Example message**</span></span> | <span data-ttu-id="34046-217">*Non è possibile soddisfare le richieste con conflitto per {id}: {percorso conflitto} Framework: {grafico di destinazione}*</span><span class="sxs-lookup"><span data-stu-id="34046-217">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> 
| <span data-ttu-id="34046-218">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-218">**Solution**</span></span> | <span data-ttu-id="34046-219">Modificare il file di progetto o `packages.config` per specificare gli intervalli di più flessibile per la dipendenza anziché la versione esatta.</span><span class="sxs-lookup"><span data-stu-id="34046-219">Edit the project file or `packages.config` to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="34046-220">NU1107 (in precedenza NU1607)</span><span class="sxs-lookup"><span data-stu-id="34046-220">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-221">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-221">**Issue**</span></span> | <span data-ttu-id="34046-222">Impossibile risolvere i vincoli di dipendenza tra pacchetti.</span><span class="sxs-lookup"><span data-stu-id="34046-222">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="34046-223">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-223">**Example message**</span></span> | <span data-ttu-id="34046-224">*Conflitto di versione per NuGet.Versioning. Fare riferimento il pacchetto direttamente dal progetto per risolvere il problema.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="34046-224">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="34046-225">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-225">**Solution**</span></span> | <span data-ttu-id="34046-226">Pacchetti con vincoli di dipendenza in versioni esatte non consentono altri pacchetti per incrementare la versione, se necessario.</span><span class="sxs-lookup"><span data-stu-id="34046-226">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="34046-227">Aggiungere un riferimento al progetto direttamente (nel file di progetto o `packages.config`) con la versione esatta richiesta.</span><span class="sxs-lookup"><span data-stu-id="34046-227">Add a reference to the project directly (in the project file or `packages.config`) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="34046-228">NU1108 (in precedenza NU1606)</span><span class="sxs-lookup"><span data-stu-id="34046-228">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-229">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-229">**Issue**</span></span> | <span data-ttu-id="34046-230">È stata rilevata una dipendenza circolare.</span><span class="sxs-lookup"><span data-stu-id="34046-230">A circular dependency was detected.</span></span> |
| <span data-ttu-id="34046-231">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-231">**Example message**</span></span> | <span data-ttu-id="34046-232">*Rilevato ciclo: A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="34046-232">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="34046-233">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-233">**Solution**</span></span> | <span data-ttu-id="34046-234">Il pacchetto sia stato creato in modo errato. contattare il proprietario del pacchetto per correggere il bug.</span><span class="sxs-lookup"><span data-stu-id="34046-234">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="34046-235">Errori di compatibilità</span><span class="sxs-lookup"><span data-stu-id="34046-235">Compatibility errors</span></span>

<span data-ttu-id="34046-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="34046-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="34046-237">NU1201</span><span class="sxs-lookup"><span data-stu-id="34046-237">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-238">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-238">**Issue**</span></span> | <span data-ttu-id="34046-239">Una dipendenza di progetto non contiene un framework compatibile con il progetto corrente.</span><span class="sxs-lookup"><span data-stu-id="34046-239">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="34046-240">In genere, il framework di destinazione del progetto è una versione successiva a quella del progetto consumer.</span><span class="sxs-lookup"><span data-stu-id="34046-240">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="34046-241">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-241">**Example message**</span></span> | <span data-ttu-id="34046-242">*Progetto ServerWeb non è compatibile con netstandard1.3 (. Moniker NETStandard, Version = v 1.3). Progetto supporta ServerWeb:<br/> -netstandard1.6 (. Moniker NETStandard, Version = v 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = v 1.0)*</span><span class="sxs-lookup"><span data-stu-id="34046-242">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="34046-243">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-243">**Solution**</span></span> | <span data-ttu-id="34046-244">Modificare il framework di destinazione del progetto a una versione uguale o inferiore a quella del progetto consumer.</span><span class="sxs-lookup"><span data-stu-id="34046-244">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="34046-245">NU1202</span><span class="sxs-lookup"><span data-stu-id="34046-245">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-246">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-246">**Issue**</span></span> | <span data-ttu-id="34046-247">Un pacchetto di dipendenze non contiene tutte le risorse compatibile con il progetto.</span><span class="sxs-lookup"><span data-stu-id="34046-247">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="34046-248">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-248">**Example message**</span></span> | <span data-ttu-id="34046-249">*Pacchetto System.ComponentModel.EventBasedAsync 4.0.11 non è compatibile con netstandard1.3 (. Moniker NETStandard, Version = v 1.3). Creare il pacchetto supporta System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, Version = v 1.0)<br/> -monotouch10 (MonoTouch, Version = v 1.0)<br/> -net45 (. NETFramework, Version = v 4.5)<br/> -netcore50 (. NETCore, Version = v 5.0)<br/> -netstandard1.0 (. Moniker NETStandard, Version = v 1.0)<br/> -portabile net45 win8 wp8 + wpa81 (. NETPortable, versione = v0.0, profilo = Profile259)<br/> -win8 (Windows, Version = v 8.0)<br/> -wp8 (WindowsPhone, Version = v 8.0)<br/> -wpa81 (WindowsPhoneApp, Version = v 8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="34046-249">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="34046-250">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-250">**Solution**</span></span> | <span data-ttu-id="34046-251">Modificare il framework di destinazione del progetto in modo che il pacchetto supporta.</span><span class="sxs-lookup"><span data-stu-id="34046-251">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="34046-252">NU1203</span><span class="sxs-lookup"><span data-stu-id="34046-252">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-253">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-253">**Issue**</span></span> | <span data-ttu-id="34046-254">Il pacchetto non supporta il progetto `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="34046-254">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="34046-255">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-255">**Example message**</span></span> | <span data-ttu-id="34046-256">*System.Example 1.0.0 fornisce un assembly di riferimento in fase di compilazione per DLL in net461, ma non sono presenti assembly di runtime compatibili.*</span><span class="sxs-lookup"><span data-stu-id="34046-256">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="34046-257">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-257">**Solution**</span></span> | <span data-ttu-id="34046-258">Modifica il `RuntimeIdentifier` valori usati nel progetto in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="34046-258">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="34046-259">NU1401</span><span class="sxs-lookup"><span data-stu-id="34046-259">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-260">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-260">**Issue**</span></span> | <span data-ttu-id="34046-261">Il pacchetto richiede caratteristiche o Framework non sono attualmente supportati dalla versione installata di NuGet.</span><span class="sxs-lookup"><span data-stu-id="34046-261">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="34046-262">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-262">**Example message**</span></span> | <span data-ttu-id="34046-263">*Il pacchetto 'NuGet.Versioning' richiede '5.0.0' alla versione client NuGet o versione successiva, ma la versione NuGet corrente è '4.3.0'.*</span><span class="sxs-lookup"><span data-stu-id="34046-263">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="34046-264">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-264">**Solution**</span></span> | <span data-ttu-id="34046-265">Installare una versione più recente di NuGet.</span><span class="sxs-lookup"><span data-stu-id="34046-265">Install a newer version of NuGet.</span></span> <span data-ttu-id="34046-266">Vedere [gli strumenti client di installazione di NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="34046-266">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="34046-267">Avvisi di input non validi</span><span class="sxs-lookup"><span data-stu-id="34046-267">Invalid input warnings</span></span>

<span data-ttu-id="34046-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="34046-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="34046-269">NU1501</span><span class="sxs-lookup"><span data-stu-id="34046-269">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-270">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-270">**Issue**</span></span> | <span data-ttu-id="34046-271">Il ripristino del progetto sta tentando di operare in non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="34046-271">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="34046-272">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-272">**Example message**</span></span> | <span data-ttu-id="34046-273">*La cartella 'c:\projects\a' non contiene un progetto da ripristinare.*</span><span class="sxs-lookup"><span data-stu-id="34046-273">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="34046-274">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-274">**Solution**</span></span> | <span data-ttu-id="34046-275">Esegue nuget restore in una cartella che contiene un progetto.</span><span class="sxs-lookup"><span data-stu-id="34046-275">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="34046-276">NU1502</span><span class="sxs-lookup"><span data-stu-id="34046-276">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-277">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-277">**Issue**</span></span> | <span data-ttu-id="34046-278">`RuntimeSupports` contiene un profilo non valido.</span><span class="sxs-lookup"><span data-stu-id="34046-278">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="34046-279">In genere, il profilo supporta non è stato trovato un `runtime.json` file dai pacchetti dipendenza corrente.</span><span class="sxs-lookup"><span data-stu-id="34046-279">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="34046-280">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-280">**Example message**</span></span> | <span data-ttu-id="34046-281">*Profilo di compatibilità sconosciuto: aaa*</span><span class="sxs-lookup"><span data-stu-id="34046-281">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="34046-282">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-282">**Solution**</span></span> | <span data-ttu-id="34046-283">Controllare il `RuntimeSupports` valore nel progetto.</span><span class="sxs-lookup"><span data-stu-id="34046-283">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="34046-284">NU1503</span><span class="sxs-lookup"><span data-stu-id="34046-284">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-285">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-285">**Issue**</span></span> | <span data-ttu-id="34046-286">Una dipendenza di progetto non importa le destinazioni di ripristino di NuGet.</span><span class="sxs-lookup"><span data-stu-id="34046-286">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="34046-287">È simile a NU1105 ma qui il progetto viene ignorato e ignorato anziché causare tutte esito negativo del ripristino.</span><span class="sxs-lookup"><span data-stu-id="34046-287">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="34046-288">Nelle soluzioni complesse sono spesso altri tipi di progetti che non supportano il ripristino.</span><span class="sxs-lookup"><span data-stu-id="34046-288">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="34046-289">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-289">**Example message**</span></span> | <span data-ttu-id="34046-290">*Mancato ripristino per il progetto 'c:\a.csproj'. Il file di progetto potrebbe essere destinazioni non valide o mancante necessarie per il ripristino.*</span><span class="sxs-lookup"><span data-stu-id="34046-290">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="34046-291">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-291">**Solution**</span></span> | <span data-ttu-id="34046-292">Questa situazione può verificarsi per i progetti che non si importano props/destinazioni comuni quali l'importazione automatica di ripristino.</span><span class="sxs-lookup"><span data-stu-id="34046-292">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="34046-293">Se il progetto non è necessaria per il ripristino può essere ignorato.</span><span class="sxs-lookup"><span data-stu-id="34046-293">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="34046-294">In caso contrario, modificare il progetto interessato per aggiungere destinazioni per il ripristino.</span><span class="sxs-lookup"><span data-stu-id="34046-294">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="34046-295">Avvisi di versione di pacchetto imprevisto</span><span class="sxs-lookup"><span data-stu-id="34046-295">Unexpected package version warnings</span></span>

<span data-ttu-id="34046-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="34046-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="34046-297">NU1601</span><span class="sxs-lookup"><span data-stu-id="34046-297">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-298">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-298">**Issue**</span></span> | <span data-ttu-id="34046-299">Una dipendenza diretta del progetto è stato ha respinto per una versione successiva a quella del progetto specificato.</span><span class="sxs-lookup"><span data-stu-id="34046-299">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="34046-300">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-300">**Example message**</span></span> | <span data-ttu-id="34046-301">*Dipendenza specificata è NuGet.Versioning (> = 3.5.0) ma è risultata NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="34046-301">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="34046-302">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-302">**Solution**</span></span> | <span data-ttu-id="34046-303">Aggiornare la dipendenza nel progetto a una versione appropriata.</span><span class="sxs-lookup"><span data-stu-id="34046-303">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="34046-304">NU1602</span><span class="sxs-lookup"><span data-stu-id="34046-304">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-305">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-305">**Issue**</span></span> | <span data-ttu-id="34046-306">Una dipendenza pacchetto manca un limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="34046-306">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="34046-307">Questo non consente il ripristino trovare il *migliore corrispondenza*.</span><span class="sxs-lookup"><span data-stu-id="34046-307">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="34046-308">Ogni ripristino verrà spostata verso il basso il tentativo di trovare una versione precedente che può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="34046-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="34046-309">Ciò significa che il ripristino passa nello stato online per controllare tutte le origini di ogni volta che invece di usare i pacchetti già esistenti nella cartella del pacchetto utente.</span><span class="sxs-lookup"><span data-stu-id="34046-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="34046-310">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-310">**Example message**</span></span> | <span data-ttu-id="34046-311">*NuGet. Packaging 4.0.0 non prevede un limite inferiore inclusivo dipendenza NuGet.Versioning (3.5.0 >). Una corrispondenza migliore approssimativa di 3.6.0 è stato risolta.*</span><span class="sxs-lookup"><span data-stu-id="34046-311">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="34046-312">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-312">**Solution**</span></span> | <span data-ttu-id="34046-313">In genere si tratta di un pacchetto con errore di creazione.</span><span class="sxs-lookup"><span data-stu-id="34046-313">This is usually a package authoring error.</span></span> <span data-ttu-id="34046-314">Contattare l'autore del pacchetto per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="34046-314">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="34046-315">NU1603</span><span class="sxs-lookup"><span data-stu-id="34046-315">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-316">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-316">**Issue**</span></span> | <span data-ttu-id="34046-317">Una dipendenza pacchetto specificata una versione che non è stata trovata.</span><span class="sxs-lookup"><span data-stu-id="34046-317">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="34046-318">In genere, le origini del pacchetto non contengono la versione prevista limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="34046-318">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="34046-319">È stata utilizzata una versione successiva, che differisce da cosa è stato creato il pacchetto base.</span><span class="sxs-lookup"><span data-stu-id="34046-319">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="34046-320">Ciò significa che il ripristino non è stata trovata la *migliore corrispondenza*.</span><span class="sxs-lookup"><span data-stu-id="34046-320">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="34046-321">Ogni ripristino verrà spostata verso il basso il tentativo di trovare una versione precedente che può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="34046-321">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="34046-322">Ciò significa che il ripristino passa nello stato online per controllare tutte le origini di ogni volta che invece di usare i pacchetti già esistenti nella cartella del pacchetto utente.</span><span class="sxs-lookup"><span data-stu-id="34046-322">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="34046-323">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-323">**Example message**</span></span> | <span data-ttu-id="34046-324">NuGet. Packaging 4.0.0 dipende NuGet.Versioning (> = 4.0.0) 4.0.0 non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="34046-324">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="34046-325">Una corrispondenza migliore approssimativa di 5.0.0 è stato risolta.</span><span class="sxs-lookup"><span data-stu-id="34046-325">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="34046-326">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-326">**Solution**</span></span> | <span data-ttu-id="34046-327">Se il pacchetto previsto non è stato rilasciato quindi potrebbe trattarsi di un pacchetto con errore di creazione.</span><span class="sxs-lookup"><span data-stu-id="34046-327">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="34046-328">Contattare l'autore del pacchetto per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="34046-328">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="34046-329">Se il pacchetto è stato rilasciato, controllare che sia disponibile per le origini del pacchetto in uso.</span><span class="sxs-lookup"><span data-stu-id="34046-329">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="34046-330">Se si utilizza un'origine privata, si potrebbe essere necessario aggiornare il pacchetto su tale feed.</span><span class="sxs-lookup"><span data-stu-id="34046-330">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="34046-331">NU1604</span><span class="sxs-lookup"><span data-stu-id="34046-331">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-332">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-332">**Issue**</span></span> | <span data-ttu-id="34046-333">Dipendenza di progetto non viene definito un limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="34046-333">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="34046-334">Ciò significa che il ripristino non è stata trovata la *migliore corrispondenza*.</span><span class="sxs-lookup"><span data-stu-id="34046-334">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="34046-335">Ogni ripristino verrà spostata verso il basso il tentativo di trovare una versione precedente che può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="34046-335">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="34046-336">Ciò significa che il ripristino passa nello stato online per controllare tutte le origini di ogni volta che invece di usare i pacchetti già esistenti nella cartella del pacchetto utente.</span><span class="sxs-lookup"><span data-stu-id="34046-336">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="34046-337">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-337">**Example message**</span></span> | <span data-ttu-id="34046-338">*Progetto dipendenza NuGet.Versioning (< = 9.0.0) doe non contengono un limite inferiore inclusivo. Includere un limite inferiore nella versione di dipendenza per garantire risultati coerenti di ripristino.*</span><span class="sxs-lookup"><span data-stu-id="34046-338">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="34046-339">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-339">**Solution**</span></span> | <span data-ttu-id="34046-340">Aggiornare il progetto `PackageReference` `Version` attributo da includere un limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="34046-340">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="34046-341">NU1605</span><span class="sxs-lookup"><span data-stu-id="34046-341">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-342">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-342">**Issue**</span></span> | <span data-ttu-id="34046-343">Un pacchetto di dipendenza è specificato un vincolo di versione in una versione superiore di un pacchetto rispetto al ripristino risolta.</span><span class="sxs-lookup"><span data-stu-id="34046-343">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="34046-344">Ovvero "più vicino wins" regola per la risoluzione dei pacchetti, a causa di un pacchetto più vicini nel grafico può avere sottoposto a override un pacchetto distante.</span><span class="sxs-lookup"><span data-stu-id="34046-344">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="34046-345">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-345">**Example message**</span></span> | <span data-ttu-id="34046-346">*Rilevato downgrade del pacchetto: NuGet.Versioning da 4.0.0 a 3.5.0. Fare riferimento il pacchetto direttamente dal progetto per selezionare una versione diversa.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="34046-346">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="34046-347">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-347">**Solution**</span></span> | <span data-ttu-id="34046-348">Aggiungere un riferimento diretto al progetto per la successiva versione del pacchetto che si desidera utilizzare.</span><span class="sxs-lookup"><span data-stu-id="34046-348">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="34046-349">Avvisi di sistema di risoluzione dei conflitti</span><span class="sxs-lookup"><span data-stu-id="34046-349">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="34046-350">NU1608</span><span class="sxs-lookup"><span data-stu-id="34046-350">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-351">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-351">**Issue**</span></span> | <span data-ttu-id="34046-352">Un pacchetto risolto è supera a quello di un vincolo di dipendenza.</span><span class="sxs-lookup"><span data-stu-id="34046-352">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="34046-353">Ciò significa che un pacchetto a cui fa riferimento direttamente un progetto ignora i vincoli di dipendenze da altri pacchetti.</span><span class="sxs-lookup"><span data-stu-id="34046-353">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="34046-354">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-354">**Example message**</span></span> | <span data-ttu-id="34046-355">*Versione del pacchetto rilevato all'esterno di vincolo dipendenza: x 1.0.0 richiede y (= 1.0.0) ma versione 2.0.0 y è stato risolto.*</span><span class="sxs-lookup"><span data-stu-id="34046-355">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="34046-356">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-356">**Solution**</span></span> | <span data-ttu-id="34046-357">In alcuni casi ciò è intenzionale e l'avviso può essere eliminato.</span><span class="sxs-lookup"><span data-stu-id="34046-357">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="34046-358">In caso contrario, modificare il riferimento del progetto al pacchetto per ampliare i vincoli di versione.</span><span class="sxs-lookup"><span data-stu-id="34046-358">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="34046-359">Avvisi di fallback di pacchetto</span><span class="sxs-lookup"><span data-stu-id="34046-359">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="34046-360">NU1701</span><span class="sxs-lookup"><span data-stu-id="34046-360">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-361">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-361">**Issue**</span></span> | <span data-ttu-id="34046-362">`PackageTargetFallback` / `AssetTargetFallback` è stato usato per selezionare asset da un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="34046-362">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="34046-363">Avviso di informerà gli utenti che le risorse potrebbero non essere compatibile al 100%.</span><span class="sxs-lookup"><span data-stu-id="34046-363">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="34046-364">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-364">**Example message**</span></span> | <span data-ttu-id="34046-365">*Pacchetto 'NuGet.Versioning' è stato ripristinato mediante 'portable net45 + win8' invece del framework di destinazione del progetto 'netstandard1.5'. Questo pacchetto potrebbe non essere completamente compatibile con il progetto.*</span><span class="sxs-lookup"><span data-stu-id="34046-365">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="34046-366">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-366">**Solution**</span></span> | <span data-ttu-id="34046-367">Modificare il framework di destinazione del progetto in modo che il pacchetto supporta.</span><span class="sxs-lookup"><span data-stu-id="34046-367">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="34046-368">Feed di avvisi</span><span class="sxs-lookup"><span data-stu-id="34046-368">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="34046-369">NU1801</span><span class="sxs-lookup"><span data-stu-id="34046-369">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-370">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-370">**Issue**</span></span> | <span data-ttu-id="34046-371">Si è verificato un errore durante la lettura dei feed quando `IgnoreFailedSources` è impostata su true, convertendolo in un messaggio di avviso non irreversibile.</span><span class="sxs-lookup"><span data-stu-id="34046-371">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="34046-372">Ciò può contenere qualsiasi messaggio ed è generico.</span><span class="sxs-lookup"><span data-stu-id="34046-372">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="34046-373">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-373">**Example message**</span></span> | <span data-ttu-id="34046-374">N/D</span><span class="sxs-lookup"><span data-stu-id="34046-374">n/a</span></span> |
| <span data-ttu-id="34046-375">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-375">**Solution**</span></span> | <span data-ttu-id="34046-376">Modificare la configurazione per specificare le origini valide.</span><span class="sxs-lookup"><span data-stu-id="34046-376">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="34046-377">Avvisi ed errori interni di NuGet</span><span class="sxs-lookup"><span data-stu-id="34046-377">NuGet internal errors and warnings</span></span>

<span data-ttu-id="34046-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="34046-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="34046-379">NU1000</span><span class="sxs-lookup"><span data-stu-id="34046-379">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-380">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-380">**Issue**</span></span> | <span data-ttu-id="34046-381">Un errore interno non specifico da NuGet.</span><span class="sxs-lookup"><span data-stu-id="34046-381">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="34046-382">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-382">**Solution**</span></span> | <span data-ttu-id="34046-383">Controllare i registri per ulteriori informazioni</span><span class="sxs-lookup"><span data-stu-id="34046-383">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="34046-384">NU1500</span><span class="sxs-lookup"><span data-stu-id="34046-384">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-385">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-385">**Issue**</span></span> | <span data-ttu-id="34046-386">Un avviso interno non specifico da NuGet.</span><span class="sxs-lookup"><span data-stu-id="34046-386">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="34046-387">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-387">**Solution**</span></span> | <span data-ttu-id="34046-388">Controllare i registri per ulteriori informazioni</span><span class="sxs-lookup"><span data-stu-id="34046-388">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="34046-389">Pacchetti firmati (creazione e la verifica)</span><span class="sxs-lookup"><span data-stu-id="34046-389">Signed packages (creation and verification)</span></span>

<span data-ttu-id="34046-390">*NuGet 4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="34046-390">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="34046-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="34046-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="34046-392">NU3000</span><span class="sxs-lookup"><span data-stu-id="34046-392">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-393">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-393">**Issue**</span></span> | <span data-ttu-id="34046-394">Un errore non specifico relativo alla firma del pacchetto e firmati verifica del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="34046-394">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="34046-395">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-395">**Solution**</span></span> | <span data-ttu-id="34046-396">Controllare i registri per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="34046-396">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="34046-397">NU3001</span><span class="sxs-lookup"><span data-stu-id="34046-397">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-398">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-398">**Issue**</span></span> | <span data-ttu-id="34046-399">Argomenti non validi a uno di [firmare comando](../tools/cli-ref-sign.md) o [verificare comando](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="34046-399">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="34046-400">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-400">**Solution**</span></span> | <span data-ttu-id="34046-401">Controllare e correggere gli argomenti forniti.</span><span class="sxs-lookup"><span data-stu-id="34046-401">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="34046-402">NU3002</span><span class="sxs-lookup"><span data-stu-id="34046-402">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-403">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-403">**Issue**</span></span> | <span data-ttu-id="34046-404">Il `-Timestamper` non è stata specificata con il [comando sign nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="34046-404">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="34046-405">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-405">**Example message**</span></span> | <span data-ttu-id="34046-406">*Il '-Timestamper' opzione non è stato specificato. Il pacchetto firmato non saranno impostati i timestamp.*</span><span class="sxs-lookup"><span data-stu-id="34046-406">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="34046-407">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-407">**Solution**</span></span> | <span data-ttu-id="34046-408">Specificare il `-Timestamper` con `nuget sign`.</span><span class="sxs-lookup"><span data-stu-id="34046-408">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="34046-409">NU3004</span><span class="sxs-lookup"><span data-stu-id="34046-409">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-410">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-410">**Issue**</span></span> | <span data-ttu-id="34046-411">È stato fornito un pacchetto non firmato per il [nuget verificare comando](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="34046-411">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="34046-412">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-412">**Solution**</span></span> | <span data-ttu-id="34046-413">Eseguire `nuget verify` con un pacchetto firmato.</span><span class="sxs-lookup"><span data-stu-id="34046-413">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="34046-414">Vedere [firmare un pacchetto](../create-packages/Sign-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="34046-414">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="34046-415">NU3008</span><span class="sxs-lookup"><span data-stu-id="34046-415">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-416">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-416">**Issue**</span></span> | <span data-ttu-id="34046-417">Il pacchetto non riuscito, vale a dire che un pacchetto firmato sia stato manomesso dopo l'accesso.</span><span class="sxs-lookup"><span data-stu-id="34046-417">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="34046-418">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-418">**Solution**</span></span> | <span data-ttu-id="34046-419">Scansione del computer con un software antivirus.</span><span class="sxs-lookup"><span data-stu-id="34046-419">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="34046-420">Quindi rimuovere il pacchetto dal computer, reinstallarlo e riprovare.</span><span class="sxs-lookup"><span data-stu-id="34046-420">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="34046-421">Se il problema persiste, contattare il proprietario dell'origine del pacchetto e il proprietario del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="34046-421">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="34046-422">NU3018</span><span class="sxs-lookup"><span data-stu-id="34046-422">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-423">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-423">**Issue**</span></span> | <span data-ttu-id="34046-424">Non è riuscita la creazione della catena di certificati per la firma primaria.</span><span class="sxs-lookup"><span data-stu-id="34046-424">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="34046-425">Il certificato di firma primario non è attendibile, revocato, o informazioni di revoca per il certificato non sono disponibile.</span><span class="sxs-lookup"><span data-stu-id="34046-425">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="34046-426">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-426">**Example message**</span></span> | <span data-ttu-id="34046-427">*Avviso: NU3018: la funzione di revoca non è riuscita a controllare la revoca del certificato.*</span><span class="sxs-lookup"><span data-stu-id="34046-427">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="34046-428">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-428">**Solution**</span></span> | <span data-ttu-id="34046-429">Usare un certificato attendibile e valido.</span><span class="sxs-lookup"><span data-stu-id="34046-429">Use a trusted and valid certificate.</span></span> <span data-ttu-id="34046-430">Verificare la connettività internet.</span><span class="sxs-lookup"><span data-stu-id="34046-430">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="34046-431">NU3028</span><span class="sxs-lookup"><span data-stu-id="34046-431">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="34046-432">**Problema**</span><span class="sxs-lookup"><span data-stu-id="34046-432">**Issue**</span></span> | <span data-ttu-id="34046-433">Non è riuscita la creazione della catena di certificati per la firma del timestamp.</span><span class="sxs-lookup"><span data-stu-id="34046-433">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="34046-434">Il certificato di firma del timestamp non è attendibile, revocato, o informazioni di revoca per il certificato non sono disponibile.</span><span class="sxs-lookup"><span data-stu-id="34046-434">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="34046-435">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="34046-435">**Example message**</span></span> | <span data-ttu-id="34046-436">*Avviso: NU3028: la funzione di revoca non è riuscita a controllare la revoca del certificato.*</span><span class="sxs-lookup"><span data-stu-id="34046-436">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="34046-437">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="34046-437">**Solution**</span></span> | <span data-ttu-id="34046-438">Usare un certificato attendibile e valido.</span><span class="sxs-lookup"><span data-stu-id="34046-438">Use a trusted and valid certificate.</span></span> <span data-ttu-id="34046-439">Verificare la connettività internet.</span><span class="sxs-lookup"><span data-stu-id="34046-439">Check internet connectivity.</span></span> |
