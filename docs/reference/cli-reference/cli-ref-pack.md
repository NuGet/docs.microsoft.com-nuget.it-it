---
title: Comando Pack dell'interfaccia della riga di comando NuGet
description: Riferimento per il comando nuget.exe Pack
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0483a75c7ee1fd851f935f44d96a417e2e86bf20
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622954"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="1426b-103">comando Pack (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="1426b-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="1426b-104">**Si applica a:** versioni supportate per la creazione di pacchetti &bullet; **:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="1426b-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="1426b-105">Crea un pacchetto NuGet basato sul file con [estensione NuSpec](../nuspec.md) o Project specificato.</span><span class="sxs-lookup"><span data-stu-id="1426b-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="1426b-106">Il `dotnet pack` comando (vedere i [comandi DotNet](../dotnet-Commands.md)) e `msbuild -t:pack` (vedere [destinazioni MSBuild](../msbuild-targets.md)) può essere usato come alternativa.</span><span class="sxs-lookup"><span data-stu-id="1426b-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="1426b-107">Usare [`dotnet pack`](../dotnet-Commands.md) o [`msbuild -t:pack`](../msbuild-targets.md) per i progetti basati su [PackageReference](../../consume-packages/package-references-in-project-files.md) .</span><span class="sxs-lookup"><span data-stu-id="1426b-107">Use [`dotnet pack`](../dotnet-Commands.md) or [`msbuild -t:pack`](../msbuild-targets.md) for [PackageReference](../../consume-packages/package-references-in-project-files.md) based projects.</span></span>
> <span data-ttu-id="1426b-108">In mono la creazione di un pacchetto da un file di progetto non è supportata.</span><span class="sxs-lookup"><span data-stu-id="1426b-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="1426b-109">È anche necessario modificare i percorsi non locali nel file nei `.nuspec` percorsi di tipo UNIX, in quanto nuget.exe non converte i nomi di percorso di Windows.</span><span class="sxs-lookup"><span data-stu-id="1426b-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="1426b-110">Uso</span><span class="sxs-lookup"><span data-stu-id="1426b-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="1426b-111">dove `<nuspecPath>` e `<projectPath>` specificano `.nuspec` rispettivamente il file di progetto o.</span><span class="sxs-lookup"><span data-stu-id="1426b-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="1426b-112">Opzioni</span><span class="sxs-lookup"><span data-stu-id="1426b-112">Options</span></span>
- **`-BasePath`**

   <span data-ttu-id="1426b-113">Imposta il percorso di base dei file definiti nel file con [estensione NuSpec](../nuspec.md) .</span><span class="sxs-lookup"><span data-stu-id="1426b-113">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span>

