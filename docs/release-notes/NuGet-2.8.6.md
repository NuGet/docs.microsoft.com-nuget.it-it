---
title: Note sulla versione di NuGet 2.8.6
description: Note sulla versione per l'inclusione di NuGet 2.8.6 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ee801a0edfe22888d65506cea557fd9c79dcf7bd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819718"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="2f64e-103">Note sulla versione di NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="2f64e-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="2f64e-104">[Note sulla versione di NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [note sulla versione di NuGet 2.8.7](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="2f64e-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="2f64e-105">È stato rilasciato NuGet 2.8.6 20 luglio 2015 come un aggiornamento secondario per il nostro 2.8.5 destinazione VSIX, con alcune correzioni e miglioramenti per supportare i pacchetti che possono essere inviati con il supporto per il modello di sviluppo UWP Windows 10.</span><span class="sxs-lookup"><span data-stu-id="2f64e-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="2f64e-106">Questa versione dell'estensione di gestione per il pacchetto NuGet fornisce il supporto solo per Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="2f64e-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="2f64e-107">In questa versione, la finestra di dialogo Gestione pacchetti NuGet ha aggiunto il supporto per:</span><span class="sxs-lookup"><span data-stu-id="2f64e-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="2f64e-108">È stato introdotto il moniker del Framework di destinazione UAP per supportare lo sviluppo di applicazioni di Windows 10.</span><span class="sxs-lookup"><span data-stu-id="2f64e-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="2f64e-109">Endpoint versione 3 del protocollo NuGet</span><span class="sxs-lookup"><span data-stu-id="2f64e-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="2f64e-110">Supporto per [NuGet](../consume-packages/configuring-nuget-behavior.md) attributo protocolVersion su origini dei repository.</span><span class="sxs-lookup"><span data-stu-id="2f64e-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="2f64e-111">Il valore predefinito è "2"</span><span class="sxs-lookup"><span data-stu-id="2f64e-111">Default value is "2"</span></span>
* <span data-ttu-id="2f64e-112">Eseguire il fallback al repository remoto se una versione del pacchetto richiesto non è disponibile nella cache locale</span><span class="sxs-lookup"><span data-stu-id="2f64e-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>