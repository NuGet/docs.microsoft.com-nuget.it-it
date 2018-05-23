---
title: NuGet errori e avvisi riferimento
description: Riferimento complete per avvisi ed errori generati da NuGet durante le varie operazioni di NuGet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
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
ms.openlocfilehash: 748c2746a61886617e2eefe3e6c4a2e2a5b9d4d3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="8e6eb-103">Errori e avvisi</span><span class="sxs-lookup"><span data-stu-id="8e6eb-103">Errors and warnings</span></span>

<span data-ttu-id="8e6eb-104">In NuGet 4.3.0+, errori e avvisi sono numerati come descritto in questo argomento e forniscono informazioni dettagliate che consentono di risolvere i problemi che interessano.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-104">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="8e6eb-105">Gli errori e avvisi elencati di seguito sono disponibili solo con [basato su PackageReference](../consume-packages/package-references-in-project-files.md) 4.3.0+ NuGet e progetti.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-105">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="8e6eb-106">NuGet anche rispetta la proprietà di MSBuild per l'esclusione di avvisi o li elevare a errori.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-106">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="8e6eb-107">Per ulteriori informazioni, vedere [procedura: esclusione di avvisi del compilatore](/visualstudio/ide/how-to-suppress-compiler-warnings) nella documentazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-107">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="8e6eb-108">**Errori**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-108">**Errors**</span></span>

| <span data-ttu-id="8e6eb-109">Gruppo</span><span class="sxs-lookup"><span data-stu-id="8e6eb-109">Group</span></span> | <span data-ttu-id="8e6eb-110">Numeri di errore</span><span class="sxs-lookup"><span data-stu-id="8e6eb-110">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="8e6eb-111">Errori di input non validi</span><span class="sxs-lookup"><span data-stu-id="8e6eb-111">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="8e6eb-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="8e6eb-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="8e6eb-113">Errori di pacchetto e progetto mancanti</span><span class="sxs-lookup"><span data-stu-id="8e6eb-113">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="8e6eb-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (in precedenza NU1607), [NU1108](#nu1108) (in precedenza NU1606)</span><span class="sxs-lookup"><span data-stu-id="8e6eb-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="8e6eb-115">Errori di compatibilità</span><span class="sxs-lookup"><span data-stu-id="8e6eb-115">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="8e6eb-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="8e6eb-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="8e6eb-117">**Avvisi**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-117">**Warnings**</span></span>

| <span data-ttu-id="8e6eb-118">Gruppo</span><span class="sxs-lookup"><span data-stu-id="8e6eb-118">Group</span></span> | <span data-ttu-id="8e6eb-119">Numeri di avviso</span><span class="sxs-lookup"><span data-stu-id="8e6eb-119">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="8e6eb-120">Avvisi di input non validi</span><span class="sxs-lookup"><span data-stu-id="8e6eb-120">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="8e6eb-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="8e6eb-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="8e6eb-122">Avvisi di versione di pacchetto imprevisto</span><span class="sxs-lookup"><span data-stu-id="8e6eb-122">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="8e6eb-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="8e6eb-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="8e6eb-124">Avvisi di sistema di risoluzione dei conflitti</span><span class="sxs-lookup"><span data-stu-id="8e6eb-124">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="8e6eb-125">NU1608</span><span class="sxs-lookup"><span data-stu-id="8e6eb-125">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="8e6eb-126">Avvisi di fallback di pacchetto</span><span class="sxs-lookup"><span data-stu-id="8e6eb-126">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="8e6eb-127">NU1701</span><span class="sxs-lookup"><span data-stu-id="8e6eb-127">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="8e6eb-128">Feed di avvisi</span><span class="sxs-lookup"><span data-stu-id="8e6eb-128">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="8e6eb-129">NU1801</span><span class="sxs-lookup"><span data-stu-id="8e6eb-129">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="8e6eb-130">Avvisi ed errori interni di NuGet</span><span class="sxs-lookup"><span data-stu-id="8e6eb-130">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="8e6eb-131">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="8e6eb-131">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="8e6eb-132">Pacchetti firmati (creazione e la verifica)</span><span class="sxs-lookup"><span data-stu-id="8e6eb-132">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="8e6eb-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="8e6eb-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="8e6eb-134">Errori di input non validi</span><span class="sxs-lookup"><span data-stu-id="8e6eb-134">Invalid input errors</span></span>