- **`-Build`**

  <span data-ttu-id="1426b-114">Specifica che il progetto deve essere compilato prima della compilazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1426b-114">Specifies that the project should be built before building the package.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="1426b-115">File di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="1426b-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1426b-116">Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="1426b-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Exclude`**

  <span data-ttu-id="1426b-117">Specifica uno o più criteri jolly da escludere durante la creazione di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1426b-117">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="1426b-118">Per specificare più di un modello, ripetere il flag-exclude.</span><span class="sxs-lookup"><span data-stu-id="1426b-118">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="1426b-119">Vedi l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="1426b-119">See example below.</span></span>

- **`-ExcludeEmptyDirectories`**

  <span data-ttu-id="1426b-120">Impedisce l'inclusione di directory vuote durante la compilazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1426b-120">Prevents inclusion of empty directories when building the package.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="1426b-121">*(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="1426b-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="1426b-122">Visualizza le informazioni della Guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="1426b-122">Displays help information for the command.</span></span>

- **`-IncludeReferencedProjects`**

  <span data-ttu-id="1426b-123">Indica che il pacchetto compilato deve includere i progetti a cui si fa riferimento come dipendenze o come parte del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1426b-123">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="1426b-124">Se un progetto a cui viene fatto riferimento ha un file corrispondente con `.nuspec` lo stesso nome del progetto, il progetto a cui si fa riferimento viene aggiunto come dipendenza.</span><span class="sxs-lookup"><span data-stu-id="1426b-124">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="1426b-125">In caso contrario, il progetto a cui si fa riferimento viene aggiunto come parte del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1426b-125">Otherwise, the referenced project is added as part of the package.</span></span>

- **`-InstallPackageToOutputPath`**

  <span data-ttu-id="1426b-126">Specificare se il comando deve preparare la directory di output del pacchetto per supportare la condivisione come feed.</span><span class="sxs-lookup"><span data-stu-id="1426b-126">Specify if the command should prepare the package output directory to support share as feed.</span></span>

- **`-MinClientVersion`**

  <span data-ttu-id="1426b-127">Impostare l'attributo *minClientVersion* per il pacchetto creato.</span><span class="sxs-lookup"><span data-stu-id="1426b-127">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="1426b-128">Questo valore eseguirà l'override del valore dell'attributo *minClientVersion* esistente, se presente, nel `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="1426b-128">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="1426b-129">*(4.0 +)* Specifica il percorso di MSBuild da usare con il comando, avendo la precedenza su `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="1426b-129">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="1426b-130">*(3.2 +)* Specifica la versione di MSBuild da usare con questo comando.</span><span class="sxs-lookup"><span data-stu-id="1426b-130">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="1426b-131">I valori supportati sono 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="1426b-131">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="1426b-132">Per impostazione predefinita, viene scelto MSBuild nel percorso; in caso contrario, per impostazione predefinita viene impostata la versione più recente di MSBuild.</span><span class="sxs-lookup"><span data-stu-id="1426b-132">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoDefaultExcludes`**

  <span data-ttu-id="1426b-133">Impedisce l'esclusione predefinita dei file e delle cartelle del pacchetto NuGet a partire da un punto, ad esempio `.svn` e `.gitignore` .</span><span class="sxs-lookup"><span data-stu-id="1426b-133">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="1426b-134">Evita la richiesta di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1426b-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoPackageAnalysis`**

  <span data-ttu-id="1426b-135">Specifica che pack non deve eseguire l'analisi del pacchetto dopo la compilazione di quest'ultimo.</span><span class="sxs-lookup"><span data-stu-id="1426b-135">Specifies that pack should not run package analysis after building the package.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="1426b-136">Specifica la cartella in cui è archiviato il pacchetto creato.</span><span class="sxs-lookup"><span data-stu-id="1426b-136">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="1426b-137">Se non viene specificata alcuna cartella, viene utilizzata la cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="1426b-137">If no folder is specified, the current folder is used.</span></span>

- **`-OutputFileNamesWithoutVersion`**

  <span data-ttu-id="1426b-138">Specificare se il comando deve preparare il nome dell'output del pacchetto senza la versione.</span><span class="sxs-lookup"><span data-stu-id="1426b-138">Specify if the command should prepare the package output name without the version.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="1426b-139">Specifica la cartella dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1426b-139">Specifies the packages folder.</span></span>

- **`-p|-Properties`**

  <span data-ttu-id="1426b-140">Viene visualizzato per ultimo nella riga di comando dopo le altre opzioni.</span><span class="sxs-lookup"><span data-stu-id="1426b-140">Should appear last on the command line after other options.</span></span> <span data-ttu-id="1426b-141">Specifica un elenco di proprietà che eseguono l'override dei valori nel file di progetto. vedere [proprietà del progetto MSBuild comuni](/visualstudio/msbuild/common-msbuild-project-properties) per i nomi di proprietà.</span><span class="sxs-lookup"><span data-stu-id="1426b-141">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="1426b-142">L'argomento Properties è un elenco di coppie token = valore, separate da punti e virgola, in cui ogni occorrenza di `$token$` nel `.nuspec` file verrà sostituita con il valore specificato.</span><span class="sxs-lookup"><span data-stu-id="1426b-142">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="1426b-143">I valori possono essere stringhe tra virgolette.</span><span class="sxs-lookup"><span data-stu-id="1426b-143">Values can be strings in quotation marks.</span></span> <span data-ttu-id="1426b-144">Si noti che per la proprietà "Configuration", il valore predefinito è "debug".</span><span class="sxs-lookup"><span data-stu-id="1426b-144">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="1426b-145">Per passare a una configurazione di versione, usare `-Properties Configuration=Release` .</span><span class="sxs-lookup"><span data-stu-id="1426b-145">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> <span data-ttu-id="1426b-146">**In generale**, le proprietà devono essere le stesse usate durante la compilazione del progetto corrispondente, in modo da evitare comportamenti potenzialmente strani.</span><span class="sxs-lookup"><span data-stu-id="1426b-146">**In general**, Properties should be the same that were used during the corresponding project build, in order to avoid potentially strange behavior.</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="1426b-147">Specifica la directory della soluzione.</span><span class="sxs-lookup"><span data-stu-id="1426b-147">Specifies the solution directory.</span></span>

