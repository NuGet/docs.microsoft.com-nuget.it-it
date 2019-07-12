---
title: Informazioni di riferimento di NuGet Open-PackagePage PowerShell
description: Informazioni di riferimento per il comando PowerShell Open-PackagePage nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fd738f15b461051c4e9413b3035456c687979b97
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842270"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (console di Gestione pacchetti in Visual Studio)

*Deprecato in 3.0 e versioni successive; disponibile solo all'interno di [Console di gestione pacchetti](package-manager-console.md) in Visual Studio in Windows.*

Avvia il browser predefinito con il progetto, licenza o URL per segnalare abusi per il pacchetto specificato.

## <a name="syntax"></a>Sintassi

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| ID | L'ID del pacchetto del pacchetto desiderato. -Id commutatore stesso è facoltativo. |
| Version | La versione del pacchetto, verrà utilizzato per la versione più recente. |
| `Source` | L'origine del pacchetto, verrà utilizzato per l'origine selezionata nell'elenco a discesa di origine. |
| Licenza | Apre il browser all'URL della licenza del pacchetto. Se viene specificato - licenza né - ReportAbuse, nel browser verrà aperta URL del progetto del pacchetto. |
| ReportAbuse | Apre il browser all'URL per segnalare abusi del pacchetto. Se viene specificato - licenza né - ReportAbuse, nel browser verrà aperta URL del progetto del pacchetto. |
| PassThru | Viene visualizzato l'URL; usare con - WhatIf per non visualizzare aprendo il browser. |

Nessuno di questi parametri accettano caratteri jolly o input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Open-PackagePage` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction e WarningVariable.

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