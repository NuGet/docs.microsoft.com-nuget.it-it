---
title: Guida di riferimento di sincronizzazione-pacchetto NuGet PowerShell | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Riferimento per il comando di PowerShell di sincronizzazione pacchetto nella Console di gestione pacchetti NuGet in Visual Studio.
keywords: Console di gestione, i comandi di Powershell di NuGet, riferimenti di NuGet Powershell, sincronizzazione pacchetto del pacchetto NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0297015c3f1b8a8aced2545b4c4c3e6ccb1c7146
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sincronizzazione-pacchetto (Package Manager Console in Visual Studio)

*Versione 3.0; disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*

Ottiene la versione del pacchetto installato dal specificato (o predefinito) del progetto e sincronizza la versione ai restanti progetti nella soluzione.

## <a name="syntax"></a>Sintassi

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| Id | (Obbligatorio) L'identificatore del pacchetto per la sincronizzazione. -Id switch stesso è facoltativo. |
| IgnoreDependencies | Installa solo questo pacchetto e non le relative dipendenze. |
| ProjectName | Progetto per sincronizzare il pacchetto, verrà utilizzato per il progetto predefinito. |
| Versione | La versione del pacchetto per la sincronizzazione, verrà utilizzato per la versione attualmente installata. |
| Origine | Il percorso URL o una cartella per l'origine del pacchetto da cercare. I percorsi di cartella locale possono essere assoluto o relativo della cartella corrente. Se omesso, `Sync-Package` Cerca l'origine pacchetto attualmente selezionata. |
| IncludePrerelease | Include pacchetti della versione provvisoria della sincronizzazione. |
| FileConflictAction | L'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto. I valori possibili sono *sovrascrittura, Ignora, None, OverwriteAll*, e *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | La versione dei pacchetti di dipendenza da usare, che può essere uno dei seguenti:<br/><ul><li>*Più basso* (impostazione predefinita): la versione minima</li><li>*HighestPatch*: la versione con la patch più basso principale, secondaria più basso, più elevata</li><li>*HighestMinor*: la versione con il minimo principali, patch più alto, minore più alto</li><li>*Più alto* (impostazione predefinita per il pacchetto di aggiornamento senza parametri): la versione più recente</li></ul>È possibile impostare il valore predefinito utilizzando il [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) impostazione di `Nuget.Config` file. |
| WhatIf | Viene illustrato che cosa accadrebbe eseguendo il comando senza eseguire effettivamente la sincronizzazione. |

Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Sync-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

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
