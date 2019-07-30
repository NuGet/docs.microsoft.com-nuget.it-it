---
title: Multitargeting per i pacchetti NuGet
description: Descrizione dei vari metodi per selezionare come destinazione più versioni di .NET Framework da un singolo pacchetto NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: d12b12c4670f5dcb4c1e7e475d77926bd5d3935b
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342510"
---
# <a name="support-multiple-net-versions"></a><span data-ttu-id="08533-103">Supporto di più versioni di .NET</span><span class="sxs-lookup"><span data-stu-id="08533-103">Support multiple .NET versions</span></span>

<span data-ttu-id="08533-104">Molte librerie hanno come destinazione una versione specifica di .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="08533-104">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="08533-105">Ad esempio, si potrebbe disporre di una versione della libreria specifica per UWP e di un'altra versione che sfrutta le funzionalità di .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="08533-105">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span> <span data-ttu-id="08533-106">Per risolvere questo problema, NuGet supporta l'inserimento di più versioni della stessa libreria in un singolo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="08533-106">To accommodate this, NuGet supports putting multiple versions of the same library in a single package.</span></span>

<span data-ttu-id="08533-107">Questo articolo descrive il layout di un pacchetto NuGet, indipendentemente dal modo in cui vengono creati il pacchetto o gli assembly, ovvero il layout è lo stesso se si usano più file con estensione *csproj* non di tipo SDK e un file personalizzato con estensione *nuspec* o un singolo file *csproj* di tipo SDK con più destinazioni.</span><span class="sxs-lookup"><span data-stu-id="08533-107">This article describes the layout of a NuGet package, regardless of how the package or assemblies are built (that is, the layout is the same whether using multiple non-SDK-style *.csproj* files and a custom *.nuspec* file, or a single multi-targetecd SDK-style *.csproj*).</span></span> <span data-ttu-id="08533-108">Per un progetto di tipo SDK, le [destinazioni per pack](../reference/msbuild-targets.md) di NuGet conoscono il layout previsto per il pacchetto e automatizzano l'inserimento degli assembly nelle cartelle lib corrette e la creazione dei gruppi di dipendenze per ogni framework di destinazione (TFM).</span><span class="sxs-lookup"><span data-stu-id="08533-108">For an SDK-style project, NuGet [pack targets](../reference/msbuild-targets.md) knows how the package must be layed out and automates putting the assemblies in the correct lib folders and creating dependency groups for each target framework (TFM).</span></span> <span data-ttu-id="08533-109">Per istruzioni dettagliate, vedere [Supportare più versioni di .NET Framework nel file di progetto](multiple-target-frameworks-project-file.md).</span><span class="sxs-lookup"><span data-stu-id="08533-109">For detailed instructions, see [Support multiple .NET Framework versions in your project file](multiple-target-frameworks-project-file.md).</span></span>

