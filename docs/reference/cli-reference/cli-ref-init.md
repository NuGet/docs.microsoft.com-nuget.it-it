---
title: Comando init CLI di NuGet
description: Riferimento per il comando nuget.exe init
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f37572624cea744ce60a9a2e58ad3cbe2696cb9e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780076"
---
# <a name="init-command-nuget-cli"></a>comando init (interfaccia della riga di comando di NuGet)

**Si applica a:** versioni supportate per la creazione di pacchetti &bullet; **:** 3.3 +

Copia tutti i pacchetti da una cartella flat in una cartella di destinazione usando un layout gerarchico come descritto per il [comando Aggiungi](cli-ref-add.md). Ovvero, l'utilizzo `init` di equivale a utilizzare il `add` comando su ogni pacchetto nella cartella.

Come per `add` , la destinazione deve essere una cartella locale o un percorso UNC; I repository del pacchetto HTTP, ad esempio nuget.org o i server privati, non sono supportati.

## <a name="usage"></a>Utilizzo

```cli
nuget init <source> <destination> [options]
```

dove `<source>` è la cartella che contiene i pacchetti e `<destination>` è la cartella locale o il percorso UNC in cui vengono copiati i pacchetti.

## <a name="options"></a>Opzioni

- **`-ConfigFile`**

  File di configurazione NuGet da applicare. Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-Expand`**

  Aggiunge tutti i file in ogni pacchetto aggiunto all'origine del pacchetto. uguale `-Expand` a quello del `add` comando.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.

- **`-?|-help`**

  Visualizza le informazioni della Guida per il comando.

- **`-NonInteractive`**

  Evita la richiesta di input o conferme dell'utente.

- **`-Verbosity [normal|quiet|detailed]`**

  Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
