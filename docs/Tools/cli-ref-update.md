---
title: Aggiornare il comando CLI NuGet | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 61fde945-6983-46a5-8636-da0fada4e641
description: Riferimento per il comando di aggiornamento di nuget.exe
keywords: NuGet Aggiorna riferimento, il comando di pacchetto dell'aggiornamento
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 654144e93a99a4a4f8d79c0db5660cfb7c6c308e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="update-command-nuget-cli"></a>comando di aggiornamento (NuGet CLI)

**Si applica a:** pacchetto consumo &bullet; **le versioni supportate:** tutti

Aggiorna tutti i pacchetti in un progetto (usando `packages.config`) alle versioni più recenti. È consigliabile eseguire ['restore'](#restore) prima di eseguire il `update`. (Per aggiornare un singolo pacchetto, utilizzare [ `nuget install` ](cli-ref-install.md) senza specificare un numero di versione, in cui NuGet case consente di installare la versione più recente.)

Nota: `update` non funziona con l'interfaccia CLI in esecuzione in Mono (Mac OSX o Linux). Il comando non funziona inoltre con i progetti utilizzando `project.json` o PackageReference gestione formati.

Il `update` comando Aggiorna anche i riferimenti all'assembly nel file di progetto, fornito quelli fa riferimento a già esiste. Se un pacchetto aggiornato è un assembly aggiunto, un nuovo riferimento è *non* aggiunto. Inoltre, nuove dipendenze di pacchetto non sono i riferimenti ad assembly aggiunto. Per includere queste operazioni come parte di un aggiornamento, aggiornare il pacchetto in Visual Studio utilizzando la UI Package Manager o la Console di gestione pacchetti.

Questo comando può essere utilizzato anche per aggiornare nuget.exe stesso utilizzando il *-self* flag.

## <a name="usage"></a>Utilizzo

```
nuget update <configPath> [options]
```

dove `<configPath>` identifica uno un `packages.config` o file di soluzione che elenca le dipendenze del progetto.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | *(2.5 +)*  Questo file di configurazione da applicare. Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato. |
| FileConflictAction | *(2.5 +)*  Specifica l'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto. I valori sono *sovrascrivere, ignorare, Nessuno*. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| Id | Specifica un elenco di ID per l'aggiornamento pacchetto. |
| MSBuildPath | *(4.0 +)*  Specifica il percorso di MSBuild da usare con il comando, che avrà la precedenza `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Specifica la versione di MSBuild da usare con questo comando. Valori supportati sono 4, 12, 14, 15. Per impostazione predefinita che viene selezionato il percorso di MSBuild, in caso contrario il valore predefinito la versione più aggiornata di MSBuild. |
| Non interattivo | Elimina richieste per l'input dell'utente o le conferme. |
| Versione provvisoria | Consente l'aggiornamento di versioni non definitive. Questo flag non è richiesto durante l'aggiornamento preliminari pacchetti che sono già installati. |
| RepositoryPath | Specifica la cartella locale in cui sono installati i pacchetti. |
| Safe | Specifica che solo gli aggiornamenti con la versione più recente disponibile all'interno della stessa versione principale e secondaria verrà installato il pacchetto installato. |
| Self | *(1.4 +)*  Aggiorna nuget.exe alla versione più recente; vengono ignorati tutti gli altri argomenti. |
| Origine | Specifica l'elenco delle origini pacchetto (come URL) da usare per gli aggiornamenti. Se omesso, il comando Usa le origini disponibili in file di configurazione, vedere [il comportamento di configurazione NuGet](../Consume-Packages/Configuring-NuGet-Behavior.md). |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate (2.5 +)*. |
| Versione | Se usato con un ID di pacchetto, specifica la versione del pacchetto da aggiornare. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
