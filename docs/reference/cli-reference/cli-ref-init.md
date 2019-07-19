---
title: Comando init CLI di NuGet
description: Informazioni di riferimento sul comando NuGet. exe init
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327778"
---
# <a name="init-command-nuget-cli"></a>comando init (interfaccia della riga di comando di NuGet)

**Si applica a:** &bullet; **versioni supportate** per la creazione di pacchetti: 3.3+

Copia tutti i pacchetti da una cartella flat in una cartella di destinazione usando un layout gerarchico come descritto per il [comando Aggiungi](cli-ref-add.md). Ovvero, l'utilizzo `init` di equivale a utilizzare il `add` comando su ogni pacchetto nella cartella.

Come per `add`, la destinazione deve essere una cartella locale o un percorso UNC; I repository del pacchetto HTTP, ad esempio nuget.org o i server privati, non sono supportati.

## <a name="usage"></a>Utilizzo

```cli
nuget init <source> <destination> [options]
```

dove `<source>` è la cartella che contiene i `<destination>` pacchetti e è la cartella locale o il percorso UNC in cui vengono copiati i pacchetti.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | File di configurazione NuGet da applicare. Se non è specificato `%AppData%\NuGet\NuGet.Config` , viene usato ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| Expand | Aggiunge tutti i file in ogni pacchetto aggiunto all'origine del pacchetto. uguale a quello del `add`comando. `-Expand` |
| ? | Visualizza le informazioni della Guida per il comando. |
| NonInteractive | Evita la richiesta di input o conferme dell'utente. |
| Verbosity | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
