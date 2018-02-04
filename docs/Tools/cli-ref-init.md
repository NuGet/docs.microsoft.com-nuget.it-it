---
title: Comando di NuGet CLI init | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando di nuget.exe init
keywords: NuGet init riferimento, il comando init
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6d7710cd024e2c2956fb73aa767c3be55b9fb0f9
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2018
---
# <a name="init-command-nuget-cli"></a>comando Init (NuGet CLI)

**Si applica a:** creazione di pacchetti &bullet; **le versioni supportate:** 3.3 +

Copia tutti i pacchetti da una cartella in una cartella di destinazione utilizzando un layout organizzato gerarchicamente, come descritto per il [aggiungere comando](cli-ref-add.md). Vale a dire usando `init` equivale all'utilizzo di `add` comando in ogni pacchetto nella cartella.

Come con `add`, la destinazione deve essere una cartella locale o un percorso UNC. Repository di pacchetti HTTP, ad esempio nuget.org o server private non sono supportati.

## <a name="usage"></a>Utilizzo

```cli
nuget init <source> <destination> [options]
```

dove `<source>` è la cartella contenente i pacchetti e `<destination>` è la cartella locale o un nome di percorso UNC in cui vengono copiati i pacchetti.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | Il file di configurazione NuGet da applicare. Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| Expand | Aggiunge tutti i file in ogni pacchetto che viene aggiunto all'origine del pacchetto; uguale a `-Expand` con il `add` comando. |
| ? | Visualizza la Guida informazioni per il comando. |
| NonInteractive | Elimina richieste per l'input dell'utente o le conferme. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
