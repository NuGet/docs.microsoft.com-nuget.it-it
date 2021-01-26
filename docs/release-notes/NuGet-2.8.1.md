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
# <a name="nuget-281-release-notes"></a><span data-ttu-id="2fd7e-103">Note sulla versione di NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="2fd7e-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="2fd7e-104">Note sulla versione di [NuGet 2,8](../release-notes/nuget-2.8.md)  |  [Note sulla versione di NuGet 2.8.2](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="2fd7e-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="2fd7e-105">NuGet 2.8.1 è stato rilasciato il 2 aprile 2014.</span><span class="sxs-lookup"><span data-stu-id="2fd7e-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="2fd7e-106">Funzionalità rilevanti della versione</span><span class="sxs-lookup"><span data-stu-id="2fd7e-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="2fd7e-107">Supporto per progetti Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="2fd7e-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="2fd7e-108">Questa versione supporta ora i nuovi moniker del Framework di destinazione seguenti che possono essere usati per la destinazione Windows Phone progetti 8,1:</span><span class="sxs-lookup"><span data-stu-id="2fd7e-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="2fd7e-109">WindowsPhone81/WP81 (per i progetti Windows Phone basati su Silverlight)</span><span class="sxs-lookup"><span data-stu-id="2fd7e-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="2fd7e-110">WindowsPhoneApp81/WPA81 (per i progetti di app Windows Phone basati su WinRT)</span><span class="sxs-lookup"><span data-stu-id="2fd7e-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="2fd7e-111">Aggiornamento dell'estensione NuGet WebMatrix</span><span class="sxs-lookup"><span data-stu-id="2fd7e-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="2fd7e-112">Questa versione aggiorna il client NuGet trovato in WebMatrix a [NuGet. Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 e offre funzionalità IT come le trasformazioni di xdt.</span><span class="sxs-lookup"><span data-stu-id="2fd7e-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="2fd7e-113">Ancora più importante, l'aggiornamento di 2.6.1 core consente al client WebMatrix di installare pacchetti NuGet che contengono versioni più recenti dello `.nuspec` schema, che include i pacchetti NuGet di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2fd7e-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="2fd7e-114">Per ulteriori informazioni sull'aggiornamento dell'estensione WebMatrix, vedere le [Note sulla versione](../release-notes/nuget-2.6.1-for-WebMatrix.md)specifiche.</span><span class="sxs-lookup"><span data-stu-id="2fd7e-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="2fd7e-115">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="2fd7e-115">Bug Fixes</span></span>
<span data-ttu-id="2fd7e-116">Oltre a queste funzionalità, questa versione di NuGet include altre correzioni di bug.</span><span class="sxs-lookup"><span data-stu-id="2fd7e-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="2fd7e-117">Sono stati risolti 16 problemi totali nella versione.</span><span class="sxs-lookup"><span data-stu-id="2fd7e-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="2fd7e-118">Per un elenco completo degli elementi di lavoro corretti in NuGet 2.8.1, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="2fd7e-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="2fd7e-119">Reshipping con Visual Studio "14" CTP</span><span class="sxs-lookup"><span data-stu-id="2fd7e-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="2fd7e-120">In Visual Studio "14" CTP rilasciato il 3 giugno 2014, NuGet 2.8.1 viene fornito nella casella.</span><span class="sxs-lookup"><span data-stu-id="2fd7e-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="2fd7e-121">Le funzionalità supportate rimangono invariate con altri VSIX 2.8.1, ad esempio quello per Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="2fd7e-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
