---
title: Ripristino dei pacchetti NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Descrizione della modalità di ripristino dei pacchetti NuGet da cui dipende un progetto, inclusa la procedura per disabilitare il ripristino e vincolare le versioni."
keywords: Ripristino di pacchetti NuGet, installazione di pacchetti NuGet, installazione pacchetto, ripristinare pacchetti, versioni con dipendenze, disabilitazione del ripristino automatico, vincolo delle versioni dei pacchetti
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2567f45b6bb36cdd94c4ce6f1418cb1c7ceac5e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="package-restore"></a><span data-ttu-id="2f085-104">Ripristino di pacchetti</span><span class="sxs-lookup"><span data-stu-id="2f085-104">Package Restore</span></span>

<span data-ttu-id="2f085-105">Per ottenere un ambiente di sviluppo ordinato e ridurre le dimensioni dei repository, l'opzione **Ripristino pacchetto** NuGet installa tutti i pacchetti a cui fa riferimento un progetto prima di compilarlo.</span><span class="sxs-lookup"><span data-stu-id="2f085-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="2f085-106">Questa funzionalità ampiamente usata garantisce che tutte le dipendenze siano disponibili in un progetto senza la necessità di archiviare tali pacchetti in un sistema di controllo del codice sorgente. Vedere [Pacchetti e controllo del codice sorgente](../consume-packages/packages-and-source-control.md) per informazioni su come configurare il repository per escludere i file binari dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="2f085-106">This widely-used feature ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span>

