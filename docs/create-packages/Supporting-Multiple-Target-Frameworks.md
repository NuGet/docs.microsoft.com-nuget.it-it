---
title: Multitargeting per i pacchetti NuGet
description: Descrizione dei vari metodi per selezionare come destinazione più versioni di .NET Framework da un singolo pacchetto NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 4413779361dad3a650da36b3c69bbb55b62804ee
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380738"
---
# <a name="support-multiple-net-versions"></a><span data-ttu-id="ff4f1-103">Supporto di più versioni di .NET</span><span class="sxs-lookup"><span data-stu-id="ff4f1-103">Support multiple .NET versions</span></span>

<span data-ttu-id="ff4f1-104">Molte librerie hanno come destinazione una versione specifica di .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-104">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="ff4f1-105">Ad esempio, si potrebbe disporre di una versione della libreria specifica per UWP e di un'altra versione che sfrutta le funzionalità di .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-105">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span> <span data-ttu-id="ff4f1-106">Per risolvere questo problema, NuGet supporta l'inserimento di più versioni della stessa libreria in un singolo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-106">To accommodate this, NuGet supports putting multiple versions of the same library in a single package.</span></span>

<span data-ttu-id="ff4f1-107">Questo articolo descrive il layout di un pacchetto NuGet, indipendentemente dalla modalità di compilazione del pacchetto o degli assembly (ovvero, il layout è lo stesso se si usano più file con *estensione csproj* non SDK e un file con *estensione NuSpec* personalizzato o una singola SDK-Style *. csproj*).</span><span class="sxs-lookup"><span data-stu-id="ff4f1-107">This article describes the layout of a NuGet package, regardless of how the package or assemblies are built (that is, the layout is the same whether using multiple non-SDK-style *.csproj* files and a custom *.nuspec* file, or a single multi-targeted SDK-style *.csproj*).</span></span> <span data-ttu-id="ff4f1-108">Per un progetto di tipo SDK, le [destinazioni per pack](../reference/msbuild-targets.md) di NuGet conoscono il layout previsto per il pacchetto e automatizzano l'inserimento degli assembly nelle cartelle lib corrette e la creazione dei gruppi di dipendenze per ogni framework di destinazione (TFM).</span><span class="sxs-lookup"><span data-stu-id="ff4f1-108">For an SDK-style project, NuGet [pack targets](../reference/msbuild-targets.md) knows how the package must be layed out and automates putting the assemblies in the correct lib folders and creating dependency groups for each target framework (TFM).</span></span> <span data-ttu-id="ff4f1-109">Per istruzioni dettagliate, vedere [Supportare più versioni di .NET Framework nel file di progetto](multiple-target-frameworks-project-file.md).</span><span class="sxs-lookup"><span data-stu-id="ff4f1-109">For detailed instructions, see [Support multiple .NET Framework versions in your project file](multiple-target-frameworks-project-file.md).</span></span>

