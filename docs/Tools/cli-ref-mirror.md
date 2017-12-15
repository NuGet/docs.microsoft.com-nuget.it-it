---
title: Comando mirror NuGet CLI | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 190d7010-172e-44b8-8a32-94a2a63be4f3
description: Riferimento per il comando di nuget.exe mirror
keywords: riferimento mirror NuGet, comando mirror
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67daa1aa278b42b7974c562ba4097a525e7bb105
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="mirror-command-nuget-cli"></a>comando mirror (NuGet CLI)

**Si applica a:** la pubblicazione del pacchetto &bullet; **le versioni supportate:** deprecata in 3.2 +

Riflette un pacchetto e le relative dipendenze dal repository di origine specificato per il repository di destinazione.

> [!NOTE]
> Per abilitare questo comando per le versioni di NuGet prima 3.2, passare a [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), selezionare la versione stabile più recente, scaricare `NuGet.ServerExtensions.dll` e `Nuget-Signed.exe` al disco locale e ridenominazione `Nuget-Signed.exe` per `nuget.exe`.

## <a name="usage"></a>Utilizzo

```
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

dove `<packageID>` è il pacchetto per eseguire il mirroring, o `<configFilePath>` identifica il `packages.config` file che elenca i pacchetti per eseguire il mirroring.

Il `<listUrlTarget>` specifica il repository di origine e `<publishUrlTarget>` specifica del repository di destinazione.

Se il repository di destinazione si trova in `https://machine/repo` che esegue [NuGet.Server](../hosting-packages/NuGet-Server.md), gli URL di elenco e push sarà `https://machine/repo/nuget` e `https://machine/repo/api/v2/package`, rispettivamente.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| apiKey | La chiave API per il repository di destinazione. Se non è presente, quella specificata nella *%AppData%\NuGet\NuGet.Config* viene utilizzato. |
| ? | Visualizza la Guida informazioni per il comando. |
| NoCache | Impedisce l'utilizzo di pacchetti dalla cache locale NuGet. |
| NOOP | Registra quali possono essere eseguite, ma non esegue le azioni; si presuppone che l'esito positivo per le operazioni di push. |
| Versione provvisoria | Include i pacchetti della versione provvisoria nell'operazione di mirroring. |
| Origine | Un elenco delle origini pacchetto per eseguire il mirroring. Se non vengono specificata alcuna origine, quelli definiti in *%AppData%\NuGet\NuGet.Config* vengono utilizzati, l'impostazione nuget.org se non è specificato. |
| Timeout | Specifica il timeout in secondi, per l'inserimento di un server. Il valore predefinito è 300 secondi (5 minuti). |
| Versione | La versione del pacchetto da installare. Se non specificato, la versione più recente è il mirroring. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