<span data-ttu-id="8e6eb-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="8e6eb-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="8e6eb-136">NU1001</span><span class="sxs-lookup"><span data-stu-id="8e6eb-136">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-137">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-137">**Issue**</span></span> | <span data-ttu-id="8e6eb-138">Il progetto non contiene uno o più Framework.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-138">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="8e6eb-139">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-139">**Example message**</span></span> | <span data-ttu-id="8e6eb-140">*ProjA il progetto non specifica alcun framework di destinazione in c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-140">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="8e6eb-141">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-141">**Solution**</span></span> | <span data-ttu-id="8e6eb-142">Aggiungere un `TargetFramework` o `TargetFrameworks` proprietà al file di progetto specificato.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-142">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="8e6eb-143">NU1002</span><span class="sxs-lookup"><span data-stu-id="8e6eb-143">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-144">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-144">**Issue**</span></span> | <span data-ttu-id="8e6eb-145">Combinazione non valida di input con una parola chiave non CRITTOGRAFATO.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-145">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="8e6eb-146">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-146">**Example message**</span></span> | <span data-ttu-id="8e6eb-147">*'CLEAR' non può essere utilizzato in combinazione con altri valori*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-147">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="8e6eb-148">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-148">**Solution**</span></span> | <span data-ttu-id="8e6eb-149">Usare deselezionare singolarmente e omettere tutti gli altri input.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-149">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="8e6eb-150">NU1003</span><span class="sxs-lookup"><span data-stu-id="8e6eb-150">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-151">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-151">**Issue**</span></span> | <span data-ttu-id="8e6eb-152">`PackageTargetFallback` e `AssetTargetFallback` comportamenti diversi per la selezione di risorse e non possono essere utilizzati insieme.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-152">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="8e6eb-153">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-153">**Example message**</span></span> | <span data-ttu-id="8e6eb-154">*PackageTargetFallback e AssetTargetFallback non possono essere utilizzati insieme. Rimuovere i riferimenti di PackageTargetFallback(deprecated) dall'ambiente del progetto.*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-154">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="8e6eb-155">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-155">**Solution**</span></span> | <span data-ttu-id="8e6eb-156">Rimuovere deprecate `PackageTargetFallback` elemento dal progetto.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-156">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="8e6eb-157">Errori di pacchetto e progetto mancanti</span><span class="sxs-lookup"><span data-stu-id="8e6eb-157">Missing package and project errors</span></span>

