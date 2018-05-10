---
title: File project.json di NuGet con progetti UWP
description: Descrizione di come il file project.json viene usato per tenere traccia delle dipendenze di NuGet nei progetti UWP (Universal Windows Platform).
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: 826aed65a69c553bedf661cb5a4f940735dfba2c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="0b3b6-103">project.json e UWP</span><span class="sxs-lookup"><span data-stu-id="0b3b6-103">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="0b3b6-104">Questo contenuto è deprecato.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-104">This content is deprecated.</span></span> <span data-ttu-id="0b3b6-105">I progetti devono usare i formati `packages.config` o PackageReference.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="0b3b6-106">Questo documento descrive la struttura del pacchetto che usa le funzionalità di NuGet 3+ (Visual Studio 2015 e versioni successive).</span><span class="sxs-lookup"><span data-stu-id="0b3b6-106">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="0b3b6-107">È possibile impostare la proprietà `minClientVersion` di `.nuspec` su 3.1 per dichiarare che sono necessarie le funzionalità descritte qui.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-107">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="0b3b6-108">Aggiunta del supporto UWP a un pacchetto esistente</span><span class="sxs-lookup"><span data-stu-id="0b3b6-108">Adding UWP support to an existing package</span></span>

<span data-ttu-id="0b3b6-109">Se è presente un pacchetto e si vuole aggiungere il supporto per le applicazioni UWP, non è necessario adottare il formato dei pacchetti descritto qui.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-109">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="0b3b6-110">Si deve adottare questo formato solo se sono necessarie le funzionalità descritte e si prevede di usare solo client che hanno eseguito l'aggiornamento alla versione 3+ del client NuGet.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-110">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="0b3b6-111">Si specifica già come destinazione netcore45</span><span class="sxs-lookup"><span data-stu-id="0b3b6-111">I already target netcore45</span></span>

<span data-ttu-id="0b3b6-112">Se si specifica già `netcore45` come destinazione e non si ha bisogno di sfruttare queste funzionalità, non è necessaria alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-112">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="0b3b6-113">I pacchetti `netcore45` possono essere utilizzati dalle applicazioni UWP.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-113">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="0b3b6-114">Si vogliono sfruttare le API specifiche di Windows 10</span><span class="sxs-lookup"><span data-stu-id="0b3b6-114">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="0b3b6-115">In questo caso è necessario aggiungere il moniker del framework di destinazione `uap10.0` (TFM, Target Framework Moniker, o TxM) al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-115">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="0b3b6-116">Creare una nuova cartella nel pacchetto e aggiungere a tale cartella l'assembly compilato per usare Windows 10.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-116">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="0b3b6-117">Non sono necessarie le API specifiche di Windows 10, ma si vogliono usare le nuove funzionalità .NET o non si ha già netcore45</span><span class="sxs-lookup"><span data-stu-id="0b3b6-117">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="0b3b6-118">In questo caso si aggiungerà il moniker TxM `dotnet` al pacchetto.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-118">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="0b3b6-119">Diversamente da altri TxM, `dotnet` non implica una superficie di attacco o una piattaforma.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-119">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="0b3b6-120">Il pacchetto funziona su tutte le piattaforme su cui funzionano le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-120">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="0b3b6-121">Quando si compila un pacchetto con il TxM `dotnet`, è probabile che si abbiano molte più dipendenze specifiche del TxM in `.nuspec`, perché è necessario definire i pacchetti BCL da cui si dipende, ad esempio `System.Text`, `System.Xml` e così via. Il pacchetto opera nelle posizioni in cui operano tali dipendenze.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-121">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="0b3b6-122">Come trovare le dipendenze</span><span class="sxs-lookup"><span data-stu-id="0b3b6-122">How do I find out my dependencies</span></span>

<span data-ttu-id="0b3b6-123">Esistono due modi per determinare le dipendenze da elencare:</span><span class="sxs-lookup"><span data-stu-id="0b3b6-123">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="0b3b6-124">Usare lo strumento **di terze parti** [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator).</span><span class="sxs-lookup"><span data-stu-id="0b3b6-124">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="0b3b6-125">Lo strumento automatizza il processo e aggiorna il file `.nuspec` con i pacchetti dipendenti in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-125">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="0b3b6-126">È disponibile tramite il pacchetto NuGet [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span><span class="sxs-lookup"><span data-stu-id="0b3b6-126">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="0b3b6-127">(Difficile) Usare `ILDasm` per esaminare il file `.dll` e verificare quali assembly sono effettivamente necessari in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-127">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="0b3b6-128">Determinare quindi il pacchetto NuGet da cui proviene ognuno.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-128">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="0b3b6-129">Per informazioni dettagliate sulla creazione di un pacchetto che supporta il TxM `dotnet`, vedere l'argomento [`project.json`](project-json.md).</span><span class="sxs-lookup"><span data-stu-id="0b3b6-129">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="0b3b6-130">Se il pacchetto deve usare progetti PCL, è consigliabile creare una cartella `dotnet` per evitare avvisi e potenziali problemi di compatibilità.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-130">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="0b3b6-131">Struttura di directory</span><span class="sxs-lookup"><span data-stu-id="0b3b6-131">Directory structure</span></span>

