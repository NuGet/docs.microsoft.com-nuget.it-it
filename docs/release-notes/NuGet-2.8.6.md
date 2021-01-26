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
# <a name="nuget-286-release-notes"></a><span data-ttu-id="6bb5d-103">Note sulla versione di NuGet versione 2.8.6</span><span class="sxs-lookup"><span data-stu-id="6bb5d-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="6bb5d-104">Note sulla versione di [NuGet 2.8.5](../release-notes/nuget-2.8.5.md)  |  [Note sulla versione di NuGet 2.8.7](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="6bb5d-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="6bb5d-105">NuGet versione 2.8.6 è stato rilasciato il 20 luglio 2015 come aggiornamento secondario di 2.8.5 VSIX con alcune correzioni e miglioramenti mirati per supportare i pacchetti che possono essere forniti con il supporto per il modello di sviluppo UWP di Windows 10.</span><span class="sxs-lookup"><span data-stu-id="6bb5d-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="6bb5d-106">Questa versione dell'estensione Gestione pacchetti NuGet fornisce il supporto solo per Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="6bb5d-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="6bb5d-107">In questa versione è stato aggiunto il supporto per la finestra di dialogo Gestione pacchetti NuGet per:</span><span class="sxs-lookup"><span data-stu-id="6bb5d-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="6bb5d-108">Introduzione del moniker del Framework di destinazione UAP per supportare lo sviluppo di applicazioni Windows 10.</span><span class="sxs-lookup"><span data-stu-id="6bb5d-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="6bb5d-109">Endpoint del protocollo NuGet versione 3</span><span class="sxs-lookup"><span data-stu-id="6bb5d-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="6bb5d-110">Supporto per [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) attributo protocolVersion nelle origini del repository.</span><span class="sxs-lookup"><span data-stu-id="6bb5d-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="6bb5d-111">Il valore predefinito è "2"</span><span class="sxs-lookup"><span data-stu-id="6bb5d-111">Default value is "2"</span></span>
* <span data-ttu-id="6bb5d-112">Fallback al repository remoto se nella cache locale non è disponibile una versione del pacchetto necessaria</span><span class="sxs-lookup"><span data-stu-id="6bb5d-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>