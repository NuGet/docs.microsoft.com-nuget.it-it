---
title: Note sulla versione di NuGet versione 2.8.6
description: Note sulla versione per NuGet versione 2.8.6, tra cui noti problemi, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546491"
---
# <a name="nuget-286-release-notes"></a>Note sulla versione di NuGet versione 2.8.6

[Note sulla versione di NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [note sulla versione di NuGet 2.8.7](../release-notes/nuget-2.8.7.md)

NuGet versione 2.8.6 è stato rilasciato il 20 luglio 2015 come aggiornamento secondario al nostro 2.8.5 destinati VSIX con alcune correzioni e miglioramenti per supportare i pacchetti che possono essere distribuiti con il supporto per il modello di sviluppo di UWP di Windows 10.

Questa versione dell'estensione Gestione pacchetti NuGet fornisce supporto solo per Visual Studio 2013.

In questa versione, la finestra di dialogo Gestione pacchetti NuGet ha aggiunto il supporto per:

* È stato introdotto il moniker del Framework di destinazione UAP per supportare lo sviluppo di applicazioni di Windows 10.
* Endpoint versione 3 del protocollo NuGet
* Supporto per [NuGet. config](../consume-packages/configuring-nuget-behavior.md) attributo delle protocolVersion sulle origini di repository. Valore predefinito è "2"
* Eseguire il fallback al repository remoto se una versione del pacchetto richiesto non è disponibile nella cache locale