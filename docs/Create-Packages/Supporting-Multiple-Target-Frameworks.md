---
title: Multitargeting per i pacchetti NuGet
description: Descrizione dei vari metodi per selezionare come destinazione più versioni di .NET Framework da un singolo pacchetto NuGet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 09/27/2017
ms.topic: conceptual
ms.openlocfilehash: d1a64c61954381b7ab3a7ecc8aa5a812cfa14e8b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="supporting-multiple-net-framework-versions"></a><span data-ttu-id="db382-103">Supporto di più versioni di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="db382-103">Supporting multiple .NET framework versions</span></span>

<span data-ttu-id="db382-104">*Per i progetti .NET Core che usano NuGet 4.0+, vedere [Pack e restore di NuGet come destinazioni MSBuild](../reference/msbuild-targets.md) per informazioni dettagliate sul crosstargeting.*</span><span class="sxs-lookup"><span data-stu-id="db382-104">*For .NET Core projects using NuGet 4.0+, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) for details on cross-targeting.*</span></span>

<span data-ttu-id="db382-105">Molte librerie hanno come destinazione una versione specifica di .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="db382-105">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="db382-106">Ad esempio, si potrebbe disporre di una versione della libreria specifica per UWP e di un'altra versione che sfrutta le funzionalità di .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="db382-106">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span>

<span data-ttu-id="db382-107">Per far fronte a questa situazione, NuGet supporta l'inserimento di più versioni della stessa libreria in un singolo pacchetto quando si usa il metodo della directory di lavoro basata su convenzioni descritto in [Creazione di un pacchetto](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="db382-107">To accommodate this, NuGet supports putting multiple versions of the same library in a single package when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="db382-108">Struttura di cartelle della versione del framework</span><span class="sxs-lookup"><span data-stu-id="db382-108">Framework version folder structure</span></span>

