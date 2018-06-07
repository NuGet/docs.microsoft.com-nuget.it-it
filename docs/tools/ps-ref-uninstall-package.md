---
title: Riferimento di PowerShell di NuGet Uninstall-Package
description: Riferimento per il comando di PowerShell Uninstall-Package nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 860a58c359c9b723564a70f83aee4eee5cebf16d
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818867"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (console di Gestione pacchetti in Visual Studio)

*Questo argomento viene descritto il comando all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows. Per il comando PowerShell Uninstall-Package generico, vedere il [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Rimuove un pacchetto da un progetto, rimuovere facoltativamente le relative dipendenze. Se altri pacchetti dipendono da questo pacchetto, il comando avrà esito negativo a meno che non – Force non sia specificata l'opzione.

## <a name="syntax"></a>Sintassi

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Se altri pacchetti dipendono da questo pacchetto, il comando avrà esito negativo a meno che non – Force non sia specificata l'opzione.

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| Id | (Obbligatorio) L'identificatore del pacchetto da disinstallare. -Id switch stesso è facoltativo. |
| Versione | La versione del pacchetto da disinstallare, verrà utilizzato per la versione attualmente installata. |
| RemoveDependencies | Disinstallare il pacchetto e delle relative dipendenze non utilizzate. Vale a dire, se tutte le dipendenze dispone di un altro pacchetto dipendente, viene ignorato. |
| ProjectName | Il progetto da cui disinstallare il pacchetto, verrà utilizzato per il progetto predefinito. |
| Force | Forza un pacchetto da disinstallare, anche se altri pacchetti dipendono da esso. |
| WhatIf | Viene illustrato che cosa accadrebbe eseguendo il comando senza eseguire effettivamente la disinstallazione. |

Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Uninstall-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
