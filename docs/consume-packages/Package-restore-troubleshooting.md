---
title: Risoluzione dei problemi relativi al ripristino dei pacchetti NuGet in Visual Studio
description: Descrizione degli errori di ripristino comuni per NuGet in Visual Studio e di come risolverli.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 9f680a714717d1bde0472f2e1266cacfd8bd4d5f
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699713"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="1fd44-103">Risoluzione degli errori relativi al ripristino dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="1fd44-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="1fd44-104">Questo articolo è dedicato agli errori comuni durante il ripristino dei pacchetti e alle procedure per risolverli.</span><span class="sxs-lookup"><span data-stu-id="1fd44-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> 

<span data-ttu-id="1fd44-105">Ripristino pacchetto tenta di installare tutte le dipendenze del pacchetto nello stato corretto che corrisponde ai riferimenti al pacchetto nel file di progetto (con estensione *csproj*) o nel file *packages.config*.</span><span class="sxs-lookup"><span data-stu-id="1fd44-105">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="1fd44-106">In Visual Studio i riferimenti vengono visualizzati in Esplora soluzioni sotto le **dipendenze \ NuGet** o il nodo **riferimenti** . Per eseguire i passaggi necessari per ripristinare i pacchetti, vedere [ripristinare i pacchetti](../consume-packages/package-restore.md#restore-packages).</span><span class="sxs-lookup"><span data-stu-id="1fd44-106">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.) To follow the required steps to restore packages, see [Restore packages](../consume-packages/package-restore.md#restore-packages).</span></span> <span data-ttu-id="1fd44-107">Se i riferimenti al pacchetto nel file di progetto (con estensione *csproj*) o nel file *packages.config* non sono corretti (non corrispondono allo stato desiderato dopo il ripristino del pacchetto), è necessario installare o aggiornare i pacchetti invece di usare Ripristino pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1fd44-107">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead of using Package Restore.</span></span>

<span data-ttu-id="1fd44-108">Se le istruzioni riportate qui non funzionano, [registrare un problema in GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) in modo che lo scenario possa essere esaminato in maggiore dettaglio.</span><span class="sxs-lookup"><span data-stu-id="1fd44-108">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="1fd44-109">Non usare il controllo "Questa pagina è stata utile?"</span><span class="sxs-lookup"><span data-stu-id="1fd44-109">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="1fd44-110">che può essere visualizzato nella pagina perché non offre la possibilità di essere contattati per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="1fd44-110">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="1fd44-111">Soluzione rapida per gli utenti di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1fd44-111">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="1fd44-112">Se si usa Visual Studio, abilitare prima di tutto il ripristino dei pacchetti come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1fd44-112">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="1fd44-113">In caso contrario, continuare con le sezioni successive.</span><span class="sxs-lookup"><span data-stu-id="1fd44-113">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="1fd44-114">Scegliere i comandi di menu **Strumenti > Gestione pacchetti NuGet > Impostazioni di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="1fd44-114">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="1fd44-115">Impostare entrambe le opzioni in **Ripristino pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="1fd44-115">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="1fd44-116">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="1fd44-116">Select **OK**.</span></span>
1. <span data-ttu-id="1fd44-117">Compilare di nuovo il progetto.</span><span class="sxs-lookup"><span data-stu-id="1fd44-117">Build your project again.</span></span>

![Abilitare il ripristino dei pacchetti NuGet in Strumenti/Opzioni](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="1fd44-119">Queste impostazioni possono essere modificate anche nel file `NuGet.config`. Vedere la sezione sul [consenso](#consent).</span><span class="sxs-lookup"><span data-stu-id="1fd44-119">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span> <span data-ttu-id="1fd44-120">Se il progetto è un progetto precedente che usa il ripristino dei pacchetti integrato in MSBuild, potrebbe essere necessario [eseguire la migrazione](package-restore.md#migrate-to-automatic-package-restore-visual-studio) al ripristino dei pacchetti automatico.</span><span class="sxs-lookup"><span data-stu-id="1fd44-120">If your project is an older project that uses the MSBuild-integrated package restore, you may need to [migrate](package-restore.md#migrate-to-automatic-package-restore-visual-studio) to automatic package restore.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="1fd44-121">Questo progetto fa riferimento a uno o più pacchetti NuGet che non sono presenti in questo computer</span><span class="sxs-lookup"><span data-stu-id="1fd44-121">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="1fd44-122">Messaggio di errore completo:</span><span class="sxs-lookup"><span data-stu-id="1fd44-122">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="1fd44-123">Questo errore si verifica quando si tenta di compilare un progetto che contiene riferimenti a uno o più pacchetti NuGet, ma tali pacchetti non sono attualmente installati nel computer o nel progetto.</span><span class="sxs-lookup"><span data-stu-id="1fd44-123">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="1fd44-124">Quando si usa il formato di gestione [PackageReference](package-references-in-project-files.md) , questo errore potrebbe essere un residuo da una packages.config alla migrazione PackageReference e deve essere [rimosso manualmente](../resources/NuGet-FAQ.md#working-with-packages) dal file di progetto.</span><span class="sxs-lookup"><span data-stu-id="1fd44-124">When using the [PackageReference](package-references-in-project-files.md) management format, this error might be a leftover from a packages.config to PackageReference migration and needs to be [manually removed](../resources/NuGet-FAQ.md#working-with-packages) from the project file.</span></span>
- <span data-ttu-id="1fd44-125">Quando si usa [packages.config](../reference/packages-config.md), questo errore indica che il pacchetto non è installato nella cartella `packages` nella radice della soluzione.</span><span class="sxs-lookup"><span data-stu-id="1fd44-125">When using [packages.config](../reference/packages-config.md), the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="1fd44-126">Generalmente questa situazione si verifica quando si ottiene il codice sorgente del progetto dal controllo del codice sorgente o tramite un altro download.</span><span class="sxs-lookup"><span data-stu-id="1fd44-126">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="1fd44-127">I pacchetti vengono in genere omessi dal controllo del codice sorgente o dai download perché possono essere ripristinati da feed di pacchetti come nuget.org (vedere [Pacchetti e controllo del codice sorgente](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="1fd44-127">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="1fd44-128">La loro aggiunta comporterebbe altrimenti un notevole aumento di dimensioni del repository oppure la creazione di file ZIP inutilmente grandi.</span><span class="sxs-lookup"><span data-stu-id="1fd44-128">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="1fd44-129">L'errore può verificarsi anche se il file di progetto contiene percorsi assoluti ai percorsi dei pacchetti e il progetto viene spostato.</span><span class="sxs-lookup"><span data-stu-id="1fd44-129">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="1fd44-130">Usare uno dei metodi seguenti per ripristinare i pacchetti:</span><span class="sxs-lookup"><span data-stu-id="1fd44-130">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="1fd44-131">Se è stato spostato il file di progetto, modificare il file direttamente per aggiornare i riferimenti ai pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1fd44-131">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="1fd44-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([ripristino automatico](package-restore.md#restore-packages-automatically-using-visual-studio) o [ripristino manuale](package-restore.md#restore-packages-manually-using-visual-studio))</span><span class="sxs-lookup"><span data-stu-id="1fd44-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([automatic restore](package-restore.md#restore-packages-automatically-using-visual-studio) or [manual restore](package-restore.md#restore-packages-manually-using-visual-studio))</span></span>
- [<span data-ttu-id="1fd44-133">Interfaccia della riga di comando di dotnet</span><span class="sxs-lookup"><span data-stu-id="1fd44-133">dotnet CLI</span></span>](package-restore.md#restore-using-the-dotnet-cli)
- [<span data-ttu-id="1fd44-134">Interfaccia della riga di comando di nuget.exe</span><span class="sxs-lookup"><span data-stu-id="1fd44-134">nuget.exe CLI</span></span>](package-restore.md#restore-using-the-nugetexe-cli)
- [<span data-ttu-id="1fd44-135">MSBuild</span><span class="sxs-lookup"><span data-stu-id="1fd44-135">MSBuild</span></span>](package-restore.md#restore-using-msbuild)
- [<span data-ttu-id="1fd44-136">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="1fd44-136">Azure Pipelines</span></span>](package-restore.md#restore-using-azure-pipelines)
- [<span data-ttu-id="1fd44-137">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="1fd44-137">Azure DevOps Server</span></span>](package-restore.md#restore-using-azure-devops-server)

<span data-ttu-id="1fd44-138">Dopo un ripristino corretto, il pacchetto deve essere presente nella cartella *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="1fd44-138">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="1fd44-139">Per i progetti che usano PackageReference, un ripristino deve ricreare il file `obj/project.assets.json`. Per i progetti che usano `packages.config`, il pacchetto deve essere visualizzato nella cartella `packages` del progetto.</span><span class="sxs-lookup"><span data-stu-id="1fd44-139">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="1fd44-140">La compilazione del progetto dovrebbe ora avvenire senza problemi.</span><span class="sxs-lookup"><span data-stu-id="1fd44-140">The project should now build successfully.</span></span> <span data-ttu-id="1fd44-141">In caso contrario, [registrare un problema in GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) in modo da ottenere il necessario supporto.</span><span class="sxs-lookup"><span data-stu-id="1fd44-141">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="1fd44-142">File di asset project.assets.json non trovato</span><span class="sxs-lookup"><span data-stu-id="1fd44-142">Assets file project.assets.json not found</span></span>

<span data-ttu-id="1fd44-143">Messaggio di errore completo:</span><span class="sxs-lookup"><span data-stu-id="1fd44-143">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="1fd44-144">Il file `project.assets.json` gestisce un grafico delle dipendenze del progetto quando si usa il formato di gestione PackageReference, che consente di assicurarsi che tutti i pacchetti necessari siano installati nel computer.</span><span class="sxs-lookup"><span data-stu-id="1fd44-144">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="1fd44-145">Dato che questo file viene generato in modo dinamico tramite il ripristino del pacchetto, in genere non viene aggiunto al controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="1fd44-145">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="1fd44-146">Di conseguenza, questo errore si verifica quando si compila un progetto con uno strumento, ad esempio `msbuild`, che non ripristina automaticamente i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1fd44-146">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="1fd44-147">In questo caso, eseguire `msbuild -t:restore` seguito da `msbuild` oppure usare `dotnet build` (che consente di ripristinare i pacchetti automaticamente).</span><span class="sxs-lookup"><span data-stu-id="1fd44-147">In this case, run `msbuild -t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="1fd44-148">È anche possibile usare uno dei metodi di ripristino dei pacchetti nella [sezione precedente](#missing).</span><span class="sxs-lookup"><span data-stu-id="1fd44-148">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="1fd44-149">Non è possibile ripristinare uno o più pacchetti NuGet perché il consenso non è stato concesso</span><span class="sxs-lookup"><span data-stu-id="1fd44-149">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="1fd44-150">Messaggio di errore completo:</span><span class="sxs-lookup"><span data-stu-id="1fd44-150">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="1fd44-151">Questo errore indica che il ripristino dei pacchetti è disabilitato nella configurazione di NuGet.</span><span class="sxs-lookup"><span data-stu-id="1fd44-151">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="1fd44-152">È possibile modificare le impostazioni applicabili in Visual Studio, come descritto in precedenza in [Soluzione rapida per gli utenti di Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="1fd44-152">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="1fd44-153">È anche possibile modificare queste impostazioni direttamente nel file `nuget.config` applicabile (in genere `%AppData%\NuGet\NuGet.Config` in Windows e `~/.nuget/NuGet/NuGet.Config` in Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="1fd44-153">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="1fd44-154">Assicurarsi che le chiavi `enabled` e `automatic` in `packageRestore` siano impostate su True:</span><span class="sxs-lookup"><span data-stu-id="1fd44-154">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> <span data-ttu-id="1fd44-155">Se si modificano le impostazioni `packageRestore` direttamente in `nuget.config`, riavviare Visual Studio per visualizzare i valori correnti nella finestra di dialogo Opzioni.</span><span class="sxs-lookup"><span data-stu-id="1fd44-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="1fd44-156">Altre condizioni potenziali</span><span class="sxs-lookup"><span data-stu-id="1fd44-156">Other potential conditions</span></span>

- <span data-ttu-id="1fd44-157">Si potrebbero verificare errori di compilazione a causa di file mancanti, con un messaggio che indica di usare il ripristino NuGet per scaricarli.</span><span class="sxs-lookup"><span data-stu-id="1fd44-157">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="1fd44-158">Tuttavia, se si esegue un ripristino potrebbe essere visualizzato il messaggio "Tutti i pacchetti sono già installati. Nessun elemento da ripristinare."</span><span class="sxs-lookup"><span data-stu-id="1fd44-158">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="1fd44-159">In questo caso, eliminare la cartella `packages` (quando si usa `packages.config`) o il file `obj/project.assets.json` (quando si usa PackageReference) e ripetere il ripristino.</span><span class="sxs-lookup"><span data-stu-id="1fd44-159">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="1fd44-160">Se l'errore persiste, usare `nuget locals all -clear` o `dotnet nuget locals all --clear` dalla riga di comando per cancellare le cartelle *global-packages* e della cache come descritto in [Gestione dei pacchetti globali e delle cartelle della cache](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="1fd44-160">If the error still persists, use `nuget locals all -clear` or `dotnet nuget locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="1fd44-161">Quando si ottiene un progetto dal controllo del codice sorgente, le cartelle di progetto potrebbero essere impostate in sola lettura.</span><span class="sxs-lookup"><span data-stu-id="1fd44-161">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="1fd44-162">Modificare le autorizzazioni delle cartelle e riprovare a ripristinare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1fd44-162">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="1fd44-163">È possibile che sia in uso una versione precedente di NuGet.</span><span class="sxs-lookup"><span data-stu-id="1fd44-163">You may be using an old version of NuGet.</span></span> <span data-ttu-id="1fd44-164">Controllare in [nuget.org/downloads](https://www.nuget.org/downloads) per ottenere le versioni più recenti consigliate.</span><span class="sxs-lookup"><span data-stu-id="1fd44-164">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="1fd44-165">Per Visual Studio 2015 è consigliata la versione 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="1fd44-165">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="1fd44-166">Se si verificano altri problemi [registrare un problema in GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) in modo da poter fornire ulteriori dettagli su richiesta.</span><span class="sxs-lookup"><span data-stu-id="1fd44-166">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
