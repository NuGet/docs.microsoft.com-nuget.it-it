---
title: Comando pack NuGet CLI
description: Informazioni di riferimento per il comando pack nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: db236b0eaac34ca9f6f67fd15ca3ad6884f6a18d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549096"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="e188b-103">Comando pack (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="e188b-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="e188b-104">**Si applica a:** creazione del pacchetto &bullet; **le versioni supportate:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="e188b-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="e188b-105">Crea un pacchetto NuGet basato sull'oggetto specificato `.nuspec` o file di progetto.</span><span class="sxs-lookup"><span data-stu-id="e188b-105">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="e188b-106">Il `dotnet pack` comando (vedere [comandi dotnet](dotnet-Commands.md)) e `msbuild /t:pack` (vedere [destinazioni di MSBuild](../reference/msbuild-targets.md)) può essere usato come alternative.</span><span class="sxs-lookup"><span data-stu-id="e188b-106">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="e188b-107">In Mono, creazione di un pacchetto da un file di progetto non è supportata.</span><span class="sxs-lookup"><span data-stu-id="e188b-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="e188b-108">È anche necessario modificare i percorsi locali non nel `.nuspec` file ai percorsi in stile Unix, come nuget.exe non converte percorsi di Windows se stesso.</span><span class="sxs-lookup"><span data-stu-id="e188b-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="e188b-109">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="e188b-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="e188b-110">in cui `<nuspecPath>` e `<projectPath>` specificare il `.nuspec` o file, rispettivamente del progetto.</span><span class="sxs-lookup"><span data-stu-id="e188b-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="e188b-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="e188b-111">Options</span></span>

