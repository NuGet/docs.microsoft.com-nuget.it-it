---
title: Riferimento di PowerShell aggiungere BindingRedirect NuGet
description: Riferimento per il comando di PowerShell Add-BindingRedirect nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f3addd95b64d78eac201deeb2c64915ea935cd71
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817623"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (console di Gestione pacchetti in Visual Studio)

*Disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*

Esamina tutti gli assembly nel percorso di output per un progetto e aggiunge reindirizzamenti di binding al file di configurazione dell'applicazione o web, se necessario. Questo comando viene eseguito automaticamente quando si installa un pacchetto.

Per informazioni dettagliate sull'associazione di reindirizzamenti e perché vengono usati, vedere [reindirizzamento delle versioni degli Assembly](/dotnet/framework/configure-apps/redirect-assembly-versions) nella documentazione di .NET.

## <a name="syntax"></a>Sintassi

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| ProjectName | (Obbligatorio) Il progetto a cui aggiungere reindirizzamenti di associazione. L'opzione - ProjectName stesso è facoltativo. |

Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Add-BindingRedirect` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```