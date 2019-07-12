---
title: Riferimento di PowerShell Register-TabExpansion NuGet
description: Informazioni di riferimento per il comando di PowerShell Register-TabExpansion nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8adb80af85e2e32fa8c35e5272cf90ff0c0ddcbb
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842491"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (Console di gestione pacchetti in Visual Studio)

*Disponibile solo all'interno di [Console di gestione pacchetti](package-manager-console.md) in Visual Studio in Windows.*

Registra un'espansione tramite tab per i parametri del comando specificato, in modo che quando scheda viene usata quando si immette un comando, i valori espansi vengono visualizzati come opzioni disponibili per il parametro in questione. Qualsiasi espansioni precedente per il comando vengono sovrascritti.

## <a name="syntax"></a>Sintassi

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| Name | (Obbligatorio) Il comando per cui si desidera registrare le espansioni. -Nome commutatore stesso è facoltativo. |
| Definizione | (Obbligatorio) Oggetto che descrive l'argomento nella sintassi `@{'<parameter>' = {'<value1>', '<value2>', ...}}` in cui `<parameter>` è il nome del parametro da modificare e ogni `<value>` fornisce un'espansione specifica. Le virgolette singole e doppie sono accettate. |

Nessuno di questi parametri accettano caratteri jolly o input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Register-TabExpansion` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

Prendere in considerazione una soluzione che contiene tre nomi di progetti EventManager, utilità e SpecialParser. Lo sviluppatore utilizza spesso il `Update-Package` comando in momenti diversi con ciascuno di questi progetti. Anna risulta utile avere la `Update-Package` comandi forniscono le espansioni di completamento automatico per il `-ProjectName` argomento in modo che non sono necessari per digitare un nome di progetto ogni volta. 

Il comando seguente, quindi Registra i nomi di tre progetti come un'espansione per il `-ProjectName` parametro:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Lo sviluppatore può quindi digitare `Update-Package -ProjectName `, premere Tab e vedere le espansioni presentate come scelte di completamento automatico:

![Esempio dell'uso di Register-TabExpansion](media/Register-TabExpansion-Example.png)
