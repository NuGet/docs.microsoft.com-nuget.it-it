---
title: Note sulla versione 2.2.1 NuGet
description: Note sulla versione per l'inclusione di NuGet 2.2.1 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fddeb4e8c9fb2d85ba1876360862461e8ef025af
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819293"
---
# <a name="nuget-221-release-notes"></a>Note sulla versione 2.2.1 NuGet

[Note sulla versione di NuGet 2.2](../release-notes/nuget-2.2.md) | [note sulla versione di NuGet 2.5](../release-notes/nuget-2.5.md)

È stata rilasciata NuGet 2.2.1 15 febbraio 2013.  Il numero di versione di estensione di Visual Studio è 2.2.40116.9051.

## <a name="localization-refresh"></a>Aggiornamento di localizzazione
NuGet fornito come parte di Visual Studio 2012, è stato completamente localizzato in inglese + 13 altri linguaggi.  Da allora NuGet 2.1 e 2.2 spediti ma la localizzazione non è stata aggiornata.  La versione NuGet 2.2.1 aggiorna la localizzazione.

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

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Modelli di Visual Studio supportano più repository di pacchetti preinstallati
Se si producono modelli di Visual Studio, è possibile utilizzare NuGet per [preinstallare pacchetti](../visual-studio-extensibility/visual-studio-templates.md) come parte del modello.  Fino ad ora, questa funzionalità era una limitazione che tutti i pacchetti necessari per provenire dalla stessa origine.  Con NuGet 2.2.1, tuttavia, è possibile disporre di pacchetti installati in più repository (all'interno del modello, un progetto VSIX o una cartella sul disco definito nel Registro di sistema).

Lo scenario principale per questa funzionalità è modelli di progetto ASP.NET personalizzati.  I modelli ASP.NET incorporati utilizzano pacchetti preinstallati, estrarre i pacchetti da disco locale.  È ora possibile creare un modello di progetto ASP.NET personalizzato che utilizza i pacchetti esistenti installati da ASP.NET, ma aggiungere pacchetti NuGet aggiuntivi nel modello.

## <a name="bug-fixes"></a>Correzioni di bug
NuGet 2.2.1 include alcune correzioni di bug di destinazione. Per un elenco di lavoro gli elementi corretti in NuGet 2.2.1,. visualizzazione di [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Problemi noti

Se si estende i modelli di progetto ASP.NET, tutti i repository di pacchetti preinstallati devono utilizzare lo stesso valore per il `isPreunzipped` attributo.