| <span data-ttu-id="e188b-112">Opzione</span><span class="sxs-lookup"><span data-stu-id="e188b-112">Option</span></span> | <span data-ttu-id="e188b-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e188b-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e188b-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="e188b-114">BasePath</span></span> | <span data-ttu-id="e188b-115">Imposta il percorso dei file definiti base il `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="e188b-115">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="e188b-116">Compilazione</span><span class="sxs-lookup"><span data-stu-id="e188b-116">Build</span></span> | <span data-ttu-id="e188b-117">Specifica che il progetto deve essere compilato prima di compilare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e188b-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="e188b-118">Escludi</span><span class="sxs-lookup"><span data-stu-id="e188b-118">Exclude</span></span> | <span data-ttu-id="e188b-119">Specifica uno o più modelli con caratteri jolly da escludere durante la creazione di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e188b-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="e188b-120">Per specificare più di un criterio, ripetere il - flag di esclusione.</span><span class="sxs-lookup"><span data-stu-id="e188b-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="e188b-121">Vedere l'esempio riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="e188b-121">See example below.</span></span> |
| <span data-ttu-id="e188b-122">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="e188b-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="e188b-123">Impedisce l'inclusione delle directory vuota quando si compila il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e188b-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="e188b-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e188b-124">ForceEnglishOutput</span></span> | <span data-ttu-id="e188b-125">*(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="e188b-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e188b-126">?</span><span class="sxs-lookup"><span data-stu-id="e188b-126">Help</span></span> | <span data-ttu-id="e188b-127">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="e188b-127">Displays help information for the command.</span></span> |
| <span data-ttu-id="e188b-128">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="e188b-128">IncludeReferencedProjects</span></span> | <span data-ttu-id="e188b-129">Indica che il pacchetto generato deve includere progetti con riferimenti come dipendenze o come parte del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e188b-129">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="e188b-130">Se un progetto di riferimento ha un corrispondente `.nuspec` file con lo stesso nome del progetto, tale progetto cui viene fatto riferimento viene aggiunto come dipendenza.</span><span class="sxs-lookup"><span data-stu-id="e188b-130">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="e188b-131">In caso contrario, il progetto di riferimento viene aggiunto come parte del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e188b-131">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="e188b-132">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="e188b-132">MinClientVersion</span></span> | <span data-ttu-id="e188b-133">Impostare il *minClientVersion* attributo per il pacchetto creato.</span><span class="sxs-lookup"><span data-stu-id="e188b-133">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="e188b-134">Questo valore sostituirà il valore dell'oggetto esistente *minClientVersion* attributo (se presente) nel `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="e188b-134">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="e188b-135">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="e188b-135">MSBuildPath</span></span> | <span data-ttu-id="e188b-136">*(4.0 +)*  Specifica il percorso di MSBuild da usare con il comando, hanno la precedenza sui `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="e188b-136">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="e188b-137">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="e188b-137">MSBuildVersion</span></span> | <span data-ttu-id="e188b-138">*(3.2 +)*  Specifica la versione di MSBuild da usare con questo comando.</span><span class="sxs-lookup"><span data-stu-id="e188b-138">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="e188b-139">Valori supportati sono 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="e188b-139">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="e188b-140">Per impostazione predefinita che viene selezionato nel proprio percorso di MSBuild, in caso contrario, per impostazione predefinita la versione installata più recente di MSBuild.</span><span class="sxs-lookup"><span data-stu-id="e188b-140">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="e188b-141">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="e188b-141">NoDefaultExcludes</span></span> | <span data-ttu-id="e188b-142">Impedisce l'esclusione predefinita di NuGet package file e i file e cartelle che iniziano con un punto, ad esempio `.svn` e `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="e188b-142">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="e188b-143">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="e188b-143">NoPackageAnalysis</span></span> | <span data-ttu-id="e188b-144">Specifica che pack non deve eseguire l'analisi del pacchetto dopo la compilazione di quest'ultimo.</span><span class="sxs-lookup"><span data-stu-id="e188b-144">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="e188b-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="e188b-145">OutputDirectory</span></span> | <span data-ttu-id="e188b-146">Specifica la cartella in cui è archiviato il pacchetto creato.</span><span class="sxs-lookup"><span data-stu-id="e188b-146">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="e188b-147">Se si specifica alcuna cartella, viene utilizzata la cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="e188b-147">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="e188b-148">Proprietà</span><span class="sxs-lookup"><span data-stu-id="e188b-148">Properties</span></span> | <span data-ttu-id="e188b-149">Dovrebbe essere visualizzato ultima nella riga di comando dopo le altre opzioni.</span><span class="sxs-lookup"><span data-stu-id="e188b-149">Should appear last on the command line after other options.</span></span> <span data-ttu-id="e188b-150">Specifica un elenco di proprietà che eseguono l'override di valori nel file di progetto. visualizzare [proprietà di progetto MSBuild comuni](/visualstudio/msbuild/common-msbuild-project-properties) per i nomi delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="e188b-150">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="e188b-151">In questo caso l'argomento della proprietà è un elenco di token = coppie valore, separate da punti e virgola, in cui ogni occorrenza di `$token$` nella `.nuspec` file verrà sostituito con il valore specificato.</span><span class="sxs-lookup"><span data-stu-id="e188b-151">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="e188b-152">I valori possono essere stringhe tra virgolette.</span><span class="sxs-lookup"><span data-stu-id="e188b-152">Values can be strings in quotation marks.</span></span> <span data-ttu-id="e188b-153">Si noti che per la proprietà "Configurazione", il valore predefinito è "Debug".</span><span class="sxs-lookup"><span data-stu-id="e188b-153">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="e188b-154">Per modificare una configurazione rilascio, usare `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="e188b-154">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="e188b-155">Suffisso</span><span class="sxs-lookup"><span data-stu-id="e188b-155">Suffix</span></span> | <span data-ttu-id="e188b-156">*(3.4.4+)*  Aggiunge un suffisso per il numero di versione generata internamente, in genere usato per l'accodamento compilazione o altri identificatori di versione non definitiva.</span><span class="sxs-lookup"><span data-stu-id="e188b-156">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="e188b-157">Ad esempio, usando `-suffix nightly` verrà creato un pacchetto con una simile a numeri di versione `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="e188b-157">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="e188b-158">I suffissi devono iniziare con una lettera per evitare gli avvisi, errori e potenziali incompatibilità con diverse versioni di NuGet e la gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="e188b-158">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="e188b-159">Simboli</span><span class="sxs-lookup"><span data-stu-id="e188b-159">Symbols</span></span> | <span data-ttu-id="e188b-160">Specifica che il pacchetto contiene origini e simboli.</span><span class="sxs-lookup"><span data-stu-id="e188b-160">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="e188b-161">Se usato con un `.nuspec` file, verrà creato un file di pacchetto NuGet normale e di pacchetto di simboli corrispondente.</span><span class="sxs-lookup"><span data-stu-id="e188b-161">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="e188b-162">Strumento</span><span class="sxs-lookup"><span data-stu-id="e188b-162">Tool</span></span> | <span data-ttu-id="e188b-163">Specifica che i file di output del progetto devono essere inseriti nel `tool` cartella.</span><span class="sxs-lookup"><span data-stu-id="e188b-163">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="e188b-164">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="e188b-164">Verbosity</span></span> | <span data-ttu-id="e188b-165">Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="e188b-165">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="e188b-166">Versione</span><span class="sxs-lookup"><span data-stu-id="e188b-166">Version</span></span> | <span data-ttu-id="e188b-167">Sostituisce il numero di versione dal `.nuspec` file.</span><span class="sxs-lookup"><span data-stu-id="e188b-167">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="e188b-168">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e188b-168">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="e188b-169">Esclusione delle dipendenze di sviluppo</span><span class="sxs-lookup"><span data-stu-id="e188b-169">Excluding development dependencies</span></span>

<span data-ttu-id="e188b-170">Alcuni pacchetti NuGet sono utili come dipendenze di sviluppo, che aiuta a creare una libreria personalizzata, ma non sono necessariamente necessarie come dipendenze di pacchetto effettivo.</span><span class="sxs-lookup"><span data-stu-id="e188b-170">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="e188b-171">Il `pack` comando verrà ignorati `package` voci `packages.config` che hanno il `developmentDependency` attributo impostato su `true`.</span><span class="sxs-lookup"><span data-stu-id="e188b-171">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="e188b-172">Queste voci non includerà come delle dipendenze del pacchetto creato.</span><span class="sxs-lookup"><span data-stu-id="e188b-172">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="e188b-173">Ad esempio, tenere presente quanto segue `packages.config` file nel progetto di origine:</span><span class="sxs-lookup"><span data-stu-id="e188b-173">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="e188b-174">Per questo progetto, il pacchetto creato da `nuget pack` avrà una dipendenza sulla `jQuery` e `microsoft-web-helpers` ma non `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="e188b-174">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="e188b-175">Esempi</span><span class="sxs-lookup"><span data-stu-id="e188b-175">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
