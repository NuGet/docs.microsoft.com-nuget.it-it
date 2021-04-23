---
title: Informazioni di riferimento Find-Package PowerShell per NuGet
description: Informazioni di Find-Package comando di PowerShell nella console Gestione pacchetti NuGet in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 263835da64340a13737b32ab54ab057cb640a080
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901759"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Gestione pacchetti Console in Visual Studio)

*Versione 3.0+; Questo argomento descrive il comando all'interno [della console Gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows. Per il comando di gestione Find-Package PowerShell generico, vedere le informazioni di [riferimento su PackageManagement di PowerShell.](/powershell/module/packagemanagement)*

Ottiene il set di pacchetti remoti con l'ID o le parole chiave specificati dall'origine del pacchetto.

## <a name="syntax"></a>Sintassi

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| Parole chiave &lt; id&gt; | (Obbligatorio) Parole chiave da usare durante la ricerca nell'origine del pacchetto. Usare -ExactMatch per restituire solo i pacchetti il cui ID pacchetto corrisponde alle parole chiave . Se non viene specificata alcuna parola chiave, restituisce un elenco dei primi 20 pacchetti per download o il `Find-Package` numero specificato da -First. Si noti che -Id è facoltativo e non operativo. |
| Source (Sorgente) | URL o percorso della cartella per l'origine del pacchetto in cui eseguire la ricerca. I percorsi delle cartelle locali possono essere assoluti o relativi alla cartella corrente. Se omesso, `Find-Package` cerca l'origine del pacchetto attualmente selezionata. |
| AllVersions | Visualizza tutte le versioni disponibili di ogni pacchetto anziché solo la versione più recente. |
| First (Primo) | Numero di pacchetti da restituire dall'inizio dell'elenco. il valore predefinito è 20. |
| Ignora | Omette i primi &lt; pacchetti int &gt; dall'elenco visualizzato.  |
| IncludePrerelease | Include i pacchetti in versione non definitiva nei risultati. |
| ExactMatch | Specificato per usare parole &lt; chiave come ID pacchetto con &gt; distinzione tra maiuscole e minuscole. |
| StartWith | Restituisce i pacchetti il cui ID pacchetto inizia con le &lt; parole chiave &gt; . |

Nessuno di questi parametri accetta l'input della pipeline o i caratteri jolly.

## <a name="common-parameters"></a>Parametri comuni

`Find-Package` supporta i parametri comuni di [PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters)seguenti: Debug, Azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```