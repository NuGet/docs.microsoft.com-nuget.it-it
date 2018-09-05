---
title: Riferimento di PowerShell di NuGet Uninstall-Package
description: Informazioni di riferimento per il comando PowerShell Uninstall-Package nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ae60473fbb716b23f40b0605be8aaa8515802315
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551643"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (console di Gestione pacchetti in Visual Studio)

*In questo argomento descrive il comando all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows. Per il comando PowerShell Uninstall-Package generico, vedere la [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Rimuove un pacchetto da un progetto, se lo si desidera rimuovere le relative dipendenze. Se altri pacchetti dipendono da questo pacchetto, il comando avrà esito negativo a meno che non – Force è specificata l'opzione.

## <a name="syntax"></a>Sintassi

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Se altri pacchetti dipendono da questo pacchetto, il comando avrà esito negativo a meno che non – Force è specificata l'opzione.

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| Id | (Obbligatorio) L'identificatore del pacchetto da disinstallare. -Id commutatore stesso è facoltativo. |
| Versione | La versione del pacchetto da disinstallare, verrà utilizzato per la versione attualmente installata. |
| RemoveDependencies | Disinstallare il pacchetto e le relative dipendenze inutilizzati. Vale a dire, se tutte le dipendenze dispone di un altro pacchetto dipendente, si viene ignorato. |
| ProjectName | Il progetto da cui disinstallare il pacchetto, verrà utilizzato per il progetto predefinito. |
| Force | Forza un pacchetto da disinstallare, anche se altri pacchetti dipendono da esso. |
| WhatIf | Viene illustrato che cosa accadrebbe quando si esegue il comando senza eseguire effettivamente la disinstallazione. |

Nessuno di questi parametri accettano caratteri jolly o input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Uninstall-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
