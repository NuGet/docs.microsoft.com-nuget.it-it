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
# <a name="nuget-286-release-notes"></a><span data-ttu-id="b5010-103">Note sulla versione di NuGet versione 2.8.6</span><span class="sxs-lookup"><span data-stu-id="b5010-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="b5010-104">[Note sulla versione di NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [note sulla versione di NuGet 2.8.7](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="b5010-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="b5010-105">NuGet versione 2.8.6 è stato rilasciato il 20 luglio 2015 come aggiornamento secondario al nostro 2.8.5 destinati VSIX con alcune correzioni e miglioramenti per supportare i pacchetti che possono essere distribuiti con il supporto per il modello di sviluppo di UWP di Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b5010-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="b5010-106">Questa versione dell'estensione Gestione pacchetti NuGet fornisce supporto solo per Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="b5010-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="b5010-107">In questa versione, la finestra di dialogo Gestione pacchetti NuGet ha aggiunto il supporto per:</span><span class="sxs-lookup"><span data-stu-id="b5010-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="b5010-108">È stato introdotto il moniker del Framework di destinazione UAP per supportare lo sviluppo di applicazioni di Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b5010-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="b5010-109">Endpoint versione 3 del protocollo NuGet</span><span class="sxs-lookup"><span data-stu-id="b5010-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="b5010-110">Supporto per [NuGet. config](../consume-packages/configuring-nuget-behavior.md) attributo delle protocolVersion sulle origini di repository.</span><span class="sxs-lookup"><span data-stu-id="b5010-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="b5010-111">Valore predefinito è "2"</span><span class="sxs-lookup"><span data-stu-id="b5010-111">Default value is "2"</span></span>
* <span data-ttu-id="b5010-112">Eseguire il fallback al repository remoto se una versione del pacchetto richiesto non è disponibile nella cache locale</span><span class="sxs-lookup"><span data-stu-id="b5010-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>