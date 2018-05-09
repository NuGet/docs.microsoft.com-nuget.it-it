---
title: Riferimento di PowerShell di NuGet. Install-Package
description: Riferimento per il comando di PowerShell Install-Package nella Console di gestione pacchetti NuGet in Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5adfbcae0affcaa402f7981c12e108490d546511
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Pacchetto di installazione (Console di gestione dei pacchetti in Visual Studio)

*Questo argomento viene descritto il comando all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows. Per il comando di PowerShell Install-Package generico, vedere il [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Installa un pacchetto e le relative dipendenze in un progetto.

## <a name="syntax"></a>Sintassi

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

In NuGet 2.8 + `Install-Package` può effettuare il downgrade di un pacchetto esistente nel progetto. Ad esempio, se si dispone di 5.1.0-rc1 italiano installato, il comando seguente sarebbe effettuare il downgrade a 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| Id | (Obbligatorio) L'identificatore del pacchetto da installare. (*3.0 +*) l'identificatore può essere un percorso o URL di un `packages.config` file o un `.nupkg` file. -Id switch stesso è facoltativo. |
| MSI | Installa solo questo pacchetto e non le relative dipendenze. |
| ProjectName | Il progetto in cui installare il pacchetto, verrà utilizzato per il progetto predefinito. |
| Origine | Il percorso URL o una cartella per l'origine del pacchetto da cercare. I percorsi di cartella locale possono essere assoluto o relativo della cartella corrente. Se omesso, `Install-Package` Cerca l'origine pacchetto attualmente selezionata. |
| Versione | La versione del pacchetto da installare, verrà utilizzato per la versione più recente. |
| IncludePrerelease | Considera i pacchetti della versione provvisoria per l'installazione. Se omesso, vengono considerati solo i pacchetti definitivi. |
| FileConflictAction | L'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto. I valori possibili sono *sovrascrittura, Ignora, None, OverwriteAll*, e *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | La versione dei pacchetti di dipendenza da usare, che può essere uno dei seguenti:<br/><ul><li>*Più basso* (impostazione predefinita): la versione minima</li><li>*HighestPatch*: la versione con la patch più basso principale, secondaria più basso, più elevata</li><li>*HighestMinor*: la versione con il minimo principali, patch più alto, minore più alto</li><li>*Più alto* (impostazione predefinita per il pacchetto di aggiornamento senza parametri): la versione più recente</li></ul>È possibile impostare il valore predefinito utilizzando il [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) impostazione di `Nuget.Config` file. |
| WhatIf | Viene illustrato che cosa accadrebbe eseguendo il comando senza eseguire effettivamente l'installazione. |

Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Install-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
