---
title: Guida di riferimento a NuGet Get-Package PowerShell
description: Informazioni di riferimento per il comando Get-Package PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 1576e3f20eba1ecdd099b1e7c23aef6b1a1a0a4f
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237231"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (console di gestione pacchetti in Visual Studio)

*In questo argomento viene descritto il comando nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows. Per il comando generico di Get-Package PowerShell, vedere le informazioni di [riferimento su PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Recupera l'elenco dei pacchetti installati nel repository locale, elenca i pacchetti disponibili da un'origine del pacchetto quando viene usato con l'opzione-ListAvailable oppure elenca gli aggiornamenti disponibili se usati con l'opzione-Update.

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
| Source (Sorgente) | URL o percorso della cartella per il pacchetto. I percorsi delle cartelle locali possono essere assoluti o relativi alla cartella corrente. Se omesso, `Get-Package` Cerca nell'origine del pacchetto attualmente selezionata. Se usato con-ListAvailable, il valore predefinito è nuget.org. |
| ListAvailable | Elenca i pacchetti disponibili da un'origine del pacchetto, per impostazione predefinita nuget.org. Mostra un valore predefinito di 50 pacchetti, a meno che non siano specificati-PageSize e/o-First. |
| Aggiornamenti | Elenca i pacchetti per i quali è disponibile un aggiornamento dall'origine del pacchetto. |
| ProjectName | Progetto da cui ottenere i pacchetti installati. Se omesso, restituisce i progetti installati per l'intera soluzione. |
| Filtro | Stringa di filtro utilizzata per restringere l'elenco dei pacchetti mediante l'applicazione dell'ID, della descrizione e dei tag del pacchetto. |
| First (Primo) | Numero di pacchetti da restituire dall'inizio dell'elenco. Se non è specificato, il valore predefinito è 50. |
| Ignora | Omette i primi &lt; pacchetti int &gt; dall'elenco visualizzato.  |
| AllVersions | Visualizza tutte le versioni disponibili di ogni pacchetto anziché solo la versione più recente. |
| IncludePrerelease | Include i pacchetti di versioni non definitive nei risultati. |
| PageSize | *(3.0 +)* Se usato con-ListAvailable (obbligatorio), il numero di pacchetti da elencare prima di fornire un prompt per continuare. |

Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Get-Package` supporta i seguenti [parametri comuni di PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

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