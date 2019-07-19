---
title: Guida di riferimento a NuGet Uninstall-Package PowerShell
description: Informazioni di riferimento sul comando Uninstall-package di PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5c963588d28cab42e5fb6a43b31a17e26e49d0d2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327278"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (console di Gestione pacchetti in Visual Studio)

*In questo argomento viene descritto il comando nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows. Per il comando generico Uninstall-package di PowerShell, vedere le informazioni di [riferimento su PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Rimuove un pacchetto da un progetto, rimuovendo facoltativamente le relative dipendenze. Se gli altri pacchetti dipendono da questo pacchetto, il comando avrà esito negativo a meno che non venga specificata l'opzione-Force.

## <a name="syntax"></a>Sintassi

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Se gli altri pacchetti dipendono da questo pacchetto, il comando avrà esito negativo a meno che non venga specificata l'opzione-Force.

## <a name="parameters"></a>Parametri

| Parametro | DESCRIZIONE |
| --- | --- |
| ID | Necessaria Identificatore del pacchetto da disinstallare. L'opzione-ID è facoltativa. |
| Version | Versione del pacchetto da disinstallare, per impostazione predefinita la versione attualmente installata. |
| RemoveDependencies | Disinstallare il pacchetto e le relative dipendenze non utilizzate. Ovvero, se una dipendenza dispone di un altro pacchetto che dipende da esso, viene ignorato. |
| ProjectName | Progetto da cui disinstallare il pacchetto, per impostazione predefinita il progetto predefinito. |
| Force | Forza la disinstallazione di un pacchetto, anche se altri pacchetti dipendono da esso. |
| Whatif | Mostra cosa accade quando si esegue il comando senza eseguire effettivamente la disinstallazione. |

Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Uninstall-Package`supporta i seguenti [parametri comuni di PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
