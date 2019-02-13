---
title: Comando di aggiornamento di NuGet CLI
description: Informazioni di riferimento per il comando update nuget.exe
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ded9b571324d810c2f0e1a46ea76375a28940406
ms.sourcegitcommit: d5a35a097e6b461ae791d9f66b3a85d5219d7305
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56145605"
---
# <a name="update-command-nuget-cli"></a>Comando update (interfaccia della riga di comando di NuGet)

**Si applica a:** consumo del pacchetto &bullet; **le versioni supportate:** tutti

Aggiorna tutti i pacchetti in un progetto (usando `packages.config`) per le versioni più recenti disponibili. È consigliabile eseguire ['restore'](cli-ref-restore.md) prima di eseguire il `update`. (Per aggiornare un singolo pacchetto, usare [ `nuget install` ](cli-ref-install.md) senza specificare un numero di versione, in cui maiuscole NuGet installa la versione più recente.)

Nota: `update` non funziona con l'interfaccia della riga di comando in esecuzione in Mono (Mac OSX o Linux) o quando si usa il formato PackageReference.

Il `update` comando inoltre aggiorna i riferimenti ad assembly nel file di progetto, purché questi fa già riferimento a esistere. Se un assembly aggiunto dispone di un pacchetto aggiornato, è un nuovo riferimento *non* aggiunto. Inoltre, nuove dipendenze di pacchetto non sono i riferimenti ad assembly aggiunto. Per includere tali operazioni come parte di un aggiornamento, aggiornare il pacchetto in Visual Studio usando il Package Manager UI o la Console di gestione pacchetti.

Questo comando può essere utilizzato anche aggiornare nuget.exe stesso tramite il *-self* flag.

## <a name="usage"></a>Utilizzo

```cli
nuget update <configPath> [options]
```

in cui `<configPath>` identifica uno un `packages.config` o file di soluzione che elenca le dipendenze del progetto.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | Il file di configurazione di NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.|
| FileConflictAction | Specifica l'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti farvi riferimento il progetto. I valori sono *sovrascrivere, ignorare, Nessuno*. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| Id | Specifica un elenco di ID per l'aggiornamento del pacchetto. |
| MSBuildPath | *(4.0 +)*  Specifica il percorso di MSBuild da usare con il comando, hanno la precedenza sui `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Specifica la versione di MSBuild da usare con questo comando. Valori supportati sono 4, 12, 14, 15.1, versione 15.3, versione 15.4, 15.5, 15.6, 15.7, 15.8, 15.9. Per impostazione predefinita che viene selezionato nel proprio percorso di MSBuild, in caso contrario, per impostazione predefinita la versione installata più recente di MSBuild. |
| NonInteractive | Elimina richieste di input o conferme dell'utente. |
| Versione preliminare | Consente l'aggiornamento alle versioni non definitive. Questo flag non è obbligatorio quando l'aggiornamento non definitive dei pacchetti che sono già installate. |
| RepositoryPath | Specifica la cartella locale in cui sono installati i pacchetti. |
| Safe | Specifica che vengono aggiornati solo con la versione più recente disponibile all'interno della stessa versione principale e secondaria come verrà installato il pacchetto installato. |
| self | Aggiorna nuget.exe alla versione più recente; tutti gli altri argomenti vengono ignorati. |
| Origine | Specifica l'elenco delle origini dei pacchetti (sotto forma di URL) da usare per gli aggiornamenti. Se omesso, il comando Usa le origini fornite nei file di configurazione, vedere [comportamento di configurazione NuGet](../consume-packages/configuring-nuget-behavior.md). |
| Livello di dettaglio | Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*. |
| Versione | Se usato con un ID di pacchetto, specifica la versione del pacchetto da aggiornare. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
