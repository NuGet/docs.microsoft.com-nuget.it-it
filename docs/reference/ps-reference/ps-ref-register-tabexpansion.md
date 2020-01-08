---
title: Registro NuGet-riferimenti PowerShell per TabExpansion
description: Riferimento per il comando Register-TabExpansion di PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 37aed96760e642b03c02bf31fe47a54f0e3cb74a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384454"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (console di gestione pacchetti in Visual Studio)

*Disponibile solo nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows.*

Registra un'espansione di tabulazione per i parametri del comando specificato, in modo che quando si immette un comando si utilizza TAB, i valori espansi vengono visualizzati come opzioni disponibili per il parametro in questione. Qualsiasi espansione precedente per il comando viene sovrascritta.

## <a name="syntax"></a>Sintassi

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| Name | Necessaria Comando a cui registrare le espansioni. L'opzione-Name è facoltativa. |
| Definizione | Necessaria Oggetto che descrive l'argomento nella sintassi `@{'<parameter>' = {'<value1>', '<value2>', ...}}` dove `<parameter>` è il nome del parametro da modificare e ogni `<value>` fornisce un'espansione specifica. Vengono accettate le virgolette singole e doppie. |

Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Register-TabExpansion` supporta i [parametri di PowerShell comuni](https://go.microsoft.com/fwlink/?LinkID=113216)seguenti: debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

Si consideri una soluzione che contiene tre nomi di progetti EventManager, Utilities e SpecialParser. Lo sviluppatore usa spesso il comando `Update-Package` in momenti diversi con ognuno di questi progetti. Trova la pratica di fare in modo che il comando `Update-Package` fornisca espansioni di completamento automatico per l'argomento `-ProjectName`, in modo che non sia necessario digitare ogni volta un nome di progetto. 

Il comando seguente, quindi, registra questi tre nomi di progetto come un'espansione per il parametro `-ProjectName`:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Lo sviluppatore può quindi digitare `Update-Package -ProjectName `, premere TAB e visualizzare le espansioni offerte come opzioni di completamento automatico:

![Esempio di uso di Register-TabExpansion](media/Register-TabExpansion-Example.png)
