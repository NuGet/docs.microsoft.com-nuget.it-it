---
title: Note sulla versione di NuGet 2.8.1
description: Note sulla versione per NuGet 2.8.1, tra cui noti problemi, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545239"
---
# <a name="nuget-281-release-notes"></a>Note sulla versione di NuGet 2.8.1

[Note sulla versione di NuGet 2.8](../release-notes/nuget-2.8.md) | [note sulla versione di NuGet 2.8.2](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 è stato rilasciato dal 2 aprile 2014.

## <a name="notable-features-in-the-release"></a>Funzionalità di rilievo nella versione

### <a name="support-for-windows-phone-81-projects"></a>Supporto per i progetti di Windows Phone 8.1
Questa versione supporta ora il seguente nuovo target framework moniker che può essere utilizzato per i progetti di destinazione Windows Phone 8.1:

* WindowsPhone81 / WP81 (per i progetti Windows Phone basate su Silverlight)
* WindowsPhoneApp81 / WPA81 (per i progetti di App di Windows Phone basate su WinRT)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Aggiornamento dell'estensione di WebMatrix NuGet
Questa versione aggiorna il client di NuGet in WebMatrix per trovare [togliere](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 e offre con include, ad esempio le trasformazioni XDT. Ancora più importante, la versione 2.6.1 update core consente al client di WebMatrix installare i pacchetti NuGet che contengono le versioni più recenti del `.nuspec` schema, che include i pacchetti NuGet ASP.NET.

Per altre informazioni sull'aggiornamento dell'estensione di WebMatrix, vedere quelli specifici [note sulla versione](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Correzioni di bug
Oltre a queste funzionalità, questa versione di NuGet include altre correzioni di bug. Si sono verificati problemi totali 16 risolti nella versione. Per un elenco completo delle operazioni elementi risolti in NuGet 2.8.1, vista la [NuGet Issue Tracker per questa versione](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Aggregano con Visual Studio "14" CTP
Nella versione CTP di Visual Studio "14" rilasciata nel mese di giugno 2014 3rd NuGet 2.8.1 viene fornito nella casella. Le funzionalità supportano restano in par con altri 2.8.1 VSIXes come quello per Visual Studio 2013.
