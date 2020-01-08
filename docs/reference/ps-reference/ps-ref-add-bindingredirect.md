---
title: Riferimenti per PowerShell Add-BindingRedirect di NuGet
description: Informazioni di riferimento per il comando Add-BindingRedirect di PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d3d156cf882229260e8cf55f8ece2804aec36dc9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384984"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (console di Gestione pacchetti in Visual Studio)

*Disponibile solo nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows.*

Esamina tutti gli assembly nel percorso di output di un progetto e aggiunge i reindirizzamenti di associazione al file di configurazione dell'applicazione o del Web, ove necessario. Questo comando viene eseguito automaticamente durante l'installazione di un pacchetto.

Per informazioni dettagliate sui reindirizzamenti di binding e sul motivo per cui vengono usati, vedere [Reindirizzamento delle versioni degli assembly](/dotnet/framework/configure-apps/redirect-assembly-versions) nella documentazione di .NET.

## <a name="syntax"></a>Sintassi

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| NomeProgetto | Necessaria Progetto a cui aggiungere reindirizzamenti di binding. L'opzione-ProjectName è facoltativa. |

Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Add-BindingRedirect` supporta i [parametri di PowerShell comuni](https://go.microsoft.com/fwlink/?LinkID=113216)seguenti: debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```