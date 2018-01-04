---
title: Installazione degli strumenti client di NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: Istruzioni per l'installazione degli strumenti client, dell'interfaccia della riga di comando e di Gestione pacchetti per Visual Studio.
keywords: interfaccia della riga di comando nuget.exe, strumenti client NuGet, Gestione pacchetti NuGet, console di Gestione pacchetti NuGet, NuGet per Visual Studio, canale beta NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1abb30458c9ebfb0ffb28be254efd9709a9627f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="installing-nuget-client-tools"></a><span data-ttu-id="d6a66-104">Installazione degli strumenti client di NuGet</span><span class="sxs-lookup"><span data-stu-id="d6a66-104">Installing NuGet client tools</span></span>

> [!Tip]
> <span data-ttu-id="d6a66-105">**Se servono istruzioni per installare un pacchetto, vedere [Guida introduttiva - Usare un pacchetto](../Quickstart/Use-a-Package.md).**</span><span class="sxs-lookup"><span data-stu-id="d6a66-105">**Looking to install a package? See [Quickstart - Use a package](../Quickstart/Use-a-Package.md).**</span></span>

<span data-ttu-id="d6a66-106">Esistono due strumenti principali per creare, pubblicare e utilizzare pacchetti NuGet:</span><span class="sxs-lookup"><span data-stu-id="d6a66-106">There are two primary tools available to help you build, publish and consume NuGet packages:</span></span>

