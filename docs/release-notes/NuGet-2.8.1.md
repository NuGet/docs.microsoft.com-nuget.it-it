---
title: Note sulla versione di NuGet 2.8.1
description: Note sulla versione per NuGet 2.8.1, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776766"
---
# <a name="nuget-281-release-notes"></a>Note sulla versione di NuGet 2.8.1

Note sulla versione di [NuGet 2,8](../release-notes/nuget-2.8.md)  |  [Note sulla versione di NuGet 2.8.2](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 è stato rilasciato il 2 aprile 2014.

## <a name="notable-features-in-the-release"></a>Funzionalità rilevanti della versione

### <a name="support-for-windows-phone-81-projects"></a>Supporto per progetti Windows Phone 8,1
Questa versione supporta ora i nuovi moniker del Framework di destinazione seguenti che possono essere usati per la destinazione Windows Phone progetti 8,1:

* WindowsPhone81/WP81 (per i progetti Windows Phone basati su Silverlight)
* WindowsPhoneApp81/WPA81 (per i progetti di app Windows Phone basati su WinRT)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Aggiornamento dell'estensione NuGet WebMatrix
Questa versione aggiorna il client NuGet trovato in WebMatrix a [NuGet. Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 e offre funzionalità IT come le trasformazioni di xdt. Ancora più importante, l'aggiornamento di 2.6.1 core consente al client WebMatrix di installare pacchetti NuGet che contengono versioni più recenti dello `.nuspec` schema, che include i pacchetti NuGet di ASP.NET.

Per ulteriori informazioni sull'aggiornamento dell'estensione WebMatrix, vedere le [Note sulla versione](../release-notes/nuget-2.6.1-for-WebMatrix.md)specifiche.

### <a name="bug-fixes"></a>Correzioni di bug
Oltre a queste funzionalità, questa versione di NuGet include altre correzioni di bug. Sono stati risolti 16 problemi totali nella versione. Per un elenco completo degli elementi di lavoro corretti in NuGet 2.8.1, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Reshipping con Visual Studio "14" CTP
In Visual Studio "14" CTP rilasciato il 3 giugno 2014, NuGet 2.8.1 viene fornito nella casella. Le funzionalità supportate rimangono invariate con altri VSIX 2.8.1, ad esempio quello per Visual Studio 2013.
