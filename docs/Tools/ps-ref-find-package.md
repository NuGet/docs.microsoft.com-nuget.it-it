---
title: Riferimento di PowerShell di NuGet. Find-Package | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 2f7b8847-8259-4366-98c0-13cab88d6e1b
description: Riferimento per il comando di PowerShell di Find-Package nella Console di gestione pacchetti NuGet in Visual Studio.
keywords: Creare un pacchetto NuGet console di gestione, i comandi di Powershell di NuGet, riferimento di Powershell di NuGet, Find-Package
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fb55cc71e0d4b8eee28b232e64d2cc42364fc153
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Package Manager Console in Visual Studio)

*Versione 3.0; questo argomento viene descritto il comando all'interno di [Console di gestione pacchetti NuGet](Package-Manager-Console.md) in Visual Studio in Windows. Per il comando di PowerShell. Find-Package generico, vedere il [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Ottiene il set di pacchetti remoti con parole chiave o un ID specificato dall'origine del pacchetto.

## <a name="syntax"></a>Sintassi

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| ID &lt;parole chiave&gt; | (Obbligatorio) Parole chiave per la ricerca dell'origine del pacchetto. Utilizzare - ExactMatch per restituire solo i pacchetti il cui ID di pacchetto consente di ricercare le parole chiave. Se nessuna parola chiave vengono specificata, `Find-Package` restituisce un elenco dei pacchetti primi 20 tramite download o il numero specificato da - prima. Si noti che - Id è facoltativo e nessuna operazione. |
| Origine | Il percorso URL o una cartella per l'origine del pacchetto da cercare. I percorsi di cartella locale possono essere assoluto o relativo della cartella corrente. Se omesso, `Find-Package` Cerca l'origine pacchetto attualmente selezionata. |
| Completaversioni | Visualizza tutte le versioni disponibili di ogni pacchetto anziché solo la versione più recente. |
| First | Il numero di pacchetti da restituire dall'inizio dell'elenco. il valore predefinito è 20. |
| Skip | Omette il primo &lt;int&gt; pacchetti nell'elenco visualizzato.  |
| IncludePrerelease | Include i pacchetti non definitiva nei risultati. |
| ExactMatch | Specificato da utilizzare &lt;parole chiave&gt; come un ID pacchetto tra maiuscole e minuscole. |
| StartWith | Restituisce pacchetti con pacchetto ID inizia con &lt;parole chiave&gt;. |

Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Find-Package`supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

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