<span data-ttu-id="db382-109">Quando si compila un pacchetto che contiene solo una versione di una libreria o che ha come destinazione più framework, si creano sempre sottocartelle in `lib` usando nomi di framework diversi con distinzione tra maiuscole e minuscole in base alla convenzione seguente:</span><span class="sxs-lookup"><span data-stu-id="db382-109">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="db382-110">Per un elenco completo dei nomi supportati, vedere le [informazioni di riferimento sui framework di destinazione](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="db382-110">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="db382-111">Non si deve mai disporre di una versione della libreria che non sia specifica di un framework e che sia inserita direttamente nella cartella `lib` radice</span><span class="sxs-lookup"><span data-stu-id="db382-111">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="db382-112">(questa funzionalità è supportata solo con `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="db382-112">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="db382-113">Così facendo, la si renderebbe compatibile con qualsiasi framework di destinazione consentendone l'installazione in qualunque posizione, comportando probabilmente errori di runtime imprevisti.</span><span class="sxs-lookup"><span data-stu-id="db382-113">Doing so would make the compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="db382-114">L'aggiunta di assembly nella cartella radice (ad esempio `lib\abc.dll`) o nelle sottocartelle (ad esempio `lib\abc\abc.dll`) è deprecata e viene ignorata quando si usa il formato PackagesReference.</span><span class="sxs-lookup"><span data-stu-id="db382-114">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="db382-115">Ad esempio, la struttura di cartelle seguente supporta quattro versioni di un assembly che sono specifiche del framework:</span><span class="sxs-lookup"><span data-stu-id="db382-115">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="db382-116">Per includere facilmente tutti i file durante la compilazione del pacchetto, usare un carattere jolly `**` ricorsivo nella sezione `<files>` di `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="db382-116">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="db382-117">Cartelle specifiche dell'architettura</span><span class="sxs-lookup"><span data-stu-id="db382-117">Architecture-specific folders</span></span>

<span data-ttu-id="db382-118">Se si dispone di assembly specifici dell'architettura, vale a dire assembly distinti che hanno come destinazione ARM, x86 e x64, è necessario inserirli in una cartella denominata `runtimes` all'interno di sottocartelle denominate `{platform}-{architecture}\lib\{framework}` o `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="db382-118">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="db382-119">Ad esempio, la struttura di cartelle seguente potrebbe contenere sia DLL native che gestite che hanno come destinazione Windows 10 e il framework `uap10.0`:</span><span class="sxs-lookup"><span data-stu-id="db382-119">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="db382-120">Vedere [Creare pacchetti UWP](../guides/create-uwp-packages.md) per un esempio di riferimento a questi file nel manifesto `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="db382-120">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="db382-121">Corrispondenza tra le versioni di assembly e il framework di destinazione in un progetto</span><span class="sxs-lookup"><span data-stu-id="db382-121">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="db382-122">Quando NuGet installa un pacchetto che dispone di più versioni di assembly, tenta di associare il nome del framework dell'assembly con il framework di destinazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="db382-122">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="db382-123">Se non viene trovata una corrispondenza, NuGet copia l'assembly per la versione più alta inferiore o uguale al framework di destinazione del progetto, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="db382-123">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="db382-124">Se non viene trovato un assembly compatibile, NuGet restituisce un messaggio di errore appropriato.</span><span class="sxs-lookup"><span data-stu-id="db382-124">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="db382-125">Si consideri ad esempio la struttura di cartelle seguente in un pacchetto:</span><span class="sxs-lookup"><span data-stu-id="db382-125">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="db382-126">Quando si installa questo pacchetto in un progetto che ha come destinazione .NET Framework 4.6, NuGet installa l'assembly nella cartella `net45`, trattandosi della versione più alta disponibile inferiore o uguale alla versione 4.6.</span><span class="sxs-lookup"><span data-stu-id="db382-126">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="db382-127">Se il progetto ha come destinazione .NET Framework 4.6.1, invece, NuGet installa l'assembly nella cartella `net461`.</span><span class="sxs-lookup"><span data-stu-id="db382-127">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="db382-128">Se il progetto ha come destinazione .NET Framework 4.0 e versioni precedenti, NuGet genera un messaggio di errore appropriato per non avere trovato un assembly compatibile.</span><span class="sxs-lookup"><span data-stu-id="db382-128">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="db382-129">Raggruppamento di assembly per versione del framework</span><span class="sxs-lookup"><span data-stu-id="db382-129">Grouping assemblies by framework version</span></span>

<span data-ttu-id="db382-130">NuGet copia gli assembly solo da una singola cartella di libreria nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="db382-130">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="db382-131">Si supponga ad esempio che un pacchetto abbia la struttura di cartelle seguente:</span><span class="sxs-lookup"><span data-stu-id="db382-131">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="db382-132">Quando il pacchetto viene installato in un progetto che ha come destinazione .NET Framework 4.5, `MyAssembly.dll` (v2.0) è l'unico assembly installato.</span><span class="sxs-lookup"><span data-stu-id="db382-132">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="db382-133">`MyAssembly.Core.dll` (v1.0) non è installato perché non è elencato nella cartella `net45`.</span><span class="sxs-lookup"><span data-stu-id="db382-133">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="db382-134">NuGet ha questo comportamento perché `MyAssembly.Core.dll` potrebbe essere stato unito nella versione 2.0 di `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="db382-134">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="db382-135">Se si vuole che `MyAssembly.Core.dll` sia installato per .NET Framework 4.5, inserire una copia nella cartella `net45`.</span><span class="sxs-lookup"><span data-stu-id="db382-135">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="db382-136">Raggruppamento di assembly per profilo del framework</span><span class="sxs-lookup"><span data-stu-id="db382-136">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="db382-137">NuGet supporta anche la selezione di uno specifico profilo del framework come destinazione accodando un trattino e il nome del profilo alla fine della cartella.</span><span class="sxs-lookup"><span data-stu-id="db382-137">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="db382-138">I profili supportati sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="db382-138">The supported profiles are as follows:</span></span>

- <span data-ttu-id="db382-139">`client`: Client Profile</span><span class="sxs-lookup"><span data-stu-id="db382-139">`client`: Client Profile</span></span>
- <span data-ttu-id="db382-140">`full`: Full Profile</span><span class="sxs-lookup"><span data-stu-id="db382-140">`full`: Full Profile</span></span>
- <span data-ttu-id="db382-141">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="db382-141">`wp`: Windows Phone</span></span>
- <span data-ttu-id="db382-142">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="db382-142">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="db382-143">Determinazione della destinazione NuGet da usare</span><span class="sxs-lookup"><span data-stu-id="db382-143">Determining which NuGet target to use</span></span>

<span data-ttu-id="db382-144">Quando si inseriscono in un pacchetto librerie che hanno come destinazione la libreria di classi portabile, può essere difficile determinare quale destinazione NuGet usare nei nomi delle cartelle e nel file `.nuspec`, in particolare se la destinazione è solo un subset della libreria di classi portabile.</span><span class="sxs-lookup"><span data-stu-id="db382-144">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="db382-145">Le risorse esterne seguenti possono essere di aiuto:</span><span class="sxs-lookup"><span data-stu-id="db382-145">The following external resources will help you with this:</span></span>

- <span data-ttu-id="db382-146">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (Profili di framework in .NET) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="db382-146">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span></span>
- <span data-ttu-id="db382-147">[Profili della libreria di classi portabile](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): tabella che enumera i profili della libreria di classi portabile e le destinazioni NuGet equivalenti</span><span class="sxs-lookup"><span data-stu-id="db382-147">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="db382-148">[Strumento per i profili della libreria di classi portabile](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): strumento da riga di comando per determinare i profili della libreria di classi portabile disponibili nel sistema</span><span class="sxs-lookup"><span data-stu-id="db382-148">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="db382-149">File di contenuto e script PowerShell</span><span class="sxs-lookup"><span data-stu-id="db382-149">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="db382-150">I file di contenuto modificabili e l'esecuzione degli script sono disponibili solo con il formato `packages.config`. Sono deprecati per tutti gli altri formati e non dovrebbero essere usati per i nuovi pacchetti.</span><span class="sxs-lookup"><span data-stu-id="db382-150">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="db382-151">Con `packages.config`, i file di contenuto e gli script PowerShell possono essere raggruppati per framework di destinazione usando la stessa convenzione di cartelle all'interno delle cartelle `content` e `tools`.</span><span class="sxs-lookup"><span data-stu-id="db382-151">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="db382-152">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="db382-152">For example:</span></span>

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

<span data-ttu-id="db382-153">Se una cartella framework viene lasciata vuota, NuGet non aggiunge riferimenti ad assembly o file di contenuto né esegue script PowerShell per tale framework.</span><span class="sxs-lookup"><span data-stu-id="db382-153">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="db382-154">Poiché `init.ps1` viene eseguito a livello di soluzione e indipendentemente dal progetto, deve essere inserito direttamente sotto la cartella `tools`.</span><span class="sxs-lookup"><span data-stu-id="db382-154">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="db382-155">Viene ignorato se inserito in una cartella framework.</span><span class="sxs-lookup"><span data-stu-id="db382-155">It's ignored if placed under a framework folder.</span></span>
