---
title: Informazioni di riferimento su PowerShell per sincronizzazione pacchetti NuGet
description: Riferimento per il comando Sync-package di PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a48a09a27b6db9b774e59b9a10652067179e2c27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327308"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (console di Gestione pacchetti in Visual Studio)

*Versione 3.0 +; disponibile solo nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows.*

Ottiene la versione del pacchetto installato dal progetto specificato (o predefinito) e sincronizza la versione con i restanti progetti nella soluzione.

## <a name="syntax"></a>Sintassi

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| ID | Necessaria Identificatore del pacchetto da sincronizzare. L'opzione-ID è facoltativa. |
| IgnoreDependencies | Installare solo questo pacchetto e non le relative dipendenze. |
| ProjectName | Progetto da cui sincronizzare il pacchetto, per impostazione predefinita il progetto predefinito. |
| Version | Versione del pacchetto da sincronizzare, per impostazione predefinita la versione attualmente installata. |
| Source | URL o percorso della cartella per l'origine del pacchetto da cercare. I percorsi delle cartelle locali possono essere assoluti o relativi alla cartella corrente. Se omesso, `Sync-Package` Cerca nell'origine del pacchetto attualmente selezionata. |
| IncludePrerelease | Include i pacchetti di versioni non definitive nella sincronizzazione. |
| FileConflictAction | Azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto. I valori possibili sono *overwrite, ignore, None, OverwriteAll*e *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | Versione dei pacchetti di dipendenze da usare. i possibili tipi sono i seguenti:<br/><ul><li>*Più bassa* (impostazione predefinita): versione più bassa</li><li>*HighestPatch*: versione con la patch principale più bassa, minore minore, più alta</li><li>*HighestMinor*: versione con la patch principale più bassa, minore più elevata</li><li>*Più alta* (impostazione predefinita per Update-Package senza parametri): la versione più recente</li></ul>È possibile impostare il valore predefinito usando l' [`dependencyVersion`](../nuget-config-file.md#config-section) impostazione `Nuget.Config` nel file. |
| Whatif | Mostra cosa accade quando si esegue il comando senza eseguire effettivamente la sincronizzazione. |

Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Sync-Package`supporta i seguenti [parametri comuni di PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