<span data-ttu-id="2f085-107">Contenuto dell'argomento:</span><span class="sxs-lookup"><span data-stu-id="2f085-107">In this topic:</span></span>
- [<span data-ttu-id="2f085-108">Guida rapida al ripristino dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="2f085-108">Quick guide to package restore</span></span>](#quick-guide-to-package-restore)
- [<span data-ttu-id="2f085-109">Panoramica del ripristino dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="2f085-109">Package restore overview</span></span>](#package-restore-overview)
- [<span data-ttu-id="2f085-110">Abilitazione e disabilitazione del ripristino dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="2f085-110">Enabling and disabling package restore</span></span>](#enabling-and-disabling-package-restore)
- [<span data-ttu-id="2f085-111">Vincolo delle versioni dei pacchetti con il ripristino</span><span class="sxs-lookup"><span data-stu-id="2f085-111">Constraining package versions with restore</span></span>](#constraining-package-versions-with-restore)
- <span data-ttu-id="2f085-112">[Ripristino dalla riga di comando](#command-line-restore), per tutte le versioni di NuGet</span><span class="sxs-lookup"><span data-stu-id="2f085-112">[Command-line restore](#command-line-restore), for all versions of NuGet</span></span>
- <span data-ttu-id="2f085-113">[Ripristino automatico in Visual Studio](#automatic-restore-in-visual-studio), per NuGet 2.7 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="2f085-113">[Automatic restore in Visual Studio](#automatic-restore-in-visual-studio), for NuGet 2.7 and later.</span></span>
- <span data-ttu-id="2f085-114">[Ripristino integrato con MSBuild in Visual Studio](#msbuild-integrated-restore), per NuGet 2.6 e versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="2f085-114">[MSBuild-integrated restore in Visual Studio](#msbuild-integrated-restore), for NuGet 2.6 and earlier.</span></span>
- [<span data-ttu-id="2f085-115">Ripristino dei pacchetti con Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="2f085-115">Package restore with Team Foundation Build</span></span>](#package-restore-with-team-foundation-build)

<span data-ttu-id="2f085-116">Il comportamento di ripristino varia in base alla versione. Per controllare la versione di NuGet, è sufficiente eseguire `nuget.exe` dalla riga di comando e guardare la prima riga dell'output.</span><span class="sxs-lookup"><span data-stu-id="2f085-116">Restore behavior does vary by version; to check your NuGet version, simply run `nuget.exe` on the command line and look at the first line of output.</span></span>

<span data-ttu-id="2f085-117">Per ulteriori dettagli sul ripristino dei pacchetti nei server di compilazione, vedere [Package restore with TFBuild](../consume-packages/team-foundation-build.md) (Ripristino di pacchetti con TFBuild).</span><span class="sxs-lookup"><span data-stu-id="2f085-117">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

> [!Note]
> <span data-ttu-id="2f085-118">I progetti configurati per il ripristino dei pacchetti funzionano anche con xbuild su Mono.</span><span class="sxs-lookup"><span data-stu-id="2f085-118">Projects configured for package restore also work with xbuild on Mono.</span></span>

## <a name="quick-guide-to-package-restore"></a><span data-ttu-id="2f085-119">Guida rapida al ripristino dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="2f085-119">Quick guide to package restore</span></span>

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> <span data-ttu-id="2f085-120">Se viene visualizzato l'errore "Questo progetto fa riferimento a uno o più pacchetti NuGet che non sono presenti in questo computer" o "Impossibile ripristinare uno o più pacchetti NuGet perché il consenso non è stato concesso", attivare il ripristino automatico seguendo le istruzioni in [Abilitazione e disabilitazione del ripristino dei pacchetti](#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="2f085-120">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="2f085-121">Panoramica del ripristino dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="2f085-121">Package restore overview</span></span>

<span data-ttu-id="2f085-122">In primo luogo, i riferimenti ai pacchetti vengono gestiti in uno dei seguenti formati di gestione dei pacchetti, in base al tipo di progetto e alla versione di NuGet.</span><span class="sxs-lookup"><span data-stu-id="2f085-122">First, package references are maintained in one of the following package management formats, depending on project type and NuGet version.</span></span> <span data-ttu-id="2f085-123">Si noti che NuGet 4 e MSBuild 15.1 vengono installati con Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2f085-123">(Note that NuGet 4 and MSBuild 15.1 are installed with Visual Studio 2017.)</span></span>

| <span data-ttu-id="2f085-124">Metodo</span><span class="sxs-lookup"><span data-stu-id="2f085-124">Method</span></span> | <span data-ttu-id="2f085-125">Versione di NuGet</span><span class="sxs-lookup"><span data-stu-id="2f085-125">NuGet Version</span></span> | <span data-ttu-id="2f085-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f085-126">Description</span></span> | 
| --- | --- | --- |
| `packages.config` | <span data-ttu-id="2f085-127">2.x+</span><span class="sxs-lookup"><span data-stu-id="2f085-127">2.x+</span></span> | <span data-ttu-id="2f085-128">Elenca il set completo di dipendenze.</span><span class="sxs-lookup"><span data-stu-id="2f085-128">Lists the complete deep set of dependencies.</span></span> <span data-ttu-id="2f085-129">I pacchetti aggiunti a `packages.config` devono essere aggiunti anche al file di progetto e anche le destinazioni e le proprietà devono essere aggiunte al file di progetto.</span><span class="sxs-lookup"><span data-stu-id="2f085-129">Packages added to `packages.config` must also be added to the project file, and Targets and Props must also be added to the project file.</span></span> <span data-ttu-id="2f085-130">Questo è il metodo di base per tutte le versioni di NuGet, ma con prestazioni inferiori rispetto alle altre opzioni.</span><span class="sxs-lookup"><span data-stu-id="2f085-130">This is the baseline method for all versions of NuGet, but has slower performance compared with the other options.</span></span> <span data-ttu-id="2f085-131">(Vedere lo [schema di packages.config](../schema/packages-config.md).)</span><span class="sxs-lookup"><span data-stu-id="2f085-131">(See [packages.config schema](../schema/packages-config.md).)</span></span> | 
| `project.json` | <span data-ttu-id="2f085-132">3.x+</span><span class="sxs-lookup"><span data-stu-id="2f085-132">3.x+</span></span> | <span data-ttu-id="2f085-133">Usato solo per impostazione predefinita con progetti UWP, ma i progetti possono essere convertiti da `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="2f085-133">Used only by default with UWP projects, but projects can be converted from `packages.config`.</span></span> <span data-ttu-id="2f085-134">`project.json` elenca solo le dipendenze di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="2f085-134">`project.json` lists only top-level dependencies.</span></span> <span data-ttu-id="2f085-135">I riferimenti, le destinazioni e le proprietà vengono aggiunti dinamicamente al progetto durante la compilazione, con prestazioni di conseguenza migliori rispetto a `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="2f085-135">References, Targets, and Props are added dynamically to the project during build, resulting in better performance compared with `packages.config`.</span></span> <span data-ttu-id="2f085-136">(Vedere lo [schema di project.json](../schema/project-json.md).)</span><span class="sxs-lookup"><span data-stu-id="2f085-136">(See [project.json schema](../schema/project-json.md).)</span></span>|
| <span data-ttu-id="2f085-137">PackageReference</span><span class="sxs-lookup"><span data-stu-id="2f085-137">PackageReference</span></span> | <span data-ttu-id="2f085-138">4.x+</span><span class="sxs-lookup"><span data-stu-id="2f085-138">4.x+</span></span> | <span data-ttu-id="2f085-139">Elenca le dipendenze direttamente nel file di progetto nel nodo `<PackageReference>`, insieme a `<Reference>` e `<ProjectReference>`.</span><span class="sxs-lookup"><span data-stu-id="2f085-139">Lists dependencies directly in the project file in the `<PackageReference>` node, alongside `<Reference>` and `<ProjectReference>`.</span></span> <span data-ttu-id="2f085-140">Funzionamento analogo a `project.json`. Vedere [Riferimenti ai pacchetti nei file di progetto](../Consume-Packages/Package-References-in-Project-Files.md).</span><span class="sxs-lookup"><span data-stu-id="2f085-140">Works similarly to `project.json`; see [Package references in project files](../Consume-Packages/Package-References-in-Project-Files.md).</span></span> |

<span data-ttu-id="2f085-141">In secondo luogo, si avvia un ripristino usando l'elenco di riferimenti in svariati modi:</span><span class="sxs-lookup"><span data-stu-id="2f085-141">Second, you start a restore using the reference list in a variety of ways:</span></span>

<span data-ttu-id="2f085-142">Dalla riga di comando o dalla [console di Gestione pacchetti](../tools/Package-Manager-Console.md):</span><span class="sxs-lookup"><span data-stu-id="2f085-142">From the command line or [Package Manager Console](../tools/Package-Manager-Console.md):</span></span>

| <span data-ttu-id="2f085-143">Comando</span><span class="sxs-lookup"><span data-stu-id="2f085-143">Command</span></span> | <span data-ttu-id="2f085-144">Scenari possibili</span><span class="sxs-lookup"><span data-stu-id="2f085-144">Applicable scenarios</span></span> |
| --- | --- | 
| `nuget restore` | <span data-ttu-id="2f085-145">Tutte le versioni di NuGet e tutti i tipi di riferimento.</span><span class="sxs-lookup"><span data-stu-id="2f085-145">All versions of NuGet and all reference types.</span></span> <span data-ttu-id="2f085-146">Vedere [Ripristino dalla riga di comando](#command-line-restore) di seguito.</span><span class="sxs-lookup"><span data-stu-id="2f085-146">See [Command-line restore](#command-line-restore) below.</span></span> | 
| `dotnet restore` | <span data-ttu-id="2f085-147">Come `nuget restore` per i progetti .NET Core.</span><span class="sxs-lookup"><span data-stu-id="2f085-147">Same as `nuget restore` for .NET Core projects.</span></span> <span data-ttu-id="2f085-148">Vedere [dotnet restore](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore).</span><span class="sxs-lookup"><span data-stu-id="2f085-148">See [dotnet restore](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore).</span></span> |
| `msbuild /t:restore` | <span data-ttu-id="2f085-149">Nuget 4.x+ e MSBuild 15.1+ con [riferimenti ai pacchetti solo nei file di progetto](../Consume-Packages/Package-References-in-Project-Files.md).</span><span class="sxs-lookup"><span data-stu-id="2f085-149">Nuget 4.x+ and MSBuild 15.1+ with [package references in project files](../Consume-Packages/Package-References-in-Project-Files.md) only.</span></span> <span data-ttu-id="2f085-150">Sia `nuget restore` che `dotnet restore` usano questo comando per i progetti applicabili.</span><span class="sxs-lookup"><span data-stu-id="2f085-150">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span> <span data-ttu-id="2f085-151">Vedere [Pack e restore di NuGet come destinazioni MSBuild - Destinazione di restore](../schema/msbuild-targets.md#restore-target).</span><span class="sxs-lookup"><span data-stu-id="2f085-151">See [NuGet pack and restore as MSBuild targets- restore target](../schema/msbuild-targets.md#restore-target).</span></span>|

<span data-ttu-id="2f085-152">Anche Visual Studio stesso ripristina i pacchetti in momenti diversi:</span><span class="sxs-lookup"><span data-stu-id="2f085-152">Visual Studio itself also restores packages at different times:</span></span>

| <span data-ttu-id="2f085-153">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f085-153">Type</span></span> | <span data-ttu-id="2f085-154">Quando viene eseguito il ripristino</span><span class="sxs-lookup"><span data-stu-id="2f085-154">When restore happens</span></span> |
| --- | --- |
| <span data-ttu-id="2f085-155">Ripristino di modello</span><span class="sxs-lookup"><span data-stu-id="2f085-155">Template restore</span></span> | <span data-ttu-id="2f085-156">Durante la creazione di un nuovo progetto, dato che alcuni modelli dipendono da pacchetti esterni.</span><span class="sxs-lookup"><span data-stu-id="2f085-156">During creation of a new project, as some templates depend on external packages.</span></span> |
| <span data-ttu-id="2f085-157">Ripristino in fase di compilazione</span><span class="sxs-lookup"><span data-stu-id="2f085-157">Build restore</span></span> | <span data-ttu-id="2f085-158">Come primo passaggio di una compilazione.</span><span class="sxs-lookup"><span data-stu-id="2f085-158">As the first step of a build.</span></span> |
| <span data-ttu-id="2f085-159">Ripristino di soluzione</span><span class="sxs-lookup"><span data-stu-id="2f085-159">Solution restore</span></span> | <span data-ttu-id="2f085-160">Quando l'utente fa clic con il pulsante destro del mouse su una soluzione e sceglie **Ripristina pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2f085-160">When user right-clicks a solution and selects **Restore NuGet Packages**.</span></span> |
| <span data-ttu-id="2f085-161">Ripristino in seguito a modifiche del progetto</span><span class="sxs-lookup"><span data-stu-id="2f085-161">Restore on project change</span></span> | <span data-ttu-id="2f085-162">*(Solo NuGet 4.x)*  Quando si usa un progetto basato su .NET Core SDK, incluso quando cambia lo stato del progetto.</span><span class="sxs-lookup"><span data-stu-id="2f085-162">*(NuGet 4.x only)* When a .NET Core SDK-based project is used, including when project state changes.</span></span> |

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="2f085-163">Abilitazione e disabilitazione del ripristino dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="2f085-163">Enabling and disabling package restore</span></span>

<span data-ttu-id="2f085-164">Il ripristino dei pacchetti viene abilitato principalmente tramite **Strumenti > Opzioni > Gestione pacchetti NuGet** in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="2f085-164">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![Controllo dei comportamenti di ripristino dei pacchetti tramite le opzioni di Gestione pacchetti NuGet](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="2f085-166">**Consenti a NuGet di scaricare i pacchetti mancanti**: controlla tutte le forme di ripristino dei pacchetti modificando l'impostazione `packageRestore/enabled` nel file `%AppData%\NuGet\NuGet.Config` come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2f085-166">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  <span data-ttu-id="2f085-167">L'impostazione `packageRestore/enabled` può essere sovrascritta a livello globale impostando una variabile d'ambiente denominata **EnableNuGetPackageRestore** con valore TRUE o FALSE prima di avviare Visual Studio o una compilazione.</span><span class="sxs-lookup"><span data-stu-id="2f085-167">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>
    

- <span data-ttu-id="2f085-168">**Verificare in automatico i pacchetti mancanti durante il build in Visual Studio**: controlla il ripristino automatico per NuGet 2.7 e versioni successive modificando l'impostazione `packageRestore/automatic` nel file `%AppData%\NuGet\NuGet.Config` come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2f085-168">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore for NuGet 2.7 and later by changing the `packageRestore/automatic` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>
            
    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

<span data-ttu-id="2f085-169">Per riferimento, vedere il [file di configurazione di NuGet - sezione packageRestore](../Schema/nuget-config-file.md#packagerestore-section).</span><span class="sxs-lookup"><span data-stu-id="2f085-169">For reference, see the [NuGet config file - packageRestore section](../Schema/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="2f085-170">In alcuni casi, uno sviluppatore o una società potrebbe avere l'esigenza di abilitare o disabilitare il ripristino dei pacchetti in un computer per impostazione predefinita per tutti gli utenti.</span><span class="sxs-lookup"><span data-stu-id="2f085-170">In some cases, a developer or company might want to enable or disable package restore on a machine by default for all users.</span></span> <span data-ttu-id="2f085-171">Questa operazione può essere eseguita aggiungendo le stesse impostazioni sopra indicate al file di configurazione NuGet globale disponibile in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span><span class="sxs-lookup"><span data-stu-id="2f085-171">This can be done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="2f085-172">I singoli utenti possono quindi abilitare il ripristino in modo selettivo, in base alle esigenze a livello di progetto.</span><span class="sxs-lookup"><span data-stu-id="2f085-172">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="2f085-173">Vedere [Configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) per informazioni dettagliate esatte su come NuGet assegna la priorità a più file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="2f085-173">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="2f085-174">Vincolo delle versioni dei pacchetti con il ripristino</span><span class="sxs-lookup"><span data-stu-id="2f085-174">Constraining package versions with restore</span></span>

<span data-ttu-id="2f085-175">Quando NuGet ripristina pacchetti con qualsiasi metodo, rispetta i vincoli specificati in `packages.config`, `project.json` o nel file di progetto:</span><span class="sxs-lookup"><span data-stu-id="2f085-175">When NuGet restores packages through any method, it will honor any constraints specified in `packages.config`, `project.json`, or the project file:</span></span>

- <span data-ttu-id="2f085-176">`packages.config`: specificare un intervallo di versioni nella proprietà `allowedVersion` della dipendenza.</span><span class="sxs-lookup"><span data-stu-id="2f085-176">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="2f085-177">Vedere [Reinstallazione e aggiornamento di pacchetti](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="2f085-177">See [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="2f085-178">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2f085-178">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="2f085-179">`project.json`: specificare un intervallo di versioni direttamente con il numero di versione della dipendenza.</span><span class="sxs-lookup"><span data-stu-id="2f085-179">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="2f085-180">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2f085-180">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- <span data-ttu-id="2f085-181">Riferimenti ai pacchetti nei file di progetto: specificare un intervallo di versioni direttamente con il numero di versione della dipendenza.</span><span class="sxs-lookup"><span data-stu-id="2f085-181">Package references in project files: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="2f085-182">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2f085-182">For example:</span></span>
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

<span data-ttu-id="2f085-183">In tutti i casi, usare la notazione descritta in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="2f085-183">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="command-line-restore"></a><span data-ttu-id="2f085-184">Ripristino dalla riga di comando</span><span class="sxs-lookup"><span data-stu-id="2f085-184">Command-line restore</span></span>

<span data-ttu-id="2f085-185">Per NuGet 2.7 e versioni successive, usare il comando [Restore](../tools/cli-ref-restore.md) per ripristinare tutti i pacchetti in una soluzione, indipendentemente dal fatto che usi `packages.config`, `project.json` o riferimenti ai pacchetti nei file di progetto.</span><span class="sxs-lookup"><span data-stu-id="2f085-185">For NuGet 2.7 and above, use the [Restore](../tools/cli-ref-restore.md) command to restore all packages in a solution (whether it uses `packages.config`, `project.json`, or package references in project files).</span></span> <span data-ttu-id="2f085-186">Per una determinata cartella di progetto, ad esempio `c:\proj\app`, ognuna delle varianti comuni di seguito consente di ripristinare i pacchetti:</span><span class="sxs-lookup"><span data-stu-id="2f085-186">For a given project folder such as `c:\proj\app`, the common variations below each restore the packages:</span></span>

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

<span data-ttu-id="2f085-187">Per NuGet 4.0+ e MSBuild 15.1+ è anche possibile usare `MSBuild /t:restore`, come descritto in [Pack e restore di NuGet come destinazioni MSBuild](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="2f085-187">For NuGet 4.0+ and MSBuild 15.1+, you can also use `MSBuild /t:restore` as described on [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="build-time-restore-in-visual-studio"></a><span data-ttu-id="2f085-188">Ripristino in fase di compilazione in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2f085-188">Build-time restore in Visual Studio</span></span>

<span data-ttu-id="2f085-189">Visual Studio consente di ripristinare automaticamente i pacchetti mancanti per impostazione predefinita all'inizio di una compilazione.</span><span class="sxs-lookup"><span data-stu-id="2f085-189">Visual Studio automatically restores missing packages by default at the beginning of a build.</span></span> <span data-ttu-id="2f085-190">Questo comportamento può essere modificato deselezionando **Strumenti > Opzioni > Gestione pacchetti NuGet > Generale > Verificare in automatico i pacchetti mancanti durante il build in Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="2f085-190">This behavior can be changed by clearing **Tools > Options > NuGet Package Manager > General > Automatically check for missing packages during build in Visual Studio**.</span></span>

<span data-ttu-id="2f085-191">Quando è abilitato, il ripristino automatico funziona nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="2f085-191">When enabled, automatic restore works as follows:</span></span>

1. <span data-ttu-id="2f085-192">All'avvio di una compilazione, Visual Studio indica a NuGet di ripristinare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="2f085-192">When a build begins, Visual Studio instructs NuGet to restore packages.</span></span>
1. <span data-ttu-id="2f085-193">NuGet cerca in modo ricorsivo tutti i file `packages.config` nella soluzione, cerca `project.json` oppure cerca nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="2f085-193">NuGet recursively looks for all `packages.config` files in the solution, looks for `project.json`, or looks in the project file.</span></span>
1. <span data-ttu-id="2f085-194">Per ogni pacchetto elencato nei file di riferimento, NuGet controlla se esiste già nella soluzione (a cartella `packages`, `project.lock.json` o `project.assets.json` a seconda che il progetto usi `packages.config`, `project.json` o riferimenti ai pacchetti nei file di progetto).</span><span class="sxs-lookup"><span data-stu-id="2f085-194">For each packages listed in the reference files, NuGet checks if it already exists in the solution (the `packages` folder, `project.lock.json`, or `project.assets.json` depending on whether the project is using `packages.config`, `project.json`, or package references in project files).</span></span>
1. <span data-ttu-id="2f085-195">Se il pacchetto non viene trovato, NuGet tenta prima di tutto di recuperare il pacchetto dalla cache (vedere [Gestione delle cache NuGet](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="2f085-195">If the package is not found, NuGet attempts to retrieve the package from its cache first (see [Managing the NuGet cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="2f085-196">Se il pacchetto non è presente nella cache, NuGet tenta di scaricare il pacchetto dalle origini abilitate elencate in **Strumenti > Opzioni > Gestione pacchetti NuGet > Origini pacchetti**, nell'ordine di visualizzazione delle origini.</span><span class="sxs-lookup"><span data-stu-id="2f085-196">If the package is not in the cache, NuGet attempts to download the package from the enabled sources as listed in **Tools > Options > NuGet Package Manager > Package Sources**, in the order that the sources appear.</span></span> <span data-ttu-id="2f085-197">In questo caso, NuGet non indica un errore per la ricerca del pacchetto fino al completamento del controllo in tutte le origini, quindi segnala l'errore solo per l'ultima origine nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="2f085-197">In this case, NuGet does not indicate a failure to find the package until all the sources have been checked, at which time it reports the failure only for the last source in the list.</span></span> <span data-ttu-id="2f085-198">Implicitamente, questo tipo di errore significa anche che il pacchetto non era presente in alcuna delle origini, anche se gli errori non vengono visualizzati singolarmente per tali origini.</span><span class="sxs-lookup"><span data-stu-id="2f085-198">By implication such an error also means that the package wasn't present on any of the other sources either, even though errors were not shown for those sources individually.</span></span>
1. <span data-ttu-id="2f085-199">Se il download ha esito positivo, NuGet memorizza il pacchetto nella cache e lo installa nella soluzione (ancora una volta, nella cartella `packages`, in `project.lock.json` o in `project.assets.json`). In caso contrario NuGet segnala un errore e anche la compilazione non riesce.</span><span class="sxs-lookup"><span data-stu-id="2f085-199">If the download is successful, NuGet caches the package and installs it into the solution (again, into either the `packages` folder, `project.lock.json`, or `project.assets.json`); otherwise NuGet fails and the build fails.</span></span>

<span data-ttu-id="2f085-200">Durante questo processo viene visualizzata una finestra di dialogo di stato con l'opzione per annullare il ripristino del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2f085-200">During this process, you see a progress dialog with the option to cancel package restore.</span></span>

## <a name="package-restore-with-team-foundation-build"></a><span data-ttu-id="2f085-201">Ripristino dei pacchetti con Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="2f085-201">Package Restore with Team Foundation Build</span></span>

<span data-ttu-id="2f085-202">La funzionalità di ripristino dei pacchetti viene comunemente usata durante la compilazione di progetti nei server di compilazione, come con Team Foundation Server (TFS) e Visual Studio Team Services, nonché altri sistemi di compilazione non trattati in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="2f085-202">Package restore is commonly used when building projects on build servers, as with Team Foundation Server (TFS) and Visual Studio Team Services (as well as other build systems, which are not covered here).</span></span>

### <a name="visual-studio-team-services"></a><span data-ttu-id="2f085-203">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="2f085-203">Visual Studio Team Services</span></span>

<span data-ttu-id="2f085-204">Quando si crea una definizione di compilazione in Team Services, includere semplicemente l'attività di ripristino dei pacchetti NuGet nella definizione prima di qualsiasi attività di compilazione.</span><span class="sxs-lookup"><span data-stu-id="2f085-204">When creating a build definition on Team Services, simply include the Restore NuGet Packages task in the definition before any build task.</span></span> <span data-ttu-id="2f085-205">Questa attività è inclusa per impostazione predefinita in vari modelli di compilazione.</span><span class="sxs-lookup"><span data-stu-id="2f085-205">This task is included by default in a number of build templates.</span></span>

![Attività di ripristino dei pacchetti NuGet in una definizione di compilazione di Visual Studio Team Services](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a><span data-ttu-id="2f085-207">Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="2f085-207">Team Foundation Server</span></span>

<span data-ttu-id="2f085-208">Con TFS 2013 e versioni successive, i pacchetti vengono ripristinati automaticamente per impostazione predefinita durante la compilazione, a condizione di usare un modello di Team Build per Team Foundation Server 2013 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="2f085-208">With TFS 2013 and later, packages are automatically restored by default during build, provided that you're using a Team Build Template for Team Foundation Server 2013 or later.</span></span>

<span data-ttu-id="2f085-209">Se si usa una versione precedente dei modelli di compilazione, ad esempio in un progetto di cui è stata eseguita la migrazione da versioni precedenti di TFS, sarà necessario eseguire la migrazione anche di questi modelli di compilazione a TFS 2013.</span><span class="sxs-lookup"><span data-stu-id="2f085-209">If you're using a previous version of build templates (such as in a project that's been migrated from earlier versions of TFS), you'll need to also migrate those build templates to TFS 2013.</span></span> <span data-ttu-id="2f085-210">Questo significa essenzialmente ricreare le parti personalizzate dei modelli di compilazione usando il modello appropriato per il controllo del codice sorgente (controllo della versione di Team Foundation o Git).</span><span class="sxs-lookup"><span data-stu-id="2f085-210">This essentially means recreating the custom parts of the Build Templates using the appropriate template for your source control (TFVC or Git).</span></span>

<span data-ttu-id="2f085-211">Per una versione precedente di TFS, è sufficiente includere un passaggio di compilazione per richiamare il comando di [ripristino della riga di comando](#command-line-restore), come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f085-211">For earlier version of TFS, you can simply include a build step to invoke [command-line restore](#command-line-restore) as described earlier.</span></span>

<span data-ttu-id="2f085-212">Per altri dettagli, vedere [Procedura dettagliata per il ripristino dei pacchetti con Team Foundation Build](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="2f085-212">For more details see then [Walkthrough of Package Restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>    
