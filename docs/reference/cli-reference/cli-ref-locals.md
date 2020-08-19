---
title: Comando variabili locali dell'interfaccia della riga di comando di NuGet
description: Riferimento per il comando nuget.exe variabili locali
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: cdc2b760021ffc4a9e02edacb45beac01cc99bf1
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623058"
---
# <a name="locals-command-nuget-cli"></a>comando locals (interfaccia della riga di comando di NuGet)

**Si applica a:** versioni supportate per l'utilizzo di pacchetti &bullet; **:** 3.3 +

Cancella o elenca le risorse NuGet locali, ad esempio la *cache HTTP*, la cartella *Global-Packages* e la cartella Temp. Il `locals` comando può essere usato anche per visualizzare un elenco di tali percorsi. Per ulteriori informazioni, vedere [gestione dei pacchetti globali e delle cartelle della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Uso

```cli
nuget locals <folder> [options]
```

dove `<folder>` è uno dei `all` , `http-cache` , `packages-cache` *(3,5 e versioni precedenti)*, `global-packages` , `temp` *(3.4 +)* e `plugins-cache` *(4.8 +)*.

## <a name="options"></a>Opzioni

- **`-Clear`**

  Cancella la cartella specificata.

- **`-ConfigFile`**

  File di configurazione NuGet da applicare. Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.

- **`-?|-help`**

  Visualizza le informazioni della Guida per il comando.

- **`-List`**

  Indica il percorso della cartella specificata o i percorsi di tutte le cartelle quando vengono utilizzati con *tutti*.

- **`-NonInteractive`**

  Evita la richiesta di input o conferme dell'utente.

- **`-Verbosity [normal|quiet|detailed]`**

  Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Per altri esempi, vedere [gestione dei pacchetti globali e delle cartelle della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).
