---
title: Procedura dettagliata per il ripristino dei pacchetti NuGet con Team Foundation Build
description: Descrizione dettagliata della procedura per il ripristino di pacchetti NuGet con Team Foundation Build (sia TFS che Visual Studio Team Services).
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 5eb8e68b800f623ef41a164f18efff2281e7c7cc
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="021f1-103">Configurazione del ripristino dei pacchetti con Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="021f1-103">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="021f1-104">Questo articolo presenta in modo dettagliato le procedure per ripristinare i pacchetti nell'ambito della [compilazione di Team Services](/vsts/build-release/index) per il controllo della versione di Git e Team Services.</span><span class="sxs-lookup"><span data-stu-id="021f1-104">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="021f1-105">Anche se questa procedura dettagliata è specifica per lo scenario d'uso di Visual Studio Team Services, i concetti si applicano anche ad altri sistemi di controllo della versione e di compilazione.</span><span class="sxs-lookup"><span data-stu-id="021f1-105">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="021f1-106">Si applica a:</span><span class="sxs-lookup"><span data-stu-id="021f1-106">Applies To:</span></span>

- <span data-ttu-id="021f1-107">Progetti MSBuild personalizzati in esecuzione in qualsiasi versione di TFS</span><span class="sxs-lookup"><span data-stu-id="021f1-107">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="021f1-108">Team Foundation Server 2012 o versione precedente</span><span class="sxs-lookup"><span data-stu-id="021f1-108">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="021f1-109">Modelli di processi personalizzati di Team Foundation Build di cui è stata eseguita la migrazione a TFS 2013 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="021f1-109">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="021f1-110">Modelli del processo di compilazione da cui è stata rimossa la funzionalità di ripristino Nuget</span><span class="sxs-lookup"><span data-stu-id="021f1-110">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="021f1-111">Se si usa Visual Studio Team Services o Team Foundation Server 2013 con i relativi modelli del processo di compilazione, il ripristino automatico dei pacchetti avviene come parte del processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="021f1-111">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="021f1-112">Approccio generale</span><span class="sxs-lookup"><span data-stu-id="021f1-112">The general approach</span></span>

