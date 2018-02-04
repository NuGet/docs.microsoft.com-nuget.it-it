---
title: Note sulla versione di NuGet 2.8.1 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per l'inclusione di NuGet 2.8.1 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet 2.8.1 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 99dd050eb06024972132d5b0dcc9f97f965adc12
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-281-release-notes"></a>Note sulla versione di NuGet 2.8.1

[Note sulla versione di NuGet 2.8](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 note](../release-notes/nuget-2.8.2.md)

È stata rilasciata NuGet 2.8.1 2 aprile 2014.

## <a name="notable-features-in-the-release"></a>Importanti funzionalità nella versione

### <a name="support-for-windows-phone-81-projects"></a>Supporto per i progetti Windows Phone 8.1
Questa versione supporta ora i moniker seguente nuovo framework di destinazione che possono essere utilizzato per i progetti di destinazione Windows Phone 8.1:

* WindowsPhone81 / WP81 (per i progetti di Windows Phone basate su Silverlight)
* WindowsPhoneApp81 / WPA81 (per i progetti di App di Windows Phone basate su WinRT)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Aggiornamento dell'estensione di WebMatrix NuGet
Questa versione aggiorna il client NuGet trovato in WebMatrix per [sono](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 e la porta con comprende, ad esempio trasformazioni XDT. Ancora più importante, la 2.6.1 aggiornamento core consente al client di WebMatrix installare i pacchetti NuGet che contengono le versioni più recenti del `.nuspec` schema, che include i pacchetti NuGet di ASP.NET.

Per ulteriori informazioni sull'aggiornamento dell'estensione di WebMatrix, vedere parametri specifici [note sulla versione](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Correzioni di bug
Oltre a queste funzionalità, questa versione di NuGet include altre correzioni di bug. Si sono verificati problemi di totali 16 risolti nella versione. Per un elenco completo delle operazioni gli elementi corretti in NuGet, 2.8.1 visualizzazione di [NuGet Issue Tracker per questa versione](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Reshipping con Visual Studio "14" CTP
Nella versione CTP di Visual Studio "14" rilasciata a giugno 2014 3rd NuGet 2.8.1 viene fornito nella casella. Le funzionalità supportano restano in pari con altri 2.8.1 VSIXes ad esempio quello per Visual Studio 2013.