<span data-ttu-id="0b3b6-132">I pacchetti NuGet che usano questo formato presentano la cartella e i comportamenti noti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0b3b6-132">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="0b3b6-133">Cartella</span><span class="sxs-lookup"><span data-stu-id="0b3b6-133">Folder</span></span> | <span data-ttu-id="0b3b6-134">comportamenti</span><span class="sxs-lookup"><span data-stu-id="0b3b6-134">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="0b3b6-135">Compilazione</span><span class="sxs-lookup"><span data-stu-id="0b3b6-135">Build</span></span> | <span data-ttu-id="0b3b6-136">Contiene i file di destinazioni e proprietà MSBuild che vengono integrati in modo diverso nel progetto, senza altre modifiche.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-136">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="0b3b6-137">Strumenti</span><span class="sxs-lookup"><span data-stu-id="0b3b6-137">Tools</span></span> | <span data-ttu-id="0b3b6-138">`install.ps1` e `uninstall.ps1` non vengono eseguiti.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-138">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="0b3b6-139">`init.ps1` funziona come sempre.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-139">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="0b3b6-140">Content</span><span class="sxs-lookup"><span data-stu-id="0b3b6-140">Content</span></span> | <span data-ttu-id="0b3b6-141">Il contenuto non viene copiato automaticamente nel progetto di un utente.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-141">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="0b3b6-142">Il supporto per l'inclusione di contenuto nel progetto è previsto per una versione successiva.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-142">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="0b3b6-143">Lib</span><span class="sxs-lookup"><span data-stu-id="0b3b6-143">Lib</span></span> | <span data-ttu-id="0b3b6-144">Per molti pacchetti `lib` funziona come in NuGet 2.x, ma con opzioni espanse per i nomi che possono essere usati e una logica migliore per la selezione della sottocartella corretta quando si utilizzano i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-144">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="0b3b6-145">Se usata in combinazione con `ref`, la cartella `lib` contiene tuttavia assembly che implementano la superficie di attacco definita dagli assembly nella cartella `ref`.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-145">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="0b3b6-146">Rif</span><span class="sxs-lookup"><span data-stu-id="0b3b6-146">Ref</span></span> | <span data-ttu-id="0b3b6-147">`ref` è una cartella facoltativa che contiene assembly .NET che definiscono la superficie pubblica (tipi e metodi pubblici) per un'applicazione in cui eseguire la compilazione.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-147">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="0b3b6-148">Gli assembly in questa cartella possono non avere implementazioni. Vengono usati esclusivamente per definire la superficie di attacco per il compilatore.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-148">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="0b3b6-149">Se il pacchetto non ha cartelle `ref`, `lib` è sia l'assembly di riferimento che l'assembly di implementazione.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-149">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="0b3b6-150">Runtimes</span><span class="sxs-lookup"><span data-stu-id="0b3b6-150">Runtimes</span></span> | <span data-ttu-id="0b3b6-151">`runtimes` è una cartella facoltativa contenente il codice specifico del sistema operativo, ad esempio l'architettura della CPU e i file binari specifici del sistema operativo o in altro modo dipendenti dalla piattaforma.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-151">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="0b3b6-152">File di destinazioni e proprietà MSBuild nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="0b3b6-152">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="0b3b6-153">I pacchetti NuGet possono contenere file `.targets` e `.props` che vengono importati nei progetti di MSBuild in cui il pacchetto viene installato.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-153">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="0b3b6-154">In NuGet 2.x a questo scopo venivano inserite istruzioni `<Import>` nel file `.csproj`. In NuGet 3.0 non è disponibile una specifica azione di "installazione nel progetto".</span><span class="sxs-lookup"><span data-stu-id="0b3b6-154">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="0b3b6-155">Il processo di ripristino del pacchetto scrive invece due file, `[projectname].nuget.props` e `[projectname].NuGet.targets`.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-155">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="0b3b6-156">MSBuild cerca questi due file e li importa automaticamente verso l'inizio e verso la fine del processo di compilazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-156">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="0b3b6-157">Il comportamento è molto simile a quello di NuGet 2.x, ma con un'importante differenza: *in questo caso non esiste un ordine garantito dei file di destinazioni/proprietà*.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-157">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="0b3b6-158">MSBuild consente tuttavia di ordinare le destinazioni tramite gli attributi `BeforeTargets` e `AfterTargets` della definizione `<Target>`. Vedere [Elemento Target (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="0b3b6-158">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="0b3b6-159">Lib e Ref</span><span class="sxs-lookup"><span data-stu-id="0b3b6-159">Lib and Ref</span></span>

