---
title: Comando config NuGet CLI
description: Riferimento per il comando config di nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 9deab9fcca740ea99da61b7d54700a29c1813e88
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818165"
---
# <a name="config-command-nuget-cli"></a>comando config (NuGet CLI)

**Si applica a:** tutti &bullet; **le versioni supportate**: tutti

Ottiene o imposta i valori di configurazione NuGet. Per ulteriori informazioni sulla sintassi, vedere [configurazione NuGet comportamento](../consume-packages/configuring-nuget-behavior.md). Per ulteriori informazioni sui nomi di chiave consentiti, vedere il [riferimento al file di configurazione NuGet](../reference/nuget-config-file.md).

## <a name="usage"></a>Utilizzo

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

dove `<name>` e `<value>` specificare una coppia chiave-valore da impostare nella configurazione. È possibile specificare un numero di coppie in base alle esigenze. Per rimuovere un valore, specificare il nome e il `=` sign ma nessun valore.

Per i nomi di chiave consentiti, vedere il [riferimento al file di configurazione NuGet](../reference/nuget-config-file.md).

In NuGet 3.4 + `<value>` consente [le variabili di ambiente](cli-ref-environment-variables.md).

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| AsPath | Restituisce la configurazione di valore come un percorso, ignorati quando `-Set` viene utilizzato. |
| ConfigFile | Il file di configurazione NuGet da modificare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.|
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| Non interattivo | Elimina richieste per l'input dell'utente o le conferme. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

### <a name="examples"></a>Esempi

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
