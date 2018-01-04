---
title: Creazione di pacchetti NuGet nativi | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 7a70d748-efe2-4f8f-a3fd-67ddb0f6214e
description: "Informazioni dettagliate sulla creazione di pacchetti NuGet nativi che contengono codice C++ anziché codice gestito, da usare in progetti C++."
keywords: Pacchetti NuGet nativi, pacchetti NuGet C++, pacchetti di codice nativo, progetti C++ di destinazione
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fa5baaa6ecbad0f5f6dd85d657679ffbbbc8a47a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="creating-native-packages"></a>Creazione di pacchetti nativi

Un pacchetto nativo contiene codice C++ nativo invece di codice gestito, in modo che possa essere usato all'interno di progetti C++. (Vedere [Pacchetti C++ nativi](../consume-packages/finding-and-choosing-packages.md#native-cpp-packages) nella sezione Utilizzare i pacchetti.)

Per essere utilizzabile in un progetto C++, un pacchetto deve essere destinato al framework `native`. Al momento, a questo framework non è assegnato alcun numero di versione perché NuGet considera uguali tutti i progetti C++.

> [!Note]
> Assicurarsi di includere *native* nella sezione `<tags>` del file `.nuspec` per aiutare gli altri sviluppatori a trovare il pacchetto eseguendo una ricerca in base a tale tag.

I pacchetti NuGet nativi con destinazione `native` forniscono quindi i file nelle cartelle `\build`, `\content` e `\tools`. In questo caso la cartella `\lib` non viene usata (NuGet non può aggiungere direttamente riferimenti a un progetto C++). Un pacchetto può anche includere file di destinazioni e proprietà in `\build` e tali file verranno importati automaticamente da NuGet nei progetti che utilizzano il pacchetto. Questi file devono avere lo stesso nome dell'ID di pacchetto con le estensioni `.targets` e/o `.props`. Ad esempio, il pacchetto [cpprestsdk](https://nuget.org/packages/cpprestsdk/) include un file `cpprestsdk.targets` nella relativa cartella `\build`.

La cartella `\build` può essere usata per tutti i pacchetti NuGet e non solo per i pacchetti nativi. La cartella `\build` rispetta i framework di destinazione così come le cartelle `\content`, `\lib` e `\tools`. Questo significa che è possibile creare una cartella `\build\net40` e una cartella `\build\net45` e NuGet importerà i file di proprietà e destinazioni appropriati nel progetto. Non occorre usare script di PowerShell per importare le destinazioni MSBuild.
