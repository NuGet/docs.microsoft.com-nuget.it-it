---
title: Guida di riferimento a NuGet Register-TabExpansion PowerShell
description: Informazioni di riferimento per il comando Register-TabExpansion PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 9d5bae2878cb6bf0848bca9a5ed9af0fee61bb85
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237153"
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
| Nome | Necessaria Comando a cui registrare le espansioni. L'opzione-Name è facoltativa. |
| Definizione | Necessaria Oggetto che descrive l'argomento nella sintassi in `@{'<parameter>' = {'<value1>', '<value2>', ...}}` cui `<parameter>` è il nome del parametro da modificare e ognuno `<value>` fornisce un'espansione specifica. Vengono accettate le virgolette singole e doppie. |

Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Register-TabExpansion` supporta i seguenti [parametri comuni di PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

Si consideri una soluzione che contiene tre nomi di progetti EventManager, Utilities e SpecialParser. Lo sviluppatore usa spesso il `Update-Package` comando in momenti diversi con ognuno di questi progetti. Trova praticità che il `Update-Package` comando fornisca espansioni di completamento automatico per l' `-ProjectName` argomento in modo che non debba digitare ogni volta un nome di progetto. 

Il comando seguente, quindi, registra questi tre nomi di progetto come un'espansione per il `-ProjectName` parametro:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Lo sviluppatore può quindi digitare `Update-Package -ProjectName ` , premere TAB e visualizzare le espansioni offerte come opzioni di completamento automatico:

![Esempio di utilizzo di Register-TabExpansion](media/Register-TabExpansion-Example.png)