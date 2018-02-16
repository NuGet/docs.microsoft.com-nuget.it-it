---
title: Riferimento di PowerShell di NuGet. Get-progetto | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando GetProject PowerShell nella Console di gestione pacchetti NuGet in Visual Studio.
keywords: Console di gestione, i comandi di Powershell di NuGet, riferimento di Powershell di NuGet, Get-progetto del pacchetto NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c347a6104d89bb29626ad7c2f33bec150eb38cd2
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-progetto (Console di gestione dei pacchetti in Visual Studio)

*Disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*

Visualizza informazioni sul valore predefinito o il progetto specificato. `Get-Project` in particolare, restituisce un riferimento per l'oggetto di Visual Studio DTE (Development Tools Environment) per il progetto.

## <a name="syntax"></a>Sintassi

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| nome | Specifica il progetto da visualizzare, verrà utilizzato per il progetto predefinito selezionato nella Console di gestione pacchetti. -Il nome del parametro è facoltativo. |
| Tutti | Visualizza informazioni per ogni progetto nella soluzione. l'ordine dei progetti non è deterministico. |

Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Get-Project` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```