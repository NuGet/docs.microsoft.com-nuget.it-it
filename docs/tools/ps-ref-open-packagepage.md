---
title: Riferimento di PowerShell di NuGet Open-PackagePage
description: Riferimento per il comando Apri PackagePage PowerShell nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e64a83c01a7baac330c99fe40ba52f328a2133b8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817720"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (console di Gestione pacchetti in Visual Studio)

*Deprecato in 3.0 +;) disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*

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

`Open-PackagePage` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

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