<span data-ttu-id="8e6eb-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="8e6eb-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="8e6eb-159">NU1100</span><span class="sxs-lookup"><span data-stu-id="8e6eb-159">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-160">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-160">**Issue**</span></span> | <span data-ttu-id="8e6eb-161">Un gruppo di dipendenze non essere risolto.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-161">A dependency group not be resolved.</span></span> <span data-ttu-id="8e6eb-162">Questo è un problema generico per tipi che non sono pacchetti o progetti.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-162">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="8e6eb-163">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-163">**Example message**</span></span> | <span data-ttu-id="8e6eb-164">*Impossibile risolvere System.Missing per net45*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-164">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="8e6eb-165">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-165">**Solution**</span></span> | <span data-ttu-id="8e6eb-166">Aprire il file di progetto ed esaminare l'elenco delle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-166">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="8e6eb-167">Verificare che ogni dipendenza presente per le origini del pacchetto in uso e che il pacchetto supporta il framework di destinazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-167">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="8e6eb-168">NU1101</span><span class="sxs-lookup"><span data-stu-id="8e6eb-168">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-169">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-169">**Issue**</span></span> | <span data-ttu-id="8e6eb-170">Impossibile trovare il pacchetto su tutte le origini.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-170">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="8e6eb-171">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-171">**Example message**</span></span> | <span data-ttu-id="8e6eb-172">*Impossibile trovare il pacchetto System.Missing. Nessun pacchetto esistenti con questo id nelle origini: dotnet-core, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="8e6eb-173">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-173">**Solution**</span></span> | <span data-ttu-id="8e6eb-174">Esaminare le dipendenze del progetto in Visual Studio per verificare che il pacchetto corretto identificatore e numero di versione in uso.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-174">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="8e6eb-175">Controllare inoltre che il [configurazione NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifica l'origine del pacchetto il prevede di utilizzare.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-175">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="8e6eb-176">Se si utilizzano i pacchetti che presentano [controllo delle versioni semantico 2.0.0](../reference/package-versioning.md#semantic-versioning-200), assicurarsi che si sta utilizzando V3 feed, `https://api.nuget.org/v3/index.json`nella [configurazione NuGet](../consume-packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="8e6eb-176">If you use packages that have [Semantic Versioning 2.0.0](../reference/package-versioning.md#semantic-versioning-200), please make sure that you are using the V3 feed, `https://api.nuget.org/v3/index.json`, in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="8e6eb-177">NU1102</span><span class="sxs-lookup"><span data-stu-id="8e6eb-177">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-178">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-178">**Issue**</span></span> | <span data-ttu-id="8e6eb-179">L'identificatore del pacchetto è stato trovato ma presente una versione all'interno dell'intervallo di dipendenza specificata non può essere una delle origini.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-179">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="8e6eb-180">L'intervallo può essere specificato da un pacchetto e non dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-180">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="8e6eb-181">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-181">**Example message**</span></span> | <span data-ttu-id="8e6eb-182">*Impossibile trovare il pacchetto NuGet.Versioning con la versione (> = 9.0.1)<br/> -30 trovare versioni in nuget.org [più vicino di versione: 4.0.0]<br/> -versioni 10 trovato in dotnet buildtools [più vicino di versione: 4.0.0-rc-2129]<br/> -9 trovato versioni in NuGetVolatile [più vicino di versione: 3.0.0-beta-00032]<br/> -0 versioni, vedere dotnet core<br/> -0 versioni, vedere dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-182">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="8e6eb-183">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-183">**Solution**</span></span> | <span data-ttu-id="8e6eb-184">Modificare il file di progetto per risolvere la versione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-184">Edit the project file to correct the package version.</span></span> <span data-ttu-id="8e6eb-185">Controllare inoltre che il [configurazione NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifica l'origine del pacchetto il prevede di utilizzare.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-185">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="8e6eb-186">Potrebbe essere necessario modificare la versione requeted se il pacchetto fa riferimento direttamente il progetto.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-186">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="8e6eb-187">NU1103</span><span class="sxs-lookup"><span data-stu-id="8e6eb-187">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-188">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-188">**Issue**</span></span> | <span data-ttu-id="8e6eb-189">Il progetto specificato una versione stabile per l'intervallo di dipendenza, ma nessuna versione stabile trovata in tale intervallo.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-189">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="8e6eb-190">Le versioni non definitive sono state trovate, ma non sono consentite.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-190">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="8e6eb-191">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-191">**Example message**</span></span> | <span data-ttu-id="8e6eb-192">*Impossibile trovare un pacchetto stabile NuGet.Versioning con la versione (> = 3.0.0)<br/> -versioni 10 trovato in dotnet buildtools [più vicino di versione: 4.0.0-rc-2129]<br/> -versioni 9 trovato in NuGetVolatile [più vicino di versione: 3.0.0-beta-00032] <br/> -0 versioni, vedere dotnet core<br/> -0 versioni, vedere dotnet roslyn*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-192">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="8e6eb-193">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-193">**Solution**</span></span> |  <span data-ttu-id="8e6eb-194">Modificare l'intervallo di versione nel file di progetto per includere le versioni non definitive.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-194">Edit the version range in the project file to include pre-release versions.</span></span> <span data-ttu-id="8e6eb-195">Vedere [il controllo delle versioni di pacchetto](../reference/Package-Versioning.md).</span><span class="sxs-lookup"><span data-stu-id="8e6eb-195">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="8e6eb-196">NU1104</span><span class="sxs-lookup"><span data-stu-id="8e6eb-196">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-197">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-197">**Issue**</span></span> | <span data-ttu-id="8e6eb-198">Un elemento ProjectReference punta a un file che non esiste.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-198">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="8e6eb-199">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-199">**Example message**</span></span> | <span data-ttu-id="8e6eb-200">*Riferimento al progetto non esiste 'c:\a.csproj'. Verificare che il riferimento al progetto sia valido e che esista il file di progetto.*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-200">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="8e6eb-201">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-201">**Solution**</span></span> | <span data-ttu-id="8e6eb-202">Modificare il file di progetto per correggere il percorso per il progetto di riferimento o per rimuovere il riferimento all'elemento se non è più necessario.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-202">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="8e6eb-203">NU1105</span><span class="sxs-lookup"><span data-stu-id="8e6eb-203">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-204">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-204">**Issue**</span></span> | <span data-ttu-id="8e6eb-205">Il file di progetto esiste ma è stata fornita alcuna informazione di ripristino per tale.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-205">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="8e6eb-206">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-206">**Example message**</span></span> | <span data-ttu-id="8e6eb-207">*Impossibile leggere le informazioni di progetto per 'c:\a.csproj'. Il file di progetto potrebbe essere destinazioni non valide o mancante necessarie per il ripristino.*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-207">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="8e6eb-208">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-208">**Solution**</span></span> | <span data-ttu-id="8e6eb-209">In Visual Studio, l'errore potrebbe indicare che il progetto viene scaricato, nel qual caso ricaricare il progetto.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-209">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="8e6eb-210">Dalla riga di comando ciò vuol dire che il file è danneggiato o che non contenga personalizzata "dopo l'importazione" necessarie per il ripristino leggere il progetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-210">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="8e6eb-211">Verificare che il file di progetto sia valido e contiene una destinazione "dopo l'importazione".</span><span class="sxs-lookup"><span data-stu-id="8e6eb-211">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="8e6eb-212">NU1106</span><span class="sxs-lookup"><span data-stu-id="8e6eb-212">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-213">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-213">**Issue**</span></span> | <span data-ttu-id="8e6eb-214">Vincoli di dipendenza non possono essere risolti.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-214">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="8e6eb-215">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-215">**Example message**</span></span> | <span data-ttu-id="8e6eb-216">*Non è possibile soddisfare le richieste con conflitto per {id}: {percorso conflitto} Framework: {grafico di destinazione}*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-216">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |
| <span data-ttu-id="8e6eb-217">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-217">**Solution**</span></span> | <span data-ttu-id="8e6eb-218">Modificare il file di progetto per specificare gli intervalli di più flessibile per la dipendenza anziché la versione esatta.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-218">Edit the project file to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="8e6eb-219">NU1107 (in precedenza NU1607)</span><span class="sxs-lookup"><span data-stu-id="8e6eb-219">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-220">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-220">**Issue**</span></span> | <span data-ttu-id="8e6eb-221">Impossibile risolvere i vincoli di dipendenza tra pacchetti.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-221">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="8e6eb-222">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-222">**Example message**</span></span> | <span data-ttu-id="8e6eb-223">*Conflitto di versione per NuGet.Versioning. Fare riferimento il pacchetto direttamente dal progetto per risolvere il problema.<br/>  NuGet. Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-223">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="8e6eb-224">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-224">**Solution**</span></span> | <span data-ttu-id="8e6eb-225">Pacchetti con vincoli di dipendenza in versioni esatte non consentono altri pacchetti per incrementare la versione, se necessario.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-225">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="8e6eb-226">Aggiungere un riferimento al progetto direttamente (nel file di progetto) con la versione esatta richiesta.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-226">Add a reference to the project directly (in the project file) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="8e6eb-227">NU1108 (in precedenza NU1606)</span><span class="sxs-lookup"><span data-stu-id="8e6eb-227">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-228">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-228">**Issue**</span></span> | <span data-ttu-id="8e6eb-229">È stata rilevata una dipendenza circolare.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-229">A circular dependency was detected.</span></span> |
| <span data-ttu-id="8e6eb-230">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-230">**Example message**</span></span> | <span data-ttu-id="8e6eb-231">*Rilevato ciclo: A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-231">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="8e6eb-232">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-232">**Solution**</span></span> | <span data-ttu-id="8e6eb-233">Il pacchetto sia stato creato in modo errato. contattare il proprietario del pacchetto per correggere il bug.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-233">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="8e6eb-234">Errori di compatibilità</span><span class="sxs-lookup"><span data-stu-id="8e6eb-234">Compatibility errors</span></span>

<span data-ttu-id="8e6eb-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="8e6eb-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="8e6eb-236">NU1201</span><span class="sxs-lookup"><span data-stu-id="8e6eb-236">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-237">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-237">**Issue**</span></span> | <span data-ttu-id="8e6eb-238">Una dipendenza di progetto non contiene un framework compatibile con il progetto corrente.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-238">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="8e6eb-239">In genere, il framework di destinazione del progetto è una versione successiva a quella del progetto consumer.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-239">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="8e6eb-240">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-240">**Example message**</span></span> | <span data-ttu-id="8e6eb-241">*Progetto ServerWeb non è compatibile con netstandard1.3 (. Moniker NETStandard, Version = v 1.3). Progetto supporta ServerWeb:<br/> -netstandard1.6 (. Moniker NETStandard, Version = v 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = v 1.0)*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-241">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="8e6eb-242">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-242">**Solution**</span></span> | <span data-ttu-id="8e6eb-243">Modificare il framework di destinazione del progetto a una versione uguale o inferiore a quella del progetto consumer.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-243">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="8e6eb-244">NU1202</span><span class="sxs-lookup"><span data-stu-id="8e6eb-244">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-245">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-245">**Issue**</span></span> | <span data-ttu-id="8e6eb-246">Un pacchetto di dipendenze non contiene tutte le risorse compatibile con il progetto.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-246">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="8e6eb-247">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-247">**Example message**</span></span> | <span data-ttu-id="8e6eb-248">*Pacchetto System.ComponentModel.EventBasedAsync 4.0.11 non è compatibile con netstandard1.3 (. Moniker NETStandard, Version = v 1.3). Creare il pacchetto supporta System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, Version = v 1.0)<br/> -monotouch10 (MonoTouch, Version = v 1.0)<br/> -net45 (. NETFramework, Version = v 4.5)<br/> -netcore50 (. NETCore, Version = v 5.0)<br/> -netstandard1.0 (. Moniker NETStandard, Version = v 1.0)<br/> -portabile net45 win8 wp8 + wpa81 (. NETPortable, versione = v0.0, profilo = Profile259)<br/> -win8 (Windows, Version = v 8.0)<br/> -wp8 (WindowsPhone, Version = v 8.0)<br/> -wpa81 (WindowsPhoneApp, Version = v 8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-248">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="8e6eb-249">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-249">**Solution**</span></span> | <span data-ttu-id="8e6eb-250">Modificare il framework di destinazione del progetto in modo che il pacchetto supporta.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-250">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="8e6eb-251">NU1203</span><span class="sxs-lookup"><span data-stu-id="8e6eb-251">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-252">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-252">**Issue**</span></span> | <span data-ttu-id="8e6eb-253">Il pacchetto non supporta il progetto `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-253">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="8e6eb-254">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-254">**Example message**</span></span> | <span data-ttu-id="8e6eb-255">*System.Example 1.0.0 fornisce un assembly di riferimento in fase di compilazione per DLL in net461, ma non sono presenti assembly di runtime compatibili.*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-255">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="8e6eb-256">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-256">**Solution**</span></span> | <span data-ttu-id="8e6eb-257">Modifica il `RuntimeIdentifier` valori usati nel progetto in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-257">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="8e6eb-258">NU1401</span><span class="sxs-lookup"><span data-stu-id="8e6eb-258">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-259">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-259">**Issue**</span></span> | <span data-ttu-id="8e6eb-260">Il pacchetto richiede caratteristiche o Framework non sono attualmente supportati dalla versione installata di NuGet.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-260">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="8e6eb-261">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-261">**Example message**</span></span> | <span data-ttu-id="8e6eb-262">*Il pacchetto 'NuGet.Versioning' richiede '5.0.0' alla versione client NuGet o versione successiva, ma la versione NuGet corrente è '4.3.0'.*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-262">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="8e6eb-263">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-263">**Solution**</span></span> | <span data-ttu-id="8e6eb-264">Installare una versione più recente di NuGet.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-264">Install a newer version of NuGet.</span></span> <span data-ttu-id="8e6eb-265">Vedere [gli strumenti client di installazione di NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="8e6eb-265">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="8e6eb-266">Avvisi di input non validi</span><span class="sxs-lookup"><span data-stu-id="8e6eb-266">Invalid input warnings</span></span>

<span data-ttu-id="8e6eb-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="8e6eb-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="8e6eb-268">NU1501</span><span class="sxs-lookup"><span data-stu-id="8e6eb-268">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-269">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-269">**Issue**</span></span> | <span data-ttu-id="8e6eb-270">Il ripristino del progetto sta tentando di operare in non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-270">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="8e6eb-271">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-271">**Example message**</span></span> | <span data-ttu-id="8e6eb-272">*La cartella 'c:\projects\a' non contiene un progetto da ripristinare.*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-272">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="8e6eb-273">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-273">**Solution**</span></span> | <span data-ttu-id="8e6eb-274">Esegue nuget restore in una cartella che contiene un progetto.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-274">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="8e6eb-275">NU1502</span><span class="sxs-lookup"><span data-stu-id="8e6eb-275">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-276">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-276">**Issue**</span></span> | <span data-ttu-id="8e6eb-277">`RuntimeSupports` contiene un profilo non valido.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-277">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="8e6eb-278">In genere, il profilo supporta non è stato trovato un `runtime.json` file dai pacchetti dipendenza corrente.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-278">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="8e6eb-279">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-279">**Example message**</span></span> | <span data-ttu-id="8e6eb-280">*Profilo di compatibilità sconosciuto: aaa*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-280">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="8e6eb-281">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-281">**Solution**</span></span> | <span data-ttu-id="8e6eb-282">Controllare il `RuntimeSupports` valore nel progetto.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-282">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="8e6eb-283">NU1503</span><span class="sxs-lookup"><span data-stu-id="8e6eb-283">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-284">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-284">**Issue**</span></span> | <span data-ttu-id="8e6eb-285">Una dipendenza di progetto non importa le destinazioni di ripristino di NuGet.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-285">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="8e6eb-286">È simile a NU1105 ma qui il progetto viene ignorato e ignorato anziché causare tutte esito negativo del ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-286">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="8e6eb-287">Nelle soluzioni complesse sono spesso altri tipi di progetti che non supportano il ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-287">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="8e6eb-288">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-288">**Example message**</span></span> | <span data-ttu-id="8e6eb-289">*Mancato ripristino per il progetto 'c:\a.csproj'. Il file di progetto potrebbe essere destinazioni non valide o mancante necessarie per il ripristino.*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-289">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="8e6eb-290">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-290">**Solution**</span></span> | <span data-ttu-id="8e6eb-291">Questa situazione può verificarsi per i progetti che non si importano props/destinazioni comuni quali l'importazione automatica di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-291">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="8e6eb-292">Se il progetto non è necessaria per il ripristino può essere ignorato.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-292">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="8e6eb-293">In caso contrario, modificare il progetto interessato per aggiungere destinazioni per il ripristino.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-293">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="8e6eb-294">Avvisi di versione di pacchetto imprevisto</span><span class="sxs-lookup"><span data-stu-id="8e6eb-294">Unexpected package version warnings</span></span>

<span data-ttu-id="8e6eb-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="8e6eb-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="8e6eb-296">NU1601</span><span class="sxs-lookup"><span data-stu-id="8e6eb-296">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-297">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-297">**Issue**</span></span> | <span data-ttu-id="8e6eb-298">Una dipendenza diretta del progetto è stato ha respinto per una versione successiva a quella del progetto specificato.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-298">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="8e6eb-299">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-299">**Example message**</span></span> | <span data-ttu-id="8e6eb-300">*Dipendenza specificata è NuGet.Versioning (> = 3.5.0) ma è risultata NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-300">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="8e6eb-301">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-301">**Solution**</span></span> | <span data-ttu-id="8e6eb-302">Aggiornare la dipendenza nel progetto a una versione appropriata.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-302">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="8e6eb-303">NU1602</span><span class="sxs-lookup"><span data-stu-id="8e6eb-303">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-304">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-304">**Issue**</span></span> | <span data-ttu-id="8e6eb-305">Una dipendenza pacchetto manca un limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-305">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="8e6eb-306">Questo non consente il ripristino trovare il *migliore corrispondenza*.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-306">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="8e6eb-307">Ogni ripristino verrà spostata verso il basso il tentativo di trovare una versione precedente che può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-307">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="8e6eb-308">Ciò significa che il ripristino passa nello stato online per controllare tutte le origini di ogni volta che invece di usare i pacchetti già esistenti nella cartella del pacchetto utente.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-308">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="8e6eb-309">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-309">**Example message**</span></span> | <span data-ttu-id="8e6eb-310">*NuGet. Packaging 4.0.0 non prevede un limite inferiore inclusivo dipendenza NuGet.Versioning (3.5.0 >). Una corrispondenza migliore approssimativa di 3.6.0 è stato risolta.*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-310">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="8e6eb-311">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-311">**Solution**</span></span> | <span data-ttu-id="8e6eb-312">In genere si tratta di un pacchetto con errore di creazione.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-312">This is usually a package authoring error.</span></span> <span data-ttu-id="8e6eb-313">Contattare l'autore del pacchetto per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-313">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="8e6eb-314">NU1603</span><span class="sxs-lookup"><span data-stu-id="8e6eb-314">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-315">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-315">**Issue**</span></span> | <span data-ttu-id="8e6eb-316">Una dipendenza pacchetto specificata una versione che non è stata trovata.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-316">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="8e6eb-317">In genere, le origini del pacchetto non contengono la versione prevista limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-317">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="8e6eb-318">È stata utilizzata una versione successiva, che differisce da cosa è stato creato il pacchetto base.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-318">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="8e6eb-319">Ciò significa che il ripristino non è stata trovata la *migliore corrispondenza*.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="8e6eb-320">Ogni ripristino verrà spostata verso il basso il tentativo di trovare una versione precedente che può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="8e6eb-321">Ciò significa che il ripristino passa nello stato online per controllare tutte le origini di ogni volta che invece di usare i pacchetti già esistenti nella cartella del pacchetto utente.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="8e6eb-322">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-322">**Example message**</span></span> | <span data-ttu-id="8e6eb-323">NuGet. Packaging 4.0.0 dipende NuGet.Versioning (> = 4.0.0) 4.0.0 non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-323">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="8e6eb-324">Una corrispondenza migliore approssimativa di 5.0.0 è stato risolta.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-324">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="8e6eb-325">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-325">**Solution**</span></span> | <span data-ttu-id="8e6eb-326">Se il pacchetto previsto non è stato rilasciato quindi potrebbe trattarsi di un pacchetto con errore di creazione.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-326">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="8e6eb-327">Contattare l'autore del pacchetto per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-327">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="8e6eb-328">Se il pacchetto è stato rilasciato, controllare che sia disponibile per le origini del pacchetto in uso.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-328">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="8e6eb-329">Se si utilizza un'origine privata, si potrebbe essere necessario aggiornare il pacchetto su tale feed.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-329">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="8e6eb-330">NU1604</span><span class="sxs-lookup"><span data-stu-id="8e6eb-330">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-331">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-331">**Issue**</span></span> | <span data-ttu-id="8e6eb-332">Dipendenza di progetto non viene definito un limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-332">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="8e6eb-333">Ciò significa che il ripristino non è stata trovata la *migliore corrispondenza*.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-333">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="8e6eb-334">Ogni ripristino verrà spostata verso il basso il tentativo di trovare una versione precedente che può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-334">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="8e6eb-335">Ciò significa che il ripristino passa nello stato online per controllare tutte le origini di ogni volta che invece di usare i pacchetti già esistenti nella cartella del pacchetto utente.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-335">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="8e6eb-336">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-336">**Example message**</span></span> | <span data-ttu-id="8e6eb-337">*Progetto dipendenza NuGet.Versioning (< = 9.0.0) doe non contengono un limite inferiore inclusivo. Includere un limite inferiore nella versione di dipendenza per garantire risultati coerenti di ripristino.*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-337">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="8e6eb-338">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-338">**Solution**</span></span> | <span data-ttu-id="8e6eb-339">Aggiornare il progetto `PackageReference` `Version` attributo da includere un limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-339">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="8e6eb-340">NU1605</span><span class="sxs-lookup"><span data-stu-id="8e6eb-340">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-341">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-341">**Issue**</span></span> | <span data-ttu-id="8e6eb-342">Un pacchetto di dipendenza è specificato un vincolo di versione in una versione superiore di un pacchetto rispetto al ripristino risolta.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-342">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="8e6eb-343">Ovvero "più vicino wins" regola per la risoluzione dei pacchetti, a causa di un pacchetto più vicini nel grafico può avere sottoposto a override un pacchetto distante.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-343">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="8e6eb-344">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-344">**Example message**</span></span> | <span data-ttu-id="8e6eb-345">*Rilevato downgrade del pacchetto: NuGet.Versioning da 4.0.0 a 3.5.0. Fare riferimento il pacchetto direttamente dal progetto per selezionare una versione diversa.<br/>  NuGet. Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-345">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="8e6eb-346">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-346">**Solution**</span></span> | <span data-ttu-id="8e6eb-347">Aggiungere un riferimento diretto al progetto per la successiva versione del pacchetto che si desidera utilizzare.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-347">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="8e6eb-348">Avvisi di sistema di risoluzione dei conflitti</span><span class="sxs-lookup"><span data-stu-id="8e6eb-348">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="8e6eb-349">NU1608</span><span class="sxs-lookup"><span data-stu-id="8e6eb-349">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-350">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-350">**Issue**</span></span> | <span data-ttu-id="8e6eb-351">Un pacchetto risolto è supera a quello di un vincolo di dipendenza.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-351">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="8e6eb-352">Ciò significa che un pacchetto a cui fa riferimento direttamente un progetto ignora i vincoli di dipendenze da altri pacchetti.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-352">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="8e6eb-353">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-353">**Example message**</span></span> | <span data-ttu-id="8e6eb-354">*Versione del pacchetto rilevato all'esterno di vincolo dipendenza: x 1.0.0 richiede y (= 1.0.0) ma versione 2.0.0 y è stato risolto.*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-354">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="8e6eb-355">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-355">**Solution**</span></span> | <span data-ttu-id="8e6eb-356">In alcuni casi ciò è intenzionale e l'avviso può essere eliminato.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-356">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="8e6eb-357">In caso contrario, modificare il riferimento del progetto al pacchetto per ampliare i vincoli di versione.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-357">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="8e6eb-358">Avvisi di fallback di pacchetto</span><span class="sxs-lookup"><span data-stu-id="8e6eb-358">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="8e6eb-359">NU1701</span><span class="sxs-lookup"><span data-stu-id="8e6eb-359">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-360">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-360">**Issue**</span></span> | <span data-ttu-id="8e6eb-361">`PackageTargetFallback` / `AssetTargetFallback` è stato usato per selezionare asset da un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-361">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="8e6eb-362">Avviso di informerà gli utenti che le risorse potrebbero non essere compatibile al 100%.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-362">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="8e6eb-363">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-363">**Example message**</span></span> | <span data-ttu-id="8e6eb-364">*Pacchetto 'NuGet.Versioning' è stato ripristinato mediante 'portable net45 + win8' invece del framework di destinazione del progetto 'netstandard1.5'. Questo pacchetto potrebbe non essere completamente compatibile con il progetto.*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-364">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="8e6eb-365">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-365">**Solution**</span></span> | <span data-ttu-id="8e6eb-366">Modificare il framework di destinazione del progetto in modo che il pacchetto supporta.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-366">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="8e6eb-367">Feed di avvisi</span><span class="sxs-lookup"><span data-stu-id="8e6eb-367">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="8e6eb-368">NU1801</span><span class="sxs-lookup"><span data-stu-id="8e6eb-368">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-369">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-369">**Issue**</span></span> | <span data-ttu-id="8e6eb-370">Si è verificato un errore durante la lettura dei feed quando `IgnoreFailedSources` è impostata su true, convertendolo in un messaggio di avviso non irreversibile.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-370">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="8e6eb-371">Ciò può contenere qualsiasi messaggio ed è generico.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-371">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="8e6eb-372">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-372">**Example message**</span></span> | <span data-ttu-id="8e6eb-373">N/D</span><span class="sxs-lookup"><span data-stu-id="8e6eb-373">n/a</span></span> |
| <span data-ttu-id="8e6eb-374">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-374">**Solution**</span></span> | <span data-ttu-id="8e6eb-375">Modificare la configurazione per specificare le origini valide.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-375">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="8e6eb-376">Avvisi ed errori interni di NuGet</span><span class="sxs-lookup"><span data-stu-id="8e6eb-376">NuGet internal errors and warnings</span></span>

<span data-ttu-id="8e6eb-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="8e6eb-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="8e6eb-378">NU1000</span><span class="sxs-lookup"><span data-stu-id="8e6eb-378">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-379">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-379">**Issue**</span></span> | <span data-ttu-id="8e6eb-380">Un errore interno non specifico da NuGet.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-380">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="8e6eb-381">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-381">**Solution**</span></span> | <span data-ttu-id="8e6eb-382">Controllare i registri per ulteriori informazioni</span><span class="sxs-lookup"><span data-stu-id="8e6eb-382">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="8e6eb-383">NU1500</span><span class="sxs-lookup"><span data-stu-id="8e6eb-383">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-384">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-384">**Issue**</span></span> | <span data-ttu-id="8e6eb-385">Un avviso interno non specifico da NuGet.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-385">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="8e6eb-386">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-386">**Solution**</span></span> | <span data-ttu-id="8e6eb-387">Controllare i registri per ulteriori informazioni</span><span class="sxs-lookup"><span data-stu-id="8e6eb-387">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="8e6eb-388">Pacchetti firmati (creazione e la verifica)</span><span class="sxs-lookup"><span data-stu-id="8e6eb-388">Signed packages (creation and verification)</span></span>

<span data-ttu-id="8e6eb-389">*4.6.0+ NuGet*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-389">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="8e6eb-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="8e6eb-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="8e6eb-391">NU3000</span><span class="sxs-lookup"><span data-stu-id="8e6eb-391">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-392">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-392">**Issue**</span></span> | <span data-ttu-id="8e6eb-393">Un errore non specifico relativo alla firma del pacchetto e firmati verifica del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-393">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="8e6eb-394">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-394">**Solution**</span></span> | <span data-ttu-id="8e6eb-395">Controllare i registri per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-395">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="8e6eb-396">NU3001</span><span class="sxs-lookup"><span data-stu-id="8e6eb-396">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-397">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-397">**Issue**</span></span> | <span data-ttu-id="8e6eb-398">Argomenti non validi a uno di [firmare comando](../tools/cli-ref-sign.md) o [verificare comando](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="8e6eb-398">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="8e6eb-399">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-399">**Solution**</span></span> | <span data-ttu-id="8e6eb-400">Controllare e correggere gli argomenti forniti.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-400">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="8e6eb-401">NU3002</span><span class="sxs-lookup"><span data-stu-id="8e6eb-401">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-402">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-402">**Issue**</span></span> | <span data-ttu-id="8e6eb-403">Il `-Timestamper` non è stata specificata con il [comando sign nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="8e6eb-403">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="8e6eb-404">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-404">**Example message**</span></span> | <span data-ttu-id="8e6eb-405">*Il '-Timestamper' opzione non è stato specificato. Il pacchetto firmato non saranno impostati i timestamp.*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-405">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="8e6eb-406">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-406">**Solution**</span></span> | <span data-ttu-id="8e6eb-407">Specificare il `-Timestamper` con `nuget sign`.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-407">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="8e6eb-408">NU3004</span><span class="sxs-lookup"><span data-stu-id="8e6eb-408">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-409">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-409">**Issue**</span></span> | <span data-ttu-id="8e6eb-410">È stato fornito un pacchetto non firmato per il [nuget verificare comando](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="8e6eb-410">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="8e6eb-411">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-411">**Solution**</span></span> | <span data-ttu-id="8e6eb-412">Eseguire `nuget verify` con un pacchetto firmato.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-412">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="8e6eb-413">Vedere [firmare un pacchetto](../create-packages/Sign-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="8e6eb-413">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="8e6eb-414">NU3008</span><span class="sxs-lookup"><span data-stu-id="8e6eb-414">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-415">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-415">**Issue**</span></span> | <span data-ttu-id="8e6eb-416">Il pacchetto non riuscito, vale a dire che un pacchetto firmato sia stato manomesso dopo l'accesso.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-416">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="8e6eb-417">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-417">**Solution**</span></span> | <span data-ttu-id="8e6eb-418">Scansione del computer con un software antivirus.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-418">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="8e6eb-419">Quindi rimuovere il pacchetto dal computer, reinstallarlo e riprovare.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-419">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="8e6eb-420">Se il problema persiste, contattare il proprietario dell'origine del pacchetto e il proprietario del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-420">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="8e6eb-421">NU3018</span><span class="sxs-lookup"><span data-stu-id="8e6eb-421">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-422">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-422">**Issue**</span></span> | <span data-ttu-id="8e6eb-423">Non è riuscita la creazione della catena di certificati per la firma primaria.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-423">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="8e6eb-424">Il certificato di firma primario non è attendibile, revocato, o informazioni di revoca per il certificato non sono disponibile.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-424">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="8e6eb-425">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-425">**Example message**</span></span> | <span data-ttu-id="8e6eb-426">*Avviso: NU3018: la funzione di revoca non è riuscita a controllare la revoca del certificato.*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-426">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="8e6eb-427">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-427">**Solution**</span></span> | <span data-ttu-id="8e6eb-428">Usare un certificato attendibile e valido.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-428">Use a trusted and valid certificate.</span></span> <span data-ttu-id="8e6eb-429">Verificare la connettività internet.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-429">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="8e6eb-430">NU3028</span><span class="sxs-lookup"><span data-stu-id="8e6eb-430">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="8e6eb-431">**Problema**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-431">**Issue**</span></span> | <span data-ttu-id="8e6eb-432">Non è riuscita la creazione della catena di certificati per la firma del timestamp.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-432">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="8e6eb-433">Il certificato di firma del timestamp non è attendibile, revocato, o informazioni di revoca per il certificato non sono disponibile.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-433">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="8e6eb-434">**Messaggio di esempio**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-434">**Example message**</span></span> | <span data-ttu-id="8e6eb-435">*Avviso: NU3028: la funzione di revoca non è riuscita a controllare la revoca del certificato.*</span><span class="sxs-lookup"><span data-stu-id="8e6eb-435">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="8e6eb-436">**Soluzione**</span><span class="sxs-lookup"><span data-stu-id="8e6eb-436">**Solution**</span></span> | <span data-ttu-id="8e6eb-437">Usare un certificato attendibile e valido.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-437">Use a trusted and valid certificate.</span></span> <span data-ttu-id="8e6eb-438">Verificare la connettività internet.</span><span class="sxs-lookup"><span data-stu-id="8e6eb-438">Check internet connectivity.</span></span> |