- **`-Suffix`**

  <span data-ttu-id="1426b-148">*(3.4.4 +)* Accoda un suffisso al numero di versione generato internamente, usato in genere per accodare gli identificatori della versione non definitiva.</span><span class="sxs-lookup"><span data-stu-id="1426b-148">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="1426b-149">Usando, ad esempio, `-suffix nightly` viene creato un pacchetto con un numero di versione come `1.2.3-nightly` .</span><span class="sxs-lookup"><span data-stu-id="1426b-149">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="1426b-150">I suffissi devono iniziare con una lettera per evitare avvisi, errori e potenziali incompatibilità con versioni diverse di NuGet e gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="1426b-150">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span>

- **`-SymbolPackageFormat`**

  <span data-ttu-id="1426b-151">Quando si crea un pacchetto di simboli, consente di scegliere tra il `snupkg` `symbols.nupkg` formato e.</span><span class="sxs-lookup"><span data-stu-id="1426b-151">When creating a symbols package, allows to choose between the `snupkg` and `symbols.nupkg` format.</span></span>

- **`-Symbols`**

  <span data-ttu-id="1426b-152">Specifica che il pacchetto contiene origini e simboli.</span><span class="sxs-lookup"><span data-stu-id="1426b-152">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="1426b-153">Quando viene usato con un `.nuspec` file, viene creato un normale file di pacchetto NuGet e il pacchetto di simboli corrispondente.</span><span class="sxs-lookup"><span data-stu-id="1426b-153">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="1426b-154">Per impostazione predefinita, crea un [pacchetto di simboli legacy](../../create-packages/Symbol-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="1426b-154">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="1426b-155">Il nuovo formato consigliato per i pacchetti di simboli è l'estensione snupkg.</span><span class="sxs-lookup"><span data-stu-id="1426b-155">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="1426b-156">Vedere [Creazione di pacchetti di simboli (estensione snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="1426b-156">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span>

- **`-Tool`**

   <span data-ttu-id="1426b-157">Specifica che i file di output del progetto devono essere inseriti nella `tool` cartella.</span><span class="sxs-lookup"><span data-stu-id="1426b-157">Specifies that the output files of the project should be placed in the `tool` folder.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="1426b-158">Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="1426b-158">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="1426b-159">Esegue l'override del numero di versione dal `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="1426b-159">Overrides the version number from the `.nuspec` file.</span></span>

<span data-ttu-id="1426b-160">Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1426b-160">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="1426b-161">Esclusione delle dipendenze di sviluppo</span><span class="sxs-lookup"><span data-stu-id="1426b-161">Excluding development dependencies</span></span>

<span data-ttu-id="1426b-162">Alcuni pacchetti NuGet sono utili come dipendenze di sviluppo, che consentono di creare una libreria personalizzata, ma non sono necessariamente necessari come dipendenze effettive del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1426b-162">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="1426b-163">Il `pack` comando ignorerà le `package` voci in con `packages.config` l' `developmentDependency` attributo impostato su `true` .</span><span class="sxs-lookup"><span data-stu-id="1426b-163">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="1426b-164">Queste voci non verranno incluse come dipendenze nel pacchetto creato.</span><span class="sxs-lookup"><span data-stu-id="1426b-164">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="1426b-165">Si consideri, ad esempio, il `packages.config` file seguente nel progetto di origine:</span><span class="sxs-lookup"><span data-stu-id="1426b-165">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="1426b-166">Per questo progetto, il pacchetto creato da `nuget pack` avrà una dipendenza da `jQuery` e `microsoft-web-helpers` non `netfx-Guard` .</span><span class="sxs-lookup"><span data-stu-id="1426b-166">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="suppressing-pack-warnings"></a><span data-ttu-id="1426b-167">Eliminazione degli avvisi di Pack</span><span class="sxs-lookup"><span data-stu-id="1426b-167">Suppressing pack warnings</span></span>

<span data-ttu-id="1426b-168">Sebbene sia consigliabile risolvere tutti gli avvisi di NuGet durante le operazioni di Pack, in determinate situazioni l'eliminazione è garantita.</span><span class="sxs-lookup"><span data-stu-id="1426b-168">While it is recommended that you resolve all NuGet warnings during your pack operations, in certain situations suppressing them is warranted.</span></span>

<span data-ttu-id="1426b-169">È possibile ottenere questo risultato nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="1426b-169">You can achieve that in the following way:</span></span> 

> <span data-ttu-id="1426b-170">Pacchetto di nuget.exe Pack. NuSpec-Properties nowarn = NU5104</span><span class="sxs-lookup"><span data-stu-id="1426b-170">nuget.exe pack package.nuspec -Properties NoWarn=NU5104</span></span>

## <a name="examples"></a><span data-ttu-id="1426b-171">Esempi</span><span class="sxs-lookup"><span data-stu-id="1426b-171">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
