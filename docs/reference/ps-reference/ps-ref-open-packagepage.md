---
title: Guida di riferimento a NuGet Open-PackagePage PowerShell
description: Informazioni di riferimento per il comando Open-PackagePage PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ba90e09c017ec66d73c35a60025474bc77cf65a7
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238062"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (console di gestione pacchetti in Visual Studio)

*Deprecato in 3.0 +; disponibile solo nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows.*

Avvia il browser predefinito con l'URL del progetto, della licenza o dell'abuso del report per il pacchetto specificato.

## <a name="syntax"></a>Sintassi

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| ID | ID del pacchetto desiderato. L'opzione-ID è facoltativa. |
| Versione | Versione del pacchetto, per impostazione predefinita la versione più recente. |
| Source (Sorgente) | Origine del pacchetto, per impostazione predefinita l'origine selezionata nell'elenco a discesa origine. |
| Licenza | Apre il browser all'URL di licenza del pacchetto. Se non si specifica né-License né-ReportAbuse, il browser apre l'URL del progetto del pacchetto. |
| ReportAbuse | Apre il browser all'URL di utilizzo del report del pacchetto. Se non si specifica né-License né-ReportAbuse, il browser apre l'URL del progetto del pacchetto. |
| PassThru | Visualizza l'URL. usare con-WhatIf per non visualizzare l'apertura del browser. |

Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Open-PackagePage` supporta i seguenti [parametri comuni di PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

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