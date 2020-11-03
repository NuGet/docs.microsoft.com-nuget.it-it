---
title: Guida di riferimento a NuGet Uninstall-Package PowerShell
description: Informazioni di riferimento per il comando Uninstall-Package PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: d164176355e32e5bbe0a017fc2b291cbc9ef326a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237127"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (console di gestione pacchetti in Visual Studio)

*In questo argomento viene descritto il comando nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows. Per il comando generico di Uninstall-Package PowerShell, vedere le informazioni di [riferimento su PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

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
| ID | Necessaria Identificatore del pacchetto da disinstallare. L'opzione-ID è facoltativa. |
| Versione | Versione del pacchetto da disinstallare, per impostazione predefinita la versione attualmente installata. |
| RemoveDependencies | Disinstallare il pacchetto e le relative dipendenze non utilizzate. Ovvero, se una dipendenza dispone di un altro pacchetto che dipende da esso, viene ignorato. |
| ProjectName | Progetto da cui disinstallare il pacchetto, per impostazione predefinita il progetto predefinito. |
| Force | Forza la disinstallazione di un pacchetto, anche se altri pacchetti dipendono da esso. |
| WhatIf | Mostra cosa accade quando si esegue il comando senza eseguire effettivamente la disinstallazione. |

Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Uninstall-Package` supporta i seguenti [parametri comuni di PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```