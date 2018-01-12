---
title: Comando config NuGet CLI | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a50295ff-8be9-47d9-a260-822e899334cb
description: Riferimento per il comando config di nuget.exe
keywords: riferimento di configurazione NuGet, il comando di configurazione
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f49751d9747687177e3b6c1890ee9d2919be8d0e
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/10/2018
---
# <a name="config-command-nuget-cli"></a>comando config (NuGet CLI)

**Si applica a:** tutti &bullet; **le versioni supportate**: tutti

Ottiene o imposta i valori di configurazione NuGet. Per ulteriori informazioni sulla sintassi, vedere [configurazione NuGet comportamento](../consume-packages/configuring-nuget-behavior.md). Per ulteriori informazioni sui nomi di chiave consentiti, vedere il [riferimento al file di configurazione NuGet](../Schema/nuget-config-file.md).

## <a name="usage"></a>Utilizzo

```
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

dove `<name>` e `<value>` specificare una coppia chiave-valore da impostare nella configurazione. È possibile specificare un numero di coppie in base alle esigenze. Per rimuovere un valore, specificare il nome e il `=` sign ma nessun valore.

Per i nomi di chiave consentiti, vedere il [riferimento al file di configurazione NuGet](../Schema/nuget-config-file.md).

In NuGet 3.4 + `<value>` consente [le variabili di ambiente](cli-ref-environment-variables.md).

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| AsPath | Restituisce la configurazione di valore come un percorso, ignorati quando `-Set` viene utilizzato. |
| ConfigFile | *(2.5 +)*  Questo file di configurazione da modificare. Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| Non interattivo | Elimina richieste per l'input dell'utente o le conferme. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate (2.5 +)*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

### <a name="examples"></a>Esempi

```
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
