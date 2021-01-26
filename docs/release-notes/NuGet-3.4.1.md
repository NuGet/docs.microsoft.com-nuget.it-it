---
title: Note sulla versione di NuGet 3.4.1
description: Note sulla versione per NuGet 3.4.1, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1e234becd2c92ae64fa0f1ac95b358e9a2fb3207
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776485"
---
# <a name="nuget-341-release-notes"></a>Note sulla versione di NuGet 3.4.1

Note sulla versione di [NuGet 3,4](../release-notes/nuget-3.4.md)  |  [Note sulla versione di NuGet 3.4.2](../release-notes/nuget-3.4.2.md)

NuGet 3.4.1 è stato rilasciato il 30 marzo 2016 allo stesso tempo della versione Visual Studio 2015 Update 2 e Visual Studio 15 Preview per risolvere diversi problemi identificati nella versione 3,4.

## <a name="updates-and-improvements"></a>Aggiornamenti e miglioramenti

* Correzione di un problema che impediva l'esplorazione dei pacchetti dall'interfaccia utente di Visual Studio con un'installazione minima di Visual Studio
* Correzione di un problema relativo all'individuazione di Visual Studio `lucene.net.dll`
* Tutte le origini non devono essere l'origine del repository predefinita dopo l'installazione o l'aggiornamento di un'estensione NuGet.  È possibile acconsentire esplicitamente a questa funzionalità dalle impostazioni di configurazione.

Continuiamo a tenere traccia dei problemi nell'elenco dei problemi di GitHub disponibili all'indirizzo: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)