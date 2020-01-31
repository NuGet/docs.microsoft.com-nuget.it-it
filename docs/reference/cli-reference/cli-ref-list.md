---
title: Comando elenco dell'interfaccia della riga di comando NuGet
description: Riferimento per il comando elenco NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813338"
---
# <a name="list-command-nuget-cli"></a>comando list (interfaccia della riga di comando di NuGet)

**Si applica a:** utilizzo del pacchetto, pubblicazione &bullet; **versioni supportate:** tutti

Visualizza un elenco di pacchetti da un'origine specificata. Se non viene specificata alcuna origine, vengono utilizzate tutte le origini definite nel file di configurazione globale, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config`. Se `NuGet.Config` non specifica alcuna origine, `list` usa il feed predefinito (nuget.org).

## <a name="usage"></a>Usage

```cli
nuget list [search terms] [options]
```

dove i termini di ricerca facoltativi filtrano l'elenco visualizzato. I termini di ricerca vengono applicati ai nomi di pacchetti, tag e descrizioni del pacchetto così come sono quando vengono utilizzati in nuget.org.

## <a name="options"></a>Options

| Opzione | Descrizione |
| --- | --- |
| AllVersions | Elencare tutte le versioni di un pacchetto. Per impostazione predefinita, viene visualizzata solo la versione più recente del pacchetto. |
| ConfigFile | File di configurazione NuGet da applicare. Se non specificato, viene usato `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| Guida di | Visualizza le informazioni della Guida per il comando. |
| IncludeDelisted | *(3.2 +)* Visualizza i pacchetti non in elenco. |
| NonInteractive | Evita la richiesta di input o conferme dell'utente. |
| PreRelease | Include i pacchetti di versioni non definitive nell'elenco. |
| Source | Specifica un elenco di origini dei pacchetti in cui eseguire la ricerca. |
| Livello di dettaglio | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

Elencare tutti i pacchetti dai feed configurati:
```
nuget list
```
Elencare i pacchetti correlati ad Azure con dettaglio dettagliato:
```
nuget list Azure -Verbosity detailed
```
Elencare tutte le versioni dei pacchetti correlati ad Azure dai feed configurati:
```
nuget list Azure -AllVersions
```
Elencare tutte le versioni dei pacchetti correlati a JSON dall'origine/feed specificata:
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
Elencare i pacchetti correlati a JSON da più origini/feed:
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

