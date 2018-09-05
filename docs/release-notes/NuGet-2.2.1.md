---
title: Note sulla versione di NuGet 2.2.1
description: Note sulla versione per NuGet 2.2.1 inclusi noti problemi, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550698"
---
# <a name="nuget-221-release-notes"></a>Note sulla versione di NuGet 2.2.1

[Note sulla versione di NuGet 2.2](../release-notes/nuget-2.2.md) | [note sulla versione di NuGet 2.5](../release-notes/nuget-2.5.md)

NuGet 2.2.1 è stato rilasciato il 15 febbraio 2013.  Il numero di versione di estensione di Visual Studio è 2.2.40116.9051.

## <a name="localization-refresh"></a>Aggiornamento localizzazione
Quando NuGet fornito come parte di Visual Studio 2012, si è stato completamente localizzato nelle inglese + 13 altri linguaggi.  Da allora, sono spedite NuGet 2.1 e 2.2, ma la localizzazione non era stata aggiornata.  La versione per NuGet 2.2.1 aggiorna la localizzazione.

Interfaccia utente e la Console di PowerShell di NuGet sono localizzati nelle lingue seguenti:

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

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Modelli di Visual Studio supportano più i repository dei pacchetti preinstallati
Se si producono modelli di Visual Studio, è possibile usare NuGet per [preinstallare pacchetti](../visual-studio-extensibility/visual-studio-templates.md) come parte del modello.  Fino ad ora, questa funzionalità era una limitazione che tutti i pacchetti necessari per provengono dalla stessa origine.  Con NuGet 2.2.1 però, è possibile avere i pacchetti installati da più repository (all'interno del modello, un progetto VSIX o una cartella sul disco definito nel Registro di sistema).

Lo scenario principale per questa funzionalità è i modelli di progetto personalizzati di ASP.NET.  I modelli predefiniti di ASP.NET usano pacchetti preinstallati, estraggano pacchetti dal disco locale.  È ora possibile creare un modello di progetto ASP.NET personalizzato che usa i pacchetti esistenti installati da ASP.NET ma aggiungere pacchetti NuGet aggiuntivi al modello.

## <a name="bug-fixes"></a>Correzioni di bug
NuGet 2.2.1 include alcune correzioni di bug di destinazione. Per un elenco di lavoro elementi di risolti in NuGet 2.2.1, vista la [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Problemi noti

Se si intende estendere i modelli di progetto ASP.NET, tutti i repository dei pacchetti preinstallati devono usare lo stesso valore per il `isPreunzipped` attributo.
