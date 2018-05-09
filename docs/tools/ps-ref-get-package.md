---
title: Riferimento di PowerShell Get-pacchetto NuGet
description: Riferimento per il comando PowerShell Get-Package nella Console di gestione pacchetti NuGet in Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: c70e60b7391f19026e2dcd502d667fbe1da7e6e2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-pacchetto (Package Manager Console in Visual Studio)

*Questo argomento viene descritto il comando all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows. Per il comando PowerShell Get-Package generico, vedere il [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Recupera l'elenco di pacchetti installati nell'archivio locale, Elenca i pacchetti disponibili da un'origine del pacchetto quando si utilizza l'opzione - ListAvailable o elenca gli aggiornamenti disponibili quando si utilizza l'opzione-Update.

## <a name="syntax"></a>Sintassi

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Senza parametri, `Get-Package` Visualizza l'elenco dei pacchetti installati nel progetto predefinito.

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| Origine | Il percorso URL o una cartella per il pacchetto. I percorsi di cartella locale possono essere assoluto o relativo della cartella corrente. Se omesso, `Get-Package` Cerca l'origine pacchetto attualmente selezionata. Quando usato con - ListAvailable, per impostazione predefinita nuget.org. |
| ListAvailable | Elenca i pacchetti disponibili da un'origine del pacchetto, verrà utilizzato nuget.org. Mostra il valore predefinito è 50 pacchetti a meno che non vengono specificati - PageSize e/o - First. |
| Aggiornamenti | Elenca i pacchetti sono disponibile un aggiornamento dall'origine del pacchetto. |
| ProjectName | Il progetto da cui recuperare i pacchetti installati. Se omesso, restituisce installati progetti per l'intera soluzione. |
| Filtro | Una stringa di filtro utilizzata per limitare l'elenco dei pacchetti viene applicato per l'ID del pacchetto, la descrizione e tag. |
| First | Il numero di pacchetti da restituire dall'inizio dell'elenco. Se non specificato, per impostazione predefinita a 50. |
| Skip | Omette il primo &lt;int&gt; pacchetti nell'elenco visualizzato.  |
| Completaversioni | Visualizza tutte le versioni disponibili di ogni pacchetto anziché solo la versione più recente. |
| IncludePrerelease | Include i pacchetti non definitiva nei risultati. |
| PageSize | *(3.0 +)*  Quando usato con - ListAvailable (obbligatorio), il numero di pacchetti per visualizzare l'elenco prima di consegnare un prompt dei comandi per continuare. |

Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Get-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```
