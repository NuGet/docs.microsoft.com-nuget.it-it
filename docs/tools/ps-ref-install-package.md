---
title: Riferimento di PowerShell di NuGet Install-Package
description: Informazioni di riferimento per il comando di PowerShell Install-Package nella Console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: e7ddf9ad97cbb4ec9cfc8b01f366511239f41416
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546026"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (console di Gestione pacchetti in Visual Studio)

*In questo argomento descrive il comando all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows. Per il comando di PowerShell Install-Package generico, vedere la [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Installa un pacchetto e le relative dipendenze in un progetto.

## <a name="syntax"></a>Sintassi

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

In NuGet 2.8 + `Install-Package` può effettuare il downgrade di un pacchetto esistente nel progetto. Ad esempio, se hai 5.1.0-rc1 ASPNET installato, il comando seguente potrebbe effettuare il downgrade alla 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| Id | (Obbligatorio) L'identificatore del pacchetto da installare. (*3.0 e versioni successive*) l'identificatore può essere un percorso o URL di un `packages.config` file o un `.nupkg` file. -Id commutatore stesso è facoltativo. |
| MSI | Installare solo il pacchetto e non le relative dipendenze. |
| ProjectName | Il progetto in cui si desidera installare il pacchetto, verrà utilizzato per il progetto predefinito. |
| Origine | Il percorso URL o una cartella per l'origine del pacchetto da cercare. I percorsi di cartella locale possono essere assoluto o relativo rispetto alla cartella corrente. Se omesso, `Install-Package` Cerca l'origine del pacchetto attualmente selezionata. |
| Versione | La versione del pacchetto da installare, verrà utilizzato per la versione più recente. |
| IncludePrerelease | Prende in considerazione i pacchetti di versione non definitivo per l'installazione. Se omesso, vengono considerati solo i pacchetti stabili. |
| FileConflictAction | L'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti farvi riferimento il progetto. I valori possibili sono *Sovrascrivi, Ignore, None, OverwriteAll*, e *(3.0 e versioni successive)* *IgnoreAll*. |
| DependencyVersion | La versione dei pacchetti di dipendenza da usare, che può essere uno dei seguenti:<br/><ul><li>*Più basso* (impostazione predefinita): la versione più bassa</li><li>*HighestPatch*: la versione con patch più bassa principali, più bassa secondaria, più alto</li><li>*HighestMinor*: la versione con il minimo principali, patch secondaria, massima più alto</li><li>*Più alto* (valore predefinito per Update-Package senza parametri): la versione più recente</li></ul>È possibile impostare il valore predefinito usando il [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) impostazione nel `Nuget.Config` file. |
| WhatIf | Viene illustrato che cosa accadrebbe quando si esegue il comando senza eseguire effettivamente l'installazione. |

Nessuno di questi parametri accettano caratteri jolly o input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Install-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione per errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

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
