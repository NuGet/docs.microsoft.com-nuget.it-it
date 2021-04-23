---
title: Informazioni di riferimento Install-Package PowerShell per NuGet
description: Informazioni di Install-Package comando di PowerShell nella console Gestione pacchetti NuGet in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ad551b8701cfc2061f7721fb050ed9b5a4fede32
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901694"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Gestione pacchetti Console in Visual Studio)

*Questo argomento descrive il comando all'interno [della console Gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows. Per il comando di gestione Install-Package PowerShell generico, vedere le informazioni di [riferimento su PackageManagement di PowerShell.](/powershell/module/packagemanagement)*

Installa un pacchetto e le relative dipendenze in un progetto.

## <a name="syntax"></a>Sintassi

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

In NuGet 2.8+, `Install-Package` è possibile eseguire il downgrade di un pacchetto esistente nel progetto. Ad esempio, se è installato Microsoft.AspNet.MVC 5.1.0-rc1, il comando seguente ne esegue il downgrade alla versione 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| Id | (Obbligatorio) Identificatore del pacchetto da installare. (*3.0+*) L'identificatore può essere un percorso o un URL di `packages.config` un file o di un `.nupkg` file. L'opzione -Id è facoltativa. |
| IgnoreDependencies | Installare solo questo pacchetto e non le relative dipendenze. |
| ProjectName | Progetto in cui installare il pacchetto, che per impostazione predefinita è il progetto predefinito. |
| Source (Sorgente) | URL o percorso della cartella per l'origine del pacchetto in cui eseguire la ricerca. I percorsi delle cartelle locali possono essere assoluti o relativi alla cartella corrente. Se omesso, `Install-Package` cerca l'origine del pacchetto attualmente selezionata. |
| Versione | Versione del pacchetto da installare, che per impostazione predefinita è la versione più recente. |
| IncludePrerelease | Considera i pacchetti di versione non definitiva per l'installazione. Se omesso, vengono presi in considerazione solo i pacchetti definitivi. |
| FileConflictAction | Azione da eseguire quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto. I valori possibili *sono Overwrite, Ignore, None, OverwriteAll* e *(3.0+)* *IgnoreAll.* |
| DependencyVersion | Versione dei pacchetti di dipendenze da usare, che può essere una delle seguenti:<br/><ul><li>*Più basso* (impostazione predefinita): la versione più bassa</li><li>*HighestPatch:* la versione con la patch principale, secondaria più bassa e più alta</li><li>*HighestMinor:* la versione con la patch principale, secondaria più alta e più alta</li><li>*Massimo* (impostazione predefinita per Update-Package senza parametri): la versione più recente</li></ul>È possibile impostare il valore predefinito usando [`dependencyVersion`](../nuget-config-file.md#config-section) l'impostazione nel `Nuget.Config` file . |
| WhatIf | Mostra cosa accade quando si esegue il comando senza eseguire effettivamente l'installazione. |

Nessuno di questi parametri accetta l'input della pipeline o i caratteri jolly.

## <a name="common-parameters"></a>Parametri comuni

`Install-Package` supporta i parametri comuni di [PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters)seguenti: Debug, Azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

## <a name="examples"></a>Esempi

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```