---
title: Comando setapikey NuGet CLI
description: Informazioni di riferimento per il comando setapikey nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549220"
---
# <a name="setapikey-command-nuget-cli"></a>comando setapikey (NuGet CLI)

**Si applica a:** utilizzo di un pacchetto, la pubblicazione &bullet; **le versioni supportate:** tutti

Consente di salvare una chiave API per un URL del server specificato in `NuGet.Config` in modo che non è necessario specificare per i comandi successivi.

## <a name="usage"></a>Utilizzo

```cli
nuget setapikey <key> -Source <url> [options]
```

in cui `<source>` identifica il server e `<key>` è la chiave o password per salvare. Se `<source>` viene omesso, viene usato nuget.org.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | Il file di configurazione di NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.|
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| Non interattive | Elimina richieste di input o conferme dell'utente. |
| Livello di dettaglio | Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
