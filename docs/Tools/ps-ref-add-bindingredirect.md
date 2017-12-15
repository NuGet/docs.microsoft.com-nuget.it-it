---
title: Riferimento di PowerShell di NuGet BindingRedirect aggiungere | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 90f4dcb0-6e5a-4948-8ea9-62e0d061d95a
description: Riferimento per il comando di PowerShell Add-BindingRedirect nella Console di gestione pacchetti NuGet in Visual Studio.
keywords: Console di gestione, i comandi di Powershell di NuGet, riferimento di Powershell di NuGet, Aggiungi BindingRedirect del pacchetto NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7bf8cdb938195f4747932b38ef0d5bb6c34b9137
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Aggiungere-BindingRedirect (Console di gestione dei pacchetti in Visual Studio)

*Disponibile solo all'interno di [Console di gestione pacchetti NuGet](Package-Manager-Console.md) in Visual Studio in Windows.*

Esamina tutti gli assembly nel percorso di output per un progetto e aggiunge reindirizzamenti di binding al file di configurazione dell'applicazione o web, se necessario. Questo comando viene eseguito automaticamente quando si installa un pacchetto.

Per informazioni dettagliate sull'associazione di reindirizzamenti e perché vengono usati, vedere [reindirizzamento delle versioni degli Assembly](https://docs.microsoft.com/dotnet/framework/configure-apps/redirect-assembly-versions) nella documentazione di .NET.

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

`Add-BindingRedirect`supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```