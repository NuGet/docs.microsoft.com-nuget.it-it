---
title: Comando di NuGet CLI mirror
description: Informazioni di riferimento per il comando mirror nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550206"
---
# <a name="mirror-command-nuget-cli"></a>Comando mirror (interfaccia della riga di comando di NuGet)

**Si applica a:** pacchetto di pubblicazione &bullet; **le versioni supportate:** deprecato in 3.2 +

Riflette un pacchetto e le relative dipendenze dal repository di origine specificato per il repository di destinazione.

> [!NOTE]
> Per abilitare questo comando per le versioni di NuGet prima 3.2, passare a [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), selezionare la versione stabile più recente, scaricare `NuGet.ServerExtensions.dll` e `Nuget-Signed.exe` al disco locale e ridenominazione `Nuget-Signed.exe` a `nuget.exe`.

## <a name="usage"></a>Utilizzo

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

in cui `<packageID>` è il pacchetto per eseguire il mirroring, oppure `<configFilePath>` identifica il `packages.config` file che elenca i pacchetti per eseguire il mirroring.

Il `<listUrlTarget>` specifica il repository del codice sorgente, e `<publishUrlTarget>` consente di specificare il repository di destinazione.

Se il repository di destinazione si trova in `https://machine/repo` che esegue [NuGet. server](../hosting-packages/nuget-server.md), gli URL elenco ed effettuare il push verrà `https://machine/repo/nuget` e `https://machine/repo/api/v2/package`, rispettivamente.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| Chiave API | La chiave API per il repository di destinazione. Se non è presente, quello specificato nel file di configurazione viene usato (`%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| ? | Visualizza la Guida informazioni per il comando. |
| NoCache | Impedisce l'uso di pacchetti memorizzati nella cache NuGet. Visualizzare [gestione dei pacchetti globali e le cartelle cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NOOP | Registra quali possono essere eseguiti, ma non esegue le azioni; si presuppone che l'esito positivo per operazioni di push. |
| Versione preliminare | Include pacchetti versione non definitivo nell'operazione di mirroring. |
| Origine | Elenco di origini dei pacchetti per eseguire il mirroring. Se non sono specificate origini, quelli definiti nel file di configurazione (vedere ApiKey precedente) vengono utilizzati, se è stato specificato nessuno. verrà utilizzato in nuget.org. |
| Timeout | Specifica il timeout, espresso in secondi, per effettuare il push a un server. Il valore predefinito è 300 secondi (5 minuti). |
| Versione | La versione del pacchetto da installare. Se non specificato, la versione più recente è sottoposto a mirroring. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
