---
title: Comando di NuGet CLI elenco | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: Riferimento per il comando di elenco di nuget.exe
keywords: riferimento elenco NuGet, comando elenco di pacchetti
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a>comando di elenco (NuGet CLI)

**Si applica a:** il consumo di pacchetti, pubblicazione &bullet; **le versioni supportate:** tutti

Visualizza un elenco di pacchetti da un'origine specificata. Se non vengono specificata alcuna origine, tutte le origini definito nel file di configurazione globale, `%AppData%\NuGet\NuGet.Config`, vengono utilizzati. Se `NuGet.Config` non specifica nessuna origine, quindi `list` Usa il feed predefinito (nuget.org).

## <a name="usage"></a>Utilizzo

```
nuget list [search terms] [options]
```

in termini di ricerca facoltativo verranno filtrato l'elenco visualizzato. I termini di ricerca vengono applicati ai nomi dei pacchetti, tag e le descrizioni di pacchetto.

## <a name="options"></a>Opzioni
| Opzione | Descrizione |
| --- | --- |
| Completaversioni | Elencare tutte le versioni di un pacchetto. Per impostazione predefinita, viene visualizzata solo la versione più recente del pacchetto. |
| ConfigFile | *(2.5 +)*  Questo file di configurazione da applicare. Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| IncludeDelisted | *(3.2 +)*  Visualizzare i pacchetti. |
| Non interattivo | Elimina richieste per l'input dell'utente o le conferme. |
| Versione provvisoria | Include pacchetti della versione provvisoria, nell'elenco. |
| Origine | Specifica un elenco di origini dei pacchetti per la ricerca. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate (2.5 +)*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
