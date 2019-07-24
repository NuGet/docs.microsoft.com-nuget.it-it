---
title: Comando config CLI di NuGet
description: Riferimento per il comando di configurazione NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433309"
---
# <a name="config-command-nuget-cli"></a>comando config (interfaccia della riga di comando di NuGet)

**Si applica a:** tutte le &bullet; **versioni supportate**: tutti

Ottiene o imposta i valori di configurazione NuGet. Per ulteriori informazioni sull'utilizzo, vedere [configurazioni comuni di NuGet](../../consume-packages/configuring-nuget-behavior.md). Per informazioni dettagliate sui nomi di chiave consentiti, vedere il [riferimento al file di configurazione NuGet](../nuget-config-file.md).

## <a name="usage"></a>Utilizzo

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

dove `<name>` e`<value>` specificano una coppia chiave-valore da impostare nella configurazione. È possibile specificare il numero desiderato di coppie. Per rimuovere un valore, specificare il nome e il `=` segno senza alcun valore.

Per i nomi di chiave consentiti, vedere informazioni di [riferimento sul file di configurazione NuGet](../nuget-config-file.md).

In NuGet 3.4 +, `<value>` può usare le [variabili di ambiente](cli-ref-environment-variables.md).

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| AsPath | Restituisce il valore di configurazione come percorso, ignorato quando `-Set` si utilizza. |
| ConfigFile | File di configurazione NuGet da modificare. Se non specificato, viene usato`%AppData%\NuGet\NuGet.Config` il file predefinito (Windows) o `~/.config/NuGet/NuGet.Config` (Mac/Linux) o `~/.nuget/NuGet/NuGet.Config` (varia in base alla distribuzione del sistema operativo).|
| ForceEnglishOutput | *(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| Help | Visualizza le informazioni della Guida per il comando. |
| NonInteractive | Evita la richiesta di input o conferme dell'utente. |
| Verbosity | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

### <a name="examples"></a>Esempi

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
