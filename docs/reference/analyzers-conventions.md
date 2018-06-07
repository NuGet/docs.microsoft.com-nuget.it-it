---
title: Formati di Analizzatore piattaforma del compilatore .NET per NuGet
description: Convenzioni per gli analizzatori .NET inseriti in un pacchetto e distribuiti con i pacchetti NuGet che implementano un'API o una libreria.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: dc5896631fa3b15dcc1b84b054cb532d56193f36
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818386"
---
# <a name="analyzer-nuget-formats"></a>Formati dell'analizzatore NuGet

.NET Compiler Platform (noto anche come "Roslyn") consentono agli sviluppatori di creare [analizzatori](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) che esaminare l'albero della sintassi e la semantica di codice mentre questa viene scritta. Ciò consente agli sviluppatori di creare strumenti di analisi specifici del dominio, come quelli che forniscono informazioni sull'uso di una particolare API o libreria. È possibile trovare altre informazioni sul wiki GitHub [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki). Vedere anche l'articolo [Usare Roslyn per scrivere un analizzatore di codice live per l'API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.

Gli analizzatori vengono in genere inseriti in pacchetti e distribuiti come parte dei pacchetti NuGet che implementano l'API o la libreria in questione.

Per un esempio, vedere il pacchetto [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers), con il contenuto seguente:

- analyzers\dotnet\System.Runtime.Analyzers.dll
- analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- tools\install.ps1
- tools\uninstall.ps1

Come si può notare, le DLL dell'analizzatore sono inserite in una cartella `analyzers` nel pacchetto.

I file con estensione props, inclusi per disabilitare le regole FxCop legacy a favore dell'implementazione dell'analizzatore, sono inseriti nella cartella `build`.

Gli script di installazione e disinstallazione che supportano i progetti che usano `packages.config` sono inseriti in `tools`.

Si noti inoltre che poiché il pacchetto non ha requisiti specifici per la piattaforma, la cartella `platform` viene omessa.


## <a name="analyzers-path-format"></a>Formato del percorso degli analizzatori

L'uso della cartella `analyzers` è analogo a quello per i [framework di destinazione](../create-packages/supporting-multiple-target-frameworks.md), con la differenza che gli identificatori nel percorso descrivono le dipendenze dell'host di sviluppo invece della fase di compilazione. Il formato generale è il seguente:

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}}/{analyzer_name}.dll

- **framework_name**: la superficie di attacco dell'API *opzionale* di .NET Framework che le DLL contenute devono eseguire. `dotnet` è attualmente l'unico valore valido perché Roslyn è l'unico host che può eseguire gli analizzatori. Se non è specificata alcuna destinazione, si presuppone che le DLL si applichino a *tutte* le destinazioni.
- **supported_language**: il linguaggio per cui si applica la DLL, uno tra `cs` (C#), `vb` (Visual Basic) e `fs` (F#). Il linguaggio indica che l'analizzatore deve essere caricato solo per un progetto che usa quel linguaggio. Se non è specificato alcun linguaggio, si presuppone che le DLL si applichino a *tutti* i linguaggi che supportano gli analizzatori.
- **analyzer_name**: specifica le DLL dell'analizzatore. Se sono necessari altri file oltre alle DLL, devono essere inclusi tramite un file di destinazioni o delle proprietà.


## <a name="install-and-uninstall-scripts"></a>Script di installazione e disinstallazione

Se il progetto dell'utente usa `packages.config`, lo script di MSBuild che rileva l'analizzatore non entra in gioco, pertanto sono necessari `install.ps1` e `uninstall.ps1` nella cartella `tools` con il contenuto descritto di seguito.

**Contenuto del file install.ps1**

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


**Contenuto del file uninstall.ps1**

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
