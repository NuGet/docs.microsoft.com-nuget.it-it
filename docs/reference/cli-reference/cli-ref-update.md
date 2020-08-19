---
title: Comando di aggiornamento CLI di NuGet
description: Riferimento per il comando nuget.exe Update
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 84f939188ac190f6d539f8ee2b422049a274f178
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622577"
---
# <a name="update-command-nuget-cli"></a>comando Update (interfaccia della riga di comando di NuGet)

**Si applica a:** versioni supportate per l'utilizzo di pacchetti &bullet; **:** tutti

Esegue l'aggiornamento di tutti i pacchetti in un progetto (usando `packages.config`) alle versioni disponibili più recenti. È consigliabile eseguire [' Restore '](cli-ref-restore.md) prima di eseguire `update` . Per aggiornare un singolo pacchetto, usare [`nuget install`](cli-ref-install.md) senza specificare un numero di versione, nel qual caso NuGet installa la versione più recente.

Nota: non `update` funziona con l'interfaccia della riga di comando in esecuzione in mono (Mac OSX o Linux) o quando si usa il formato PackageReference.

Il `update` comando Aggiorna inoltre i riferimenti ad assembly nel file di progetto, a condizione che tali riferimenti esistano già. Se un pacchetto aggiornato include un assembly aggiunto, *non* viene aggiunto un nuovo riferimento. Anche per le nuove dipendenze dei pacchetti non sono stati aggiunti riferimenti ad assembly. Per includere queste operazioni come parte di un aggiornamento, aggiornare il pacchetto in Visual Studio usando l'interfaccia utente di gestione pacchetti o la console di gestione pacchetti.

Questo comando può essere usato anche per aggiornare nuget.exe stesso usando il flag *-self* .

## <a name="usage"></a>Uso

```cli
nuget update <configPath> [options]
```

dove `<configPath>` identifica un `packages.config` file di soluzione o che elenca le dipendenze del progetto.

## <a name="options"></a>Opzioni

- **`-ConfigFile`**

  File di configurazione NuGet da applicare. Se non è specificato, `%AppData%\NuGet\NuGet.Config` viene usato (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  Specifica l'azione predefinita quando un file di un pacchetto esiste già nel progetto di destinazione. Impostare su `Overwrite` per sovrascrivere sempre i file. Impostare su `Ignore` per ignorare i file.

  `PromptUser`Per impostazione predefinita, l'azione richiederà tutti i file in conflitto, a meno che non `OverwriteAll` `IgnoreAll` sia specificato o, che verrà applicato a tutti i file rimanenti.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Impone l'esecuzione nuget.exe usando impostazioni cultura invarianti in lingua inglese.

- **`-?|-help`**

  Visualizza le informazioni della Guida per il comando.

- **`-Id`**

  Specifica un elenco di ID di pacchetto da aggiornare.

- **`-MSBuildPath`**

  *(4.0 +)* Specifica il percorso di MSBuild da usare con il comando, avendo la precedenza su `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 +)* Specifica la versione di MSBuild da usare con questo comando. I valori supportati sono 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Per impostazione predefinita, viene scelto MSBuild nel percorso; in caso contrario, per impostazione predefinita viene impostata la versione più recente di MSBuild.

- **`-NonInteractive`**

  Evita la richiesta di input o conferme dell'utente.

- **`-PreRelease`**

  Consente l'aggiornamento alle versioni provvisorie. Questo flag non è obbligatorio quando si aggiornano i pacchetti di versioni non definitive già installati.

- **`-RepositoryPath`**

  Specifica la cartella locale in cui sono installati i pacchetti.

- **`-Safe`**

  Specifica che verranno installati solo gli aggiornamenti con la versione più recente disponibile all'interno della stessa versione principale e secondaria del pacchetto installato.

- **`-Self`**

  Aggiorna nuget.exe alla versione più recente. tutti gli altri argomenti vengono ignorati.

- **`-Source`**

  Specifica l'elenco di origini di pacchetti (come URL) da usare per gli aggiornamenti. Se omesso, il comando usa le origini fornite nei file di configurazione, vedere [configurazioni comuni di NuGet](../../consume-packages/configuring-nuget-behavior.md).

- **`-Verbosity [normal|quiet|detailed]`**

  Specifica la quantità di dettaglio visualizzata nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .

- **`-Version`**

  Se utilizzata con un ID pacchetto, specifica la versione del pacchetto da aggiornare.

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
