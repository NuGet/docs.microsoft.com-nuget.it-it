---
title: Comando help NuGet CLI | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 780d7f52-d6c6-45cd-8a62-218ff8c0b270
description: Riferimento per il comando della Guida di nuget.exe
keywords: riferimento alla Guida NuGet, comandi della Guida.
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 55dc263fedd7ed5a3e48b76dbc9a3ccc220655cf
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="help-or--command-nuget-cli"></a>Guida in linea o? comando (CLI NuGet)

**Si applica a:** tutti &bullet; **le versioni supportate**: tutti

Generale consente di visualizzare informazioni della Guida e le informazioni sui comandi specifici.

## <a name="usage"></a>Utilizzo

```
nuget help [command] [options]
nuget ? [command] [options]
```

dove [comando] identifica un comando specifico per cui si desidera visualizzare la Guida.

> [!Warning]
> Con alcuni comandi, tenere in considerazione specificare *Guida* prima, come con `nuget help install`, perché è un pacchetto denominato "help" in nuget.org. Se si fornisce il comando `nuget install help`, si otterrà non della Guida per il comando di installazione, ma invece verrà installato il pacchetto denominato della Guida.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| Tutti | Stampa la Guida dettagliata per tutti i comandi disponibili; ignorato se non viene specificato un comando specifico. |
| ConfigFile | *(2.5 +)*  Questo file di configurazione da applicare. Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando della Guida. |
| Markdown | Stampare informazioni della Guida dettagliate in formato markdown se utilizzata con `-All`. Ignorato in caso contrario. |
| Non interattivo | Elimina richieste per l'input dell'utente o le conferme. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate (2.5 +)*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
