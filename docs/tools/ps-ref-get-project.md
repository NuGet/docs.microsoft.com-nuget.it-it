---
title: Riferimento di PowerShell Get-progetti per NuGet
description: Informazioni di riferimento per il comando GetProject PowerShell nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 849261711fafcadbab38bf6fe99340c4b79e1e21
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550437"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (console di Gestione pacchetti in Visual Studio)

*Disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*

Visualizza informazioni sull'impostazione predefinita o progetto specificato. `Get-Project` in particolare, restituisce un riferimento all'oggetto per il progetto di Visual Studio DTE (Development Tools Environment).

## <a name="syntax"></a>Sintassi

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| nome | Specifica il progetto per la visualizzazione, verrà utilizzato per il progetto predefinito selezionato nella Console di gestione pacchetti. -Nome del commutatore è a sua volta facoltativo. |
| Tutti | Visualizza le informazioni per ogni progetto nella soluzione; l'ordine dei progetti non è deterministico. |

Nessuno di questi parametri accettano caratteri jolly o input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Get-Project` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```