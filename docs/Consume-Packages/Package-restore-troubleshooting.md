---
title: Risoluzione dei problemi relativi al ripristino dei pacchetti NuGet in Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Descrizione degli errori di ripristino comuni per NuGet in Visual Studio e di come risolverli.
keywords: Ripristinare pacchetti NuGet, ripristino di pacchetti, risoluzione dei problemi, risolvere problemi
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="13766-104">Risoluzione degli errori relativi al ripristino dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="13766-104">Troubleshooting package restore errors</span></span>

<span data-ttu-id="13766-105">Questo articolo è dedicato agli errori comuni durante il ripristino dei pacchetti e alle procedure per risolverli.</span><span class="sxs-lookup"><span data-stu-id="13766-105">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="13766-106">Per informazioni dettagliate complete sul ripristino dei pacchetti, vedere [Ripristino di pacchetti](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="13766-106">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="13766-107">Se le istruzioni riportate qui non funzionano, [registrare un problema in GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) in modo che lo scenario possa essere esaminato in maggiore dettaglio.</span><span class="sxs-lookup"><span data-stu-id="13766-107">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="13766-108">Non usare il controllo "Questa pagina è stata utile?"</span><span class="sxs-lookup"><span data-stu-id="13766-108">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="13766-109">che può essere visualizzato nella pagina perché non offre la possibilità di essere contattati per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="13766-109">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="13766-110">Soluzione rapida per gli utenti di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="13766-110">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="13766-111">Se si usa Visual Studio, abilitare prima di tutto il ripristino dei pacchetti come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="13766-111">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="13766-112">In caso contrario, continuare con le sezioni successive.</span><span class="sxs-lookup"><span data-stu-id="13766-112">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="13766-113">Scegliere i comandi di menu **Strumenti > Gestione pacchetti NuGet > Impostazioni di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="13766-113">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="13766-114">Impostare entrambe le opzioni in **Ripristino pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="13766-114">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="13766-115">Scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="13766-115">Select **OK**.</span></span>
1. <span data-ttu-id="13766-116">Compilare di nuovo il progetto.</span><span class="sxs-lookup"><span data-stu-id="13766-116">Build your project again.</span></span>

![Abilitare il ripristino dei pacchetti NuGet in Strumenti/Opzioni](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="13766-118">Queste impostazioni possono essere modificate anche nel file `NuGet.config`. Vedere la sezione sul [consenso](#consent).</span><span class="sxs-lookup"><span data-stu-id="13766-118">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="13766-119">Questo progetto fa riferimento a uno o più pacchetti NuGet che non sono presenti in questo computer</span><span class="sxs-lookup"><span data-stu-id="13766-119">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="13766-120">Messaggio di errore completo:</span><span class="sxs-lookup"><span data-stu-id="13766-120">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="13766-121">Questo errore si verifica quando si tenta di compilare un progetto che contiene riferimenti a uno o più pacchetti NuGet, ma tali pacchetti non sono attualmente memorizzati nella cache nel progetto.</span><span class="sxs-lookup"><span data-stu-id="13766-121">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently cached in the project.</span></span> <span data-ttu-id="13766-122">(I pacchetti vengono memorizzati nella cache in una cartella `packages` nella radice della soluzione se il progetto usa `packages.config` oppure nel file `obj/project.assets.json`, se il progetto usa il formato PackageReference.)</span><span class="sxs-lookup"><span data-stu-id="13766-122">(Packages are cached in a `packages` folder at the solution root if the project uses `packages.config`, or in the `obj/project.assets.json` file if the project uses the PackageReference format.)</span></span>

<span data-ttu-id="13766-123">Generalmente questa situazione si verifica quando si ottiene il codice sorgente del progetto dal controllo del codice sorgente o tramite un altro download.</span><span class="sxs-lookup"><span data-stu-id="13766-123">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="13766-124">I pacchetti vengono in genere omessi dal controllo del codice sorgente o dai download perché possono essere ripristinati da feed di pacchetti come nuget.org (vedere [Pacchetti e controllo del codice sorgente](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="13766-124">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="13766-125">La loro aggiunta comporterebbe altrimenti un notevole aumento di dimensioni del repository oppure la creazione di file ZIP inutilmente grandi.</span><span class="sxs-lookup"><span data-stu-id="13766-125">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="13766-126">Usare uno dei metodi seguenti per ripristinare i pacchetti:</span><span class="sxs-lookup"><span data-stu-id="13766-126">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="13766-127">In Visual Studio abilitare il ripristino dei pacchetti. A tale scopo, selezionare il comando di menu **Strumenti > Gestione pacchetti NuGet > Impostazioni di Gestione pacchetti**, impostare entrambe le opzioni **Ripristino pacchetto** e selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="13766-127">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="13766-128">Compilare quindi di nuovo la soluzione.</span><span class="sxs-lookup"><span data-stu-id="13766-128">Then build the solution again.</span></span>
- <span data-ttu-id="13766-129">Per i progetti .NET Core, eseguire `dotnet restore` o `dotnet build` (che esegue automaticamente il ripristino).</span><span class="sxs-lookup"><span data-stu-id="13766-129">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="13766-130">Nella riga di comando eseguire `nuget restore` (ad eccezione dei progetti creati con `dotnet`, nel qual caso usare `dotnet restore`).</span><span class="sxs-lookup"><span data-stu-id="13766-130">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="13766-131">Nella riga di comando con i progetti che usano il formato PackageReference, eseguire `msbuild /t:restore`.</span><span class="sxs-lookup"><span data-stu-id="13766-131">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="13766-132">Dopo il completamento di un ripristino dovrebbe essere visibile una cartella `packages` (quando si usa`packages.config`) o il file `obj/project.assets.json` (quando si usa PackageReference).</span><span class="sxs-lookup"><span data-stu-id="13766-132">After a successful restore, you should see either a `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference).</span></span> <span data-ttu-id="13766-133">La compilazione del progetto dovrebbe ora avvenire senza problemi.</span><span class="sxs-lookup"><span data-stu-id="13766-133">The project should now build successfully.</span></span> <span data-ttu-id="13766-134">In caso contrario, [registrare un problema in GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) in modo da ottenere il necessario supporto.</span><span class="sxs-lookup"><span data-stu-id="13766-134">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="13766-135">File di asset project.assets.json non trovato</span><span class="sxs-lookup"><span data-stu-id="13766-135">Assets file project.assets.json not found</span></span>

<span data-ttu-id="13766-136">Messaggio di errore completo:</span><span class="sxs-lookup"><span data-stu-id="13766-136">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="13766-137">Questo errore si verifica per gli stessi motivi descritti nella [sezione precedente](#missing) e le soluzioni sono le stesse.</span><span class="sxs-lookup"><span data-stu-id="13766-137">This error occurs for the same reasons as explained in the [previous section](#missing), and has the same remedies.</span></span> <span data-ttu-id="13766-138">Ad esempio, l'esecuzione di `msbuild` su un progetto .NET Core ottenuto dal controllo del codice sorgente non comporterà automaticamente il ripristino dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="13766-138">For example, running `msbuild` on a .NET Core project that's been obtained from source control won't automatically restore packages.</span></span> <span data-ttu-id="13766-139">In questo caso, eseguire `msbuild /t:restore` seguito da `msbuild` oppure usare `dotnet build` (che consente di ripristinare i pacchetti automaticamente).</span><span class="sxs-lookup"><span data-stu-id="13766-139">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="13766-140">Non è possibile ripristinare uno o più pacchetti NuGet perché il consenso non è stato concesso</span><span class="sxs-lookup"><span data-stu-id="13766-140">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="13766-141">Messaggio di errore completo:</span><span class="sxs-lookup"><span data-stu-id="13766-141">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="13766-142">Questo errore indica che il ripristino dei pacchetti è disabilitato nella configurazione di NuGet.</span><span class="sxs-lookup"><span data-stu-id="13766-142">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="13766-143">È possibile modificare le impostazioni applicabili in Visual Studio, come descritto in precedenza in [Soluzione rapida per gli utenti di Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="13766-143">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="13766-144">È anche possibile modificare queste impostazioni direttamente nel file `nuget.config` applicabile (in genere `%AppData%\NuGet\NuGet.Config` in Windows e `~/.nuget/NuGet/NuGet.Config` in Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="13766-144">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="13766-145">Assicurarsi che le chiavi `enabled` e `automatic` in `packageRestore` siano impostate su True:</span><span class="sxs-lookup"><span data-stu-id="13766-145">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

<span data-ttu-id="13766-146">Si noti che se si modificano le impostazioni `packageRestore` direttamente in `nuget.config`, occorre riavviare Visual Studio per visualizzare i valori correnti nella finestra di dialogo Opzioni.</span><span class="sxs-lookup"><span data-stu-id="13766-146">Note that if you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="13766-147">Altre condizioni potenziali</span><span class="sxs-lookup"><span data-stu-id="13766-147">Other potential conditions</span></span>

- <span data-ttu-id="13766-148">Si potrebbero verificare errori di compilazione a causa di file mancanti, con un messaggio che indica di usare il ripristino NuGet per scaricarli.</span><span class="sxs-lookup"><span data-stu-id="13766-148">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="13766-149">Tuttavia, se si esegue un ripristino potrebbe essere visualizzato il messaggio "Tutti i pacchetti sono già installati. Nessun elemento da ripristinare."</span><span class="sxs-lookup"><span data-stu-id="13766-149">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="13766-150">In questo caso, eliminare la cartella `packages` (quando si usa `packages.config`) o il file `obj/project.assets.json` (quando si usa PackageReference) e ripetere il ripristino.</span><span class="sxs-lookup"><span data-stu-id="13766-150">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span>

- <span data-ttu-id="13766-151">Quando si ottiene un progetto dal controllo del codice sorgente, le cartelle di progetto potrebbero essere impostate in sola lettura.</span><span class="sxs-lookup"><span data-stu-id="13766-151">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="13766-152">Modificare le autorizzazioni delle cartelle e riprovare a ripristinare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="13766-152">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="13766-153">È possibile che sia in uso una versione precedente di NuGet.</span><span class="sxs-lookup"><span data-stu-id="13766-153">You may be using an old version of NuGet.</span></span> <span data-ttu-id="13766-154">Controllare in [nuget.org/downloads](https://www.nuget.org/downloads) per ottenere le versioni più recenti consigliate.</span><span class="sxs-lookup"><span data-stu-id="13766-154">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="13766-155">Per Visual Studio 2015 è consigliata la versione 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="13766-155">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="13766-156">Se si verificano altri problemi [registrare un problema in GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) in modo da poter fornire ulteriori dettagli su richiesta.</span><span class="sxs-lookup"><span data-stu-id="13766-156">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>