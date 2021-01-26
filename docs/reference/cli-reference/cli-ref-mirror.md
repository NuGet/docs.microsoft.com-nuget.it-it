---
title: Comando mirror CLI NuGet
description: Riferimento per il comando nuget.exe mirror
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6ecd5c11383f78fdaeb01090366a8ffe294b4f8b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779176"
---
# <a name="mirror-command-nuget-cli"></a>comando mirror (interfaccia della riga di comando di NuGet)

**Si applica a:** versioni supportate per la pubblicazione di pacchetti &bullet; **:** deprecate in 3.2 +

Rispecchia un pacchetto e le relative dipendenze dai repository di origine specificati al repository di destinazione.

> [!NOTE]
> NuGet.ServerExtensions.dll e NuGet-Signed.exe che in precedenza supportano questo comando in NuGet 2. x (rinominando NuGet-Signed.exe in nuget.exe) non sono più disponibili per il download. Per usare un comando simile a questo, provare [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).

## <a name="usage"></a>Utilizzo

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

dove `<packageID>` è il pacchetto di cui eseguire il mirroring o `<configFilePath>` identifica il `packages.config` file in cui sono elencati i pacchetti di cui eseguire il mirroring.

`<listUrlTarget>`Specifica il repository di origine e `<publishUrlTarget>` specifica il repository di destinazione.

Se il repository di destinazione è in `https://machine/repo` esecuzione [NuGet. Server](../../hosting-packages/nuget-server.md), l'elenco e gli URL push saranno `https://machine/repo/nuget` rispettivamente e `https://machine/repo/api/v2/package` .

## <a name="options"></a>Opzioni

- **`-ApiKey`**

  Chiave API per il repository di destinazione. Se non è presente, viene usato quello specificato nel file di configurazione ( `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).

- **`-Help`**

  Visualizza le informazioni della Guida per il comando.

- **`-NoCache`**

  Impedisce a NuGet di usare pacchetti memorizzati nella cache. Vedere [gestione dei pacchetti globali e delle cartelle della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-Noop`**

  Registra il risultato dell'operazione, ma non esegue le azioni; presuppone l'esito positivo delle operazioni push.

- **`-PreRelease`**

  Include pacchetti di versioni non definitive nell'operazione di mirroring.

- **`-Source`**

  Elenco di origini dei pacchetti di cui eseguire il mirroring. Se non viene specificata alcuna origine, vengono usati quelli definiti nel file di configurazione (vedere ApiKey), per impostazione predefinita nuget.org se non ne viene specificato alcuno.

- **`-Timeout`**

  Specifica il timeout, in secondi, per il push in un server.  Il valore predefinito è 300 secondi (5 minuti).

- **`-Version`**

  Versione del pacchetto da installare. Se non è specificato, viene riflessa la versione più recente.

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
