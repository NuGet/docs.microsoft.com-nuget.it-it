---
title: Comando config CLI di NuGet
description: Riferimento per il comando nuget.exe config
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3d50c12e34f71d7a62fe177da1dbb33eb702347a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775966"
---
# <a name="config-command-nuget-cli"></a>comando config (interfaccia della riga di comando di NuGet)

**Si applica a:** tutte le &bullet; **versioni supportate**: tutti

Ottiene o imposta i valori di configurazione NuGet. Per ulteriori informazioni sull'utilizzo, vedere [configurazioni comuni di NuGet](../../consume-packages/configuring-nuget-behavior.md). Per informazioni dettagliate sui nomi di chiave consentiti, vedere il [riferimento al file di configurazione NuGet](../nuget-config-file.md).

## <a name="usage"></a>Utilizzo

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

dove `<name>` e `<value>` specificano una coppia chiave-valore da impostare nella configurazione. È possibile specificare il numero desiderato di coppie. Per rimuovere un valore, specificare il nome e il `=` segno senza alcun valore.

Per i nomi di chiave consentiti, vedere informazioni di [riferimento sul file di configurazione NuGet](../nuget-config-file.md).

In NuGet 3.4 +, `<value>` può usare le [variabili di ambiente](cli-ref-environment-variables.md).

## <a name="options"></a>Opzioni


- **`AsPath`**

  Restituisce il valore di configurazione come percorso, ignorato quando `-Set` si utilizza.

- **`-ConfigFile`**

  File di configurazione NuGet da applicare. Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.

- **`-?|-help`**

  Visualizza le informazioni della Guida per il comando.

- **`-NonInteractive`**

  Evita la richiesta di input o conferme dell'utente.

- **`-Set`**

  Una per più coppie chiave-valore da impostare nel file config.

- **`-Verbosity [normal|quiet|detailed]`**

  Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

### <a name="examples"></a>Esempi

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
