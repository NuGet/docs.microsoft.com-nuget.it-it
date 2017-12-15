---
title: Comando di NuGet CLI setapikey | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a64c0462-973d-4100-ba3f-8902a2b127f7
description: Riferimento per il comando di nuget.exe setapikey
keywords: NuGet setapikey riferimento, il comando setapikey
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a07c35b8bdd57157391e391e04a90204342b1d5c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
## <a name="setapikey-command-nuget-cli"></a>comando setapikey (NuGet CLI)

**Si applica a:** il consumo di pacchetti, pubblicazione &bullet; **le versioni supportate:** tutti

Salva una chiave API per un URL del server specificato in `NuGet.Config` in modo che non deve essere inserito per i comandi successivi.

## <a name="usage"></a>Utilizzo

```
nuget setapikey <key> -Source <url> [options]
```

dove `<source>` identifica il server e `<key>` è la chiave o una password per salvare. Se `<source>` viene omesso, verrà utilizzato nuget.org.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | *(2.5 +)*  Questo file di configurazione da modificare. Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| Non interattivo | Elimina richieste per l'input dell'utente o le conferme. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate (2.5 +)*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
