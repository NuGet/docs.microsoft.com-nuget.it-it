---
title: Procedura dettagliata per il ripristino dei pacchetti NuGet con Team Foundation Build | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3113cccd-35f7-4980-8a6e-fc06556b5064
description: Descrizione dettagliata della procedura per il ripristino di pacchetti NuGet con Team Foundation Build (sia TFS che Visual Studio Team Services).
keywords: Ripristino di pacchetti NuGet, NuGet e TFS, NuGet e VSTS, sistemi di compilazione NuGet, team foundation build, progetti MSBuild personalizzati, compilazione nel cloud, integrazione continua
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82decfa1a39cb99c405840a8f13b0bc993111c09
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="4ca05-104">Configurazione del ripristino dei pacchetti con Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="4ca05-104">Setting up package restore with Team Foundation Build</span></span>

> <span data-ttu-id="4ca05-105">Si applica a:</span><span class="sxs-lookup"><span data-stu-id="4ca05-105">Applies To:</span></span>
>  - <span data-ttu-id="4ca05-106">Progetti MSBuild personalizzati in esecuzione in qualsiasi versione di TFS</span><span class="sxs-lookup"><span data-stu-id="4ca05-106">Custom MSBuild projects running on any version of TFS</span></span>
>  - <span data-ttu-id="4ca05-107">Team Foundation Server 2012 o versione precedente</span><span class="sxs-lookup"><span data-stu-id="4ca05-107">Team Foundation Server 2012 or earlier</span></span>
>  - <span data-ttu-id="4ca05-108">Modelli di processi personalizzati di Team Foundation Build di cui è stata eseguita la migrazione a TFS 2013 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="4ca05-108">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
>  - <span data-ttu-id="4ca05-109">Modelli del processo di compilazione da cui è stata rimossa la funzionalità di ripristino Nuget</span><span class="sxs-lookup"><span data-stu-id="4ca05-109">Build Process Templates With Nuget Restore functionality removed</span></span>
>
> <span data-ttu-id="4ca05-110">Se si usa Visual Studio Team Services o Team Foundation Server 2013 in locale con i relativi modelli del processo di compilazione, il ripristino automatico dei pacchetti avviene come parte del processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="4ca05-110">If you're using Visual Studio Team Services or on-premises Team Foundation Server 2013 with its build process templates, Automatic Package Restore happens as part of the build process.</span></span>

<span data-ttu-id="4ca05-111">Questa sezione presenta in modo dettagliato le procedure per ripristinare i pacchetti nell'ambito della [compilazione di Team Services](/vsts/build-release/index) per il controllo della versione di Git e Team Services.</span><span class="sxs-lookup"><span data-stu-id="4ca05-111">This section will provide a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="4ca05-112">Anche se questa procedura dettagliata è specifica per lo scenario d'uso di Visual Studio Team Services, i concetti si applicano anche ad altri sistemi di controllo della versione e di compilazione.</span><span class="sxs-lookup"><span data-stu-id="4ca05-112">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="4ca05-113">Approccio generale</span><span class="sxs-lookup"><span data-stu-id="4ca05-113">The general approach</span></span>

