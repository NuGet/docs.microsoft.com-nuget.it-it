---
title: Creazione di pacchetti NuGet nativi
description: Informazioni dettagliate sulla creazione di pacchetti NuGet nativi che contengono codice C++ anziché codice gestito, da usare in progetti C++.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 086084bdfae5eace0b0a6aab17140a1fa48ae977
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817060"
---
# <a name="creating-native-packages"></a>Creazione di pacchetti nativi

Un pacchetto nativo contiene codice C++ nativo invece di codice gestito, in modo che possa essere usato all'interno di progetti C++. (Vedere [Pacchetti C++ nativi](../consume-packages/finding-and-choosing-packages.md#native-c-packages) nella sezione Utilizzare i pacchetti.)

Per essere utilizzabile in un progetto C++, un pacchetto deve essere destinato al framework `native`. Al momento, a questo framework non è assegnato alcun numero di versione perché NuGet considera uguali tutti i progetti C++.

> [!Note]
> Assicurarsi di includere *native* nella sezione `<tags>` del file `.nuspec` per aiutare gli altri sviluppatori a trovare il pacchetto eseguendo una ricerca in base a tale tag.

I pacchetti NuGet nativi con destinazione `native` forniscono quindi i file nelle cartelle `\build`, `\content` e `\tools`. In questo caso la cartella `\lib` non viene usata (NuGet non può aggiungere direttamente riferimenti a un progetto C++). Un pacchetto può anche includere file di destinazioni e proprietà in `\build` e tali file verranno importati automaticamente da NuGet nei progetti che utilizzano il pacchetto. Questi file devono avere lo stesso nome dell'ID di pacchetto con le estensioni `.targets` e/o `.props`. Ad esempio, il pacchetto [cpprestsdk](https://nuget.org/packages/cpprestsdk/) include un file `cpprestsdk.targets` nella relativa cartella `\build`.

La cartella `\build` può essere usata per tutti i pacchetti NuGet e non solo per i pacchetti nativi. La cartella `\build` rispetta i framework di destinazione così come le cartelle `\content`, `\lib` e `\tools`. Questo significa che è possibile creare una cartella `\build\net40` e una cartella `\build\net45` e NuGet importerà i file di proprietà e destinazioni appropriati nel progetto. Non occorre usare script di PowerShell per importare le destinazioni MSBuild.
