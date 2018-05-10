---
title: Configurazione dei feed NuGet locali
description: Come creare un feed locale per i pacchetti NuGet usando le cartelle nella rete locale
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 4710a6fd13bdd89492e2a7246d1e15f6c01a5368
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="local-feeds"></a>Feed locali

I feed locali per i pacchetti NuGet sono semplicemente strutture di cartelle gerarchiche nella rete locale (o nel computer personale) in cui vengono posizionati i pacchetti. Questi feed possono quindi essere usati come origini di pacchetto con tutte le altre operazioni NuGet tramite l'interfaccia della riga di comando, l'interfaccia utente di Gestione pacchetti e la console di Gestione pacchetti.

Per abilitare l'origine, aggiungere il nome del percorso (ad esempio `\\myserver\packages`) all'elenco delle origini tramite l'[interfaccia utente di Gestione pacchetti](../tools/package-manager-ui.md#package-sources) o il comando [`nuget sources`](../tools/cli-ref-sources.md).

> [!Note]
> Le strutture di cartelle gerarchiche sono supportate in NuGet 3.3+. Le versioni precedenti di NuGet usano solo una singola cartella contenente i pacchetti, con prestazioni molto inferiori rispetto alla struttura gerarchica.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Inizializzazione e gestione delle cartelle gerarchiche

L'albero delle cartelle gerarchiche con versioni ha la struttura generale seguente:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

NuGet crea questa struttura automaticamente quando si usa il comando [`nuget add`](../tools/cli-ref-add.md) per copiare un pacchetto nel feed:

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

Il comando `nuget add` funziona con un pacchetto alla volta e ciò può risultare poco pratico per la configurazione di un feed con più pacchetti.

In questi casi, usare il comando [`nuget init`](../tools/cli-ref-init.md) per copiare tutti i pacchetti in una cartella nel feed, come se si eseguisse `nuget add` su ognuno singolarmente. Ad esempio, il comando seguente copia tutti i pacchetti da `c:\packages` a un albero gerarchico in `\\myserver\packages`:

```cli
nuget init c:\packages \\myserver\packages
```

Come con il comando `add`, `init` crea una cartella per ogni identificatore di pacchetto, ognuna delle quali contiene una cartella con numero di versione, all'interno della quale si trova il pacchetto appropriato.
