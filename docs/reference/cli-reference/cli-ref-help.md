---
title: Comando della Guida CLI di NuGet
description: Riferimento per il comando della Guida nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 12776b7c16aeef223a0b682ee2468edec8ea3295
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623110"
---
# <a name="help-or--command-nuget-cli"></a>help o ? (interfaccia della riga di comando di NuGet)

**Si applica a:** tutte le &bullet; **versioni supportate**: tutti

Visualizza informazioni generali sulla guida e informazioni su comandi specifici.

## <a name="usage"></a>Uso

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

dove [Command] identifica un comando specifico per il quale visualizzare la guida.

> [!Warning]
> Con alcuni comandi, prestare attenzione a specificare prima di tutto la *Guida* , come con `nuget help install` , perché in NuGet.org è presente un pacchetto denominato "Help". Se si assegna il comando `nuget install help` , non si otterrà la guida sul comando di installazione, ma si installerà il pacchetto denominato Help.

## <a name="options"></a>Opzioni

- **`-All`**

  Stampa la guida dettagliata per tutti i comandi disponibili; viene ignorato se viene specificato un comando specifico.

- **`-ConfigFile`**

  File di configurazione NuGet da applicare. Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.

- **`-?|-help`**

  Visualizza le informazioni della Guida per il comando.

- **`-Markdown`**

  Stampa la guida dettagliata nel formato Markdown quando viene usato con `-All` . In caso contrario, verrà ignorato.

- **`-NonInteractive`**

  Evita la richiesta di input o conferme dell'utente.

- **`-Verbosity [normal|quiet|detailed]`**

  Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
