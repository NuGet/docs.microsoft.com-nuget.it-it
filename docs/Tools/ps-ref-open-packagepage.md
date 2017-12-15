---
title: Riferimento di PowerShell di NuGet Open-PackagePage | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: e9f84530-6b3d-43b0-a832-0acb2997f6fc
description: Riferimento per il comando Apri PackagePage PowerShell nella Console di gestione pacchetti NuGet in Visual Studio.
keywords: Console di gestione, i comandi di Powershell di NuGet, riferimenti di NuGet Powershell, aprire PackagePage del pacchetto NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ec4310ea9d13926b1cb3b227b17016742a70bc16
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Apri-PackagePage (Console di gestione dei pacchetti in Visual Studio)

*Deprecato in 3.0 +;) disponibile solo all'interno di [Console di gestione pacchetti NuGet](Package-Manager-Console.md) in Visual Studio in Windows.*

Avvia il browser predefinito con il progetto, licenza o report abuso URL per il pacchetto specificato.

## <a name="syntax"></a>Sintassi

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| Id | L'ID del pacchetto del pacchetto desiderato. -Id switch stesso è facoltativo. |
| Versione | La versione del pacchetto, verrà utilizzato per la versione più recente. |
| Origine | L'origine del pacchetto, verrà utilizzato per l'origine selezionata nell'elenco a discesa di origine. |
| Licenza | Apre il browser all'URL di licenza del pacchetto. Se viene specificato - licenza né - ReportAbuse, si apre il browser con URL di progetto del pacchetto. |
| ReportAbuse | Apre il browser all'URL di evitare eventuali abusi Report del pacchetto. Se viene specificato - licenza né - ReportAbuse, si apre il browser con URL di progetto del pacchetto. |
| PassThru | Visualizza l'URL; utilizzare con - WhatIf esclusione aprendo il browser. |

Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Open-PackagePage`supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```