1. <span data-ttu-id="d6a66-107">L'[**interfaccia della riga di comando di NuGet**](#nuget-cli) è l'utilità della riga di comando per Windows che fornisce tutte le funzionalità di NuGet. Può essere eseguita anche in Mac OSX e Linux tramite Mono o tramite l'interfaccia della riga di comando di .NET Core (`dotnet`).</span><span class="sxs-lookup"><span data-stu-id="d6a66-107">The [**NuGet CLI**](#nuget-cli) is the command-line utility for Windows that provides all NuGet capabilities; it can also be run on Mac OSX and Linux using Mono, or through the .NET Core CLI (`dotnet`).</span></span>
1. <span data-ttu-id="d6a66-108">[**Gestione pacchetti NuGet in Visual Studio**](#nuget-package-manager-in-visual-studio) (solo Windows) è uno strumento GUI per la gestione dei pacchetti e include una console di PowerShell tramite cui è possibile usare alcuni comandi NuGet direttamente all'interno di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d6a66-108">The [**NuGet Package Manager in Visual Studio**](#nuget-package-manager-in-visual-studio) (Windows only) is a GUI tool for managing packages and includes a PowerShell console through which you can use certain NuGet commands directly within Visual Studio.</span></span> <span data-ttu-id="d6a66-109">L'interfaccia utente e la console di Gestione pacchetti sono entrambi inclusi in Visual Studio (in Windows) 2012 e versioni successive e possono essere installati manualmente per le versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="d6a66-109">The Package Manager UI and Console are both included with Visual Studio (on Windows) 2012 and later and can be installed manually for earlier versions.</span></span>

    <span data-ttu-id="d6a66-110">In Visual Studio per Mac, le funzionalità NuGet sono incorporate direttamente.</span><span class="sxs-lookup"><span data-stu-id="d6a66-110">With Visual Studio for Mac, NuGet capabilities are built in directly.</span></span> <span data-ttu-id="d6a66-111">Per una procedura dettagliata, vedere [Inserimento di un pacchetto NuGet nel progetto](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="d6a66-111">See [Including a NuGet package in your project](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough) for a walkthrough.</span></span>

    <span data-ttu-id="d6a66-112">Visual Studio Code attualmente non include il supporto predefinito per NuGet.</span><span class="sxs-lookup"><span data-stu-id="d6a66-112">Visual Studio Code at present does not have any built-in NuGet support.</span></span> <span data-ttu-id="d6a66-113">Usare l'interfaccia della riga di comando di NuGet o l'[interfaccia della riga di comando di dotnet](../Tools/dotnet-Commands.md).</span><span class="sxs-lookup"><span data-stu-id="d6a66-113">Use the NuGet CLI or the [dotnet CLI](../Tools/dotnet-Commands.md).</span></span>

<span data-ttu-id="d6a66-114">L'interfaccia della riga di comando e Gestione pacchetti NuGet supportano entrambi le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6a66-114">The NuGet CLI and Package Manager both support the following operations:</span></span>

- <span data-ttu-id="d6a66-115">Ricerche nei pacchetti</span><span class="sxs-lookup"><span data-stu-id="d6a66-115">Search packages</span></span>
- <span data-ttu-id="d6a66-116">Installazione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="d6a66-116">Install packages</span></span>
- <span data-ttu-id="d6a66-117">Aggiornamento di pacchetti</span><span class="sxs-lookup"><span data-stu-id="d6a66-117">Update packages</span></span>
- <span data-ttu-id="d6a66-118">Disinstallazione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="d6a66-118">Uninstall packages</span></span>
- <span data-ttu-id="d6a66-119">Ripristino di pacchetti (solo tramite interfaccia utente in Gestione pacchetti)</span><span class="sxs-lookup"><span data-stu-id="d6a66-119">Restore packages (UI only in the Package Manager)</span></span>
- <span data-ttu-id="d6a66-120">Gestione delle origini NuGet</span><span class="sxs-lookup"><span data-stu-id="d6a66-120">Manage NuGet sources</span></span>

<span data-ttu-id="d6a66-121">Le funzionalità seguenti sono supportate solo nell'interfaccia della riga di comando di NuGet:</span><span class="sxs-lookup"><span data-stu-id="d6a66-121">The following capabilities are supported only in the NuGet CLI:</span></span>

- <span data-ttu-id="d6a66-122">Gestione dei pacchetti (nuget.org o feed privato)</span><span class="sxs-lookup"><span data-stu-id="d6a66-122">Manage packages (nuget.org or private feed)</span></span>
- <span data-ttu-id="d6a66-123">Creazione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="d6a66-123">Create packages</span></span> 
- <span data-ttu-id="d6a66-124">Pubblicazione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="d6a66-124">Publish packages</span></span>
- <span data-ttu-id="d6a66-125">Gestione di NuGet.config</span><span class="sxs-lookup"><span data-stu-id="d6a66-125">Manage Nuget.Config</span></span>
- <span data-ttu-id="d6a66-126">Gestione delle cache NuGet</span><span class="sxs-lookup"><span data-stu-id="d6a66-126">Manage the NuGet cache</span></span>
- <span data-ttu-id="d6a66-127">Replica di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="d6a66-127">Replicating a package</span></span>

> [!Note]
> <span data-ttu-id="d6a66-128">Un altro strumento utile è [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), uno strumento open source autonomo per esplorare, creare e modificare visivamente i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="d6a66-128">Another good tool is the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), an open-source, stand-alone tool to visually explore, create, and edit NuGet packages.</span></span> <span data-ttu-id="d6a66-129">È molto utile, ad esempio, per apportare modifiche sperimentali alla struttura di un pacchetto senza dovere ricompilare il pacchetto ogni volta.</span><span class="sxs-lookup"><span data-stu-id="d6a66-129">It's very helpful, for example, to make experimental changes to a package structure without having to rebuild the package each time.</span></span>
> <span data-ttu-id="d6a66-130">La toolchain dell'[interfaccia della riga di comando .NET Core](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) multipiattaforma, usata per lo sviluppo di applicazioni .NET Core, supporta vari comandi NuGet, ad esempio delete, locals, push, pack e restore.</span><span class="sxs-lookup"><span data-stu-id="d6a66-130">The cross-platform [.NET Core CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) toolchain, used for developing .NET Core applications, supports several NuGet commands, such as delete, locals, push, pack, and restore.</span></span> 

## <a name="nuget-cli"></a><span data-ttu-id="d6a66-131">Interfaccia della riga di comando di NuGet</span><span class="sxs-lookup"><span data-stu-id="d6a66-131">NuGet CLI</span></span>

<span data-ttu-id="d6a66-132">L'interfaccia della riga di comando di NuGet consente di accedere a tutte le funzionalità di NuGet e può essere eseguita in Windows, Mac OSX e Linux, come descritto nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="d6a66-132">The NuGet command-line interface provides access to all NuGet capabilities, and can be run on Windows, Mac OSX, and Linux as described in the following sections.</span></span>

### <a name="windows"></a><span data-ttu-id="d6a66-133">Windows</span><span class="sxs-lookup"><span data-stu-id="d6a66-133">Windows</span></span>

<span data-ttu-id="d6a66-134">**Download diretto:**</span><span class="sxs-lookup"><span data-stu-id="d6a66-134">**Direct download:**</span></span>

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> <span data-ttu-id="d6a66-135">Con NuGet 1.4+ è possibile usare `nuget update -self` per aggiornare la copia esistente di nuget.exe alla versione più recente.</span><span class="sxs-lookup"><span data-stu-id="d6a66-135">With NuGet 1.4+, you can use `nuget update -self` to update your existing nuget.exe to the latest version.</span></span>

<span data-ttu-id="d6a66-136">**Altri metodi:**</span><span class="sxs-lookup"><span data-stu-id="d6a66-136">**Other methods:**</span></span>

- <span data-ttu-id="d6a66-137">**Chocolatey**: installare il pacchetto Chocolatey [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) tramite il client [Chocolatey](http://chocolatey.org).</span><span class="sxs-lookup"><span data-stu-id="d6a66-137">**Chocolatey**: Install the [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey package using the [Chocolatey](http://chocolatey.org) client.</span></span> 

    ```ps
    choco install nuget.commandline
    ```

- <span data-ttu-id="d6a66-138">**Visual Studio**: installare il pacchetto [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) dalla console di Gestione pacchetti in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d6a66-138">**Visual Studio**: Install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the Package Manager Console in Visual Studio.</span></span>

    > [!Note]
    > <span data-ttu-id="d6a66-139">**Per gli utenti di NuGet 2.x**: a causa di modifiche sostanziali introdotte in NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) punta all'ultima versione stabile di NuGet 2.x per evitare potenziali interruzioni per i sistemi di integrazione continua.</span><span class="sxs-lookup"><span data-stu-id="d6a66-139">**For NuGet 2.x users**: Because of breaking changes introduced in NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) points to the latest stable NuGet 2.x release to prevent continuous integration systems from potentially breaking.</span></span>

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a><span data-ttu-id="d6a66-140">Mac OSX e Linux</span><span class="sxs-lookup"><span data-stu-id="d6a66-140">Mac OSX and Linux</span></span>

<span data-ttu-id="d6a66-141">In Mac OSX e Linux, esistono due modi per eseguire l'interfaccia della riga di comando di NuGet:</span><span class="sxs-lookup"><span data-stu-id="d6a66-141">On Mac OSX and Linux, there are two ways to run the NuGet CLI:</span></span>

- <span data-ttu-id="d6a66-142">Installare [.NET Core SDK](https://www.microsoft.com/net/download/core), che include le funzionalità principali di NuGet.</span><span class="sxs-lookup"><span data-stu-id="d6a66-142">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core), which includes the core NuGet capabilities.</span></span> <span data-ttu-id="d6a66-143">I download sono elencati anche in [github.com/dotnet/cli](https://github.com/dotnet/cli).</span><span class="sxs-lookup"><span data-stu-id="d6a66-143">Downloads are also listed on [github.com/dotnet/cli](https://github.com/dotnet/cli).</span></span> <span data-ttu-id="d6a66-144">Se sono necessarie funzionalità più complete, scegliere la seconda opzione descritta di seguito per usare `nuget.exe` con Mono.</span><span class="sxs-lookup"><span data-stu-id="d6a66-144">If you need fuller capabilities, then use the second option below to use `nuget.exe` with Mono.</span></span>

- <span data-ttu-id="d6a66-145">Installare [Mono](http://www.mono-project.com/docs/getting-started/install/) e quindi usare l'eseguibile della riga di comando `nuget.exe` per Windows (versione 3.2 e versioni successive) da [nuget.org/downloads](https://nuget.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="d6a66-145">Install [Mono](http://www.mono-project.com/docs/getting-started/install/) and then use the `nuget.exe` command-line executable for Windows (version 3.2 and later) from [nuget.org/downloads](https://nuget.org/downloads).</span></span> <span data-ttu-id="d6a66-146">L'esecuzione di NuGet in Mono è soggetta alle limitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6a66-146">Running NuGet on Mono is subject to the following limitations:</span></span>

    - <span data-ttu-id="d6a66-147">Comandi di cui è stato testato il funzionamento:</span><span class="sxs-lookup"><span data-stu-id="d6a66-147">Commands tested to work:</span></span>
        - <span data-ttu-id="d6a66-148">config</span><span class="sxs-lookup"><span data-stu-id="d6a66-148">config</span></span>
        - <span data-ttu-id="d6a66-149">delete</span><span class="sxs-lookup"><span data-stu-id="d6a66-149">delete</span></span>
        - <span data-ttu-id="d6a66-150">guida</span><span class="sxs-lookup"><span data-stu-id="d6a66-150">help</span></span>
        - <span data-ttu-id="d6a66-151">install</span><span class="sxs-lookup"><span data-stu-id="d6a66-151">install</span></span>
        - <span data-ttu-id="d6a66-152">list</span><span class="sxs-lookup"><span data-stu-id="d6a66-152">list</span></span>
        - <span data-ttu-id="d6a66-153">push</span><span class="sxs-lookup"><span data-stu-id="d6a66-153">push</span></span>
        - <span data-ttu-id="d6a66-154">setApiKey</span><span class="sxs-lookup"><span data-stu-id="d6a66-154">setApiKey</span></span>
        - <span data-ttu-id="d6a66-155">sources</span><span class="sxs-lookup"><span data-stu-id="d6a66-155">sources</span></span>
        - <span data-ttu-id="d6a66-156">spec</span><span class="sxs-lookup"><span data-stu-id="d6a66-156">spec</span></span>

    - <span data-ttu-id="d6a66-157">Comandi che funzionano parzialmente:</span><span class="sxs-lookup"><span data-stu-id="d6a66-157">Partially-working commands:</span></span>
        - <span data-ttu-id="d6a66-158">pack: funziona con i file `.nuspec` ma non con i file di progetto.</span><span class="sxs-lookup"><span data-stu-id="d6a66-158">pack: works with `.nuspec` files but not with project files.</span></span>
        - <span data-ttu-id="d6a66-159">restore: funziona con i file `packages.config` e `project.json` ma non con i file di soluzione (`.sln`).</span><span class="sxs-lookup"><span data-stu-id="d6a66-159">restore: works with `packages.config` and `project.json` files but not with solution (`.sln`) files.</span></span>

    - <span data-ttu-id="d6a66-160">Comandi che non funzionano:</span><span class="sxs-lookup"><span data-stu-id="d6a66-160">Commands that do not work:</span></span>
        - <span data-ttu-id="d6a66-161">update</span><span class="sxs-lookup"><span data-stu-id="d6a66-161">update</span></span>

### <a name="related-topics"></a><span data-ttu-id="d6a66-162">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="d6a66-162">Related topics</span></span>

- [<span data-ttu-id="d6a66-163">Informazioni di riferimento sull'interfaccia della riga di comando di NuGet</span><span class="sxs-lookup"><span data-stu-id="d6a66-163">NuGet CLI reference</span></span>](../tools/nuget-exe-cli-reference.md)
- [<span data-ttu-id="d6a66-164">Creazione di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="d6a66-164">Creating a package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="d6a66-165">Pubblicazione di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="d6a66-165">Publishing a Package</span></span>](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a><span data-ttu-id="d6a66-166">Gestione pacchetti NuGet in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d6a66-166">NuGet Package Manager in Visual Studio</span></span>

<span data-ttu-id="d6a66-167">Gestione pacchetti NuGet è incluso in ogni edizione di Visual Studio in Windows 2012 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="d6a66-167">The NuGet Package Manager is included in every edition of Visual Studio on Windows, 2012 and later.</span></span> <span data-ttu-id="d6a66-168">Include l'interfaccia utente di Gestione pacchetti ([riferimento](../tools/package-manager-ui.md)) e la console di Gestione pacchetti tramite cui è possibile accedere agli strumenti forniti con alcuni pacchetti ([riferimento](../tools/package-manager-console.md)).</span><span class="sxs-lookup"><span data-stu-id="d6a66-168">It includes the Package Manager UI ([reference](../tools/package-manager-ui.md)), and the Package Manager Console through which you can access tools that come with certain packages ([reference](../tools/package-manager-console.md)).</span></span>

<span data-ttu-id="d6a66-169">Il programma di installazione di Visual Studio 2017 include Gestione pacchetti NuGet in qualsiasi carico di lavoro che usa .NET.</span><span class="sxs-lookup"><span data-stu-id="d6a66-169">The Visual Studio 2017 installer includes the NuGet Package Manager with any workload that employs .NET.</span></span> <span data-ttu-id="d6a66-170">Per eseguire l'installazione separatamente o per verificare che Gestione pacchetti sia installato, eseguire il programma di installazione di Visual Studio 2017 e selezionare l'opzione **Singoli componenti > Strumenti per il codice > Gestione pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d6a66-170">To install separately, or to verify that the Package Manager is installed, run the Visual Studio 2017 installer and check the option under **Individual Components > Code tools > NuGet package manager**.</span></span>

> [!Note]
> <span data-ttu-id="d6a66-171">La console richiede [PowerShell 2.0](http://support.microsoft.com/kb/968929), che sarà già installato in Windows 7 o versione successiva e Windows Server 2008 R2 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="d6a66-171">The console requires [PowerShell 2.0](http://support.microsoft.com/kb/968929), which will already be installed on Windows 7 or higher and Windows Server 2008 R2 or higher.</span></span>
>
> <span data-ttu-id="d6a66-172">I comandi della console di Gestione pacchetti, inoltre, funzionano solo all'interno di Visual Studio in Windows.</span><span class="sxs-lookup"><span data-stu-id="d6a66-172">Package Manager Console commands also work only within Visual Studio on Windows.</span></span> <span data-ttu-id="d6a66-173">Usare l'interfaccia della riga di comando di NuGet al di fuori di tale ambiente, inclusi Visual Studio per Mac e Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d6a66-173">Use the NuGet CLI outside of that environment, including with Visual Studio for Mac and Visual Studio Code.</span></span>

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a><span data-ttu-id="d6a66-174">Installazione di Gestione pacchetti per Visual Studio 2010 e versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="d6a66-174">Package Manager installation for Visual Studio 2010 and earlier</span></span>

<span data-ttu-id="d6a66-175">*Questi passaggi non sono necessari per Visual Studio 2012 e versioni successive, che includono già Gestione pacchetti.*</span><span class="sxs-lookup"><span data-stu-id="d6a66-175">*These steps are not necessary for Visual Studio 2012 and later, which already include the Package Manager.*</span></span>

1. <span data-ttu-id="d6a66-176">In Visual Studio 2010 e versioni precedenti, fare clic su **Strumenti > Estensioni e aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="d6a66-176">In Visual Studio 2010 and earlier, click **Tools > Extension and Updates**.</span></span>
1. <span data-ttu-id="d6a66-177">Passare a **Online**, quindi cercare "NuGet Package Manager per Visual Studio" e fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="d6a66-177">Navigate to **Online**, then search for "NuGet Package Manager for Visual Studio" and click **Download**.</span></span>
1. <span data-ttu-id="d6a66-178">Nella finestra di dialogo del programma di installazione fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="d6a66-178">In the Installer dialog box, click **Install**.</span></span>
1. <span data-ttu-id="d6a66-179">Al termine dell'installazione, riavviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d6a66-179">When installation is complete, restart Visual Studio.</span></span>

> [!Tip]
> <span data-ttu-id="d6a66-180">Se non si riesce a usare la finestra di dialogo **Estensioni e aggiornamenti** in Visual Studio (ad esempio, perché è bloccata da un proxy), è possibile scaricare le estensioni per Visual Studio 2013 e 2015 direttamente all'indirizzo [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="d6a66-180">If you're unable to use the **Extensions and Updates** dialog in Visual Studio (for example, its blocked by a proxy), you can download extensions for Visual Studio 2013 and 2015 directly at [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

### <a name="updating-the-package-manager"></a><span data-ttu-id="d6a66-181">Aggiornamento di Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="d6a66-181">Updating the Package Manager</span></span>

<span data-ttu-id="d6a66-182">Per Visual Studio 2015 Update 2 e versioni successive, Gestione pacchetti viene aggiornato automaticamente all'ultima versione stabile.</span><span class="sxs-lookup"><span data-stu-id="d6a66-182">For Visual Studio 2015 Update 2 and later, the Package Manager is automatically updated to the latest stable release.</span></span>

<span data-ttu-id="d6a66-183">Per Visual Studio 2015 Update 1 e versioni precedenti, scegliere il comando **Strumenti > Estensioni e aggiornamenti** e fare clic sulla scheda **Aggiornamenti** per vedere se è disponibile una nuova versione di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d6a66-183">For Visual Studio 2015 Update 1 and earlier, select the **Tools > Extensions and Updates** command and click on the **Updates** tab to see if a new version of the Package Manager is available.</span></span>  

### <a name="nuget-previews"></a><span data-ttu-id="d6a66-184">Versioni di anteprima di NuGet</span><span class="sxs-lookup"><span data-stu-id="d6a66-184">NuGet previews</span></span>

<span data-ttu-id="d6a66-185">Se si desidera visualizzare in anteprima le funzionalità future di NuGet, installare [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), una versione di anteprima affiancata alle versioni stabili di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d6a66-185">If you'd like to preview upcoming NuGet features, install the [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), which works side-by-side with stable releases of Visual Studio.</span></span>

<span data-ttu-id="d6a66-186">Si noti che il canale beta di NuGet precedente (`https://dotnet.myget.org/F/nuget-beta/vsix/`) per Visual Studio 2015 non viene più usato.</span><span class="sxs-lookup"><span data-stu-id="d6a66-186">Note that the previous NuGet Beta Channel (`https://dotnet.myget.org/F/nuget-beta/vsix/`) for Visual Studio 2015 is no longer used.</span></span>

<span data-ttu-id="d6a66-187">Per segnalare problemi relativi a qualsiasi versione di NuGet o per condividere idee, aprire un problema nel [repository GitHub di NuGet](https://github.com/Nuget/Home).</span><span class="sxs-lookup"><span data-stu-id="d6a66-187">To report problems with any release of NuGet or to share ideas, open an issue on the [NuGet GitHub repository](https://github.com/Nuget/Home).</span></span>

### <a name="related-topics"></a><span data-ttu-id="d6a66-188">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="d6a66-188">Related topics</span></span>

- [<span data-ttu-id="d6a66-189">Package Manager UI reference (Informazioni di riferimento sull'interfaccia utente di Gestione pacchetti)</span><span class="sxs-lookup"><span data-stu-id="d6a66-189">Package Manager UI reference</span></span>](../tools/package-manager-ui.md)
- [<span data-ttu-id="d6a66-190">Package Manager Console reference (Informazioni di riferimento sulla console di Gestione pacchetti)</span><span class="sxs-lookup"><span data-stu-id="d6a66-190">Package Manager Console reference</span></span>](../tools/package-manager-console.md)
- [<span data-ttu-id="d6a66-191">Package Manager Console PowerShell reference (Informazioni di riferimento sull'interfaccia PowerShell per la console di Gestione pacchetti)</span><span class="sxs-lookup"><span data-stu-id="d6a66-191">Package Manager Console PowerShell reference</span></span>](../tools/powershell-reference.md)