---
title: Comando di NuGet CLI init
description: Informazioni di riferimento per il comando init nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551410"
---
# <a name="init-command-nuget-cli"></a>comando Init (NuGet CLI)

**Si applica a:** creazione del pacchetto &bullet; **le versioni supportate:** 3.3 +

Copia tutti i pacchetti da una cartella flat in una cartella di destinazione utilizzando un layout organizzato gerarchicamente, come descritto per il [Aggiungi comando](cli-ref-add.md). Vale a dire usando `init` equivale all'uso di `add` comando in ogni pacchetto nella cartella.

Come con `add`, la destinazione deve essere una cartella locale o un percorso UNC. I repository dei pacchetti HTTP, ad esempio nuget.org o server privati non sono supportati.

## <a name="usage"></a>Utilizzo

```cli
nuget init <source> <destination> [options]
```

in cui `<source>` è la cartella che contiene i pacchetti e `<destination>` è la cartella locale o il nome di percorso UNC in cui vengono copiati i pacchetti.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | Il file di configurazione di NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.|
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese. |
| Expand | Aggiunge tutti i file in ogni pacchetto che viene aggiunto all'origine del pacchetto; uguale allo `-Expand` con il `add` comando. |
| ? | Visualizza la Guida informazioni per il comando. |
| Non interattive | Elimina richieste di input o conferme dell'utente. |
| Livello di dettaglio | Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
