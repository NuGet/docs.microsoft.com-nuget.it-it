---
title: Guida di riferimento a NuGet Find-Package PowerShell
description: Informazioni di riferimento per il comando Find-Package PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 83d0d62bbda07d07ea1e3b58e531447e2001b680
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777505"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (console di gestione pacchetti in Visual Studio)

*Versione 3.0 +; in questo argomento viene descritto il comando nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows. Per il comando generico di Find-Package PowerShell, vedere le informazioni di [riferimento su PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Ottiene il set di pacchetti remoti con ID o parole chiave specificati dall'origine del pacchetto.

## <a name="syntax"></a>Sintassi

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| &lt;Parole chiave ID&gt; | Necessaria Parole chiave da usare durante la ricerca nell'origine del pacchetto. Usare-ExactMatch per restituire solo i pacchetti il cui ID pacchetto corrisponde alle parole chiave. Se non viene specificata alcuna parola chiave, `Find-Package` restituisce un elenco dei primi 20 pacchetti per download o il numero specificato da-First. Si noti che-ID è facoltativo e un no-op. |
| Source (Sorgente) | URL o percorso della cartella per l'origine del pacchetto da cercare. I percorsi delle cartelle locali possono essere assoluti o relativi alla cartella corrente. Se omesso, `Find-Package` Cerca nell'origine del pacchetto attualmente selezionata. |
| AllVersions | Visualizza tutte le versioni disponibili di ogni pacchetto anziché solo la versione più recente. |
| First (Primo) | Numero di pacchetti da restituire dall'inizio dell'elenco; il valore predefinito è 20. |
| Ignora | Omette i primi &lt; pacchetti int &gt; dall'elenco visualizzato.  |
| IncludePrerelease | Include i pacchetti di versioni non definitive nei risultati. |
| ExactMatch | Specificato per usare &lt; parole chiave &gt; come ID pacchetto con distinzione tra maiuscole e minuscole. |
| Cominciamo | Restituisce i pacchetti il cui ID di pacchetto inizia con &lt; parole chiave &gt; . |

Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Find-Package` supporta i seguenti [parametri comuni di PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

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