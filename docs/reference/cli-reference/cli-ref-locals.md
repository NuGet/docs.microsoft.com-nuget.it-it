---
title: Comando variabili locali dell'interfaccia della riga di comando di NuGet
description: Informazioni di riferimento per il comando locals di NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327808"
---
# <a name="locals-command-nuget-cli"></a>Comando locals (interfaccia della riga di comando di NuGet)

**Si applica a:** &bullet; **versioni supportate** per l'utilizzo di pacchetti: 3.3+

Cancella o elenca le risorse NuGet locali, ad esempio la *cache HTTP*, la cartella *Global-Packages* e la cartella Temp. Il `locals` comando può essere usato anche per visualizzare un elenco di tali percorsi. Per ulteriori informazioni, vedere [gestione dei pacchetti globali e delle cartelle della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Utilizzo

```cli
nuget locals <folder> [options]
```

dove `<folder>` è uno dei `all`, `http-cache` `global-packages` `temp` `plugins-cache` , `packages-cache` *(3,5 e versioni precedenti)* ,, *(3.4 +)* e *(4.8 +)* .

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| Cancella | Cancella la cartella specificata. |
| ConfigFile | File di configurazione NuGet da applicare. Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| Help | Visualizza le informazioni della Guida per il comando. |
| List | Indica il percorso della cartella specificata o i percorsi di tutte le cartelle quando vengono utilizzati con *tutti*. |
| NonInteractive | Evita la richiesta di input o conferme dell'utente. |
| Verbosity | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Per altri esempi, vedere [gestione dei pacchetti globali e delle cartelle della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).
