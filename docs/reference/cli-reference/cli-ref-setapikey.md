---
title: Comando setApiKey dell'interfaccia della riga di comando NuGet
description: Informazioni di riferimento per il comando setApiKey di NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327608"
---
# <a name="setapikey-command-nuget-cli"></a>comando setApiKey (interfaccia della riga di comando di NuGet)

**Si applica a:** utilizzo del pacchetto &bullet; , pubblicazione delle **versioni supportate:** tutti

Salva una chiave API per un URL del server specificato `NuGet.Config` in in modo che non debba essere immessa per i comandi successivi.

## <a name="usage"></a>Utilizzo

```cli
nuget setapikey <key> -Source <url> [options]
```

dove `<source>` identifica il server e `<key>` è la chiave o la password da salvare. Se `<source>` viene omesso, viene utilizzato NuGet.org.

## <a name="options"></a>Opzioni

| Opzione | DESCRIZIONE |
| --- | --- |
| ConfigFile | File di configurazione NuGet da applicare. Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| Help | Visualizza le informazioni della Guida per il comando. |
| NonInteractive | Evita la richiesta di input o conferme dell'utente. |
| Verbosity | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
