---
title: Comando di NuGet CLI variabili locali | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando di nuget.exe variabili locali
keywords: riferimento di variabili locali NuGet, il comando di variabili locali
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="locals-command-nuget-cli"></a>comando variabili locali (NuGet CLI)

**Si applica a:** pacchetto consumo &bullet; **le versioni supportate:** 3.3 +

Cancella o elenca le risorse locali di NuGet, ad esempio la cache della richiesta http, la cache di pacchetti e la cartella pacchetti globali a livello di computer. Il `locals` comando può essere utilizzato anche per visualizzare un elenco di tali percorsi. Per ulteriori informazioni, vedere [gestione delle NuGet Cache](../consume-packages/managing-the-nuget-cache.md).

## <a name="usage"></a>Utilizzo

```cli
nuget locals <cache> [options]
```

dove `<cache>` è uno dei `all`, `http-cache`, `packages-cache`, `global-packages`, e `temp` *(3.4 +)*.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| Cancella | Cancella la cache specificata. |
| ConfigFile | Il file di configurazione NuGet da applicare. Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| List | Elenca il percorso della cache specificata o i percorsi di tutte le cache se utilizzata con *tutti*. |
| NonInteractive | Elimina richieste per l'input dell'utente o le conferme. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget locals all -list
nuget locals http-cache -clear
```
