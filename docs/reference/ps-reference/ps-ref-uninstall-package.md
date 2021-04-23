---
title: Informazioni di riferimento su NuGet Uninstall-Package PowerShell
description: Informazioni di Uninstall-Package comando di PowerShell nella console Gestione pacchetti NuGet in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 371e95c341efbce1c4a15facefc15cd51b266141
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901785"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Gestione pacchetti Console in Visual Studio)

*Questo argomento descrive il comando all'interno [della console Gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows. Per il comando powershell Uninstall-Package generico, vedere le informazioni di [riferimento su PackageManagement di PowerShell.](/powershell/module/packagemanagement)*

Rimuove un pacchetto da un progetto, rimuovendo facoltativamente le relative dipendenze. Se altri pacchetti dipendono da quello corrente, il comando ha esito negativo a meno che l'opzione –Force non sia specificata.

## <a name="syntax"></a>Sintassi

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Se altri pacchetti dipendono da quello corrente, il comando ha esito negativo a meno che l'opzione –Force non sia specificata.

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| Id | (Obbligatorio) Identificatore del pacchetto da disinstallare. L'opzione -Id è facoltativa. |
| Versione | Versione del pacchetto da disinstallare, che per impostazione predefinita è la versione attualmente installata. |
| RemoveDependencies | Disinstallare il pacchetto e le relative dipendenze inutilizzate. In altre informazioni, se una dipendenza ha un altro pacchetto che dipende da essa, viene ignorata. |
| ProjectName | Progetto da cui disinstallare il pacchetto, con il progetto predefinito. |
| Force | Forza la disinstallazione di un pacchetto, anche se altri pacchetti dipendono da esso. |
| WhatIf | Mostra cosa accade quando si esegue il comando senza eseguire effettivamente la disinstallazione. |

Nessuno di questi parametri accetta l'input della pipeline o i caratteri jolly.

## <a name="common-parameters"></a>Parametri comuni

`Uninstall-Package` supporta i parametri comuni di [PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters)seguenti: Debug, Azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```