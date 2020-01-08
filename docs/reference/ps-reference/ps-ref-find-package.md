---
title: Guida di riferimento a NuGet Find-Package PowerShell
description: Informazioni di riferimento sul comando find-package di PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4118b5a38f80a2300b3945738315d56bda096f9a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384633"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (console di Gestione pacchetti in Visual Studio)

*Versione 3.0 +; in questo argomento viene descritto il comando nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows. Per il comando Generic PowerShell Find-Package, vedere la Guida di [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Ottiene il set di pacchetti remoti con ID o parole chiave specificati dall'origine del pacchetto.

## <a name="syntax"></a>Sintassi

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| ID &lt;parole chiave&gt; | Necessaria Parole chiave da usare durante la ricerca nell'origine del pacchetto. Usare-ExactMatch per restituire solo i pacchetti il cui ID pacchetto corrisponde alle parole chiave. Se non viene specificata alcuna parola chiave, `Find-Package` restituisce un elenco dei primi 20 pacchetti per download o il numero specificato da-First. Si noti che-ID è facoltativo e un no-op. |
| Source | URL o percorso della cartella per l'origine del pacchetto da cercare. I percorsi delle cartelle locali possono essere assoluti o relativi alla cartella corrente. Se omesso, `Find-Package` Cerca nell'origine del pacchetto attualmente selezionata. |
| AllVersions | Visualizza tutte le versioni disponibili di ogni pacchetto anziché solo la versione più recente. |
| First | Numero di pacchetti da restituire dall'inizio dell'elenco; il valore predefinito è 20. |
| Skip | Omette la prima &lt;i pacchetti int&gt; dall'elenco visualizzato.  |
| IncludePrerelease | Include i pacchetti di versioni non definitive nei risultati. |
| ExactMatch | Specificato per utilizzare &lt;parole chiave&gt; come ID pacchetto con distinzione tra maiuscole e minuscole. |
| StartWith | Restituisce i pacchetti il cui ID di pacchetto inizia con &lt;parole chiave&gt;. |

Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Find-Package` supporta i [parametri di PowerShell comuni](https://go.microsoft.com/fwlink/?LinkID=113216)seguenti: debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

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