<span data-ttu-id="ff4f1-110">È necessario impostare manualmente il layout del pacchetto come descritto in questo articolo quando si usa il metodo della directory di lavoro basata sulle convenzioni descritto in [Creazione di un pacchetto](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="ff4f1-110">You must manually lay out the package as described in this article when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> <span data-ttu-id="ff4f1-111">Per un progetto di tipo SDK, è consigliabile usare il metodo automatico, ma è anche possibile scegliere di impostare manualmente il layout del pacchetto come descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-111">For an SDK-style project, the automated method is recommended, but you may also choose to manually lay out the package as described in this article.</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="ff4f1-112">Struttura di cartelle della versione del framework</span><span class="sxs-lookup"><span data-stu-id="ff4f1-112">Framework version folder structure</span></span>

<span data-ttu-id="ff4f1-113">Quando si compila un pacchetto che contiene solo una versione di una libreria o che ha come destinazione più framework, si creano sempre sottocartelle in `lib` usando nomi di framework diversi con distinzione tra maiuscole e minuscole in base alla convenzione seguente:</span><span class="sxs-lookup"><span data-stu-id="ff4f1-113">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="ff4f1-114">Per un elenco completo dei nomi supportati, vedere le [informazioni di riferimento sui framework di destinazione](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="ff4f1-114">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="ff4f1-115">Non si deve mai disporre di una versione della libreria che non sia specifica di un framework e che sia inserita direttamente nella cartella `lib` radice</span><span class="sxs-lookup"><span data-stu-id="ff4f1-115">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="ff4f1-116">(questa funzionalità è supportata solo con `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="ff4f1-116">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="ff4f1-117">Così facendo, si renderebbe la libreria compatibile con qualsiasi framework di destinazione consentendone l'installazione in qualunque posizione, con probabili errori di runtime imprevisti.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-117">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="ff4f1-118">L'aggiunta di assembly nella cartella radice (ad esempio `lib\abc.dll`) o nelle sottocartelle (ad esempio `lib\abc\abc.dll`) è deprecata e viene ignorata quando si usa il formato PackagesReference.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-118">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="ff4f1-119">Ad esempio, la struttura di cartelle seguente supporta quattro versioni di un assembly che sono specifiche del framework:</span><span class="sxs-lookup"><span data-stu-id="ff4f1-119">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="ff4f1-120">Per includere facilmente tutti i file durante la compilazione del pacchetto, usare un carattere jolly `**` ricorsivo nella sezione `<files>` di `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="ff4f1-120">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="ff4f1-121">Cartelle specifiche dell'architettura</span><span class="sxs-lookup"><span data-stu-id="ff4f1-121">Architecture-specific folders</span></span>

<span data-ttu-id="ff4f1-122">Se si dispone di assembly specifici dell'architettura, vale a dire assembly distinti che hanno come destinazione ARM, x86 e x64, è necessario inserirli in una cartella denominata `runtimes` all'interno di sottocartelle denominate `{platform}-{architecture}\lib\{framework}` o `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-122">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="ff4f1-123">Ad esempio, la struttura di cartelle seguente potrebbe contenere sia DLL native che gestite che hanno come destinazione Windows 10 e il framework `uap10.0`:</span><span class="sxs-lookup"><span data-stu-id="ff4f1-123">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="ff4f1-124">Poiché questi assembly saranno disponibili solo in fase di esecuzione, per fornire l'assembly corrispondente anche in fase di compilazione, l'assembly `AnyCPU` deve essere presente nella cartella `/ref/{tfm}`.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-124">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref/{tfm}` folder.</span></span> 

<span data-ttu-id="ff4f1-125">Ricordare che, poiché NuGet seleziona sempre questi asset di compilazione o di runtime da una sola cartella, se sono presenti asset compatibili in `/ref`, `/lib` non verrà considerata per l'aggiunta di assembly in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-125">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="ff4f1-126">Analogamente, se sono presenti alcune risorse compatibili da `/runtime`, anche `/lib` verranno ignorate per il Runtime.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-126">Similarly, if there are some compatible assets from `/runtime` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="ff4f1-127">Vedere [Creare pacchetti UWP](../guides/create-uwp-packages.md) per un esempio di riferimento a questi file nel manifesto `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-127">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="ff4f1-128">Vedere anche [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2) (Creazione di un pacchetto di un componente app di Windows Store con NuGet)</span><span class="sxs-lookup"><span data-stu-id="ff4f1-128">Also, see [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="ff4f1-129">Corrispondenza tra le versioni di assembly e il framework di destinazione in un progetto</span><span class="sxs-lookup"><span data-stu-id="ff4f1-129">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="ff4f1-130">Quando NuGet installa un pacchetto che dispone di più versioni di assembly, tenta di associare il nome del framework dell'assembly con il framework di destinazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-130">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="ff4f1-131">Se non viene trovata una corrispondenza, NuGet copia l'assembly per la versione più alta inferiore o uguale al framework di destinazione del progetto, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-131">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="ff4f1-132">Se non viene trovato un assembly compatibile, NuGet restituisce un messaggio di errore appropriato.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-132">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="ff4f1-133">Si consideri ad esempio la struttura di cartelle seguente in un pacchetto:</span><span class="sxs-lookup"><span data-stu-id="ff4f1-133">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="ff4f1-134">Quando si installa questo pacchetto in un progetto che ha come destinazione .NET Framework 4.6, NuGet installa l'assembly nella cartella `net45`, trattandosi della versione più alta disponibile inferiore o uguale alla versione 4.6.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-134">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="ff4f1-135">Se il progetto ha come destinazione .NET Framework 4.6.1, invece, NuGet installa l'assembly nella cartella `net461`.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-135">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="ff4f1-136">Se il progetto ha come destinazione .NET Framework 4.0 e versioni precedenti, NuGet genera un messaggio di errore appropriato per non avere trovato un assembly compatibile.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-136">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="ff4f1-137">Raggruppamento di assembly per versione del framework</span><span class="sxs-lookup"><span data-stu-id="ff4f1-137">Grouping assemblies by framework version</span></span>

<span data-ttu-id="ff4f1-138">NuGet copia gli assembly solo da una singola cartella di libreria nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-138">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="ff4f1-139">Si supponga ad esempio che un pacchetto abbia la struttura di cartelle seguente:</span><span class="sxs-lookup"><span data-stu-id="ff4f1-139">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="ff4f1-140">Quando il pacchetto viene installato in un progetto che ha come destinazione .NET Framework 4.5, `MyAssembly.dll` (v2.0) è l'unico assembly installato.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-140">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="ff4f1-141">`MyAssembly.Core.dll` (v1.0) non è installato perché non è elencato nella cartella `net45`.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-141">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="ff4f1-142">NuGet ha questo comportamento perché `MyAssembly.Core.dll` potrebbe essere stato unito nella versione 2.0 di `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-142">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="ff4f1-143">Se si vuole che `MyAssembly.Core.dll` sia installato per .NET Framework 4.5, inserire una copia nella cartella `net45`.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-143">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="ff4f1-144">Raggruppamento di assembly per profilo del framework</span><span class="sxs-lookup"><span data-stu-id="ff4f1-144">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="ff4f1-145">NuGet supporta anche la selezione di uno specifico profilo del framework come destinazione accodando un trattino e il nome del profilo alla fine della cartella.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-145">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="ff4f1-146">I profili supportati sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="ff4f1-146">The supported profiles are as follows:</span></span>

- <span data-ttu-id="ff4f1-147">`client`: Client Profile</span><span class="sxs-lookup"><span data-stu-id="ff4f1-147">`client`: Client Profile</span></span>
- <span data-ttu-id="ff4f1-148">`full`: Full Profile</span><span class="sxs-lookup"><span data-stu-id="ff4f1-148">`full`: Full Profile</span></span>
- <span data-ttu-id="ff4f1-149">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="ff4f1-149">`wp`: Windows Phone</span></span>
- <span data-ttu-id="ff4f1-150">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="ff4f1-150">`cf`: Compact Framework</span></span>

## <a name="declaring-dependencies-advanced"></a><span data-ttu-id="ff4f1-151">Dichiarazione delle dipendenze (scenari avanzati)</span><span class="sxs-lookup"><span data-stu-id="ff4f1-151">Declaring dependencies (Advanced)</span></span>

<span data-ttu-id="ff4f1-152">Quando si crea un pacchetto per il file di progetto, NuGet tenta di generare automaticamente le dipendenze dal progetto.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-152">When packing a project file, NuGet tries to automatically generate the dependencies from the project.</span></span> <span data-ttu-id="ff4f1-153">Le informazioni contenute in questa sezione sull'uso di un file con estensione *nuspec* per dichiarare le dipendenze sono in genere necessarie solo per gli scenari avanzati.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-153">The information in this section about using a *.nuspec* file to declare dependencies is typically necessary for advanced scenarios only.</span></span>

<span data-ttu-id="ff4f1-154">*(Versione 2.0 +)* È possibile dichiarare le dipendenze del pacchetto nel file *nuspec* corrispondente al framework di destinazione del progetto di destinazione usando elementi `<group>` all'interno dell'elemento `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-154">*(Version 2.0+)* You can declare package dependencies in the *.nuspec* corresponding to the target framework of the target project using `<group>` elements within the `<dependencies>` element.</span></span> <span data-ttu-id="ff4f1-155">Per altre informazioni, vedere [Elemento dependencies](../reference/nuspec.md#dependencies-element).</span><span class="sxs-lookup"><span data-stu-id="ff4f1-155">For more information, see [dependencies element](../reference/nuspec.md#dependencies-element).</span></span>

<span data-ttu-id="ff4f1-156">Ogni gruppo ha un attributo denominato `targetFramework` e contiene zero o più elementi `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-156">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="ff4f1-157">Tali dipendenze vengono installate insieme quando il framework di destinazione è compatibile con il profilo di framework del progetto.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-157">Those dependencies are installed together when the target framework is compatible with the project's framework profile.</span></span> <span data-ttu-id="ff4f1-158">Vedere [Framework di destinazione](../reference/target-frameworks.md) per gli identificatori di framework esatti.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-158">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

<span data-ttu-id="ff4f1-159">Si consiglia di usare un gruppo per ogni moniker framework di destinazione (TFM) per i file nelle cartelle *lib/* e *ref/* .</span><span class="sxs-lookup"><span data-stu-id="ff4f1-159">We recommend using one group per Target Framework Moniker (TFM) for files in the *lib/* and *ref/* folders.</span></span>

<span data-ttu-id="ff4f1-160">L'esempio seguente mostra variazioni diverse dell'elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="ff4f1-160">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>

    <group targetFramework="net472">
        <dependency id="jQuery" version="1.10.2" />
        <dependency id="WebActivatorEx" version="2.2.0" />
    </group>

    <group targetFramework="net20">
    </group>

</dependencies>
```

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="ff4f1-161">Determinazione della destinazione NuGet da usare</span><span class="sxs-lookup"><span data-stu-id="ff4f1-161">Determining which NuGet target to use</span></span>

<span data-ttu-id="ff4f1-162">Quando si inseriscono in un pacchetto librerie che hanno come destinazione la libreria di classi portabile, può essere difficile determinare quale destinazione NuGet usare nei nomi delle cartelle e nel file `.nuspec`, in particolare se la destinazione è solo un subset della libreria di classi portabile.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-162">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="ff4f1-163">Le risorse esterne seguenti possono essere di aiuto:</span><span class="sxs-lookup"><span data-stu-id="ff4f1-163">The following external resources will help you with this:</span></span>

- <span data-ttu-id="ff4f1-164">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (Profili di framework in .NET) (stephencleary.com)</span><span class="sxs-lookup"><span data-stu-id="ff4f1-164">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span></span>
- <span data-ttu-id="ff4f1-165">[Profili della libreria di classi portabile](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): tabella che enumera i profili della libreria di classi portabile e le destinazioni NuGet equivalenti</span><span class="sxs-lookup"><span data-stu-id="ff4f1-165">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="ff4f1-166">[Strumento per i profili della libreria di classi portabile](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): strumento da riga di comando per determinare i profili della libreria di classi portabile disponibili nel sistema</span><span class="sxs-lookup"><span data-stu-id="ff4f1-166">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="ff4f1-167">File di contenuto e script PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff4f1-167">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="ff4f1-168">I file di contenuto modificabili e l'esecuzione degli script sono disponibili solo con il formato `packages.config`. Sono deprecati per tutti gli altri formati e non dovrebbero essere usati per i nuovi pacchetti.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-168">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="ff4f1-169">Con `packages.config`, i file di contenuto e gli script PowerShell possono essere raggruppati per framework di destinazione usando la stessa convenzione di cartelle all'interno delle cartelle `content` e `tools`.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-169">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="ff4f1-170">Esempio:</span><span class="sxs-lookup"><span data-stu-id="ff4f1-170">For example:</span></span>

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

<span data-ttu-id="ff4f1-171">Se una cartella framework viene lasciata vuota, NuGet non aggiunge riferimenti ad assembly o file di contenuto né esegue script PowerShell per tale framework.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-171">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="ff4f1-172">Poiché `init.ps1` viene eseguito a livello di soluzione e indipendentemente dal progetto, deve essere inserito direttamente sotto la cartella `tools`.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-172">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="ff4f1-173">Viene ignorato se inserito in una cartella framework.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-173">It's ignored if placed under a framework folder.</span></span>
