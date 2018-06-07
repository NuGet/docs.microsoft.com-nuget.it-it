---
title: Comando setapikey NuGet CLI
description: Riferimento per il comando di nuget.exe setapikey
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 66fc62074b4e7c39ff2ed6b515eee9f821530536
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817684"
---
# <a name="setapikey-command-nuget-cli"></a>comando setapikey (NuGet CLI)

**Si applica a:** il consumo di pacchetti, pubblicazione &bullet; **le versioni supportate:** tutti

Salva una chiave API per un URL del server specificato in `NuGet.Config` in modo che non deve essere inserito per i comandi successivi.

## <a name="usage"></a>Utilizzo

```cli
nuget setapikey <key> -Source <url> [options]
```

dove `<source>` identifica il server e `<key>` è la chiave o una password per salvare. Se `<source>` viene omesso, verrà utilizzato nuget.org.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | Il file di configurazione NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.|
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| Non interattivo | Elimina richieste per l'input dell'utente o le conferme. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