<span data-ttu-id="0b3b6-160">Il comportamento della cartella `lib` non è cambiato di molto in NuGet v3.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-160">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="0b3b6-161">Tutti gli assembly devono tuttavia essere in sottocartelle denominate in base a un TxM e non possono più essere inseriti direttamente sotto la cartella `lib`.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-161">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="0b3b6-162">Un TxM è il nome di una piattaforma per cui si suppone che funzioni un determinato asset in un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-162">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="0b3b6-163">Si tratta ovviamente di un'estensione del moniker del framework di destinazione (TFM, Target Framework Moniker). `net45`, `net46`, `netcore50` e `dnxcore50` sono tutti esempi di TxM. Vedere [Framework di destinazione](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="0b3b6-163">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../reference/target-frameworks.md).</span></span> <span data-ttu-id="0b3b6-164">TxM può indicare un framework (TFM), oltre ad altre superfici di attacco specifiche della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-164">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="0b3b6-165">Il TxM UWP (`uap10.0`), ad esempio, rappresenta la superficie di attacco .NET, oltre alla superficie di attacco Windows per le applicazioni UWP.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-165">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="0b3b6-166">Struttura lib di esempio:</span><span class="sxs-lookup"><span data-stu-id="0b3b6-166">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="0b3b6-167">La cartella `lib` contiene assembly usati in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-167">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="0b3b6-168">Per la maggior parte dei pacchetti, è sufficiente una cartella sotto `lib` per ogni TxM di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-168">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="0b3b6-169">Rif</span><span class="sxs-lookup"><span data-stu-id="0b3b6-169">Ref</span></span>

<span data-ttu-id="0b3b6-170">A volte è necessario usare un assembly diverso durante la compilazione, in questo caso un assembly di riferimento .NET.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-170">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="0b3b6-171">In questi casi, usare una cartella di primo livello denominata `ref` (abbreviazione per "assembly di riferimento").</span><span class="sxs-lookup"><span data-stu-id="0b3b6-171">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="0b3b6-172">La maggior parte degli autori di pacchetti non richiede la cartella `ref`.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-172">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="0b3b6-173">È utile per i pacchetti che devono fornire una superficie di attacco coerente per la compilazione e IntelliSense, ma hanno implementazioni diverse a seconda del TxM.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-173">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="0b3b6-174">Il caso d'uso principale sono i pacchetti `System.*` che vengono generati nell'ambito dell'invio di .NET Core in NuGet.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-174">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="0b3b6-175">Questi pacchetti hanno svariate implementazioni che vengono unificate da un set coerente di assembly di riferimento.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-175">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="0b3b6-176">Gli assembly inclusi nella cartella `ref` sono ovviamente gli assembly di riferimento che vengono passati al compilatore.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-176">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="0b3b6-177">Per chi ha usato csc.exe si tratta degli assembly passati all'[opzione /reference di C#](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option).</span><span class="sxs-lookup"><span data-stu-id="0b3b6-177">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="0b3b6-178">La struttura della cartella `ref` è la stessa di `lib`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0b3b6-178">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll

<span data-ttu-id="0b3b6-179">In questo esempio gli assembly nelle directory `ref` saranno tutti identici.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-179">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="0b3b6-180">Runtimes</span><span class="sxs-lookup"><span data-stu-id="0b3b6-180">Runtimes</span></span>

<span data-ttu-id="0b3b6-181">La cartella runtimes contiene assembly e librerie native necessari per l'esecuzione in specifici "runtime", definiti in genere dal sistema operativo e dall'architettura della CPU.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-181">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="0b3b6-182">Questi runtime vengono identificati usando gli [identificatori di runtime](/dotnet/core/rid-catalog), ad esempio `win`, `win-x86`, `win7-x86`, `win8-64` e così via.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-182">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-helpers-to-use-platform-specific-apis"></a><span data-ttu-id="0b3b6-183">Helper nativi per usare API specifiche della piattaforma</span><span class="sxs-lookup"><span data-stu-id="0b3b6-183">Native helpers to use platform-specific APIs</span></span>

<span data-ttu-id="0b3b6-184">L'esempio seguente illustra un pacchetto che ha solo un'implementazione gestita per più piattaforme, ma usa helper nativi in Windows 8 dove può chiamare le API native specifiche di Windows 8.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-184">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

