---
title: Guida di riferimento a NuGet Get-Project PowerShell
description: Riferimento per il comando di PowerShell GetProject nella console di gestione pacchetti NuGet in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 16b3ffc0a375b8027c615020243a7289520715f8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777475"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (console di gestione pacchetti in Visual Studio)

*Disponibile solo nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows.*

Visualizza le informazioni relative al progetto predefinito o specificato. `Get-Project` in particolare, restituisce un referente all'oggetto DTE di Visual Studio (ambiente degli strumenti di sviluppo) per il progetto.

## <a name="syntax"></a>Sintassi

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| Nome | Specifica il progetto da visualizzare, per impostazione predefinita il progetto predefinito selezionato nella console di gestione pacchetti. L'opzione-Name è facoltativa. |
| Tutti | Visualizza le informazioni per ogni progetto nella soluzione. l'ordine dei progetti non è deterministico. |

Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Get-Project` supporta i seguenti [parametri comuni di PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```