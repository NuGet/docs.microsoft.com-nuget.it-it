---
title: Formati dell'analizzatore di .NET Compiler Platform per NuGet
description: Convenzioni per gli analizzatori .NET inseriti in un pacchetto e distribuiti con i pacchetti NuGet che implementano un'API o una libreria.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0a8db9f6c55b7e79f9b338119e0b3ac6cb7a1e35
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520511"
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="b728b-103">Formati dell'analizzatore NuGet</span><span class="sxs-lookup"><span data-stu-id="b728b-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="b728b-104">.NET Compiler Platform (noto anche come "Roslyn") consente agli sviluppatori di creare [analizzatori](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) che esaminano l'albero della sintassi e la semantica del codice durante la scrittura.</span><span class="sxs-lookup"><span data-stu-id="b728b-104">The .NET Compiler Platform (also known as "Roslyn") allows developers to create [analyzers](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="b728b-105">In questo modo gli sviluppatori possono creare strumenti di analisi specifici del dominio, come quelli che forniscono informazioni sull'uso di una particolare API o libreria.</span><span class="sxs-lookup"><span data-stu-id="b728b-105">This provides developers with a way to create domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="b728b-106">È possibile trovare altre informazioni sul wiki GitHub [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki).</span><span class="sxs-lookup"><span data-stu-id="b728b-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="b728b-107">Vedere anche l'articolo [Usare Roslyn per scrivere un analizzatore di codice live per l'API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span><span class="sxs-lookup"><span data-stu-id="b728b-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span></span>

<span data-ttu-id="b728b-108">Gli analizzatori vengono in genere inseriti in pacchetti e distribuiti come parte dei pacchetti NuGet che implementano l'API o la libreria in questione.</span><span class="sxs-lookup"><span data-stu-id="b728b-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="b728b-109">Per un esempio, vedere il pacchetto [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers), con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="b728b-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="b728b-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="b728b-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="b728b-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="b728b-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="b728b-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="b728b-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="b728b-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="b728b-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="b728b-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="b728b-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="b728b-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="b728b-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="b728b-116">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="b728b-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="b728b-117">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="b728b-117">tools\install.ps1</span></span>
- <span data-ttu-id="b728b-118">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="b728b-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="b728b-119">Come si può notare, le DLL dell'analizzatore sono inserite in una cartella `analyzers` nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="b728b-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="b728b-120">I file con estensione props, inclusi per disabilitare le regole FxCop legacy a favore dell'implementazione dell'analizzatore, sono inseriti nella cartella `build`.</span><span class="sxs-lookup"><span data-stu-id="b728b-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="b728b-121">Gli script di installazione e disinstallazione che supportano i progetti che usano `packages.config` sono inseriti in `tools`.</span><span class="sxs-lookup"><span data-stu-id="b728b-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="b728b-122">Si noti inoltre che poiché il pacchetto non ha requisiti specifici per la piattaforma, la cartella `platform` viene omessa.</span><span class="sxs-lookup"><span data-stu-id="b728b-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="b728b-123">Formato del percorso degli analizzatori</span><span class="sxs-lookup"><span data-stu-id="b728b-123">Analyzers path format</span></span>

<span data-ttu-id="b728b-124">L'uso della cartella `analyzers` è analogo a quello per i [framework di destinazione](../create-packages/supporting-multiple-target-frameworks.md), con la differenza che gli identificatori nel percorso descrivono le dipendenze dell'host di sviluppo invece della fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="b728b-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="b728b-125">Il formato generale è il seguente:</span><span class="sxs-lookup"><span data-stu-id="b728b-125">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- <span data-ttu-id="b728b-126">**framework_name**: la superficie di attacco dell'API *opzionale* di .NET Framework che le DLL contenute devono eseguire.</span><span class="sxs-lookup"><span data-stu-id="b728b-126">**framework_name**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="b728b-127">`dotnet` è attualmente l'unico valore valido perché Roslyn è l'unico host che può eseguire gli analizzatori.</span><span class="sxs-lookup"><span data-stu-id="b728b-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="b728b-128">Se non è specificata alcuna destinazione, si presuppone che le DLL si applichino a *tutte* le destinazioni.</span><span class="sxs-lookup"><span data-stu-id="b728b-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="b728b-129">**supported_language**: il linguaggio per cui si applica la DLL, uno tra `cs` (C#), `vb` (Visual Basic) e `fs` (F#).</span><span class="sxs-lookup"><span data-stu-id="b728b-129">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="b728b-130">Il linguaggio indica che l'analizzatore deve essere caricato solo per un progetto che usa quel linguaggio.</span><span class="sxs-lookup"><span data-stu-id="b728b-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="b728b-131">Se non è specificato alcun linguaggio, si presuppone che la DLL sia applicabile a *tutti* i linguaggi che supportano gli analizzatori.</span><span class="sxs-lookup"><span data-stu-id="b728b-131">If no language is specified then the DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="b728b-132">**analyzer_name**: specifica le DLL dell'analizzatore.</span><span class="sxs-lookup"><span data-stu-id="b728b-132">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="b728b-133">Se sono necessari altri file oltre alle DLL, devono essere inclusi tramite un file di destinazioni o delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="b728b-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="b728b-134">Script di installazione e disinstallazione</span><span class="sxs-lookup"><span data-stu-id="b728b-134">Install and uninstall scripts</span></span>

<span data-ttu-id="b728b-135">Se il progetto dell'utente usa `packages.config`, lo script di MSBuild che rileva l'analizzatore non entra in gioco, pertanto è necessario posizionare `install.ps1` e `uninstall.ps1` nella cartella `tools` con il contenuto descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="b728b-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should place `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="b728b-136">**Contenuto del file install.ps1**</span><span class="sxs-lookup"><span data-stu-id="b728b-136">**install.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Install the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Install language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}
```


<span data-ttu-id="b728b-137">**Contenuto del file uninstall.ps1**</span><span class="sxs-lookup"><span data-stu-id="b728b-137">**uninstall.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                try
                {
                    $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
                }
                catch
                {

                }
            }
        }
    }
}
```