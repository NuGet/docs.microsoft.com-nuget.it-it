---
title: Configurazione dei feed NuGet locali
description: Come creare un feed locale per i pacchetti NuGet usando le cartelle nella rete locale
author: JonDouglas
ms.author: jodou
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 1eb194c9ddaee05281749c7a0420cbaf77044fe3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774035"
---
# <a name="local-feeds"></a>Feed locali

I feed locali per i pacchetti NuGet sono semplicemente strutture di cartelle gerarchiche nella rete locale (o nel computer personale) in cui vengono posizionati i pacchetti. Questi feed possono quindi essere usati come origini di pacchetto con tutte le altre operazioni NuGet tramite l'interfaccia della riga di comando, l'interfaccia utente di Gestione pacchetti e la console di Gestione pacchetti.

Per abilitare l'origine, aggiungere il nome del percorso (ad esempio `\\myserver\packages`) all'elenco delle origini tramite l'[interfaccia utente di Gestione pacchetti](../consume-packages/install-use-packages-visual-studio.md#package-sources) o il comando [`nuget sources`](../reference/cli-reference/cli-ref-sources.md).

> [!Note]
> Le strutture di cartelle gerarchiche sono supportate in NuGet 3.3+. Le versioni precedenti di NuGet usano solo una singola cartella contenente i pacchetti, con prestazioni molto inferiori rispetto alla struttura gerarchica.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Inizializzazione e gestione delle cartelle gerarchiche

L'albero delle cartelle gerarchiche con versioni ha la struttura generale seguente:

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      └─<other files>
```

NuGet crea automaticamente questa struttura quando si usa il [`nuget add`](../reference/cli-reference/cli-ref-add.md) comando per copiare un pacchetto nel feed:

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

Il comando `nuget add` funziona con un pacchetto alla volta e ciò può risultare poco pratico per la configurazione di un feed con più pacchetti.

In questi casi, usare il [`nuget init`](../reference/cli-reference/cli-ref-init.md) comando per copiare tutti i pacchetti in una cartella nel feed come se fossero stati eseguiti `nuget add` singolarmente. Ad esempio, il comando seguente copia tutti i pacchetti da `c:\packages` a un albero gerarchico in `\\myserver\packages`:

```cli
nuget init c:\packages \\myserver\packages
```

Come con il comando `add`, `init` crea una cartella per ogni identificatore di pacchetto, ognuna delle quali contiene una cartella con numero di versione, all'interno della quale si trova il pacchetto appropriato.
