---
title: Note sulla versione di NuGet versione 2.8.6
description: Note sulla versione per NuGet versione 2.8.6, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776705"
---
# <a name="nuget-286-release-notes"></a>Note sulla versione di NuGet versione 2.8.6

Note sulla versione di [NuGet 2.8.5](../release-notes/nuget-2.8.5.md)  |  [Note sulla versione di NuGet 2.8.7](../release-notes/nuget-2.8.7.md)

NuGet versione 2.8.6 è stato rilasciato il 20 luglio 2015 come aggiornamento secondario di 2.8.5 VSIX con alcune correzioni e miglioramenti mirati per supportare i pacchetti che possono essere forniti con il supporto per il modello di sviluppo UWP di Windows 10.

Questa versione dell'estensione Gestione pacchetti NuGet fornisce il supporto solo per Visual Studio 2013.

In questa versione è stato aggiunto il supporto per la finestra di dialogo Gestione pacchetti NuGet per:

* Introduzione del moniker del Framework di destinazione UAP per supportare lo sviluppo di applicazioni Windows 10.
* Endpoint del protocollo NuGet versione 3
* Supporto per [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) attributo protocolVersion nelle origini del repository. Il valore predefinito è "2"
* Fallback al repository remoto se nella cache locale non è disponibile una versione del pacchetto necessaria