<span data-ttu-id="08533-110">È necessario impostare manualmente il layout del pacchetto come descritto in questo articolo quando si usa il metodo della directory di lavoro basata sulle convenzioni descritto in [Creazione di un pacchetto](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="08533-110">You must manually lay out the package as described in this article when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> <span data-ttu-id="08533-111">Per un progetto di tipo SDK, è consigliabile usare il metodo automatico, ma è anche possibile scegliere di impostare manualmente il layout del pacchetto come descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="08533-111">For an SDK-style project, the automated method is recommended, but you may also choose to manually lay out the package as described in this article.</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="08533-112">Struttura di cartelle della versione del framework</span><span class="sxs-lookup"><span data-stu-id="08533-112">Framework version folder structure</span></span>

<span data-ttu-id="08533-113">Quando si compila un pacchetto che contiene solo una versione di una libreria o che ha come destinazione più framework, si creano sempre sottocartelle in `lib` usando nomi di framework diversi con distinzione tra maiuscole e minuscole in base alla convenzione seguente:</span><span class="sxs-lookup"><span data-stu-id="08533-113">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="08533-114">Per un elenco completo dei nomi supportati, vedere le [informazioni di riferimento sui framework di destinazione](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="08533-114">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="08533-115">Non si deve mai disporre di una versione della libreria che non sia specifica di un framework e che sia inserita direttamente nella cartella `lib` radice</span><span class="sxs-lookup"><span data-stu-id="08533-115">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="08533-116">(questa funzionalità è supportata solo con `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="08533-116">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="08533-117">Così facendo, si renderebbe la libreria compatibile con qualsiasi framework di destinazione consentendone l'installazione in qualunque posizione, con probabili errori di runtime imprevisti.</span><span class="sxs-lookup"><span data-stu-id="08533-117">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="08533-118">L'aggiunta di assembly nella cartella radice (ad esempio `lib\abc.dll`) o nelle sottocartelle (ad esempio `lib\abc\abc.dll`) è deprecata e viene ignorata quando si usa il formato PackagesReference.</span><span class="sxs-lookup"><span data-stu-id="08533-118">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="08533-119">Ad esempio, la struttura di cartelle seguente supporta quattro versioni di un assembly che sono specifiche del framework:</span><span class="sxs-lookup"><span data-stu-id="08533-119">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="08533-120">Per includere facilmente tutti i file durante la compilazione del pacchetto, usare un carattere jolly `**` ricorsivo nella sezione `<files>` di `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="08533-120">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="08533-121">Cartelle specifiche dell'architettura</span><span class="sxs-lookup"><span data-stu-id="08533-121">Architecture-specific folders</span></span>

<span data-ttu-id="08533-122">Se si dispone di assembly specifici dell'architettura, vale a dire assembly distinti che hanno come destinazione ARM, x86 e x64, è necessario inserirli in una cartella denominata `runtimes` all'interno di sottocartelle denominate `{platform}-{architecture}\lib\{framework}` o `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="08533-122">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="08533-123">Ad esempio, la struttura di cartelle seguente potrebbe contenere sia DLL native che gestite che hanno come destinazione Windows 10 e il framework `uap10.0`:</span><span class="sxs-lookup"><span data-stu-id="08533-123">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

<span data-ttu-id="08533-124">Poiché questi assembly saranno disponibili solo in fase di esecuzione, per fornire l'assembly corrispondente anche in fase di compilazione, l'assembly `AnyCPU` deve essere presente nella cartella `/ref{tfm}`.</span><span class="sxs-lookup"><span data-stu-id="08533-124">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref{tfm}` folder.</span></span> 

<span data-ttu-id="08533-125">Ricordare che, poiché NuGet seleziona sempre questi asset di compilazione o di runtime da una sola cartella, se sono presenti asset compatibili in `/ref`, `/lib` non verrà considerata per l'aggiunta di assembly in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="08533-125">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="08533-126">Analogamente, se sono presenti asset compatibili in `/runtime`, `/lib` verrà ignorata anche per il runtime.</span><span class="sxs-lookup"><span data-stu-id="08533-126">Similarly, if there are some compatbile assets from `/runtime` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="08533-127">Vedere [Creare pacchetti UWP](../guides/create-uwp-packages.md) per un esempio di riferimento a questi file nel manifesto `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="08533-127">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="08533-128">Vedere anche [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2) (Creazione di un pacchetto di un componente app di Windows Store con NuGet)</span><span class="sxs-lookup"><span data-stu-id="08533-128">Also, see [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="08533-129">Corrispondenza tra le versioni di assembly e il framework di destinazione in un progetto</span><span class="sxs-lookup"><span data-stu-id="08533-129">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="08533-130">Quando NuGet installa un pacchetto che dispone di più versioni di assembly, tenta di associare il nome del framework dell'assembly con il framework di destinazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="08533-130">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="08533-131">Se non viene trovata una corrispondenza, NuGet copia l'assembly per la versione più alta inferiore o uguale al framework di destinazione del progetto, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="08533-131">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="08533-132">Se non viene trovato un assembly compatibile, NuGet restituisce un messaggio di errore appropriato.</span><span class="sxs-lookup"><span data-stu-id="08533-132">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="08533-133">Si consideri ad esempio la struttura di cartelle seguente in un pacchetto:</span><span class="sxs-lookup"><span data-stu-id="08533-133">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="08533-134">Quando si installa questo pacchetto in un progetto che ha come destinazione .NET Framework 4.6, NuGet installa l'assembly nella cartella `net45`, trattandosi della versione più alta disponibile inferiore o uguale alla versione 4.6.</span><span class="sxs-lookup"><span data-stu-id="08533-134">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="08533-135">Se il progetto ha come destinazione .NET Framework 4.6.1, invece, NuGet installa l'assembly nella cartella `net461`.</span><span class="sxs-lookup"><span data-stu-id="08533-135">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="08533-136">Se il progetto ha come destinazione .NET Framework 4.0 e versioni precedenti, NuGet genera un messaggio di errore appropriato per non avere trovato un assembly compatibile.</span><span class="sxs-lookup"><span data-stu-id="08533-136">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="08533-137">Raggruppamento di assembly per versione del framework</span><span class="sxs-lookup"><span data-stu-id="08533-137">Grouping assemblies by framework version</span></span>

<span data-ttu-id="08533-138">NuGet copia gli assembly solo da una singola cartella di libreria nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="08533-138">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="08533-139">Si supponga ad esempio che un pacchetto abbia la struttura di cartelle seguente:</span><span class="sxs-lookup"><span data-stu-id="08533-139">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="08533-140">Quando il pacchetto viene installato in un progetto che ha come destinazione .NET Framework 4.5, `MyAssembly.dll` (v2.0) è l'unico assembly installato.</span><span class="sxs-lookup"><span data-stu-id="08533-140">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="08533-141">`MyAssembly.Core.dll` (v1.0) non è installato perché non è elencato nella cartella `net45`.</span><span class="sxs-lookup"><span data-stu-id="08533-141">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="08533-142">NuGet ha questo comportamento perché `MyAssembly.Core.dll` potrebbe essere stato unito nella versione 2.0 di `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="08533-142">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="08533-143">Se si vuole che `MyAssembly.Core.dll` sia installato per .NET Framework 4.5, inserire una copia nella cartella `net45`.</span><span class="sxs-lookup"><span data-stu-id="08533-143">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="08533-144">Raggruppamento di assembly per profilo del framework</span><span class="sxs-lookup"><span data-stu-id="08533-144">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="08533-145">NuGet supporta anche la selezione di uno specifico profilo del framework come destinazione accodando un trattino e il nome del profilo alla fine della cartella.</span><span class="sxs-lookup"><span data-stu-id="08533-145">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="08533-146">I profili supportati sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="08533-146">The supported profiles are as follows:</span></span>

- <span data-ttu-id="08533-147">`client`: Client Profile</span><span class="sxs-lookup"><span data-stu-id="08533-147">`client`: Client Profile</span></span>
- <span data-ttu-id="08533-148">`full`: Full Profile</span><span class="sxs-lookup"><span data-stu-id="08533-148">`full`: Full Profile</span></span>
- <span data-ttu-id="08533-149">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="08533-149">`wp`: Windows Phone</span></span>
- <span data-ttu-id="08533-150">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="08533-150">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="08533-151">Determinazione della destinazione NuGet da usare</span><span class="sxs-lookup"><span data-stu-id="08533-151">Determining which NuGet target to use</span></span>

<span data-ttu-id="08533-152">Quando si inseriscono in un pacchetto librerie che hanno come destinazione la libreria di classi portabile, può essere difficile determinare quale destinazione NuGet usare nei nomi delle cartelle e nel file `.nuspec`, in particolare se la destinazione è solo un subset della libreria di classi portabile.</span><span class="sxs-lookup"><span data-stu-id="08533-152">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="08533-153">Le risorse esterne seguenti possono essere di aiuto:</span><span class="sxs-lookup"><span data-stu-id="08533-153">The following external resources will help you with this:</span></span>

- <span data-ttu-id="08533-154">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (Profili di framework in .NET) (stephencleary.com)</span><span class="sxs-lookup"><span data-stu-id="08533-154">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span></span>
- <span data-ttu-id="08533-155">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (Profili della libreria di classi portabile) (plnkr.co): tabella che enumera i profili della libreria di classi portabile e le destinazioni NuGet equivalenti</span><span class="sxs-lookup"><span data-stu-id="08533-155">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="08533-156">[Strumento per i profili della libreria di classi portabile](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): strumento da riga di comando per determinare i profili della libreria di classi portabile disponibili nel sistema</span><span class="sxs-lookup"><span data-stu-id="08533-156">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="08533-157">File di contenuto e script PowerShell</span><span class="sxs-lookup"><span data-stu-id="08533-157">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="08533-158">I file di contenuto modificabili e l'esecuzione degli script sono disponibili solo con il formato `packages.config`. Sono deprecati per tutti gli altri formati e non dovrebbero essere usati per i nuovi pacchetti.</span><span class="sxs-lookup"><span data-stu-id="08533-158">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="08533-159">Con `packages.config`, i file di contenuto e gli script PowerShell possono essere raggruppati per framework di destinazione usando la stessa convenzione di cartelle all'interno delle cartelle `content` e `tools`.</span><span class="sxs-lookup"><span data-stu-id="08533-159">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="08533-160">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="08533-160">For example:</span></span>

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

<span data-ttu-id="08533-161">Se una cartella framework viene lasciata vuota, NuGet non aggiunge riferimenti ad assembly o file di contenuto né esegue script PowerShell per tale framework.</span><span class="sxs-lookup"><span data-stu-id="08533-161">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="08533-162">Poiché `init.ps1` viene eseguito a livello di soluzione e indipendentemente dal progetto, deve essere inserito direttamente sotto la cartella `tools`.</span><span class="sxs-lookup"><span data-stu-id="08533-162">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="08533-163">Viene ignorato se inserito in una cartella framework.</span><span class="sxs-lookup"><span data-stu-id="08533-163">It's ignored if placed under a framework folder.</span></span>