<span data-ttu-id="0b3b6-185">Con il pacchetto precedente si verifica quanto segue:</span><span class="sxs-lookup"><span data-stu-id="0b3b6-185">Given the above package the following things happen:</span></span>

- <span data-ttu-id="0b3b6-186">Se non in Windows 8, viene usato l'assembly `lib/net40/MyLibrary.dll`.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-186">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="0b3b6-187">Se in Windows 8, viene usato `runtimes/win8-<architecture>/lib/MyLibrary.dll` e `native/MyNativeHelper.dll` viene copiato nell'output della compilazione.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-187">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="0b3b6-188">Nell'esempio precedente l'assembly `lib/net40` è solo codice gestito, mentre gli assembly nella cartella runtimes useranno p/invoke nell'assembly degli helper nativi per chiamare le API specifiche di Windows 8.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-188">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="0b3b6-189">Poiché viene sempre selezionata una sola cartella `lib`, se è presente una cartella specifica del runtime, questa viene preferita a una cartella `lib` non specifica del runtime.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-189">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="0b3b6-190">La cartella nativa è additiva. Se esiste, viene copiata nell'output della compilazione.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-190">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="0b3b6-191">Wrapper gestito</span><span class="sxs-lookup"><span data-stu-id="0b3b6-191">Managed wrapper</span></span>

<span data-ttu-id="0b3b6-192">Un altro modo per usare i runtime consiste nell'inviare un pacchetto che è solo un wrapper gestito tramite un assembly nativo.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-192">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="0b3b6-193">In questo scenario si crea un pacchetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="0b3b6-193">In this scenario you create a package like the following:</span></span>

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

<span data-ttu-id="0b3b6-194">In questo caso non sono presenti cartelle `lib` di primo livello uguali a tale cartella perché non esistono implementazioni di questo pacchetto che non si basano sull'assembly nativo corrispondente.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-194">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="0b3b6-195">Se l'assembly gestito, `MyLibrary.dll`, fosse esattamente lo stesso in entrambi i casi, sarebbe possibile inserirlo in una cartella `lib` di primo livello, ma, poiché l'assenza di un assembly nativo non impedisce la corretta installazione del pacchetto se venisse installato in una piattaforma diversa da win-x86 o win-x64, la cartella lib di primo livello verrebbe usata, ma nessun assembly nativo verrebbe copiato.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-195">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="0b3b6-196">Creazione di pacchetti per NuGet 2 e NuGet 3</span><span class="sxs-lookup"><span data-stu-id="0b3b6-196">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="0b3b6-197">Se si vuole creare un pacchetto che possa essere utilizzato dai progetti che usano `packages.config`, oltre a pacchetti che usano `project.json`, si applica quanto descritto di seguito:</span><span class="sxs-lookup"><span data-stu-id="0b3b6-197">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="0b3b6-198">Ref e runtimes funzionano solo in NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-198">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="0b3b6-199">Vengono entrambi ignorati da NuGet 2.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-199">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="0b3b6-200">Non è possibile basarsi su `install.ps1` o su `uninstall.ps1` per il funzionamento.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-200">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="0b3b6-201">Questi file vengono eseguiti quando si usa `packages.config`, ma vengono ignorati con `project.json`.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-201">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="0b3b6-202">È quindi necessario che i pacchetti siano utilizzabili senza eseguirli.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-202">So your package needs to be usable without them running.</span></span> <span data-ttu-id="0b3b6-203">`init.ps1` viene ancora eseguito in NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-203">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="0b3b6-204">Poiché l'installazione di file di destinazioni e proprietà è diversa, verificare che il pacchetto funzioni come previsto in entrambi i client.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-204">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="0b3b6-205">Le sottodirectory di lib devono essere un TxM in NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-205">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="0b3b6-206">Non è possibile inserire librerie nella radice della cartella `lib`.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-206">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="0b3b6-207">Il contenuto non viene copiato automaticamente con NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-207">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="0b3b6-208">Gli utenti del pacchetto possono copiare manualmente i file o usare uno strumento, ad esempio uno strumento di esecuzione attività, per automatizzare la copia dei file.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-208">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="0b3b6-209">Le trasformazioni dei file di configurazione e di origine non vengono eseguite da NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-209">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="0b3b6-210">Se si supportano NuGet 2 e 3, `minClientVersion` dovrà essere la versione più bassa del client NuGet 2 in cui il pacchetto funziona.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-210">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="0b3b6-211">Nel caso di un pacchetto esistente, non deve essere modificata.</span><span class="sxs-lookup"><span data-stu-id="0b3b6-211">In the case of an existing package it shouldn't need to change.</span></span>
