---
title: Comando di elenco NuGet CLI
description: Riferimento per il comando di elenco di nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b0f144d8abbba7388fe39cd113e4eeddccbca2c6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818438"
---
# <a name="list-command-nuget-cli"></a>comando di elenco (NuGet CLI)

**Si applica a:** il consumo di pacchetti, pubblicazione &bullet; **le versioni supportate:** tutti

Visualizza un elenco di pacchetti da un'origine specificata. Se non vengono specificata alcuna origine, tutte le origini definito nel file di configurazione globale, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config`, vengono utilizzati. Se `NuGet.Config` non specifica nessuna origine, quindi `list` Usa il feed predefinito (nuget.org).

## <a name="usage"></a>Utilizzo

```cli
nuget list [search terms] [options]
```

in termini di ricerca facoltativo verranno filtrato l'elenco visualizzato. I termini di ricerca vengono applicati ai nomi dei pacchetti, tag e le descrizioni di pacchetto, esattamente come quando il loro utilizzo su nuget.org.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| Completaversioni | Elencare tutte le versioni di un pacchetto. Per impostazione predefinita, viene visualizzata solo la versione più recente del pacchetto. |
| ConfigFile | Il file di configurazione NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.|
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| IncludeDelisted | *(3.2 +)*  Visualizzare i pacchetti. |
| Non interattivo | Elimina richieste per l'input dell'utente o le conferme. |
| Versione provvisoria | Include pacchetti della versione provvisoria, nell'elenco. |
| Origine | Specifica un elenco di origini dei pacchetti per la ricerca. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
