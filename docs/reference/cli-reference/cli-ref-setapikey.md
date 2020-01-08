---
title: Comando setApiKey dell'interfaccia della riga di comando NuGet
description: Informazioni di riferimento per il comando setApiKey di NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383969"
---
# <a name="setapikey-command-nuget-cli"></a>comando setApiKey (interfaccia della riga di comando di NuGet)

**Si applica a:** utilizzo del pacchetto, pubblicazione &bullet; **versioni supportate:** tutti

Salva una chiave API per un URL server specificato in `NuGet.Config` in modo che non debba essere immessa per i comandi successivi.

## <a name="usage"></a>Usage

```cli
nuget setapikey <key> -Source <url> [options]
```

dove `<source>` identifica il server e `<key>` è la chiave o la password da salvare. Se `<source>` viene omesso, viene utilizzato nuget.org.

> [!NOTE]
> La chiave API non viene usata per l'autenticazione con il feed privato. Fare riferimento a [`nuget sources` comando](../cli-reference/cli-ref-sources.md) per gestire le credenziali per l'autenticazione con l'origine.

## <a name="options"></a>Options

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | File di configurazione NuGet da applicare. Se non specificato, viene usato `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| Guida di | Visualizza le informazioni della Guida per il comando. |
| NonInteractive | Evita la richiesta di input o conferme dell'utente. |
| Livello di dettaglio | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
