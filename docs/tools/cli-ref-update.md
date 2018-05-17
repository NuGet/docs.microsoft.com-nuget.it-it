---
title: Comando update NuGet CLI
description: Riferimento per il comando di aggiornamento di nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e6964d92436ce1bac9e6af85f6dae75fcf40378d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="update-command-nuget-cli"></a>Comando update (interfaccia della riga di comando di NuGet)

**Si applica a:** pacchetto consumo &bullet; **le versioni supportate:** tutti

Aggiorna tutti i pacchetti in un progetto (usando `packages.config`) alle versioni più recenti. È consigliabile eseguire ['restore'](cli-ref-restore.md) prima di eseguire il `update`. (Per aggiornare un singolo pacchetto, utilizzare [ `nuget install` ](cli-ref-install.md) senza specificare un numero di versione, in cui NuGet case consente di installare la versione più recente.)

Nota: `update` non funziona con l'interfaccia CLI in esecuzione in Mono (Mac OSX o Linux) o quando si utilizza il formato PackageReference.

Il `update` comando Aggiorna anche i riferimenti all'assembly nel file di progetto, fornito quelli fa riferimento a già esiste. Se un pacchetto aggiornato è un assembly aggiunto, un nuovo riferimento è *non* aggiunto. Inoltre, nuove dipendenze di pacchetto non sono i riferimenti ad assembly aggiunto. Per includere queste operazioni come parte di un aggiornamento, aggiornare il pacchetto in Visual Studio utilizzando la UI Package Manager o la Console di gestione pacchetti.

Questo comando può essere utilizzato anche per aggiornare nuget.exe stesso utilizzando il *-self* flag.

## <a name="usage"></a>Utilizzo

```cli
nuget update <configPath> [options]
```

dove `<configPath>` identifica uno un `packages.config` o file di soluzione che elenca le dipendenze del progetto.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | Il file di configurazione NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.|
| FileConflictAction | Specifica l'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto. I valori sono *sovrascrivere, ignorare, Nessuno*. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| Id | Specifica un elenco di ID per l'aggiornamento pacchetto. |
| MSBuildPath | *(4.0 +)*  Specifica il percorso di MSBuild da usare con il comando, che avrà la precedenza `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Specifica la versione di MSBuild da usare con questo comando. Valori supportati sono 4, 12, 14, 15. Per impostazione predefinita che viene selezionato il percorso di MSBuild, in caso contrario il valore predefinito la versione più aggiornata di MSBuild. |
| Non interattivo | Elimina richieste per l'input dell'utente o le conferme. |
| Versione provvisoria | Consente l'aggiornamento di versioni non definitive. Questo flag non è richiesto durante l'aggiornamento preliminari pacchetti che sono già installati. |
| RepositoryPath | Specifica la cartella locale in cui sono installati i pacchetti. |
| Safe | Specifica che solo gli aggiornamenti con la versione più recente disponibile all'interno della stessa versione principale e secondaria verrà installato il pacchetto installato. |
| Self | Nuget.exe gli aggiornamenti per la versione più recente; tutti gli altri argomenti vengono ignorati. |
| Origine | Specifica l'elenco delle origini pacchetto (come URL) da usare per gli aggiornamenti. Se omesso, il comando Usa le origini disponibili in file di configurazione, vedere [il comportamento di configurazione NuGet](../consume-packages/configuring-nuget-behavior.md). |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |
| Versione | Se usato con un ID di pacchetto, specifica la versione del pacchetto da aggiornare. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
