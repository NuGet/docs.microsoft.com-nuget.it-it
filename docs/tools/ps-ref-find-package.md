---
title: Riferimento di PowerShell di NuGet. Find-Package
description: Informazioni di riferimento per il comando di PowerShell di Find-Package nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: fee0ad0496f27d0796eddf177edc235bcb10da70
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842530"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (console di Gestione pacchetti in Visual Studio)

*Versione 3.0 e versioni successive; In questo argomento descrive il comando all'interno di [Console di gestione pacchetti](package-manager-console.md) in Visual Studio in Windows. Per il comando di PowerShell. Find-Package generico, vedere la [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Ottiene il set di pacchetti remoti con ID specificato oppure le parole chiave dall'origine del pacchetto.

## <a name="syntax"></a>Sintassi

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | DESCRIZIONE |
| --- | --- |
| ID &lt;parole chiave&gt; | (Obbligatorio) Parole chiave da usare durante la ricerca dell'origine del pacchetto. Utilizzare - ExactMatch per restituire solo i pacchetti il cui ID pacchetto corrisponde a parole chiave. Se nessuna parola chiave vengono specificata, `Find-Package` restituisce un elenco dei primi 20 pacchetti download o il numero specificato da - prima di tutto. Si noti che - Id è facoltativo e no-op. |
| `Source` | Il percorso URL o una cartella per l'origine del pacchetto da cercare. I percorsi di cartella locale possono essere assoluto o relativo rispetto alla cartella corrente. Se omesso, `Find-Package` Cerca l'origine del pacchetto attualmente selezionata. |
| AllVersions | Consente di visualizzare tutte le versioni disponibili di ogni pacchetto invece solo la versione più recente. |
| Primo | Il numero di pacchetti da restituire dall'inizio dell'elenco; il valore predefinito è 20. |
| Skip | Omette il primo &lt;int&gt; pacchetti nell'elenco visualizzato.  |
| IncludePrerelease | Include pacchetti versione non definitivo nei risultati. |
| ExactMatch | Specificato da utilizzare &lt;parole chiave&gt; come un ID pacchetto distinzione maiuscole/minuscole. |
| StartWith | Restituisce i pacchetti il cui pacchetto ID inizia con &lt;parole chiave&gt;. |

Nessuno di questi parametri accettano caratteri jolly o input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Find-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```
