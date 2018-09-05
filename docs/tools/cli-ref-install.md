---
title: Comando di installazione NuGet CLI
description: Informazioni di riferimento per il comando di installazione nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 8261cdb83af72d9d9379124f4c446c7cd2a50299
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549136"
---
# <a name="install-command-nuget-cli"></a>Comando install (interfaccia della riga di comando di NuGet)

**Si applica a:** consumo del pacchetto &bullet; **le versioni supportate:** tutti

Scarica e installa un pacchetto in un progetto, utilizzando per impostazione predefinita nella cartella corrente, usando origini pacchetto specificato.

> [!Tip]
> Per scaricare il pacchetto direttamente all'esterno del contesto di un progetto, visitare la pagina del pacchetto su [nuget.org](https://www.nuget.org) e selezionare il **scaricare** collegamento.

Se non sono specificate origini, quelli elencati nel file di configurazione globali `%appdata%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), vengono usati. Visualizzare [comportamento di configurazione NuGet](../consume-packages/configuring-nuget-behavior.md) per altri dettagli.

Se non ci sono pacchetti specifici vengono specificati, `install` installa tutti i pacchetti elencati del progetto `packages.config` file, rendendola simile [ `restore` ](cli-ref-restore.md).

Il `install` comando non modifica un file di progetto o `packages.config`; in questo modo è simile a `restore` perché solo consente di aggiungere pacchetti su disco ma non modifica le dipendenze del progetto.

Per aggiungere una dipendenza, aggiungere un pacchetto tramite l'interfaccia utente di gestione pacchetti o la Console in Visual Studio oppure modificare `packages.config` ed eseguire uno `install` o `restore`.

## <a name="usage"></a>Utilizzo

```cli
nuget install <packageID | configFilePath> [options]
```

in cui `<packageID>` denomina il pacchetto di installazione (usando la versione più recente), oppure `<configFilePath>` identifica il `packages.config` file che elenca i pacchetti da installare. È possibile indicare una versione specifica con la `-Version` opzione.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | Il file di configurazione di NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.|
| DependencyVersion | *(4.4 +)*  La versione dei pacchetti di dipendenza da usare, che può essere uno dei seguenti:<br/><ul><li>*Più basso* (impostazione predefinita): la versione più bassa</li><li>*HighestPatch*: la versione con patch più bassa principali, più bassa secondaria, più alto</li><li>*HighestMinor*: la versione con il minimo principali, patch secondaria, massima più alto</li><li>*Più alto*: la versione più recente</li></ul> |
| DisableParallelProcessing | Disabilita l'installazione di più pacchetti in parallelo. |
| ExcludeVersion | Installa il pacchetto in una cartella denominata con solo il nome del pacchetto e non il numero di versione. |
| FallbackSource | *(3.2 +)*  Un elenco di origini dei pacchetti da usare come fallback nel caso in cui il pacchetto non viene trovato nel database primario o di un'origine predefinita. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese. |
| Framework | *(4.4 +)*  Framework di destinazione usato per la selezione di dipendenze. Il valore predefinito è 'Any' Se non specificato. |
| ? | Visualizza la Guida informazioni per il comando. |
| NoCache | Impedisce l'uso di pacchetti memorizzati nella cache NuGet. Visualizzare [gestione dei pacchetti globali e le cartelle cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| Non interattive | Elimina richieste di input o conferme dell'utente. |
| OutputDirectory | Specifica la cartella in cui sono installati i pacchetti. Se si specifica alcuna cartella, viene utilizzata la cartella corrente. |
| PackageSaveMode | Specifica i tipi di file da salvare dopo l'installazione del pacchetto: uno dei `nuspec`, `nupkg`, o `nuspec;nupkg`. |
| Versione preliminare | Consente a pacchetti versione non definitivo da installare. Questo flag non è obbligatorio quando il ripristino dei pacchetti con `packages.config`. |
| RequireConsent | Verifica che il ripristino dei pacchetti sia abilitato prima di scaricare e installare i pacchetti. Per informazioni dettagliate, vedere [ripristino dei pacchetti](../consume-packages/package-restore.md). |
| SolutionDirectory | Specifica la cartella radice della soluzione per cui si desidera ripristinare i pacchetti. |
| Origine | Specifica l'elenco delle origini dei pacchetti (sotto forma di URL) per l'uso. Se omesso, il comando Usa le origini fornite nei file di configurazione, vedere [comportamento di configurazione NuGet](../consume-packages/configuring-nuget-behavior.md). |
| Livello di dettaglio | Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*. |
| Versione | Specifica la versione del pacchetto da installare. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
