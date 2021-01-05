---
title: Comando elenco dell'interfaccia della riga di comando NuGet
description: Riferimento per il comando elenco nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d8e5c8574b44375e651f3ff1a4868681b3ce6d66
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699852"
---
# <a name="list-command-nuget-cli"></a>comando list (interfaccia della riga di comando di NuGet)

**Si applica a:** utilizzo del pacchetto, pubblicazione delle &bullet; **versioni supportate:** tutti

Visualizza un elenco di pacchetti da un'origine specificata. Se non viene specificata alcuna origine, vengono utilizzate tutte le origini definite nel file di configurazione globale `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` . Se `NuGet.Config` non specifica alcuna origine, `list` Usa il feed predefinito (NuGet.org).

## <a name="usage"></a>Utilizzo

```cli
nuget list [search terms] [options]
```

dove i termini di ricerca facoltativi filtrano l'elenco visualizzato. I [termini di ricerca](../../consume-packages/finding-and-choosing-packages.md#search-syntax) vengono applicati ai nomi di pacchetti, tag e descrizioni del pacchetto così come sono quando vengono utilizzati in NuGet.org. 

## <a name="options"></a>Opzioni

- **`-AllVersions`**

  Elencare tutte le versioni di un pacchetto. Per impostazione predefinita, viene visualizzata solo la versione più recente del pacchetto.

- **`-ConfigFile`**

  File di configurazione NuGet da applicare. Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.

- **`-?|-help`**

  Visualizza le informazioni della Guida per il comando.

- **`-IncludeDelisted`**

  *(3.2 +)* Visualizza i pacchetti non in elenco.

- **`-NonInteractive`**

  Evita la richiesta di input o conferme dell'utente.

- **`-PreRelease`**

  Include i pacchetti di versioni non definitive nell'elenco.

- **`-Source`**

  Origine del pacchetto da cercare. È possibile specificare più origini usando l' `-Source` opzione più volte.

- **`-Verbosity [normal|quiet|detailed]`**

  Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .

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
