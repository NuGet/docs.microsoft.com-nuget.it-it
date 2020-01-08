---
title: Guida di riferimento a NuGet Get-Project PowerShell
description: Riferimento per il comando di PowerShell GetProject nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 3343952535c2d3c822f5cac24cb30c8f5bfa5be3
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384620"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (console di Gestione pacchetti in Visual Studio)

*Disponibile solo nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows.*

Visualizza le informazioni relative al progetto predefinito o specificato. `Get-Project` restituisce in modo specifico un oggetto referente all'oggetto DTE di Visual Studio (ambiente degli strumenti di sviluppo) per il progetto.

## <a name="syntax"></a>Sintassi

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| Name | Specifica il progetto da visualizzare, per impostazione predefinita il progetto predefinito selezionato nella console di gestione pacchetti. L'opzione-Name è facoltativa. |
| Tutte le | Visualizza le informazioni per ogni progetto nella soluzione. l'ordine dei progetti non è deterministico. |

Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Get-Project` supporta i [parametri di PowerShell comuni](https://go.microsoft.com/fwlink/?LinkID=113216)seguenti: debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```