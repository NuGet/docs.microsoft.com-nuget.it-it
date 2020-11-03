---
title: Guida di riferimento a NuGet Install-Package PowerShell
description: Informazioni di riferimento per il comando Install-Package PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5bda888e0fb526faca79e88da93b0ceb9aff5348
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237205"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (console di gestione pacchetti in Visual Studio)

*In questo argomento viene descritto il comando nella [console di gestione pacchetti](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows. Per il comando generico di Install-Package PowerShell, vedere le informazioni di [riferimento su PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Installa un pacchetto e le relative dipendenze in un progetto.

## <a name="syntax"></a>Sintassi

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

In NuGet 2.8 +, `Install-Package` può effettuare il downgrade di un pacchetto esistente nel progetto. Se, ad esempio, è installato Microsoft. AspNet. MVC 5.1.0-RC1, il comando seguente esegue il downgrade a 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametri

| Parametro | Descrizione |
| --- | --- |
| ID | Necessaria Identificatore del pacchetto da installare. ( *3.0 +* ) L'identificatore può essere un percorso o un URL di un `packages.config` file o di un `.nupkg` file. L'opzione-ID è facoltativa. |
| IgnoreDependencies | Installare solo questo pacchetto e non le relative dipendenze. |
| ProjectName | Progetto in cui installare il pacchetto, per impostazione predefinita il progetto predefinito. |
| Source (Sorgente) | URL o percorso della cartella per l'origine del pacchetto da cercare. I percorsi delle cartelle locali possono essere assoluti o relativi alla cartella corrente. Se omesso, `Install-Package` Cerca nell'origine del pacchetto attualmente selezionata. |
| Versione | Versione del pacchetto da installare, per impostazione predefinita la versione più recente. |
| IncludePrerelease | Considera i pacchetti di versioni non definitive per l'installazione. Se omesso, vengono presi in considerazione solo i pacchetti definitivi. |
| FileConflictAction | Azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto. I valori possibili sono *overwrite, ignore, None, OverwriteAll* e *(3.0 +)* *IgnoreAll* . |
| DependencyVersion | Versione dei pacchetti di dipendenze da usare. i possibili tipi sono i seguenti:<br/><ul><li>*Minimo* (impostazione predefinita): versione più bassa</li><li>*HighestPatch* : versione con la patch principale più bassa, minore minore, più alta</li><li>*HighestMinor* : versione con la patch principale più bassa, minore più elevata</li><li>*Massimo* (impostazione predefinita per Update-Package senza parametri): la versione più recente</li></ul>È possibile impostare il valore predefinito usando l' [`dependencyVersion`](../nuget-config-file.md#config-section) impostazione nel `Nuget.Config` file. |
| WhatIf | Mostra cosa accade quando si esegue il comando senza eseguire effettivamente l'installazione. |

Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.

## <a name="common-parameters"></a>Parametri comuni

`Install-Package` supporta i seguenti [parametri comuni di PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

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