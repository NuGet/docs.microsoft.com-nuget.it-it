---
title: Comando di aggiornamento dell'interfaccia della riga di comando di NuGet
description: Riferimento per il comando nuget.exe update
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323648"
---
# <a name="update-command-nuget-cli"></a>Comando update (interfaccia della riga di comando NuGet)

**Si applica a:** Utilizzo pacchetti &bullet; **Versioni supportate:** tutte

Esegue l'aggiornamento di tutti i pacchetti in un progetto (usando `packages.config`) alle versioni disponibili più recenti. È consigliabile eseguire ['restore'](cli-ref-restore.md) prima di eseguire `update` . Per aggiornare un singolo pacchetto, usare senza specificare un numero di versione, nel qual caso [`nuget install`](cli-ref-install.md) NuGet installa la versione più recente.

Nota: non funziona con l'interfaccia della riga di comando in esecuzione in Mono (Mac OSX o Linux) o quando `update` si usa il formato PackageReference.

Il `update` comando aggiorna anche i riferimenti agli assembly nel file di progetto, a condizione che tali riferimenti esistano già. Se a un pacchetto aggiornato è stato aggiunto un assembly, non viene aggiunto *un nuovo* riferimento. Alle nuove dipendenze del pacchetto non vengono aggiunti anche i riferimenti agli assembly. Per includere queste operazioni come parte di un aggiornamento, aggiornare il pacchetto in Visual Studio usando l'interfaccia Gestione pacchetti o la console Gestione pacchetti.

Questo comando può essere usato anche per aggiornare nuget.exe usando il flag *-self.*

## <a name="usage"></a>Utilizzo

```cli
nuget update <configPath> [options]
```

dove `<configPath>` identifica un file di soluzione o che elenca le `packages.config` dipendenze del progetto.

## <a name="options"></a>Opzioni

- **`-ConfigFile`**

  File di configurazione NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` viene usato `~/.nuget/NuGet/NuGet.Config` (Windows) o `~/.config/NuGet/NuGet.Config` (Mac/Linux).
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  Specifica la versione dei pacchetti di dipendenze da usare, che può essere una delle seguenti:<br/><ul><li>*Minimo* (impostazione predefinita): la versione più bassa</li><li>*HighestPatch:* la versione con la patch principale, secondaria più bassa e più alta</li><li>*HighestMinor:* la versione con la patch principale, secondaria più alta e più alta</li><li>*Più alta:* la versione più alta</li><li>*Ignora:* non verranno usati pacchetti di dipendenze</li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  Specifica l'azione predefinita quando un file di un pacchetto esiste già nel progetto di destinazione. Impostare su `Overwrite` per sovrascrivere sempre i file. Impostare su `Ignore` per ignorare i file.

  L'azione, l'impostazione predefinita, richiederà ogni file in conflitto, a meno che non venga specificato o `PromptUser` , che verrà applicato a tutti i file `OverwriteAll` `IgnoreAll` rimanenti.

- **`-ForceEnglishOutput`**

  *(3.5+)* Forza nuget.exe'esecuzione usando impostazioni cultura invarianti basate sull'inglese.

- **`-?|-help`**

  Visualizza le informazioni della Guida per il comando.

- **`-Id`**

  Specifica un elenco di ID pacchetto da aggiornare.

- **`-MSBuildPath`**

  *(4.0+)* Specifica il percorso di MSBuild da usare con il comando , che ha la precedenza su `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2+)* Specifica la versione di MSBuild da usare con questo comando. I valori supportati sono 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9. Per impostazione predefinita, msBuild nel percorso viene selezionato, in caso contrario viene impostata la versione installata più elevata di MSBuild.

- **`-NonInteractive`**

  Elimina le richieste di input o di conferma dell'utente.

- **`-PreRelease`**

  Consente l'aggiornamento alle versioni non definitive. Questo flag non è obbligatorio quando si aggiornano pacchetti non definitive già installati.

- **`-RepositoryPath`**

  Specifica la cartella locale in cui vengono installati i pacchetti.

- **`-Safe`**

  Specifica che verranno installati solo gli aggiornamenti con la versione più recente disponibile nella stessa versione principale e secondaria del pacchetto installato.

- **`-Self`**

  Aggiornamenti `nuget.exe` alla versione più recente. `-Source` È possibile usare tuttavia tutti gli altri argomenti vengono ignorati. Se non viene specificata alcuna origine, verifica `nuget.org` la disponibilità di aggiornamenti indipendentemente dalle `NuGet.Config` impostazioni.

- **`-Source`**

  Specifica l'elenco di origini dei pacchetti (come URL) da usare per gli aggiornamenti. Se omesso, il comando usa le origini fornite nei file di configurazione, vedere [Configurazioni NuGet comuni](../../consume-packages/configuring-nuget-behavior.md).

- **`-Verbosity [normal|quiet|detailed]`**

  Specifica la quantità di dettagli visualizzati nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .

- **`-Version`**

  Se usato con un ID pacchetto, specifica la versione del pacchetto da aggiornare.

Vedere anche [Variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
