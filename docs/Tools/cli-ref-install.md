---
title: Comando di installazione NuGet CLI | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando di installazione di nuget.exe
keywords: NuGet riferimento, il comando pacchetto installato
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b77e0e6ce045d1a1e59b29f770b5aca13fc4e7e3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="install-command-nuget-cli"></a>installare comando (CLI NuGet)

**Si applica a:** pacchetto consumo &bullet; **le versioni supportate:** tutti

Scarica e installa un pacchetto in un progetto, verrà utilizzato per la cartella corrente, usando l'origine del pacchetto specificato.

> [!Tip]
> Per scaricare un pacchetto direttamente all'esterno del contesto di un progetto, visitare la pagina del pacchetto su [nuget.org](https://www.nuget.org) e selezionare il **scaricare** collegamento.

Se non vengono specificata alcuna origine, quelli elencati nel file di configurazione globale, `%APPDATA%\NuGet\NuGet.Config`, vengono utilizzati. Vedere [il comportamento di configurazione NuGet](../consume-packages/configuring-nuget-behavior.md) per altri dettagli.

Se non viene specificato alcun pacchetto specifico, `install` installa tutti i pacchetti elencati del progetto `packages.config` file, rendendola simile a [ `restore` ](cli-ref-restore.md).

Il `install` comando non modifichi un file di progetto o `packages.config`; in questo modo è simile a `restore` perché solo aggiunge i pacchetti su disco ma non modificare le dipendenze di un progetto.

Per aggiungere una dipendenza, aggiungere un progetto tramite l'interfaccia utente di gestione di pacchetto o la Console in Visual Studio oppure modificare `packages.config` e quindi eseguire uno `install` o `restore`.

## <a name="usage"></a>Utilizzo

```cli
nuget install <packageID | configFilePath> [options]
```

dove `<packageID>` denomina il pacchetto di installazione (utilizzando la versione più recente), o `<configFilePath>` identifica il `packages.config` file che elenca i pacchetti da installare. È possibile indicare una versione specifica con la `-Version` opzione.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | Il file di configurazione NuGet da applicare. Se non specificato, *%AppData%\NuGet\NuGet.Config* viene utilizzato. |
| DependencyVersion | *(4.4 +)*  Specifica una versione specifica, si esegue l'override del comportamento di risoluzione dipendenza predefinito. |
| DisableParallelProcessing | Disabilita l'installazione di più pacchetti in parallelo. |
| ExcludeVersion | Installa il pacchetto in una cartella denominata con solo il nome del pacchetto e non il numero di versione. |
| FallbackSource | *(3.2 +)*  Un elenco delle origini pacchetto da utilizzare come fallback nel caso in cui il pacchetto non viene trovato nel database primario o di origine predefinita. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| Framework | *(4.4 +)*  Framework di destinazione utilizzato per la selezione delle dipendenze. Il valore predefinito 'Any' Se non specificato. |
| ? | Visualizza la Guida informazioni per il comando. |
| NoCache | Impedisce l'utilizzo di pacchetti dalla cache locale NuGet. |
| NonInteractive | Elimina richieste per l'input dell'utente o le conferme. |
| OutputDirectory | Specifica la cartella in cui sono installati i pacchetti. Se viene specificata alcuna cartella, viene utilizzata la cartella corrente. |
| PackageSaveMode | Specifica i tipi di file da salvare dopo l'installazione del pacchetto: uno dei `nuspec`, `nupkg`, o `nuspec;nupkg`. |
| Versione provvisoria | Consente di pacchetti della versione provvisoria da installare. Questo flag non è necessario durante il ripristino di pacchetti con `packages.config`. |
| RequireConsent | Verifica che il ripristino dei pacchetti è abilitato prima di scaricare e installare i pacchetti. Per informazioni dettagliate, vedere [il ripristino del pacchetto](../consume-packages/package-restore.md). |
| SolutionDirectory | Specifica la cartella radice della soluzione per cui si desidera ripristinare i pacchetti. |
| Origine | Specifica l'elenco delle origini pacchetto (come URL) per l'utilizzo. Se omesso, il comando Usa le origini disponibili in file di configurazione, vedere [il comportamento di configurazione NuGet](../Consume-Packages/Configuring-NuGet-Behavior.md). |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |
| Versione | Specifica la versione del pacchetto da installare. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
