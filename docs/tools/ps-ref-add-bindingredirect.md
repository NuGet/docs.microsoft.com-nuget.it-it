---
title: Informazioni di riferimento di NuGet aggiungere-BindingRedirect PowerShell
description: Informazioni di riferimento per il comando di PowerShell Add-BindingRedirect nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5f318ddfb2bb8498ab3e608f8036be05dcb0706
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842533"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (console di Gestione pacchetti in Visual Studio)

*Disponibile solo all'interno di [Console di gestione pacchetti](package-manager-console.md) in Visual Studio in Windows.*

Esamina tutti gli assembly all'interno del percorso di output per un progetto e aggiunge reindirizzamenti di binding al file di configurazione dell'applicazione o web dove necessario. Questo comando viene eseguito automaticamente quando si installa un pacchetto.

Per informazioni dettagliate sull'associazione di reindirizzamenti e il motivo per cui vengono usati, vedere [reindirizzamento delle versioni degli Assembly](/dotnet/framework/configure-apps/redirect-assembly-versions) nella documentazione di .NET.

## <a name="syntax"></a>Sintassi

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| ProjectName | (Obbligatorio) Il progetto a cui aggiungere reindirizzamenti di associazione. L'opzione - nomeprogetto è facoltativo. |

Nessuno di questi parametri accettano caratteri jolly o input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Add-BindingRedirect` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```