---
title: Riferimento di PowerShell Sync-pacchetto NuGet
description: Informazioni di riferimento per il comando PowerShell Sync-pacchetto nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8119664b1bafe9238b12b1819cc46dc1ee7bdd00
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547994"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (console di Gestione pacchetti in Visual Studio)

*Versione 3.0 e versioni successive; disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*

Ottiene la versione del pacchetto installato da specificato (o predefinito) del progetto e sincronizza la versione per il resto dei progetti nella soluzione.

## <a name="syntax"></a>Sintassi

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| Id | (Obbligatorio) L'identificatore del pacchetto per la sincronizzazione. -Id commutatore stesso è facoltativo. |
| MSI | Installare solo il pacchetto e non le relative dipendenze. |
| ProjectName | Il progetto per la sincronizzazione del pacchetto, verrà utilizzato per il progetto predefinito. |
| Versione | La versione del pacchetto per la sincronizzazione, verrà utilizzato per la versione attualmente installata. |
| Origine | Il percorso URL o una cartella per l'origine del pacchetto da cercare. I percorsi di cartella locale possono essere assoluto o relativo rispetto alla cartella corrente. Se omesso, `Sync-Package` Cerca l'origine del pacchetto attualmente selezionata. |
| IncludePrerelease | Include pacchetti versione non definitivo in sincronizzazione. |
| FileConflictAction | L'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti farvi riferimento il progetto. I valori possibili sono *Sovrascrivi, Ignore, None, OverwriteAll*, e *(3.0 e versioni successive)* *IgnoreAll*. |
| DependencyVersion | La versione dei pacchetti di dipendenza da usare, che può essere uno dei seguenti:<br/><ul><li>*Più basso* (impostazione predefinita): la versione più bassa</li><li>*HighestPatch*: la versione con patch più bassa principali, più bassa secondaria, più alto</li><li>*HighestMinor*: la versione con il minimo principali, patch secondaria, massima più alto</li><li>*Più alto* (valore predefinito per Update-Package senza parametri): la versione più recente</li></ul>È possibile impostare il valore predefinito usando il [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) impostazione nel `Nuget.Config` file. |
| WhatIf | Viene illustrato che cosa accadrebbe quando si esegue il comando senza effettivamente eseguire la sincronizzazione. |

Nessuno di questi parametri accettano caratteri jolly o input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Sync-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

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
