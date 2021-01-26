---
title: Note sulla versione di NuGet 2,9-RC
description: Note sulla versione per NuGet 2,9 RC, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b9d32f09fae7e12f81cf92b5b6e6b36c71d55f26
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780318"
---
# <a name="nuget-29-rc-release-notes"></a>Note sulla versione di NuGet 2,9-RC

Note sulla versione di [NuGet 2.8.7](../release-notes/nuget-2.8.7.md)  |  [Note sulla versione di NuGet 3,0 Preview](../release-notes/nuget-3.0-preview.md)

NuGet 2,9 è stato rilasciato il 10 settembre 2015 come aggiornamento di 2.8.7 VSIX per Visual Studio 2012 e 2013.

### <a name="updates-in-this-release"></a>Aggiornamenti in questa versione

* L'elaborazione dei pacchetti verrà ignorata se il `.nuspec` documento contenuto è in formato non corretto- [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Correzione della gestione multipartwebrequest di \r\n per scenari UNIX/Linux- [776](https://github.com/NuGet/Home/issues/776)
* Correzione dell'integrazione con gli eventi di compilazione in Visual Studio 2013 Community Edition- [1180](https://github.com/NuGet/Home/issues/1180)


L'elenco completo delle correzioni in questa versione è disponibile in GitHub nell' [attività cardine 2.8.8](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
