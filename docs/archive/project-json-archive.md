---
title: Contenuto dell'archivio project.json NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/17/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Varie parti del contenuto di project.json rimosse da altre aree della documentazione di NuGet.
keywords: File project.json di NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 16361fe16d8ecc7064af4b6d636435a31a5663dc
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="projectjson-archive"></a><span data-ttu-id="a9da7-104">archivio project.json</span><span class="sxs-lookup"><span data-stu-id="a9da7-104">project.json archive</span></span>

<span data-ttu-id="a9da7-105">Il formato di gestione `project.json` è stato introdotto con NuGet 3.x e usato per determinati tipi di progetto.</span><span class="sxs-lookup"><span data-stu-id="a9da7-105">The `project.json` management format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="a9da7-106">È stato deprecato in seguito all'introduzione del formato PackageReference, con il quale le dipendenze vengono elencate direttamente in un file di progetto.</span><span class="sxs-lookup"><span data-stu-id="a9da7-106">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="a9da7-107">Vedere anche:</span><span class="sxs-lookup"><span data-stu-id="a9da7-107">Also see:</span></span>

- [<span data-ttu-id="a9da7-108">Schema di project.json</span><span class="sxs-lookup"><span data-stu-id="a9da7-108">project.json schema</span></span>](project-json.md)
- <span data-ttu-id="a9da7-109">[project.json impact on package authors](project-json-impact.md) (Impatto di project.json sugli autori di pacchetti)</span><span class="sxs-lookup"><span data-stu-id="a9da7-109">[project.json impact on package authors](project-json-impact.md)</span></span>
- [<span data-ttu-id="a9da7-110">project.json e UWP</span><span class="sxs-lookup"><span data-stu-id="a9da7-110">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a><span data-ttu-id="a9da7-111">Formato di gestione project.json</span><span class="sxs-lookup"><span data-stu-id="a9da7-111">project.json management format</span></span>

<span data-ttu-id="a9da7-112">*Originariamente in [Ripristino di pacchetti](../what-is-nuget.md).*</span><span class="sxs-lookup"><span data-stu-id="a9da7-112">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="a9da7-113">Nell'elenco dei formati di gestione:</span><span class="sxs-lookup"><span data-stu-id="a9da7-113">In the list of management formats:</span></span>

- <span data-ttu-id="a9da7-114">[`project.json`](project-json.md): *(deprecato)* File JSON che gestisce un elenco delle dipendenze del progetto con un grafico dei pacchetti complessivo in un file associato, `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="a9da7-114">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="a9da7-115">Questo formato è deprecato a favore di PackageReference.</span><span class="sxs-lookup"><span data-stu-id="a9da7-115">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="a9da7-116">nuget restore su Mono</span><span class="sxs-lookup"><span data-stu-id="a9da7-116">nuget restore on Mono</span></span>

<span data-ttu-id="a9da7-117">*Originariamente in [Installare gli strumenti client di NuGet](../install-nuget-client-tools.md).*</span><span class="sxs-lookup"><span data-stu-id="a9da7-117">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="a9da7-118">Funziona con `project.json`.</span><span class="sxs-lookup"><span data-stu-id="a9da7-118">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="a9da7-119">Vincolo delle versioni dei pacchetti con il ripristino</span><span class="sxs-lookup"><span data-stu-id="a9da7-119">Constraining package versions with restore</span></span>

<span data-ttu-id="a9da7-120">*Originariamente in [Ripristino di pacchetti](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span><span class="sxs-lookup"><span data-stu-id="a9da7-120">*Originally in [Package restore](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span></span>

- <span data-ttu-id="a9da7-121">`project.json`: specificare un intervallo di versioni direttamente con il numero di versione della dipendenza.</span><span class="sxs-lookup"><span data-stu-id="a9da7-121">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="a9da7-122">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a9da7-122">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="a9da7-123">Comandi dell'interfaccia della riga di comando di NuGet</span><span class="sxs-lookup"><span data-stu-id="a9da7-123">NuGet CLI commands</span></span>

- <span data-ttu-id="a9da7-124">`nuget install` non funziona con `project.json`.</span><span class="sxs-lookup"><span data-stu-id="a9da7-124">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="a9da7-125">`nuget restore`: con i progetti che usano `project.json`, genera un file `project.lock.json` e un file `<project>.nuget.props`, all'occorrenza.</span><span class="sxs-lookup"><span data-stu-id="a9da7-125">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="a9da7-126">(Entrambi i file possono essere omessi dal controllo del codice sorgente). L'argomento `<projectPath>` può puntare a un file `project.json`, con un comportamento uguale a puntare a `packages.config` o un file di progetto.</span><span class="sxs-lookup"><span data-stu-id="a9da7-126">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="a9da7-127">Nell'ordine di priorità per le cartelle dei pacchetti, la ricerca viene prima eseguita in `%userprofile%\.nuget\packages` quando si usa `project.json`.</span><span class="sxs-lookup"><span data-stu-id="a9da7-127">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="a9da7-128">`nuget update`: in Mono questo comando non funziona con i progetti che usano `project.json`.</span><span class="sxs-lookup"><span data-stu-id="a9da7-128">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="a9da7-129">Risoluzione delle dipendenze con PackageReference</span><span class="sxs-lookup"><span data-stu-id="a9da7-129">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="a9da7-130">*Originariamente in [Risoluzione delle dipendenze](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span><span class="sxs-lookup"><span data-stu-id="a9da7-130">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="a9da7-131">Il comportamento di PackageReference si applica anche a `project.json`.</span><span class="sxs-lookup"><span data-stu-id="a9da7-131">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="a9da7-132">Il ripristino NuGet scrive il grafico dipendenze in un file denominato `project.lock.json` insieme a `project.json`.</span><span class="sxs-lookup"><span data-stu-id="a9da7-132">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="a9da7-133">Gestione degli asset delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="a9da7-133">Managing dependency assets</span></span>

<span data-ttu-id="a9da7-134">*Originariamente in [Risoluzione delle dipendenze](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span><span class="sxs-lookup"><span data-stu-id="a9da7-134">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="a9da7-135">Quando si usa il formato `project.json`, è possibile controllare quali asset delle dipendenze vengono inseriti nel progetto di primo livello.</span><span class="sxs-lookup"><span data-stu-id="a9da7-135">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="a9da7-136">Per informazioni dettagliate, vedere [project.json](project-json.md).</span><span class="sxs-lookup"><span data-stu-id="a9da7-136">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="a9da7-137">Esclusione dei riferimenti</span><span class="sxs-lookup"><span data-stu-id="a9da7-137">Excluding references</span></span>

<span data-ttu-id="a9da7-138">*Originariamente in [Risoluzione delle dipendenze](../consume-packages/dependency-resolution.md#excluding-references).*</span><span class="sxs-lookup"><span data-stu-id="a9da7-138">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="a9da7-139">`project.json`: aggiungere `"exclude" : "all"` nella dipendenza per il pacchetto C (PackageC):</span><span class="sxs-lookup"><span data-stu-id="a9da7-139">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="a9da7-140">Risoluzione degli errori dei pacchetti incompatibili</span><span class="sxs-lookup"><span data-stu-id="a9da7-140">Resolving incompatible package errors</span></span>

<span data-ttu-id="a9da7-141">*Originariamente in [Risoluzione delle dipendenze](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span><span class="sxs-lookup"><span data-stu-id="a9da7-141">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="a9da7-142">Un ulteriore metodo per la risoluzione degli errori:</span><span class="sxs-lookup"><span data-stu-id="a9da7-142">An added means of resolving errors:</span></span>

- <span data-ttu-id="a9da7-143">**Non consigliato**: come soluzione temporanea mentre si collabora con l'autore del pacchetto, i progetti che hanno come destinazione `netcore`, `netstandard` e `netcoreapp` possono indicare altri framework come compatibili, consentendo pertanto di usare i pacchetti che hanno come destinazione questi altri framework.</span><span class="sxs-lookup"><span data-stu-id="a9da7-143">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="a9da7-144">Vedere la [sezione Imports di project.json](project-json.md#imports) e la [sezione PackageTargetFallback delle destinazioni di ripristino di MSBuild](../reference/msbuild-targets.md#packagetargetfallback).</span><span class="sxs-lookup"><span data-stu-id="a9da7-144">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="a9da7-145">Ciò può causare comportamenti imprevisti, pertanto ancora una volta è consigliabile risolvere le incompatibilità dei pacchetti collaborando con l'autore del pacchetto alla realizzazione di un aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="a9da7-145">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="a9da7-146">Framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="a9da7-146">Target frameworks</span></span>

<span data-ttu-id="a9da7-147">*Originariamente in [Framework di destinazione](../reference/target-frameworks.md).*</span><span class="sxs-lookup"><span data-stu-id="a9da7-147">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="a9da7-148">[project.json](project-json.md): il nodo `frameworks` specifica le versioni del framework per le quali può essere compilato il progetto.</span><span class="sxs-lookup"><span data-stu-id="a9da7-148">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="a9da7-149">Creazione di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="a9da7-149">Creating a package</span></span>

<span data-ttu-id="a9da7-150">*Originariamente in [Creazione di un pacchetto](../create-packages/creating-a-package.md)*</span><span class="sxs-lookup"><span data-stu-id="a9da7-150">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="a9da7-151">Impostazione di un tipo di pacchetto</span><span class="sxs-lookup"><span data-stu-id="a9da7-151">Setting a package type</span></span>

<span data-ttu-id="a9da7-152">Con .NET Core 1.x, quando viene installato un pacchetto DotnetCliTool, Visual Studio inserisce il pacchetto nel nodo `tools` di `project.json` invece che nel nodo `dependencies`.</span><span class="sxs-lookup"><span data-stu-id="a9da7-152">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="a9da7-153">I tipi di pacchetto vengono impostati in `project.json`.</span><span class="sxs-lookup"><span data-stu-id="a9da7-153">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="a9da7-154">`project.json`: indica il tipo di pacchetto in un codice json della proprietà `packOptions.packageType`:</span><span class="sxs-lookup"><span data-stu-id="a9da7-154">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="a9da7-155">Aggiunta di destinazioni e proprietà per MSBuild</span><span class="sxs-lookup"><span data-stu-id="a9da7-155">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="a9da7-156">*Originariamente in [Creare pacchetti NuGet di .NET Standard con Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span><span class="sxs-lookup"><span data-stu-id="a9da7-156">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="a9da7-157">Quando si usa `project.json`, le destinazioni non vengono aggiunte al progetto, ma vengono rese disponibili tramite `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="a9da7-157">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="a9da7-158">Controllo delle versioni dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="a9da7-158">Package versioning</span></span>

<span data-ttu-id="a9da7-159">*Originariamente in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md).*</span><span class="sxs-lookup"><span data-stu-id="a9da7-159">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="a9da7-160">Quando si usa il formato `project.json`, NuGet supporta anche l'uso di una notazione con caratteri jolly, \*, per le parti del numero suffisso per versione principale, secondaria, patch e non definitiva.</span><span class="sxs-lookup"><span data-stu-id="a9da7-160">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="a9da7-161">Informazioni di riferimento su NuGet.config</span><span class="sxs-lookup"><span data-stu-id="a9da7-161">NuGet.Config reference</span></span>

