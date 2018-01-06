---
title: Comando pack NuGet CLI | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 55e9e4d2-8039-4e9b-bdd9-c8b3eb0e894b
description: Riferimento per il comando di nuget.exe pack
keywords: riferimento pacchetto NuGet, il comando di Service pack
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 22643ee4c7d5f858da728ba9d9d2886d600d20f0
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="2f760-104">comando Pack (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2f760-104">pack command (NuGet CLI)</span></span>

<span data-ttu-id="2f760-105">**Si applica a:** creazione di pacchetti &bullet; **le versioni supportate:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="2f760-105">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="2f760-106">Crea un pacchetto NuGet in base all'opzione `.nuspec` o file di progetto.</span><span class="sxs-lookup"><span data-stu-id="2f760-106">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="2f760-107">Il `dotnet pack` comando (vedere [comandi dotnet](dotnet-Commands.md)) e `msbuild /t:pack` (vedere [destinazioni di MSBuild](../schema/msbuild-targets.md)) possono essere utilizzati come valori alternativi.</span><span class="sxs-lookup"><span data-stu-id="2f760-107">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../schema/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="2f760-108">In Mono, crea un pacchetto da un file di progetto non è supportata.</span><span class="sxs-lookup"><span data-stu-id="2f760-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="2f760-109">È inoltre necessario modificare i percorsi locali non nel `.nuspec` file per i percorsi di tipo Unix, come nuget.exe non converte i nomi di percorso di Windows se stesso.</span><span class="sxs-lookup"><span data-stu-id="2f760-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="2f760-110">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="2f760-110">Usage</span></span>

```
nuget pack <nuspecPath | projectPath> [options]
```

<span data-ttu-id="2f760-111">dove `<nuspecPath>` e `<projectPath>` specificare il `.nuspec` o un progetto di file, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="2f760-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="2f760-112">Opzioni</span><span class="sxs-lookup"><span data-stu-id="2f760-112">Options</span></span>

| <span data-ttu-id="2f760-113">Opzione</span><span class="sxs-lookup"><span data-stu-id="2f760-113">Option</span></span> | <span data-ttu-id="2f760-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f760-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2f760-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="2f760-115">BasePath</span></span> | <span data-ttu-id="2f760-116">Imposta il percorso dei file definiti base il `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="2f760-116">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="2f760-117">Compilazione</span><span class="sxs-lookup"><span data-stu-id="2f760-117">Build</span></span> | <span data-ttu-id="2f760-118">Specifica che il progetto deve essere compilato prima di creare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2f760-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="2f760-119">Escludi</span><span class="sxs-lookup"><span data-stu-id="2f760-119">Exclude</span></span> | <span data-ttu-id="2f760-120">Specifica uno o più modelli jolly da escludere quando si crea un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2f760-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> |
| <span data-ttu-id="2f760-121">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="2f760-121">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="2f760-122">Impedisce l'inclusione di una directory vuota quando si compila il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2f760-122">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="2f760-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2f760-123">ForceEnglishOutput</span></span> | <span data-ttu-id="2f760-124">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="2f760-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2f760-125">?</span><span class="sxs-lookup"><span data-stu-id="2f760-125">Help</span></span> | <span data-ttu-id="2f760-126">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="2f760-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="2f760-127">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="2f760-127">IncludeReferencedProjects</span></span> | <span data-ttu-id="2f760-128">Indica che il pacchetto generato deve includere i progetti di riferimento come dipendenze o come parte del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2f760-128">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="2f760-129">Se un progetto a cui fa riferimento ha un corrispondente `.nuspec` file con lo stesso nome del progetto, quindi il progetto di cui viene fatto riferimento viene aggiunto come dipendenza.</span><span class="sxs-lookup"><span data-stu-id="2f760-129">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="2f760-130">In caso contrario, il progetto di riferimento viene aggiunto come parte del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2f760-130">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="2f760-131">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="2f760-131">MinClientVersion</span></span> | <span data-ttu-id="2f760-132">Impostare il *minClientVersion* attributo per il pacchetto creato.</span><span class="sxs-lookup"><span data-stu-id="2f760-132">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="2f760-133">Questo valore sostituirà il valore dell'oggetto esistente *minClientVersion* attributo (se presente) di `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="2f760-133">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="2f760-134">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="2f760-134">MSBuildPath</span></span> | <span data-ttu-id="2f760-135">*(4.0 +)*  Specifica il percorso di MSBuild da usare con il comando, che avrà la precedenza `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="2f760-135">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="2f760-136">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="2f760-136">MSBuildVersion</span></span> | <span data-ttu-id="2f760-137">*(3.2 +)*  Specifica la versione di MSBuild da usare con questo comando.</span><span class="sxs-lookup"><span data-stu-id="2f760-137">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="2f760-138">Valori supportati sono 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="2f760-138">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="2f760-139">Per impostazione predefinita che viene selezionato il percorso di MSBuild, in caso contrario il valore predefinito la versione più aggiornata di MSBuild.</span><span class="sxs-lookup"><span data-stu-id="2f760-139">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="2f760-140">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="2f760-140">NoDefaultExcludes</span></span> | <span data-ttu-id="2f760-141">Impedisce l'esclusione predefinito di NuGet file del pacchetto e i file e cartelle inizia con un punto, ad esempio `.svn` e `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="2f760-141">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="2f760-142">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="2f760-142">NoPackageAnalysis</span></span> | <span data-ttu-id="2f760-143">Specifica che pack non deve eseguire l'analisi del pacchetto dopo la compilazione di quest'ultimo.</span><span class="sxs-lookup"><span data-stu-id="2f760-143">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="2f760-144">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="2f760-144">OutputDirectory</span></span> | <span data-ttu-id="2f760-145">Specifica la cartella in cui è archiviato il pacchetto creato.</span><span class="sxs-lookup"><span data-stu-id="2f760-145">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="2f760-146">Se viene specificata alcuna cartella, viene utilizzata la cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="2f760-146">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="2f760-147">Proprietà</span><span class="sxs-lookup"><span data-stu-id="2f760-147">Properties</span></span> | <span data-ttu-id="2f760-148">Specifica un elenco di proprietà che eseguono l'override di valori nel file di progetto. vedere [proprietà di progetto MSBuild comuni](/visualstudio/msbuild/common-msbuild-project-properties) per i nomi delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="2f760-148">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="2f760-149">In questo caso l'argomento della proprietà è un elenco di token = coppie di valore, separate da punti e virgola, in cui ogni occorrenza di `$token$` nel `.nuspec` file verrà sostituito con il valore specificato.</span><span class="sxs-lookup"><span data-stu-id="2f760-149">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="2f760-150">I valori possono essere stringhe tra virgolette.</span><span class="sxs-lookup"><span data-stu-id="2f760-150">Values can be strings in quotation marks.</span></span> <span data-ttu-id="2f760-151">Si noti che per la proprietà "Configurazione", il valore predefinito è "Debug".</span><span class="sxs-lookup"><span data-stu-id="2f760-151">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="2f760-152">Per modificare in una configurazione di rilascio, utilizzare `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="2f760-152">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="2f760-153">Suffisso</span><span class="sxs-lookup"><span data-stu-id="2f760-153">Suffix</span></span> | <span data-ttu-id="2f760-154">*(3.4.4+)*  Aggiunge un suffisso per il numero di versione generato internamente, in genere utilizzato per l'aggiunta di compilazione o altri identificatori di versione non definitiva.</span><span class="sxs-lookup"><span data-stu-id="2f760-154">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="2f760-155">Ad esempio, usando `-suffix nightly` verrà creato un pacchetto con un tipo di numero versione `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="2f760-155">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="2f760-156">I suffissi devono iniziare con una lettera per evitare potenziali problemi di incompatibilità con diverse versioni di NuGet e gestione pacchetti NuGet, errori e avvisi.</span><span class="sxs-lookup"><span data-stu-id="2f760-156">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="2f760-157">Simboli</span><span class="sxs-lookup"><span data-stu-id="2f760-157">Symbols</span></span> | <span data-ttu-id="2f760-158">Specifica che il pacchetto contiene origini e simboli.</span><span class="sxs-lookup"><span data-stu-id="2f760-158">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="2f760-159">Quando si utilizza un `.nuspec` file, verrà creato un file del pacchetto NuGet regolari e il corrispondente il pacchetto di simboli.</span><span class="sxs-lookup"><span data-stu-id="2f760-159">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="2f760-160">Strumento</span><span class="sxs-lookup"><span data-stu-id="2f760-160">Tool</span></span> | <span data-ttu-id="2f760-161">Specifica che i file di output del progetto devono essere inseriti nel `tool` cartella.</span><span class="sxs-lookup"><span data-stu-id="2f760-161">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="2f760-162">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="2f760-162">Verbosity</span></span> | <span data-ttu-id="2f760-163">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="2f760-163">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="2f760-164">Versione</span><span class="sxs-lookup"><span data-stu-id="2f760-164">Version</span></span> | <span data-ttu-id="2f760-165">Sostituisce il numero di versione di `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="2f760-165">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="2f760-166">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2f760-166">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="2f760-167">Esclusione delle dipendenze di sviluppo</span><span class="sxs-lookup"><span data-stu-id="2f760-167">Excluding development dependencies</span></span>

<span data-ttu-id="2f760-168">Alcuni pacchetti NuGet sono utili come dipendenze di sviluppo, che consentono di creare la propria libreria, ma non necessariamente necessari come dipendenze di pacchetto effettivo.</span><span class="sxs-lookup"><span data-stu-id="2f760-168">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="2f760-169">Il `pack` verrà ignorata `package` voci `packages.config` che dispongono di `developmentDependency` attributo impostato su `true`.</span><span class="sxs-lookup"><span data-stu-id="2f760-169">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="2f760-170">Queste voci non includerà come delle dipendenze del pacchetto creato.</span><span class="sxs-lookup"><span data-stu-id="2f760-170">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="2f760-171">Ad esempio, tenere presente quanto segue `packages.config` file nel progetto di origine:</span><span class="sxs-lookup"><span data-stu-id="2f760-171">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="2f760-172">Per questo progetto, il pacchetto creato da `nuget pack` avrà una dipendenza sulla `jQuery` e `microsoft-web-helpers` ma non `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="2f760-172">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="2f760-173">Esempi</span><span class="sxs-lookup"><span data-stu-id="2f760-173">Examples</span></span>

```
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5
```
