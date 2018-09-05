---
title: Comando di NuGet CLI?
description: Informazioni di riferimento per il comando help nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546563"
---
# <a name="help-or--command-nuget-cli"></a>help or ? (interfaccia della riga di comando di NuGet)

**Si applica a:** tutte &bullet; **le versioni supportate**: tutti

Generale consente di visualizzare informazioni della Guida e informazioni sui comandi specifici per il supporto.

## <a name="usage"></a>Utilizzo

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

dove [comando] identifica un comando specifico per cui si desidera visualizzare la Guida.

> [!Warning]
> Con alcuni comandi, tenere conto specificare *aiutare* prima, come con `nuget help install`, essendo presente un pacchetto denominato "help" su nuget.org. Qualora il Licenziatario fornisca il comando `nuget install help`, si otterranno della Guida sul comando install ma verranno invece installare il pacchetto denominato della Guida.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| Tutti | Stampa una Guida dettagliata per tutti i comandi disponibili; ignorato se viene fornito un comando specifico. |
| ConfigFile | Il file di configurazione di NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.|
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando della Guida in linea se stesso. |
| Markdown | Stampa la Guida dettagliata in formato markdown quando usato con `-All`. Ignorato in caso contrario. |
| Non interattive | Elimina richieste di input o conferme dell'utente. |
| Livello di dettaglio | Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
