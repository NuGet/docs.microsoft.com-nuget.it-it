---
title: Risoluzione dei problemi relativi ai pacchetti installati
description: Come trovare l'origine del pacchetto usata per i singoli pacchetti
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387571"
---
# <a name="troubleshooting-installed-packages"></a>Risoluzione dei problemi relativi ai pacchetti installati

In alcuni casi può essere necessario convalidare l'origine da cui è stato installato un pacchetto specifico. Ecco alcuni modi per verificare.

> [!Note]
> Alcune origini di pacchetti supportano un concetto noto come origini upstream. Ad esempio, [Azure Artifacts origini upstream](/azure/devops/artifacts/concepts/upstream-sources). I client NuGet non sanno se un pacchetto proveniva da un'origine upstream. Pertanto, qualsiasi registrazione dell'origine del pacchetto ese elencata l'origine configurata, non l'origine upstream.

## <a name="nupkgmetadata-file-in-global-packages-folder"></a>`.nupkg.metadata` file nella cartella dei pacchetti globali

Quando un pacchetto viene estratto nella *cartella global-packages,* viene scritto `.nupkg.metadata` un file. A partire da NuGet 5.9.0, NuGet aggiungerà l'origine del pacchetto. Vedere di seguito per eseguire il mapping delle versioni di NuGet Visual Studio o .NET SDK. Ad esempio:

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> Se la cartella *global-packages* contiene pacchetti estratti prima dell'aggiornamento a una versione più recente degli strumenti con NuGet 5.9.0, il file sarà la versione 1 e non conterrà l'origine del `.nupkg.metadata` pacchetto. È possibile [cancellare la cartella *global-packages* per assicurarsi](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) che tutti i pacchetti contengano l'origine del pacchetto.

> [!Tip]
> NuGet scrive il `.nupkg.metadata` file solo nella cartella *global-packages.* I progetti `packages.config` che usano usano una cartella dei pacchetti della soluzione, che non crea un `.nupkg.metadata` file.

## <a name="installed-package-log-message"></a>Messaggio di log del pacchetto installato

A partire da NuGet 5.9.0, NuGet restituisce l'origine del pacchetto nel messaggio di ripristino che informa che è stato installato un pacchetto. Ad esempio:

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> Questo messaggio viene restituito al livello di dettaglio normale/informativo. Visual Studio e l'interfaccia della riga di comando hanno un livello di dettaglio minimo, quindi questo `dotnet` messaggio non sarà visibile per impostazione predefinita. Per `msbuild` impostazione predefinita, gli strumenti e dell'interfaccia della riga di comando hanno un livello di dettaglio normale, quindi questo messaggio `nuget` sarà visibile per impostazione predefinita.

## <a name="http-log-message"></a>Messaggio di log HTTP

Quando un pacchetto non è disponibile in locale, nella cartella *global-packages,* in una cartella di fallback o in un'origine file locale, NuGet lo scarica da qualsiasi origine pacchetto configurata tramite HTTP. Le richieste e le risposte HTTP vengono registrate al livello di dettaglio normale e dovrebbero essere presenti solo una singola richiesta e risposta per ogni versione del pacchetto. Ad esempio:

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

Se i file sono stati scaricati di recente, potrebbero essere recuperati dalla *http-cache di NuGet*

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

Il formato dell'URL può essere diverso per le diverse implementazioni del server HTTP NuGet e per l'implementazione del protocollo HTTP NuGet V2 o V3.

Se sono definite più origini HTTP, verranno visualizzati più richieste al file di ogni `nuget.config` `index.json` pacchetto, una per ogni origine. Tuttavia, per ogni versione del pacchetto sarà disponibile un solo `nupkg` download.

## <a name="package-signature-log-message"></a>Messaggio del log della firma del pacchetto

Se il pacchetto scaricato è firmato, NuGet convalida la firma e registra il messaggio seguente con un livello di dettaglio dettagliato:

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

Questo messaggio verrà segnalato se il pacchetto è stato scaricato da un'origine del pacchetto HTTP o copiato da un'origine del pacchetto locale. Non verrà restituito se il pacchetto è già disponibile nella *cartella global-packages* o in una cartella di fallback.

> [!Important]
> A causa [della rimozione dell'attendibilità di VeriSign CA](https://github.com/dotnet/announcements/issues/180) NuGet, la verifica dei pacchetti firmati è stata disabilitata in determinate piattaforme, in determinate versioni di NuGet e .NET SDK. Di conseguenza, gli stessi pacchetti possono avere log o tali log potrebbero non essere presenti, a seconda della piattaforma in cui si esegue il ripristino e della versione di .NET o NuGet in `PackageSignatureVerificationLog` uso.

## <a name="nuget-version-map"></a>Mappa delle versioni di NuGet

Le versioni seguenti di NuGet hanno modifiche importanti relative alla registrazione dell'origine del pacchetto:

|Versione di NuGet|Versione di Visual Studio|Versione di .NET SDK|
|---|---|---|
|NuGet 5.9.0|Visual Studio 2019 16.9.0|.NET 5 SDK 5.0.200|