<span data-ttu-id="4ca05-114">Un vantaggio dell'uso di NuGet è la possibilità di usarlo per evitare l'archiviazione dei file binari nel sistema di controllo della versione.</span><span class="sxs-lookup"><span data-stu-id="4ca05-114">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="4ca05-115">Questo aspetto è particolarmente interessante se si usa un sistema di [controllo della versione distribuito](http://en.wikipedia.org/wiki/Distributed_revision_control) come Git, perché gli sviluppatori devono clonare un intero repository, compresa la cronologia completa, prima di poter lavorare in locale.</span><span class="sxs-lookup"><span data-stu-id="4ca05-115">This is especially interesting if you are using a [distributed version control](http://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="4ca05-116">L'archiviazione dei file binari può causare un aumento significativo delle dimensioni del repository, perché i file binari vengono in genere archiviati senza compressione delta.</span><span class="sxs-lookup"><span data-stu-id="4ca05-116">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="4ca05-117">NuGet supporta il [ripristino dei pacchetti](../consume-packages/package-restore.md) come parte della compilazione già da molto tempo.</span><span class="sxs-lookup"><span data-stu-id="4ca05-117">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="4ca05-118">L'implementazione precedente presentava un circolo vizioso per i pacchetti che volevano estendere il processo di compilazione, perché NuGet ripristinava i pacchetti durante la compilazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="4ca05-118">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="4ca05-119">MSBuild non consente tuttavia di estendere la compilazione durante la compilazione. Si potrebbe sostenere che è un problema di MSBuild, ma è in effetti un problema intrinseco.</span><span class="sxs-lookup"><span data-stu-id="4ca05-119">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="4ca05-120">A seconda dell'aspetto che è necessario estendere, potrebbe essere troppo tardi effettuarne la registrazione al momento del ripristino del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4ca05-120">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="4ca05-121">Per evitare questo problema, è necessario assicurarsi che i pacchetti vengano ripristinati come primo passaggio del processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="4ca05-121">The cure to this problem is making sure that packages are restored as the first step in the build process.</span></span> <span data-ttu-id="4ca05-122">NuGet 2.7+ facilita questa procedura tramite una riga di comando semplificata:</span><span class="sxs-lookup"><span data-stu-id="4ca05-122">NuGet 2.7+ makes this easy via a simplified command line:</span></span>

```
nuget restore path\to\solution.sln
```

<span data-ttu-id="4ca05-123">Quando il processo di compilazione ripristina i pacchetti prima di compilare il codice, non è necessario archiviare i file `.targets`</span><span class="sxs-lookup"><span data-stu-id="4ca05-123">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="4ca05-124">I pacchetti devono essere creati in modo da consentire il caricamento in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4ca05-124">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="4ca05-125">In caso contrario, può essere ancora necessario archiviare i file `.targets` in modo che altri sviluppatori possano semplicemente aprire la soluzione senza dover prima ripristinare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="4ca05-125">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="4ca05-126">Il progetto dimostrativo seguente illustra come configurare la compilazione in modo che non sia necessario archiviare le cartelle `packages` e i file `.targets`.</span><span class="sxs-lookup"><span data-stu-id="4ca05-126">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="4ca05-127">Illustra anche come configurare una compilazione automatizzata in Team Foundation Service per questo progetto di esempio.</span><span class="sxs-lookup"><span data-stu-id="4ca05-127">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="4ca05-128">Struttura del repository</span><span class="sxs-lookup"><span data-stu-id="4ca05-128">Repository structure</span></span>

<span data-ttu-id="4ca05-129">Il progetto dimostrativo è un semplice strumento da riga di comando che usa l'argomento della riga di comando per eseguire query in Bing.</span><span class="sxs-lookup"><span data-stu-id="4ca05-129">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="4ca05-130">È destinato a .NET Framework 4 e usa molti dei [pacchetti BCL](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async) e [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span><span class="sxs-lookup"><span data-stu-id="4ca05-130">It targets the .NET Framework 4 and uses many of the [BCL packages](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="4ca05-131">La struttura del repository è simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="4ca05-131">The structure of the repository looks as follows:</span></span>

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

<span data-ttu-id="4ca05-132">È possibile notare che non sono stati archiviati né la cartella `packages` né qualsiasi file `.targets`.</span><span class="sxs-lookup"><span data-stu-id="4ca05-132">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="4ca05-133">È stato tuttavia archiviato il file `nuget.exe`, perché è necessario durante la compilazione.</span><span class="sxs-lookup"><span data-stu-id="4ca05-133">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="4ca05-134">Seguendo una convenzione ampiamente diffusa, il file è stato archiviato in una cartella `tools` condivisa.</span><span class="sxs-lookup"><span data-stu-id="4ca05-134">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="4ca05-135">Il codice sorgente è disponibile nella cartella `src`.</span><span class="sxs-lookup"><span data-stu-id="4ca05-135">The source code is under the `src` folder.</span></span> <span data-ttu-id="4ca05-136">Anche se la demo usa una singola soluzione, si può facilmente immaginare che questa cartella possa contenere più di una soluzione.</span><span class="sxs-lookup"><span data-stu-id="4ca05-136">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="4ca05-137">Ignorare i file</span><span class="sxs-lookup"><span data-stu-id="4ca05-137">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="4ca05-138">Esiste attualmente un [bug noto del client NuGet](https://nuget.codeplex.com/workitem/4072) a causa del quale il client aggiunge comunque la cartella `packages` al controllo della versione.</span><span class="sxs-lookup"><span data-stu-id="4ca05-138">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="4ca05-139">La soluzione alternativa consiste nel disabilitare l'integrazione del controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="4ca05-139">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="4ca05-140">A tale scopo, è necessario un file `Nuget.Config ` nella cartella `.nuget` parallela alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="4ca05-140">In order to do that, you'll need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="4ca05-141">Se questa cartella non esiste ancora, è necessario crearla.</span><span class="sxs-lookup"><span data-stu-id="4ca05-141">If this folder doesn't exist yet, you'll need to create it.</span></span> <span data-ttu-id="4ca05-142">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md) aggiungere il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="4ca05-142">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```


<span data-ttu-id="4ca05-143">Per comunicare al sistema di controllo della versione che non si intende archiviare il contenuto delle cartelle **packages**, sono stati anche aggiunti i file da ignorare sia per Git (`.gitignore`) che per il controllo della versione di Team Foundation (`.tfignore`).</span><span class="sxs-lookup"><span data-stu-id="4ca05-143">In order to communicate to the version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="4ca05-144">Questi file descrivono i modelli di file che non si vuole archiviare.</span><span class="sxs-lookup"><span data-stu-id="4ca05-144">These files describes patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="4ca05-145">Il file `.gitignore` è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4ca05-145">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages

<span data-ttu-id="4ca05-146">Il file `.gitignore` offre [molte potenzialità](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="4ca05-146">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="4ca05-147">Ad esempio, se in genere non si vuole archiviare il contenuto della cartella `packages`, ma si vogliono rispettare le indicazioni precedenti di archiviare i file `.targets`, è possibile usare la regola seguente:</span><span class="sxs-lookup"><span data-stu-id="4ca05-147">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="4ca05-148">Questa regola escluderà tutte le cartelle `packages` ma includerà di nuovo tutti i file `.targets` contenuti.</span><span class="sxs-lookup"><span data-stu-id="4ca05-148">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="4ca05-149">È possibile trovare un modello per i file `.gitignore` su misura per le esigenze degli sviluppatori di Visual Studio [qui](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="4ca05-149">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="4ca05-150">Il controllo della versione di Team Foundation supporta un meccanismo molto simile tramite il file [tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control).</span><span class="sxs-lookup"><span data-stu-id="4ca05-150">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="4ca05-151">La sintassi è sostanzialmente la stessa:</span><span class="sxs-lookup"><span data-stu-id="4ca05-151">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages

## <a name="buildproj"></a><span data-ttu-id="4ca05-152">build.proj</span><span class="sxs-lookup"><span data-stu-id="4ca05-152">build.proj</span></span>

<span data-ttu-id="4ca05-153">Per questa demo, il processo di compilazione viene mantenuto piuttosto semplice.</span><span class="sxs-lookup"><span data-stu-id="4ca05-153">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="4ca05-154">Si creerà un progetto MSBuild che compila tutte le soluzioni assicurandosi che i pacchetti vengano ripristinati prima di compilare le soluzioni.</span><span class="sxs-lookup"><span data-stu-id="4ca05-154">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="4ca05-155">Questo progetto includerà le tre destinazioni convenzionali `Clean`, `Build` e `Rebuild`, oltre a una nuova destinazione `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="4ca05-155">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="4ca05-156">Le destinazioni `Build` e `Rebuild` dipendono entrambe da `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="4ca05-156">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="4ca05-157">Ciò assicura di poter eseguire sia `Build` che `Rebuild`, nonché di essere certi del ripristino dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="4ca05-157">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="4ca05-158">`Clean`, `Build` e `Rebuild` richiamano la destinazione MSBuild corrispondente in tutti i file di soluzione.</span><span class="sxs-lookup"><span data-stu-id="4ca05-158">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="4ca05-159">La destinazione `RestorePackages` richiama `nuget.exe` per ogni file di soluzione.</span><span class="sxs-lookup"><span data-stu-id="4ca05-159">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="4ca05-160">Questa operazione viene eseguita tramite la [funzionalità di invio in batch di MSBuild](/visualstudio/msbuild/msbuild-batching).</span><span class="sxs-lookup"><span data-stu-id="4ca05-160">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="4ca05-161">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="4ca05-161">The result looks as follows:</span></span>

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

## <a name="configuring-team-build"></a><span data-ttu-id="4ca05-162">Configurazione di Team Build</span><span class="sxs-lookup"><span data-stu-id="4ca05-162">Configuring Team Build</span></span>

<span data-ttu-id="4ca05-163">Team Build offre vari modelli di processo.</span><span class="sxs-lookup"><span data-stu-id="4ca05-163">Team Build offers various process templates.</span></span> <span data-ttu-id="4ca05-164">Per questa dimostrazione, si usa Team Foundation Service.</span><span class="sxs-lookup"><span data-stu-id="4ca05-164">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="4ca05-165">Le installazioni locali di TFS saranno comunque molto simili.</span><span class="sxs-lookup"><span data-stu-id="4ca05-165">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="4ca05-166">Per Git e il controllo della versione di Team Foundation sono disponibili modelli diversi di Team Build, pertanto le operazioni seguenti varieranno in base al sistema di controllo della versione in uso.</span><span class="sxs-lookup"><span data-stu-id="4ca05-166">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="4ca05-167">In entrambi i casi, è sufficiente selezionare il file build.proj come progetto da compilare.</span><span class="sxs-lookup"><span data-stu-id="4ca05-167">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="4ca05-168">Prima di tutto verrà esaminato il modello di processo per Git.</span><span class="sxs-lookup"><span data-stu-id="4ca05-168">First, let's look at the process template for git.</span></span> <span data-ttu-id="4ca05-169">Nel modello basato su Git, la compilazione viene selezionata tramite la proprietà `Solution to build`:</span><span class="sxs-lookup"><span data-stu-id="4ca05-169">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Processo di compilazione per Git](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="4ca05-171">Si noti che questa proprietà è un percorso nel repository.</span><span class="sxs-lookup"><span data-stu-id="4ca05-171">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="4ca05-172">Dato che il file `build.proj` del progetto di esempio si trova nella radice, è stato usato semplicemente `build.proj`.</span><span class="sxs-lookup"><span data-stu-id="4ca05-172">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="4ca05-173">Se si posizionasse il file di compilazione in una cartella denominata `tools`, il valore sarebbe `tools\build.proj`.</span><span class="sxs-lookup"><span data-stu-id="4ca05-173">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="4ca05-174">Nel modello del controllo della versione di Team Foundation, il progetto viene selezionato tramite la proprietà `Projects`:</span><span class="sxs-lookup"><span data-stu-id="4ca05-174">In the TF version control template the project is selected via the property `Projects`:</span></span>

![Processo di compilazione per il controllo della versione di Team Foundation](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="4ca05-176">A differenza del modello basato su Git, il controllo della versione di Team Foundation supporta le selezioni (il pulsante sul lato destro con tre puntini).</span><span class="sxs-lookup"><span data-stu-id="4ca05-176">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="4ca05-177">Per evitare errori di digitazione, è quindi consigliabile usarle per selezionare il progetto.</span><span class="sxs-lookup"><span data-stu-id="4ca05-177">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>