<span data-ttu-id="021f1-113">Un vantaggio dell'uso di NuGet è la possibilità di usarlo per evitare l'archiviazione dei file binari nel sistema di controllo della versione.</span><span class="sxs-lookup"><span data-stu-id="021f1-113">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="021f1-114">Questo aspetto è particolarmente interessante se si usa un sistema di [controllo della versione distribuito](http://en.wikipedia.org/wiki/Distributed_revision_control) come Git, perché gli sviluppatori devono clonare un intero repository, compresa la cronologia completa, prima di poter lavorare in locale.</span><span class="sxs-lookup"><span data-stu-id="021f1-114">This is especially interesting if you are using a [distributed version control](http://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="021f1-115">L'archiviazione dei file binari può causare un aumento significativo delle dimensioni del repository, perché i file binari vengono in genere archiviati senza compressione delta.</span><span class="sxs-lookup"><span data-stu-id="021f1-115">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="021f1-116">NuGet supporta il [ripristino dei pacchetti](../consume-packages/package-restore.md) come parte della compilazione già da molto tempo.</span><span class="sxs-lookup"><span data-stu-id="021f1-116">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="021f1-117">L'implementazione precedente presentava un circolo vizioso per i pacchetti che volevano estendere il processo di compilazione, perché NuGet ripristinava i pacchetti durante la compilazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="021f1-117">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="021f1-118">MSBuild non consente tuttavia di estendere la compilazione durante la compilazione. Si potrebbe sostenere che è un problema di MSBuild, ma è in effetti un problema intrinseco.</span><span class="sxs-lookup"><span data-stu-id="021f1-118">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="021f1-119">A seconda dell'aspetto che è necessario estendere, potrebbe essere troppo tardi effettuarne la registrazione al momento del ripristino del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="021f1-119">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="021f1-120">Per evitare questo problema, è necessario assicurarsi che i pacchetti vengano ripristinati come primo passaggio del processo di compilazione:</span><span class="sxs-lookup"><span data-stu-id="021f1-120">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="021f1-121">Quando il processo di compilazione ripristina i pacchetti prima di compilare il codice, non è necessario archiviare i file `.targets`</span><span class="sxs-lookup"><span data-stu-id="021f1-121">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="021f1-122">I pacchetti devono essere creati in modo da consentire il caricamento in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="021f1-122">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="021f1-123">In caso contrario, può essere ancora necessario archiviare i file `.targets` in modo che altri sviluppatori possano semplicemente aprire la soluzione senza dover prima ripristinare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="021f1-123">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="021f1-124">Il progetto dimostrativo seguente illustra come configurare la compilazione in modo che non sia necessario archiviare le cartelle `packages` e i file `.targets`.</span><span class="sxs-lookup"><span data-stu-id="021f1-124">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="021f1-125">Illustra anche come configurare una compilazione automatizzata in Team Foundation Service per questo progetto di esempio.</span><span class="sxs-lookup"><span data-stu-id="021f1-125">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="021f1-126">Struttura del repository</span><span class="sxs-lookup"><span data-stu-id="021f1-126">Repository structure</span></span>

<span data-ttu-id="021f1-127">Il progetto dimostrativo è un semplice strumento da riga di comando che usa l'argomento della riga di comando per eseguire query in Bing.</span><span class="sxs-lookup"><span data-stu-id="021f1-127">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="021f1-128">È destinato a .NET Framework 4 e usa molti dei [pacchetti BCL](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async) e [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span><span class="sxs-lookup"><span data-stu-id="021f1-128">It targets the .NET Framework 4 and uses many of the [BCL packages](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="021f1-129">La struttura del repository è simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="021f1-129">The structure of the repository looks as follows:</span></span>

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

<span data-ttu-id="021f1-130">È possibile notare che non sono stati archiviati né la cartella `packages` né qualsiasi file `.targets`.</span><span class="sxs-lookup"><span data-stu-id="021f1-130">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="021f1-131">È stato tuttavia archiviato il file `nuget.exe`, perché è necessario durante la compilazione.</span><span class="sxs-lookup"><span data-stu-id="021f1-131">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="021f1-132">Seguendo una convenzione ampiamente diffusa, il file è stato archiviato in una cartella `tools` condivisa.</span><span class="sxs-lookup"><span data-stu-id="021f1-132">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="021f1-133">Il codice sorgente è disponibile nella cartella `src`.</span><span class="sxs-lookup"><span data-stu-id="021f1-133">The source code is under the `src` folder.</span></span> <span data-ttu-id="021f1-134">Anche se la demo usa una singola soluzione, si può facilmente immaginare che questa cartella possa contenere più di una soluzione.</span><span class="sxs-lookup"><span data-stu-id="021f1-134">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="021f1-135">Ignorare i file</span><span class="sxs-lookup"><span data-stu-id="021f1-135">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="021f1-136">Esiste attualmente un [bug noto del client NuGet](https://nuget.codeplex.com/workitem/4072) a causa del quale il client aggiunge comunque la cartella `packages` al controllo della versione.</span><span class="sxs-lookup"><span data-stu-id="021f1-136">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="021f1-137">La soluzione alternativa consiste nel disabilitare l'integrazione del controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="021f1-137">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="021f1-138">A tale scopo, è necessario un file `Nuget.Config ` nella cartella `.nuget` parallela alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="021f1-138">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="021f1-139">Se questa cartella non esiste ancora, è necessario crearla.</span><span class="sxs-lookup"><span data-stu-id="021f1-139">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="021f1-140">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md) aggiungere il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="021f1-140">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="021f1-141">Per comunicare al sistema di controllo della versione che non si intende archiviare il contenuto delle cartelle **packages**, sono stati anche aggiunti i file da ignorare sia per Git (`.gitignore`) che per il controllo della versione di Team Foundation (`.tfignore`).</span><span class="sxs-lookup"><span data-stu-id="021f1-141">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="021f1-142">Questi file descrivono i modelli di file che non si vuole archiviare.</span><span class="sxs-lookup"><span data-stu-id="021f1-142">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="021f1-143">Il file `.gitignore` è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="021f1-143">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

<span data-ttu-id="021f1-144">Il file `.gitignore` offre [molte potenzialità](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="021f1-144">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="021f1-145">Ad esempio, se in genere non si vuole archiviare il contenuto della cartella `packages`, ma si vogliono rispettare le indicazioni precedenti di archiviare i file `.targets`, è possibile usare la regola seguente:</span><span class="sxs-lookup"><span data-stu-id="021f1-145">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="021f1-146">Questa regola escluderà tutte le cartelle `packages` ma includerà di nuovo tutti i file `.targets` contenuti.</span><span class="sxs-lookup"><span data-stu-id="021f1-146">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="021f1-147">È possibile trovare un modello per i file `.gitignore` su misura per le esigenze degli sviluppatori di Visual Studio [qui](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="021f1-147">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="021f1-148">Il controllo della versione di Team Foundation supporta un meccanismo molto simile tramite il file [tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control).</span><span class="sxs-lookup"><span data-stu-id="021f1-148">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="021f1-149">La sintassi è sostanzialmente la stessa:</span><span class="sxs-lookup"><span data-stu-id="021f1-149">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a><span data-ttu-id="021f1-150">build.proj</span><span class="sxs-lookup"><span data-stu-id="021f1-150">build.proj</span></span>

<span data-ttu-id="021f1-151">Per questa demo, il processo di compilazione viene mantenuto piuttosto semplice.</span><span class="sxs-lookup"><span data-stu-id="021f1-151">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="021f1-152">Si creerà un progetto MSBuild che compila tutte le soluzioni assicurandosi che i pacchetti vengano ripristinati prima di compilare le soluzioni.</span><span class="sxs-lookup"><span data-stu-id="021f1-152">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="021f1-153">Questo progetto includerà le tre destinazioni convenzionali `Clean`, `Build` e `Rebuild`, oltre a una nuova destinazione `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="021f1-153">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="021f1-154">Le destinazioni `Build` e `Rebuild` dipendono entrambe da `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="021f1-154">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="021f1-155">Ciò assicura di poter eseguire sia `Build` che `Rebuild`, nonché di essere certi del ripristino dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="021f1-155">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="021f1-156">`Clean`, `Build` e `Rebuild` richiamano la destinazione MSBuild corrispondente in tutti i file di soluzione.</span><span class="sxs-lookup"><span data-stu-id="021f1-156">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="021f1-157">La destinazione `RestorePackages` richiama `nuget.exe` per ogni file di soluzione.</span><span class="sxs-lookup"><span data-stu-id="021f1-157">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="021f1-158">Questa operazione viene eseguita tramite la [funzionalità di invio in batch di MSBuild](/visualstudio/msbuild/msbuild-batching).</span><span class="sxs-lookup"><span data-stu-id="021f1-158">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="021f1-159">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="021f1-159">The result looks as follows:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a><span data-ttu-id="021f1-160">Configurazione di Team Build</span><span class="sxs-lookup"><span data-stu-id="021f1-160">Configuring Team Build</span></span>

<span data-ttu-id="021f1-161">Team Build offre vari modelli di processo.</span><span class="sxs-lookup"><span data-stu-id="021f1-161">Team Build offers various process templates.</span></span> <span data-ttu-id="021f1-162">Per questa dimostrazione, si usa Team Foundation Service.</span><span class="sxs-lookup"><span data-stu-id="021f1-162">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="021f1-163">Le installazioni locali di TFS saranno comunque molto simili.</span><span class="sxs-lookup"><span data-stu-id="021f1-163">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="021f1-164">Per Git e il controllo della versione di Team Foundation sono disponibili modelli diversi di Team Build, pertanto le operazioni seguenti varieranno in base al sistema di controllo della versione in uso.</span><span class="sxs-lookup"><span data-stu-id="021f1-164">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="021f1-165">In entrambi i casi, è sufficiente selezionare il file build.proj come progetto da compilare.</span><span class="sxs-lookup"><span data-stu-id="021f1-165">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="021f1-166">Prima di tutto verrà esaminato il modello di processo per Git.</span><span class="sxs-lookup"><span data-stu-id="021f1-166">First, let's look at the process template for git.</span></span> <span data-ttu-id="021f1-167">Nel modello basato su Git, la compilazione viene selezionata tramite la proprietà `Solution to build`:</span><span class="sxs-lookup"><span data-stu-id="021f1-167">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Processo di compilazione per Git](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="021f1-169">Si noti che questa proprietà è un percorso nel repository.</span><span class="sxs-lookup"><span data-stu-id="021f1-169">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="021f1-170">Dato che il file `build.proj` del progetto di esempio si trova nella radice, è stato usato semplicemente `build.proj`.</span><span class="sxs-lookup"><span data-stu-id="021f1-170">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="021f1-171">Se si posizionasse il file di compilazione in una cartella denominata `tools`, il valore sarebbe `tools\build.proj`.</span><span class="sxs-lookup"><span data-stu-id="021f1-171">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="021f1-172">Nel modello del controllo della versione di Team Foundation, il progetto viene selezionato tramite la proprietà `Projects`:</span><span class="sxs-lookup"><span data-stu-id="021f1-172">In the TF version control template the project is selected via the property `Projects`:</span></span>

![Processo di compilazione per il controllo della versione di Team Foundation](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="021f1-174">A differenza del modello basato su Git, il controllo della versione di Team Foundation supporta le selezioni (il pulsante sul lato destro con tre puntini).</span><span class="sxs-lookup"><span data-stu-id="021f1-174">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="021f1-175">Per evitare errori di digitazione, è quindi consigliabile usarle per selezionare il progetto.</span><span class="sxs-lookup"><span data-stu-id="021f1-175">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>
