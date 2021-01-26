---
title: Note sulla versione di NuGet 2.2.1
description: Note sulla versione per NuGet 2.2.1, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776813"
---
# <a name="nuget-221-release-notes"></a>Note sulla versione di NuGet 2.2.1

Note sulla versione di [NuGet 2,2](../release-notes/nuget-2.2.md)  |  [Note sulla versione di NuGet 2,5](../release-notes/nuget-2.5.md)

NuGet 2.2.1 è stato rilasciato il 15 febbraio 2013.  Il numero di versione dell'estensione di Visual Studio è 2.2.40116.9051.

## <a name="localization-refresh"></a>Aggiornamento della localizzazione
Quando NuGet è stato fornito come parte di Visual Studio 2012, è stato completamente localizzato in inglese + 13 altre lingue.  Da allora, NuGet 2,1 e 2,2 sono stati spediti ma la localizzazione non è stata aggiornata.  La versione di NuGet 2.2.1 Aggiorna la localizzazione.

L'interfaccia utente e la console di PowerShell di NuGet sono localizzate nelle seguenti lingue:

1. Cinese (semplificato)
1. Cinese (tradizionale)
1. Ceco
1. Inglese
1. Francese
1. Tedesco
1. Italiano
1. Giapponese
1. Coreano
1. Polacco
1. Portoghese (Brasile)
1. Russo
1. Spagnolo
1. Turco

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>I modelli di Visual Studio supportano più repository di pacchetti preinstallati
Se si producono modelli di Visual Studio, è possibile usare NuGet per [preinstallare i pacchetti](../visual-studio-extensibility/visual-studio-templates.md) come parte del modello.  Fino ad ora, questa funzionalità aveva una limitazione che tutti i pacchetti dovevano provenire dalla stessa origine.  Con NuGet 2.2.1, tuttavia, i pacchetti possono essere installati da più repository, all'interno del modello, in un progetto VSIX o in una cartella su disco definita nel registro di sistema.

Lo scenario principale di questa funzionalità è il modello di progetto ASP.NET personalizzato.  I modelli ASP.NET predefiniti usano i pacchetti preinstallati, estraendo i pacchetti dal disco locale.  È ora possibile creare un modello di progetto ASP.NET personalizzato che usa i pacchetti esistenti installati da ASP.NET ma aggiungere pacchetti NuGet aggiuntivi al modello.

## <a name="bug-fixes"></a>Correzioni di bug
NuGet 2.2.1 include alcune correzioni di bug mirate. Per un elenco degli elementi di lavoro corretti in NuGet 2.2.1, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Problemi noti

Se si estendono i modelli di progetto ASP.NET, tutti i repository di pacchetti preinstallati devono usare lo stesso valore per l' `isPreunzipped` attributo.
