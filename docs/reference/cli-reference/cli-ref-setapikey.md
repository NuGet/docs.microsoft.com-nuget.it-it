---
title: Comando setApiKey dell'interfaccia della riga di comando NuGet
description: Riferimento per il comando nuget.exe setApiKey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b84d4257c580f6e734c26ebfc589be27bea10c82
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622811"
---
# <a name="setapikey-command-nuget-cli"></a>comando setApiKey (interfaccia della riga di comando di NuGet)

**Si applica a:** utilizzo del pacchetto, pubblicazione delle &bullet; **versioni supportate:** tutti

Salva una chiave API per un URL del server specificato in in `NuGet.Config` modo che non debba essere immessa per i comandi successivi.

## <a name="usage"></a>Uso

```cli
nuget setapikey <key> -Source <url> [options]
```

dove `<source>` identifica il server e `<key>` è la chiave da salvare. Se `<source>` viene omesso, viene utilizzato NuGet.org. 

> [!NOTE]
> La chiave API non viene usata per l'autenticazione con il feed privato. Fare riferimento al [ `nuget sources` comando](../cli-reference/cli-ref-sources.md) per gestire le credenziali per l'autenticazione con l'origine.
> Le chiavi API possono essere ottenute dai singoli server NuGet. Per creare e gestire APIKeys per nuget.org, vedere [acquisizione-an-API-Key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)

## <a name="options"></a>Opzioni

- **`-ConfigFile`**

  File di configurazione NuGet da applicare. Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.

- **`-?|-help`**

  Visualizza le informazioni della Guida per il comando.

- **`-NonInteractive`**

  Evita la richiesta di input o conferme dell'utente.

- **`-src|-Source`**

  URL del server in cui la chiave API è valida.

- **`-Verbosity [normal|quiet|detailed]`**

  Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
