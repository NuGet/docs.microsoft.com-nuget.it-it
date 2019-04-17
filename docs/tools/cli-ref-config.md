---
title: Comando config di NuGet CLI
description: Informazioni di riferimento per il comando config nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 376b69186ad22d4d94a1df51146b833a1f6f9bd9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546478"
---
# <a name="config-command-nuget-cli"></a>comando config di NuGet CLI)

**Si applica a:** tutte &bullet; **le versioni supportate**: tutti

Ottiene o imposta i valori di configurazione NuGet. Per altre informazioni sulla sintassi, vedere [configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md). Per informazioni dettagliate sui nomi di chiave consentiti, vedere la [riferimento al file di configurazione NuGet](../reference/nuget-config-file.md).

## <a name="usage"></a>Utilizzo

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

in cui `<name>` e `<value>` specificare una coppia chiave-valore da impostare nella configurazione. È possibile specificare un numero di coppie in base alle esigenze. Per rimuovere un valore, specificare il nome e il `=` sign ma nessun valore.

Per i nomi di chiave consentiti, vedere la [riferimento al file di configurazione NuGet](../reference/nuget-config-file.md).

In NuGet 3.4 + `<value>` utilizzabile [variabili di ambiente](cli-ref-environment-variables.md).

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| AsPath | Restituisce la configurazione di valore come percorso UNC, ignorati quando `-Set` viene usato. |
| ConfigFile | Il file di configurazione di NuGet da modificare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.|
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese. |
| Help | Visualizza la Guida informazioni per il comando. |
| NonInteractive | Elimina richieste di input o conferme dell'utente. |
| Verbosity | Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

### <a name="examples"></a>Esempi

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
