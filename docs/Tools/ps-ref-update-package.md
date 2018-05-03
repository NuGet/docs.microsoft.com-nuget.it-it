---
title: Riferimento di PowerShell Update-pacchetto NuGet
description: Riferimento per il comando di PowerShell di pacchetto di aggiornamento nella Console di gestione pacchetti NuGet in Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 621e59633117a29c58fe643860ee7e2b40a4fbe2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Pacchetto di aggiornamento (Console di gestione dei pacchetti in Visual Studio)

*Disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*

Aggiorna un pacchetto e le relative dipendenze o tutti i pacchetti in un progetto a una versione più recente.

## <a name="syntax"></a>Sintassi

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

In NuGet 2.8 + `Update-Package` può essere usato per effettuare il downgrade di un pacchetto esistente nel progetto. Ad esempio, se si dispone di 5.1.0-rc1 italiano installato, il comando seguente sarebbe effettuare il downgrade a 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametri

|  Parametro | Descrizione |
| --- | --- |
| Id | L'identificatore del pacchetto da aggiornare. Se omesso, Aggiorna tutti i pacchetti. -Id switch stesso è facoltativo. |
| MSI | Ignora le dipendenze del pacchetto di aggiornamento. |
| ProjectName | Il nome del progetto contenente i pacchetti da aggiornare, verrà utilizzato per tutti i progetti. |
| Versione | La versione da utilizzare per l'aggiornamento, verrà utilizzato per la versione più recente. In NuGet 3.0 e successive, il valore di versione deve essere uno dei *minima, massima, HighestMinor*, o *HighestPatch* (equivalente a - Safe). |
| Safe | Vincola gli aggiornamenti alle versioni sole con la stessa versione principale e secondaria del pacchetto attualmente installata. |
| Origine | Il percorso URL o una cartella per l'origine del pacchetto da cercare. I percorsi di cartella locale possono essere assoluto o relativo della cartella corrente. Se omesso, `Update-Package` Cerca l'origine pacchetto attualmente selezionata. |
| IncludePrerelease | Include pacchetti della versione provvisoria per gli aggiornamenti. |
| Reinstallazione | Pacchetti di Resintalls utilizzando la versione attualmente installata. Vedere [Reinstallazione e aggiornamento di pacchetti](../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | L'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto. I valori possibili sono *sovrascrittura, Ignora, None, OverwriteAll*, e *IgnoreAll* (3.0 +). |
| DependencyVersion | La versione dei pacchetti di dipendenza da usare, che può essere uno dei seguenti:<br/><ul><li>*Più basso* (impostazione predefinita): la versione minima</li><li>*HighestPatch*: la versione con la patch più basso principale, secondaria più basso, più elevata</li><li>*HighestMinor*: la versione con il minimo principali, patch più alto, minore più alto</li><li>*Più alto* (impostazione predefinita per il pacchetto di aggiornamento senza parametri): la versione più recente</li></ul>È possibile impostare il valore predefinito utilizzando il [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) impostazione di `Nuget.Config` file. |
| ToHighestPatch | Vincola gli aggiornamenti solo alle versioni con la stessa versione secondaria del pacchetto attualmente installata. |
| ToHighestMinor | Vincola gli aggiornamenti solo alle versioni con la stessa versione principale del pacchetto attualmente installata. |
| WhatIf | Viene illustrato che cosa accadrebbe eseguendo il comando senza eseguire effettivamente l'aggiornamento. |

Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.

### <a name="common-parameters"></a>Parametri comuni

`Update-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

### <a name="examples"></a>Esempi

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
