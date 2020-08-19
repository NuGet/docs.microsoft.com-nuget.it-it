---
title: Riferimenti per PowerShell Add-BindingRedirect di NuGet
description: Informazioni di riferimento per il comando Add-BindingRedirect di PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f5ba4bd8140fa8cac7da8bf1351ad5448671b768
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623123"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (console di gestione pacchetti in Visual Studio)

*Disponibile solo nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows.*

Esamina tutti gli assembly nel percorso di output di un progetto e aggiunge i reindirizzamenti di associazione al file di configurazione dell'applicazione o del Web, ove necessario. Questo comando viene eseguito automaticamente durante l'installazione di un pacchetto.

> [!NOTE]
> Questo vale solo per gli scenari che usano un file di packages.config. Per altre informazioni, vedere Guida di [riferimento ai file di packages.config NuGet](~/reference/packages-config.md).

Per informazioni dettagliate sui reindirizzamenti di binding e sul motivo per cui vengono usati, vedere [Reindirizzamento delle versioni degli assembly](/dotnet/framework/configure-apps/redirect-assembly-versions) nella documentazione di .NET.

## <a name="syntax"></a>Sintassi

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| ProjectName | Necessaria Progetto a cui aggiungere reindirizzamenti di binding. L'opzione-ProjectName è facoltativa. |

Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Add-BindingRedirect` supporta i seguenti [parametri comuni di PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```
