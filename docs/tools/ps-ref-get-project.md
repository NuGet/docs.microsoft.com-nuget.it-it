---
title: Riferimento di PowerShell Get-progetti per NuGet
description: Informazioni di riferimento per il comando GetProject PowerShell nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 2ceb1557eafd213c148d3ab870925ef5bbbee145
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842273"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (console di Gestione pacchetti in Visual Studio)

*Disponibile solo all'interno di [Console di gestione pacchetti](package-manager-console.md) in Visual Studio in Windows.*

Visualizza informazioni sull'impostazione predefinita o progetto specificato. `Get-Project` in particolare, restituisce un riferimento all'oggetto per il progetto di Visual Studio DTE (Development Tools Environment).

## <a name="syntax"></a>Sintassi

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| NOME | Specifica il progetto per la visualizzazione, verrà utilizzato per il progetto predefinito selezionato nella Console di gestione pacchetti. -Nome del commutatore è a sua volta facoltativo. |
| Tutti | Visualizza le informazioni per ogni progetto nella soluzione; l'ordine dei progetti non è deterministico. |

Nessuno di questi parametri accettano caratteri jolly o input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Get-Project` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```