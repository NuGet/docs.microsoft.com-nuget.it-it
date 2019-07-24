---
title: Comando della Guida CLI di NuGet
description: Riferimento per il comando della Guida di NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327798"
---
# <a name="help-or--command-nuget-cli"></a>help or ? (interfaccia della riga di comando di NuGet)

**Si applica a:** tutte le &bullet; **versioni supportate**: tutti

Visualizza informazioni generali sulla guida e informazioni su comandi specifici.

## <a name="usage"></a>Utilizzo

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

dove [Command] identifica un comando specifico per il quale visualizzare la guida.

> [!Warning]
> Con alcuni comandi, prestare attenzione a specificare  prima di tutto la Guida `nuget help install`, come con, perché in NuGet.org è presente un pacchetto denominato "Help". Se si assegna il comando `nuget install help`, non si otterrà la guida sul comando di installazione, ma si installerà il pacchetto denominato Help.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| Tutti | Stampa la guida dettagliata per tutti i comandi disponibili; viene ignorato se viene specificato un comando specifico. |
| ConfigFile | File di configurazione NuGet da applicare. Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| ? | Visualizza le informazioni della Guida per il comando della guida. |
| Markdown | Stampa la guida dettagliata nel formato Markdown quando viene `-All`usato con. In caso contrario, verrà ignorato. |
| NonInteractive | Evita la richiesta di input o conferme dell'utente. |
| Verbosity | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
