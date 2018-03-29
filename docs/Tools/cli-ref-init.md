---
title: Comando di NuGet CLI init | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Riferimento per il comando di nuget.exe init
keywords: NuGet init riferimento, il comando init
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 01a3553622020b5868e33ece09cd7555cb712fd3
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="init-command-nuget-cli"></a>comando Init (NuGet CLI)

**Si applica a:** creazione di pacchetti &bullet; **versioni supportate:** 3.3 +

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
| ConfigFile | Il file di configurazione NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.|
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
