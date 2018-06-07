---
title: Comando help NuGet CLI
description: Riferimento per il comando della Guida di nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d7112209a0a2a267343c3458ebacaf6b744786a9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818256"
---
# <a name="help-or--command-nuget-cli"></a>help or ? (interfaccia della riga di comando di NuGet)

**Si applica a:** tutti &bullet; **le versioni supportate**: tutti

Generale consente di visualizzare informazioni della Guida e le informazioni sui comandi specifici.

## <a name="usage"></a>Utilizzo

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

dove [comando] identifica un comando specifico per cui si desidera visualizzare la Guida.

> [!Warning]
> Con alcuni comandi, tenere in considerazione specificare *Guida* prima, come con `nuget help install`, perché è un pacchetto denominato "help" in nuget.org. Se si fornisce il comando `nuget install help`, si otterranno della Guida sul comando di installazione, ma invece verrà installato il pacchetto denominato della Guida.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| Tutti | Stampa la Guida dettagliata per tutti i comandi disponibili; ignorato se non viene specificato un comando specifico. |
| ConfigFile | Il file di configurazione NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.|
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando della Guida. |
| Markdown | Stampare informazioni della Guida dettagliate in formato markdown se utilizzata con `-All`. Ignorato in caso contrario. |
| Non interattivo | Elimina richieste per l'input dell'utente o le conferme. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