<span data-ttu-id="a9da7-162">*Originariamente in [Informazioni di riferimento su NuGet.config](../reference/nuget-config-file.md).*</span><span class="sxs-lookup"><span data-stu-id="a9da7-162">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="a9da7-163">`globalPackagesFolder` si applica solo a `project.json`.</span><span class="sxs-lookup"><span data-stu-id="a9da7-163">`globalPackagesFolder` applies only to `project.json`.</span></span> <span data-ttu-id="a9da7-164">(Aggiunta di una nota: si applica anche a PackageReference.)</span><span class="sxs-lookup"><span data-stu-id="a9da7-164">(Added note: also applies to PackageReference.)</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="a9da7-165">Informazioni di riferimento sul file .nuspec</span><span class="sxs-lookup"><span data-stu-id="a9da7-165">nuspec file reference</span></span>

<span data-ttu-id="a9da7-166">*Originariamente in [Informazioni di riferimento sul file .nuspec](../reference/nuspec.md).*</span><span class="sxs-lookup"><span data-stu-id="a9da7-166">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="a9da7-167">L'elemento `<contentFiles>` viene usato al posto di `<files>` con `project.json`.</span><span class="sxs-lookup"><span data-stu-id="a9da7-167">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="a9da7-168">Controllo delle opzioni di Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="a9da7-168">Package manager options control</span></span>

<span data-ttu-id="a9da7-169">*Originariamente in [Package Manager UI reference](../tools/package-manager-ui.md) (Informazioni di riferimento sull'interfaccia utente di Gestione pacchetti).*</span><span class="sxs-lookup"><span data-stu-id="a9da7-169">*Originally in [Package Manager UI reference](../tools/package-manager-ui.md).*</span></span>

<span data-ttu-id="a9da7-170">I progetti che usano il formato di gestione `project.json` mostrano solo l'opzione **Visualizza finestra di anteprima**.</span><span class="sxs-lookup"><span data-stu-id="a9da7-170">Projects using `project.json` management format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="a9da7-171">Modelli di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a9da7-171">Visual Studio Templates</span></span>

<span data-ttu-id="a9da7-172">*Originariamente in [Pacchetti NuGet nei modelli di Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*</span><span class="sxs-lookup"><span data-stu-id="a9da7-172">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="a9da7-173">Procedure consigliate: i modelli non includono un file `project.json` e non includono riferimenti o contenuto che verrebbero aggiunti durante l'installazione di pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="a9da7-173">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>