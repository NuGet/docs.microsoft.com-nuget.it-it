---
title: Guida di riferimento a NuGet Update-Package PowerShell
description: Informazioni di riferimento per il comando Update-Package PowerShell nella console di gestione pacchetti NuGet in Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: af918d11e8f976be962d52084c5eda4d53e382c6
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238036"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (console di gestione pacchetti in Visual Studio)

*Disponibile solo nella [console di gestione pacchetti NuGet](../../consume-packages/install-use-packages-powershell.md) in Visual Studio in Windows.*

Aggiorna un pacchetto e le relative dipendenze o tutti i pacchetti di un progetto a una versione più recente.

## <a name="syntax"></a>Sintassi

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

In NuGet 2.8 +, `Update-Package` può essere usato per eseguire il downgrade di un pacchetto esistente nel progetto. Se, ad esempio, è installato Microsoft. AspNet. MVC 5.1.0-RC1, il comando seguente esegue il downgrade a 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametri

|  Parametro | Descrizione |
| --- | --- |
| ID | Identificatore del pacchetto da aggiornare. Se omesso, aggiorna tutti i pacchetti. L'opzione-ID è facoltativa. |
| IgnoreDependencies | Ignora l'aggiornamento delle dipendenze del pacchetto. |
| ProjectName | Nome del progetto contenente i pacchetti da aggiornare, per impostazione predefinita tutti i progetti. |
| Versione | Versione da usare per l'aggiornamento, per impostazione predefinita la versione più recente. In NuGet 3.0 +, il valore della versione deve essere uno dei valori *minimo, massimo, HighestMinor* o *HighestPatch* (equivalente a-safe). |
| Safe | Vincola gli aggiornamenti solo alle versioni con la stessa versione principale e secondaria del pacchetto attualmente installato. |
| Source (Sorgente) | URL o percorso della cartella per l'origine del pacchetto da cercare. I percorsi delle cartelle locali possono essere assoluti o relativi alla cartella corrente. Se omesso, `Update-Package` Cerca nell'origine del pacchetto attualmente selezionata. |
| IncludePrerelease | Include pacchetti di versioni non definitive per gli aggiornamenti. |
| Reinstallazione | Resintalls i pacchetti usando le versioni attualmente installate. Vedere [Reinstallazione e aggiornamento di pacchetti](../../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | Azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto. I valori possibili sono *overwrite, ignore, None, OverwriteAll* e *IgnoreAll* (3.0 +). |
| DependencyVersion | Versione dei pacchetti di dipendenze da usare. i possibili tipi sono i seguenti:<br/><ul><li>*Minimo* (impostazione predefinita): versione più bassa</li><li>*HighestPatch* : versione con la patch principale più bassa, minore minore, più alta</li><li>*HighestMinor* : versione con la patch principale più bassa, minore più elevata</li><li>*Massimo* (impostazione predefinita per Update-Package senza parametri): la versione più recente</li></ul>È possibile impostare il valore predefinito usando l' [`dependencyVersion`](../nuget-config-file.md#config-section) impostazione nel `Nuget.Config` file. |
| ToHighestPatch | equivalente a-safe. |
| ToHighestMinor | Vincola gli aggiornamenti solo alle versioni con la stessa versione principale del pacchetto attualmente installato. |
| WhatIf | Mostra cosa accade quando si esegue il comando senza eseguire effettivamente l'aggiornamento. |

Nessuno di questi parametri accetta caratteri jolly o di input della pipeline.

### <a name="common-parameters"></a>Parametri comuni

`Update-Package` supporta i seguenti [parametri comuni di PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.

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
Update-Package Elmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package Elmah –reinstall -ignoreDependencies
```
