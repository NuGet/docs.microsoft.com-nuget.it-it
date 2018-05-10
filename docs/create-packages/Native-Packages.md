---
title: Creazione di pacchetti NuGet nativi
description: Informazioni dettagliate sulla creazione di pacchetti NuGet nativi che contengono codice C++ anziché codice gestito, da usare in progetti C++.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 1fa8bf23a3fbed686b99f1c783b0ce55b373e548
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="creating-native-packages"></a>Creazione di pacchetti nativi

Un pacchetto nativo contiene codice C++ nativo invece di codice gestito, in modo che possa essere usato all'interno di progetti C++. (Vedere [Pacchetti C++ nativi](../consume-packages/finding-and-choosing-packages.md#native-c-packages) nella sezione Utilizzare i pacchetti.)

Per essere utilizzabile in un progetto C++, un pacchetto deve essere destinato al framework `native`. Al momento, a questo framework non è assegnato alcun numero di versione perché NuGet considera uguali tutti i progetti C++.

> [!Note]
> Assicurarsi di includere *native* nella sezione `<tags>` del file `.nuspec` per aiutare gli altri sviluppatori a trovare il pacchetto eseguendo una ricerca in base a tale tag.

I pacchetti NuGet nativi con destinazione `native` forniscono quindi i file nelle cartelle `\build`, `\content` e `\tools`. In questo caso la cartella `\lib` non viene usata (NuGet non può aggiungere direttamente riferimenti a un progetto C++). Un pacchetto può anche includere file di destinazioni e proprietà in `\build` e tali file verranno importati automaticamente da NuGet nei progetti che utilizzano il pacchetto. Questi file devono avere lo stesso nome dell'ID di pacchetto con le estensioni `.targets` e/o `.props`. Ad esempio, il pacchetto [cpprestsdk](https://nuget.org/packages/cpprestsdk/) include un file `cpprestsdk.targets` nella relativa cartella `\build`.

La cartella `\build` può essere usata per tutti i pacchetti NuGet e non solo per i pacchetti nativi. La cartella `\build` rispetta i framework di destinazione così come le cartelle `\content`, `\lib` e `\tools`. Questo significa che è possibile creare una cartella `\build\net40` e una cartella `\build\net45` e NuGet importerà i file di proprietà e destinazioni appropriati nel progetto. Non occorre usare script di PowerShell per importare le destinazioni MSBuild.
