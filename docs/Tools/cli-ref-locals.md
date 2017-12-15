---
title: Comando di NuGet CLI variabili locali | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 7f672c7c-74c9-4296-bc27-4d47882b541c
description: Riferimento per il comando di nuget.exe variabili locali
keywords: riferimento di variabili locali NuGet, il comando di variabili locali
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8cc06eedc20507e2bdd210e40c471ff551b89563
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
## <a name="locals-command-nuget-cli"></a>comando variabili locali (NuGet CLI)

**Si applica a:** pacchetto consumo &bullet; **le versioni supportate:** 3.3 +

Cancella o elenca le risorse locali di NuGet, ad esempio la cache della richiesta http, la cache di pacchetti e la cartella pacchetti globali a livello di computer. Il `locals` comando può essere utilizzato anche per visualizzare un elenco di tali percorsi. Per ulteriori informazioni, vedere [gestione delle NuGet Cache](../consume-packages/managing-the-nuget-cache.md).

## <a name="usage"></a>Utilizzo

```
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
| Elenco | Elenca il percorso della cache specificata o i percorsi di tutte le cache se utilizzata con *tutti*. |
| Non interattivo | Elimina richieste per l'input dell'utente o le conferme. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```
nuget locals all -list
nuget locals http-cache -clear
```
