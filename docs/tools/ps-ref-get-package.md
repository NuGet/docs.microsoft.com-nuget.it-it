---
title: Riferimento di PowerShell Get-pacchetto NuGet
description: Informazioni di riferimento per il comando PowerShell Get-Package nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d0d25cb6e21f6d0d42389e08340b6f1e1baf8a64
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842509"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (console di Gestione pacchetti in Visual Studio)

*In questo argomento descrive il comando all'interno di [Console di gestione pacchetti](package-manager-console.md) in Visual Studio in Windows. Per il comando PowerShell Get-Package generico, vedere la [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Recupera l'elenco dei pacchetti installati nel repository locale, sono elencati i pacchetti disponibili da un'origine del pacchetto quando usato con l'opzione - ListAvailable o elenca gli aggiornamenti disponibili quando usato con l'opzione-Update.

## <a name="syntax"></a>Sintassi

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Senza parametri, `Get-Package` consente di visualizzare l'elenco dei pacchetti installati nel progetto predefinito.

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| `Source` | Il percorso URL o una cartella per il pacchetto. I percorsi di cartella locale possono essere assoluto o relativo rispetto alla cartella corrente. Se omesso, `Get-Package` Cerca l'origine del pacchetto attualmente selezionata. Quando usato con - ListAvailable, per impostazione predefinita in nuget.org. |
| ListAvailable | Elenca i pacchetti disponibili da un'origine del pacchetto, verrà utilizzato in nuget.org. Mostra un valore predefinito di 50 pacchetti a meno che non vengono specificati - PageSize e/o - First. |
| Aggiornamenti | Elenca i pacchetti che hanno un aggiornamento disponibile dall'origine del pacchetto. |
| ProjectName | Il progetto da cui ottenere i pacchetti installati. Se omesso, restituisce installati progetti per l'intera soluzione. |
| Filtro | Una stringa di filtro utilizzata per limitare l'elenco dei pacchetti viene applicato per l'ID del pacchetto, la descrizione e tag. |
| Primo | Il numero di pacchetti da restituire dall'inizio dell'elenco. Se non specificato, valore predefinito è 50. |
| Skip | Omette il primo &lt;int&gt; pacchetti nell'elenco visualizzato.  |
| AllVersions | Consente di visualizzare tutte le versioni disponibili di ogni pacchetto invece solo la versione più recente. |
| IncludePrerelease | Include pacchetti versione non definitivo nei risultati. |
| PageSize | *(3.0 e versioni successive)*  Quando utilizzato con - ListAvailable (obbligatorio), il numero di pacchetti per ottenere l'elenco prima di fornire un prompt dei comandi per continuare. |

Nessuno di questi parametri accettano caratteri jolly o input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Get-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction e WarningVariable.

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
