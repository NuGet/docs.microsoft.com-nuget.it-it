---
title: Comando di NuGet CLI list
description: Informazioni di riferimento per il comando list nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549801"
---
# <a name="list-command-nuget-cli"></a>comando List (NuGet CLI)

**Si applica a:** utilizzo di un pacchetto, la pubblicazione &bullet; **le versioni supportate:** tutti

Visualizza un elenco dei pacchetti da un'origine specificata. Se non sono specificate origini, tutte le origini definite nel file di configurazione globali `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config`, vengono usati. Se `NuGet.Config` non specifica nessuna origine, quindi `list` Usa il feed predefinito (nuget.org).

## <a name="usage"></a>Utilizzo

```cli
nuget list [search terms] [options]
```

in cui i termini di ricerca facoltativo filtrerà l'elenco visualizzato. I termini di ricerca vengono applicati ai nomi dei pacchetti, tag e descrizioni dei pacchetti, esattamente come lo sono quando vengono utilizzati in nuget.org.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| AllVersions | Elencare tutte le versioni di un pacchetto. Per impostazione predefinita, viene visualizzato solo l'ultima versione del pacchetto. |
| ConfigFile | Il file di configurazione di NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.|
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| IncludeDelisted | *(3.2 +)*  Visualizzare pacchetti rimossi dall'elenco. |
| Non interattive | Elimina richieste di input o conferme dell'utente. |
| Versione preliminare | Include prerelease pacchetti nell'elenco. |
| Origine | Specifica un elenco di origini di pacchetti per la ricerca. |
| Livello di dettaglio | Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
