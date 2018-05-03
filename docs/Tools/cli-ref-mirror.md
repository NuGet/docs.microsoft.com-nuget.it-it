---
title: Comando mirror NuGet CLI
description: Riferimento per il comando di nuget.exe mirror
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5ba13196d385abf42a5af2faa3fe6f0e80fb59d8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="mirror-command-nuget-cli"></a>comando mirror (NuGet CLI)

**Si applica a:** la pubblicazione del pacchetto &bullet; **le versioni supportate:** deprecata in 3.2 +

Riflette un pacchetto e le relative dipendenze dal repository di origine specificato per il repository di destinazione.

> [!NOTE]
> Per abilitare questo comando per le versioni di NuGet prima 3.2, passare a [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), selezionare la versione stabile più recente, scaricare `NuGet.ServerExtensions.dll` e `Nuget-Signed.exe` al disco locale e ridenominazione `Nuget-Signed.exe` a `nuget.exe`.

## <a name="usage"></a>Utilizzo

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

dove `<packageID>` è il pacchetto per eseguire il mirroring, o `<configFilePath>` identifica il `packages.config` file che elenca i pacchetti per eseguire il mirroring.

Il `<listUrlTarget>` specifica il repository di origine e `<publishUrlTarget>` specifica del repository di destinazione.

Se il repository di destinazione si trova in `https://machine/repo` che esegue [NuGet.Server](../hosting-packages/nuget-server.md), gli URL di elenco e push sarà `https://machine/repo/nuget` e `https://machine/repo/api/v2/package`, rispettivamente.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| apiKey | La chiave API per il repository di destinazione. Se non è presente, quello specificato nel file di configurazione viene utilizzato (`%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux)). |
| ? | Visualizza la Guida informazioni per il comando. |
| NoCache | Impedisce l'uso memorizzati nella cache dei pacchetti NuGet. Vedere [gestione dei pacchetti globali e alla cartella della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NOOP | Registra quali possono essere eseguite, ma non esegue le azioni; si presuppone che l'esito positivo per le operazioni di push. |
| Versione provvisoria | Include i pacchetti della versione provvisoria nell'operazione di mirroring. |
| Origine | Un elenco delle origini pacchetto per eseguire il mirroring. Se non vengono specificata alcuna origine, quelli definiti nel file di configurazione (vedere ApiKey precedente) vengono utilizzati, l'impostazione nuget.org se è stata specificata alcuna. |
| Timeout | Specifica il timeout in secondi, per l'inserimento di un server. Il valore predefinito è 300 secondi (5 minuti). |
| Versione | La versione del pacchetto da installare. Se non specificato, la versione più recente è il mirroring. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
