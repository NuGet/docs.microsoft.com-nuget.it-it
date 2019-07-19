---
title: Comando di aggiornamento CLI di NuGet
description: Riferimento per il comando di aggiornamento di NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327508"
---
# <a name="update-command-nuget-cli"></a>Comando update (interfaccia della riga di comando di NuGet)

**Si applica a:** &bullet; **versioni supportate** per l'utilizzo di pacchetti: tutti

Esegue l'aggiornamento di tutti i pacchetti in un progetto (usando `packages.config`) alle versioni disponibili più recenti. È consigliabile eseguire [' Restore '](cli-ref-restore.md) prima di eseguire `update`. Per aggiornare un singolo pacchetto, usare [`nuget install`](cli-ref-install.md) senza specificare un numero di versione, nel qual caso NuGet installa la versione più recente.

Nota: `update` non funziona con l'interfaccia della riga di comando in esecuzione in mono (Mac OSX o Linux) o quando si usa il formato PackageReference.

Il `update` comando Aggiorna inoltre i riferimenti ad assembly nel file di progetto, a condizione che tali riferimenti esistano già. Se un pacchetto aggiornato include un assembly aggiunto, *non* viene aggiunto un nuovo riferimento. Anche per le nuove dipendenze dei pacchetti non sono stati aggiunti riferimenti ad assembly. Per includere queste operazioni come parte di un aggiornamento, aggiornare il pacchetto in Visual Studio usando l'interfaccia utente di gestione pacchetti o la console di gestione pacchetti.

Questo comando può essere usato anche per aggiornare NuGet. exe con il flag *-self* .

## <a name="usage"></a>Utilizzo

```cli
nuget update <configPath> [options]
```

dove `<configPath>` identifica un `packages.config` file di soluzione o che elenca le dipendenze del progetto.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | File di configurazione NuGet da applicare. Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| FileConflictAction | Specifica l'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto. I valori sono *overwrite, ignore, None*. |
| ForceEnglishOutput | *(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| Help | Visualizza le informazioni della Guida per il comando. |
| ID | Specifica un elenco di ID di pacchetto da aggiornare. |
| MSBuildPath | *(4.0 +)* Specifica il percorso di MSBuild da usare con il comando, avendo la precedenza `-MSBuildVersion`su. |
| MSBuildVersion | *(3.2 +)* Specifica la versione di MSBuild da usare con questo comando. I valori supportati sono 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Per impostazione predefinita, viene scelto MSBuild nel percorso; in caso contrario, per impostazione predefinita viene impostata la versione più recente di MSBuild. |
| NonInteractive | Evita la richiesta di input o conferme dell'utente. |
| PreRelease | Consente l'aggiornamento alle versioni provvisorie. Questo flag non è obbligatorio quando si aggiornano i pacchetti di versioni non definitive già installati. |
| RepositoryPath | Specifica la cartella locale in cui sono installati i pacchetti. |
| Safe | Specifica che verranno installati solo gli aggiornamenti con la versione più recente disponibile all'interno della stessa versione principale e secondaria del pacchetto installato. |
| Auto | Aggiorna NuGet. exe alla versione più recente. tutti gli altri argomenti vengono ignorati. |
| Source | Specifica l'elenco di origini di pacchetti (come URL) da usare per gli aggiornamenti. Se omesso, il comando usa le origini fornite nei file di configurazione, vedere [configurazioni comuni di NuGet](../../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |
| Version | Se utilizzata con un ID pacchetto, specifica la versione del pacchetto da aggiornare. |

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
