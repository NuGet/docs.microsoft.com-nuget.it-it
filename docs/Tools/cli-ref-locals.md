---
title: Comando di NuGet CLI variabili locali | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Riferimento per il comando di nuget.exe variabili locali
keywords: riferimento di variabili locali NuGet, il comando di variabili locali
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0122c79e55b12838bd123cf91bfcbc5dbbd2a65c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="locals-command-nuget-cli"></a>comando variabili locali (NuGet CLI)

**Si applica a:** pacchetto consumo &bullet; **versioni supportate:** 3.3 +

Cancella o elenca le risorse locali di NuGet, ad esempio il *cache http*, *globale pacchetti* cartella e la cartella temporanea. Il `locals` comando può essere utilizzato anche per visualizzare un elenco di tali percorsi. Per altre informazioni, vedere [gestione dei pacchetti globali e alla cartella della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Utilizzo

```cli
nuget locals <folder> [options]
```

in cui `<folder>` è uno dei `all`, `http-cache`, `packages-cache` *(3.5 e versioni precedenti)*, `global-packages`, e `temp` *(3.4 +)*.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| Cancella | Cancella la cartella specificata. |
| ConfigFile | Il file di configurazione NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.|
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| List | Elenca il percorso della cartella specificata o i percorsi di tutte le cartelle se usato con *tutti*. |
| NonInteractive | Elimina richieste per l'input dell'utente o le conferme. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Per ulteriori esempi, vedere [gestione dei pacchetti globali e alla cartella della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).
