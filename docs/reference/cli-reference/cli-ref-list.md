---
title: Comando elenco dell'interfaccia della riga di comando NuGet
description: Riferimento per il comando elenco NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327738"
---
# <a name="list-command-nuget-cli"></a>comando list (interfaccia della riga di comando di NuGet)

**Si applica a:** utilizzo del pacchetto &bullet; , pubblicazione delle **versioni supportate:** tutti

Visualizza un elenco di pacchetti da un'origine specificata. Se non viene specificata alcuna origine, vengono utilizzate tutte le origini definite nel file `%AppData%\NuGet\NuGet.Config` di configurazione globale ( `~/.nuget/NuGet/NuGet.Config`Windows) o. Se `NuGet.Config` non specifica alcuna origine `list` , usa il feed predefinito (NuGet.org).

## <a name="usage"></a>Utilizzo

```cli
nuget list [search terms] [options]
```

dove i termini di ricerca facoltativi filtrano l'elenco visualizzato. I termini di ricerca vengono applicati ai nomi di pacchetti, tag e descrizioni del pacchetto così come sono quando vengono utilizzati in nuget.org.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| AllVersions | Elencare tutte le versioni di un pacchetto. Per impostazione predefinita, viene visualizzata solo la versione più recente del pacchetto. |
| ConfigFile | File di configurazione NuGet da applicare. Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| Help | Visualizza le informazioni della Guida per il comando. |
| IncludeDelisted | *(3.2 +)* Visualizza i pacchetti non in elenco. |
| NonInteractive | Evita la richiesta di input o conferme dell'utente. |
| PreRelease | Include i pacchetti di versioni non definitive nell'elenco. |
| Source | Specifica un elenco di origini dei pacchetti in cui eseguire la ricerca. |
| Verbosity | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
