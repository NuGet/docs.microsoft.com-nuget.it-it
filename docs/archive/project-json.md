---
title: Informazioni di riferimento sul file project.json per NuGet
description: In alcuni tipi di progetto, il file project.json include l'elenco aggiornato dei pacchetti NuGet usati nel progetto.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: e4d8b5b9ab4605516827ead8939f278d110c7a48
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547784"
---
# <a name="projectjson-reference"></a><span data-ttu-id="c0197-103">Riferimenti di project.json</span><span class="sxs-lookup"><span data-stu-id="c0197-103">project.json reference</span></span>

<span data-ttu-id="c0197-104">*NuGet 3.x+*</span><span class="sxs-lookup"><span data-stu-id="c0197-104">*NuGet 3.x+*</span></span>

<span data-ttu-id="c0197-105">Il file `project.json` include un elenco dei pacchetti usati in un progetto, noto come formato di gestione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="c0197-105">The `project.json` file maintains a list of packages used in a project, known as a package management format.</span></span> <span data-ttu-id="c0197-106">Prevale su `packages.config`, ma viene a sua volta sostituito da [PackageReference](../consume-packages/package-references-in-project-files.md) con NuGet 4.0+.</span><span class="sxs-lookup"><span data-stu-id="c0197-106">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="c0197-107">Il file [`project.lock.json`](#projectlockjson) (descritto sotto) viene anche usato nei progetti che impiegano `project.json`.</span><span class="sxs-lookup"><span data-stu-id="c0197-107">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="c0197-108">`project.json` presenta la struttura di base seguente, dove ognuno dei quattro oggetti di primo livello può avere un numero indeterminato di oggetti figlio:</span><span class="sxs-lookup"><span data-stu-id="c0197-108">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a><span data-ttu-id="c0197-109">Dipendenze</span><span class="sxs-lookup"><span data-stu-id="c0197-109">Dependencies</span></span>

<span data-ttu-id="c0197-110">Elenca le dipendenze del pacchetto NuGet per il progetto nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="c0197-110">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="c0197-111">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c0197-111">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="c0197-112">Nella sezione `dependencies` la finestra di dialogo Gestione pacchetti NuGet aggiunge le dipendenze del pacchetto al progetto.</span><span class="sxs-lookup"><span data-stu-id="c0197-112">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="c0197-113">L'ID del pacchetto corrisponde all'ID del pacchetto in nuget.org, che è uguale all'ID usato nella console di Gestione pacchetti: `Install-Package Microsoft.NETCore`.</span><span class="sxs-lookup"><span data-stu-id="c0197-113">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="c0197-114">Quando si ripristinano i pacchetti, il vincolo della versione `"5.0.0"` implica `>= 5.0.0`,</span><span class="sxs-lookup"><span data-stu-id="c0197-114">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="c0197-115">vale a dire che se la versione 5.0.0 non è disponibile sul server, ma la 5.0.1 lo è, NuGet installa la 5.0.1 e avvisa dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="c0197-115">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="c0197-116">In caso contrario, NuGet seleziona la versione più bassa possibile corrispondente al vincolo.</span><span class="sxs-lookup"><span data-stu-id="c0197-116">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="c0197-117">Per altre informazioni dettagliate sulle regole di risoluzione, vedere [Risoluzione delle dipendenze](../consume-packages/dependency-resolution.md).</span><span class="sxs-lookup"><span data-stu-id="c0197-117">See [Dependency resolution](../consume-packages/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="c0197-118">Gestione degli asset delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="c0197-118">Managing dependency assets</span></span>

<span data-ttu-id="c0197-119">Per controllare quali asset delle dipendenze confluiscono nel progetto di primo livello, specificare un set di tag delimitati da virgole nelle proprietà `include` ed `exclude` del riferimento alle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="c0197-119">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="c0197-120">I tag sono elencati nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="c0197-120">The tags are listed the table below:</span></span>

| <span data-ttu-id="c0197-121">Tag di inclusione/esclusione</span><span class="sxs-lookup"><span data-stu-id="c0197-121">Include/Exclude tag</span></span> | <span data-ttu-id="c0197-122">Cartelle di destinazione interessate</span><span class="sxs-lookup"><span data-stu-id="c0197-122">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="c0197-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="c0197-123">contentFiles</span></span> | <span data-ttu-id="c0197-124">Content</span><span class="sxs-lookup"><span data-stu-id="c0197-124">Content</span></span>  |
| <span data-ttu-id="c0197-125">runtime</span><span class="sxs-lookup"><span data-stu-id="c0197-125">runtime</span></span> | <span data-ttu-id="c0197-126">Runtime, Resources e FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="c0197-126">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="c0197-127">compile</span><span class="sxs-lookup"><span data-stu-id="c0197-127">compile</span></span> | <span data-ttu-id="c0197-128">lib</span><span class="sxs-lookup"><span data-stu-id="c0197-128">lib</span></span> |
| <span data-ttu-id="c0197-129">build</span><span class="sxs-lookup"><span data-stu-id="c0197-129">build</span></span> | <span data-ttu-id="c0197-130">build (proprietà e destinazioni MSBuild)</span><span class="sxs-lookup"><span data-stu-id="c0197-130">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="c0197-131">native</span><span class="sxs-lookup"><span data-stu-id="c0197-131">native</span></span> | <span data-ttu-id="c0197-132">native</span><span class="sxs-lookup"><span data-stu-id="c0197-132">native</span></span> |
| <span data-ttu-id="c0197-133">none</span><span class="sxs-lookup"><span data-stu-id="c0197-133">none</span></span> | <span data-ttu-id="c0197-134">Nessuna cartella</span><span class="sxs-lookup"><span data-stu-id="c0197-134">No folders</span></span> |
| <span data-ttu-id="c0197-135">tutti</span><span class="sxs-lookup"><span data-stu-id="c0197-135">all</span></span> | <span data-ttu-id="c0197-136">Tutte le cartelle</span><span class="sxs-lookup"><span data-stu-id="c0197-136">All folders</span></span> |

<span data-ttu-id="c0197-137">I tag specificati con `exclude` hanno la precedenza rispetto a quelli specificati con `include`.</span><span class="sxs-lookup"><span data-stu-id="c0197-137">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="c0197-138">Ad esempio, `include="runtime, compile" exclude="compile"` equivale a `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="c0197-138">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="c0197-139">Ad esempio, per includere le cartelle `build` e `native` di una dipendenza, usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="c0197-139">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

<span data-ttu-id="c0197-140">Per escludere le cartelle `content` e `build` di una dipendenza, usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="c0197-140">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a><span data-ttu-id="c0197-141">Framework</span><span class="sxs-lookup"><span data-stu-id="c0197-141">Frameworks</span></span>

<span data-ttu-id="c0197-142">Elenca i framework in cui viene eseguito il progetto, ad esempio `net45`, `netcoreapp`, `netstandard`.</span><span class="sxs-lookup"><span data-stu-id="c0197-142">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="c0197-143">Nella sezione `frameworks` è consentita una sola voce.</span><span class="sxs-lookup"><span data-stu-id="c0197-143">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="c0197-144">Fanno eccezione i file `project.json` per i progetti ASP.NET compilati con la toolchain DNX deprecata, che consente più destinazioni.</span><span class="sxs-lookup"><span data-stu-id="c0197-144">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX tool chain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="c0197-145">Runtimes</span><span class="sxs-lookup"><span data-stu-id="c0197-145">Runtimes</span></span>

<span data-ttu-id="c0197-146">Elenca i sistemi operativi e le architetture in cui l'app viene eseguita, ad esempio `win10-arm`, `win8-x64`, `win8-x86`.</span><span class="sxs-lookup"><span data-stu-id="c0197-146">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

<span data-ttu-id="c0197-147">Non è necessario specificare un runtime per un pacchetto contenente una libreria PCL che può essere eseguita in qualsiasi runtime.</span><span class="sxs-lookup"><span data-stu-id="c0197-147">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="c0197-148">Ciò deve valere anche per qualsiasi dipendenza. In caso contrario, è necessario specificare i runtime.</span><span class="sxs-lookup"><span data-stu-id="c0197-148">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="c0197-149">Supports</span><span class="sxs-lookup"><span data-stu-id="c0197-149">Supports</span></span>

<span data-ttu-id="c0197-150">Definisce un set di controlli per le dipendenze dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="c0197-150">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="c0197-151">È possibile definire dove si prevede che la libreria PCL o l'app venga eseguita.</span><span class="sxs-lookup"><span data-stu-id="c0197-151">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="c0197-152">Le definizioni non sono restrittive perché il codice può essere eseguito altrove,</span><span class="sxs-lookup"><span data-stu-id="c0197-152">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="c0197-153">ma, se si specificano questi controlli, NuGet controlla che tutte le dipendenze siano rispettate nei TxM elencati.</span><span class="sxs-lookup"><span data-stu-id="c0197-153">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="c0197-154">Alcuni esempi di valori validi sono `net46.app`, `uwp.10.0.app` e così via.</span><span class="sxs-lookup"><span data-stu-id="c0197-154">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="c0197-155">Questa sezione verrà popolata automaticamente quando si seleziona una voce nella finestra di dialogo delle destinazioni Libreria di classi portabile.</span><span class="sxs-lookup"><span data-stu-id="c0197-155">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="c0197-156">Imports</span><span class="sxs-lookup"><span data-stu-id="c0197-156">Imports</span></span>

<span data-ttu-id="c0197-157">Le importazioni sono progettate per consentire ai pacchetti che usano il TxM `dotnet` di interagire con pacchetti che non dichiarano un TxM dotnet.</span><span class="sxs-lookup"><span data-stu-id="c0197-157">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="c0197-158">Se il progetto usa il TxM `dotnet`, anche tutti i pacchetti da cui si dipende devono avere un TxM `dotnet`, a meno che non si aggiunga il codice seguente a `project.json` per consentire alle piattaforme non `dotnet` di essere compatibili con `dotnet`:</span><span class="sxs-lookup"><span data-stu-id="c0197-158">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="c0197-159">Se si usa il TxM `dotnet`, il sistema del progetto PCL aggiunge l'istruzione `imports` appropriata in base alle destinazioni supportate.</span><span class="sxs-lookup"><span data-stu-id="c0197-159">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="c0197-160">Differenze rispetto alle app portabili e ai progetti Web</span><span class="sxs-lookup"><span data-stu-id="c0197-160">Differences from portable apps and web projects</span></span>

<span data-ttu-id="c0197-161">Il file `project.json` usato da NuGet è un subset di quello presente nei progetti ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="c0197-161">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="c0197-162">In ASP.NET Core `project.json` viene usato per i metadati del progetto, le informazioni di compilazione e le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="c0197-162">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="c0197-163">Se viene usato in altri sistemi di progetto, questi tre elementi vengono divisi in file separati e `project.json` contiene meno informazioni.</span><span class="sxs-lookup"><span data-stu-id="c0197-163">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="c0197-164">Ecco le differenze principali:</span><span class="sxs-lookup"><span data-stu-id="c0197-164">Notable differences include:</span></span>

- <span data-ttu-id="c0197-165">Nella sezione `frameworks` può essere presente un solo framework.</span><span class="sxs-lookup"><span data-stu-id="c0197-165">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="c0197-166">Il file non può contenere le dipendenze, le opzioni di compilazione e così via presenti nei file `project.json` DNX.</span><span class="sxs-lookup"><span data-stu-id="c0197-166">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="c0197-167">Dal momento che può esserci un solo framework, non ha senso immettere dipendenze specifiche del framework.</span><span class="sxs-lookup"><span data-stu-id="c0197-167">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="c0197-168">La compilazione viene gestita da MSBuild, quindi le opzioni di compilazione, le definizioni del preprocessore e così via fanno tutte parte del file di progetto MSBuild e non di `project.json`.</span><span class="sxs-lookup"><span data-stu-id="c0197-168">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="c0197-169">In NuGet 3+ non è previsto che gli sviluppatori modifichino manualmente `project.json`, perché è l'interfaccia utente di Gestione pacchetti in Visual Studio a modificare il contenuto.</span><span class="sxs-lookup"><span data-stu-id="c0197-169">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="c0197-170">Ciò premesso, è ovviamente possibile modificare il file, ma è necessario compilare il progetto per avviare un ripristino del pacchetto o richiamare il ripristino in un altro modo.</span><span class="sxs-lookup"><span data-stu-id="c0197-170">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="c0197-171">Vedere [Ripristino di pacchetti](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="c0197-171">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="c0197-172">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="c0197-172">project.lock.json</span></span>

<span data-ttu-id="c0197-173">Il file `project.lock.json` viene generato durante il processo di ripristino dei pacchetti NuGet nei progetti che usano `project.json`.</span><span class="sxs-lookup"><span data-stu-id="c0197-173">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="c0197-174">Contiene uno snapshot di tutte le informazioni generate quando NuGet analizza il grafo dei pacchetti e include la versione, i contenuti e le dipendenze di tutti i pacchetti del progetto.</span><span class="sxs-lookup"><span data-stu-id="c0197-174">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="c0197-175">Il sistema di compilazione lo usa per scegliere i pacchetti pertinenti da un percorso globale quando si compila il progetto invece di dipendere da una cartella di pacchetti locale nel progetto stesso.</span><span class="sxs-lookup"><span data-stu-id="c0197-175">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="c0197-176">Ne deriva un miglioramento delle prestazioni di compilazione perché è necessario leggere solo `project.lock.json` invece di più file `.nuspec` separati.</span><span class="sxs-lookup"><span data-stu-id="c0197-176">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="c0197-177">`project.lock.json` viene automaticamente generato durante il ripristino del pacchetto, quindi può essere omesso dal controllo del codice sorgente aggiungendolo ai file `.gitignore` e `.tfignore`. Vedere [Pacchetti e controllo del codice sorgente](../consume-packages/packages-and-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="c0197-177">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="c0197-178">Se tuttavia lo si include nel controllo del codice sorgente, la cronologia modifiche indica le modifiche apportate alle dipendenze nel corso del tempo.</span><span class="sxs-lookup"><span data-stu-id="c0197-178">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
