---
title: Come gestire la memorizzazione nella cache dei pacchetti in NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Come gestire le diverse cache per i pacchetti NuGet esistenti in un computer, usate durante l'installazione o il ripristino dei pacchetti.
keywords: Cache dei pacchetti NuGet, memorizzazione nella cache dei pacchetti, cache NuGet, gestione delle cache, cache NuGet locale, cache NuGet globale, comando locals NuGet, cancellazione di una cache
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 84bc34e02572a912fb86ce1a5cf54d8ff212ac6e
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2018
---
# <a name="managing-the-nuget-cache"></a>Gestione delle cache NuGet

NuGet gestisce varie cache locali per evitare il download di pacchetti già disponibili nel computer e per fornire il supporto offline. NuGet esegue automaticamente il fallback alla cache durante l'installazione o la reinstallazione dei pacchetti senza una connessione di rete.

Le posizioni delle cache possono essere recuperate tramite il comando [locals](../tools/cli-ref-locals.md):

```cli
nuget locals all -list
```

L'output tipico è simile al seguente:

```output
http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder
```

Se si verificano problemi di installazione dei pacchetti o si vuole essere certi di eseguire l'installazione dei pacchetti da una raccolta remota, usare l'opzione `locals -clear`:

```cli
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

Si noti che la gestione della cache è attualmente supportata solo dalla riga di comando di NuGet e non all'interno di Visual Studio o mediante la console di Gestione pacchetti. La gestione della cache 2. x non è inoltre supportata in NuGet 3.6 e versioni successive.

Durante l'uso di `nuget locals` possono verificarsi gli errori seguenti:

- **La cancellazione delle risorse locali non è riuscita. Non è possibile eliminare uno o più file.**
- **La directory non è vuota**

Questi errori indicano che non si dispone dell'autorizzazione per eliminare i file nella cache o che uno o più file nella cache sono in uso da un altro processo, che deve essere chiuso prima di poter rimuovere tali file.
