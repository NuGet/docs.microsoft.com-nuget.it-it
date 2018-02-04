---
title: Note sulla versione di NuGet 2.8.6 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 920c551c-18a7-40f4-a32b-ce84de6ea766
description: "Note sulla versione per l'inclusione di NuGet 2.8.6 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet 2.8.6 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4dfd0a76967280cc6a16b37fe2b2a3362231fce5
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-286-release-notes"></a>Note sulla versione di NuGet 2.8.6

[Note sulla versione di NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [note sulla versione di NuGet 2.8.7](../release-notes/nuget-2.8.7.md)

È stato rilasciato NuGet 2.8.6 20 luglio 2015 come un aggiornamento secondario per il nostro 2.8.5 destinazione VSIX, con alcune correzioni e miglioramenti per supportare i pacchetti che possono essere inviati con il supporto per il modello di sviluppo UWP Windows 10.

Questa versione dell'estensione di gestione per il pacchetto NuGet fornisce il supporto solo per Visual Studio 2013.

In questa versione, la finestra di dialogo Gestione pacchetti NuGet ha aggiunto il supporto per:

* È stato introdotto il moniker del Framework di destinazione UAP per supportare lo sviluppo di applicazioni di Windows 10.
* Endpoint versione 3 del protocollo NuGet
* Supporto per [NuGet](../consume-packages/configuring-nuget-behavior.md) attributo protocolVersion su origini dei repository. Il valore predefinito è "2"
* Eseguire il fallback al repository remoto se una versione del pacchetto richiesto non è disponibile nella cache locale