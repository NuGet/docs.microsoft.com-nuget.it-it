---
title: Informazioni di riferimento Get-Package PowerShell per NuGet
description: Informazioni di Get-Package comando di PowerShell nella console Gestione pacchetti NuGet in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7c91faecaac2967c7a01dd81e72b9097e7bd6cae
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901733"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Gestione pacchetti Console in Visual Studio)

*Questo argomento descrive il comando all'interno [della console Gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows. Per il comando di gestione Get-Package PowerShell generico, vedere le informazioni di [riferimento su PackageManagement di PowerShell.](/powershell/module/packagemanagement)*

Recupera l'elenco dei pacchetti installati nel repository locale, elenca i pacchetti disponibili da un'origine del pacchetto se usati con l'opzione -ListAvailable oppure elenca gli aggiornamenti disponibili quando vengono usati con l'opzione -Update.

## <a name="syntax"></a>Sintassi

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Senza parametri, `Get-Package` visualizza l'elenco dei pacchetti installati nel progetto predefinito.

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| Source (Sorgente) | URL o percorso della cartella per il pacchetto . I percorsi delle cartelle locali possono essere assoluti o relativi alla cartella corrente. Se omesso, `Get-Package` cerca l'origine del pacchetto attualmente selezionata. Se usato con -ListAvailable, il valore predefinito è nuget.org. |
| ListAvailable | Elenca i pacchetti disponibili da un'origine pacchetto, che per impostazione predefinita nuget.org. Mostra un valore predefinito di 50 pacchetti, a meno che non siano specificati -PageSize e/o -First. |
| Aggiornamenti | Elenca i pacchetti che dispongono di un aggiornamento disponibile dall'origine del pacchetto. |
| ProjectName | Progetto da cui ottenere i pacchetti installati. Se omesso, restituisce i progetti installati per l'intera soluzione. |
| Filtra | Stringa di filtro utilizzata per restringere l'elenco di pacchetti applicandolo all'ID, alla descrizione e ai tag del pacchetto. |
| First (Primo) | Numero di pacchetti da restituire dall'inizio dell'elenco. Se non specificato, il valore predefinito è 50. |
| Ignora | Omette i primi &lt; pacchetti int &gt; dall'elenco visualizzato.  |
| AllVersions | Visualizza tutte le versioni disponibili di ogni pacchetto anziché solo la versione più recente. |
| IncludePrerelease | Include i pacchetti di versione non definitiva nei risultati. |
| PageSize | *(3.0+)* Se usato con -ListAvailable (obbligatorio), il numero di pacchetti da elencare prima di chiedere di continuare. |

Nessuno di questi parametri accetta l'input della pipeline o i caratteri jolly.

## <a name="common-parameters"></a>Parametri comuni

`Get-Package` supporta i parametri comuni di [PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters)seguenti: Debug, Azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

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