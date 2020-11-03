---
title: Gestire pacchetti NuGet tramite l'interfaccia della riga di comando di nuget.exe
description: Istruzioni per usare l'interfaccia della riga di comando di nuget.exe insieme a pacchetti NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237387"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>Gestire pacchetti tramite l'interfaccia della riga di comando nuget.exe

Lo strumento della riga di comando consente di aggiornare e ripristinare facilmente pacchetti NuGet in progetti e soluzioni. Questo strumento offre tutte le funzionalità di NuGet in Windows e anche la maggior parte delle funzionalità in Mac e Linux per l'esecuzione in Mono.

L'interfaccia della riga di comando di `nuget.exe` viene usata per il progetto .NET Framework e per i progetti non di tipo SDK, ad esempio un progetto non di tipo SDK destinato alle librerie .NET Standard. Se si usa un progetto non di tipo SDK, di cui è stata eseguita la migrazione a `PackageReference`, usare invece l'interfaccia della riga di comando di `dotnet`. L'interfaccia della riga di comando di `nuget.exe` richiede un file [packages.config](../reference/packages-config.md) per i riferimenti ai pacchetti.

> [!NOTE]
> Nella maggior parte degli scenari è consigliabile [eseguire la migrazione dei progetti non di tipo SDK](../consume-packages/migrate-packages-config-to-package-reference.md) che usano `packages.config` a PackageReference, per poter poi usare l'interfaccia della riga di comando di `dotnet` anziché l'interfaccia della riga di comando di `nuget.exe`. La migrazione non è attualmente disponibile per i progetti C++ e ASP.NET.

Questo articolo illustra l'utilizzo di base di alcuni dei comandi più comuni dell'interfaccia della riga di comando di `nuget.exe`. Per la maggior parte di questi comandi, lo strumento della riga di comando cerca un file di progetto nella directory corrente, a meno che non venga specificato un file di progetto nel comando. Per un elenco completo dei comandi e degli argomenti che è possibile usare, vedere [Informazioni di riferimento sull'interfaccia della riga di comando di nuget.exe](../reference/nuget-exe-cli-reference.md).

## <a name="prerequisites"></a>Prerequisiti

- Installare l'interfaccia della riga di comando `nuget.exe` scaricandola da [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), salvare il file `.exe` in una cartella appropriata e aggiungere tale cartella alla variabile di ambiente PATH.

## <a name="install-a-package"></a>Installare un pacchetto

Il comando [install](../reference/cli-reference/cli-ref-install.md) scarica e installa un pacchetto in un progetto (per impostazione predefinita nella cartella corrente) usando le origini pacchetto specificate. Installare i nuovi pacchetti nella cartella *packages* nella directory radice del progetto.

> [!IMPORTANT]
> Il comando `install` non modifica un file di progetto o *il file packages.config* . È pertanto simile a `restore` perché aggiunge soltanto pacchetti su disco, ma non modifica le dipendenze di un progetto. Per aggiungere una dipendenza, aggiungere un pacchetto tramite l'interfaccia utente di Gestione pacchetti o la console in Visual Studio oppure modificare il file *packages.config* , quindi eseguire `install` o `restore`.

1. Aprire una riga di comando e passare alla directory che contiene il file di progetto.

2. Usare il comando seguente per installare un pacchetto NuGet nella cartella *packages* .

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    Per installare il pacchetto `Newtonsoft.json` nella cartella *packages* , usare il comando seguente:

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

In alternativa, è possibile usare il comando seguente per installare un pacchetto NuGet tramite un file `packages.config` esistente nella cartella *packages* . In questo modo non si aggiunge il pacchetto alle dipendenze del progetto, ma si installa il pacchetto localmente.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>Installare una versione specifica di un pacchetto

Se la versione non viene specificata quando si usa il comando [install](../reference/cli-reference/cli-ref-install.md), NuGet installa la versione più recente del pacchetto. È anche possibile installare una versione specifica di un pacchetto Nuget:

```cli
nuget install <packageID | configFilePath> -Version <version>
```

Per aggiungere ad esempio la versione 12.0.1 del pacchetto `Newtonsoft.json`, usare questo comando:

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

Per altre informazioni sulle limitazioni e sul comportamento del comando `install`, vedere [Installare un pacchetto](#install-a-package).

## <a name="remove-a-package"></a>Rimuovere un pacchetto

Per eliminare uno o più pacchetti, eliminare i pacchetti che si vogliono rimuovere dalla cartella *packages* .

Se si vuole reinstallare i pacchetti, usare il comando `restore` o `install`.

## <a name="list-packages"></a>Elencare i pacchetti

È possibile visualizzare un elenco dei pacchetti da un'origine specificata usando il comando [list](../reference/cli-reference/cli-ref-list.md). Usare l'opzione `-Source` per limitare la ricerca.

```cli
nuget list -Source <source>
```

Elencare ad esempio i pacchetti nella cartella *packages* .

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

Se si usa un termine di ricerca, la ricerca includerà i nomi, i tag e le descrizioni dei pacchetti.

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>Aggiornare un singolo pacchetto

Se la versione del pacchetto non viene specificata, NuGet installa la versione del pacchetto più recente quando si usa il comando `install`.

## <a name="update-all-packages"></a>Aggiornare tutti i pacchetti

Usare il comando [update](../reference/cli-reference/cli-ref-update.md) per aggiornare tutti i pacchetti. Esegue l'aggiornamento di tutti i pacchetti in un progetto (usando `packages.config`) alle versioni disponibili più recenti. È consigliabile eseguire il comando `restore` prima di eseguire il comando `update`.

```cli
nuget update
```

## <a name="restore-packages"></a>Ripristinare pacchetti

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a>Ottenere la versione dell'interfaccia della riga di comando

Usare questo comando:

```cli
nuget help
```

La prima riga nell'output del comando help mostra la versione. Per evitare lo scorrimento, usare invece `nuget help | more`.