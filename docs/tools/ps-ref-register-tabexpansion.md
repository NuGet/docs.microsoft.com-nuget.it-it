---
title: Riferimento di PowerShell di NuGet. Register-TabExpansion
description: Riferimento per il comando Register-TabExpansion PowerShell nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8011c0e6aa951a32114d460803c493810964a7e0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818416"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (Console di gestione dei pacchetti in Visual Studio)

*Disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*

Registra l'espansione tramite tab per i parametri del comando specificato, in modo che quando scheda viene usata quando si immette un comando, i valori espansi vengono visualizzati come opzioni disponibili per il parametro in questione. Qualsiasi espansioni precedente per il comando vengono sovrascritti.

## <a name="syntax"></a>Sintassi

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| nome | (Obbligatorio) Il comando in cui registrare le espansioni. -Nome switch stesso è facoltativo. |
| Definizione | (Obbligatorio) Oggetto che descrive l'argomento nella sintassi `@{'<parameter>' = {'<value1>', '<value2>', ...}}` in `<parameter>` è il nome del parametro da modificare e ogni `<value>` fornisce una specifica espansione. Le virgolette singole e doppie vengono accettate. |

Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Register-TabExpansion` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

Prendere in considerazione una soluzione che contiene tre nomi di progetti EventManager, utilità e SpecialParser. Lo sviluppatore utilizza spesso il `Update-Package` comando in momenti diversi, ognuno di questi progetti. Individua consigliabile utilizzare il `Update-Package` comando forniscono le espansioni di completamento automatico per il `-ProjectName` argomento, quindi non necessita di digitare un nome di progetto ogni volta. 

Il comando seguente, quindi Registra i nomi di tre progetti come un'espansione per le `-ProjectName` parametro:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Lo sviluppatore può quindi digitare `Update-Package -ProjectName `, premere il tasto Tab e vedere le espansioni presentate come scelte di completamento automatico:

![Esempio di utilizzo registro TabExpansion](media/Register-TabExpansion-Example.png)
